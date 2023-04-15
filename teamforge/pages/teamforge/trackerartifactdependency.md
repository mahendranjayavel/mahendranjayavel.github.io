---
title: Create Dependent Tracker Artifacts
keywords: how to make an artifact dependent on another artifact, making an artifact dependent on another artifacts, make a parent artifact, make a child artifact
tags: [project_member_tasks, trackers]
sidebar: teamforge_sidebar
last_updated: Mar 15, 2019
folder: teamforge
permalink: trackerartifactdependency.html
summary: To organize your work with tracker artifacts, you can make an artifact a child or a parent of another artifact.
---

## Make a Tracker Artifact depend on another Artifact

* A child artifact can have only one parent.
* A parent artifact can have any number of children.
* A parent artifact cannot be closed if a child is open.

{% include note.html content="`Open` or `Closed` in this context, refers to a type of status, not the status itself. A tracker administrator can specify a group of statuses such as `Deferred`, `Fixed`, `Rejected`, as equivalent to `Closed`, while `In progress` and `Under consideration` might be specified as `Open` statuses. For example, when you look at the artifact summaries at the top of any tracker list page, you are seeing a summary of the status type, not the status, of the artifacts. " %}

1. On the artifact page, click the _DEPENDENCIES_ tab.
2. Choose or create the related artifact.
   * If the parent artifact already exists, click **Choose Child** or **Choose Parent**. In the pop-up, type in the artifact ID or choose from the list of your recently edited artifacts.
   * If the related artifact does not exist yet, click **Create Child in** or **Cread Parent in** and select the tracker that the new related artifact will belong to. Fill in the form the same way as you would for submitting an unrelated artifact.
   {% include note.html content="If **Choose Parent** or **Create New Parent** is not visible, the artifact already has a parent artifact. An artifact can only have one parent artifact." %}
 3. Click **Next**.
 4. Write a comment that describes the relationship, if appropriate, and click **Finish**.
    {% include note.html content="When a dependency is added to or removed from a tracker artifact, a notification mail is sent to users monitoring the artifact. An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings](siteadmin-configuresiteviaui.html)." %}

The parent-child relationship between the artifacts is established.

   * To cancel a parent dependency, click **Remove**.
   * To cancel a child dependency, select the child artifact and click **Remove**.

{% include note.html content="Task dependencies and tracker artifact dependencies are different from each other." %}

{% capture dependencies %}
   {% include inline_image.html file="status-success-small.png" %} For tracker artifacts, an artifact with dependencies ( a "parent" artifact) can't be considered closed unless all of its dependent artifacts ("children") are closed. <br>
   {% include inline_image.html file="status-success-small.png" %} For tasks, a dependency means one task can't start until another task is completed.
{% endcapture %}
{% include callout.html type="primary" content=dependencies %}

## Tracker Dependency Updates Within Change Log  

* Artifact dependency updates such as adding or removing parent or child artifact are now added to the artifact's **Change Log** tab.
* The dependency change log includes information such as the user who updated the dependency, the time when the update was done, and a brief description of the old and new dependency values.
* This change log can come in handy for auditing purposes.

## Context Menu to create Dependencies, Associations or Add Attachments

Use the context menu available in planning folder list view to quickly choose a "parent" or "child", remove a "parent", add associations, add attachments or clone artifacts.

In the planning folder list view, you can see a down arrow icon next to the artifact ID (as shown in the following screen)when you move your mouse pointer over artifact rows.

**Down arrow icon**

{% include inline_image.html file="downarrowicon.png" %}<br>

A context-sensitive menu pops up on clicking the down arrow icon.

**Context menu if an artifact has a parent**
{% include image.html file="withparent.png" %} <br>

**Context menu if an artifact has no parent**
{% include image.html file="noparent.png" %} <br>

**To quickly choose a parent or child, add associations and attachments, or remove a parent:**

1. Select a planning folder on the **List Trackers**, **Planning Folder** and **Teams** page. The planning folder **List Artifacts** page appears.
2. Move your mouse over an artifact's ID. A down arrow icon appears.
3. Click the down arrow icon to see the context menu. Depending on the context, you can do one of the following tasks.
   * [Choose a Child](#chooseachild)
   * [Choose a Parent](#chooseaparent)
   * [Remove a Parent](#removeaparent)
   * [Add Associations](#addassociations)   
   * [Add Attachments](#addattachments)
   * [Clone an Artifact](#cloneanartifact)

### Choose a Child {#chooseachild}

1. Click **Choose Child** from the context menu. The **Selection Children...** window appears.
2. Select the **Enter Artifact ID** option and type an artifact ID. This artifact becomes the child.
   {% include tip.html content="You can select the **Add from Recently Edited** option and choose a child from the list of recently edited artifacts." %}
3. Click **Next**.
4. You mad add a comment in the **DEPENDENCY COMMENT** text box.
5. Click **Finish**.
   {% include note.html content="You may also click **Finish and Add Another** to continue adding more children for the same artifact." %}

### Choose a Parent {#chooseaparent}
1. Click **Choose Parent** from the context menu. The **Selecting Parent...** window appears.
2. Select the **Enter Artifact ID** option and type an artifact ID. This artifact becomes the parent.
    {% include tip.html conten="You can also select the **Add from Recently Edited** option and select a parent from the list of recently edited artifacts." %}
3. Click **Next**.
4. You may add a comment in the **DEPENDENCY COMMENT** text box.
5. Click **Finish**.

### Remove a Parent {#removeaparent}
1.  Click **Remove Parent** from the context menu. A confirmation message appears as: `Do you want to remove the dependency?`
2. Click **OK**.

### Add Associations {#addassociations}

1. Click **Add Association** from the context menu. The **Add Association Wizard** appears.
2. Select the **Enter Item ID** option and type an artifact ID for creating an association.
   {% include tip.html content="You can select the **Add from Recently Edited** option and select an artifact from the list of recently edited artifacts." %}
3. Click **Next**.
4. You may add a comment in the **Association Comment** text box.
5. Click **Finish**.
   {% include note.html content="You may also click **Finish and Add Another** to continue associating more artifacts." %}

### Add Attachments {#addattachments}

1. Click **Add Attachments** from the context menu. The **Add Attachments** window appears.
   {% include note.html content="You can add any number of files by dragging and dropping them or by adding multiple files using the Browse button on the **Add Attachments** window." %}
2. Type a comment for the attachments in the **COMMENT TEXT** box.
3. Click **Choose File**.
4. Browse and select the file you want to attach.
5. Click the **Attach another file** link to add more attachments. Repeat this step for adding more attachments.
6. Click **Add** to attach the selected files to the artifact.

### Clone an Artifact {#cloneanartifact}

1. Click **Clone** from the context menu. The **Clone Artifact** window appears.
2. Provide a name and description for cloning the artifact.
3. Click **Clone** to clone the artifact.


{% include links.html %}