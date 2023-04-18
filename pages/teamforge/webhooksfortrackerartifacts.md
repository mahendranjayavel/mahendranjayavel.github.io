---
title: Set up Webhooks for Tracker Artifacts (Pre-submit and Post-submit Webhooks)
keywords: webhooks, tracker, artifacts
tags: [ctf_19.3, project_admin_tasks, webhooks, trackers, webr]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jan 29, 2020
permalink: webhooksfortrackerartifacts.html
summary: Create pre-submit webhooks to enforce business rules on tracker artifacts and post-submit webhooks to deliver (custom-formatted) event messages to other tools. These webhooks are triggered when certain tracker events occur such as artifact create, update, move, clone or delete. You must have Project Admin permissions to set up pre-submit and post-submit webhooks.
---

* Pre-submit and post-submit webhooks for tracker artifacts are built on top of the TeamForge Webhooks-based Event Broker (WEBR), which is a webhook-driven message broker delivered as a microservice along with TeamForge.
* The WEBR application is installed by default when you install or upgrade to TeamForge {{site.data.identifiers.teamforge}}. For more information, see TeamForge {{site.data.identifiers.teamforge}} install and upgrade instructions.
* Every pre-submit or post-submit webhook you create is essentially a subscription to a TeamForge tracker event, typically with a subscription filter.
* The subscription filter is the one that defines whether a subscription is qualified to receive a message or not. For more information, see [Subscription Filter][scripts_filters]. 
* Speaking of pre-submit and post-submit webhooks, there is a publisher of events, which is TeamForge—a message broker, which is WEBR—and subscribers of events, which are applications such as JIRA, TestLink, Nexus, Jenkins or a server-side Javascript rules application.
* A subscriber application can have one or more subscriptions to a TeamForge event.

  {% include important.html content="You cannot create more than one subscription with the same subscription filter." %}

For more information about WEBR, see [WEBR Documentation][webhooks-event-broker-overview].

{% include warning.html content="Though WEBR is an independent microservice by itself, it is not intended for use outside of TeamForge. It is bundled with TeamForge and is only intended for creating webhooks-based integrations with TeamForge." %} 

## Pre-submit Webhooks {#pre-submit-webhooks}

While message brokers are—by and large—built to deliver messages in an asynchronous manner, synchronous delivery and response also have specific uses in the form of externalizing the application behaviour. Pre-submit webhooks are for enforcing business rules on TeamForge tracker artifacts, typically using an external rules engine, when certain events occur—for example, artifact create or update events.

The WEBR application—upon receiving a post-submit (TOPIC type) or QUEUE type event messages—stores them in its database—and asynchronously delivers the message to all qualified subscriptions with a matching subscription filter. 

However, upon receiving a pre-submit event message—WEBR accepts the message, resolves all active subscriptions to single out one and only one subscription that has a qualified subscription filter, invokes it and synchronously returns the response to the publisher (in this case TeamForge), along with the http status code returned by the subscription endpoint.

For more information about how a pre-submit event is handled by WEBR, see [Pre-submit Event Handling][sync-event-type].

Here's a list of pre-submit events that a subscriber can subscribe to in TeamForge.
* Teamforge.Artifact.Create.Presubmit
* Teamforge.Artifact.Update.Presubmit
* Teamforge.Artifact.Move.Presubmit
* Teamforge.Artifact.Clone.Presubmit
* Teamforge.Artifact.Delete.Presubmit
* Teamforge.Artifact.AddDependency.Presubmit
* Teamforge.Artifact.RemoveDependency.Presubmit

The subscriber of the pre-submit tracker artifact events could be an external rules application—for example a server-side Javascript rules application—or an internal Javascript Virtual Machine (VM). In both these cases, the subscriber accepts the TeamForge event paylod from WEBR, applies the defined business rules and returns the response along with the http status code (returned by the subscription endpoint) to TeamForge.

Each tracker in TeamForge has its own set of fields and hence you can create tracker-specific business rules for individual trackers. For example, you may want to ensure that when a user updates a story (from the Stories tracker):
* the "Estimated Effort" can be changed if and only if the "Status" of the artifact is set to `Analyzing`.
* the artifact "Status" can be changed to one of the states ending with `...ing` if and only if the artifact is assigned to someone (in other words, the "Assigned To" cannot not be `None` when you change the "Status" to `Analyzing`, for example).

