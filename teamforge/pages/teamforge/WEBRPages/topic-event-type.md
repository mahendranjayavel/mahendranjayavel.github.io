---
title: TOPIC Event Type
keywords: webhooks, event broker, event type
tags: [ctf_20.0, ctf_19.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: topic-event-type.html
last_updated: Mar 1, 2020  
summary: A TOPIC event type within the TeamForge Webhooks-based Event Broker is called as a Post-Submit event in TeamForge. The message of this event type is delivered to all the subscription endpoints.
---

Topics are the bread-and-butter of any integration broker and the TeamForge Webhooks-based Event Broker is no different. The TeamForge Webhooks-based Event Broker provides for a robust scalable architecture for handling thousands of topic messages and for delivering them to the subscription endpoints in a guaranteed, once and once-only, in-order manner.

## How it works?

A TOPIC event type within the TeamForge Webhooks-based Event Broker is called as a Post-Submit event in TeamForge. When a TOPIC event type message is published to the TeamForge Webhooks-based Event Broker, this message is sent to all subscription endpoints that qualify for the message, based on the subscription filter. 

A subscription that has no subscription filter will receive all messages pertaining to that event. Example: `TeamForge.Artifact.Create`.

1. When the TeamForge-based Event Broker receives a TOPIC event message, it first identifies all ACTIVE subscriptions that qualify to receive the messages.

2. Subscriptions that subscribe to the event, with no filters will qualify.

3. If a subscription has `HeaderFilterString` property, then the subscription will qualify only if the message is sent along with a http header called `FILTER_STRING`, which should contain the same value as the `HeaderFilerString` property in the subscription. This is a pure string comparison and does not involve parsing the body.

4. If a subscription filter is present (a subscription filter can be added in addition to the `HeaderFilterString`), the filter is applied to the combined header and body of the message. For more information, [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]. If the condition evaluates to true, then the subscription will qualify. 

5. The input message along with all qualifying subscriptions are saved in a single transaction.

6. Multiple messages per subscription are stored.

7. This data is then used by the TOPIC sender processes as detailed below.

As far as TOPIC subscriptions are concerned, the TeamForge Webhooks-based Event Broker guarantees once and once-only, in-order delivery at a subscriber level. To understand what it means, it is critical to understand how the TeamForge Webhooks-based Event Broker enables it, so that it can be used effectively.

1. In the TeamForge Webhooks-based Event Broker architecture, a subscriber equates to an application, which must receive its messages in the order in which it occurs.

2. The TeamForge Webhooks-based Event Broker starts a dedicated sender process for every subscriber.

3. The Sender process reads `PENDING` messages for that subscriber (using the `MaxQueuedToSend` configuration parameter) and sends the message to the Webhook endpoint specified in the subscription.

4. If the endpoint is down, the sender pauses and retries again. It will continue to retry until the endpoint is reachable or the subscription is made `INACTIVE`.
<!-- Artifact artf395884 : [webR] Expect unlimited retries for HTTP status code 503 - StatusServiceUnavailable -->
5. If the Webhook endpoint returns the status `5xx`, the current message is kept `PENDING` and the next message is sent. This PENDING message will again be sent in the next run. However, in case of `HTTP 503 - StatusServiceUnavailable` response, the WEBR's sender process keeps retrying to deliver the message to the webhook endpoint until it succeeds.

6. If the endpoint returns the status `4xx`, the current message is marked as `REJECTED` and the next message is processed. `REJECTED` messages are never sent again.

7. If the endpoint returns the status `3xx`, the current message is marked as `3xxNOTSUPPORTED` and the next message is processed. Such messages are never sent again.

8. Once all messages are sent, then the sender reads `PENDING` messages from the database and the whole process repeats.


## Points to Note

The above ensure that all messages are delivered in a guaranteed and in-order manner to subscription endpoints. However, given the Sender architecture, it is important for customers to design subscribers in terms of how messages are to be delivered. If message order is not important for an application, other than for the same event, it will make sense to create once subscriber per event.

To illustrate, if a subscriber (application ABC), needs all events from TeamForge in the same order they are triggered, then it makes sense to create one single subscriber called ABC and have multiple subscriptions.

However, if a subscriber is fine with receiving the `Artifact.Create` and `Artifact.Update` events in parallel, but want each of these event types in sequence, then it would be better to create two subscribers, say, `ABC.Create` and `ABC.Update` so that the messages are delivered in parallel. 

Please note that out-of-order cases such as the application receiving the update first before the create due to some issue with the network can be taken care of by ensuring the subscription endpoint returns `5xx` when it receives an `Artifact.Update` for an artifact that does not exist within ABC. The TeamForge Webhooks-based Event Broker will mark it as `PENDING` and re-deliver it in the next run.

Given the needs related to guaranteed in-order delivery, each Sender will repeatedly read the oldest messages, to the extent of `MaxQueuedToSend` each time. Hence it is important to mark as `INACTIVE` any subscription whose endpoint is not up and running. Else such subscriptions tend to block delivery of messages to the subscriber. Since the TeamForge Webhooks-based Event Broker expects the subscription maintainer to mark inactive subscriptions as `INACTIVE` in the TeamForge Webhooks-based Event Broker, it will never automatically mark subscription endpoints as `INACTIVE`.



{{site.data.alerts.hr_shaded}}
#### Related Links

* [SYNC Event Type][sync-event-type]
* [QUEUE Event Type][queue-event-type]
* [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]


{% include links.html %}
