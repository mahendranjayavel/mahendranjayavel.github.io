---
title: FAQs on Concepts and Terms in TeamForge
keywords: FAQ, frequently asked questions
tags: [faq, projects, trackers, teams, associations, boards, project_templates]
sidebar: teamforge_sidebar
permalink: conceptsandterms-faqs.html
last_updated: Sep 25, 2019
summary: These are some of the frequently asked questions on TeamForge concepts and terms.
---

## What is an Association?

TeamForge allows users to easily associate, or link together, any objects in the system to simplify knowledge sharing and provide traceability throughout the lifecycle.

For example, a discussion post regarding a customer problem could be linked to a document specifying the feature requirement. An issue might be created to track the defect, the source code commits that fix the issue, and the release that contains the fix. All of these records can be linked together with an association. When any item is associated with another, the link appears on the item's _ASSOCIATIONS_ tab.

Associations enable development organizations to improve information sharing, capture institutional knowledge, and simplify regulatory compliance.

 {% include note.html content="When an association is added to or removed from TeamForge objects such as tracker artifacts, tasks, documents, discussions, and file releases, a notification mail is sent to users monitoring these objects.

 An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui]." %}
{{site.data.alerts.hr_shaded}}

## What is the Look Project?

The **look** project contains special files that can override your site's default appearance and content, such as the default icons, fonts, colors, and labels.

Unlike most projects, the look project has no members. It is only visible to users with site administration permission. Its only purpose is to control your site's look and feel, including such things as fonts, background colors, icons, and the wording of the onscreen labels that appear throughout your site.

Any project on your TeamForge site can have one or more Subversion repositories associated with it. The **look** project has just one Subversion repository. That repository is named **branding**.

When a user requests a page from your site, TeamForge checks the branding repository to see if any files there specify custom fonts, colors or text strings. If such specifications are found, TeamForge displays the page according to those specifications. If not, the page displays according to the default design.

Having your custom look-and-feel specifications in a Subversion repository enables you to roll back changes, track contributions, and use all the other features of a source code versioning system.
{{site.data.alerts.hr_shaded}}

## What is a Patch?

A patch is a package of code that fixes or adds to the functionality of a CollabNet product. Patches are also known as "component upgrades."

### Things to Know About Patches

 * Patches are cumulative. You don't need to apply multiple patches sequentially to get to the desired patch level. You can move up (or down) one or more patch levels with a single operation.

 * The Level option (-l) allows you to downgrade or upgrade to any patch level (within the maximum available in the cumulative patch).

 * The Rollback option (-r) allows you to revert the site to the previous patch level it was at, before the current patch was applied.

 * The Uninstall option (-u) allows you to downgrade the patch level on the site by one.

 * When a patch installation fails you can use the Force option (-F) to proceed, without manually uninstalling previous patches.

 * The system displays a summary of what happens during the patch installation.

 * Before proceeding with the patch installation, you can use the "dry run" mode (-t option) to see the summary of actions that will be performed during the installation.


### Best Practices

Before applying a patch, note the following principles.

 * The upgrade scripts are usable only with an existing installation.

 * No data migration will occur if any changes have been made to the database schema.

 * You must use the `sudo` command or have an account that is equivalent to root in order to complete a patch installation successfully.

 {% include important.html content="Before installing a patch, verify that it has been fully tested and qualified." %}
{{site.data.alerts.hr_shaded}}

## What are Planning, Task, and Kanban Boards? {#plantaskkanban}

When you have set up your planning folders and teams, you have four views available to work with them: **List**, **Plan**, **Task**, and **Kanban**.

TeamForge user roles and permissions that are in place for planning folders apply to all the four views.

{% include image.html file="listplantrack01.png" %}

### Planning Board

The Planning Board is an important tool for your TeamForge project's Agile planning activities. It enables you to plan and monitor the features that are required in each sprint (or iteration) and assign them from the product backlog to specific sprints. The planning board view complements the list view. While the latter offers you capabilities to accomplish various actions such as create, edit, and delete artifacts, planning folders and teams, the former offers product owners (or similar users) the ability to view, rank and move artifacts across the three planning folders (swimlanes) in a physical board-like user interface. In the Planning Board, planning folder are represented as swimlanes. In each swimlane, the tracker artifacts for the selected planning folders are represented as cards. You can also have a team's view of artifacts (backlogs and tasks), which is a swimlane representation of artifact cards for the selected team in the selected planning folder.


### Task Board

