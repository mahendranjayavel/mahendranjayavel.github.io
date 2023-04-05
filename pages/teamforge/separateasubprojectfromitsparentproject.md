---
title: Separate a Subproject from Its Parent Project
keywords: projects, project, approve, lock, unlock, create, rename, delete, templates, categories, parent, child, subproject
tags: [projects, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: separateasubprojectfromitsparentproject.html
last_updated: Mar 2, 2018
summary: When a subproject grows beyond its original scope, you may want to make it stand-alone project or move it to a different project hierarchy. By removing the association with a parent project, you can manage the subproject as a separate project.
---
{% include note.html content="Only one parent project can be selected for a subproject. However, the parent project can be changed or removed, as required." %}

1. Click **PROJECT ADMIN** from the **Project Home** menu.
2. On the **Project Settings** page, click **Edit Parent**.
3. Change the parent project as required. 
   
   You can be a project administrator or a site administrator to change or remove a parent project. As a project administrator, you can remove or change a parent project only if you have administrator permissions for both the projects that are being linked.
   {% include note.html content="A parent project can be removed or changed only when its members, user groups and roles are not in use in any other project. In other words, you can not remove/change a parent project while its members, user groups or roles are in use in any other project." %}
4. On the **Choose a Parent Project** page, select the desired parent project and click **Update**.
   {% include note.html content="If the project hierarchy exists, the project and its subprojects are moved only under the project from which members, user groups or roles are inherited. If project hierarchy does not exist and no inheritance is in use, the project is made a `Root` project." %}
5. Click **Remove Parent** in the **Project Settings** page to remove the association with parent project.
6. On the pop-up message box, click **OK**, if you wish to make the project a `Root` project.
   
   The project hierarchy is changed or removed in accordance with role based access control and inheritance rules.

{% include links.html %}