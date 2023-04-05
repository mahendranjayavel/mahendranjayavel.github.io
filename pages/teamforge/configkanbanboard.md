---
title: Set up Kanban Board
keywords: project workflow with Kanban Board
tags: [project_admin_tasks, boards, trackers]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Apr 17, 2018
permalink: configkanbanboard.html
summary: The Kanban Board is a project management tool, which gives you a snapshot of the work items, in which states they are, how they are progressing and if there is any bottleneck to be cleared for a smooth delivery of the product on time.
---

As a project administrator, you can configure your Kanban Board based on your project requirements.

Create Kanban Board states for the different stages of your project development process, specify workflow constraints for each state and map them to your tracker statuses.

 1. Click **TRACKERS** from the **Project Home** menu.

 2. In the **List Trackers, Planning Folders and Teams** page, click **Kanban**.

    {% include image.html file="artfviews-kanban.png" %}

    The following message is displayed prompting you to configure a Kanban Board for the current project. 

    `Kanban Board is not configured for the project.`

 3. Click the Kanban Board configuration icon ( {% include inline_image.html file="taskbdconfigicon.PNG" %}) to open the **Settings** window. 

    {% include note.html content="Use the configuration icon when you create a Kanban Board for the first time or when you want to modify the settings of your current Kanban Board." %}

    Alternatively, you can use **Manage Boards** ( {% include inline_image.html file="manageboards.png" %})  to create a new board.

    For more information about its usage, see [Use Kanban Board][usekanbanboard].

 4. Give a name to the new Kanban Board.

 5. Select the trackers whose artifacts you want to view on your Kanban Board. (These are the trackers you created for your project. For more information on how to create a tracker, see [Create a tracker][trackers-createatracker].)

 6. Click **Next**.

    **Kanban States and Constraints**

    A kanban state is the status of a work item in a value stream (swimlanes). The constraints or the limits that you specify here dictates the behaviour of the board. These are checkpoints which eventually help you track the progress of a work item, identify bottlenecks and fix them. The default kanban statuses are 'Not Started', 'In Progress' and 'Closed'.

    You can create your own kanban statuses, delete any state including the default one and rearrange the order in which they would appear as swimlanes on your Kanban Board.

    {% include note.html content="If there are only three kanban statuses, the `Delete Status` icon is disabled disallowing you to delete any more because you must maintain a minimum of three statuses." %}

    {% include image.html file="kanbansetting1.png" %}

 7. Create and configure kanban statuses.

    1. Click the **Add Status** icon. You can have a maximum of 20 statuses.

    2. Give a label and description to the new status.

       {% include note.html content="The kanban status label can have a maximum of 64 characters and the description, a maximum of 256 characters. Alpha numeric and special characters are allowed." %}

    3. Select the **Constrain Artifact Count** check box to specify the minimum and maximum workflow constraints, that is, specify the minimum and maximum number of work items (artifact cards) that ought to be present in each status. You may specify these values based on the number of work items in the queue versus the number of resources available.

       Remember the following when you set the minimum or maximum value to -1.

       <table>
       	<tr><th>Constraint Name</th><th>Logic</th><th>Example</th></tr>
       	<tr><td>Minimum value = -1</td><td>This is treated as zero. Therefore, though the maximum value should be greater than the minimum value, the following value range is allowed: Minimum = -1; Maximum = 0 and above</td><td>Let us assume that you are in the last iteration of your release. As a project manager, you would not want to see any artifact in the 'Impeded' status. So you set the minimum to -1 and maximum to 0, which translates to zero artifacts. When this constraint is applied, your Kanban Board flags a violation, if artifacts show up in the 'Impeded' status, thereby drawing your attention to address the issue immediately.</td></tr>
       	<tr><td>Maximum value = -1</td><td>This indicates there is no limit to the maximum value.</td><td>You may choose to set -1 as the maximum constraint for the 'Closed' status because you would want to see as many closed artifacts as possible.</td></tr>
       </table>
       	
       {% include important.html content="These constraints are applicable only at the planning folder level and not at the team level because the Kanban Board is expected to give an overall visibility to the work items for an iteration or release within a planning folder and not just within a specific team." %}


      **Map Kanban States with Tracker Status**

       Next, make a logical mapping of the kanban states with the tracker statuses to view those tracker artifacts on your Kanban Board. For example, to view defects, you must first make a meaningful mapping of the kanban states with the defect tracker status(es). The mapped kanban states appear as swimlanes on the Kanban Board.

       The trackers (you had selected in Step 5) and their statuses appear on the left. All the kanban statuses appear at the top. The tracker statuses are unmapped by default.

       * You need to map a minimum of 3 kanban statuses.

       * You can map a single kanban status to one or more tracker statuses, but you cannot map a single tracker status to more than one kanban status.

       {% include image.html file="kb-mapstatus.png"%}

 8. Click the appropriate check box. For example, for an Epic tracker, map 'Completed' and 'Rejected' tracker statuses with the Kanban statuses 'Closed' by selecting the appropriate check boxes as shown in the following screenshot.

    {% include image.html file="kb-mapstatus1.png" %}

 9. Click **Finish** to complete the process.

    **Manage Boards**

    You can create and manage multiple kanban boards per your requirement. As a project administrator, you may want to create multiple boards at the iteration level, at each unit level, (Dev, QA and so on), at the hierarchical level or at each project team level, depending upon the needs of the users. For example, to get the big picture and make executive decisions you may want to create a kanban board at the management level; at the same time, at a project member level, you can create a board to focus on the immediate tasks to be completed.

 10. Use the various icons available in **Manage Boards** to maintain multiple kanban boards in a project.   

     <table>
     	<tr><th>To do this...</th><th>Click this icon</th></tr>
     	<tr><td>To use <b>Manage Boards</b></td><td><img src="images/manageboards.png"/></td></tr>
     	<tr><td>To create a new board</td><td><img src="images/createnewboard.png"/></td></tr>
     	<tr><td>To edit a board</td><td><img src="images/editboard.png"/></td></tr>
     	<tr><td>To delete a board</td><td><img src="images/deleteicon.png"/></td></tr>
     	<tr><td>To set a default board</td><td><img src="images/setdefaultboard.png"/></td></tr>
     </table>	

     {% include note.html content=" You cannot delete the default Kanban Board. When you delete your current active board, the default one shows up automatically." %}

{% include links.html %}