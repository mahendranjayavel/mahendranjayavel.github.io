---
title: TeamForge Webhooks-based Event Broker Overview
keywords: webhooks, event broker
tags: [ctf_20.1, ctf_20.0, ctf_19.3, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: webhooks-event-broker-overview.html
last_updated: Apr 28, 2020  
summary: TeamForge Webhooks-based Event Broker is a webhook driven integration broker, delivered as a free technical microservice along with TeamForge. It is a replacement for the event brokering aspects of the now deprecated EventQ product.
---

{% include important.html content="Usage of the TeamForge Webhooks-based Event Broker outside of TeamForge is not supported, as it is bundled with TeamForge and is only supported for TeamForge webhook integration." %}

## Features

The current release, called the **V4 Engine** is the new version of the TeamForge Webhooks-based Event Broker, delivered as part of TeamForge 19.3. It provides the following features:

{% capture webrfeatures %}

{% include inline_image.html file="status-success-small.png" %} Event registration <br>
{% include inline_image.html file="status-success-small.png" %} Subscriber and Subscription registration <br>
{% include inline_image.html file="status-success-small.png" %} Publisher registration <br>
{% include inline_image.html file="status-success-small.png" %} Topics, Queues, and Sync events <br>
{% include inline_image.html file="status-success-small.png" %} Guaranteed, once and once-only, in-order delivery <br>
{% include inline_image.html file="status-success-small.png" %} Message, Header, URL and Method transformation capabilities <br>
{% include inline_image.html file="status-success-small.png" %} Message callback support for asynchronous load-balanced long-running jobs <br>
{% include inline_image.html file="status-success-small.png" %} Sophisticated JSON subscription filters for both Header and content based filtering of messages<br>
{% include inline_image.html file="status-success-small.png" %} In-built ES5 compliant JavaScript engine for message transformations and synchronous responses, business rules execution, and orchestration

{% endcapture %}
{% include callout.html type="primary" content=webrfeatures %}


## Events

An event in WEBR is basically a message type. Examples of events include:

* Artifact create (`TeamForge.Artifact.Create`) or Artifact update (`TeamForge.Artifact.Update`) in TeamForge
* Build event in Jenkins
* Defect being filed in Jira (`JIRA.Bug.Create`), and so on

Where, `TeamForge.Artifact.Create` and `JIRA.Bug.Create` are the event names in WEBR. Every message published to WEBR should be tagged with an event name.

Events to be published through the TeamForge Webhooks-based Event Broker must be registered. Registering an event is required before you register the publisher or subscriber.

An event has the following key properties:

* a unique Event Name
* Content Type (Example: application/json)
* Event Type (TOPIC/QUEUE/SYNC)
* Event Format—This is a sample event that is used to understand the encoding and format of the message. JSON messages are validated. There is no message schema support.

### Event Types

This table provides the supported event types—TOPIC, SYNC, and QUEUE.

<table>
  <tr>
    <th>Event Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td width="400">TOPIC (Post-Submit)</td>
    <td>
      <ul>
        <li>These message types are typically to be used for post-submit scenarios.</li>
        <li>Each event can be subscribed to by multiple subscribers and subscriptions.</li>
        <li>The message is delivered to all the subscription endpoints.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>SYNC (Pre-Submit)</td>
    <td>
      <ul>
        <li>These are used for pre-submit scenarios, typically to externalize business rules.</li>
        <li>Subscriptions are restricted to only one. However, subscription filters can be used to maintain multiple subscription endpoints. In such cases, one single subscription endpoint is resolved at runtime.</li>
        <li>The publisher is guaranteed to get the response from the subscription endpoint synchronously.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>QUEUE</td>
    <td>
      <ul>
        <li>These message types are used for Web API driven load balancing.</li>
        <li>Subscriptions are grouped by filters.</li>
        <li>Only one subscription in a subscription group will be delivered the message.</li>
      </ul>
    </td>
  </tr>
</table>   

## Publishers

Publishers publish events. In the case of the TeamForge Webhooks-based Event Broker, a Publisher can be equated to an application. Example: TeamForge, Ossum, JIRA, Jenkins, Nexus.

Each registered publisher gets a unique ID. This ID is used while publishing messages to WEBR.

## Subscribers

Subscribers subscribe to and receive messages. Subscribers in the TeamForge Webhooks-based Event Broker equated to applications. Example: TeamForge, Ossum, JIRA, Jenkins, Nexus.

### Subscriptions

Each subscriber can have several subscriptions per event. Each subscription consists of the following critical properties:

* Subscriber
* Event Name
* <a href="#" data-toggle="tooltip" data-original-title="This is the endpoint URL to which the message is delivered.">Webhook Endpoint URL</a>—This can be an external URL or an internal endpoint such as `webr://` (which is used internally by the pre-submit webhooks to deliver the message to the internal ES5 compliant Javascript virtual machine for executing the business rules) or `orch://\<orchname\>` (to run an orchestration script).
* Header and content based subscription filter. For more information on subscription filter, see [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters].
* Headers to be passed to the URL, typically only external webhook endpoint URLs. 
* For TOPIC subscriptions, a "Transform script" can be provided if message transformation is required. For more information on transform script, see [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters].
* For SYNC subscriptions, if the response is embedded with the TeamForge Webhooks-based Event Broker using the "Internal JSVM" (internal JavaScript Virtual Machine), a response script can be provided. For more information on response script, see [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters].


## TeamForge Integrations Using the TeamForge Webhooks-based Event Broker

TeamForge can be integrated with Jenkins, JIRA, TestLink, and Nexus using the TeamForge Webhooks-based Event Broker.

For more information, see:

* [TeamForge-Jenkins Integration][teamforge-jenkins-integration]
* [TeamForge-JIRA Integration][teamforge-jira-integration]
* [TeamForge-TestLink Integration][teamforge-testlink-integration]
 


{{site.data.alerts.hr_shaded}}
#### Related Links

* [Install the TeamForge Webhooks-based Event Broker][install-webhooks-event-broker]
* [TeamForge Webhooks-based Event Broker Settings][webhooks-event-broker-settings]
* [TOPIC Event Type][topic-event-type]
* [SYNC Event Type][sync-event-type]
* [QUEUE Event Type][queue-event-type]
* [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]

{% include links.html %}
