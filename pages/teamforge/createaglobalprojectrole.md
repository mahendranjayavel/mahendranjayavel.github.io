---
title: Create a Global Project Role
keywords: global project roles
tags: [site_admin_tasks, role_based_access_control]
sidebar: teamforge_sidebar
permalink: createaglobalprojectrole.html
last_updated: Mar 2, 2018
summary: To help project managers get their project members set up quickly, provide ready-made project roles that any project on your site can use.
---
{% include note.html content="You need the `Role-Create` permission to create global project roles. All site administrators and some restricted site administrators have this permission." %}

1. Go to **My Workspace > Admin**.
2. Click **Roles** from the **Projects** menu.
3. Click the **GLOBAL PROJECT ROLES** tab. All the existing Global Project Roles are listed here. It is a good idea to check this list before you create another role.
   {% include note.html content="You can suggest that the project administrators check the **Project Admin > Permissions > Roles > View: Global Project Roles** list before creating any new roles in their projects." %}
4. Click **Create**.
5. On the **Create Global Project Role** page, write a name and description for the role. The role name is case-sensitive.
   {% include tip.html content="Remember that the role name can not be the same as a site-wide role name." %}
6. To allow inheritance of the role's permissions into private sub-projects, clear the **PREVENT INHERITANCE** check box.
7. To allow the project members to be able to request this role, select **PROJECT MEMBERS CAN REQUEST THIS ROLE**. Project members can submit requests for `Available upon Request` roles. For a project, the project administrators can set an `Available upon Request` role to be automatically granted to the project member requesting it.
8. Click **Create**. The new global project role is created. The **Edit global project role permissions** page appears.
9. Select the application permissions that are relevant to the role, from those listed on the **ROLE PERMISSIONS** tab.
   {% include tip.html content="You may want to restrain providing project or application administration permissions, until required." %}

   The role is created. The project administrators can assign it to their project members any time.

{% include links.html %}