---
title: Add an AngularJS Customization to Your TeamForge Site
keywords: teamforge, custom, angularjs, customization
tags: [ctf_20.1, extend_teamforge, customize, site_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: addangularjscustomization.html
last_updated: May 5, 2020
toc: no
summary: When you add an AngularJS customization to your TeamForge site using .jar files.
---
TeamForge uses AngularJS to power some of its pages. AngularJS (a.k.a first version of Google's Angular framework).

By using AngularJS Customization you can customize angularjs pages in TeamForge UI. Do note that this also supports the usual CSS and image/logo customizations as well.

For example, you might want to 

* Change default TeamForge brand logo and replace it with your organization's logo
* You can add a button in a form and wire up a click event handler to it.

AngularJS Customization framework works similar to custom event handler mechanism. However, unlike custom event handlers, UI customization does not need the `event.xml` or any java code. Click [here][addcustomeventhandler] for more information about Custom Event Handlers.

In a nutshell:
1. Package all your UI/AngularJS code as a .jar file.
2. In the jar file, it is recommended that 
    - all CSS files are placed in <jar>/css folder
    - all bundle/images files are placed in <jar>/bundle/images folder
    - all JavScript and AngularJS files are placed in <jar>/js folder
3. Make sure that the [ENABLE_UI_FOR_CUSTOM_EVENT_HANDLERS][siteoptiontokens.html#enableuiforcustomeventhandlers] token is set to `true`.
4. Go to **My Workspace > Admin**.
5. Click **SYSTEM TOOLS** from the **Projects** menu.
6. Click **Customizations**.
7. Click **Create** and click **Browse** to locate your `.jar` file.
8. Click **Add**.
   {% include note.html content="Debug your event handler if you see the `Error Parsing Event Jar File` error." %}

   Up on successful upload of the .jar file, the event cache is cleared. All the events you specified in your event handler are now captured and sent to the external web service.

{% include links.html %}