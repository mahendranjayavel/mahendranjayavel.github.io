---
title: Scripts and Filters in the TeamForge Webhooks-based Event Broker
keywords: webhooks, event broker, scripts, filters
tags: [ctf_19.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: scripts_filters.html
last_updated: Jan 23, 2020  
summary: The TeamForge Webhooks-based Event Broker v4 engine provides powerful scripting using JavaScript and custom JSON filtering capabilities that provide customization capability to products through webhooks.
---

## Filters

Subscriptions for events can be universal (no filters), which means, the subscription endpoint will qualify for receipt of any messages pertaining to the event.

However, filters enable routing of messages based on both the HTTP header as well as the message content. The following operators are supported for JSON payloads.

<table>
  <tr>
    <th>Operator</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>-></td>
    <td>Access element as JSON object</td>
  </tr>
  <tr>
    <td>->></td>
    <td>Access element as text value</td>
  </tr>
  <tr>
    <td>->'id'</td>
    <td>Access element id within JSON object, returning a JSON object</td>
  </tr>
  <tr>
    <td>->>'id'</td>
    <td>Access element id within JSON object, returning a text value</td>
  </tr>
  <tr>
    <td>->1</td>
    <td>Access element number 2 within JSON array object, returing a JSON object. Note that array subscripts are `0` based.</td>
  </tr>
  <tr>
    <td>->>1</td>
    <td>Access element number 2 within JSON array object, returning a JSON object. Not that array subscripts are `0` based.</td>
  </tr>
  <tr>
    <td>()</td>
    <td>Used to group conditions</td>
  </tr>
  <tr>
    <td>AND, OR, NOT</td>
    <td>Used for building complex conditions</td>
  </tr>
  <tr>
    <td>?</td>
    <td>Check if an element is present</td>
  </tr>
</table>

To demonstrate the usage of these operators, let us consider the following simplified message from a TeamForge.Artifact.Update event.

```shell
{
"comment":"Hello",
"event_type":"update",
"id":"artf1084",
"timestamp":"2019-06-20T15:29:53+05:30",
"url":"https://10.2.0.92.localdomain/sf/go/artf1084",
"author":{
"username":"admin"
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

The TeamForge Webhooks-based Event Broker exposes a special variable `$$` that contains both the http headers and the payload in a Header and a Body property. The above payload is accessible through the `$$->Body` property.

For example, to filter the messages for project `proj1008`, we need to access the project id property within the message body. Hence the subscription filter for this will have the syntax:

```shell
$$->’Body’->’original’->’project’->>’id’ = ‘proj1008’
````

You can also check for multiple values like this.

```shell
$$->’Body’->’original’->’project’->>’id’ in (‘proj1008’, 'proj1010')
````

Within the filter string, a single arrow (`->`) is used to retrieve the JSON object, while a double-arrow (`->>`) is used to retrieve the value as text.

To subscribe to messages only when the `actualEffort` field has changed, the filter condition will be

```shell
$$->’Body’->’original’->’fields’->’actualEffort’ != $$->’Body’->’updated’->’fields’->’actualEffort’
````

Subscription filters also support complex conditions using paranthesis, AND, OR, and NOT. For example, to have a subscription only when actual effort has changed, but only for the project `proj1008`, one can code the following condition:

```shell
($$->’Body’->’original’->’project’->>’id’ = ‘proj1008) AND ($$->’Body’->’original’->’fields’->’actualEffort’ != $$->’Body’->’updated’->’fields’->’actualEffort’)
````

Array access is also possible. For example, to make sure that a subscription is fired only when the `Estimated Effort` flex field has changed, one can code the following condition:

```shell
$$->’Body’->’original’->’fields’->’flexFields’->’Estimated Effort’->>0 != $$->’Body’->’updated’->’fields’->’flexFields’->’Estimated Effort’->>0
````

## Scripts

The TeamForge Webhooks-based Event Broker provides an in-built ES5 compliant JavaScript engine for message transformations and synchronous responses, business rules execution, and orchestration.

The TeamForge Webhooks-based Event Broker supports scripts in two scenarios:

1. In subscriptions for TOPIC events, for message transformation and orchestration.
2. In subscriptions for SYNC events, when using the TeamForge Webhooks-based Event Broker's in-built JS VM (JavaScript Virtual Machine) to code the SYNC event handler.

The TeamForge Webhooks-based Event Broker's Script Environment provides the following features:

1. The input payload is available in an in-built JS variable called `$inmessage`.

2. The output is to be assigned to the variable `$outmessage`.

3. The special variable `$statuscode`can be set to return http status codes in the case of SYNC event handlers.

4. An in-built JS function, `ctf_get`, which works only for SYNC event handlers. This can be used to issue REST GET calls to TeamForge to retrieve additional information for processing.

Let's understand through a couple of examples.

#### Example 1

Assume that you have a Post-submit subscription, which is a TOPIC event subscription for the TeamForge.Artifact.Update event, whose payload is shown above. Also, assume that you want a custom message format delivered to the subscription endpoint, only for messages where the `actualEffort` field has changed. Let the required format have the following sample JSON structure:

```shell
{
ProjectID: ‘proj1008’,
TrackerID: ‘tracker1005’,
TrackerTitle: ‘Defects’,
ArtifactID: ‘artf1084’,
OldEffort: 7,
NewEffort: 10
}
````

Then, you can create a subscription with a subscription filter as specified in the previous section for filtering messages where effort has changed. In the Script section, the following script must be entered:

```shell
v = $inmessage;
$outmessage = {
ProjectID: v.original.project.id,
TrackerID: v.original.tracker.id,
TrackerTitle: v.original.tracker.title,
ArtifactID: v.id,
OldEffort: v.original.fields.flexFields['Estimated Effort'].values[0],
NewEffort: v.updated.fields.flexFields['Estimated Effort'].values[0]
};
````

Such a message transformation feature is provided for Post-Submit (TOPIC) messages in the TeamForge Webhooks-based Event Broker, as TOPIC subscriptions are typically used for integration between different applications and each application might have its own message format.

#### Example 2 

In the case of SYNC event subscriptions (Pre-Submit in TeamForge), a script can be provided as an alternative to having an external web endpoint. Here the TeamForge Webhooks-based Event Broker itself acts as the subscriber.

Assume that you need to implement a business rule to validate the flex field `Estimated Effort`. The rule is that, this field can be changed only when the artifact is in an `Analyzing` state. Such a rule can be implemented using the following script within the TeamForge Webhooks-based Event Broker. For this to work, the endpoint must be the special URL `webr://`.

```shell
v = $inmessage;
body = $inmessage;
origEstimatedEffort = body.original.fields.flexFields['Estimated Effort'].values[0];
newEstimatedEffort = body.updated.fields.flexFields['Estimated Effort'].values[0];
$outmessage = '';
if (origEstimatedEffort !== newEstimatedEffort && body.updated.fields.status != 'Analyzing') {
$outmessage ='Estimated Effort field is only allowed to change on artifacts in an analyzing state';
$statuscode = 400;
}
````

The `$statuscode` variable is returned as the HTTP response code, while the `$outmessage` will be the message payload. This feature enables TeamForge 19.3 and later to fail the transaction when the status code is not `200` and to display the error message from the script.

{% include note.html content="`$statuscode` by default has the value `200`. Hence for success cases, there is no need to set it explicitly." %}

### ctf_get Function

For SYNC messages, the TeamForge Webhooks-based Event Broker supports a `ctf_get` function that can be used within the internal script. This takes a TeamForge REST GET API as input and returns the response as a JSON object. For this to work, the SYNC message must have an Authorization header containing the TeamForge Auth token. This token is used to access TeamForge, to ensure security.

Example:

```shell
ctf_get(‘/foundation/v1/users/myself’);
````

Let us say, within the script, you want to check if the current user, as per the auth token, is a super-user. You can code it as follows:

```shell
var myself = ctf_get(‘/foundation/v1/users/myself’);
if (myself.superUser) {
// execute rules related to super user
} else {
// execute rules related to normal user
}
````

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TOPIC Event Type][topic-event-type]
* [SYNC Event Type][sync-event-type]
* [QUEUE Event Type][queue-event-type]


{% include links.html %}
