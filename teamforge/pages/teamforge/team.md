---
title: Manage Your Project Teams
keywords: an overview of teams, create a team, edit a team, delete a team, view a team
tags: [project_admin_tasks, project_member_tasks, teams]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Apr 17, 2018
permalink: team.html
summary: The Team feature, as the name implies, enables you to create logical groups of team members to carry out project activities more efficiently in an agile environment. Using the Team list view, you can create, edit, delete and view teams at the project level.
---

## Teams - An Overview

Using Teams, project activities can be planned, tracked, collaborated, reported and executed in a more organized and structed manner.

This features facilitates effective communication among the team members who need to be aware of the changes and latest updates occurring in their projects and act accordingly. For example, using the team's view of backlogs, any project impediment can be communicated to the team and resolved quickly.

The Team list view consists of a tree structure of all the teams in a project, a summary and a filter table of the selected team. The filter table allows you to assign artifacts to a specific team. You can configure your team filter table and filter work items depending on the information you want. The filter table lists only the artifacts for the selected team. If you have selected a parent team, the filter table does not include the artifacts of the subteams (child teams).

 {% include important.html content="To access the Team feature, you must have the Tracker 'view' permission." %}
 {% include image.html file="teamview.png" %}

## Team Roles and Permissions

Other than the Tracker 'view' permission, there are no role permissions that you need to set specifically for Team on the **Permissions** page of **Project Admin**. Depending upon your project role, you can view the appropriate icons on the Team list view and perform Team related tasks.

The following table lists the various roles and their specific permissions associated with Team:

 * **Project Administrator** - You can create, edit, delete, and view teams.

 * **Team Owner** - Any team member can be designated as a team owner. You can be a team owner for more than one team. As a team owner, you can only edit and view your team details.

 * **Team Member** - Any project member can be added to a team. As a team member, you are only allowed to view the team members.

<table>
	<tr><th rowspan="2">Permissions</th><th colspan="3">Roles</th></tr>
	<tr><td><b>Team member</b></td><td><b>Team owner</b></td><td><b>Project admin</b></td></tr>
	<tr><td>Create a Team</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Delete a Team</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Add team members while creating a team</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Designate team owner while creating a team</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Edit your team details</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Add / delete team members while editing your team(s)</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Designate a team member as the team owner while editing your team</td><td><center><img src="images/status-failure-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>View a team tree</td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>
	<tr><td>Assign artifacts to any team / team member</td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td><td><center><img src="images/status-success-small.png"/></center></td></tr>	
</table>	

## Create a Parent Team

As a project administrator, you can create a parent team at the root level - **Project Teams**.

 1. Click **TRACKERS** from the **Project Home** menu.

 2. On the left pane of the default list view, click **TEAMS**. All the teams in your project are displayed on the pane.

 3. Select **Project Teams** and click **NEW** to create a new team. Alternatively, you can hover the mouse on **Project Teams** and click the **Create Team** ( {% include inline_image.html file="createicon.png" %}) button.

     The **Create Team** window is displayed.

     {% include image.html file="team_create.png" %}

 4. Give a name and description to the new team

    * The team name is a required field. You are allowed to enter a maximum of 64 characters including spaces.

    * No two teams on the same level in the Team tree hierarchy can have the same name within a project; however, a team can have the same name as that of a deleted team.

 5. Add team members by selecting the users from the list displayed. Alternatively, you can search for specific users by typing the relevant alphabets and selecting from the list of matching names.

    * The user who creates a team becomes the team owner automatically.

    * A team member can be a part of more than one team.

 6. Designate a team member as the team owner by hovering the mouse on the specific name and clicking the **Team Owner** ( {% include inline_image.html file="team-teamowner.png" %}) button.

 7. Click **Create**. A new team is created.


## Create a Sub Team

A team can have many sub teams.

 1. On the Team tree view, select the team for which you want to create a sub team and click **NEW** or hover your mouse on the specific team and click the **Create Sub Team** ( {% include inline_image.html file="createicon.png" %}) button.

    The **Create Sub Team** window is displayed.

 2. Provide all the required information, and click **Create**. A sub team is created.

## Edit a Team

As a project administrator, you can edit any team in your project. Similarly, if you are a team owner, you can edit the team(s) for which you are the owner.

 1. On the Team tree, hover your mouse on the team you want to edit and click the **Edit Team** ( {% include inline_image.html file="editicon.png" %}) button.

     The **Edit Team** window is displayed.

     {% include image.html file="team_edit.png" %}

 2. Make the required changes:

    * Edit the team name and description.

    * To add more team members, select the names from the list displayed.

    * To delete team members, hover the mouse on the specific name and click the **Remove Member** ( {% include inline_image.html file="team-deletemembericon.png" %}) button.

    * To designate another team member as the team owner, hover the mouse on the specific name and click the **Team Owner** ( {%include inline_image.html file="team-teamowner.png" %}) button.

      {% include note.html content="As a team owner, you may decide to designate a different user as your team owner. In that case, once you update your changes, you will only be a team member and you will no longer have the permission to edit your team." %}

 3. Click **Save**.

## Delete a Team

As a project administrator, you can delete any team from your project. If a team has sub teams (child teams), you can delete the parent team only after deleting all its child teams.

To delete a team, on the Team tree, hover your mouse on the team you want to delete and click the **Delete Team** ( {% include inline_image.html file="deleteicon.png" %}) button.


## View Team Members

On the Team tree, hover your mouse on the team whose members you want to view and click the **View Team Members** ( {% include inline_image.html file="team-viewmembersicon.png" %}) button.

The **Team Members** window is displayed.

 {% include image.html file="team_viewmember.png" %}







{% include links.html %}