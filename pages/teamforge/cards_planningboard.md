---
title: Work with Artifact Cards
keywords: work with artifact cards
tags: [project_member_tasks, boards, trackers, planninf_folder]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Mar 15, 2018
permalink: cards_planningboard.html
summary: In the Planning Board, artifact cards are displayed in ranked sequence within each swim lane. Using Planning Board, you can quickly add new cards (quick add), edit cards, move cards within a swimlane to rank them and move cards between swim lanes to reassign them to other planning folders.
---

## Add Artifacts Quickly

You can add artifacts (quick add) in select planning folders with minimum required artifact information. 

 {% include important.html content="While you quickly add artifacts with data for just three fields such as the tracker type, title and description, the artifacts are, however, saved with default values for other required fields, which you may choose to update later. You cannot add artifacts from the Planning Board if a workflow is configured for the meta status change from `New` to `Open`." %}

 1. Select a planning folder in one of the swim lanes. The quick add ( {% include inline_image.html file="quikaddbutton.png" %}) button at the top of the swim lane is enabled.

    {% include note.html content="To be able to add artifacts in Planning Board, you need to have the required permissions." %}

 2. Click the quick add ( {% include inline_image.html file="quikaddbutton.png" %}) button. The **Create Artifact** window appears.

    {% include image.html file="createartifact.PNG" %}

 3. Select a tracker type from the **TRACKER** drop-down list.

 4. Type a title and description. You can select the **USE TITLE AS A DESCRIPTION** check box to copy the title you type to the **DESCRIPTION** text box.

    **Artifacts support @mentions**: Artifact description and comments now support @mentions and users called out via @mentions are added to the monitoring list. Include usernames with "@" as prefix (for example, @mphippard) to add users to the monitoring list.

     {% include note.html content="Users called out via @mentions must have `Artifact View` permission to be added to the monitoring list." %}

 5. Click **Submit**. The artifact is added as the bottommost artifact in the swim lane (planning folder). You may choose to rank the artifact (if you have rank permission) or update the artifact with more meta data later. To update the artifact, click the artifact ID link.

## Rank a Card

If you have the requisite permission, you can drag and drop a card about or below the other cards within a swim lane to position it in the order you want the artifact addressed.

 {% include note.html content="The positioning of cards is retained when you switch between the list and board views (planning, task and kanbar). For related information on ranking artifacts in the list view, see [Reorder the Contents of a Planning Folder][reorderplanningfoldercontent]." %}

 
## Reassign (move) a Card

In the course of planning your release, you may want to assign an artifact from the product backlog to a specific sprint or team, or move an artifact from one sprint to another. To do this, just drag and drop the artifact card from one swim lane to the other.

 {% include note.html content="When you drop the card, its rank is relative to its position in the new swim lane. However, if a child artifact is moved to a swim lane (planning folder) where its parent is already present, the child artifact is file under its parent and its rank is relative to the parent's position." %}

To be able to move cards between swim lanes, you need to have the permission to update planning folders and rank artifact cards.

## Edit an Artifact using the Artifact ID Link

 1. Click the artifact ID link.

    {% include image.html file="pboard_artfcard_edit.png" %}

    <br>

    The **View Artifact** page appears.

 2. Make the necessary changes and click **Update** to update the artifact and return to the Planning Board.

     **To quickly edit an artifact:**

 3. Click the edit artifact ( {% include inline_image.html file="editartifactsbutton.PNG" %}) button in a card. The **Edit Artifact** window appears.

     {% include note.html content="To be able to edit artifacts, you need to have the required permissions." %}
     {% include image.html file="editartifactswindow.PNG" %}

 4. You can edit the following in the **Edit Artifact** window:

     * **Artifact title**

     * **Artifact description**

     * **Primary and secondary attributes**

          You have two expandable frames, **Primary Attributes** and **Secondary Attributes**, that list fields you can edit. Primary attributes include Priority, Status, Assigned To, Team, Estimated Effort, Remaining Effort, Actual Effort and Points. The expandable frames and the fields listed in them depend on your application configuration that you set in Tracker Settings. For example:
          
          * Configurable fields which are enabled. For more information, see [Enable or Disable Tracker Fields][trackers-creatingatracker.html#enabledisablefields].
          * User-defined fields (flex fields) with the field type Text Entry and Single Select and set as **Required** (Tracker Settings > Tracker Administration > Create Field) or workflow configured. For more information, see [Create Custom Tracker Fields][trackers-creatingatracker.html#customfields] and [Create a Tracker Workflow][trackers-creatingatracker.html#createatrackerworkflow].

            {% include note.html content="You cannot change the status of an artifact in the Planning Board view, if `Assigned To` is set as a mandatory field for status changes per your tracker workflow settings (Tracker Settings). However, you can edit the status of an artifact in the List view with the same `Assigned To` workflow constraint." %}
     
            By default, the following field types which you select while creating a user-defined field (Tracker Settings), are non-editable from the planning board's **Edit Artifact** window: Multiple select, Date picker and User picker.

            {% include image.html file="noneditablefields.png" %}        
     
     * **Comments**

       In this expandable frame, in addition to adding comments, you can view the last five comments for an artifact.

     **Artifacts support @mentions**: Artifact description and comments now support @mentions and users called out via @mentions are added to the monitoring list. Include usernames with "@" as prefix (for example, @mphippard) to add users to the monitoring list.

       {% include note.html content="Users called out via @mentions must have `Artifact View` permission to be added to the monitoring list." %}

 5. After editing an artifact, click **Update**.

{% include links.html %}