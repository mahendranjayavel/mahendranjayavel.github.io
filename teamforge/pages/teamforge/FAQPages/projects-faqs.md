---
title: FAQs on Projects 
keywords: FAQ, frequently asked questions, project, template, templates
tags: [faq, projects, project_admin_tasks, project_member_tasks, project_templates]
sidebar: teamforge_sidebar
permalink: projects-faqs.html
last_updated: Apr 5, 2018
summary: These are some of the frequently asked questions on projects.
---

## How is a project template structured?

When you create a template that includes project content, each tool brings in its own kind of structure, depending on the type of content it manages.

### Folders

Some tools, such as Documents, Tasks, and File Releases, can be thought of as folders that contain individual items, subfolders, or both.

For example, the Documents tool has a Root Folder, inside which you can create a tree of subfolders to organize your documents according to your project's needs. Every document lives inside one of these folder.

  {% include note.html content="This works the same way regardless of the name of the root folder. For example,in the Tasks tool, the root folder is called the Tasks Summary, and in the Discussions tool, the root folder is called the Forum Summary." %}

In a project that has been in use for any significant time, users have probably created some number of documents, which they have shared by adding them to a folder in the Documents tool. When you create a project template from that project, you can choose to include those documents in the project template or not.

  * If you choose to include the documents in the template, those documents will appear in any new project that is created using that template.
  * If you do not include the documents in the template, new projects based on that template will include the Documents tool, including the root folder and its sub-folders, but none of the documents that existed in the original project.

### Not Folders

The Reports and Wiki tools are not organized in folders. When you include the content from these tools in a template, new projects created from that template include a flat collection of all the Wiki pages or reports in the original project, with all their text and data.
{{site.data.alerts.hr_shaded}}

## Why do I get 'Name is Invalid' error when trying to create a project using createProject() method via the SOAP API?

You need to pass certain default parameters to createProject() method.

The default parameters that can be passed to createProject() method are:

```shell 
(sessionId, name, title, description)
where, name = URL Name [in UI]
title = Project Name [in UI]
````
       
In TeamForge, URL Name ['name'] accepts only lower case and the numeric characters. If the value of 'name' contains any other character than the aforesaid, user will end up seeing the 'Name is Invalid' error and the project creation would fail.
{{site.data.alerts.hr_shaded}}

## Why do I get a TeamForge system error in the project template creation page?

This may be because of a few stale permissions in the project in which you are trying to create the template.

You can resolve this by identifying and deleting the stale records using this SQL.

```shell
select role_id from role_operation ro left outer join ia_project_association ia 
on (ro.resource_value = ia.id) where ia.id is null and resource_value like '%prpl%' ;
````

```shell
select role_id from operation_cluster ro left outer join ia_project_association ia 
on (ro.resource_value = ia.id) where ia.id is null and resource_value like '%prpl%' ;
````
{{site.data.alerts.hr_shaded}}

## How does TeamForge support dynamic planning?

TeamForge helps you maximize your team's effectiveness by keeping you in close touch with the multiple moving targets facing your project.

In a development project, each piece of the picture constantly changes in response to changes in the other parts. As you continue to iterate through the process, a feedback loop like this takes shape. (Click a node for more detail.)

The new Dynamic Planning features in TeamForge 18.0 give you a more open and extensible platform that integrates and centralizes the software development tools necessary in modern application life cycles.

 {% include note.html content="The Dynamic Planning features helps you effectively utilize Agile­-like processes, but you can use any process model you like." %}

### Tracker summary screen

TeamForge incorporates a new Tracker Summary screen display to accommodate planning folders, tree­views, and multiple tracker viewing. The Tracker Summary section is available at the top of the screen with summaries of open and closed artifacts as well as a summary of open artifacts by priority. The Planning Folders section is located at the bottom of the Tracker Summary screen. This section includes summaries of open and closed artifacts, a summary of open artifacts by priority, and a summary of Effort for each planning folder.

### Tree view

TeamForge incorporates an expandable and collapsible tree­ view of the planning folder hierarchical structure to display parent/child relationships of artifacts.

The tree ­view allows for the viewing of artifacts in a hierarchical structure and displays parent/child relationships across multiple trackers.
{{site.data.alerts.hr_shaded}}

## How can I make the project pages invisible for any user who is authorized to see the project?

This can be customized by a Project Administrator.

The Project Administrator can set this using these steps:

 1. Click the link **On** next to Configure, on the top right-hand side of the project home page.

 2. Scroll to the page you want to hide and click the **Edit Properties** icon. This can be found on the right side of the title bar for the page you want to edit, next to **Edit** or **Create** buttons. The tooltip displays if you hover over the tool.

 3. Choose **Hidden - Visible only to project administrators in configure mode**.

 4. Click **Save**.

{{site.data.alerts.hr_shaded}}

## How do I put a notice to my users on the project home page?

To do this you will need to create a news item within the project. News items are posted and displayed on the project home page. News items are also displayed on the TeamForge home page.

To post a news item:

 1. Navigate to the home page of the project in which you want to post the news item.

    * From within the project, click **Project Home**.

    * From anywhere in TeamForge, choose the project from the list pf projects available under **My Workspace > My Projects**.

 2. In the Project News section, click **Add**. The **Create News Post** page is displayed.

 3. Enter a title for the news item.

 4. Enter the text for the news item in the message field (up to 4000 characters including spaces), then click **Add**.

The news item is submitted. It is displayed on the project home page and the TeamForge home page immediately.
{{site.data.alerts.hr_shaded}}

## How do I remove a news item?

You can delete any news item that you no longer want displayed on the project home page. Deleting a news item from a project also deletes it from the TeamForge home page.

To delete a news item:

 1. Navigate to the project home page.

 2. From within the project, click **Project Home** in the project navigation bar. From anywhere in TeamForge, choose the project from the **Projects** menu in the navigation bar.

 3. In the **Project News** section, click **Delete** next to the news item that you want to delete. When prompted, confirm that you want to delete the news item, and it will be deleted.

{% include links.html %}