---
title: Associate Tracker Artifacts
keywords: associate tracker artifacts with documents, associate tracker artifacts with tasks, associate tracker artifacts with integrated applications, associate tracker artifacts with forums, associate tracker artifacts with a file release, associate tracker artifacts with a code commit
tags: [ctf_20.2, project_member_tasks, trackers, associations]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jul 13, 2020
permalink: trackers-associatingtrackerartifactswithotheritems.html
summary: You can connect tracker artifacts with other Digital.ai TeamForge items such as documents or topics. Creating associations between items enables you to define relationships, track dependencies, and enforce work flow rules.
---

## Associate a Tracker Artifact with a Document, Task, Integrated Application Object, or Forum

When a tracker artifact is related to other TeamForge items, such as tasks, documents, integrated application objects, or discussions, you can connect the tracker artifact to the other item by creating an association.

Creating associations between items helps you to define relationships, track dependencies, and enforce work flow rules.

1. Click **Trackers** from the **Project Home** menu.
2. On the list of project trackers, find the tracker artifact with which you want to create an association. Use the filter if needed.
3. Click the artifact title.
4. On the **View Artifact** page, click the _Associations_ tab. The list of existing associations appears.
5. Click **Add**.
6. In the **Add Association Wizard** window, select the items with which you want to associate the artifact:
   * **ENTER ITEM ID** -  If you know the item's ID, you can enter it directly.
     {% include note.html content="To associate an object in an integrated application from within TeamForge, use the `[<prefix_objectid>]` format. Successful associations appear hyperlinked. Each integrated application displays its prefix on moving the mouse over the application name in the tool bar." %} 
   * **ADD FROM RECENTLY VIEWED** - Select one of the last ten items you looked at during this session.
   * **ADD FROM RECENTLY EDITED** - Select one of the last ten items you changed.
7. Click **Next**.
8. You may add a comment in the **ASSOCIATION COMMENT** text box.
9. Save your work.
   * Click **Finish and Add Another** to add additional associations.
   * Click **Finish** to return to **Details** page.  
10. Click the _Associations_ tab to view a graphical representation of all the associated items. Through the Association Viewer, you can choose to view associations in the form of a list or flip over to the Trace view to explore the layers of associations (including parent/child dependencies) laid out in a timeline. You can scroll across the Trace view by dragging the mouse over the association layer or use the 'Previous' and 'Next' arrows to view all the objects as events in a timeline.

While the _Associations_ tab shows the count of the total number of associations, you can only view the most recent 500 associations when you click the _Associations_ tab in case the artifact has more than 500 associations. You can, however, browse through the Association Viewer to view older associations.

You can click on each node on the graphical association viewer to filter and display the associated items in the table below the association viewer thus matching the number of associations provided on the selected node. For example, if the node that you select for filtering is having two associations on it, the table displays the two associated items as a result of the filtering process.

## Associate a Tracker Artifact with a File Release

To track the source and resolution of a bug or a feature request, associate its tracker artifact with the file release in which it was discovered and fixed.

Tracker artifacts associated with file releases are also displayed separately, providing a simply way to track all issues that were discovered in or fixed in a specific file release.
   {% include tip.html content="You can also add associations from the tracker artifact's **View Artifact** page." %}

1. On the **Project Administration** page, enable both the **REPORTED IN RELEASE** and **FIXED IN RELEASE** fields.
   * **REPORTED IN RELEASE** - When submitting a new artifact, the user can choose from a drop-down list of all releases in the project to identify the release in which the issue was discovered.

   * **FIXED IN RELEASE** - After the issue is fixed, the user can choose from a drop-down list of all releases in the project to identify the release in which the issue was fixed.

   {% include tip.html content="If either of these fields says `Unknown`, the artifact you are working on may be associated with a file release that you don't have permission to view. You can leave that as it is or change it to a file release that you do have permission to view." %}

2. When submitting a new artifact, choose the release in which the issue was discovered from the **REPORTED IN RELEASE** drop-down list. The drop-down list shows all releases in the project, except those that are in **pending** status.

3. After the issue is fixed, update the artifact by choosing the release in which the issue was resolved from the **FIXED IN RELEASE** drop-down list. The drop-down list shows all releases in the project, except those that are in **pending** status.

The associated tracker artifacts are displayed on the **View Release** page, in the **REPORTED TRACKER ARTIFACTS** and **FIXED TRACKER ARTIFACTS** sections.

## Associate a Tracker Artifact with a Code Commit

When checking in files to your SCM repository, you can create links to one or more tracker artifacts or other Digital.ai TeamForge items.

Associations track the links between code and the bugs, feature requests, or other tracker artifacts that the code addresses. You can also associate code commits with other TeamForge items, such as tasks or documents.

A project administrator can make associations mandatory for all code commits. When this is made mandatory, the following additional rules pertaining to code commit can also be set:

   * Code commits can be performed only for open artifacts.
   * To perform a code commit, the committer must be the owner of the specific artifact.

   {% include note.html content="Once you enforce the above rules, validations are strictly enforced for commits against tracker artifacts only. In case you commit against any other TeamForge object, for example a wiki or a document, mere existence of the object ID ensures successful commit and association and no validations are performed against the status of the object or who it is assigned to." %} 

You can create tracker artifact associations from whatever interface you normally use to check code into your SCM repository. You do not have to log into TeamForge.

Use the same syntax for commits to Subversion repositories.

When making a code commit, add the associate command in the commit message like this: `[<item id>]`, such as the TeamForge tracker artifact ID or task ID.
    
   * TeamForge item IDs are always letters followed by four or more numbers, such as `task1029` or `artf10011`.
   * To associate a commit with multiple TeamForge items, separate the item IDs with commas.
   * All associations are displayed in the _Associations_ tab of the **Commit Details** page.
   * The **Comment** section lists the comments made with each commit.

{% include note.html content="To associate an object in an integrated application, use the `[<prefix_objectid>]` format. Each integrated application displays its prefix or moving the mouse over the application name." %}

{% include note.html content="When an association is added to or removed from TeamForge objects such as tracker artifacts, tasks, documents, discussions, and file releases, a notification mail is sent to users monitoring these objects. A option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings](siteadmin-configuresiteviaui.html)." %}  

{% include note.html content="To remind yourself of the details of the association later, look in the _Change Log_ tab of the associated **View Artifact** page." %} 


{% include links.html %}