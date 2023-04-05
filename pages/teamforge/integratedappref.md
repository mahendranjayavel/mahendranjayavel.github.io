---
title: Integrated Application References
keywords: teamforge, extend, api, integrated app references
tags: [extend_teamforge, path_based_permission, integration, SOAP, role_based_access_control, authentication, project_templates]
sidebar: teamforge_sidebar
folder: teamforge
permalink: integratedappref.html
last_updated: Apr 5, 2018
layouts: "pagefaqs"
summary: Here is some stuff you may need to know to work with integrated applications.
---

## IntegratedAppSupport {#integratedappsupport}

CollabNet provides servlet helper libraries that take care of authenticating integrated application requests with TeamForge. They also provide context information for each subsequent form processing within the application or links clicked within the application.

The heart of this is the `IntegratedAppSupport` class, which must be called during every request of an integrated application. This class takes the HttpServletRequest and HttpServletResponse for each request and determines whether the user is already authenticated. It also provides project- and user-related information that can be used throughout the request.

 {% include tip.html content="It is a good idea to store this as a ThreadLocal so that it can be used from anywhere in the application." %}

IntegratedAppSupport, on successful validation, provides several objects that can be used through the integrated application. .

### Parameters

The method is specified within parentheses at the end of each parameter.

#### SoapSessionId

This identifies a user. It can be used for making any TeamForge webservice calls over SOAP. TeamForge expects that every call be associated with a valid SoapSessionId. This method lets you fetch the SoapSessionId for the current session of the user. (getSoapSessionId())

#### WebSessionId

This is the jsessionid for the current user. This is the servlet-container-specific id that might be used for some integrated applications. (getWebSessionId())

#### CtfBaseUrl

Retrieves the base URL for Collabnet TeamForge (getCtfBaseUrl()).

#### ProjectPath

Retrieves the TeamForgeProject path for this project. This would typically be “projects.<projectname>” (getProjectPath())

#### CollabNetSoap handle

Retrieves the handle for CollabNet SOAP (Refer to ctf_xxx_sdk.zip for SOAP calls that can be made using TeamForge) (
getCollabNetSoap()). Documentation for the SOAP methods exposed are available in ctf_xxx_sdk.zip.


#### PluggableAppSoap handle

Retrieves the handle for pluggable application SOAP calls (getPluggableAppSoap()).Documentation for the SOAP methods exposed are available in ctf_xxx_sdk.zip.

#### RbacAppSoap
Retrieves the handle for RBAC SOAP Calls (getRbacAppSoap()).Documentation for the SOAP methods exposed are available in ctf_xxx_sdk.zip.

#### IntegratedAppId

Retrieves the linkid for this request. (getIntegratedAppId())

#### IntegratedAppPrefix

Retrieves the Prefix to use for go-urls, associations and linkifications (getIntegratedAppPrefix()).

#### IntegratedAppName

Retrieves the name of this integrated app (getIntegratedAppName()).

#### ProjectId

Retrieves the TeamForge project id (getProjectId()).

#### userSoapDO

Retrieves the SOAP data object information for the current user (getUserSoapDO()).

## SOAP Calls for Integrated Applications

When you integrate an application with TeamForge, you will need to make SOAP calls from the integrated application into TeamForge to respond to events on either side.

To integrate an application with TeamForge using the Integrated Application Framework, you have to implement the following methods for TeamForge to communicate with the integrated application.

The interface should be exposed via SOAP, and the endpoint for this interface should be defined by the `<endpoint>` tag in the XML Application configuration file.

 {% include tip.html content="There is no direct API for managing users/groups from TeamForge to an integrated application. However, if your integrated application has the notion of users and user groups, you can listen to “user events” or “group events” through an event handler in TeamForge and call this interface using that data. You can also make SOAP calls from the integrated application directly into TeamForge to get user information." %}

### SOAP Calls for Adding, Editing or Deleting an Integrated Application

You can use these SOAP calls to enable project administrators to add an integrated application to their projects, edit an integrated application, or delete it from their projects.

#### createProjectConfig

This method is called when an integrated application is added to a project from **Project Admin > Tools > Add Tool**.

#### editProjectConfig

This method is called when editing an integrated application in a project from **Project Admin > Tools**.

#### deleteProjectConfig

This method is called when deleting an integrated application in a project from **Project Admin > Tools**.

### SOAP Calls for SCM in Integrated Applications

You can use these SOAP calls to enable users to change data in an integrated application based on actions in a TeamForge source code repository.

#### scmPreCommit

This serves as the pre-Commit hook for an integrated application. TeamForge will call this method if require-scm-integration flag is set to true in the integrated app xml descriptor. This would mean that a commit made into TeamForge will only succeed if this method returns a “true” (String).

 {% include note.html content="All TeamForge ids and ids from other integrated applications are removed from this list even though it could be part of the original commit message. Also these ids are without the prefix. The integrated application can use these ids to find if they are valid for the particular commit and respond with a `true` or a `false` followed by an optional error message that can be displayed to the user who is making the commit." %}

#### scmPostCommit

This method is called after a commit is made and post processing needs to happen for that particular commit in the integrated application. A typical use case will be to store the commit information as part of some object within the integrated application. Please note that any errors thrown as part of this will not stop the commit from happening as the commit has been already made.

### SOAP Calls for Search in Integrated Applications

The **getSearchResults** method is called by TeamForge as part of doing a regular search. Use this method to include data from your integrated application in TeamForge search results.

### SOAP Calls for Project Templates in Integrated Applications

You can use these SOAP calls to enable an integrated application to be included in project templates created by TeamForge.

#### createTemplate

This method is called when a TeamForge template is created on a project that contains this integrated application.

#### getTemplateMetadata

This method is called when displaying the template content in “Project Tools/Included in Template” section at the time of template creation.

#### getTemplateContent

This method is called when viewing the content of an existing template.

#### validateParametersForTemplatizedProject

This method is called to validate the configuration parameters provided when creating a project from a template.

#### createTemplatizedProjectConfig

This method is called when a project is created from a template and this integrated application is part of the template. This is the equivalent of the “createProjectConfig” call except that it can be called when a project gets created from a template.


{% include links.html %}