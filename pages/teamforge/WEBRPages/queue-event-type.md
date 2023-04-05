---
title: QUEUE Event Type
keywords: webhooks, event broker, event type
tags: [ctf_19.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: queue-event-type.html
last_updated: Jan 23, 2020  
summary: Queue type events are provided within the TeamForge Webhooks-based Event Broker to support client server processing and http based load balancing. It provides a robust mechanism for invoking jobs asynchronously and receiving the response through callbacks. 
---

{% include warning.html content="Callbacks through CallbackURL is an experimental feature in TeamForge 19.3 and may not function correctly." %}

QUEUE type events are to be used purely for intra-application, asynchronous job management. Such events are typically expected to be named to have meaning only within applications (Example: Baseline.Create.Package.Request).

## How it works?

Each QUEUE type message is processed individually by the TeamForge Webhooks-based Event Broker. The Subscriber is ignored and the TeamForge Webhooks-based Event Broker purely acts based on subscriptions. Hence, there is no subscriber based sender here. To parallelize operations, the TeamForge Webhooks-based Event Broker uses five dedicated queue senders, each operating separately based on the result of the modulo operator on the message ID.

### Message Receipts

1. When the TeamForge Webhooks-based Event Broker receives a QUEUE event message, it first identifies all `ACTIVE` subscriptions that qualify to receive the messages.

2. Subscriptions that subscribe to the event, with no filters will qualify.

3. If a subscription has a `HeaderFilterString` property, then the subscription will qualify only if the message is sent along with a http header called `FILTER_STRING`, which should contain the same value as the `HeaderFilterString` property in the subscription. This is a pure string comparison and doesn't involve parsing the body.

4. If a subscription filter is present (a subscription filter can be added in addition to the `HeaderFilterString`), the filter is applied to the combined header and body of the message.  For more information, [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]. If the condition evaluates to `true`, then the subscription will qualify.

5. The input message along with all qualifying subscriptions are saved in a single transaction.

6. Multiple messages per subscription are stored.

7. This data is then used by the QUEUE Sender processes. For more information, see [Message Processing][queue-event-type.html#messageprocessing].

### Message Processing {#messageprocessing}

1. Given the way QUEUE messages are to be used, the TeamForge Webhooks-based Event Broker groups all subscriptions for each event by their subscription filter.

2. It essentially means, you can create subscriptions without any filter for a QUEUE event like Baseline.Create and the TeamForge Webhooks-based Event Broker will create one group for the event.

3. Or, you could have multiple subscriptions, one for Baseline.Package.Create with filter for projects with specific project codes and another set of subscriptions for projects with a different set of project codes. The TeamForge Webhooks-based Event Broker will then create two QUEUE subscription groups for that event.

4. The message is delivered to only one of the subscription endpoints within a subscription group. 

5. To make this happen, the TeamForge Webhooks-based Event Broker jumbles the endpoints and then tries to deliver to each endpoint.

6. If an endpoint processes it successfully, it is marked as `DELIVERED` and messages targeted at other subscription endpoints are marked as `REDUNDANT`.

7. If all endpoints are down, the message is kept pending and delivered again in the next cycle.

8. If a URL is provided in a **CallbackURL** http header, the TeamForge Webhooks-based Event Broker will form an internal URL and pass it in the **CallbackURL** http header while calling the subscription endpoint.

9. Once the subscription endpoint completes processing the message, it can then call the TeamForge Webhooks-based Event Broker provided callback URL to post the response.

10. This callback message is then stored and sent back to the original **CallbackURL** endpoint in a guaranteed manner. There is no necessity for the CallbackURL to point to the publisher. It can be a different URL altogether, forming a chain.

## Simulating QUEUE with TOPIC

It is possible to simulate the same use case using TOPIC messages instead of QUEUEs. However, this will need two events.

For example, instead of having a single **Baseline.Package.Create** event and specifying a **CallbackURL**, you can implement the same functionality by having the server subscribing to an event, such as **Baseline.Package.Create.Request** and then triggering another event, say **Baseline.Package.Create.Reply**.

However, callbacks allow for flexibility in specifying a callback URL on a per message basis, as the callback URL is part of the message header. It is hence possible to form a custom URL as a callback URL, with the message specific paths added to it.

Such facilities are lost when using TOPICs. Again, there might be more features added to QUEUEs later and hence for a robust load-balanced asynchronous job execution, it is recommended to use QUEUE event messages.

Again, it is impossible to load balance effectively between different endpoints, or to bring down one endpoint and restart another and to expect the message to be delivered effectively, as TOPIC type messages are always delivered to all qualifying endpoints.


{{site.data.alerts.hr_shaded}}
#### Related Links

* [TOPIC Event Type][topic-event-type]
* [QUEUE Event Type][queue-event-type]
* [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]

{% include links.html %}
