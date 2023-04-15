---
title: Create a Project Template
keywords: project template, project templates, templates, creating project templates, how to create project template, how to create project templates, create project templates
tags: [project_admin_tasks, getting_started, projects, boards, project_templates]
last_updated: Apr 5, 2018
sidebar: teamforge_sidebar
toc: no
permalink: creatingaprojecttemplate.html
summary: To make it easier to start projects, provide project templates based on existing projects.
---
A project template is used to populate new projects with the structure and configuration of the Source project. It can also include the actual content of the project it is based on, such as tasks, tracker items and documents.

When you create a project template, it is available only to projects on your own site. To make it available more widely, you can export the project template and share it with others. Ask your CollabNet representative for more information about doing this.

{% capture templatenotes %}
The access settings for a project template are the same as the access settings for the project on which the template is based. For example: <br><br>
  {% include inline_image.html file="status-success-small.png" %} If you create a template from a project that has hidden applications, any project you create from that template will have the same applications hidden.<br><br>
  {% include inline_image.html file="status-success-small.png" %} If you create a template from a project that is private, any project created from that template will also be private.
{% endcapture %}
{% include callout.html type="primary" content=templatenotes %}

1. Set up the project that will serve as the basis for the new project template.
   {% include tip.html content="If you need a clean project template, you may want to create a new project specifically for this purpose." %}
2. Click **Project Admin** from the **Project Home** menu.
3. On the **Project Settings** page, click **Create Project Template**.
4. Write a name and description for the template.
   {% include tip.html content="Consider the uses that you or other project managers might have for this project template, and include keyworkds in your description that are related to those uses." %}
5. Every new project includes the following project related components. Choose the items that you want to make available in new projects that are created from this template.

   * **Trackers** component into which you can add new trackers.
     {% include note.html content="When you select **Artifacts and their dependencies** from optional content, it copies the artifacts along with their associated tags." %}
   * **Planning Folder** into which you can add new planning folders.
   * **Tasks** into which you can add more task folders and tasks.
   * **File Releases** into which you can add packages and releases.
   * **Documents** folder into which you can add more document folders and documents. 
   * **Wiki** into which you can add wiki pages  to share project informaiton.
   * **Discussions** into which you can add discussion forums and respective discussions.
   * **Teams** into which you can add project teams and the members.
   * **Task Board** which you can configure to see a set of tasks for each project.
   * **Kanban Board** which you can configure to see different stages of your project development activities, specify workflow constraints for each state and map them to your tracker statuses. 

   If you wish, you can include the actual project components from the current project's components.
6. Click **OK**.

The project template is created. The template is available to all users who have the required permission to create new projects. When the templates are used, the number of projects associated to individual template is displayed in the **projects created** field.

The template name and description appear on the _Template_ tab of the **Projects** list, accessible from your personal navigation bar.

#### Related Links

 * [What is a project template?][conceptsandterms-faqs.html#whatisaprojecttemplate]
 * [What is in a project template?][conceptsandterms-faqs.html#whatisinaprojecttemplate]

{% include links.html %}