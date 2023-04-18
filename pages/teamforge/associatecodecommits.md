---
title: Associate Code Commits
keywords: manage source code, get the code, view code commits, associate code commits with other items, create a source code repository, delete a source code repository, replicate a repository, check command history, check out code, review code, search code
tags: [ctf_20.2, project_member_tasks, source_code, git_gerrit, scm, associations]
sidebar: teamforge_sidebar
last_updated: Jul 10, 2020
permalink: associatecodecommits.html
folder: teamforge
summary: Create associations between code commits and other Digital.ai TeamForge items, such as tracker artifacts or documents, to help define relationships, track dependencies, and enforce workflow rules.
---
For example:

 * Associate a code commit with the bugs, feature requests, or other tracker artifacts that the code addresses.
 * Associate a code commit with the task requiring its completion.
 * Associate a code commit with an object in an integrated application.
 * Associate a code commit with a requirements document.
 
 {% include note.html content="When you commit files to your source code repository, a source code commit notification mail is sent to users who are monitoring that source code repository. An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui]." %}

## Associate Code with Other Items While Committing

When you commit files to your source code repository, use the commit comment to quickly link your commit with one or more tracker artifacts or other TeamForge items.

Associations track the links between code and the bugs, feature requests, or other tracker artifacts that the code addresses. You also associate code commits with other TeamForge items, such as tasks or documents.

A project administrator can make associations mandatory for all code commits. When this is made mandatory, the following additional rules pertaining to code commit can also be set. These rules will be enforced when performing the code commit.

 * the artifact and the commit must be in the same TeamForge project.
 * the artifact must be in open state.
 * the committer must be the owner of the specific artifact.
 
 {% include note.html content="Once you enforce the above rules, validations are strictly enforced for commits against tracker artifacts only. In case you commit against any other TeamForge object, for example a wiki or a document, mere existence of the object ID ensures successful commit and association and no validations are performed against the status of the object or who it is assigned to." %}

You can create tracker artifact associations from whatever interface you normally use to check code into your SCM repository. You do not have to log into TeamForge.

Use the same syntax for commits to Subversion repositories.

When making a code commit, add the associate command in the commit message like this: \[\<item id\>\], such as the TeamForge tracker artifact ID or task ID.

 * TeamForge item IDs are always letters followed by four or more numbers, such as `task1029` or `artf10011`.
 * To associate a commit with multiple TeamForge items, separate the item IDs with commas.
 * All associations are displayed in the _ASSOCIATIONS_ tab of the **Commit Details** page.
 * The **Comment** section lists the comments made with each commit.

 {% include note.html content="To associate an object in an integrated application, use the \[\<prefix_objectid\>\] format. Each integrated application displays its prefix on moving the mouse over the application name." %}

 {% include note.html content="When you commit files to your source code repository, a source code commit notification mail is sent to users who are monitoring that source code repository. An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui]. " %}

 {% include tip.html content="To remind yourself of the details of the association later, look in the <i>CHANGE LOG</i> tab of the associated <b>View Artifact</b> page." %}

## Create Associations with Code That is Already Committed

At any time after a code commit is made, you can associate the code commit with other Digital.ai TeamForge items, such as tasks, integrated application objects, or documents.

1. Click **SOURCE CODE** from the **Project Home** menu.
2. On the list of project repositories, select the repository containing the code commit with which you want to create an association.
3. Click **View Commits**.
4. On the **Repository Details** page, click the name of the commit with which you want to create an association.
5. On the **Commit Details** page, click the _ASSOCIATIONS_ tab.
6. On the list of existing associations, click **Add**.
7. In the **Add Association Wizard** window, select the items with which you want to associate the artifact:
   * **ENTER ITEM ID** - If you know the item's ID, you can enter it directly.
     {% capture association %}
     {% include inline_image.html file="status-success-small.png" %} To associate an object in an integrated application from with TeamForge, use the \[\<prefix_objectid\>\] format.<br><br>
     {% include inline_image.html file="status-success-small.png" %} Each integrated application displays its prefix on moving the mouse over the application name in the tool bar.
     {% endcapture %}
     {% include callout.html type="primary" content=association %}
   
   * **ADD FROM RECENTLY VIEWED** - Select one of the last ten items you looked at during this session.
   * **ADD FROM RECENTLY EDITED** - Select one of the last ten items you changed.
8. Click **Next**.
9. You may add a comment in the **ASSOCIATION COMMENT** text box.
10. Save your work.
    * Click **Finish and Add Another** to add additional associations.
    * Click **Finish** to return to the **Details** page.

    {% include note.html content="When you commit files to your source code repository, a source code commit notification mail is sent to users who are monitoring that source code repository. An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui]." %}
11. Click the _Associations_ tab to view a graphical representation of all the associated items. Through the Association Viewer, you can choose to view associations in the form of a list or flip over to the Trace view to explore the layers of associations (including parent/child dependencies) laid out in a timeline. You can scroll across the Trace view by dragging the mouse over the association layer or use the 'Previous' and 'Next' arrows to view all the objects as events in a timeline.

    While the _Associations_ tab shows the count of the total number of associations, you can only view the most recent 500 associations when you click the _Associations_ tab in case the artifact has more than 500 associations. You can, however, browse through the Association Viewer to view older associations.

    You can click on each node on the graphical association viewer to filter and display the associated items in the table below the association viewer thus matching the number of associations provided on the selected node. For example, if the node that you select for filtering is having two associations on it, the table displays the two associated items as a result of the filtering process.


{% include links.html %}