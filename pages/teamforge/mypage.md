---
title: My Workspace
keywords: My Workspace, My Workspace widgets, dashboard
tags: [ctf_210, ctf_19.3, getting_started, project_member_tasks]
sidebar: teamforge_sidebar
permalink: mypage.html
last_updated: Feb 3, 2021
summary: Your My Workspace is a personal workspace that offers a handful of configurable widgets such as My Recent Projects, My Recent Repositories, Git Code Reviews, Project News and so on. You can use these widgets to view recent projects, recent repositories, recent commits, items assigned to you (TeamForge artifacts and document reviews), Git code reviews, project news, reports and more.
---

{% include callout.html type="primary" content="After logging into TeamForge, you are taken to your **My Workspace**." %}

You can create one or more dashboards to categorize and view data in many different views. For instance, you may decide to create three dashboards: Dashboard A, B and C. With these three dashboards, you may choose to configure Dashboard A and B to view events from projects A and B respectively and configure Dashboard C to view just the code reviews.


{% include image.html file="multiple-workspaces.png" %}

## Create and Configure Dashboards: Step by Step

1. To create a new dashboard, click **New Workspace** from the workspace drop-down on your dashboard.
   {% include image.html file="workspaces.png" %}
   {% include note.html content=" you can create as many dashboards as required." %} 
2. Enter a name for the dashboard that you're going choose from the dashboard layouts provided.
   {% include image.html file="dashboard-layout.png" %}
3. Click **Add widget** and select a widget.
   {% include note.html content="You can add multiple instances of the same widget to your dashboard. For example, you can add two instances of the **Artifacts** widget, one each to show the **Open** and **Closed** artifacts assigned to you." %} 
4. All widgets have criteria or content that controls what information they display. These settings can be configured by clicking the **Edit widget configuration** icon {% include inline_image.html file="174-myworkspace-05.png" %} on the widget after adding them to the My Workspace.
5. Arrange widgets by clicking the **Change widget location** icon {% include inline_image.html file="174-myworkspace-07.png" %} and dragging the widget to the place in your layout where you want to see it.
6. Use the Collapse widget {% include inline_image.html file="174-myworkspace-08.png" %} and Remove widget {% include inline_image.html file="174-myworkspace-09.png" %} icons to collapse and remove widgets.
7. Repeat steps 4 through 7 to add and configure more widgets.
8. When you are done, click **Save**. 

You can select a dashboard from the drop-down list and click **X** next to the dashboard drop-down list to delete the dashboard.
{% include image.html file="delete-dashboard.png" %}

## My Workspace Widgets {#myworkspacewidgets}

Widgets, which provide the functionality you want to expose on your dashboard.

{% include image.html file="selectmywidget.png" %}

A variety of widgets have been provided, which include the following:
* Approval Requests: Shows a summary of pending approval requests
* Artifacts: Shows artifacts assigned to the user
* Document Reviews: Shows document reviews assigned to the user
* Documents: Shows documents of a selected project
* Events: Shows TeamForge events
* Git Code Reviews: Shows Git Code Reviews
* Markdown: Generic Markdown renderer and editor
* Project News: Shows project news
* Recent History: Shows objects most recently accessed by the user
* Recent Projects: Shows projects most recently accessed by the user
* Recent Repositories: Shows repositories most recently accessed by the user
* Reports: Shows TeamForge reports

You can select the desired widgets and click the **Add selected widgets** to add them to your **My Workspace** dashboard.

## Artifacts Widget {#myartifactswidget}

Shows the list of artifacts assigned to the user.

<!-- The following enhancements are added for the **My Artifacts** widget in TeamForge 18.3. -->

* **Filter Artifacts by Title**&mdash;Click the **Title** header on the **My Artifacts** widget to filter the artifacts by their title.

  {% include image.html file="my-artifacts-title-filtering.png" %}

* **View Monitored Artifacts**&mdash;You can view the artifacts that you're monitoring using the **Include Monitored by Me** option. 

  To enable the **Include Monitored by Me** option:

  1. Click the edit icon ( {% include inline_image.html file="my-workspace-edit-button.png" %}) on **My Workspace** page.

  2. Click the **Edit widget configuration** icon ( {% include inline_image.html file="174-myworkspace-05.png" %}) on the **My Artifacts** widget.

  3. Select the **Include Monitored by Me** check box on the **Artifacts** pane.

     {% include note.html content="The **Assigned To** and **Created By** fields will be not be shown, when you select the **Include Monitored by Me** check box." %}

     {% include image.html file="my-artifacts-monitorbyme-option.png" %}

  4. Click **Apply**. 

     You can now see the artifacts monitored by you on the **My Artifacts** widget. A bell icon ( {% include inline_image.html file="monitored-button.png" %}) is shown for the artifacts that you're monitoring. Click this icon against the artifact that you don't want to monitor.

     The monitoring icon toggles between blue ( {% include inline_image.html file="monitored-button.png" %}) color for artifacts that you're monitoring and grey ( {% include inline_image.html file="monitor-button.png" %}) color for artifacts that you're no longer monitoring.

     {% include image.html file="my-artifacts-monitoredartifacts.png" %}

The following filters of the **Artifacts** widget are multi-select filters that let you narrow your filter scope: `Project`, `Assigned To`, `Created By`, `Status` and `Priority`. For example, you can now configure the **Artifacts** widget to filter and show artifacts from a select list of multiple projects, multiple users, multiple priorities and so on.

You can also choose the maximum number of artifacts to show.

{% include image.html file="210-myworkspace-01.png" caption="Maximum number of artifacts to show" %}

If the number of artifacts exceeds your preferred number of artifacts to show, a **View All** link shows up.

<!-- [artf417676] Artifacts widget in My workspace--behavioral changes in 21.0 --> 
Click the **View All** link to view the entire list of artifacts assigned to you on the **All My Assigned Artifacts** page. However, out of all the filters you may have configured in the **Artifacts** widget, the **All My Assigned Artifacts** page can only inherit and apply the following filters:

* Priority
* Created By
* Status
* Tracker
* Project

For example, you might have used the **Date Submitted** filter of the **Artifacts** widget to filter and view only those artifacts submitted in the last 90 days. However, when you click **View All**, the **All My Assigned Artifacts** page shows all the artifacts assigned to you regardless of the date of submission.

<!--artf277203 -- TeamForge 19.3 -->
### Document Widget {#documentswidget}

From TeamForge 19.3, you can add the **Documents** widget to your **My Workspace** page. 

{% include image.html file="selectmywidget-documents.png" caption="New \"Documents\" widget option" %}

Select the **Documents** option from the **Add new widget** page and click **Add selected widgets** to add the **Documents** widget to your **My Workspace** page.

Click the **Edit widget configuration** (gear icon) on the **Documents** widget and select the criteria based on which the documents would get listed on the **Documents Widget**.

{% include image.html file="myworkspace-documents-filter-criteria.png" caption="Filter criteria based on which documents get listed on the \"Documents\" widget" %}

{% include image.html file="myworkspace-documents-widget.png" caption="Documents Widget listing documents based on selected project and other filter criteria" %}
<!--artf277203 -- TeamForge 19.3 -->

{% include links.html %}