Such business rule validations are possible by setting up pre-submit webhooks for the Stories tracker with an appropriate subscription filter. Similarly, you can create more such pre-submit webhooks for other trackers such as Defects, Epics and so on and so forth. 

You can create a pre-submit webhook with the following parameters.
* The subscriber application's name.
* The pre-submit event to which the application subscribes to.
* The subscriber application's webhook endpoint URL.
  {% include note.html content="The webhook endpoint URL is not needed if you choose to use the internal Javascript VM. `webr://` is the default subscription endpoint URL when you use the internal JS VM. In other words, WEBR itself acts as the subscriber. However, a custom response script is required to enforce the business rules and return the response to TeamForge." %}
* The subscription filter.

### Pre-submit Webhooks Tutorial
Here's a tutorial that walks you through the process of creating a pre-submit webhook for the Stories tracker. 

#### Pre-submit Webhook Use Case
Let us create a pre-submit webhook that enforces the following two business rules whenever a user updates a story:
  * Allow the user to change the "Estimated Effort" field, if and only if the "Status" of the artifact is (set to) `Analyzing`.
  * Allow the user to change the artifact "Status" to one of the states ending with `...ing`, if and only if the artifact is assigned to someone (in other words, the "Assigned To" cannot not be `None` when a user changes the "Status" to `Analyzing`).

#### The External Rules Application
Suppose that the external server-side Javascript rules application runs on a separate server—for example, `http://rulesnodeapp.com` on port `4000`. For example, let us use the following `node.js` code to create the rules application that validates the two business rules discussed earlier.

  ```js
  const http = require('http')
  const port = 4000
​
  const requestHandler = (request, response) => {
      const { headers, method, url } = request;
    let body = [];
    request.on('error', (err) => {
      console.error(err);
    }).on('data', (chunk) => {
      body.push(chunk);
    }).on('end', () => {
        var messages = [];
        var statusCode = 200;
      body = JSON.parse(Buffer.concat(body).toString());
      origEstimatedEffort = body.original.fields.flexFields['Estimated Effort'].values[0];
      newEstimatedEffort = body.updated.fields.flexFields['Estimated Effort'].values[0];
      console.log ('Estimated effort=', origEstimatedEffort, newEstimatedEffort);
      if (origEstimatedEffort !== newEstimatedEffort && body.updated.fields.status != 'Analyzing') {
          messages.push ('Estimated Effort field is only allowed to change on artifacts in an analyzing state');
          statusCode = 400;
      }
      if (body.updated.fields.assignedToUsername === 'nobody' && body.updated.fields.status.endsWith('ing')) {
          messages.push ("Assignment to nobody is not allowed for '...ing' states");
          statusCode = 400;
      }
    
      response.writeHead(statusCode, {'Content-Type': 'application/json'});
  
    response.end(JSON.stringify(messages));
    })
  
  }
​
  const server = http.createServer(requestHandler)
​
  server.listen(port, (err) => {
    if (err) {
      return console.log('something bad happened', err)
    }
​
    console.log(`server is listening on ${port}`)
  })
  ````

This `node.js` application runs on the `http://rulesnodeapp.com` server, on port `4000`. The webhook endpoint URL for the external rules application is: `http://rulesnodeapp.com:4000`.


#### The Subscription Filter
As we are enforing these business rules on the Stories tracker, here's the subscription filter that lets you subscribe to the Stories tracker pre-submit event messages.

```shell
$$->'Body'->'original'->'tracker'->>'title'='Stories'
````

#### The Response Script
In case you use the internal JS VM instead of the external server-side Javascript application, here's the code for the custom response script that validates the two business rules discussed earlier and returns the response and status code to TeamForge.

  ```js
  body = $inmessage;
  var messages=[];
  var statusCode = 200;

  origEstimatedEffort = body.original.fields.estimatedEffort;
  newEstimatedEffort = body.updated.fields.estimatedEffort;
  if (origEstimatedEffort !== newEstimatedEffort && body.updated.fields.status != 'Analyzing') {
  message.push ('Estimated Effort field is only allowed to change on artifacts in an analyzing state');
  statusCode = 400;
  }
  if (body.updated.fields.assignedToUsername === 'nobody' && body.updated.fields.status === 'Analyzing') {
  message.push ("Assignment to nobody is not allowed for '...ing' states");
  statusCode = 400;
  }

  $outmessage=message;
  $statusCode=statusCode;

  ````

With these, let us now create the pre-submit webhook. 

