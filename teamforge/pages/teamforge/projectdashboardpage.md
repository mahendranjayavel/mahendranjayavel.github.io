---
title: The Project Dashboard Page
keywords: My Page, Project Dashboard
tags: [getting_started, project_admin_tasks]
sidebar: teamforge_sidebar
permalink: projectdashboardpage.html
last_updated: Mar 13, 2018
summary: The Project Dashboard offers a centralized view into all development projects managed in TeamForge .
---
The Project Dashboard provides managers with an at-a-glance overview of the status of each of their projects. It provides summary information on the number and status of the tasks and tracker artifacts in each project, and calculates project overrun and underrun statistics.

The Project Dashboard also provides overview information such as project start and end dates and project ranking.

You can see the Project Dashboard if you have both the View Tracker and View Task permissions for one or more projects. Only those projects for which you have both the View Tracker and View Task permissions appear on your Project Dashboard.

In the TeamForge navigation bar, click **My Workspace > Dashboard**.

You can view the Project Dashboard if you have both the View Tracker and View Task permissions for one or more projects. Only those projects for which you have both the View Tracker and View Task permissions are displayed on your Project Dashboard.
Contents

For each project, the Project Dashboard displays the following information:

* **Project Activity ranking**--The activity of the project in relation to all other TeamForge projects.
* **Start Date or End Date**--The start and end date of the project, based on the start and end dates of all project tasks.
* **Task Status**--The status of the project, based on the "rolled-up" status of all project tasks and task folders. You can configure the "roll up" criteria for each project from the project's Task Manager Settings page.
* **Status History**--The history of the project's "rolled-up" status color. These figures are calculated in real time, but do not calculate time that the project's status was Not Started or Completed.
  
  Click the status bar to go to the project's Task Summary page.
* **Task and Tracker Effort** - The project's current overrun or underrun, based on the difference between estimated and actual effort spent on project tasks and tracker artifacts.

  Only completed and closed tasks and tracker artifacts, with values in the estimated and actual effort fields, contribute to the overrun or underrun calculations.
* **Tracker Status**--The number of open tracker artifacts in the project, per priority value. The number of open tracker artifacts is indicated in parentheses.
  
  Click the status bar to go to the project's Tracker Summary page.



{% include links.html %}