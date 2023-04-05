---
title: SYNC Event Type
keywords: webhooks, event broker, event type
tags: [ctf_19.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: sync-event-type.html
last_updated: Jan 23, 2020  
summary: A SYNC event type within the TeamForge Webhooks-based Event Broker is called as a Pre-Submit event in TeamForge. Only one subscription is allowed for this event type.
---

While asynchronous operations are typical uses of a message broker, synchronous responses also have specific uses in the form of externalizing application behaviour, such as executing business rules.

The TeamForge Webhooks-based Event Broker provides for SYNC events (Pre-submit). Unlike other event types where the TeamForge Webhooks-based Event Broker responds back once the message is stored within it, for SYNC messages, the TeamForge Webhooks-based Event Broker resolves subscriptions to one endpoint, invokes it, and passes back the response to the caller, along with the http status code returned by the subscription endpoint.

## How it works?

Fundamental to effective usage of SYNC events is to understand their primary purpose &mdash; externalizing application behavior through business rules. Therefore, when such an event, such as `Artifact.Create.Presubmit` is sent to the TeamForge Webhooks-based Event Broker, there must be only one subscription to invoke and return the response.

Hence, the TeamForge Webhooks-based Event Broker validates the subscriptions for an event as follows:

1. If there is no filter specified, there can only be one subscription per SYNC event.
2. If a subscription filter is provided, the TeamForge Webhooks-based Event Broker ensures that duplicate subscriptions with the same filter are not provided.
3. However, at the time when subscriptions are entered, it is not possible to check whether a later incoming message could resolve to more than one subscription. Hence, such a check is done during message intake. For more information, see [Message Receipts and Processing][sync-event-type.html#msgreceiptsandprocessing].

### Message Receipts and Processing {#msgreceiptsandprocessing}

1. When the TeamForge Webhooks-based Event Broker receives a SYNC event message, it first identifies all `ACTIVE` subscriptions that qualify to receive the messaes.

2. Subscriptions that subscribe to the event, with no filters will qualify.

3. If a subscription has a `HeaderFilterString` property, then the subscription will qualify only if the message is sent along with a http header called `FILTER_STRING`, which should contain the same value as the `HeaderFilterString` property in the subscription. This is a pure string comparison and doesn't involve parsing the body.

4. If the subscription filter is present (a subscription filter can be added in addition to the `HeaderFilterString`), the filter is applied to the combined header and body of the message. For more information on the subscription filter, see [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]. If the condition evaluates to `true`, then the subscription will qualify. 

5. The expectation is that either none or one subscription will quality. If more than one subscription qualifies for the message, the TeamForge Webhooks-based Event Broker will take only the first subscription and log an error listing the multiple subscriptions that are qualified for the message.

6. It will check if the subscription endpoint URL is `webr://`. This means the handler is implemented internally using the in-built JavaScript engine.

7. IF subscription is internal,

   1. A new JS VM (JavaScript Virtual Machine) is instantiated.

   2. Variables `$inheader`, `$inmessage`, `$outmessage`, and `$statuscode` are seeded into the VM.

   3. The incoming http headers are parsed into a native JSON object and assigned to `$inheader`.

   4. The incoming message payload is assigned to `$inmessage`.

   5. `$statuscode` is set to `200`.

   6. If the content type is `application/json`, the `$inmessage` is converted to a JSON object. Else, it is left as a string.

   7. The script is now executed within the context of the above variables.

   8. `$outmessage` is retrieved and forms the response payload. `$statuscode` is retrieved and set as the response http status code.

   9. Response is sent bact to caller.

8. ELSE

   1. The payload and headers are sent to the webhook endpoints.
   2. The response and return http statuses are passed back to the caller.

For the examples on how it can be used, see [Scripts and Filters in TeamForge Webhooks-based Event Broker][scripts_filters].

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TOPIC Event Type][topic-event-type]
* [QUEUE Event Type][queue-event-type]
* [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]


{% include links.html %}
