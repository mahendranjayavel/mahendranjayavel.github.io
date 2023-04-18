---
title: TeamForge SOAP API Reference
keywords: teamforge, extend, api
tags: [extend_teamforge, path_based_permission, SOAP, role_based_access_control, authentication]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforgesoapapiref.html
last_updated: Feb 11, 2020
layouts: "pagefaqs"
summary: TeamForge provides a SOAP service for each tool in the application.
---

## What can I do with the SOAP API?

You can use the TeamForge SOAP API to do almost anything a user can do in the TeamForge web user interface.

TeamForge exposes a subset of the APIs defined by the application server as web services, through the SOAP protocol.

A SOAP proxy server and a SOAP API layer, both running on Apache Axis, expose a set of web services representing each TeamForge application. The SOAP server serves the following functions:

 * Provides web services by accepting SOAP requests from the clients.
 * Performs SOAP client authentication.
 * Implements TeamForge role-based access control (RBAC) and caching service.
 * Accesses the application server via RMI stubs.

You can get the API here: http://www.collab.net/community/teamforge

The SOAP API can provide more types of functionality than the Web UI alone. For example, it can be time-consuming for a user with Tracker Admin permissions to copy a tracker workflow from one tracker to another in the Web UI. However, the SOAP method that provides a workflow copy function makes this task easy.

### Access permissions

For access permissions (authorization, as distinct from authentication), the SOAP API follows the same rules imposed by the TeamForge role-based access control (RBAC) system. A user using a SOAP API-based client has no more access to data than they have in the Web UI.

The Digital.ai TeamForge architecture allows you to quickly and easily develop integration points between Digital.ai TeamForge and applications you develop.

### User-centric services

All services and APIs are user‐centric, meaning that all integrated applications must establish an individual connection to the SOAP server for each user. This differs from programming directly with an application server where one connection can be established for any number of users.

Activities that can be performed using the SOAP interface are by definition user‐based, such as retrieving a list of a userʹs projects, tasks, or assigned tracker artifacts. These activities therefore require an individual connection for each user.

Requiring individual connections also ensures that role‐based access control is checked for each action performed by each user. To ensure that security is enforced, RBAC checks are performed on each SOAP API call and cannot be disabled at the client level.

### Consistent interaction

While each Digital.ai TeamForge service has its own SOAP interface, interaction with each service is designed to be as consistent as possible. The calls for each service are similar, although the data format and specific call parameters may be different.

For example, the following calls are consistent across all services:

* list
* get
* set
* delete
* create

The call parameters, however, are different. For example:

* When working with the CollabNet service, you might call `getProjectList(string sessionID)`.
* When working with the TaskApp service, you might call `getTaskList(string sessionID, string taskFolderID)`.

## Get started with the Digital.ai TeamForge SOAP API