1. Go to the project where you want to create a pre-submit webhook for the Stories tracker. 
2. Select **Project Home > Project Admin**. 
3. Select **Webhooks** from the **Project Admin Menu** on the left. 
4. Click **Create WebHook**.
   
   {% include image.html file="webhook-create.png" %}

   The **Create Webhook** page appears.

   {% include image.html file="webhooks-trackerartifacts.png" %}
5. Type a name and description for the webhook.
6. Click **Add New Subscriber** and type the name of the subscriber on the **Create New Subscriber** dialog box. This is just a logical name you use to refer to the subscriber application.
7. Once added, select the subscriber application from the **Subscriber** drop-down list.
8. Select **Pre-submit** from the **Event Type** drop-down list.

9. Depending on whether you are using an external rules application or the internal JS VM:
   
   * Copy and paste the external rules application's webhook URL (`http://rulesnodeapp.com:4000`) into the **Webhook URL** text box.

      **Or**

   * Select the **Use Internal JS VM** check box and copy and paste the response script code into the **Response Script** text box. 
10. Select one of the pre-submit events from the **Event Name** drop-down list. For this tutorial, select the `Teamforge.Artifact.Update.Presubmit` event. 
11. Copy and paste the subscription filter (`$$->'Body'->'original'->'tracker'->>'title'='Stories'`) for the Stories tracker into the **Subscription Filter** text box.
12. Click **Save**. 

You have now created the pre-submit webhook to enforce the two business rules discussed earlier on the Stories tracker. Try updating a story artifact and verify if the rules are applied. 


## Post-submit Webhooks {#post-submit-webhooks}

Post-submit webhooks are meant for integrating TeamForge with other heterogeneous applications. Speaking of TeamForge trackers, post-submit webhooks are meant for publishing TeamForge tracker event messages (for example, artifact create or update event messages) to one or more subscriber applications such as Jira, TestLink and so on and so forth. The subscriber of the TeamForge post-submit events could be any application that you want to integrate with TeamForge. 

As the name suggests, post-submit webhooks are asynchronous in nature. TeamForge publishes the event payload to WEBR. Upon receiving the event payload, WEBR delivers the message to all the active subscription endpoints that have a qualified subscription filter. Subscriptions with no subscription filter are, by default, qualified to receive all the post-submit event messages.

Here's a list of post-submit events that a subscriber can subscribe to in TeamForge.

* Teamforge.Artifact.Create
* Teamforge.Artifact.Update
* Teamforge.Artifact.Move
* Teamforge.Artifact.Clone
* Teamforge.Artifact.Delete
* Teamforge.Artifact.AddDependency
* Teamforge.Artifact.RemoveDependency

While TeamForge delivers its event messages in a pre-defined JSON format, these other applications may need the messages in a different format. WEBR supports such needs by extending its message transformation capabilities.

You can create a post-submit webhook with the following parameters: 

* The subscriber application's name.
* The post-submit event to which the application subscribes to.
* The subscriber application's webhook endpoint URL.
* The custom transform script (optional).
* The subscription filter (optional).

For more information about how a post-submit event is handled by WEBR, see [Post-submit Event Handling][topic-event-type].

### Post-Submit Webhooks Tutorial {#post-submit-webhooks-tutorial}
Here's a tutorial that walks you through the process of creating a post-submit webhook that delivers a custom-formatted message to another application.

#### Post-submit Webhooks Use Case
Let's create a post-submit webhook that listens to the `TeamForge.Artifact.Update` event, accepts the default TeamForge event payload, transforms it with a transform script and delivers the custom-formatted message to the subscriber application. 

