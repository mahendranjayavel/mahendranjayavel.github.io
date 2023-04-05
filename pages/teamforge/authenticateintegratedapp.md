---
title: Authenticate your Integrated Application with TeamForge
keywords: teamforge, extend, api, integrated app authentication
tags: [extend_teamforge, path_based_permission, integration, SOAP, role_based_access_control, authentication]
sidebar: teamforge_sidebar
folder: teamforge
permalink: authenticateintegratedapp.html
last_updated: May 29, 2019
layouts: "pagefaqs"
summary: To help third party developers write integrated applications, CollabNet provides an SDK.
---

At the heart of the SDK is the IntegratedAppSupport helper class. You use IntegratedAppSupport to authenticate integrated application requests with TeamForge, and provide context information for subsequent processing of forms and links within the application.

You can download the SDK from [here](https://forge.collab.net/apidoc/).

You must call the [IntegratedAppSupport][integratedappref.html#integratedappsupport] class for every request made by the integrated application. This class takes HttpServletRequest and HttpServletResponse for each request and determines whether the user is already authenticated. It also provides project- and user-related information that can be used throughout the request.

 {% include tip.html content="It is a good idea to store this as a ThreadLocal so that it can be used from anywhere in the application." %}

Here's what you need to do to call IntegratedAppSupport from the application:

 * To create an object, pass in these three parameters:

   * TeamForge Base URL -- this is where TeamForge is installed

   * Integrated application URL -- this is where the application is installed

   * Application Name -- the name of the application as defined in the integrated application's descriptor

   Typically these parameters are stored as web.xml initialization parameters so that they are passed to IntegratedAppSupport's constructor.

 * When you have a validated IntegratedAppSupport object, store it in a ThreadLocal object so that it can be used in other places. For example, when constructing the blog URLs, we get IntegratedAppSupport from ThreadLocal and retrieve the IntegratedAppId from there. Once the object is created, another method called processRequest is called on it. This takes an HttpServletRequest and HttpServletResponse object that the servlet or a filter gets.

 * For each request that enters your system and needs to be validated, create an IntegratedAppRequest object.

   Subsequently, you also need to call the processRequest method to set the required parameters internally.

Where you construct the IntegratedAppSupport and call ProcessRequest subsequently depends on the architecture of your application. We've provided two cases -- for servlet filters and httpservlets.

 * If your application has servlet filters, use them as shown in the example of respective integrated application.

 * If your application does not use servlet filters, but directly calls an HttpServlet as the point of entry, place the call to IntegratedAppRequest where the application enters the HttpServlet code.

ProcessRequest does the following tasks:

 * If the URL is coming in for the first time from the TeamForge, it will have the singlesignon token. The method validates the token and stores a cookie which identifies the soap session for the user as well as the project for which this request is being made. This will also be the case for a Go URL coming in from TeamForge.

 * If it is a subsequent request (from a form submission or a click from a previous page), then the cookie information is picked up and used in IntegratedAppSupport. For this, the integrated application expects that the linkid (the id linking the integrated application and the project, obtained through IntegratedAppSupport.getIntegratedAppId()) is provided either as a request attribute or as a request parameter or in the request path -- it can be any one of these:

   ```shell
   http://my.integrated.application/reach/linkid/prplxxxx/me
   http://my.integrated.application/reach/me?linkId=prplxxxx
   ````

   a request parameter obtained through any other means and set as a Request Attribute.

It is advisable to set it so that all originating URLs (forms and other links to the application) have the `/linkid/prplxxxx` in their request URL. This helps subsequent URLs to be validated correctly. You can retrieve the linkid using IntegratedAppSupport.getIntegratedAppId.

{% include links.html %}