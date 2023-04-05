---
title: Custom Event Handlers in TeamForge
keywords: teamforge, extend, api
tags: [ctf_203, extend_teamforge, customize]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforgecustomeventhandlers.html
last_updated: Aug 27, 2020
layouts: "pagefaqs"
summary: You can create custom workflows in TeamForge using custom event handlers.
---

## How TeamForge Custom Event Handlers Work?

The TeamForge custom event handling framework allows third-party event handlers to register for TeamForge-specific application events and notifies them whenever such an event occurs.

The event handling framework implements an extended flavor of the observer pattern. The TeamForge application events are triggered whenever a property of a TeamForge object (e.g. tracker item, discussion item, wiki page) has been changed or is going to be changed, if no event handler objects (i.e. blocks the event).

For example, you can block deletions of projects for all users, add a comment to a tracker item whenever an association has been modified, or design your own tracker workflow engine.

Writing custom event handlers requires at least some basic knowledge in the Java programming language or (if you use the examples shipped with this post) a script language that is installed on the TeamForge server, such as shell, Python, or Perl. For these instructions, we'll assume that you are familiar with basic programming techniques.

The event handler framework differentiates between two types of events:

 * **Asynchronous** - If a handler registers for asynchronous events, it is informed that a change has just happened. The handler can decide to trigger further changes by calling TeamForge web services, but it cannot block the change because it has already happened.

