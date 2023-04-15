---
title: Manage User Groups
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license]
sidebar: teamforge_sidebar
permalink: manageusergroups.html
last_updated: Mar 5, 2018
summary: To manage multiple users at once, create a group and add users to such user groups.
---
## Create a User Group
To manage multiple users at once, create a group that represents them.

1. Go to **My Workspace > Admin**.
2. Select **USER GROUPS** from the **Projects** menu.
3. Click **Create** and provide a name for the group and a description of its purpose.
   {% include note.html content="If your project is a child of another project, it may have inherited one or more user groups from its parent project. To work with inherited users and user groups, you must go to the project that they belong to." %}
4. Click **Create**.

## Add a User to a User Group
Put together multiple users who share characteristics in a user group.

1. Go to **My Workspace > Admin**.
2. Select **User Groups** from the **Projects** menu.
   {% include tip.html content="In TeamForge 18.1 and later, **Groups** (in earlier versions of the product), has been renamed to **User Groups** to better distinguish user groups from project groups." %}
3. Under **User Groups**, click the group to which you want to add the user.
4. On the **Edit Group** page, click **Add**.
5. Use the picker to move users into the group, and click **OK**. You can select the inherited project members also from the list.
6. Click **Return**.

## Find a User's Groups
You can get a consolidated view of all user groups, which a user is a member of.

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. On the **Users Details** page, click the **USER GROUP MEMBERSHIP** tab.
   
   The groups listed on this tab are the groups that this user is a member of.

## Edit a User Group
1. Go to **My Workspace > Admin**.
2. Select **User Groups** from the **Projects** menu.
3. Under **Groups**, click the group's name you want to edit.
4. Click **EDIT**.
5. Make your changes and click **Update**.

{% include links.html %}