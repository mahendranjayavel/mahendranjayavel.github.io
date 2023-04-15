---
title: Integrate Tools Using WEBR Orchestration Scripts
keywords: webhooks
tags: [ctf_20.1, integration, webhooks, webr]
sidebar: teamforge_sidebar
permalink: webr-orchestration.html
last_updated: Sep 22, 2020
summary: WEBR Orchestration is a webhook integration capability that lets you integrate tools using orchestration scripts.   
---
<!-- Artifact artf397007 : webr - Orchestration - MVP - User Guide -->

The TeamForge Webhooks-based Event Broker (WEBR) provides a webooks-based orchestration framework (for TOPIC type events) that lets you build integrations using an orchestration script, which otherwise would take creation of multiple subscriptions for the tools being integrated. 

In addition, the WEBR orchestration framework lets you create orchestration endpoints that abstract the subscription URL, username, password (encrypted), header and so on. Once you create an endpoint you can use it in your orchestration scripts (with calls such as webGet, webPost, webPatch, webPut and webDelete). 

{% include important.html content="Orchestration scripts can only be used for TOPIC type events." %}

Let us understand WEBR's orchestration capabilities with a simple TeamForge—Jira integration. 

WEBR Orchestration Use Case
: When a Story is created in TeamForge, create a Story in JIRA and store the Jira Story ID in a TeamForge custom field.