The Task Board is an important tool in the Agile process. It helps the team to focus on the work at hand in the current sprint and feed progress data back into the system. Unlike the list view and planning board view, which can be used for agile project planning, the task board view is for tracking tasks in a sprint. TeamForge project administrators can configure the Task Board. Once that's done, project members can use the Task Board to break down the stories into tasks and then progress the tasks, and the store, towards completion.

The Task Board can have at least two and up to seven swimlanes depending on how your project administrator configures it. Every swimlane in the Task Board represents a task status. Once configured, team members can use the Task Board to view tasks in a selected planning folder or filter tasks for a specific team within the selected planning folder, add new tasks for a backlog item (epic, story, etc.) and move tasks from one swimlane to the other as tasks progress from one status to the other.

### Kanban Board

The Kanban Board is an agile project management tool, which gives you a snapshot of the statuses of work items within a planning folder, how your project teams are placed in terms of work distribution and directs you to re-distribute the tasks to ensure optimal resource utilization.

Kanban Board uses the kanban method for project implementation. Kanban is built on two basic concepts: value stream mapping and WIP (work-in-progress) limits.

 * **Value stream map** : A value stream, as defined in the [APICS (American Production and Inventory Control Society)](http://www.apics.org/apics-for-individuals/publications-and-research/apics-dictionary) dictionary, comprises "the processes of creating, producing, and delivering a good or service to the market". In software development, a value stream map is an end-to-end mapping of the flow of activities (tasks/work items) from one state to another, starting from conceptualization to delivering the product to the customer.
 
 * **WIP limits**: These are constraints (minimum and maximum) applied on each point or state (Planning, In Progress, etc.,) in the value stream to ensure optimal WIP. This defines the minimum and maximum artifact count that ought to be present in each state so that if these constraints are violated, Kanban Board flags the issue for you to fix the bottleneck.

 For example, let us assume that you want to view the status of the work items for a planning folder called 'Iteration 1' and assess the distribution of work between teams, Team A and Team B within this planning folder. You want to see a maximum of 8 artifacts in the 'In Progress' state and you configure your Kanban Board accordingly. When you go to your Kanban Board and view the artifacts for the selected planning folder, you see a constraint violation because there are 14 artifacts in this status. In addition, when you see the work split-up between the teams, Team A has 14 artifacts whereas Team B has none. This is clearly an indication that not only is the overall count of artifacts more than the maximum constraint, but even between the teams, Team A is overloaded and Team B is underutilized; this calls for re-distribution of work items to avoid any delay in the development process.

You can configure the Kanban Board based on your project activities and you can configure as many boards as you require.

### List, Plan, Task, and Kanban Views

You can click the LIST, PLAN, TASK and KANBAN buttons to toggle between these views.

When you make a planning folder or team selection in the respective list view, (either from the planning folder/team tree or through the Jump to ID box), the selection is retained when you move to the task board or kanban board view. Similarly, when you select a planning folder or team in the task board or kanban board view, the selection is retained as well when you move to the list view. These selections are retained across browser sessions as well.

 {% include note.html content="An exception to this case is when you select the root planning folder or team ('Project Teams') in the list view, this selection is not retained when you move to the task or kanban board view; instead, the selection of a specific planning folder or team you had made prior to this one is retained." %}

In the Planning Board, multiple planning folder and team selections are retained when you navigate to other pages in TeamForge and return to your planning board.
{{site.data.alerts.hr_shaded}}

## What is a project dashboard page and what it consists of?

The **Project Dashboard** offers a centralized view into all development projects managed in TeamForge.

### Overview

The **Project Dashboard** provides managers with an at-a-glance overview of the status of each of their projects. It provides summary information on the number and status of the tasks and tracker artifacts in each project, and calculates project overrun and underrun statistics.

The **Project Dashboard** also provides overview information such as project start and end dates and project ranking.

You can see the **Project Dashboard** if you have both the View Tracker and View Task permissions for one or more projects. Only those projects for which you have both the View Tracker and View Task permissions appear on your **Project Dashboard**.

### Getting there

In the TeamForge navigation bar, click **My page > Dashboard**.

You can view the **Project Dashboard** if you have both the View Tracker and View Task permissions for one or more projects. Only those projects for which you have both the View Tracker and View Task permissions are displayed on your **Project Dashboard**.

### Contents

For each project, the **Project Dashboard** displays the following information:

* **Project Activity ranking** - The activity of the project in relation to all other TeamForge projects.
* **Start Date** or **End Date** - The start and end date of the project, based on the start and end dates of all project tasks.
* **Task Status** - The status of the project, based on the "rolled-up" status of all project tasks and task folders. You can configure the "roll up" criteria for each project from the project's **Task Manager Settings** page.
* **Status History** - The history of the project's "rolled-up" status color. These figures are calculated in real time, but do not calculate time that the project's status was **Not Started** or **Completed**.

  Click the status bar to go to the project's **Task Summary** page.

* **Task and Tracker Effort** - The project's current overrun or underrun, based on the difference between estimated and actual effort spent on project tasks and tracker artifacts.

  Only completed and closed tasks and tracker artifacts, with values in the estimated and actual effort fields, contribute to the overrun or underrun calculations.

* **Tracker Status** - The number of open tracker artifacts in the project, per priority value. The number of open tracker artifacts is indicated in parentheses.

Click the status bar to go to the project's **Tracker Summary** page.
{{site.data.alerts.hr_shaded}}


## What is a project template? {#whatisaprojecttemplate}

Project templates enable you to capture and re-use the structure and content of existing projects, including project pages, custom tracker fields, and work flow definitions, to speed new project creation and standardize lifecycle processes.

Project templates allow you to create and configure new projects quickly, enforce organizational standards, and facilitate process improvement.

To create a new project, you can use any project template created by any project administrator.

 {% include note.html content="You can also create a new project without using a template." %}

The template name and description appear on the Templates tab of the **Projects** list, accessible from the navigation bar on your **My Workspace** page. If your site administrator has made it possible to preview the contents of project templates, click the name of a template to see what's in it.

A template can include the structure of the original project without any of the content, or it can include both the structure and the content of the original project.

 * "Structure" means the folders and sub-folders in the original project.

 * "Project content" means any work items you or any other project member have created as part of the project. For example, when you create a tracker artifact to manage a piece of work, that tracker artifact is part of your project's content. Any documents you upload to the project and any wiki pages you create are part of the project's content.
{{site.data.alerts.hr_shaded}}


## What is in a project template? {#whatisinaprojecttemplate}

When you create a template from an existing project, each project tool contributes its own structure to the template, and its content if you want it.

For each tool, you can include or omit the actual content that was created with that tool.

For example, suppose you have a project for which you have created some tracker artifacts, and these artifacts have proved useful to members of the project.

 * You can include those artifacts in your template, so that people who create a new project from that template will have access to the same artifacts that you developed for your original project.

 * You can leave those artifacts out of the template and let future users create new artifacts to fit their own needs.

Imagine that you have documented company-wide process standards on wiki pages in an existing project.

 * You can include those wiki pages in a project template, so that the manager of a project created from that template won't have to go find those pages and copy them into the new project.

 * Or you can leave the wiki tool empty and let the new project's users create new wiki content for themselves.

  {% include note.html content="You can choose not to include content from the original project, but you can't choose not to include a project tool. Every project template you create must include all the project tools, even if the project from which you created the template does not use all the tools. Every project you create from a template will include all the tools." %}

<table>
<tr>
<th>﻿Tool</th>
<th>Always in Template</th>
<th>Can Be in Template</th>
</tr>
<tr>
<td>
  Tracker
</td>
<td>
  You can have any number of separate trackers in a project. When you create a project template from that project, all the trackers that exist in the original project are copied into the project template. Any default column configurations, select field dependencies or text field validation rules are also included.
</td>
<td>
  You can include the artifacts that were created in the original project, and any parent-child dependencies among them. If users of the original project have shared saved searches, these can be included too.
</td>
</tr>
<tr>
<td>
  Planning folders
</td>
<td></td>
<td>
  You can include all the planning folders in the original project, or none of them.
</td>
</tr>
<tr>
<td>
  Documents
</td>
<td>
  When you create a project template from an existing project, all the document folders that were created in the original project are copied into the project template.
</td>
<td>
If users have created documents and attachments in the original project, you can choose to include these documents in the project template.
</td>
</tr>
<tr>
<td>
  Tasks
</td>
<td>
  A project can have any number of task folders. All of those folders will be included in any project template that you create from that project.
</td>
<td>
  You can include the tasks that were created in the original project, and any dependencies among them.
</td>
</tr>
<tr>
<td>
  Discussions
</td>
<td>
  All discussion forums that have been created in the original project will be included in any project template that you create from that project.
</td>
<td>
  You can choose to include discussion topics, posts and attachments in your template, or leave them out.
</td>
</tr>
<tr>
<td>
  File Releases
</td>
<td>
  Any packages or releases that have been created in the original project will be included in the project template. If you have mapped a planning folder to a file release, that mapping is also included.
</td>
<td></td>
</tr>
<tr>
<td>
  Wiki
</td>
<td></td>
<td>
  When you create a template from an existing project, all wiki pages that users have created in the original project can be included in the project template.
</td>
</tr>
<tr>
<td>
  Integrated applications
</td>
<td>
  All external applications you have integrated into the existing project become part of the project template.</td>
    <td>Which elements are included depends on the application that is integrated. See the <b>Content includes</b> section of the <i>Projects &gt; Templates</i> tab.
</td>
</tr>
</table>

{{site.data.alerts.hr_shaded}}

## What is a story point?

A story point is a measure of effort that expresses the relative difficulty of implementing a user story. You can use story points, also referred to simply as "points", to help estimate how much work can be done in a sprint.

Story points are useful for relative measurement. A story point has no specific value in hours, or lines of code, or anything else. When you are estimating work, use story points only to compare one piece of work with another.

When you record a value in the **POINTS** field of an artifact, that value is added to the total points (story points) in the planning folder that the artifact belongs to. You can then use that figure to support forecasting.

In the parent artifact, you can view the total of story points assigned to each of its children. The calculator icon indicates that the artifact’s points is a sum of its child artifacts’ points within the project. If the parent artifact has children in other projects across the TeamForge, you can include those points in the total as well. The icon ( {% include inline_image.html file="Includeartifactsacrossprojects.png" %})  indicates that the artifact’s points include its foreign child artifacts’ points.

 {% include note.html content="The Tracker Admin needs to set the tracker to include foreign children in points calculations." %}

{{site.data.alerts.hr_shaded}}

## What is a tracker workflow?

To help users handle their tracker items effectively, you can set up some work flow rules. Workflow rules require a user to do something to a tracker before they can reassign it or update its status.

Administrators can define these kinds of workflow rules:

 * **Status transitions that a user can make based on an artifact's current status** - For example, if an artifact is `Open`, you can specify that it can be changed to `Pending` or `Cannot Reproduce`, but not to `Closed`.

 * **Status transitions that a user can make based on his or her role** - For example, if an artifact is `Pending`, you can specify that only users with the role **QA Engineer** can change it to `Closed`.

 * **Field values that a user must provide when making a specific status change** - For example, if an artifact is `Closed`, you can specify that a user must enter a comment in the `Comments` field before changing the artifact's status to `Open`. You can also require an attachment.

You can create a workflow for each combination of tracker status values in a tracker. A tracker can be cloned within a project or across the projects along with the workflow. If a user role is not existing in the destination project, a new role is created with the same name. The permissions associated with the role are not copied from the source project.

{{site.data.alerts.hr_shaded}}

## What is a user group?

To manage multiple users at once, create a group to represent them.

You can create a group to facilitate managing many users who share one or more characteristics.

For example, giving all the users in the accounting division access to all financial projects might be laborious if you assigned the permissions one at a time. Instead, create a group and assign it access to the financial projects category.

A user group can have any number of roles. When a role is assigned to a group, every member of that group has that role.

If a project is a subproject of another project, it may inherit user groups and their associated roles from the parent project.

 {% include note.html content="A user who has a role in a project by virtue of group membership is not necessarily a member of that project. Becoming a member of a project is a separate process." %}

Group permissions are cumulative. This means that each member of the user group has all the access permissions allowed by all of the assigned roles, plus any permissions that may have been assigned by other methods, such as application permissions or individually assigned roles.

### Related Links
* [Manage User Groups][manageusergroups]

{{site.data.alerts.hr_shaded}}


### Velocity and Average Velocity

Your team's velocity is the amount of work the team has shown it has completed in an iteration. You can use this information to help estimate how much work can be completed in future iterations.

In the planning folder summary page, you can see your team's velocity for the specific Iteration planning folder.

 {% include note.html content="Velocity is displayed only on the Iteration planning folder summary page." %}

Velocity is calculated based on the sum of points of closed artifacts in an iteration.

Note that velocity calculation takes into account the following:

 * Points of the parent artifacts, that is, only closed artifacts which are at the top level of the planning folder. For example, in the following illustration, only the points of the highlighted artifacts and not their child artifacts are taken into account for velocity calculation.

   {% include image.html file="velocitycal-parentartf.png" %}

 * Autosummed points of these closed parent artifacts do count as well.

Velocity only makes sense as a relative measure. There is no specific velocity that is good or bad or standard, because no two teams take on work of exactly the same scale or complexity. However, if your team's velocity is increasing from sprint to sprint, you can surmise that you are on the right track.

### Average Velocity

The average velocity is calculated for completed and ongoing iterations and is displayed only on the Release planning folder summary page. Average Velocity calculation is as follows:

`Average velocity = Sum of iteration velocity of all iterations within the specific Release/Total number of iterations`

Note the following for velocity and average velocity calculation:

 * Nested iteration planning folders (child iteration planning folders or subfolders) are not included for velocity or average velocity calculation for the parent planning folder. For example, in the following illustration:

   Average velocity for Release 1 = Sum of velocity of Iteration 1 and Iteration 2 / 2.

     {% include image.html file="velocitycal-nestedpf.png" %}

   In the above calculation, Iteration 1.1 (being the subfolder) is not included. Similarly, velocity calculation for Iteration 1 does not take into account its subfolder Iteration 1.1.
{{site.data.alerts.hr_shaded}}

## What is an activity table component?

An activity table is a special kind of text component that gives project members quick access to a focused set of artifacts, action items and work products.

An activity table includes organized links to up-to-the-minute information about work that is going on in the project. You can add, remove or change these links with the HTML editor that comes with every text component.

You can add static links to particular artifacts, or you can link to a search query. When you link to a query, you enable project users to get all the results of the query with a single click.

The activity table template is just a suggestion for how you might want to organize your information. You can change any of its properties to support the way your project members work.
{{site.data.alerts.hr_shaded}}


## What is a documents component?

A documents component allows team members to work with documents directly from a project page.

A documents component is like a window into your Documents tool. Instead of making users go to the documents tool and search for a document on their own, you can create a documents component on your project page that is linked to a folder in your documents tool. Each page can have its own list of relevant documents.

Users still go the documents tool, but now you guide them to what they need there.

{{site.data.alerts.hr_shaded}}


## What is a global project role?

A global project role is a ready-to-use role available in all projects. Only site administrators or restricted site administrators can create and manage a ready-to-use role.

As a project administrator, you can use global project roles provided by the site administrators instead of creating and managing roles tailored to your projects.

 {% include note.html content="You can use the ready-to-use roles to set up your team faster and with little fuss. However, you may not be able to edit the ready-to-use roles." %}

Before you create a role in your project, it is a good idea to check all the available ready-to-use roles. You are likely to get ones that grant the desired set of permissions.

Global project roles serve a different purpose from that of a site-wide role. The site-wide roles enable site administrators to create restricted site administrators for providing assitance in site management. Besides that, site-wide roles can be used to grant tool/application access across the site to a user.
{{site.data.alerts.hr_shaded}}

## What is a project page?

A CollabNet project page is a place where users can see and add information about the project, such as messages from the project manager, open issues or documents you want people to read.

You can build your own project pages to design, manage and track your project’s lifecycle. When you create a project page, users automatically see it in their navigation panes.

To post information or provide functionality on your project page, you add a page component of the appropriate type for the information or functionality you are working with.

For example, to let people know about how the project is coming along, add a Project Statistics component to the page. To let project members upload documents for other users to read, you add a documents component.

If the page is a part of a parent page, it appears as a node in the tree in the left navigation area.

You can add a page directly to the top of the project, or as a subpage.

 {% include tip.html content="When you have your project pages defined and your process honed, you can export your project pages in the form of a project template, so other projects in your organization can reuse the resources you created. See [Create a Project Template][creatingaprojecttemplate]." %}
{{site.data.alerts.hr_shaded}}

## What is a project page component?

A project page is a collection of simple portlet-like components that enable you to add custom HTML content, reports, project tracker queries, and much more to the project home page so your team quickly access what is important.

Project page components add functionality to a project page. You can use components to communicate with users or project members, or to invite them to contribute information or resources to the project.

 * Promote a standard lifecycle for all of your projects by using project pages to lay out information the way that works best for your business.
 * Increase developers' productivity by putting the information most relevant to your project right on the homepage.
 * Improve project coordination by combining related documents, graphs, artifacts, and content into single, digestible web pages.
 * Maintain information security. The project manager controls who has access to each of the pages and components.
 * Keep project members informed with live data and content that can be quickly updated as often as you like.

Project pages put the project manager in the driver's seat. You define how you want your project to look and what information you wish to share with your members and customers. Using a simple portlet-like layout, project pages let you add custom HTML content, reports, project tracker queries, and much more to the project home page so your team can quickly access what is important. All your pages are organized and displayed in a simple navigation menu on the left side of the home page.

In addition to customizing the project home page itself, you can also create and integrate additional web pages on the fly. Whether you need a page to display daily status reports or want to publish an HTML blog, a few clicks is all you need. No need to use any fancy tools or even know HTML.

For example, on a project page titled QA, you might have:

 * A trend graph showing the open bugs in your project over a period of time.
 * A Tracker query list showing you what hot bugs are currently in the system.
 * A block of custom HTML content that the QA lead updates daily giving users his or her take on how the quality of the product is doing that day.
{{site.data.alerts.hr_shaded}}

## What is an Available upon Request role?

The **Available upon Request** role is a role which a project member in TeamForge can submit a request for. You must be a site administrator or project administrator to create an Available upon Request role.

While creating global or project roles, you can select the **Available upon Request** option to allow the project member to see the role in **Request Additional Roles** section on the **Project Home** page.

When a project member requests a role, the request is submitted to the project administrator for approval. The project member receives an email notification when the request is either approved or denied.

 {% include note.html content="Based on the project administrator's discretion, a few role requests may be granted immediately on request, while the other role requests may need approval." %}
{{site.data.alerts.hr_shaded}}

## What is a Tracker Search Results component?

A Tracker Search Results component provides quick access to Tracker information from a project page.

Some tracker searches are used so frequently that you want people to be able to see their results without exploring. For example:

 * People working on your project may need to know at the beginning of every work day which artifacts have been updated overnight by a remote team.
 * A cross-project leadership team may need a daily count of started and completed work items to support forecasting and planning.

Such heavily-used information might be a good candidate for a tracker search component on a prominent project page, such as the project home page. When you set up this component based on a popular tracker search that you devised and saved, project members and users can save time by viewing the information at a glance, without having to go find the information themselves.

 {% include note.html content="If your site administrator has set up Project Tracker for your project, you can also use a project page query component to search your Project Tracker data." %}
{{site.data.alerts.hr_shaded}}

## What is a project statistics component?

A _project statistics component_ gives users a graphical view of recent statistics for tasks, trackers, documents, and file releases from the project page.

For more information about the project statistics component, see [Create a Project Page Component][projectsite.html#createprojectpage].
{{site.data.alerts.hr_shaded}}

## What is a text component?

A text component is a self-contained editor with which you can write anything you want on your project page.

You don't have to know anything about HTML.

Text components include everything you would expect in a fully functional HTML editor. You can add tables, upload images to embed into the page, create hyperlinks, and assign font colors and styles. Advanced users can work directly with the HTML source.
{{site.data.alerts.hr_shaded}}

## What is the complete wiki syntax that TeamForge supports?

Since TeamForge makes use of the JSPWiki rendering engine internally, you may reference the JSPWiki syntax documentation at the link below for a complete list.

http://www.ecyrd.com/JSPWiki/wiki/TextFormattingRules

Please note however that JSPWiki has progressed beyond the release available in TeamForge currently, so there may be some discrepancy between what JSPWiki supports and what TeamForge supports. TeamForge also does not currently support the JSPWiki plugin framework, so any formatting plugins referenced on the URL will not be available for TeamForge.
{{site.data.alerts.hr_shaded}}

## What is Team?

Teams helps you create logical groups of cross-functional members comprising architects, developers, testers and so on.

A team's view of backlogs complements the planning folder view. While planning folders represent backlogs (release, iteration, etc), a team's list view represents the team's view of the backlog (across releases, iterations, etc).

In an agile environment, project activities are broken into smaller units of work items and are assigned to various project teams. The Teams feature allows you to create these physical teams in TeamForge so that you get the specific team's view of backlogs. This knowledge of the team's view of work items helps you facilitate effective communication and execute project activities in a more structured and organized fashion. For example, you can easily view and filter artifacts which are taking longer than estimated within a team, analyze the scenario, and identify the impediments. Once identified, you can communicate them to the relevant team(s), re-assign it to other appropriate team(s) or team member(s), and resolve them quickly.
{{site.data.alerts.hr_shaded}}

## What is a team owner?

Any project member can be designated as a team owner.

The team owner does not have the permission to create or delete teams. They can view their team information and edit them; while editing their team details, they can add or remove members, or designate another member as the team owner.
{{site.data.alerts.hr_shaded}}

## What is a Publishing repository? How does it work? {#publishingrepository}
Publishing repository, like the branding repository, is one of the default repositories that's created automatically when a TeamForge project is created and is intended to contain publicly-consumable files.

The Publishing repo has a www directory. Files in the www directory are checked out to a working directory and served by the Apache server with no user authentication checks. In other words, files stored in the www directory do not go through TeamForge's RBAC checks and are publicly accessible even if the user is not logged in (accessible via a direct link to the file). By design, the files stored in the www directory are meant to be public on both "public" and "private" projects no matter whatsoever. However, files stored in no other directories but www are publicly accessible.

Additional security Enhancements added to Publishing Repository
Site administrators can now toggle access to Publishing Repositories and restrict access based on defined RBAC. See [DISABLE_REMOTE_PUBLISHING][siteoptiontokens.html#DISABLE_REMOTE_PUBLISHING] for more information.
{{site.data.alerts.hr_shaded}}

## What is a CERT Advisory?

CollabNet Product Support monitors the CERT coordination center (http://www.cert.org/) for notification of vulnerabilities or exploits against applications that Digital.ai TeamForge provides.

If CollabNet Technical Support identifies an advisory that may indicate potential challenges for users who have deployed Digital.ai TeamForge, Support proactively releases a notification and a statement of action. CollabNet will provide product updates as it deems appropriate or necessary.
{{site.data.alerts.hr_shaded}}

## Advantages of Using the Apache TIKA Parser Library for Indexing

Starting TeamForge 7.0, the underlying parser library for indexing has been changed from Stellent to Apache TIKA.

The Apache TIKA parser library has the following advantages over the Stellent parser library:

<table>
<tr>
<th>Issue</th>
<th>Stellent</th>
<th>Apache TIKA</th>
</tr>
<tr>
<td>Stale process issue</td>
<td>Parsing of corrupt or unrecognized files by the Stellent parser libraries often result in stale processes that consume swap space and add to the load on the system, which may at times lead to site outage. To manage such processes, you may choose to create and deploy stale process monitors and the stale processes, when detected, must be removed manually to prevent site outage.</td>
<td>Parsing of unrecognized or corrupt files by Apache TIKA libraries is robust and needs no manual intervention as there are no stale process issues.</td>
</tr>
<tr>
<td>Search queue processing speed</td>
<td>It takes five minutes to timeout when the Stellent parser library encounters a corrupt or unrecognized file that it knows not how to parse. If there are more such corrupt or unrecognized files, more time is wasted by the indexer waiting for a response (or a timeout) from the Stellent parser, which in turn adversely impacts the search queue processing speed.</td>
<td>The Apache TIKA parser library is capable of determining whether a file it encounters can be parsed or not. As no time is wasted by the indexer waiting for a response (or a timeout) from the parser, the search queue processing speed is better with the Apache TIKA.</td>
</tr>
<tr>
<td>Multiple processes Vs Single JVM</td>
<td>For parsing files, the Stellent parser library spawns one subprocess per file. Meaning, the number of subprocesses is equal to the number of files to be parsed and it is possible that we may end up with the stale process issue as discussed earlier. As a result, if the Stellent processes consume more resources, other processes and applications are left with scarce resources.</td>
<td>The Apache TIKA, being a Java-based parser library, works within the JVM and makes the external resource pool available exclusively for other processes and applications. As the search JVM, where the Apache TIKA library lives, can also be separated starting TeamForge 7.0, it can be managed better.</td>
</tr>
</table>


{% include links.html %}

<!--### How Do TeamForge Licenses Work? {#teamforgelicenses}

When you purchase a TeamForge license, you get the right to assign licenses to a specified number of users.

TeamForge supports a more flexible and granular approach to tool instantiation. TeamForge's license model consists of the following license types: ALM, SCM, DevOps, Version Control, Collaboration and Trackers. These license types are tailored to suit the needs of specific set of users that need access to certain tools and functions. A TeamForge user's license type determines the tools available to the user in TeamForge.

 {% include attention.html content="While TeamForge supports more selective tool options with these new license changes, there's no impact on customers, both new and existing, requiring all the tools that TeamForge supports." %}

The following table lists the license types and the tools that go with them (refer to the table at the end of this topic for a complete list of tools and functions).

<table>
<tr><th>License Type</th><th>Available Tools</th></tr>
<tr>
<td>
	ALM
</td>
<td>
	Offers the full range of ALM tools and functions to users.
</td>
</tr>
<tr>
<td>
	SCM
</td>
<td>
	Offers core Source Code Management tools and functions to users. Includes all the ALM tools and functions but Tracker and Documents component.
</td>
</tr>
<tr>
<td>
	Version Control
</td>
<td>
	Offers Source Code Management, File Releases and Review tools and functions to users.
</td>
</tr>
<tr>
<td>
	DevOps
</td>
<td>
	Package Management (Application & Environment) and File Releases tools and functions to users.
</td>
</tr>
<tr>
<td>
	Collaboration
</td>
<td>
	Offers a range of collaboration tools such as Documents, Wiki and Discussion Forums to users.
</td>
</tr>
<tr>
<td>
	Trackers
</td>
<td>
	Offers TeamForge's Tracker capability (Trackers, Planning Folder, Teams, Planning Board, Task Board and Kanban Board)to users. Also includes File Releases.
</td>
</tr>
</table>

In addition to the tools offering, the Reporting framework is also controlled by the licenses you have. Meaning, you can view and generate reports based on the license types assigned to you. For example, you must have SCM license to view or generate SCM activity reports.

Check with your CollabNet representative if you aren't sure how many licenses or what kind of licenses you want/have.

 * Your license key contains a few important numbers:

   * The number of users eligible to use specific licenses such as ALM, SCM, DevOps, Version Control, Collaboration and Trackers.

   * The IP address of the machine that your site runs on.

   For example, if your organization has 80 users who will use only the source code management features, 10 users who will use DevOps and 100 users who need the Application Lifecycle Management features, your license key string may look like this: 
   
   ```shell
   ALM=100:SCM=80:DEVOPS=10:supervillaininc:144.16.116.25.:302D02150080D7853DB3E5C6F67EABC65BD3AC17D4D35CB3Z00214141D70455B18583BF0A5000CA56B34817ADF8DBFI32353A6E657492617369633A38372E3139342E3136102E31322E`
   ````

   * Your license key only works for the IP address (or range of addresses) of the hardware that your Digital.ai TeamForge is running on, as specified in your order form. If your site uses a separate server for its database or source code repositories, make sure your license key reflects the IP addresses of all the necessary servers. If any of these addresses change, ask your CollabNet representative to generate a new key.
   
   * When you create a user account, you can assign the user with available licenses.

   * You can purchase a TeamForge license for as many years as you want. The validity period is encoded into your license when it is generated by your CollabNet representative.

   * How many users your site can support depends on the type of license. Check with your CollabNet representative if you aren't sure what kind of licenses you have.

   * Your license key is attached to the IP address of the server where your site runs. You can get a license key for a single IP address or for a range of IP addresses.

   * Your service year starts the first time you log into your site, or the first time you create or edit any item on your site, such as a tracker artifact or a document. Whichever of these events comes first starts the clock.

   * The expiration date of your license is shown on the License Info page. (Go to **My Workspace > Admin** and select **Projects > License Info**).

   * When your service year expires, you can still see the project data on your site, but you cannot make any changes to it. However, you can still carry out some critical maintenance functions for your site:

     * Enter a new license key.
     * Deactivate or delete users.
     * Change user passwords.
     * Get forgotten user passwords.

<table name="Tools Availability Matrix">
<tr>
<th>﻿Tools</th>
<th>ALM</th>
<th>SCM</th>
<th>Version Control</th>
<th>DevOps</th>
<th>Collaboration</th>
<th>Tracker</th>
</tr>

<tr>
<td>Agile Task and Planning Boards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Tracker</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Git/SVN Repository Management and Replication</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>  
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>
  
<tr>
<td>Code Review</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>Build Automation</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
</tr>
  
<tr>
<td>Test Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>File Releases</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>  
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Binary Repository Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>EventQ/Activity Stream</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td> 
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
  </tr>

<tr>
<td>Access Controls</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Project Work Spaces</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Wiki and Discussion Forums</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
</tr>

<tr>
<td>Document Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
</tr>
  
<tr>
<td>User Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Flexible Process and Toolchain Templates</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Reusable Dashboards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Categories and Groups</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td> 
</tr>

<tr>
<td>Cross Project Visibility</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>


<tr>
<td>Cross Project Reporting and Dashboards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Cross Project Search</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Site-wide Administration</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Custom Branding and Custom Integrations</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Security Architecture</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
</tr>

<tr>
<td>Onsite and Hosted Provisioning</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>SVN Auto Updates</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>SVN Repository Backup and Monitoring</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>
</table>-->