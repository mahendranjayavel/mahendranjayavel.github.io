---
title: Add a Parent Project to Your Project
keywords: parent, project, child, subproject, add
tags: [projects, project_admin_tasks]
last_updated: Apr 5, 2018
sidebar: teamforge_sidebar
folder: teamforge
permalink: addparentproject.html
summary: You can coordinate work among multiple projects; enable the user, user group and role inheritance by adding a common parent project to several projects.
---
A parent project is the base from which a subproject's members, user groups and roles, with their corresponding permissions, are derived. A subproject can inherit project members, user groups and roles from its parent project.

You can create a parent project to track and manage several smaller assignments as subprojects.

When you define users and roles with specific permissions in a project, those users and roles are passed down to any subprojects that belong to that project. This helps you avoid the repeated effort of defining users, user groups and roles across projects.

{% capture addparentprojectnotes %}
{% include inline_image.html file="status-success-small.png" %} A subproject can have only one parent. You can change or remove that at any time. <br><br>
{% include inline_image.html file="status-success-small.png" %} You must be a project administrator or site administrator to add, edit or remove the parent projects.
{% endcapture %}
{% include callout.html type="primary" content=addparentprojectnotes %}

1. Click **Project Admin** from the **Project Home** menu.
2. On the **Project Settings** page, click **Add Parent**.
3. Choose a parent project that it makes sense for your project to belong to, and click **Update**.
   {% include note.html content="You cannot add a parent project for the `Look` project as it is a special project in itself." %}

{% include links.html%}   
  