1. Create a Post-submit webhook in TeamForge with the following information: 
   * Publisher: TeamForge
   * Subscriber: Jira
   * Event Name: TeamForge.Artifact.Create
   * Filter: $$->'Body'->'original'->'tracker'->>'title’='Stories'
   * WebhookEndpoint: `orch://ctf2jiraCreateStory` (this is the WEBR's internal orchestration endpoint where TeamForge messages are delivered)
   * Transform script: <None>

2. Create a function, `ConvertCtfStory2Jira`, and add it to the [webr_init.js][siteoptiontokens.html#WEBR_INIT_JSFILE] file. This is optional, but a recommended step, as isolating such common code in a common file enables reuse and also reduces the orchestration script size.

   The `ConvertCtfStory2Jira` function essentially takes the `TeamForge.Artifact.Create` event's payload (passed as `$inmessage` to the `ConvertCtfStory2Jira` function), maps the TeamForge field values with JIRA field values, and returns the result ($outmessage) to the orchestration script.

   Here's an example `TeamForge.Artifact.Create` event payload.

	```json	
	{
	 "comment": "",
	 "event_type": "create",
	 "id": "artf1114",
	 "timestamp": "2020-09-23T07:10:36+05:30",
	 "url": "https://cu079.cloud.maa.collab.net/sf/go/artf1114",
	 "author": {
	     "username": "admin"
	 },
	 "original": {
	     "project": {
	         "id": "proj1012",
	         "url": "https://cu079.cloud.maa.collab.net/sf/go/proj1012",
	         "title": "test2"
	     },
	     "tracker": {
	         "description": "Project2Tracker2",
	         "title": "Project2Tracker2",
	         "icon": "https://cu079.cloud.maa.collab.net/sf-images/tracker/icons/icon_01.png",
	         "id": "tracker1030",
	         "url": "https://cu079.cloud.maa.collab.net/sf/go/tracker1030"
	     },
	     "fields": {
	         "actualEffort": 0,
	         "assignedToUsername": "nobody",
	         "autosumming": false,
	         "category": "",
	         "customer": "",
	         "description": "test",
	         "estimatedEffort": 0,
	         "folderId": "tracker1030",
	         "artifactGroup": "",
	         "lastModifiedByUsername": "admin",
	         "lastModifiedDate": "2020-09-23T07:10:36+05:30",
	         "path": "projects.test2/tracker.project2tracker2/artf1114",
	         "planningFolderId": "",
	         "points": 0,
	         "priority": 4,
	         "remainingEffort": "0",
	         "effortSpent": "0",
	         "reportedInReleaseId": "",
	         "resolvedInReleaseId": "",
	         "status": "Open",
	         "statusClass": "Open",
	         "submittedByUsername": "admin",
	         "submittedDate": "2020-09-23T07:10:36+05:30",
	         "title": "test",
	         "version": 100,
	         "flexFields": {}
	     }
	 }
	}
	````

   Here's the code for the `ConvertCtfStory2Jira` function.
   ```js
   function ConvertCtfStory2Jira($inmessage) {
   priority = $inmessage.original.fields.priority;
   jirapriority = ['', 'Highest', 'High', 'Medium', 'Low', 'Lowest'];
       priority1 = 'Medium';
       if (priority >= 1 && priority <= 5) priority1 = jirapriority[priority];
       $outmessage = {
           fields: {
               project: {
                   key: "TEST"
               },
               summary: $inmessage.original.fields.title,
               description: $inmessage.original.fields.description,
               customfield_10007: $inmessage.id,
               issuetype: {
                   name: "Story"
               },
               priority: {
                   name: priority1
               }
           }
       };
       return $outmessage;
   }
   ````

3. Create two endpoints using the `Create Endpoint` API, one for Jira and the other for TeamForge. 

   Here are the endpoints created for both TeamForge and Jira. 

	```json
	{
	    "HTTPStatusCode": 200,
	    "HTTPStatusText": "OK",
	    "Success": true,
	    "ErrorText": "",
	    "ErrorMessages": null,
	    "Response": [
	        {
	            "EndpointID": 1,
	            "EndpointName": "JIRA",
	            "EndpointURL": "http://cu493.cloud.maa.collab.net:8080/rest/api/2",
	            "Username": "admin",
	            "Password": "H4sIAAAAAAAA/0pMyc3MAwAAAP//AQAA//92DQ6IBQAAAA==",
	            "HttpHeaders": "{}",
	            "CreatedDate": "2020-04-07 11:05:22.786375 +0530 IST",
	            "UpdatedDate": "0001-01-01 05:53:28 +0553 LMT"
	        },
	        {
	            "EndpointID": 2,
	            "EndpointName": "Teamforge",
	            "EndpointURL": "ctf://",
	            "Username": "admin",
	            "Password": "H4sIAAAAAAAA/0pMyc3MAwAAAP//AQAA//92DQ6IBQAAAA==",
	            "HttpHeaders": "{\"If-Match\": \"*\"}",
	            "CreatedDate": "2020-04-07 11:06:42.686029 +0530 IST",
	            "UpdatedDate": "0001-01-01 05:53:28 +0553 LMT"
	        }
	    ]
	}
	````
	The `EndpointURL` for TeamForge, if given as `ctf://`, would be replaced by the TeamForge hostname as defined in the WEBR config file.


4. Create an orchestration (orchestration name: `ctf2jiraCreateStory`) using the `Create Orch Script` API.

   Here's the orchestration script with the required `webPost` and `webPatch` calls to Jira and TeamForge respectively.

	```js
	$outmessage = ConvertCtfStory2Jira($inmessage);
	ret = webPost('JIRA', '/issue', $outmessage);
	TFMessage = {
	    "flexfields": [
	        {
	            "name": "JiraDefectID",
	            "values": [ret.Response.key],
	            "type": "String"
	        }
	    ]
	};
	ret = webPatch('Teamforge', 'ctfrest/tracker/v1/artifacts/' + $inmessage.id, TFMessage);
	````
Here's how the orchestration works:
: * With the above configuration, when you create a TeamForge story, the `TeamForge.Artifact.Create` event triggers the subscription as defined in Step 1 of the WEBR orchestration use case.
: * The endpoint for the subscription is given as `orch://ctf2jiraCreateStory`.
: * WEBR fetches the relevant orchestration script and executes it.
: * The orchestration script calls the `CovertCtfStory2Jira` function with the TeamForge payload ($inmessage), which in turn returns the result ($outmessage) back to the orchestration script.
: * This result ($outmessage) from the `CovertCtfStory2Jira` function is then fed to Jira via a webPost call with which Jira creates the story in its tracker and returns the Response object that includes the key (Jira story ID). (You also get the Status and Error).
: * With the Jira Response object at hand, we now construct a message (TFMessage) for TeamForge that has the Jira story ID stored as the value (ret.Response.key) of the TeamForge flex field.
: * This TeamForge message is then fed to TeamForge via a webPatch call, which updates the TeamForge story with the Jira story ID.

{% include links.html %}	