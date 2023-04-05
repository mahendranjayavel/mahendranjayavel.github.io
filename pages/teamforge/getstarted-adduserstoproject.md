---
title: Add Users to a Project
keywords: add users
tags: [project_admin_tasks, role_based_access_control, users, projects, users]
sidebar: teamforge_sidebar
permalink: getstarted-adduserstoproject.html
last_updated: Feb 6, 2018
summary: Before a person can work on a project, you have to make him a member of the project.
---
You can make any registered user on your TeamForge site a project member. You can assign roles to the user at the same time.
{% include note.html content="Project members, roles and the associated permissions can be inherited via project hierarchy and reused in subprojects. If your project is a subproject of any other project, you may have inherited some roles, project members or user groups." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **User Membership** from the **Project Admin** menu.
3. Click **Add**.
4. On the **Add Users** page, find the users you want by one of these methods:
   * Under **FIND USERS**, filter the list of site users eligible to join this project. You can filter by full or partial name or user name.
     {% include callout.html type="primary" content="Search text is not case-sensitive." %}
   * Browse the list of registered users on the site. Sort them by name, user name, email address or membership status.
     {% include callout.html type="primary" content="The inherited project members continue to hold the inherited roles with corresponding permissions, as specified in the source projects. If a site has a great many users, you must filter them first to narrow down the list. This helps avoid slowing down the system." %}
5. Select the users you want to add.
6. Under **Assign Roles**, select the roles you want the users to have.

   You can select any global project role, role created just for this project, or inherited role that is available.

   {% include callout.html type="primary" content="If your project is a child project of another project, the members of the parent project become inherited members of your project. The user roles specified in the parent project are available in your project provided the role inheritance is not prevented. If you assign a role in your project to a user, that user becomes a direct member of your project." %}

   {% include callout.html type="primary" content="If you prefer, you can skip this step and assign roles later on the **Project Admin > Permissions** page. Note that using the **Assigned Project Members** page, you can assign roles only to the direct project members." %}

7. Save your changes.
   * Click **Save** to return to the **User Membership** page.
   * Click **Save and Add More** to keep adding users.

{{site.data.alerts.hr_shaded}}
#### Related Links
* [Remove a User from a Project][projectadmin-removinguserfromaproject]
* [Handle a Request for Project Membership][projectadmin-handlingarequestforprojectmem]
* [Handle a Request to Leave a Project][projectadmin-handlingarequesttoleaveaproj]

{% include links.html %}