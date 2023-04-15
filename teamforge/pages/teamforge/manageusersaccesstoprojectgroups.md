---
title: Manage User Access to Project Groups
keywords: project groups, group
tags: [ctf_20.2, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: manageusersaccesstoprojectgroups.html
last_updated: Jul 13, 2020
summary: As a project group administrator, you know that the key to any user's access to the project group and the projects belonging to the group, is in the role you assign to the user. You can do almost all the role-related activities with project groups that you could do with individual projects.
---
You can create site-wide roles and assign the users to those roles and then bring them into your project group. You can create roles specifically for your project group and assign users to those or use global project roles, as required. The permissions inherited through the assigned roles are subject to the "Prevent Inheritance" option setting done while creating the roles.

### Give a Role to Project Group Members
A role can be assigned to many project group users at once.

While the user-role matrix provides a convenient way to add project group members to a role, it can become unwieldy if the project has a large number of users or roles. When that is the case, try assigning roles to multiple project group users at one time.
1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. On the **Roles** tab, click the **Global Project Roles** or **Roles Created For a Project** option of **View**, to display existing global roles or roles created just for this project.
6. Click the name of the role that you want to assign to project group members.
7. On the **Edit Role** page, click the **Assigned Users** tab. The **Assigned Users** page shows all users who currently have the role.
8. Click **Add**.
9. In the **Find a User** window, select the project group members you want to add, and move them from the **Found Users** list to the **Selected Users** list.
10. Click **Add** to move selected users.
11. Click **Add All** to move all users.
    {% include note.html content="You can search by full or partial user name or full name to find the desired project group members." %}
12. Click **OK**.
    
    The project group members are now assigned the role.

### Give Roles to a Project Group Member
A project group member can have any number of roles. As project group administrator, you must assign each project group member's roles with care. The roles would impact not just an individual project, but would also grant same permissions across the projects in a project group.

Permissions are cumulative. The project group member has all of the access permissions allowed by all of the assigned roles, plus any permissions that may have been assigned globally using application permissions.
1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. Click the **User-Role Matrix** tab.
   Observe the users listed on the left and all the available roles (global and direct) on the right. Users can be assigned global roles and roles created just for this project.
6. Select roles for each project member.
7. Click **Save**.
   
   The roles are now assigned to each project group member.

### Assign roles in multiple projects to a user group
Project managers can assign a role to multiple users at once by assigning the role to a user group that contains all those users. As a site administrator, you can do the same thing across multiple projects, by treating the projects as part of a project group.

1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. On the **Project Group** page, click **Permissions**.
4. On the **User Group-Role Matrix** tab, add the user group you want, then select the roles you want to assign to that user group.
5. Click **Finish** or **Finish and Add More**.
   {% include important.html content="When you give a group access to a Wandisco Subversion repository, members of the group can view the repository but cannot do repository actions, such as commit and update. You must assign those permissions to users individually." %}

### Assign User Groups to a Role
To manage permissions for a lot of groups or roles at once, try assigning user groups to roles.

1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. On the **Roles** tab, to display existing global or direct roles, click the global project roles or **Direct Roles** option of **View**. You can assign the project group users or user groups to a global project role or a role created just for this project.
6. Click the name of the role that you want to assign to the user group members in the project group.
7. On the **Edit Role** page, click the **Assigned User Groups** tab. The **Assigned User Groups** table shows all user groups who currently have the role.
8. Click **Add**.
9. Type some of the group’s name in the Name (search) box and click **Find**.
10. From the **Add User Group to Role** table, select the user groups that you want to add, and click **Finish**.
    {% include important.html content="When you give a group access to a Wandisco Subversion repository, members of the group can view the repository but cannot do repository actions, such as commit and update. You must assign those permissions to users individually." %}

### Create a Role in a Project Group
A role defines the applications that project group members with that role can use, and the specific things project group members can do in each application.

Any project groups administrator can create and assign a role. It is a good idea to check the existing global project roles before creating any new role for a project group.
Note: Any existing site-wide or global project role can be associated with a project group. It is advisable to check the permissions granted via a role before assigning it to users or user groups in a project group as it would impact more than a single project.
1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. On the **Roles** tab, click **View: Roles Created For this Project Group**.
   You can view global project roles by selecting **View: Global Project Roles** before creating a new role for this project.
6. Click **Create**.
7. On the **Create Role** page, write a name and description for the role.
8. To allow the inheritance of the role into private subprojects, clear the **Prevent Inheritance** check box.
   {% include note.html content="By default, the role inheritance into private subprojects is prevented. For example, you may not want administrator roles to be inherited in subprojects, until required. Selecting the option to prevent role inheritance does not affect public and gated projects." %}
9. Click **Create**. The role is created. The **Edit Role** page appears.
10. For each application listed on the **Role Permissions** page, select the permissions and resources you want to make available to users with this role.
    {% include note.html content="You can specify access to individual top-level folders, but not to specific subfolders." %}
11. Click **Save**.
    
    The role is created. You can assign it to project group members or user groups associated with the project group at any time.

### Edit a Role in a Project Group
As a project group administrator, you may need to update the permissions granted by a role being used across the projects.

While modifying a role, it is better to be cautious about granting more access than required by the users or a user group. In the case of project groups, as a role could be mapped across projects, consider being restrictive.
1. Go to **My Workspace > Admin**.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. On the **Roles** tab, click **View: Roles Created For a Project**. The existing roles created for this project are listed.
   You can view global project roles by selecting View: Global Project Roles, if required.
6. Select the role that you want to modify and click **Edit**.
7. On the **Edit Role** page, make the desired changes.
   
   You can update the role name, description and inheritance settings on clicking **Edit**.
   
   The role's permissions, assigned users or assigned user groups can also be modified as required.
8. Click **Save** after making the changes.
   The role in the project group is updated.

### Delete a Role in a Project Group
When you no longer need a role that you created for a project, it's a good idea to delete that role.

Any project groups administrator can create and assign a role. It is good to keep the project role tray as small and as manageable as possible.
{% include note.html content="Any existing site-wide or global project role can be associated with a project group. It is advisable to check the permissions granted via a role before assigning it to users or user groups in a project group as it would impact more than a single project." %}

1. Go to **My Workspace > Admin**.
2. Click **PROJECT GROUPS** from the **Projects** menu.
   The existing project groups are listed here.
3. Click your project group. The **Project Group Details** page appears.
4. From the left navigation pane, click the **Permissions** link to specify user roles applicable to the project group.
5. On the **Roles** tab, click **View: Roles Created For a Project**.
   You can view global project roles by selecting **View: Global Project Roles**. However, you can only delete roles created for this project here.
6. Select the role and click **Delete**. 
   
   You may get a warning message if the role you are trying to delete is in use. 
7. Click **OK** to proceed with deleting the non-required role. 
   
   The selected role is deleted.


{% include links.html %}