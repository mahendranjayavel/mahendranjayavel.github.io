---
title: TeamForge WebConnect UIs
keywords: webhooks
tags: [ctf_20.3, integration, webhooks, webr]
sidebar: teamforge_sidebar
permalink: webconnectui.html
last_updated: Nov 4, 2020
summary: TeamForge 20.3 brings you intuitive UIs for TeamForge WebConnect (also known as TeamForge WEBR). You can now use the UIs to accomplish tasks such as creating events, endpoints, subscriptions, and so on—which otherwise could be done only via APIs.   
---

{% include important.html content="You must use the TeamForge WebConnect administrator credentials to log on to WebConnect." %}

* You can get the WebConnect administrator user's credentials from the `/opt/collabnet/teamforge/runtime/conf/webr/webr.config.json` file.
* The administrator password is auto-generated and encrypted when WebConnect is installed as part of the TeamForge installation.

## Log on to TeamForge WebConnect
1. Go to `<teamforge-domain>:<webconnect-port>/webr/`. For example, `https://cu079.cloud.maa.collab.net:3000/webr/`.
	{% include image.html file="203-webconnect-02.png" caption="TeamForge WebConnect Login page" %}
2. Type the WebConnect username and password. 
3. Click **Login**.

   {% include image.html file="203-webconnect-09.png" %}

## Enable Enhanced Logging

Click **Enhanced Logging** on the top navigation bar to turn enhanced logging on or off. 


## Create New Events

1. Click **Events** from the left pane. 
2. CLick **+ New**. 
3. Type a name and description for the event and select the event's type.
   {% include image.html file="203-webconnect-03.png" caption="The Add Event page" %}
4. Click **Save**.

Here’s a list of predefined post-submit and pre-submit events in TeamForge WebConnect.

* Teamforge.Artifact.Create
* Teamforge.Artifact.Update
* Teamforge.Artifact.Move
* Teamforge.Artifact.Clone
* Teamforge.Artifact.Delete
* Teamforge.Artifact.Create.Presubmit
* Teamforge.Artifact.Update.Presubmit
* Teamforge.Artifact.Move.Presubmit
* Teamforge.Artifact.Clone.Presubmit
* Teamforge.Artifact.Delete.Presubmit

## Create New Endpoints

1. Click **Endpoints** from the left pane. 
2. CLick **+ New**. 
3. Type a name, URL, username, passowrd and http headers for the endpoint.
   {% include image.html file="203-webconnect-04.png" caption="The Create Endpoint page" %}
4. Click **Save**.

## Create Common (Reusable) Scripts

Common scripts are scripts that are commonly reusable in orchestration, transformation and response scripts using the `$include$scriptname` syntax.

1. Click **</> Common Scripts** from the left pane. 
2. CLick **+ New**. 
3. Type a script name. 
4. Type (or copy/paste) the script.
   {% include image.html file="203-webconnect-05.png" caption="The Create Script page" %}
5. Click **Save**.

## Create New Orchestration Scripts

For more information about orchestration scripts, see [Integrate Tools Using WEBR Orchestration Scripts][webr-orchestration].

1. Click **Orchestrations** from the left pane. 
2. CLick **+ New**. 
3. Type an orchestration name. 
4. Type (or copy/paste) the orchestration script.
   {% include image.html file="203-webconnect-06.png" caption="The Create Orchestration page" %}
5. Click **Save**.

## Create New Subscribers

For more information, see [Subscribers and Subscriptions][webhooks-event-broker-overview].

1. Click **Subscribers** from the left pane. 
2. CLick **+ New**. 
3. Type a subscriber name, description, and http headers for the subscriber.
4. Select a status for the subscriber—**Active** or **Inactive**—from the drop-down list. 
   {% include image.html file="203-webconnect-07.png" caption="The Create Subscriber page" %}
5. Click **Save**.

## Create New Subscriptions

For more information, see [Subscribers and Subscriptions][webhooks-event-broker-overview].

1. Click **Subscriptions** from the left pane. 
2. CLick **+ New**. 
3. Type a subscription name and enter all the other required subscription information such as the event name, subscriber, webhook URL and so on.
   
   For more information, about subscription filter, tranform/response script, and header filter, see [Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]. 
   {% include image.html file="203-webconnect-08.png" caption="The Create Subscription page" %}
5. Click **Save**.

## Search Messages

Click **Message Search** from the left pane and you can search for messages using filters such as:
* Event Name
* Endpoint Name
* Message ID range (From MsgID and To MsgID)
* Date range

## View Server Logs

Click **Server Log** from the left pane to view the server logs. 

{% include links.html %}	