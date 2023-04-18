---
title: Give Project-independent Access for Project Tools
keywords: site admin tasks, additional administrators
tags: [site_admin_tasks, role_based_access_control]
sidebar: teamforge_sidebar
permalink: giveproject-independentaccessforprojecttools.html
last_updated: Mar 1, 2018
summary: To allow some Digital.ai TeamForge users to use one or more Digital.ai TeamForge tools across several projects, create site-wide roles with specific project permissions, minus site administrative permissions. Assign these site-wide roles to those who may need to access the project tools in any project.
---
For example, you may want a user to be able to use the "Tracker" across several projects. You don't need to create and assign a role supporting the task individually across all projects. Just do it one time as a site-wide role and assign it to the user.

1. Go to **My Workspace > Admin**.
2. Click **Roles** from the **Projects** menu.
3. Click **Create**.
4. On the **Create Site-wide Role** page, write a name and description for the role. The role name is case-sensitive.
5. To prevent inheritance of the role into private projects, select the **PREVENT ACCESS** option.
   {% include note.html content="Selecting the option to prevent role inheritance does not affect access to public and gated projects. On selecting Prevent access, the user may not be allowed to do project-permissions related tasks in private projects." %}
6. Click **Create**. The site-wide role is created. The **Edit Site-wide Role Permissions** page appears.
   {% include note.html content="You can select the permissions for applications and resources available across all projects." %}
7. Select the required project permissions listed on the **ROLE PERMISSIONS** tab, to match the tasks you want the user with that role to perform.
   {% include tip.html content="Select `Tracker-Create` permission if you want the user to be able to create new trackers." %}

   The role is created. You can assign it to site members at any time.



{% include links.html %}