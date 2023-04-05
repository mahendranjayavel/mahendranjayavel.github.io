---
title: Add a Custom Event Handler to Your TeamForge Site
keywords: teamforge, custom, event, handler, extend, api, system, tools, customization
tags: [extend_teamforge, customize, system_tools]
sidebar: teamforge_sidebar
folder: teamforge
permalink: addcustomeventhandler.html
last_updated: Apr 5, 2018
toc: no
summary: When you add an event handler to your TeamForge site, you can automatically react to system events in ways that help your site's project members or administrators.
---
An event handler is a program that watches for events on a TeamForge site and communicates them to another system. You can add your own event handlers to the set that are built into TeamForge.

For example, some of your site's members may be using TeamForge alongside a legacy issue tracking system. You may want to write an event handler that listens to the `Artifact Create` event on your TeamForge site and sends the details about any newly created artifact to the legacy system through a webservice.

1. Create your custom event handler and package it as a .jar file.
2. Check with your system administrator that the [ENABLE_UI_FOR_CUSTOM_EVENT_HANDLERS][siteoptiontokens.html#enableuiforcustomeventhandlers] token in the site configuration file is set to `true`.
3. Go to **My Workspace > Admin**.
4. Click **SYSTEM TOOLS** from the **Projects** menu.
5. Click **Customizations**.
6. Click **Create** and use the **Browse** control to locate your `.jar` file.
7. Click **Add**.
   {% include note.html content="If the system reports `Error Parsing Event Jar File`, debug your event handler until the error message no longer appears." %}

   Your `.jar` file is uploaded to your TeamForge site and the event cache is cleared. All the events you specified in your event handler are now captured and sent to the external web service.




{% include links.html %}