#### The TeamForge.Artifact.Update Event Payload
Here's a sample JSON payload for the `TeamForge.Artifact.Update` event.
```json
{
"comment":"Hello",
"event_type":"update",
"id":"artf1084",
"timestamp":"2019-06-20T15:29:53+05:30",
"url":"https://10.2.0.92.localdomain/sf/go/artf1084",
"author":{
"username":"jmahendran"
},
"original":{
"project":{
"id":"proj1008",
"url":"https://10.2.0.92.localdomain/sf/go/proj1008",
"title":"CollabNet Agile Baseline 2.0"
},
"tracker":{
"title":"Defects",
"icon":"https://10.2.0.92.localdomain/sf-images/tracker/icons/icon_13.png",
"id":"tracker1005",
"url":"https://10.2.0.92.localdomain/sf/go/tracker1005"
},
"fields":{
"actualEffort":0,
"assignedToUsername":"nobody",
"flexFields":{
"Estimated Effort":{
"type":"String",
"values":["7"]
},
"Department Name":{
"type":"String",
"values":["Dev"]
},
"ART STATUS":{
"type":"String",
"values":["Open","In Progress"]
}
}
}
},
"updated":{
"project":{
"id":"proj1008",
"url":"https://10.2.0.92.localdomain/sf/go/proj1008",
"title":"CollabNet Agile Baseline 2.0"
},
"tracker":{
"title":"Defects",
"icon":"https://10.2.0.92.localdomain/sf-images/tracker/icons/icon_13.png",
"id":"tracker1005",
"url":"https://10.2.0.92.localdomain/sf/go/tracker1005"
},
"fields":{
"actualEffort":0,
"assignedToUsername":"nobody",
"flexFields":{
"Estimated Effort":{
"type":"String",
"values":["10"]
},
"Department Name":{
"type":"String",
"values":["Dev"]
},
"ART STATUS":{
"type":"String",
"values":["Open","In Progress"]
}
}
}
}
}
````

Suppose that you want the above JSON message—transformed to a custom format only when the "Estimated Effort" field has been changed—and delivered to the subscription endpoint. Let the desired custom format have the following JSON structure:

```js
{
ProjectID: ‘proj1008’,
TrackerID: ‘tracker1005’,
TrackerTitle: ‘Defects’,
ArtifactID: ‘artf1084’,
OldEffort: 7,
NewEffort: 10
}
````

#### The Subscription Filter
Here's the subscription filter for subscribing to post-submit artifact update events that have the "Estimated Effort" changed.
```js
$$->’Body’->’original’->’fields’->’Estimated Effort’ != $$->’Body’->’updated’->’fields’->’Estimated Effort’
`````

#### The Transform Script
Here's the transform script that transforms the standard `TeamForge.Artifact.Update` event's payload to the desired format. 
```js
v = $inmessage;
$outmessage = {
ProjectID: v.original.project.id,
TrackerID: v.original.tracker.id,
TrackerTitle: v.original.tracker.title,
ArtifactID: v.id,
OldEffort: v.original.fields.flexFields['Estimated Effort'].values[0],
NewEffort: v.updated.fields.flexFields['Estimated Effort'].values[0]
};
`````

With these, let us now create the post-submit webhook. 

1. Go to the project where you want to create a post-submit webhook. 
2. Select **Project Home > Project Admin**. 
3. Select **Webhooks** from the **Project Admin Menu** on the left. 
4. Click **Create WebHook**. The **Create Webhook** page appears.
5. Type a name and description for the webhook.
6. Click **Add New Subscriber** and type the name of the subscriber on the **Create New Subscriber** dialog box. This is just a logical name you use to refer to the subscriber application.
7. Once added, select the subscriber application from the **Subscriber** drop-down list.
8. Select **Post-submit** from the **Event Type** drop-down list.
9. Select one of the post-submit events from the **Event Name** drop-down list. For this tutorial, select the `Teamforge.Artifact.Update` event.
10. Type the Webhook URL of the subscriber application.
11. Copy and paste the subscription filter (`$$->’Body’->’original’->’fields’->’Estimated Effort’ != $$->’Body’->’updated’->’fields’->’Estimated Effort’`) into the **Subscription Filter** text box.
12. Copy and paste the transform script into the **Transform Script** text box. 
12. Click **Save**.

You have now created the post-submit webhook to transform and deliver a TeamForge artifact update event message. Try updating an artifact by changing the "Estimated Effort" field and verify if the subscriber application's endpoint receives a custom-formatted message as configured.

## Update a Webhook

 1. On the webhooks list page, click the webhook that you want to edit.

 2. Make the desired changes on the **Edit Webhook** page.

 3. Click **Save**.

## Delete a Webhook

 1. On the webhook list page, click the Delete icon of the webhook that you want to delete.

 2. A confirmation message shows up. `Are you sure you want to remove the webhook from project?`

 3. Click **OK** to delete.   

{{site.data.alerts.hr_shaded}}
#### Related Links

* [Set up Webhooks for Repositories][webhooksforrepositories]
* [Set up Webhooks for Projects][webhooksforprojects]
* [TOPIC Event Type][topic-event-type]
* [SYNC Event Type][sync-event-type]
* [Subscription Filters, Transform Scripts and Response Scripts][scripts_filters]

{% include links.html %}