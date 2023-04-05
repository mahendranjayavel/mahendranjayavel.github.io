---
title: Use Task Board
keywords: task board
tags: [boards, project_member_tasks, planning_folder, trackers]
sidebar: teamforge_sidebar
permalink: usetaskboard.html
last_updated: Sep 25, 2019
summary: During a sprint, TeamForge project members can use the Task Board to view tasks, create tasks for backlog items, edit tasks and drag and drop tasks across swimlanes as they progress.
---
With the Task Board, you can:

 * View backlog items of a selected planning folder in the **Backlog Items** swimlane, which is the leftmost swimlane of the task board.
 * View tasks (belonging to backlog items) pinned to swimlanes based on the status.
 * Edit backlog items and tasks by clicking the artifact ID link.
 * Move tasks (cards) from one swimlane to the other as tasks progress.
 * Add new tasks for backlog items.

 1. Click **TRACKERS** from the **Project Home** menu.

 2. In the **List Trackers, Planning Folders and Teams** page, click **TASK**.

    {% include image.html file="listplantrack02.PNG" %}

    A Task Board for the current project context is displayed.

 3. Select a planning folder from the drop-down list. The Task Board is populated with backlog items and their tasks.

    * If a selected planning folder has subfolders, the artifacts within the subfolders are not displayed.

    * Cards have a color-coded bar to visually identify the priority. In addition, the open and closed cards' background is color-coded to uniquely identify the status.

    * For each card, the artifact ID, title, priority, assigned to and effort (in terms of 'Points' for backlog items and 'Hours' for tasks) are displayed. Status information is shown on backlog cards only. Relevant tooltips appear when you hover your mouse over these data elements. You can also hover your mouse over the tracker icon in backlog and task cards to know the tracker name.

    {% include note.html content="Earlier, the Tracker Artifacts without parent artifacts and with/without dependent or child artifacts were only displayed in the **Backlog Items** swimlane for a selected planning folder on the Task Board. From TeamForge 19.3, all the artifacts which have parent artifacts are also shown in the **Backlog Items** swimlane. In other words, the **Backlog Items** swimlane now shows all the artifacts irrespective of their dependencies." %}

    <br>
    **Add New Tasks**

 4. Click the **+** icon.

    {% include image.html file="taskbdcard02.png" %} 

    The **Create Task** window appears.

    {% include image.html file="createtasks.PNG" %}

 5. Type a title and description and click **Submit**.

    {% include tip.html content="To use the title you type as the description, select the `Use Title as Description' check box." %}

    <br>
    **To edit a backlog item or task using the task ID link:**

 6. On the **List Trackers, Planning Folders and Teams** page, select the planning folder.

 7. From the listed backlog items and tasks, click the artifact ID link you want to edit.

    {% include image.html file="taskbdcard01.png" %}

    The **View Artifact** page appears.
 
 8. Modify the backlog item or task and click **Update** to update the artifact and return to the Task Board.

    <br>
    **To quickly edit a task**

 9. Click the edit artifact ( {% include inline_image.html file="editartifactsbutton.PNG" %}) button in a task. The **Edit Task** window appears.    
    
    {% include image.html file="tb_edittaskwindow.png" %} 

 10. You can edit the following on the **Edit Task** window:

     * **Artifact title**
     * **Artifact description**
     * **Primary and secondary attributes**

       You have two expandable frames, **Primary Attributes** and **Secondary Attributes**, that list fields you can edit. Primary attributes include Priority, Status, Assigned To, Estimated Effort, Remaining Effort, Actual Effort, Points and Team. The expandable frames and the fields listed in them depend on your application configuration that you set in Tracker Settings. For example:

       * Configurable fields which are enabled. For more information, see [Enable or Disable Fields][trackers-creatingatracker.html#enabledisablefields].

       * User-defined fields (flex fields) with the field type Text Entry and Single Select and set as **Required** (Tracker Settings > Tracker Administration > Create Field). For more information, see [Create Custom Tracker Fields][trackers-creatingatracker.html#customfields].

       * Fields which are workflow configured. For more information, see [Create a Tracker Workflow][trackers-creatingatracker.html#createatrackerworkflow].

     By default, the following field types, which you select while creating a user-defined field (Project Admin > Tracker Settings), are non-editable from the task board's Edit Task window: Multiple select (Multiple Select), Date picker (Select Date) and User picker (Select User(s)).

     * **Comments**

       In this expandable frame, in addition to adding comments, you can view the last five comments for an artifact.

 11. After editing an artifact, click **Update**.

     <br>
     **Move tasks across swimlanes**

 12. To move tasks across swimlanes, drag a task card from the source swimlane and drop it on the destination swimlane.
 
     {% include note.html content="You need to have task tracker 'edit' permission to move cards across swimlanes." %}

     <br>
     **View both 'open' and 'closed' backlog items**

 13. Click the **Show/hide closed artifacts** ( {% include inline_image.html file="showclosedartifacts.png" %}) toggle button to view both 'open' and 'closed' backlog items.

     {% include note.html content="When you select a planning folder, the Task Board shows only 'open' backlog items by default." %}

     <br>
     **Refresh the Task Board**

 14. Click the **Refresh** ( {% include inline_image.html file="swimlanerefresh.png" %}) button to refresh the Task Board.

     <br> 
     **Auto assign task**

        If a task is not assigned to anyone, that is, if it is assigned to **None**, then it can be assigned to the user who has logged in using the **Auto Assign Task to Me** feature. This check box appears only if:

        * The Task Board is configured.
        * The user who logged in has the edit permission to the task tracker.
        * The project is not locked.

 15. Select the **Auto Assign Task to Me** check box and drag the artifact from one swimlane to another (from one status to another) and the artifact is automatically assigned to you.

     <br>
     **Position artifact cards**

 16. If you have the requisite permission, you can drag and drop a card above or below the other cards within a swimlane to position it in the order you want the artifact addressed.

     {% include note.html content="The positioning of cards is retained when you switch between the list and board views (planning, task and kanban). For related information on ranking artifacts in the list view, see [Reorder the Contents of a Planning Folder][reorderplanningfoldercontent]." %}
{% include links.html %}

