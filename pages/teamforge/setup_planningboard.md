---
title: Set up Planning Board
keywords: planning board, boards, planning
tags: [ctf_20.2, project_admin_tasks, boards, planning_folder, trackers]
sidebar: teamforge_sidebar
permalink: setup_planningboard.html
last_updated: Jul 15, 2020
summary: The Planning Board is an important tool for your TeamForge project's agile planning activities. It enables you to plan and monitor the features that are required in each sprint (or iteration), and assign them from the product backlog to specific sprints.
---

When you've set up your planning folders, you have four views available to work with them: 

 {% include image.html file="listplantrack01.png" %}

 * **LIST**: The list view.
 * **PLAN**: The planning board view.
 * **TASK**: The task board view.
 * **KANBAN**: The kanban board view.

The planning board view complements the list view. While the latter offers you capabilities to accomplish various actions such as create, edit, and delete artifacts, planning folders and teams, the former offers product owners (or similar users) the ability to view, rank and move artifacts across the three planning folders (swimlanes) in a physical board-like user interface. In the Planning Board, planning folders are represented as swimlanes. In each swimlane, the tracker artifacts for the selected planning folders are represented as cards. You can also have a team's view of artifacts (backlogs and tasks), which is a swimlane representation of artifact cards for the selected team in the selected planning folder.

TeamForge user roles and permissions that are in place for planning folders apply to all the four views.

## Use the Planning Board

You start populating the Planning Board by selecting a planning folder for each swin lane.

The drop-down list for each swim lane displays the hierarchy of active planning folders for the all the sprints and scrum teams that are under the project's root planning folder. By default, inactive planning folders are not shown in the swim lane drop-down list. You can organize the Planning Board the way you want by populating the swim lanes with planning folders of interest to you: for example, you may select the planning folder corresponding to the product backlog in the leftmost swim lane and various teams working on the release in the other two swim lanes, or a different sprint in each swim lange. Your selections are remembered for the current session.

In the Planning Board, artifact cards are displayed in ranked sequence within each swim lane. The tasks that you can accomplish while you work with the Planning Board include:

 * Adding artifacts (quick add) in select planning folders with minimum required artifact information.

 * Editing artifacts.

 * Moving artifact cards within a swim lane and ranking them in select planning folders.

 * Reassigning (move) artifacts from one planning folder to the other.


 1. Click **TRACKERS** from the **Project Home** menu.

 2. In the **List Trackers, Planning Folders and Teams** page, click **PLAN**. A Planning Board for the current project context is displayed.

 3. For each swim lane in the Planning Board, select a planning folder from the drop-down list. The tracker artifacts contained by the planning folders are displayed as story cards within the corresponding swim lanes.

    * If a selected planning folder has subfolders, the artifacts within the subfolders are not displayed.

    * Cards have a color-coded bar to visually identify the priority. In addition, the open and closed card's background is color-coded to uniquely identify the status.

    * For each card, the artifact ID, title, priority, status, assigned to and points (story points) are displayed. For an artifact, the estimated effort (in hours) in shown only if its points=0. Relevant tooltips appear when you hover your mouse over these data elements.

    Assistive information such as the number of cards in the selected planning folder and planning folder points capacity are displayed at the top of the swim lane.

     {% include note.html content="The Planning folder points capacity is not displayed for `Iteration` folder types." %}

    For example, in the following screenshot, the planning folder points capacity is shown as `36/100 Pts`. Which means, you planned for 100 points, whereas the current points capacity (the sum of all open and closed artifacts) is 36 points. In other words, you have room for taking up more work in that particular planning folder.

     {% include image.html file="swimlane.png" %}

    You can also see 2 cards at the top of the swim lane, which is the count of the number of cards in the selected planning folder (by default, only open cards are counted).

    Click the **Show/hide closed artifacts** ( {% include inline_image.html file="showclosedartifacts.png" %}) toggle button to see the count of both open and closed artifacts.

     {% include note.html content="You must have set the `Points Capacity` while creating planning folders to be able to see the current points capacity against the planned points capacity. For more information, see [Create a Planning Folder][creatingplanningfolder]" %}.

 4. Click the swin lane refresh ( {% include inline_image.html file="swimlanerefresh.png" %}) button to refresh individual swim lanes.

 5. To know more about an artifact, click the artifact ID link. The **View Artifact** page is displayed.

 6. By default, closed artifacts are not shown in swim lanes. Click the Show/hide ( {% include inline_image.html file="showclosedartifacts.png" %}) toggle button to show or hide closed artifacts in swim lanes.

 7. To expand an artifact that has child artifacts, click the "**+**" symbol in the artifact card. The first, second and third-level child artifacts are displayed. When you expand an artifact, the parent and child artifacts are visually outline by means of colored boxes as shown in the following screenshot.

     {% include image.html file="coloredboxes.png" %}

## View Artifacts That Are Not Assigned to Any Planning Folder
<!-- [artf413446] Documentation for artf397153--Plan Board - View artifacts that are not assigned to a Planning Folder -->

* A new planning folder, `None`, is now available to select from the **Select a Planning Folder** drop-down list of the Planning Board swim lanes.
  {% include image.html file="202-nonpfpb.png" caption="View artifacts that are not assigned to any planning folder" %}
* Selecting `None` from the drop-down list populates the swim lane with all the artifacts that are not assigned to a planning folder yet (in other words, artifacts with `None` as Planning Folder).
* This is to let you view the list of all artifacts that do not have a planning folder assigned yet. 
* You cannot rank or reorder the artifacts in the **None** swim lane like you do with artifacts from a normal planning folder.
* Moving an artifact into the **None** swim lane strips the artifact of its rank and order.   


{% include links.html %}