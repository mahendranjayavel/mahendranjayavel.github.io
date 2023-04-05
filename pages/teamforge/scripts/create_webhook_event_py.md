---
title: create_webhook_event.py
keywords: create, webhook event, subscriber, publisher
tags: [webhooks, upgrade, scripts, integration, site_admin_tasks, ctf_19.0]
sidebar: teamforge_sidebar
permalink: create_webhook_event_py.html
last_updated: Jul 11, 2019
summary: This script creates an event, a publisher (with the Webhook URL), and a subscriber in TeamForge Webhooks-based Event Broker for a specified application. 
---

## Usage
Use the following command to run this script.
```shell
[RUNTIME_DIR]/scripts/create_webhook_event.py --appName=[Jenkins|Jira|TestLink|Binary]
````
## Parameters

<table>
<tr>
	<th>Parameter</th>
	<th>Description</th>
</tr>
<tr>
	<td>--appName</td>
	<td>The application for which the event, the publisher (with the Webhooks URL), and the subscriber are created.<br><br>
		Accepted values: 
		<ul>
			<li>Jenkins</li>
			<li>JIRA</li>
			<li>TestLink</li>
			<li>Binary</li>
		</ul>
	</td>
</tr>
<tr>
	<td>-h | --help</td>
	<td> Help information for the script.</td>
</tr>
</table>


{% include links.html %}