Asynchronous event handlers are good for triggering system events, such as changing an artifact status or sending an email. See [Using an Asynchronous Event Handler: Trigger Follow-up Events][teamforgecustomeventhandlers.html#asynceventhandler].

 * **Synchronous** - If a handler has registered for synchronous events, it gets informed whenever a change has been anticipated by a user. It can examine the properties that should be changed and decide whether to accept the change or block it. A synchronous event handler cannot trigger further changes on the currently processed object, since other handlers in the event handler chain must also have the chance to block the anticipated change.

 A synchronous event handler is the appropriate way to show an alert directly in the TeamForge UI, for example. See [Using a synchronous event handler: Send event handler output to the TeamForge UI][teamforgecustomeventhandlers.html#synceventhandler].

Technically, all event handlers have to be part of a Java archive (JAR) file with a TeamForge specific deployment descriptor that describes which events should be intercepted. This JAR file then has to be uploaded to the TeamForge application server. No restart is necessary, but the event handling cache has to be refreshed.

In practice, you can customize a TeamForge site's behavior without any knowledge of Java if you can write scripts in a language that can deal with environment variables, write to standard out/error (to control what will be displayed in the TeamForge UI as result of the handler’s execution) and control the return code (to decide whether to block the event or not).

We will show you how to come up with your own custom event handlers based on a couple of examples.

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">
If you are starting to create or customize an event handler, you need to have the code set up. All the examples described here are available in a Maven module format, inside the TeamForge installation directory located at `/opt/collabnet/teamforge/dist/static-files/apidoc/sdk-package.zip`.
</div>
</div>

## Event Handler Example - Comment on Associations {#commentonassociations}

This event handler adds a comment to a tracker item whenever an association is added to or deleted from this tracker item.

This example illustrates how to intercept a specific event, trigger a follow-up action by calling TeamForge web services, and add a comment based on the formatting template which is specified as part of a property file.

The code for this example can be found at `/opt/collabnet/teamforge/dist/static-files/apidoc/sdk-package.zip`.

 {% include tip.html content="You can just extract it with your favorite zip program and have a look at the files that are part of it." %}

 1. When you extract the ZIP file you'll find a structure like this: `com/vasoftware/sf/plugin`. This directory contains the class file of your event handler. There may be additional directories containing Java class files. If you like to include Java libraries, you have to unpack their JAR files and add their class files (including directory structure) in the event handler JAR. 

    The `META-INF/config.properties` file contains the events and operations your handler class will intercept. It is also common to have additional files in the META-INF directory, such as property files to control the behavior of the event handler.

    This example event handler is provided as-is (i.e. not supported as part of any TeamForge release). As with all event handlers, use it at your own risk. CollabNet cannot guarantee any SLAs on third-party code.

     {% include tip.html content="If you want to change the behavior of custom event handlers at runtime (without redeploying the JAR file), you may want to look at the TeamForge integration data API. For the purpose of this example, we will stick with property files." %}

 2. In the `AsynchronousRelationshipEventListener.java` file, you can find some code like this:

    ```shell
    @EventListener(version = SoapVersion.SOAP_60)
    public class AsynchronousRelationshipEventListener {

        @Asynchronous(topic = {"object.Relationship.*"}, user="system")
        public void addCommentToArtfOnAssociation(final EventContext context) throws Exception {
            ...
        }
    }
    ````

   This tells the event handling framework that the class `AsynchronousRelationshipEventListener` is responsible for intercepting events of type `Relationship` (aka associations) for every possible operation. The handler will be called after the event has happened (asynchronous mode) and the passed data structures will be compatible with the events format defined in TeamForge SOAP60. The topic property indicates the object type and operation you are interested in.  Object types in TeamForge are User, Project, Role, Tracker, Artifact, DocumentFolder, Document, and so on. If you only want to intercept certain operations, you can specify those instead of the wildcard character (*). For example, `object.Relationship.create`. Supported operations are usually create, update, move and delete, but every event has its own operations.

 3. The `config.properties` file is used to control the formatting of the comment that gets added when an association has been modified. The initialize-method of the handler class (`AsynchronousRelationshipEventListener`) shows how property files can be parsed within a custom event handler.

 4. By default, the user triggering the event is also the user executing the event handler. If you want to run your event handler with a different user account, specify it in the user property, like this:

    ```shell
    @Synchronous(topic = {"object.Relationship.*"}, user = "foo")
    public void addComment(final EventContext context) throws Exception {
         ...
    }
    ````

    {% include note.html content="Be careful with this option, because running code on behalf of a different user opens the door for all kind of exploits if you do not check the user’s input properly. Also, this option will not allow you to access the original user’s session id any more, but you can always create a new session with a super user account (credentials saved in a property file) if you have to." %}

## Event Handler Example - Execute a Hook Script

When a TeamForge event arrives, this event handler looks to see whether there is a script in the TeamForge file system with the name/operation of the event, and then calls that script with all information from the event contained within environment variables.

This example illustrates how to intercept arbitrary TeamForge events, examine the event’s properties, map them to system environment variables and call a script in the file system with a name corresponding to the intercepted event.

You can use this event handler to customize your TeamForge site’s behavior without any knowledge of the Java programming language as long as you can write scripts in a language that can deal with environment variables, write to standard out/error (to influence what will be displayed in TeamForge’s UI as result of the handler’s execution) and influence the return code (to decide whether to block the event or not).

The code for this example can be found at `/opt/collabnet/teamforge/dist/static-files/apidoc/sdk-package.zip`.

 {% include tip.html content="You can just extract it with your favorite zip program and have a look at the files that are part of it." %}

 1. When you extract the ZIP file you'll find a structure like this: `com/collabnet/ctf/events`. This directory contains the class file of your event handler. There may be additional directories containing Java class files. If you like to include Java libraries, you have to unpack their JAR files and add their class files (including directory structure) in the event handler JAR.

   This example event handler is provided as-is (i.e. not supported as part of any TeamForge release). As with all event handlers, use it at your own risk. CollabNet cannot guarantee any SLAs on third-party code.

   {% include tip.html content="If you want to change the behavior of custom event handlers at runtime (without redeploying the JAR file), you may want to look at the TeamForge integration data API. For the purpose of this example, we will stick with property files." %}

 2. In the `SynchronousHookScriptEventListener` file, you can find some code like this:

    ```shell
    @EventListener(version = SoapVersion.SOAP_60)
    public class SynchronousHookScriptEventListener {

        @Synchronous(topic = {"*.*"})
        public void executeHookScript(final EventContext context) throws Exception {
            ...
        }
    }
    ````

    These lines tell TeamForge to register two event handlers, one asynchronous (`AsynchronousHookScriptEventListener`) and one synchronous (`SynchronousHookScriptEventListener`) for arbitrary events (wildcard *).

 3. By default, the user triggering the event is also the user executing the event handler. If you want to run your event handler with a different user account, specify it in the user element, like this:

    ```shell
    @Synchronous(topic = {"*.*"}, user = "foo")
    public void executeHookScript(final EventContext context) throws Exception {
         ...
    }
    ````

    {% include note.html content="Be careful with this option, because running code on behalf of a different user opens the door for all kind of exploits if you do not check the user’s input properly. Also, this option will not allow you to access the original user’s session id any more, but you can always create a new session with a super user account (credentials saved in a property file) if you have to." %}

It is possible to register multiple handlers for different events, but you can also use one handler to intercept both synchronous and asynchronous events.

## Event Handler Example - Hook Scripts

These sample hook scripts should give you an idea how custom event handlers can be written. Feel free to adjust them to your own needs.

 {% include note.html content="These sample event handlers are not officially supported by CollabNet and must be used at your own risk." %}

 * Hooks must be owned by `sf-admin` for security, and must have the executable bit set.

 * To configure a site to prevent projects being deleted, we could create this file: `/opt/collabnet/teamforge/hooks/synchronous/project_delete`

 ```shell
 #!/bin/sh
 echo Sorry, projects cannot be deleted on this site 1>&2
 exit 1
 ````

 * To automatically create an initial directory structure in an SVN repository when the repository is created, you might create this file: `/opt/collabnet/teamforge/hooks/asynchronous/repository_create`

 ```shell
 #!/bin/sh
 /usr/bin/svn
 mkdirhttp://localhost/svn/repos/${tf_original_RepositoryDirectory:9:999}/trunk
 http://localhost/svn/repos/${tf_original_RepositoryDirectory:9:999}/tags
 http://localhost/svn/repos/${tf_original_RepositoryDirectory:9:999}/branches
 -m "Inital Structure"
 --username admin --password mypassword --non-interactive --no-auth-cache
 exit 0
 ````

## Event Handler Example - SOAP to REST Compatibility

{% include warning.html content="This example event handler is not intended for production use as-is." %}

This example illustrates the ability of a custom event handler to make both SOAP and REST calls.

<div class="panel panel-info">
<div class="panel-heading">TeamForge REST Clients Can Use SOAP Session Keys</div>
<div class="panel-body" markdown="1">
<!-- https://forge.collab.net/sf/go/artf318318 -->
The SOAP session key has been enhanced in TeamForge 19.0 to support REST API calls as well. With this enhancement, SOAP clients can now invoke TeamForge REST APIs using existing SOAP session keys.
</div>
</div>

This example listens to a Project Creation event and then creates a new Tracker with randomized
details, like a default templated tracker.

The code for this example can be found [here](https://ctf.open.collab.net/sf/frs/do/viewRelease/projects.ccf/frs.teamforge_evenet_handlers.soap_to_rest_compatibility).

## Event Handler Example - Artifact Update Validator

{% include warning.html content="This example event handler is not intended for production use as-is." %}

This example illustrates the ability of a custom event handler to validate artifact update activities.
Basically, it makes sure that the users of the site wont be able to update an artifact if it's in
`Closed` meta-status.

This example listens to artifact update events and then fails the update if the artifact is
in `Closed` meta-status. The user can only update the artifact after re-opening it.

The code for this example can be found at `/opt/collabnet/teamforge/dist/static-files/apidoc/sdk-package.zip`.

The folloiwng table lists the topics of TeamForge event object types:

| TeamForge Object | Topics |
| ------------- |-------------|
| User | `object.user.create`<br>`object.user.update`<br>`object.user.delete` |
| UserGroup | `object.group.create`<br>`object.group.update`<br>`object.group.delete` |
| GroupMembership | `GroupMembership.addMember`<br>`GroupMembership.removeMemer` |
| Project | `object.project.create`<br>`object.project.update`<br>`object.project.delete` |
| ProjectMembership | `ProjectMembership.addMember`<br>`ProjectMembership.removeMember` |
| Role | `RoleEvent.create`<br>`RoleEvent.update`<br>`RoleEvent.delete` |
| RoleMembership | `RoleMembership.addMember`<br>`RoleMembership.removeMember` |
| RoleGroup | `RoleGroup.add`<br>`RoleGroup.remove` |
| Field | `object.field.create`<br>`object.field.update`<br>`object.field.delete` |
| Team | `object.team.create`<br>`object.team.update`<br>`object.team.delete` |
| Relationship | `object.Relationship.create`<br>`object.Relationship.update`<br>`object.Relationship.delete` |
| Tracker | `object.folder.Tracker.create`<br>`object.folder.Tracker.update`<br>`object.folder.Tracker.delete`<br>`object.folder.Tracker.move` |
| PlanningFolder | `object.folder.PlanningFolder.create`<br>`object.folder.PlanningFolder.update`<br>`object.folder.PlanningFolder.delete`<br>`object.folder.PlanningFolder.move` |
| DocumentFolder | `object.folder.DocumentFolder.create`<br>`object.folder.DocumentFolder.update`<br>`object.folder.DocumentFolder.delete`<br>`object.folder.DocumentFolder.move` |
| Discussion | `object.folder.Forum.create`<br>`object.folder.Forum.update`<br>`object.folder.Forum.delete` |
| Discusson Topic | `object.folder.Topic.create`<br>`object.folder.Topic.update`<br>`object.folder.Topic.delete` |
| Artifact | `object.item.Artifact.create`<br>`object.item.Artifact.update`<br>`object.item.Artifact.delete`<br>`object.item.Artifact.move`<br>`object.item.Artifact.cloned`<br>`object.item.Artifact.commentEdit` |
| Document | `object.item.Document.create`<br>`object.item.Document.update`<br>`object.item.Document.delete`<br>`object.item.Document.move` |
| Discussion Post | `object.item.Post.create`<br>`object.item.Post.update`<br>`object.item.Post.delete` |
| Wiki | `object.item.WikiPage.create`<br>`object.item.WikiPage.update`<br>`object.item.WikiPage.delete` |

 * There are some interesting methods of the EventContext class you can call:

     * **EventContext** - A data structure containing the event topic, operation, project, comment and user name.

     * **getSessionKey** - Returns a session id of the user that is going to (synchronous handler) / has triggered (asynchronous handler) the event we just intercepted. If you used the user property, it will contain a session id for the user you specified there.

     * **getOriginalData** - In case of a synchronous event handler, this will return a representation of the object the event is going to change. In case of an asynchronous event handler, this will return the representation of the object before it was changed by the event. The data structure used to represent the object is the same that would have been used in CollabNet’s SOAP API.

     * **getUpdatedData** - In case of a synchronous event handler, this will return a representation of the object how it will look after the event has happened (you can still block it). In case of an asynchronous event handler, this will return the representation of the object after it was changed by the event.


   Let’s assume a user wants to change the priority of a tracker item from 3 to 4. If you have registered a synchronous event handler, this one is triggered before the change can actually be performed. `getOriginalData` returns an `ArtifactSoapDO` object of the tracker item with the priority field set to 3. `getUpdatedData` contains an `ArtifactSoapDO` object of the tracker item with the priority field set to 4.

     * If you block the event (by throwing an exception), the change does not happen and the user is presented with an error message. (See next section for how to influence this error message.)

     * If you do not block the event (by just returning from the processEvent method), all registered asynchronous handlers are called. `getOriginalData` and `getUpdatedData` contain exactly the same objects as in the synchronous case. However, the semantic is different: They are no longer representing the current and anticipated state, but the previous and current state of the object in question.


 * The following code snippet (taken from our "Hook script" event handler example) shows how to retrieve all the information available to an event handler.

 ```shell
 String topic = context.getTopic();
 String operation = context.getOperation();
 String projectId = context.getProjectId();
 String comment = context.getComment();
 String userName = context.getUsername();
 String originalDataClassName = context.getOriginalData().getClass().toString();
 String updatedDataClassName = context.getUpdatedData().getClass().toString();
 Object originalData = context.getOriginalData();
 Object updatedData = context.getUpdatedData();
 ````

Example Custom Event Handler java file:

 ```shell
 package your.event.handler.path;

 import com.collabnet.ce.soap60.webservices.tracker.ArtifactSoapDO;
 import com.collabnet.ctf.events.Asynchronous;
 import com.collabnet.ctf.events.EventContext;
 import com.collabnet.ctf.events.EventListener;
 import com.collabnet.ctf.events.SoapVersion;

 @EventListener(version = SoapVersion.SOAP_60)
 public class AsynchronousListenerSample {

     @Asynchronous(topic = {"object.item.Artifact.update"}, user = "system")
     public void sendEmail(final EventContext context) throws Exception {
         String projectId = context.getProjectId();
 
         ArtifactSoapDO originalDO = (ArtifactSoapDO) context.getOriginalData();
         ArtifactSoapDO updatedDO = (ArtifactSoapDO) context.getUpdatedData();
         String artifactId = updatedDO.getId();
         context.logInfo("Send Email:" + artifactId);

         String sender = "John";
         String senderAddress = "foo@domain.com";
         String recipient = "David";
         String toAddress = "bar@domain.com";
         String subject = artifactId + ": " + updatedDO.getTitle();
         String subject = artifactId + ": " + updatedDO.getTitle();
         String body = updatedDO.getDescription();
         context.sendHtmlEmail(sender, senderAddress, recipient, toAddress, subject, body, null);
     }
 }
 ````

## Using a Synchronous Event Handler: Send Event Handler Output to the TeamForge UI {#synceventhandler}

When we have extracted all data available to the event handler, how do we interact with the user interface?

 {% include note.html content="Only synchronous event handlers can directly communicate with the UI, because if the event has already happened (as it has, in the case of asynchronous handlers), the user who triggered the event may already have been logged out." %}

 * You use three independent actions to interact with the TeamForge UI:

    1. Add a success message to the UI that gets displayed as the result of the action just triggered by the user. This can be done by calling the `addSuccessMessage` method of the `EventContext` class (see SynchronousHookScriptEventListener.java of example two for details).

    2. Add an error message to the UI that gets displayed as the result of the action just triggered by the user. This can be done by calling the `addErrorMessage` method of the `EventContext` class.

    3. Block the event you intercepted. This can be done by throwing an exception in your event handler method. The payload of your exception will be displayed in the UI.


   All three forms of UI feedback can be used in combination. For example, it is possible to display an error message even if you did not block the event, and it is possible to show many error and success messages together.

* What happens if the event in question was not triggered by a user logged into the TeamForge Web UI but by a client using the TeamForge web services?

In this case, error and success messages do not reach the SOAP client. However, the payload of the exception object thrown when the event was blocked is delivered as part of the SOAP fault element.

* While synchronous event handlers enable you to block events and/or to provide additional feedback to the currently logged in user, they should not be used to trigger follow-up actions (like changing TeamForge artifacts or interacting with external systems).

Remember that these handlers are running in the main TeamForge event loop and nothing else will happen until you return from your event handler method, so return as fast as you can.

## Using an Asynchronous Event Handler: Trigger Follow-up Events {#asynceventhandler}

Use an asynchronous event handler to communicate with TeamForge, external systems, processes or system resources.

 {% include important.html content="To avoid accidentally locking the main TeamForge event queue down (and essentially rendering the system unusable), use only asynchronous event handlers (not synchronous event handlers) to trigger events." %}

Interacting with TeamForge is done as you would do it if you had to write a Java program to interact with TeamForge using its web services API. The only difference is that you will connect to `localhost` (since your handler is running locally) and that you already have a valid session ID.

 * You do not have to include the SOAP SDK classes in your event JAR file, because they are already in the TeamForge class path. This code snippet extracted from our association converter example ([Event Handler example: Comment on Associations][/teamforgecustomeventhandlers.html#commentonassociations]) shows how to do it:

 ```shell
 ITrackerAppSoap trackerClient = (ITrackerAppSoap) ClientSoapStubFactory.getSoapStub(
 ITrackerAppSoap.class, "http://localhost:8080");
 ...
 ArtifactSoapDO artifact = trackerClient.getArtifactData(getSessionKey(), originId);
 trackerClient.setArtifactData(getSessionKey(), artifact, finalComment, null, null, null); 
 ````

 {% include tip.html content="You may use external libraries in your event handler by placing their `.class` files into your event JAR file. The only tricky part is if TeamForge is using a different version of this library (which will take precedence). In this case, you would have to recompile your library with a different package namespace." %}

 * Using the session key provided by the event handler is actually only going to work if the SOAP call you are using is not throwing an exception. The session ID passed into your handler is associated with an already running transaction that will be aborted if an exception is thrown as part of this session. Part of rolling back the transaction is rolling back the JVM’s call stack which contains your event handling code, so you will not be able to catch the web services exception. If you like to to handle web service exceptions, you have to create your own session id by logging into TeamForge again by calling ICollabNetSoap.login with some credentials stored as part of your handler. (You can store them in a property file in the META-INF directory.)

## Best Practices for Working with Custom TeamForge Event Handlers

In general, watch out for deadlocks and favor asynchronous over synchronous event handlers.

### Beware of Deadlocks

Having custom event handlers that modify other objects can be dangerous if there it is possible for that handler or another handler to chain in the opposite direction. An example of this is an event handler that updates a task when an associated artifact is updated and updates the artifact when the associated task is updated. It is possible for two users to modify each object at the same time causing the two event handlers to wait on each other. The task handler would have a lock on the task bean in the application server while the artifact handler would have a lock on the artifact bean. When the custom event handlers fired, they would wait for the locks to be released but since the two threads have the locks each other needs and are waiting on the opposite objects, a deadlock would occur.

### Asynchronous is Safer

Custom event handlers will be the least worrisome when they are responsible for data validation or secondary object creation (or association creation). Object modification is possible but adds greater complexity due to the risks involved with locking multiple objects across many threads. If you are unsure, use asynchronous handlers to modify objects instead since the lock on the original object will be gone by the time the asynchronous handler is executed.

Calling and waiting for synchronous hooks currently doesnt have a timeout. As long as your synchronous hook is running, the whole TeamForge site will be blocked for all users accessing the site. Some events trigger other events. For example creating a project actually calls the create project hook, wiki page hooks, and so on. Badly written or slow hooks can cripple a site.

### Write to a File

Write your diagnostics messages in a file and not on stdout/stderr, since TeamForge does not read from stdout/stderr before the script completes. In the case of synchronous hooks, this could lead to a situation where the script blocks because the pipes buffer between the script process and the TF process is completely filled.

### No Cascading

Due to the nature of custom event handling, custom events cannot cascade. This means that if a custom event handler catches an event and creates an object that it or another custom event handler would normally process, the event bypasses the custom event handlers. This is to prevent looping and infinite object creation. While there are ways for event handlers to avoid this, it would be a fairly difficult task since all of your event handlers would have to use a circular event detection algorithm. Rather than adding that complexity, we just eliminated the possibility.

### Event Handler Life Cycle

For every single call to the processEvent method, a new object of your class will be instantiated. A best practice to avoid costly reinitialization every time (remember that the TeamForge event loop thread is blocked while you are doing this) is to delegate all synchronization work to a method you always call in your constructor which checks a static variable whether the initialization has already been done and if not, just returns without any further action (code snippet from example one):

```shell
private static boolean initialized = false;
public  AsynchronousRelationshipEventListener() {
initialize();
}

private synchronized void initialize() {
if (initialized ) {
return;
}
initialized = true;
// proceed with initialization
...
}
````

Logging in into TeamForge and initializing network connections file resources are costly operations that should be handled in such a method instead of doing it all over again.

### Event Spooling

While it is true that asynchronous handlers may consume considerably more time than synchronous ones, there is only one thread for those handlers, so events may queue up if you do expensive operations. A best practice is to capture the event in your asynchronous event handler, write all necessary information to the local file system (comparable to a mail spooling directory) and return. At the same time, you can have a separate application reading from the spooling directory. This way, you never get into a situation where you miss TeamForge events, or things queue up just because you run into a blocking operation.

### Incremental Changes

The event handler parser is really picky on the exact format of your JAR file. A best practice is to base your work on an already existing event handler and then adapt it to your own needs by doing incremental changes while checking whether it still works.

### Watch out for Loops

Your follow-up actions may trigger your handler to be called again. You have to protect your handler from an infinite update loop if that happens. A best practice is to add a check to your event handler to see whether the user initiating the event is the same user you are using to perform follow-up actions.

### Roll Back Sparingly

Throwing an exception in a synchronous event handler blocks the intercepted event and rolls back the transaction associated with the change. Rolling back transactions also means that the data the user entered is not saved. If this happens accidentally due to a wrongly programmed event handler, it can be frustrating to your users, so make sure that you only throw exceptions in your handler code when you really want to enforce the rollback.

### Catch Errors Generically

It is quite easy to miss an exception you did not expect (like a null pointer exception, parsing exception, time out exception, any other malfunction in your own code). A best practice is to introduce a generic catch block in your handler and only rethrow the exception if it was an intended exception (see SynchronousHookScriptEventListener):

```shell
} catch (Exception e) {
 if (!intendedException) {
 log.error("Exception occured: " + e.getMessage(), e);
 } else {
...
 throw e;
 }
 }
````

{% include links.html %}