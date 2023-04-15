---
title: Reference Information About Custom Event Handlers
keywords: teamforge, extend, api
tags: [extend_teamforge]
sidebar: teamforge_sidebar
folder: teamforge
permalink: customeventhandlersreference.html
last_updated: Sep 12, 2018
summary: Here is some stuff you may need to know to work with event handlers.
---

## Create a New "event.xml" File for Your Custom Event Handler

Here is an example of an `event.xml` file. Use it to create a new event.xml file for your custom event handler in the META-INF directory of your jar file.

In this example, the CreateTestCaseWorkflow class will be invoked only on artifact creation and will run after the artifact creation is successfully committed. The EventTestListener will run for every single event and will run synchronously thereby having the opportunity to cancel the event.

```shell
<?xml version="1.0"?>
<!DOCTYPE event-handler
  PUBLIC "-//VA Software, Inc.//DTD Data Object 1.1//EN"
  "http://schema.vasoftware.com/sf/dtd/sf-event-handler_1_0.dtd">

<event-handler>
    <event api="6.1" mode="asynchronous">
       <type>artifact</type>
       <operation>create</operation>
       <user>admin</user>
  <handler>com.collabnet.ctf.events.CreateTestCaseWorkflow</handler>
    </event>

  <event api="6.1" mode="synchronous">
       <type>*</type>
       <operation>*</operation>
  <handler>com.collabnet.ctf.events.EventTestListener</handler>
    </event>
</event-handler>
````

## DTD for Custom Event Handler

An event handler works by subscribing to system events and then responding when event occurs. You subscribe to events by placing an XML file in the custom event handler JAR that describes what events are being monitored and who is doing the monitoring.

Here is the current DTD:

```shell

<!ELEMENT event-handler (description?, event+)>

<!-- Optional description for the Event Handler -->
<!ELEMENT description (#PCDATA)>

<!ELEMENT event (type, operation, user?, handler)>

<!-- This is the API level that the event handler expects the ObjectSoapDO objects to be marshaled for -->
<!ATTLIST event api (6.1|6.2) #REQUIRED>

<!--
    Whether the event handler should run synchronously (allows it to cancel the event) or asynchronously after the event
    has completed and is committed to the database.
-->
<!ATTLIST event mode (synchronous|asynchronous) #REQUIRED>

<!-- The object type being handled (e.g., artifact, task, document). '*' is all object types. -->
<!ELEMENT type (#PCDATA)>

<!-- This is the operation that is being listened for (e.g., create. delete. move, update). '*' is all operations. -->
<!ELEMENT operation (#PCDATA)>

<!--
    If the event handler needs to run as a different user (ie., a site admin account) the username should be
    passed in this attribute.  If the username is not valid the event handler will throw an abort exception.  That
    means that if the handler is processing synchronously the event will be canceled and the user will get an
    exception message.
-->
<!ELEMENT user (#PCDATA)>

<!--
   Name of a fully qualified class to handle the event.
-->
<!ELEMENT handler (#PCDATA)> 
````



{% include links.html %}