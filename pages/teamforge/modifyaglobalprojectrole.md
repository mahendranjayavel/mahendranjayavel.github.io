---
title: Modify a Global Project Role
keywords: global project roles
tags: [site_admin_tasks, role_based_access_control]
sidebar: teamforge_sidebar
permalink: modifyaglobalprojectrole.html
last_updated: Mar 2, 2018
summary: You may need to add or remove certain permissions from an existing global project role to assign new tasks or change the access permissions given via the role.
---
{% include note.html content="Only site administrators or restricted site administrators with `Role-Edit` permission can edit global project roles." %}

1. Go to **My Workspace > Admin**.
2. Click **Roles** from the **Projects** menu.
3. Click the **GLOBAL PROJECT ROLES** tab. All the existing global project roles are listed here.
4. Select the role that you want to edit and click **Edit** or just click the hyperlinked role name. The **Edit global project role permissions** page appears.
5. Click **Edit** to make changes to the role details.
6. Modify the **Role Name** or **Description**, if required. The role name is case-sensitive and must not be the same as a site-wide role.
7. Change the inheritance setting to prevent or allow inheritance of the role's permissions into private sub-projects.
8. To make the role requestable or non-requestable, change the Project members can request this role setting. Project members can submit requests for `Available upon Request` roles. For a project, the project administrators can set a `Available upon Request` role to be automatically granted to the project member requesting it.
9. Click **Update**. The global project role is modified.
10. Select the application permissions that are relevant to the role, from those listed on the **ROLE PERMISSIONS** tab and click **Save**.
    {% include tip.html content="You may want to restrain removing project or application administration permissions as the change impacts existing users too." %}

    The role is modified.

{% include links.html %}