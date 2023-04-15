---
title: Use Kanban Board
keywords: how to use kanban board
tags: [project_member_tasks, boards, trackers, planning_folder]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Mar 15, 2018
toc:  no
permalink: usekanbanboard.html
summary: After the kanban board is configured, you can use it to view, plan and track work items for the selected planning folder or the selected team within that planning folder.
---

1. Click **TRACKERS** from the **Project Home** menu.

2. In the **List Trackers, Planning Folders and Teams** page, click **Kanban**.

   {% include image.html file="listplantrack03.png" %}

3. Select the required kanban board from **Manage Boards** (available only for project administrators). If you are a project member, select your kanban board from the **Select Board** list. The selected kanban board for the current project context is displayed.

4. Select the planning folder for which you want to view the status of the artifacts. If your project contains teams, the **Select a Team** drop-down list appears. From this drop-down, select **All artifacts** or if you want to view artifacts specific to a team within the selected planning folder, select the relevant team. Depending upon your selection, artifacts pertaining to the mapped trackers are displayed in the appropriate swimlane.

   * You can view a maximum of 5 swimlanes at a time on your Kanban Board. If there are more, use the carousel scroll to slide across the swimlanes. You can expand or collapse each swimlane. When there are no results to display in a swimlane, the **Expand/Collapse** button does not appear.

   * Based on the configuration values, if the constraints are violated, the relevant status headers are highlighted appropriately. A violation of minimum constraint is highlighted in orange indicating that resources are underutilized whereas that of maximum constraint is highlighted in red indicating resources being overloaded and bottlenecks to be fixed. For more information on how a kanban board is configured, see [Set up Kanban Board][configkanbanboard].

     {% include image.html file="kanbanboard.png" %}

   * Each swimlane header displays the status label, the total number of artifacts within the selected planning folder, and the minimum and maximum constraints that were configured for the kanban state.

     {% include image.html file="kb-swimlaneheader.png" %}

     In the above scenario, for the 'In Progress' status:

      * '3' is the total number of artifacts in the 'In Progress' status within the selected planning folder.
 
      * '2' indicates the minimum constraint and '*' indicates the maximum constraint '-1'. (-1 as the minimum constraint translates to 0 whereas -1 as maximum indicates there is no limit and so represented by an *.)

         {% include important.html content="These values and constraint validation are planning folder specific and not team specific. For example, in the above scenario, the total number of artifacts is the overall count of artifacts which are in the 'In Progress' status within the selected planning folder and not within the selected team." %}
 
   * Each artifact card displays its points (story points) or estimated effort if these fields are enabled in your tracker settings. If both are enabled, only the estimated effort is displayed hovering the mouse on which the artifact's points is displayed. Similarly, if all the effort fields (estimated, remaining and actuals) are enabled, you can view them by hovering the mouse on the estimated effort.

   * Cards have a color-coded bar to visually identify the priority. In addition, the open and closed cards' background is color-coded to uniquely identify the status.

   * A parent artifact card displays the count of its child artifacts (**Show/Hide child artifacts** button). Click this button to view or hide the child artifacts. If there are more than 5 child artifacts, when you expand the parent artifact, you will see pagination arrows ('Previous'/Next') at the bottom of the parent artifact card.

     {% include image.html file="kb-parentchildartf.png" %}

   * If the tracker types of both the parent and child artifacts have been mapped with the kanban statuses, the child artifacts appear within their parent artifact card and also as an individual card. In the above scenario, Epic (parent artifact) and Story (child artifact) trackers have been mapped to the kanban status 'In Progress'. Story 'artf1014' is the child artifact of the epic 'artf1002'. So you will see 'artf1014' within the parent artifact card as well as outside of it as an individual artifact card.
 
   * When a child artifact is closed, a 'Closed' tag appears next to the child artifact ID within the parent artifact card.

     <br>
     **Edit artifacts**

     Use Kanban Board to edit an artifact using the Edit icon on the artifact card or move artifacts from one status to another appropriately. Based on the status changes you make, the swimlane headers get updated appropriately.


     {% capture kanbanboardnote %}
     **Remember:**<br>
     You can edit an artifact only if you have the tracker edit permission. Otherwise, you can only view it.
     {% endcapture %}
     {% include callout.html type="primary" content=kanbanboardnote %}

     **Artifacts support @mentions**: Artifact description and comments now support @mentions and users called out via @mentions are added to the monitoring list. Include usernames with "@" as prefix (for example, @mphippard) to add users to the monitoring list.

     {% include note.html content="Users called out via @mentions must have `Artifact View` permission to be added to the monitoring list." %}

 5. When you drag the artifacts from one swimlane to another, note the following validations:

    * The changes you see in swimlane headers do not apply to any specific team but takes into account the total count of artifacts within the selected planning folder.

    * You cannot move an artifact card to a status that is not mapped to that particular tracker type. For example, a 'Ready for QA' kanban status may not have been mapped to any of the epic tracker statuses. So when you attempt to move an epic to that status, you will get an `Invalid status configuration` error.

    * You can move a parent artifact to the 'Closed' status only if all its child artifacts are closed. However, a child artifact is independent of its parent with regard to the status change, that is, when you move a parent artifact from one status to another, the status of the child may still remain unchanged. For example, an epic may have many stories, the status of some may change from 'Not Started' to 'In Progress' whereas some may not. So when the status of an epic as one single unit may change, it need not apply to all of its child artifacts.

    * When your move violates a constraint (minimum or maximum), a warning is displayed; but you can still move the artifacts.

    * If a kanban status is mapped to more than one tracker status, when you move an artifact, you have an option to choose a status as shown in the following screen shot.

      {% include image.html file="kb-selectstatus.png" %} 

      <br>
      **Create artifacts and child artifacts**

      Using the Create Artifact icon on the top right of your kanban board, you can quickly create an artifact. The Create Artifact icon appears only when you configure a kanban board and select a planning folder.

      Similarly, using the Create Child Artifact icon available on the artifact card, you can quickly create a child artifact for any artifact card displayed on Kanban Board.

      {% include note.html content="The Create Child Artifact icon does not appear on closed artifact cards." %}

      You can create an artifact or a child artifact only if you have the required tracker permission.

      **Artifacts support @mentions**: Artifact description and comments now support @mentions and users called out via @mentions are added to the monitoring list. Include usernames with "@" as prefix (for example, @mphippard) to add users to the monitoring list.

      {% include note.html content="Users called out via @mentions must have `Artifact View` permission to be added to the monitoring list." %}

 6. Click the required icon: Create Artifact or Create Child Artifact ( {% include inline_image.html file="kb_createartf.PNG" %}).

 7. Enter the required information in the relevant window and click **Submit**.

    * Only trackers configured for the kanban board appear in the Trackers drop-down list.

    * While you quickly add artifacts with data for just three fields such as the tracker type, title and description, the artifacts are, however, saved with default values for other required fields, which you may choose to update later. If the default state of the selected tracker is not mapped for the newly created artifact or child artifact, the artifact card does not show up on the kanban board.

     <br>
     **Show / Hide closed cards**

 8. When you have a large volume of closed cards in a planning folder, you can restrict the number of closed cards you want to view by toggling between the 'Show all closed artifacts' icon ( {% include inline_image.html file="kb_showall.PNG" %}).


    Or the 'Hide artifacts older than 60 days' icon using which you can hide closed cards older than 60 days. This is the default option ( {% include inline_image.html file="kb_show60days.PNG" %}).

    {% include note.html content="The Show/Hide toggle icon appears only on configured kanban boards. Your selection is saved for the subsequent sessions as well."%}
    
    
    <br>
    **Position artifact cards**

 9. If you have the requisite permission, you can drag and drop a card above or below the other cards within a swim lane to position it in the order you want the artifact addressed.

    {% include note.html content="The positioning of cards is retained when you switch between the list and board views (planning, task and kanban). For related information on ranking artifacts in the list view, see [Reorder the Contents of a Planning Folder][reorderplanningfoldercontent]." %}





{% include links.html %}