A Digital.ai TeamForge plugin can provide any of the features a user can access through the Web interface.

 1. Browse the [CollabNet User Help](http://docs.collab.net/) to get a full picture of the functionality you can deliver with the SOAP API.

 2. Get an idea of the sorts of applications that have been developed.

    * Look at the available applications.

    * Review the reference applications on the [CollabNet community site](https://www.open.collab.net/community/cif_sfee/samples/). These samples illustrate some of the more common methods for using TeamForge via the SOAP API. They interact with most of the TeamForge data objects, including users, projects, trackers and artifacts, code commits and tasks.

    {% include note.html content="If you find a defect in a sample program or have a suggestion for improvement, please post a message in the [developer discussion forum](https://forums.open.collab.net/ds/viewForumSummary.do?dsForumId=738)." %}

 3. Set up the tools you will need:

    * A Java JDK, 1.8.0_131 or later, from http://www.oracle.com/technetwork/java/index.html.

    * Apache Ant, version 1.7.0 or later, from http://ant.apache.org.

 4. Choose a place to host your plugin project online. We recommend http://www.collab.net/community, because you get access to all the collaboration support tools that Digital.ai TeamForge provides.

 5. Get the SDK from http://www.collab.net/community/teamforge. The SDK includes everything needed to develop and deploy your application:

    * Source files and compiled output.

    * Full JavaDoc reference material. Inside the package, look for docs/com/collabnet/ce/soap60/webservices.

    * Annotated code examples.


 5. Get help from other Digital.ai TeamForge users and CollabNet staff in the TeamForge [API discussion forum](https://forums.open.collab.net/ds/viewForumSummary.do?dsForumId=738).

## Send Commit Data to TeamForge via SOAP

Use the Commit Tool provided with TeamForge to transmit your commit data to TeamForge.

The SCM Adapter allows you to develop integrations with almost any SCM tool, then exchange commit data with TeamForge. After you have created an SCM integration using the TeamForge API, you will use the Commit Tool provided with TeamForge to transmit your commit data to TeamForge.

For any SCM tool that supports triggers, you can use the tool’s triggering mechanism to script the following actions. Otherwise, you can perform them manually for each commit.

 {% include note.html content="The SCM Adapter option is always available, but will work only if you have developed an integration with an SCM tool using the TeamForge API." %}

 1. Get the Commit Tool from `$SOURCEFORGE_HOME/integration/CommitTool.py`.

 2. Add the SCM server to your TeamForge installation. For the end user instructions, see [Integrate a Source Code Server][integrateasourcecodeserver].

 3. Create a repository on the SCM server. For the end user instructions, see [Create a Source Code Repository][createasourcecoderepository].

 4. Use the Commit Tool to start a commit.

    ```shell
    CommitTool.py create <systemId> <path> <username> <host> <port>
    ````

    where:

    * `systemId` is the external system identifier that was given to the integration server. You can find this on the **Repository Details** page.

    * `path` is the path on the external system that was given to the repository. See the **Repository Details** page.

    * `username` is the TeamForge user name that will be performing the commit.

    * `host` is the TeamForge application server machine hostname.

    * `port` is the TeamForge application server machine SOAP port.

 5. After the commit has been created, use the Commit Tool to add files with versions and actions.

    ```shell
    CommitTool.py add <filename <version [<status [<fromfile <fromversion]]
    ````

    where:

    * `filename` is the name of the file that is being placed into the commit.

    * `version` is the version of the file that is being placed into the commit.

    * `status` is the status of the file in the repository. Valid status values are ʹaddedʹ, ʹdeletedʹ, ʹmodifiedʹ, ʹmovedʹ, and ʹcopiedʹ. Status is optional and will default to ʹaddedʹ if no value is provided.

    * `fromfile` is the name of the original filename if this file was copied or moved. It is required on a copy or move, but is not allowed on an add, delete, or modify.

    * `fromversion` is the version of the original filename is this file was copied or moved. It is required on a copy or move, but is not allowed on an add, delete, or modify.


 6. When all actions and files have been added to the commit, use the Commit Tool to transmit the commit to Digital.ai TeamForge.

    ```shell
    CommitTool.py commit <commitmessage>
    ````

    where `<commitmessage>` is a description about the commit that will be displayed along with the files, versions, and operations.

    {% include note.html content="To create an association, use the standard associate command [<item id>]. No special syntax is required when using the Commit Tool." %}

    For all of the above commands, when run correctly, there will be no output, and the return value of the program will be “0”, indicating success. Failure will show a message and return with a non “0” return value.

    To see the status of the current commit, you can use the Commit Tool to print the output of the current commit: 

    ```shell
    CommitTool.py print
    ````

    It will show output similar to this:

    ```shell
    Repository: <username>@<systemid>:<path> Modified filename 1.2 Added document 1.1 Copied newfile 1.1 (From: origfile 1.3) <status> <filename> <version> (From: <fromfile> <fromversion>)
    ````

## Update an application to TeamForge {{site.data.identifiers.teamforge}} API

To use any of the new API calls introduced in TeamForge  {{site.data.identifiers.teamforge}}, you must update your existing applications to use the {{site.data.identifiers.teamforge}} API.

See TeamForge {{site.data.identifiers.teamforge}} [Javadoc](http://docs.collab.net/teamforge221/javadoc/index.html) for more information. 

 * For calls that use the TeamForge-provided Java SDK classes, update all references to the package containing the classes.

   The package is located at `com.collabnet.ce.soap60`.

 * For calls that access the WSDL directly, point your application to the new WSDL location.

   The WSDL is located at `http://<teamforge‐server>/ce‐soap60/services/<service‐name>?wsdl`.

 * Update any calls that have been changed in the {{site.data.identifiers.teamforge}} API.

## TeamForge Services Available via SOAP

TeamForge provides a SOAP service for each tool in the application.

 {% include note.html content="The WSDL for each TeamForge service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/<myService>?wsdl`. For an example, to review the WSDL for the Tracker service, see http://ctf.open.collab.net/ce-soap60/services/TrackerApp?wsdl. For information on the SOAP API, including the pluggable component package and classes, see the SOAP package summary." %}

### The CollabNet Service

The CollabNet service is the primary service that handles logging into and out of Digital.ai TeamForge , finding and creating users, and retrieving lists of projects, project members, and project data.

The CollabNet service must always be accessed first, to authenticate the user and return a sessionId. The sessionId is a necessary parameter that must be passed to the methods in the other services.

The CollabNet service also handles retrieving and managing lists of users and projects, which are often the first steps that an application must perform.

Some examples of activities that are managed by the CollabNet service are:

 * Returning a list of all Digital.ai TeamForge users or projects.
 * Creating a new user.
 * Providing a user with a list of all projects of which he or she is a member.
 * Creating an association between two items.
 * Managing user groups and their membership.

User groups, added in Digital.ai TeamForge Enterprise Edition 4.4 Service Pack 1, simplify permission management for projects. User groups are site‐wide sets of users, managed by site administrators. Project administrators can add user groups to roles, just like they can add individual project members.

After authenticating the user through the CollabNet service, you can then access all of the other services that manage the items and activities associated with the other Digital.ai TeamForge applications, such as trackers, tasks, documents, or file releases. A new “Anonymous Login” capability introduced in Digital.ai TeamForge Enterprise Edition 4.4 adds the ability to log in with the privileges and access rights of a non‐authenticated user.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/CollabNet?wsdl`. For example, here's the copy on the CollabNet web site: http://ctf.open.collab.net/ce-soap60/services/CollabNet?wsdl.

### The Discussion Service

The DiscussionApp service handles the activities and items associated with forums.

Some examples of activities that are managed by the DiscussionApp service are:

 * Creating a forum, forum topic, or forum post.
 * Returning a list of all posts in a forum.
 * Returning a list of forum posts created by a specified user.
 * Returning a list of forum posts matching a search string.
 * Deleting a forum, forum topic, or forum post.

After authenticating the user through the CollabNet service, you can then access the DiscussionApp service to work with forums, forum topics, and forum posts.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/DiscussionApp?wsdl`. For example, here's the copy on the CollabNet web site: http://ctf.open.collab.net/ce-soap60/services/DiscussionApp?wsdl.

### The Document Service

The DocumentApp service handles the activities and items associated with documents and document folders.

Some examples of activities that are managed by the DocumentApp service are:

 * Creating a document or document folder.
 * Editing a document’s details.
 * Returning the name of the user who last edited or locked a document.
 * Returning a list of documents matching a search string.
 * Returning a list of all document folders in a project.
 * Returning a list of all open document reviews in a project.
 * Moving a document or document folder.

After authenticating the user through the CollabNet service, you can access the DocumentApp service to work with documents and document folders.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/DocumentApp?wsdl`. For example, here's the copy on the CollabNet web site: http://ctf.open.collab.net/ce-soap60/services/DocumentApp?wsdl.

### The File Release Service

The FrsApp service handles the activities and items associated with file releases.

Some examples of activities that are managed by the FrsApp service are:

 * Creating a package, release, or file.
 * Editing a package, release, or file.
 * Returning a list of all packages in a project.
 * Returning a list of all releases in a package.
 * Returning the status, maturity value, or other attribute of a release.

After authenticating the user through the CollabNet service, you can access the FrsApp service to work with file releases.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/FrsApp?wsdl`. For example, here's the copy on the CollabNet web site: http://ctf.open.collab.net/ce-soap60/services/FrsApp?wsdl.

### The File Storage service

The FileStorageApp and SimpleFileStorageApp services handle uploading of files and simple data bytes.

Some examples of activities that are managed by the FileStorageApp and SimpleFileStorageApp services are:

 * Uploading a file to Digital.ai TeamForge.
 * Downloading a file from Digital.ai TeamForge.
 * Checking the size of a file.

After authenticating the user through the CollabNet service, you can then access the FileStorageApp and SimpleFileStorageApp services to work with file uploads.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/FileStorageApp?wsdl`. For example, here's the copy on the CollabNet web site: http://ctf.open.collab.net/ce-soap60/services/FileStorageApp?wsdl.

### The Integration Data Service

The IntegrationDataApp service enables applications to associate their own data or metadata with Digital.ai TeamForge objects.

An application can register its own namespace, to prevent collisions with other applications, and then store key‐value pairs of data that are associated with any Digital.ai TeamForge object.

 * Developers who are creating integrations between Digital.ai TeamForge and external applications can use this service to maintain associations between Digital.ai TeamForge objects and counterparts in other systems.
 * Developers creating customizations or enhancements can use this service to store additional data not directly supported by other Digital.ai TeamForge APIs. For example, you can create extra, hidden fields on any object (such as an artifact, a user or a project) and use a Velocity customization to display that data where you need it.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/IntegrationDataApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/IntegrationDataApp?wsdl.

### The News Service

The NewsApp service handles the activities and items associated with news posts.

News posts for a project are visible on the projectʹs home page, and the applicationʹs main page lists news posts for all projects visible to the current user.

Starting with Digital.ai TeamForge , project news is presented on the projectʹs home page via a "Project News" page component, which can optionally be deleted or added to other pages. Each instance of the Project News component is a view of the same set of project news posts.

Some examples of activities that are managed by the NewsApp service are:

 * Returning a list of all news posts in a project.
 * Returning a list of all news posts matching a search string.
 * Returning a list of all news posts in all projects of which a specified user is a member.
 * Creating a news post.
 * Deleting a news post.

After authenticating the user through the CollabNet service, you can access the NewsApp service to work with news posts.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/NewsApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/NewsApp?wsdl.

### The Planning Folder Service

The Planning Folder service enables you to create and maintain planning folders from external applications.

Planning folders are visible in the tracker tool of each project, as an organizing level sitting on top of trackers. Planning folders are deisgned to support agile management practices.

Some examples of activities managed by the PlanningApp service are:

 * Creating and deleting planning folders.
 * Reordering planning folders.
 * Setting the statuses of planning folders.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/PlanningApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/PlanningApp?wsdl.

### The Project Pages Service

The PageApp service handles the activities and items associated with project pages.

The project pages feature enables project owners to customize their project home by creating their own custom pages. Multiple pages can be added, and these pages can be assembled into a hierarchy, browseable via a "tree" navigation on the left side of the projectʹs home. The content of each page can be customized by adding components of various types, such as Text, News, and Document Folder.

Some examples of activities that are managed by the PageApp service are:

 * Creating pages and components.
 * Managing the page hierarchy.
 * Managing the order of components on a page.
 * Updating text components with new HTML content.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/PageApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/PageApp?wsdl.

### The Project Categorization Service

The CategorizationApp service handles the activities and items associated with creation and management of Project Categorization.

Some examples of activities that are managed by the CategorizationApp service are:

 * Creating categories
 * Adding categories to projects
 * Retrieving category and project data.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/CategorizationApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/CategorizationApp?wsdl.

### The Role-based Access Control Service

The RbacApp service handles the activities and items associated with role creation and management.

Some examples of activities that are managed by the RbacApp service are:

 * Creating a role.
 * Adding a user to a role.
 * Adding permissions to a role.
 * Adding a user group to a role.

Permissions are managed in terms of “clusters.” Permission clusters correspond to the sets of permissions that are managed in the role administration section of the application’s user interface, such as “view” or “create/edit/view.” Clusters can be associated with top‐level folders in the application (e.g. with trackers in the Tracker application, or packages in the File Releases application). The RbacApp service allows this same permission management to be performed via SOAP.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/RbacApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/RbacApp?wsdl.

### The Software Configuration Management (SCM) Service

The ScmApp service handles the activities and items associated with integrated software configuration management (SCM) applications.

Some examples of activities that are managed by the ScmApp service are:

 * Returning a list of files associated with a code commit.
 * Returning a list of all repositories in a project.
 * Returning a list of all code commits in a repository.
 * Editing commit information.

After authenticating the user through the CollabNet service, you can access the ScmApp service to work with integrated SCM applications.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com/>/ce-soap60/services/ScmApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/ScmApp?wsdl.

#### SCM Adapter

The SCM Adapter allows you to develop integrations with almost any SCM tool, then exchange commit data with Digital.ai TeamForge. An SCM Adapter option is added to the Type menu on the Digital.ai TeamForge Create Integration page. Use this option to add your SCM integration server to Digital.ai TeamForge.

 {% include note.html content="The SCM Adapter option is always available, but will work only if you have developed an integration with an SCM tool using the Digital.ai TeamForge API." %}

After you have created an SCM integration using the Digital.ai TeamForge API, you will use the Commit Tool provided with Digital.ai TeamForge to transmit your commit data to Digital.ai TeamForge.

### The Tag Service

The TagApp service provides SOAP services for tag objects.

Some examples of activities that are managed by the TagApp service are:

 * Create a tag in a specific project.
 * Deleting a tag from a project.
 * Get tag data for a given tag ID.
 * Gets the list of tags in a project.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/TagApp?wsdl`. For example, here's the copy on the CollabNet web site: https://www.open.collab.net/community/cif_sfee/samples/TagApp.xml.

### The Tasks Service

The TaskApp service handles the activities and items associated with tasks and task folders.

Some examples of activities that are managed by the Task App service are:

 * Returning a list of all tasks assigned to a specified user.
 * Returning a list of all task folders in a project.
 * Returning a list of all tasks matching a search string.
 * Listing task dependencies.
 * Creating a task or task folder.
 * Editing a task.
 * Moving tasks and task folders.

After authenticating the user through the CollabNet service, you can access the TaskApp service to work with tasks and task folders.

 {% include note.html content="Task folders are referred to as task groups in the method descriptions." %}

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/TaskApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/TaskApp?wsdl.


### The Tracker Service

The TrackerApp service handles the activities and items associated with trackers and tracker artifacts.

Some examples of activities that are managed by the TrackerApp service are:

 * Returning a list of all trackers in a project.
 * Returning a list of all tracker artifacts matching a search string.
 * Returning a list of all tracker artifacts assigned to a specified user.
 * Creating a tracker artifact.
 * Editing a tracker artifact.
 * Moving a tracker artifact.

After authenticating the user through the CollabNet service, you can access the TrackerApp service to work with trackers and tracker artifacts.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/TrackerApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/TrackerApp?wsdl.

### The Wiki Service

The WikiApp service handles activities associated with project wiki pages.

Some examples of activities that are managed by the WikiApp service are:

 * Creating a Wiki page.
 * Adding Wiki content.
 * Retrieving Wiki content in HTML format.

For a complete description of each method, including its parameter definitions and SOAP faults and for a list of new and changed methods, see the JavaDoc for this service.

The WSDL for this service is available on your TeamForge site at `https://<mysite.com>/ce-soap60/services/WikiApp?wsdl`. For example, here's the copy on the CollabNet web site: https://ctf.open.collab.net/ce-soap60/services/WikiApp?wsdl.

## Context-specific Objects for Manipulating Velocity Pages

The rendering context is a set of objects made available to the Velocity template. You can access the members of these objects in a template using the standard Velocity syntax.

### ArrayTool

This is necessary because Velocity does not provide accessors into arrays and some of the API calls will return SoapNamedValues objects that have two matching arrays of name and value.

#### length(Object[] array)

The array will be examined and will get the length of the array.

The function returns the length of the array (null array will return 0).

#### get(Object[] array, int index)

Get the object at the specified index of the array that contains the object of interest. The index is from which we pull the object from.

This function returns the object stored at that array of null if the array is empty or position is invalid.

### FORM [FormTool]

Manages opening and closing of forms.

* **startForm(String action, String formId)**

  Get the opening tag for a form.

  1. **action** - The path to the action that is handling the form (e.g. `/cemain/do/ login`).
  2. **formId** - The id/name of the form (they will be the same).

  This function returns the open tag for the form and any standard hidden elements.

* **startForm(String action, String formId, String formName)**

  Get the opening tag for a form.

  1. **action** - The path to the action that is handling the form (e.g. `/cemain/do/ login`).
  2. **formId** - The id of the form.
  3. **formName** - The name of the form.

  This function returns the open tag for the form and any standard hidden elements.

* **endForm()**

  Close out a form.

  This function returns the form closing tag.

### LINK [LinkTool]

Creates links; see default templates for examples.

* **getPageUrl(String urlBase, String action)**

  Get the url for a page being linked to.

  1. **urlBase** - The base url.
  2. **action** - The action being linked to.

  This function returns the value to place in the href attribute of a link.

* **getUserUrl(String username, String fullName)**

  Generates URL for user details.

  1. **username** - User name.
  2. **fullName** - User's full name.

  This function returns the URL to user details page.

### MESSAGE [MessageTool]

Enables internationalization of templates, providing functions for localizing strings.

* **get(String bundle, String key[, String arg0[, String arg1[, String arg2]]])**

  Returns the message.

  1. **bundle** - Resource bundle.
  2. **key** - Message key.
  3. **arg0** - Message argument.
  4. **arg1** - Message argument.
  5. **arg2** - Message argument.

  This function returns the message.

* **getFieldLabel(String bundle, String key, boolean required)**

  Returns the message with the appropriate label modifier (':' and possibly an asterisk if field is required).

  1. **bundle** - The bundle where the message lives.
  2. **key** - The key where the message is stored.
  3. **required** - If the field is required.

  This function returns the message with appropriate label modifiers.

### STRING [StringTool]

Returns a formatted file size string, such as 45KB, 100MB, or 1GB.

* **formatFileSize(long fileSize)**

  Returns the file size string.

  **fileSize** - File size in bytes.
  
  This function returns the file size string.

* **wordWrap(String text, int width)**

  Wraps text string at word boundaries.

  1. **s** - String to word wrap.
  2. **width** - Number of characters at which to wrap.

  This function returns word wrapped string.

* **escapeXml(String s)**

  Escape out the xml from the text.

  **s** - The text that we need to escape xml from.

  This function returns the text with xml escaped.

### TEXTPARSER [TextParserTool]

Converts text into “linkified” html, with IDs and wiki words converted into appropriate links.

* **parseText(String text)**

  Returns linkified text (add href tags to object ids and urls).

  **text** - Text to process.

  This function returns the replacement text with link replacement.

### PAGE_INFO [PageInformationTool]

Allows access to information specific to the page that is passed in.

<table>
<tr>
<th>Information</th>
<th>Description</th>
<th rowspan="12"></th>
</tr>
<tr>
<td>actionName</td>
<td>The name of the action that was requested (e.g. viewArtifact, listTrackers)</td>
<td></td>
</tr>
<tr>
<td>currentUser</td>
<td>User object that contains information about the current user: <br>
<ul>
<li>$PAGE_INFO.currentUser.username (Login ID)</li>
<li>$PAGE_INFO.currentUser.fullName (Full name)</li>
<li>$PAGE_INFO.currentUser.email (E‐mail address)</li>
<li>$PAGE_INFO.currentUser.locale (Locale, such as en_US)</li>
<li>$PAGE_INFO.currentUser.lastLogin (Date and time of last login)</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td>path</td>
<td>The full path string of the requestʹs target object (e.g. projects.test/trackers.foo/bar). If no path is present on the request, this returns an empty string.</td>
<td></td>
</tr>
<tr>
<td>projectPath</td>    
<td></td>
<td>The project path (e.g. projects.test) on the current folderPath or an empty string if none exists (no path context or just a project context).</td>
</tr>
<tr>
<td>itemName</td>
<td>The name of the item (e.g. artf1234, Home) on the current request or an empty string if there is no path context or just a project or folder context.</td>
<td></td>
</tr>
<tr>
<td>objectId</td>
<td>The id of the requested object (e.g. artf1234, proj1234).</td>
<td></td>
</tr>
<tr>
<td>objectType</td>
<td>The type string of the current object (i.e. An artifact would have Tracker.Artifact)</td>
<td></td>
</tr>
<tr>
<td>projectId</td>
<td>The ID of the project on the request or the project that contains the current folder or item.</td>
<td></td>
</tr>
<tr>
<td>requestUrl</td>
<td>The URL that was requested (e.g. /ce/tracker/do/viewArtifact/projects.test/tracker.foo/artf1234).</td>
<td></td>
</tr>
<tr>
<td>isSuperUser</td>
<td>True, if the current user is a site admin.</td>
<td></td>
</tr>
<tr>
<td>isLoggedIn</td>
<td>True, if the current user is logged into the system.</td>
<td></td>
</tr>
</table>

### GLOBAL [GlobalTool]

Allows access to various kinds of static information about the site.

<table>
<tr>
<th>Static Information</th>
<th>Description</th>
</tr>
<tr>
<td>datePattern</td>
<td>The standard date pattern used for date conversions.</td>
</tr>
<tr>
<td>imageRoot</td>
<td>The root URL path of Digital.ai TeamForge images.</td>
</tr>
<tr>
<td>isApprovalRequiredForNewUsers</td>
<td>A flag that indicates whether new users must be approved before they can use the site.</td>
</tr>
<tr>
<td>isRequireAssociationOnDocumentCreate</td>
<td>A flag that indicates whether creation of a document requires an association with an object.</td>
</tr>
<tr>
<td>isSelfCreationEnabled</td>
<td>A flag that indicates whether visitors are allowed to create new accounts in the application by themselves.</td>
</tr>
<tr>
<td>isUsingExternalAuthentication</td>
<td>A flag that indicates whether logins are authenticated against an external server. (Currently this means LDAP.)</td>
</tr>
</table>

### ApiTool

API60 [ApiTool] exposes the Digital.ai TeamForge SOAP service interfaces for use by Velocity templates.

While the interfaces corresponding to the SOAP API are provided, the implementation is efficient; the SOAP network protocol is not actually used.

 {% include note.html content="API50 is present for backward compatibility and may be removed in future. API44 and API43 are removed completely." %}

#### Interfaces

<table>
<tr>
<th>Interface</th>
<th>Description</th>
</tr>
<tr>
<td>sessionKey</td>
<td>Gets the soap session id that should be passed in as the first parameter to soap service methods.</td>
</tr>
<tr>
<td>discussionApp</td>
<td>Gives access to the methods in the Discussion application.</td>
</tr>
<tr>
<td>documentApp</td>
<td>Gives access to the methods in the Documents application.</td>
</tr>
<tr>
<td>frsApp</td>
<td> Gives access to the methods in the File Releases application.</td>
</tr>
<tr>
<td>integrationDataApp</td>
<td>Gives access to the methods for Data Integration.</td>
</tr>
<tr>
<td>newsApp</td>
<td>Gives access to the methods in the Project News application.</td>
</tr>
<tr>
<td>rbacApp</td>
<td>Gives access to the methods for role‐based access control.</td>
</tr>
<tr>
<td>scmApp</td>
<td>Gives access to the methods for version control (SCM) integration.</td>
</tr>
<tr>
<td>SourceForge</td>
<td>Gives access to the methods in the main Digital.ai TeamForge application.</td>
</tr>
<tr>
<td>taskApp</td>
<td>Gives access to the methods in the Tasks application.</td>
</tr>
<tr>
<td>trackerApp</td>
<td>Gives access to the methods in the Tracker application.</td>
</tr>
<tr>
<td>wikiApp</td>
<td>Gives access to the methods in the Wiki application.</td>
</tr>
<tr>
<td>categorizationApp</td>
<td>Gives access to the methods in project categorization.</td>
</tr>
<tr>
<td>emptyFilter</td>
<td>Gets an empty filter that can be passed into methods that require soap filters.</td>
</tr>
<tr>
<td>PageApp</td>
<td>Handles the activities and items associated with project pages.</td>
</tr>
<tr>
<td>PlanningApp</td>
<td>Gives access to methods in the Planning application.</td>
</tr>
</table>

#### Example

This is an example of how you might use some popular API calls in a Velocity template:

```shell
## Display Server version, current project title and description
#set( $sessionKey = $API60.sessionKey ) 
#set( $projectId = $PAGE_INFO.projectId ) 
#set( $projectData = $API60.sourceForge.getProjectData($sessionKey,$projectId) )

<p>Server Version: $API60.sourceForge.getVersion($sessionKey)</p>
<p>Project Title: ${projectData.title}</p>
<p>Project Desc: ${projectData.description}</p>
````

## Lab Management API Methods

Almost all Lab Management functionality is available via an API method.

Lab Management API methods come in two forms: signed and unsigned.

 * Signed methods require authentication, in accordance with the [User Authentication documentation][teamforgesoapapiref.html#teamforgelabmanagement]. Most of the API methods in Lab Management, and all of the most useful ones, are signed methods which require authentication to use. The `cubit_api_client.py` client makes using these signed methods easy by handling the authentication negotiation for you.

 * Unsigned methods do not require authentication.

 {% include note.html content="This API is under active development. We have started with what we feel are the most common actions which would need to be performed on an automated basis, and will be expanding this list over time as we receive feedback about what our users want and need. Please let us know if there are missing features or bugs!" %}

### CheckHostConsistency

Check the setup of all hosts in the domain to make sure their representation is internally complete within Lab Management.

#### Overview

This method is only available to users to Lab Management Domain Admins and can be considered a maintenance method that should rarely, if ever, need to be run. Three areas of setup consistency are checked for each host:

 1. Verification and re-application of the host's internal database representation within Lab Management. This may be needed after an upgrade of the Lab Management application is installed.

 2. Verification that the IP address assigned to the host matches the hostname. If you suspect DNS setup issues in your domain, this test should catch them (unless the errors are transient). Lab Management will not let you create hosts with invalid DNS, but if DNS for the host gets changed improperly after the host is created, your host will experience many problems in the Lab Management environment until it is fixed.

 3. Verification of the IP mask/gateway configured for the host with the actual one it resolves to.

 4. Re-generation of statistics system performance monitoring configuration files for the host. If monitoring is not properly working for a host, regenerating the configuration files will usually fix the problem.

Depending on the number of hosts in your domain, this method can take some time to complete. If you have questions on the output of this method, please see your local Lab Management Administrator or contact CollabNet directly for assistance.


#### URL

```shell
/cubit_api/1/check_host_consistency
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful completion of host consistency check:
    
```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <output>All Hosts OK</output>
    </cubit>

    If the user is not a Lab Management Domain Admin:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>User 'grue' is not authorized to run this method.</error>
    </cubit>

    If there is an error re-generating the host's internal database 
    representation for at least one host:
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
            <output>Hosts which were not successfully updated:
            cu011.dev.cubitdemo.net</output>
    </cubit>

    If the system performance statistics configuration files are not
    properly generated for at least one host:
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
            <output>Hosts which are not properly setup to collect
            performance data: cu011.dev.cubitdemo.net</output>
    </cubit>

    If there is a DNS mismatch for at least one host:
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
            <output>Hosts which require re-ip'ing:
            cu011.dev.cubitdemo.net</output>
    </cubit>

    If there is a IP mask mis-match:
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
            <output>Hosts whose IP mask/gateway does not match with the
            IP mask/gateway it resolves to:
            cu011.dev.cubitdemo.net</output>
    </cubit>
````
            
#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### CloudCreateHosts

Create one or more hosts from a cloud given the host-type and size.

The cloud will match the host-type and size to one (or more) source(s) from the cloud in order to fill the entire order. Host types and sizes cannot be mixed in a single API call. All the hosts must be the same type/size. The method will fail if the cloud's sources cannot accomodate that many hosts of the given type/size.

Any user who is a member of a project that has been given permission to allocate from this cloud can create instances.

#### URL

```shell
/cubit_api/1/allocate_hosts_from_cloud
````

#### Authentication

This method requires authentication using an API key.


#### Parameters

* **alloc_hours** (zero or once)

  * Amount of time for which to allocate the host. The allocation limit is subject to the limit set by the project or cloud administrator.
  * Type: Float

* **alloc_minutes** (zero or once)

  * Similar to alloc_hours parameter, but in minutes. It is mutually exclusive with the `alloc_hours` option, neither of these options should be specified, or only one of these options should be specified. If `alloc_hours` or `alloc_minutes` is set to 0, or if `alloc_hours` and `alloc_minutes` is unset, the allocation time defaults to the longest possible time available in the project.
  * Type: Integer

* **cloud** (Required, once)

  * Name of Lab Management cloud to allocate instances from.
  * Type: String

* **count** (zero or once)

  * The number of identical instances to bring up. The instances will all be running the same profile and version. Must be an integer greater than 0. If unset, defaults to 1.
  * Type: Integer

* **descr** (zero or once)

  * Set the specified string as a description for the allocated hosts. This is useful if you wish to uniquely identify a group of hosts which have all been allocated to the same user at the same time for the same purpose.
  * Type: String

* **dont_delete** (zero or once)

  * By default, EC2 instances will automatically be deleted when they are deallocated. If `dont_delete` is set to `True`, the instances created will not be deleted when they are deallocated, and will instead revert back to the project pool.
  * Type: String

* **host_type** (Required, once)

  * The name of the host_type of machine to create. Must be one of the host-types supported by the cloud.
  * Type: String

* **profile** (Required, once)

  * Name of the profile to assign to the host. The profile must, of course, be a profile that is eligible to be built by the host-type/size you selected.
  * Type: String

* **project** (Required, once)

  * Name of Lab Management project to place hosts into. You must have permission to add hosts to this project: that is, you must either be a Project Admin or Delegated Host Management must be turned on in your project.
  * Type: String

* **revision** (zero or once)

  * Revision number of the profile you wish to assign to the host. Mutually exclusive with the `version` option, but at least one of the `version` or `revision` options must be specified.
  * Type: Integer

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **size** (Required, once)

  * The name of the machine size to create. Must be one of the sizes supported by the given host_type.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

* **version** (zero or once)
  
  * Version number or tag name of the profile you wish to assign to the host. The special version tag `HEAD` always denotes the latest version of the profile at the moment of execution. Note that profile tags can move between versions: this is a useful feature, but you should be aware of it. Mutually exclusive with the `revision` option, but at least one of the `version` or `revision` options must be specified.
  * Type: String

#### Example Response

Successful allocation of 10 instances:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <output>ec2-pending-1204832590-85</output>
        <output>ec2-pending-1204832595-09</output>
        <output>ec2-pending-1204832599-97</output>
        <output>ec2-pending-1204832611-49</output>
        <output>ec2-pending-1204832615-60</output>
        <output>ec2-pending-1204832620-29</output>
        <output>ec2-pending-1204832624-25</output>
        <output>ec2-pending-1204832628-46</output>
        <output>ec2-pending-1204832640-90</output>
        <output>ec2-pending-1204832645-60</output>
    </cubit>

    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user lacks permission to create hosts in the project:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to create hosts in this project.</error>
    </cubit>

    If the project does not have the permissions to allocate from the
    requested cloud:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>This project is not authorized to create hosts in this cloud.</error>
    </cubit>

    If the cloud does not have enough space on the sources to allocate that many hosts:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>This cloud does not have enough resources to create [n] hosts.</error>
    </cubit>
````

#### Response Codes

* 400 - Login failed / Insufficient permissions

### GetAuthToken

GetAuthToken(userid) -> token

#### URL

```shell
/cubit_api/1/get_auth_token
````

#### Authentication

This method does not require authentication.

#### Parameters

This method does not take any parameters.

#### Response Codes

This method does not have any documented response codes.


### HostAllocate

Allocate a host to a user.

Hosts must be in the Free state to be allocated, although users with Project Admin access can re-allocate hosts which are in the `Allocated` state to other users in their project. Domain Admin users can re-allocate machines between projects and users, although if a machine is reallocated to a user in another project, that user must also be a member of the destination project. The user must be authorized to allocate the host. If the host is in any of the following states, this method will fail. 

 * Immutable
 * Powercycle
 * Rebuild or 
 * Rebuilding


#### URL

```shell
/cubit_api/1/alloc_host
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **alloc_hours** (zero or once)

  * Amount of time for which to allocate the host. The allocation limit is subject to the limit set by the project or cloud administrator.
  * Type: Float

* **alloc_minutes** (zero or once)

  * Similar to alloc_hours parameter, but in minutes. It is mutually exclusive with the `alloc_hours` option, neither of these options should be specified, or only one of these options should be specified. If `alloc_hours` or `alloc_minutes` is set to `0`, or if `alloc_hours` and `alloc_minutes` is unset, the allocation time defaults to the longest possible time available in the project.
  * Type: Integer

* **alloc_proj** (zero or once)

  * The project to allocate the machine to. The alloc_user must be a valid Lab Management user in the project, or else this method will fail. Only Domain Admins can change the project that a host is assigned to. If not specified, the project is not changed. At least one of `alloc_user` or `alloc_proj` must be specified.
  * Type: String

* **alloc_user** (zero or once)

  * Login name of user to allocate host to. Only Project Admins or better can specify a user other than themselves. Other users can only allocate machines to themselves. If not specified, defaults to userid. At least one of `alloc_user` or `alloc_proj` must be specified.
  * Type: String

* **force** (zero or once)

  * If the machine is currently in the Allocated state, the force option must be given to reassign the host to another user. The force option is only available to Project Admins and above. If the host is a virtual host, and any virtual guests of this host are in the Allocated state, this option must also be used, or the entire allocation will fail. The only valid value for this parameter is `True`.
  * Type: String

* **guests** (zero or once)

  * If the machine is a virtual host and has active virtual guests, setting this parameter to `True` will move the virtual guests along with the virtual host. Because moving a virtual host will move several hosts at once, we have a separate parameter to confirm this action. The only valid value for this parameter is `True`. If the host has no virtual guests, this option has no effect.
  * Type: String

* **host** (Required, once)

  * Fully qualified hostname to allocate.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful host allocation:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized, or the host does not exist:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to allocate this host.</error>
    </cubit>

    If the host is allocated to a deleted project:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>Cannot allocate host 'cu001.dev.cubitdemo.net' to a
        deleted project 'look'</error>
    </cubit>
````

#### Response Codes

 * 200 - ok
 * 400 - Login failed / Insufficient permissions

### HostAssignProfileAndRebuild

Assign a profile to the host and rebuild it with that profile/version.

The user must be authorized to rebuild the host. If the host is in any of the states which disallow rebuilding, such as `Immutable`, `Rebuild`, or `Rebuilding`, this method will fail. The host must also not be of a type which prohibits rebuilding (e.g., an EC2 host). If you do not want to change the profile a host is running, and just want to rebuild a host, you can save a few keystrokes and use the Rebuild method instead.

#### URL

```shell
/cubit_api/1/assign_rebuild
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **host** (Required, once)

  * Fully qualified hostname to assign profile to and rebuild.
  * Type: String

* **profile** (Required, once)

  * Name of the profile to assign to the host.
  * Type: String

* **revision** ( zero or once )

  * Revision number of the profile you wish to assign to the host. Mutually exclusive with the version option, but at least one of the version or revision options must be specified.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

* **version** (zero or once)

  * Version number or tag name of the profile you wish to assign to the host. The special version tag `HEAD` always denotes the latest version of the profile at the moment of execution. Note that profile tags can move between versions: this is a useful feature, but you should be aware of it. Mutually exclusive with the `revision` option, but at least one of the `version` or `revision` options must be specified.
  * Type: String

#### Example Response

Successful initiation of rebuild:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized, or the host does not exist:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to allocate a profile to this host and rebuild it.</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostDelete

Delete one or more hosts.

The host must not be in the `Immutable` state for this method to work. Hosts can be deleted by users under the following conditions:

 * Lab Management Domain Admins can delete any host, regardless if it is physical, virtual, or from a remote cloud.
 * Users who are not Lab Management Domain Admins can delete `virtual guests` if the parent host is allocated to them and Delegated Host Management is turned on in their project.
 * Users who are not Lab Management Domain Admins can also delete `remote cloud hosts` allocated to them if Delegated Host Management is turned on in their project.

#### URL

```shell
/cubit_api/1/delete_host
````

#### Authentication

This method requires authentication using an API key.


#### Parameters

* **force** (zero or once)

  * If the machine being deleted does not belong to the user initiating the request, the force option is required. The only valid value for this parameter is `True`.
  * Type: String

* **guests** (zero or once)

  * If the machine is a virtual host and has active virtual guests, setting this parameter to `True` will delete the virtual guests along with the virtual host. Because deleting a virtual host will delete several hosts at once, we have a separate parameter to confirm this action. The only valid value for this parameter is `True`. If the host has no virtual guests, this option has no effect. Use of this option can be really convenient, or it can really ruin someone's day!
  * Type: String

* **hosts** (Required, once)

  * List of comma-separated, fully qualified hostnames to delete. Hosts must not be in the `Immutable` state.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful host delete of the host `cu011.cubit.example.com`:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <output>cu011.cubit.example.com</output>
    </cubit>

    If the user is unauthorized:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>0 of 1 hosts deleted successfully. Failed hosts below.</error>
        <output>cu013.cubit.example.com: You are not authorized to delete this host.</output>
    </cubit>

    If a deletion of hosts partially succeeds:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>6 of 8 hosts deleted successfully. Failed hosts below.</error>
        <output>cu013.cubit.example.com: You are not authorized to delete this host</output>
        <output>cu016.cubit.example.com: Host deletion failed</output>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostFree

Free a host currently assigned to a user.

Hosts must be in the `Allocated` state to be freed. A user can only free hosts already assigned to them, although Project Admins and Domain Admins can free hosts in their project which are currently allocated. If it is a virtual guest and "Delete on Deallocation" flag is ON, the virtual guest would be deleted after it is set Free.

#### URL

```shell
/cubit_api/1/free_host
````

#### Authentication

This method requires authentication using an API key.


#### Parameters

* **force** (zero or once)

  * If the machine being freed does not belong to the user initiating the request, the force option is required. Only Project Admins and Domain Admins can free hosts which do not belong to them. The only valid value for this parameter is `True`.
  * Type: String

* **host** (Required, once)

  * Fully qualified hostname to free. Hosts must be in the Allocated state to be freed.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful freeing of host:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized, or the host does not exist:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to free this host.</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostGetAssignedProfile

Get the assigned profile for the host, and returns the profile name along with the revision and version number.

Output is available in both text and XML formats. You can also get this information from the QueryAlloc method, but the output of this method is easier to parse if you have scripts checking a profile. The user requesting information about a host must have at least login privileges to that host.

#### URL

```shell
/cubit_api/1/assigned_profile
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **host** (Required, once)

  * Fully qualified hostname to query.
  * Type: String

* **output** (Required, once)

  * Output type, either 'txt' (for text output) or 'xml' (for XML output).
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Sample XML output:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
      <profile revision="1838" version="5">solaris10_x86</profile>
    </cubit>

    Sample text output:
    solaris10_x86  1838  5

    If user is unauthorized:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You do not have permissions to view this host</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostGetMyAssignedProfile

Get the profile and version assigned to the host invoking this method.

#### URL

```shell
/cubit_api/1/my_profile
````

#### Authentication

This method does not require authentication.


#### Parameters

* **output** (Required, once)

  * Output type, either 'txt' (for text output) or 'xml' (for XML output).
  * Type: String

#### Example Response

Sample XML output:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
      <profile revision="26" version="2">rhel3_base</profile>
    </cubit>

    Sample text output:
    rhel3_base  26  2
````

#### Response Codes

* 200 - ok

### HostPerfColl

Get performance collection data from remote hosts managed by Lab Management.

This method takes one parameter, `data`. The hostname is auto-derived using reverse DNS. There is no other way to verify the sending host.

The currently supported statgroups are:

* **net** - Returns a dictionary of network interface transfer metrics. The key is the name of the interface. Value is a tuple containing: (`bytes_in`, `bytes_out`, `errors_in`, `errors_out`, `pkts_in`, `pkts_out`).
* **loadavg** - Returns a tuple containing the (1, 5, 15) minute load average on the system.
* **storage** - Returns a dictionary of disk storage metrics. The key is the name of the mounted partition and the value is a tuple of: (`block_size`, `blocks_avail`, `blocks_used`, `block_errors`).
* **systatd** - Returns a string containing the systatd output file for the system.

#### URL

```shell
/cubit_api/1/host_perfcoll
````

#### Authentication

This method does not require authentication.

#### Parameters

This method does not take any parameters.

#### Response Codes

This method does not have any documented response codes.

### HostPowercycle

Powercycle a host.

This method immediately executes a powercycle of the host. No graceful shutdown is run on the host at the operating system level. It is recommended that this method only be run when the normal operating shutdown/reboot sequence has failed or is unavailable. You can only powercycle machines in the `Allocated`, `Free`, and `Immutable` states.

#### URL

```shell
/cubit_api/1/powercycle
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **force** (zero or once)

  * If the machine being powercycled is a virtual host, the force option is required. The only valid value for this parameter is `True`.
  * Type: String

* **host** (Required, once)

  * Fully qualified hostname to powercycle.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful completion of powercycle:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized, or the host does not exist:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to powercycle this host.</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostRebuildCancel

Cancel a rebuild for a host.

The host must be in `Rebuild` state for this method to work. In order to cancel a rebuild for a host, the user must have permission to rebuild the host, that is, they must either:

 * Have the host allocated to them
 * Be a Lab Management Project Admin in the project, or
 * Be a Lab Management Domain Admin

#### URL

```shell
/cubit_api/1/rebuild_cancel
````

#### Authentication

This method requires authentication using an API key.


#### Parameters

* **host** (Required, once)

  * Fully qualified hostname to cancel rebuild of. Hosts must be in the `Rebuild` state.
  * Type: String

* **sig** (Required, once)

   * API authentication hash signature.
   * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful host rebuild cancel:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to cancel a rebuild for this host.</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### HostRebuild

Rebuild a host with the currently selected profile and profile version.

The user must be authorized to rebuild the host. The host must also not be in any of the states which prohibit rebuilding, such as `Immutable`, `Powercycle`, `Rebuild`, or `Rebuilding`, or this method will fail.

The host must also indicate that it is rebuildable (e.g., not an EC2 host), or this method will fail.


#### URL

```shell
/cubit_api/1/rebuild
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **host** (Required, once)

  * Fully qualified hostname to rebuild.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful initiation of rebuild:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>

    If the user is unauthorized, or the host does not exist:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>You are not authorized to rebuild this host.</error>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### PblChangeDesc

Project Build Library (PBL) file and directory description changing interface. This function is used to change the description for files and directories in the Project Build Library. This function may be useful if you are building your own PBL client.

#### URL

```shell
/cubit_api/1/pbl_changedesc
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **comment** (zero or once)

  * An optional comment to leave about the operation being performed. The comment will not appear in the PBL, but it will be in the audit log entry for this event.
  * Type: String

* **desc** (Required, once)

  * The new text description of the file. This description will completely replace any description currently set for the file.
  * Type: String

* **path** (Required, once)

  * The path to the file being operated on. For example, if the complete file URL is `/pbl/zork/pub/foo/bar/test.txt`, the path would be `/foo/bar/test.txt`.
  * Type: String

* **proj** (Required, once)

  * The name of the project which contains the file we are operating on.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

 * **type** (Required, once)

   * The type of file that we are operating on. Valid values are 'pub' and 'priv'.
   * Type: String

 * **userid** (Required, once)

   * The login name of the user initiating the request.
   * Type: String

#### Example Response

```shell  
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### PblDelete

Project Build Library (PBL) file and directory delete interface. This function is used to permanently remove files and directories in the Project Build Library. This function may be useful if you are building your own PBL client.

#### URL

```shell
/cubit_api/1/pbl_delete
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **comment** (zero or once)

  * An optional comment to leave about the operation being performed. This will not appear in the PBL, but it will be in the audit log entry for this event.
  * Type: String

* **dryrun** (Required, once)

  * If this parameter is set to True, the specified path will not actually be deleted. The only valid value for this parameter is `True`.
  * Type: String

* **force** (zero or once)

  * If the force option is present and set to True, and the specified path argument is a directory, a recursive delete of the directory will be performed. The only valid value for this parameter is `True`.
  * Type: String

* **path** (Required, once)

  * The path to the file being operated on. For example, if the complete file URL is `/pbl/zork/pub/foo/bar/test.txt`, the path would be `/foo/bar/test.txt`.
  * Type: String

* **proj** (Required, once)

  * The name of the project which contains the file we are operating on.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **type** (Required, once)

  * The type of file that we are operating on. Valid values are 'pub' and 'priv'.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

```shell        
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### PblMove

Project Build Library (PBL) file and directory move interface. This function may be useful if you are building your own PBL client.

#### URL

```shell
/cubit_api/1/pbl_move
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **comment** (zero or once)

  * An optional comment to leave about the operation being performed. This will not appear in the PBL, but it will be in the audit log entry for this event.
  * Type: String

* **destpath** (Required, once)

  * The path to move the destination file to. For example, if the complete file URL is `/pbl/zork/pub/foo/bar/test.txt`, the srcpath would be `/foo/bar/test.txt`. Two important things to note about this parameter:

    1. If you specify a path which does not exist, that path will be automatically created for you as part of the move.
    2. If the `destpath` parameter ends with a slash ("/"), the destination will be assumed to be a directory. If it does not end with a slash, the destination will be assumed to be a file.
  * Type: String

* **destprj** (zero or once)

  * The destination project for the file. You must have permissions to upload files into both the `srcprj` and the `destprj`, or the move will fail. If not specified, defaults to `srcprj`.
  * Type: String

* **desttype** (zero or once)

  * The destination type of the file. Valid values are 'pub' and 'priv'. If not specified, defaults to `srctype`.
  * Type: String

* **force** (zero or once)

  * If the force option is present, the file will be moved even if a file with that name currently exists, and the previous file will be deleted and replaced with this file. The only valid value for this parameter is `True`.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **srcpath** (Required, once)

  * The path to the source file being operated on. For example, if the complete file URL is `/pbl/zork/pub/foo/bar/test`.txt, the srcpath would be `/foo/bar/test.txt`.
  * Type: String

* **srcprj** (Required, once)

  * The project in which the source file is located.
  * Type: String

* **srctype** (Required, once )

  * The source type of the file. Valid values are 'pub' and 'priv'.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

```shell        
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### PblUpload

Project Build Library (PBL) file and directory upload interface. This function is used to create files and directories in the Project Build Library. Unless you are building your own PBL client, this function will not be very useful to you.

#### URL

```shell
/cubit_api/1/pbl_upload
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **comment** (zero or once)

  * An optional comment to leave about the operation being performed. This will not appear in the PBL, but it will be in the audit log entry for this event.
  * Type: String

* **desc** (zero or once)

  * The text description of the file.
  * Type: String

* **file** (Required, once)

  * URL-encoded name and contents of the file, encoded as per RFC 1867.
  * Type: String

* **force** (zero or once)

  * If the force option is present, the file will be uploaded even if a file with that name currently exists. A file cannot be uploaded over a directory of the same name, even if the force parameter is present. The only valid value for this parameter is `True`.
  * Type: String

* **md5sum** (Required, once)

  * The md5 checksum of the file being uploaded.
  * Type: String

* **path** (Required, once)
  
  * The path to the file being operated on. For example, if the complete file URL is `/pbl/zork/pub/foo/bar/test.txt`, the path would be `/foo/bar`. 

    {% include note.html content="The path parameter is used slightly differently in this method than in other methods, since the filename is not appended to the end of the parameter." %}
  * Type: String

* **proj** (Required, once)

  * The name of the project which contains the file we are operating on.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **type** (Required, once)

  * The type of file that we are operating on. Valid values are 'pub' and 'priv'.
  * Type: String

* **userid** (Required, once)
 
  * The login name of the user initiating the request.
  * Type: String

#### Example Response

```shell        
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### ProfileAdd

Add a profile to the system.

The following conditions must hold for a profile to be added by name:

 * The `profile_name` must be specified.
 * The `profile_file` must not specified.
 * The profile must already exist in SVN.
 * The user calling this method must be a Domain Admin.

The following conditions must hold for a profile to be uploaded:

 * The `profile_file` must be specified.
 * The `profile_name` must not be specified.
 * The user calling this method must have permission to add profiles to the specified project.

#### URL

```shell
/cubit_api/1/add_profile
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **can_users_modify** (Required, once)

  * Set this to `True` if user's with Root Access or better should be able to make modifications to the project. If set to `False`, only the owning user and users with Project Admin access (or better) will be able to modify the profile.
  * Type: String

* **is_prebuilt** (Required, once)

  * Set this to `True` if this profile is a prebuilt image, `False` if this profile is installed via a network install method.
  * Type: String

* **is_public** (Required, once)

  * If the profile is public (i.e can be built by any project). Valid value can be either `True` or `False`.
  * Type: String

* **owner** (zero or once)

  * Lab Management user that this profile will be associated with. The user must be a member of the owning project in order to be able to modify the profile. If unset, this profile will not belong to any particular user.
  * Type: String

* **profile_file** (zero or once)

  * The filename of a profile to be uploaded. The specified file must:

    1. Exist on your local system.
    2. Contain a valid profile name. Profile names can only contain letters, numbers, underscores ("_"), and dashes ("-"). Profile names are case sensitive.
    3. Not currently exist as a profile name on the system.
    4. Be a valid XML file, and contain all the needed attributes for a Lab Management profile.
  * Type: String

* **profile_name** (zero or once)

  * The name of a profile that already exists in Lab Management's Subversion Repository.
  * Type: String

* **project** (zero or once)

  * Project that will own this profile. If unset, this profile will not belong to any particular project.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **summary** (Required, once)

  * Summary of the purpose of this profile.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful addition of the profile rhel3_base:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <output>rhel3_base</output>
    </cubit>

    If the user is unauthorized:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>Failed to add profile rhel3_base.</error>
        <output>User 'userid' does not have Domain Admin rights.</output>
    </cubit>
````
    
#### Response Codes

 * 200 - ok
 * 400 - Login failed / Insufficient permissions

### ProfileDelete

Delete a profile from the system.

Profiles can be deleted under the following conditions:

 * No host has ever been built or is currently building with this profile.
 * The user calling this method has permission to modify this profile.

#### URL

```shell
/cubit_api/1/delete_profile
````

#### Authentication

This method requires authentication using an API key.


#### Parameters

* **profiles** (Required, once)

  * List of comma-separated, profile names to delete. Profiles must never have been used to build any hosts. The user invoking this API must have modify rights on the profiles.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Successful delete of the profile rhel3_base:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <output>rhel3_base</output>
    </cubit>

    If the user is unauthorized:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>0 of 1 profiles deleted successfully. Failed profiles below.</error>
        <output>rhel3_base: You do not have modify rights on this profile.</output>
    </cubit>

    If a deletion of profiles partially succeeds:
    <?xml version='1.0'?>
    <cubit version='1'>
        <error>7 of 8 profiles deleted successfully. Failed profiles below.</error>
        <output>rhel3_base: This profile has been used to build hosts.</output>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### ProfileGetMyPkglist

List the packages associated with the profile assigned to the calling host.

#### URL

```shell
/cubit_api/1/getmypkglist
````

#### Authentication

This method does not require authentication.

#### Parameters

* **output** (Required, once)

  * Output type, either 'txt' (for text output) or 'xml' (for XML output).
  * Type: String

#### Example Response

Sample XML output:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
      <package version="1.4.3-6">libtool-libs</package>
      <package version="2.1.15-10">cyrus-sasl-md5</package>
      <package version="20020927-11.30.4">iputils</package>
      <package version="3.03-28">perl-HTML-Tagset</package>
      <package version="1.4.1-2">python-optik</package>
      ...
      <package version="1.7-23">time</package>
      <package version="3.2.3-54">cpp</package>
      <package version="8.3.5-92.4">tcl</package>
      <package version="0.2.3-7.1">audiofile</package>
    </cubit>
  
    Sample text output:
    libtool-libs  1.4.3-6
    cyrus-sasl-md5  2.1.15-10
    iputils  20020927-11.30.4
    perl-HTML-Tagset  3.03-28
    python-optik  1.4.1-2
    ...
    time  1.7-23
    cpp  3.2.3-54
    tcl  8.3.5-92.4
    audiofile  0.2.3-7.1
````

#### Response Codes

* 200 - ok

### ProfileGetPkglist

List packages associated with a particular version or revision of a profile.

If neither version nor revision is set, the latest (HEAD) revision of the profile is selected. You must have permissions to view the profile in order to retrieve a package listing. The profile must be public, or you must be a valid user in the project that owns the profile.

#### URL

```shell
/cubit_api/1/getpkglist
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **output** (zero or once)

  * Ouput mode. 'txt' or 'xml'
  * Type: String

* **profile** (Required, once)

  * Profile to get package list for.
  * Type: String

* **revision** (zero or once)

  * Revision of profile to get package list for.
  * Type: Integer

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

* **version** (zero or once)

  * Version of profile to get package list for.
  * Type: Integer

#### Example Response

```shell        
    (output='xml'):

    <?xml version='1.0'?>
    <cubit version='1'>
      <package version="1.2.3">pkgname1</package>
      <package version="4.5.6">pkgname2</package>
      <package version="7.8.9">pkgname3</package>
    </cubit>

    (output='txt'):
    pkg1  1.2.3
    pkg2  4.5.6
    pkg3  7.8.9
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### QueryAlloc

Determine, at either a `domain`, `project`, `user`, or `host` level, how hosts are allocated and who they are allocated to.

Users are only allowed to get information about hosts which they have access to see. For example, if you are not a member of a project, you cannot query that project's host allocations. If you query the domain, you will only see allocation information for projects to which you belong. This method is used by Lab Management internally, and it is made available for users as well, since they may find this data useful.

#### URL

```shell
/cubit_api/1/query_alloc
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **full** (zero or once)

  * If `full=true` then the complete information about the host is printed.
  * Type: String

* **maxhosts** (zero or once)

  * The maximum number of hosts to return for the query. If `type=domain`, this will be the maximum number of hosts to return per project (i.e. if this is set to 5 and there are two projects in the domain, up to 10 hosts may be returned). If `type=host`, this parameter will not be used. If maxhosts is set, the returned hosts will be sorted by the host's name.
  * Type: Integer

* **name** (zero or once)

  * The name of the host, project, or user to be queried. If `type=domain`, this argument is not required. If `type={host,project}` then this argument is required. If `type=user`, this argument is optional, defaulting to the name of the user who you authenticate as. Only Lab Management Domain Admins are allowed to query user allocations for users other than themselves.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **skiphosts** (zero or once)

  * The number of initial hosts that will be skipped over when returning the results. This only has an effect when maxhosts is also used. If type=domain, the hosts skipped are per per project. If `type=hosts`, this paramenter will not be used.
  * Type: Integer

* **type** (Required, once)

  * The type of service. Valid values are `host`, `project`, `user` and `domain`.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Here is a sample output where we query type=host and

```shell
    name=cu011.dev.cubitdemo.net:

    <?xml version='1.0'?>
    <cubit version='1'>
      <project name="zork">
        <host version="2">
          <name>cu011.dev.cubitdemo.net</name>
          <alloc_user>yz</alloc_user>
          <alloc_project>zork</alloc_project>
          <labels>
            <label name="cubit_user">yz</label>
            <label name="cubit_project">zork</label>
          </labels>
        </host>
      </project>
    </cubit>

    Here is a sample output where we query type=host,
    name=cu011.dev.cubitdemo.net and full=True:

    <?xml version='1.0'?>
    <cubit version='1'>
          <project name=zork>
            <host version="2">
    <name>cu011.dev.cubitdemo.net</name>
    <alloc_user>yz</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>2</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">2048</memsize>
            <disksize unit="GB">144</disksize>
    </hardware>
    <labels>
      <label name='cfprofile' rev='322' version='4'>rhel3_base</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170799967</label>
      <label name='cubit_state_mtime'>1170799967</label>
      <label name='cubit_build_time'>1169682748</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>yz</label>
      <label name='vmware-server'/>
      <label name='cubit_lom_addr'>cu3-l.sjc.collab.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:16:35:c3:9b:ed</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.21</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu011.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>

          </project>
    </cubit>

    Here is a sample output where we query type=domain:

    <?xml version='1.0'?>
    <cubit version='1'>
      <domain>
      <project name="zork">
          <host>
            <name>cu011.dev.cubitdemo.net</name>
            <alloc_user>yz</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">yz</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host>
            <name>cu012.dev.cubitdemo.net</name>
            <alloc_user>yz</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">yz</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
      </project>
      </domain>
    </cubit>

    Here is a sample output where we query type=domain and full=True:

    <?xml version='1.0'?>
    <cubit version='1'>
      <domain>
      <project name="zork">
          <host version="2">
    <name>cu011.dev.cubitdemo.net</name>
    <alloc_user>yz</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>2</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">2048</memsize>
            <disksize unit="GB">144</disksize>
    </hardware>
    <labels>
      <label name='cfprofile' rev='322' version='4'>rhel3_base</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170799967</label>
      <label name='cubit_state_mtime'>1170799967</label>
      <label name='cubit_build_time'>1169682748</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>yz</label>
      <label name='vmware-server'/>
      <label name='cubit_lom_addr'>cu3-l.sjc.collab.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:16:35:c3:9b:ed</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.21</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu011.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>

          <host version="2">
    <name>cu012.dev.cubitdemo.net</name>
    <alloc_user>yz</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>1</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">2048</memsize>
            <disksize unit="GB">144</disksize>
    </hardware>
    <labels>
      <label name='cfprofile' rev='322' version='4'>rhel3_all</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170800012</label>
      <label name='cubit_state_mtime'>1170800012</label>
      <label name='cubit_build_time'>1169687903</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>yz</label>
      <label name='vmware-server'/>
      <label name='cubit_lom_addr'>cu4-l.sjc.collab.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:16:35:5a:fe:39</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.22</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu012.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>
    </project>
    </domain>
    </cubit>

    Here is a sample output where we query type=project and name=zork:

    <?xml version='1.0'?>
    <cubit version='1'>
      <project name="zork">
          <host version="2">
            <name>cu011.dev.cubitdemo.net</name>
            <alloc_user>yz</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">yz</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu012.dev.cubitdemo.net</name>
            <alloc_user>yz</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">yz</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu013.dev.cubitdemo.net</name>
            <alloc_user>grue</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">grue</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu014.dev.cubitdemo.net</name>
            <alloc_user>root</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">root</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu019.dev.cubitdemo.net</name>
            <alloc_user>root</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">root</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu022.dev.cubitdemo.net</name>
            <alloc_user>grue</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">grue</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
          <host version="2">
            <name>cu091.dev.cubitdemo.net</name>
            <alloc_user>root</alloc_user>
            <alloc_project>zork</alloc_project>
            <labels>
              <label name="cubit_user">root</label>
              <label name="cubit_project">zork</label>
            </labels>
          </host>
      </project>
    </cubit>

    Here is a sample output where we query type=project, name=zork and
    full=True:

    <?xml version='1.0'?>
    <cubit version='1'>
      <project name="zork">
          <host version="2">
    <name>cu011.dev.cubitdemo.net</name>
    <alloc_user>yz</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>2</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">2048</memsize>
            <disksize unit="GB">144</disksize>
    </hardware>
    <labels>
      <label name='cfprofile' rev='322' version='4'>rhel3_base</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170799967</label>
      <label name='cubit_state_mtime'>1170799967</label>
      <label name='cubit_build_time'>1169682748</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>yz</label>
      <label name='vmware-server'/>
      <label name='cubit_lom_addr'>cu3-l.sjc.collab.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:16:35:c3:9b:ed</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.21</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu011.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>

          <host version="2">
    <name>cu012.dev.cubitdemo.net</name>
    <alloc_user>yz</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>1</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">2048</memsize>
            <disksize unit="GB">144</disksize>
    </hardware>
    <labels>
      <label name='cfprofile' rev='322' version='4'>rhel3_all</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170800012</label>
      <label name='cubit_state_mtime'>1170800012</label>
      <label name='cubit_build_time'>1169687903</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>yz</label>
      <label name='vmware-server'/>
      <label name='cubit_lom_addr'>cu4-l.sjc.collab.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:16:35:5a:fe:39</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.22</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu012.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>

          <host version="2">
    <name>cu013.dev.cubitdemo.net</name>
    <alloc_user>grue</alloc_user>
    <alloc_project>zork</alloc_project>
    <hardware>
            <vendor>Collabnet</vendor>
            <modelname>HP DL380</modelname>
            <ncpu>1</ncpu>
            <cpuarch>i386</cpuarch>
            <cpuname>Xeon</cpuname>
            <cpumhz>1400</cpumhz>
            <memsize unit="MB">1024</memsize>
            <disksize unit="GB">25</disksize>
    </hardware>
    <uuid>51 51 bb a0 00 15 15 51-81 9d fb 47 77 00 51 61</uuid>
    <labels>
      <label name='cfprofile' rev='322' version='6'>rhel4_all</label>
        <label name='install_mode'>kickstart-net</label>
      <label name='cubit_state'>Allocated</label>
      <label name='cubit_alloc_time'>1170960674</label>
      <label name='cubit_state_mtime'>1170963906</label>
      <label name='cubit_build_time'>1170963906</label>
      <label name='cubit_project'>zork</label>
      <label name='cubit_user'>grue</label>
      <label name='vmware-guest'>cu011.dev.cubitdemo.net</label>
      <label name='cubit_lom_addr'>cu011.dev.cubitdemo.net</label>
    </labels>
    <groups>
      <aigroup>DEFAULT</aigroup>
    </groups>
    <network>
      <routing>
        <default>
          <ipv4_addr>192.168.202.1</ipv4_addr>
         </default>
      </routing>
         <interface>
             <name>eth0</name>
             <sol_name>e1000g0</sol_name>
             <mac_addr>00:50:56:00:00:01</mac_addr>
             <bootproto>static</bootproto>
             <addr>
                 <ipv4_addr>192.168.202.23</ipv4_addr>
                 <ipv4_mask>255.255.255.0</ipv4_mask>
                 <dnsname>cu013.dev.cubitdemo.net</dnsname>
             </addr>
         </interface>
    </network>
    </host>
      </project>
    </cubit>
````

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### QueryMembership

Determine the projects and the hosts that the user has permission to access.

If name parameter is not passed, the permission details of the initiating user will be displayed. Only Lab Management Domain Admins are permitted to query users other than themselves.

#### URL

```shell
/cubit_api/1/query_membership
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **name** (zero or once)

  * The name of the user to get the permission details. This argument is optional, defaulting to the name of the user who you authenticate as. Only Lab Management Domain Admins are permitted to query users other than themselves.
  * Type: String

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

Here is a sample output where we query name=grue:

```shell
    <?xml version='1.0'?>
    <cubit version='1'>
      <user name="grue">
        <project name="testing">
          <summary>Cubit Testing</summary>
          <roles>CUBIT - Domain Admin</roles>
        </project>
        <project name="zim">
          <summary>invador</summary>
          <roles>CUBIT - Domain Admin</roles>
        </project>
        <project name="zork">
          <summary>For dorks</summary>
          <roles>CUBIT - Domain Admin</roles>
        </project>
      </user>
    </cubit>
````
    
#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### Status

Return the status of the Lab Management web service. This provides some indication of whether or not the Lab Management web service is working properly. The only status returned is `OK`.

### URL

```shell
/cubit_api/1/status
````

#### Authentication

This method does not require authentication.

#### Parameters

This method does not take any parameters.

#### Example Response

```shell        
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
    </cubit>
````

#### Response Codes

* 200 - ok

### StatusSigned

Return the status of the Lab Management web service, and the name of the authenticated user when authentication is used via a signed method.

This provides proof that the API, and authentication to the API are working properly. The only status returned is `OK`. If the authentication is not successful, you will get a `Permission Denied` error. If the API key is expired, you will get a `Permission Denied: API key expired` error.

### URL

```shell
/cubit_api/1/status_signed
````

#### Authentication

This method requires authentication using an API key.

#### Parameters

* **sig** (Required, once)

  * API authentication hash signature.
  * Type: String

* **userid** (Required, once)

  * The login name of the user initiating the request.
  * Type: String

#### Example Response

```shell        
    <?xml version='1.0'?>
    <cubit version='1'>
        <status>OK</status>
        <userid>grue</userid>
    </cubit>
````

In addition to returning the OK message, the username of the authenticated user is provided.

#### Response Codes

* 200 - ok
* 400 - Login failed / Insufficient permissions

### UserCanLogin

Given a userid and a hostname, return whether or not the user is authorized to login provided that the appropriate credentials are presented.

The HTTP response code will always be 200 for a successful query whether or not access is permitted. The document body will be text only, and contain one of the following:

 * **0** - no access
 * **1** - user level access
 * **2** - root level access
 * **3** - host owner access
 * **4** - project admin access

#### URL

```shell
/cubit_api/1/can_login
````

#### Authentication

This method does not require authentication.

#### Parameters

* **host** (Required, once)

  * The fully qualified hostname of the host to test for access.
  * Type: String

* **userid** (Required, once)

  * The Lab Management userid of the user to test for access.
  * Type: String

#### Example Response

```shell
3
````

#### Response Codes

* 200 - ok

### Use the TeamForge Lab Management API {#teamforgelabmanagement}

The Lab Management Web Services API is a set of callable methods that enable your build and test systems to integrate with Lab Management's capabilities to manage infrastructure for software development.

The API requires a client which speaks at least HTTP, if you are going to be making requests only from the secure local network that Lab Management nodes are located on. HTTPS support is required to make API requests from anywhere else. It is recommended that you use HTTPS for your API requests whenever possible.

The Lab Management API is implemented as a client distributed with Lab Management, `cubit_api_client.py`. This client runs on any platform that Python runs on. Pre-compiled executables, which do not require Python, are available for Windows. The client is open-source, and you are free to modify it and redistribute it in accordance with its license terms. You can use it to build the basis of your own client in Python or any other language

 {% include note.html content="Use of Lab Management's Web Services API is governed under the same terms as your use of the rest of TeamForge Lab Management. While we do not place any restrictions on the number of API calls any user can make in any time period, we request that users make use of only the API calls that they really need, and we reserve the right to limit the access of users who overuse the service." %}

 1. Generate a new API key or view your current API key from your Lab Management **Start** page.

    {% include important.html content="Your API key allows you to execute any API calls within Lab Management as you, as if you were logged into the Web interface. Keep your key safe using the same types of precautions you would use for your password." %}

 2. Set yourself up to use _signed_ API methods. Lab Management API methods are _signed_ to avoid embedding your API key in the URL body of requests and keep it secure from snooping.

    1. Make a request to the server for a _token_. This will be used along with your API key to encrypt the arguments.

    2. Encode the arguments into a hash using a known secret (your API key, plus your token). We call this hash the _signature_.

    3. Make a second request to the server, passing the _signature_ and the list of _key/value argument pairs_. If your key/value pairs contain unicode data, the hashed list of arguments must be UTF-8 encoded, otherwise, UTF-8 encoding of the argument hash is optional.

 3. To use a signed method, pass the following command-line options to the `cubit_api_client.py` program:

    <table>
    <tr>
    <td><b>-s</b></td>
    <td>This indicates that the method is a signed method, and an authentication should be performed.</td>
    </tr>
    <tr>
    <td><b>--api-user|-u username</b></td>
    <td>This argument specifies the username to authenticate as.</td>
    </tr>
    <tr>
    <td><b>--api-key|-k api_key</b></td>
    <td>This argument specifies your API key. You can generate and view your API key from your Lab Management Start Page. You can change your API key at anytime independently of your Lab Management password.</td>
    </tr>
    </table>

    In addition to these required arguments, most web services require other parameters. These are specified as space-separated key=value pairs. For example, consider the following command, which will allocate the host "cu012.cubit.domain" to the user "alice" in the project "webtesting", while authenticating as the user "bob" with bob's API key:

    ```shell
    cubit_api_client.py --api-url=http://cubit.domain/cubit_api/1 --api-user=bob --api-key=713cdf90-2549-1350-80c3-2d0bcf9a1142 -s alloc_host  host=cu012.cubit.domain alloc_user=alice alloc_proj=webtesting
    ````
 4. To use an unsigned method, fetch the following URL: `https://<cubit.domain>/cubit_api/1/status"/>`(where `<cubit.domain>` is the domain name of your Lab Management site).

    {% include tip.html content="The `status` method is the most basic of all the API methods, and will always return an OK string as a response." %}

    To demonstrate the unsigned status method with `cubit_api_client.py`:

    ```shell
    cubit_api_client.py -l http://cubit.domain/cubit_api/1 status
                        cubit_api_client.py: OK
    ````
    
    Again, this time with XML output:

    ```shell
    cubit_api_client.py -l http://cubit.domaincubit_api/1 --xml status
                        <?xml version='1.0'?>
                        <cubit version='1'>
                        <status>OK</status>
                        </cubit>
    ````

## Is the Digital.ai TeamForge SOAP API backward-compatible?

The Digital.ai TeamForge Enterprise Edition 5.x and Digital.ai TeamForge Enterprise 6.x APIs (including Service Pack updates) are fully compatible with Digital.ai TeamForge.

Applications developed using these earlier APIs will continue to function after you upgrade to Digital.ai TeamForge. A release of Digital.ai TeamForge may be accompanied by updates to the API. These changes are always backward compatible with earlier versions of the API. However, the calls from the different API versions are not interchangeable.

* For updates and patch releases, existing methods are incremented, not overwritten. For example, if an update is made to the `createDocument` method, it is reflected in a new method `createDocument1`. You do not have to update your existing applications to reflect a new API with any Service Pack or Hot Fix release.

* For a major Digital.ai TeamForge release, such as this 18.0 release, updates are merged into a new API version. At this point, if you want to use the new API calls, you must update your existing applications.

## How should my API client store user passwords?

Any reputable method of storing passwords will work, as long as your site is protected by SSL.

All client tools rely on the TeamForge SOAP API for authentication, and therefore use whatever authentication method TeamForge is using.

 {% include important.html content="Because SOAP is simply XML transmitted over HTTP, all values are sent in clear text. For that reason it is very important that your TeamForge site be SSL-enabled and protected by server-side SSL certificates. This will ensure that any usernames or passwords sent from a client tool will be encrypted." %}

Many standalone client tools are able to cache a copy of the user's credentials to make it easier for them to access the site. The CollabNet Eclipse Desktop stores passwords in the encrypted Java keystore, and the CollabNet Windows clients use the Windows keystore.

CollabNet's Subversion clients and other Subversion clients, such as Tortoise and Subclipse, are also able to store user credentials. While CollabNet has no control over how third-party tools store such credentials, it our experience that the mainstream tools all use an appropriate keystore for secure storage of user credentials. CollabNet recommends that customers independently verify the storage methods of those tools and set a policy appropriate with their own security guidelines.

Subversion users on Linux systems have the option to use the Gnome keyring to securely store user credentials. CollabNet recommends that customers set their own policy for how their users should use the Linux Subversion client.

## How does an application interact with TeamForge SOAP services?

TeamForge exposes a subset of the APIs defined by the application server as web services, through the SOAP protocol.

### SOAP APIs

A SOAP proxy server and a SOAP API layer, both running on Apache Axis, expose a set of web services representing each TeamForge application.

The SOAP server provides the following functions:

 * Provides web services by accepting SOAP requests from the clients.
 * Performs SOAP client authentication.
 * Implements TeamForge role‐based access control (RBAC) and caching services.
 * Accesses the application server via RMI stubs.

While each TeamForge service has its own SOAP interface, interaction with all the services is designed to be as consistent as possible. The calls for each service are similar, although the data format and specific call parameters may be different.

For example, the following calls are consistent across all services:

 * list
 * get
 * set
 * delete
 * create

The call parameters, however, are different. For example:

 * When working with the CollabNet service, you might call `getProjectList(string sessionID)`.
 * When working with the TaskApp service, you might call `getTaskList(string sessionID, string taskFolderID)`.

### User-centric services

All services and APIs are user‐centric, meaning that all integrated applications must establish an individual connection to the SOAP server for each user. This differs from programming directly with an application server where one connection can be established for any number of users.

Activities that can be performed using the SOAP interface are by definition user‐based, such as retrieving a list of a userʹs projects, tasks, or assigned tracker artifacts. These activities therefore require an individual connection for each user.

Requiring individual connections also ensures that role‐based access control is checked for each action performed by each user. To ensure that security is enforced, RBAC checks are performed on each SOAP API call and cannot be disabled at the client level.

## How do I enable/disable path-based permissions via SOAP?

The Path Based Permissions (PBP) are handled via the *roleList, *Cluster methods of rbacAppSoap. To enable PBP, use the "scm_fgp" (fine grained permissions) argument to addCluster.

See the below psudeocode.

```shell

		    from com.collabnet.ce.soap60.webservices import *
            from com.collabnet.ce.soap60.webservices.ClientSoapStubFactory import getSoapStub
            from com.collabnet.ce.soap60.types import *
            
            hostname = "http://server/"
            username = "admin"
            password = "admin"
            project = "proj1007"
            roleName = "tracker"
            
            sfSoap = getSoapStub(cemain.ICollabNetSoap, hostname)
            sfSession = sfSoap.login(username,password)
            rbacAppSoap = getSoapStub(rbac.IRbacAppSoap, hostname)
            
            roles = rbacAppSoap.getRoleList(sfSession,project).getDataRows().tolist()
            roleId = None
            
            for row in roles:
            if row.getDescription() == roleName :
            roleId = row.getId()
            print "found tracker role, %s" % roleId
            
            if roleId == None:
            raise Exception("Cant find role ")
            
            clusters = rbacAppSoap.listClusters(sfSession, roleId).getDataRows().tolist()
            for row in clusters:
            print row.getFolderId(), row.getOperationClusterName()
            if row.getOperationClusterName() == "scm_commit":
            print "found target!"
            rbacAppSoap.removeCluster(sfSession, roleId, row.getOperationClusterName(), row.getFolderId())
            rbacAppSoap.addCluster(sfSession, roleId, "scm_fgp", row.getFolderId())
            
            sfSoap.logoff(username,sfSession)
````

{% include links.html %}