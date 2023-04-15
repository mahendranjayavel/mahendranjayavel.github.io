---
title: Control Project Access - Create a Role Based Access Control (RBAC)
keywords: control project access, roles, rbac, pbp, path based permissions
tags: [ctf_20.2, project_admin_tasks, role_based_access_control, license, projects, path_based_permission]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jul 13, 2020
layouts: "pagefaqs"
permalink: projectadmin-controllingprojectaccess.html
summary: To control who can access your project, consider the purpose of your project and the appropriate type of user.
---

## Control Access by User Role

Project administrators use existing global project roles or create and assign roles to project members to define what those project members can do in the project.

If you choose to use existing global project roles, you can quickly assign relevant roles to your project members. It is a good practice to create a new role in your project only when a suitable global project role is not available.

 {% include note.html content="If your project is a subproject of any other project, your project may have inherited some roles from the parent project. To work with the properties and permissions associated with inherited roles, you must go to the parent project where those roles are specified." %}

### Create a User Role {#createuserrole}

A role defines the applications that project members with that role can use, and the specific things project members can do in each application.

Any project administrator can create and assign a role.

 {% include tip.html content="It is a good idea to check the existing global project roles via `Project Admin > Permissions > Roles > View: global project roles` before creating any new role in a project." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**.

 3. On the _ROLES_ tab, select **View: Roles Created For a Project**.

 4. Click **Create**.

 5. On the **Create Role** page, write a name and description for the role.

 6. To let this role be automatically added to any private subprojects of this project, clear the **PREVENT INHERITANCE** option.

    By default, roles are inherited by public and gated subprojects, but not private subprojects.

     {% include tip.html content="If this project is a subproject of any other project, you may already have inherited some roles." %}

 7. To allow project members to be able to request this role, select **PROJECT MEMBERS CAN REQUEST THIS ROLE**. Project members can submit requests for requestable roles, which the project administrator can approve or reject.

    {% include tip.html content="Select GRANT AUTOMATICALLY ON REQUEST to skip the need to approve or reject a request." %}

 8. Click **Create**. The role is created. The **Edit Role** page appears.

 9. For each application listed on the **Role Permissions** page, select the permissions and resources you want to make available to users with this role.

    {% include tip.html content="You can specify the permissions for Binaries and integrated applications here too." %}
    {% include note.html content="You can specify access to individual top-level folders, but not to specific subfolders.However, in the case of documents, you can specify access to individual subfolders as well." %}

10. Click **Save**.

The role is created. You can assign it to project members at any time.

 {% include tip.html content="Based on the earlier settings, a project member may be able to submit a request for the role." %}

### Create a Project Administrator Role

The project administrator is responsible for managing the project's users and roles.

The project creator is assigned the Founder Project Admin role, a special role granting all project and application administration permissions for the project. You can transfer the Founder Project Admin role to another user.

If the project creator is a Digital.ai TeamForge administrator, no Founder Project Admin is created.

 {% include note.html content="By default, project adminstrators do not have application administration permissions, such as Tracker Admin or Task Admin. Application administration permissions can be included in a project administrator role, but must be assigned separately." %}

 1. On the **Role Permissions** page, select **Project Admin Permissions**.

    {% include note.html content="If this is an inherited role, you can not edit the permissions associated with it. You can edit the project members and user groups to whom this inherited role is assigned." %}

    * If you want the role to contain only the project administrator permissions to manage users and roles, **Project Admin Permissions** is all you need to select.

    * If you want the role to contain additional application administration or other permissions, check the additional permissions.

 2. Click **Save**.

 All project members assigned this role have project administrator permissions to manage the project's users and roles.


### Change a Role

 If users need to do things that are not allowed by a role you have assigned to them, you may need to change the permissions associated with that role.

When you edit a role, all project members with that role get the updated permissions automatically.

 {% include note.html content="If your project is a subproject of any other project, your project may have inherited some roles from the parent project. To work with the properties and permissions associated with inherited roles, you must go to the parent project where those roles are specified." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin** menu, click **Permissions**.

 3. From the list of roles created for this project, click the role you want to edit.

    {% include note.html content="You can assign a role to direct project members and user groups of the project regardless of whether the role belongs directly to this project or is inherited from a parent project." %}

 4. On the **Role** page, make the changes you need.

    * To edit the title or other role details, click **Edit**. Make the required changes and click **Update**.

    * To edit the role's permissions, choose an application from the left side of the page and select or deselect permissions and resources.

    * To edit the project members to whom the role is assigned, click **Assigned Project Members**.

    * To edit the user groups to whom the role is assigned, click **Assigned Groups**.

 9. Click **Save**.

The role is modified.


### Give Roles to a Project Member

A project member can have any number of roles. As project administrator, you must assign each project member's roles.

Permissions are cumulative. The project member has all of the access permissions allowed by all of the assigned roles, plus any permissions that may have been assigned globally using application permissions.


 {% include note.html content="If your project is a subproject of any other project, you may have inherited some roles, project members or user groups from the parent project. You can assign any role to any project member, regardless of whether it's a global project role, or the role belongs directly to the project, or is inherited from a parent project." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**, then click the _User-Role Matrix_ tab. Observe the users listed on the left and all the available roles (global, direct and inherited) on the right.

    {% capture projectmemberrole %}
    Users can be assigned global, direct and inherited roles. Inherited users have all the permissions that they have in the parent project. <br><br>
    {% include inline_image.html file="status-success-small.png" %}If you assign another inherited role to an inherited user, that user gets both the roles. <br><br>
    {% include inline_image.html file="status-success-small.png" %} If you assign a role to a user in a project, that user becomes a current member in that project.
    {% endcapture %}
    {% include callout.html type="primary" content=projectmemberrole %}

 3. Select roles for each project member.

    {% include note.html content="A user's license type also influences what the user can see and do on your site. A user's license type supersedes any role assignments. Ask your site administrator how many licenses of each kind are available for your users. For more information, see [How do TeamForge Licenses Work?][teamforgelicense]." %}

    The **USER_ROLE MATRIX** page is also equipped with a smart search (filter) function that makes it easy to filter a user by name and assign roles. Use it to quickly search for a user to which you want to assign one or more roles.

     {% include image.html file="1610_userrolematrix.png" %}

 4. Click **Save**.

The roles are now assigned to each project member.

### Give a Role to Multiple Project Members

A role can be assigned to many users at once.

The user-role matrix provides a convenient way to add project members to a role, but it can become unwieldy if the project has a large number of users or roles. When that is the case, try assigning roles to multiple users at one time.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**.

 3. Click the name of the role that you want to assign to project members.

 4. On the **Role Permissions** page, click the _Assigned Project Members_ tab. The **Assigned Project Members** page shows all users who currently have the role.

    {% include tip.html content="You can assign the role only to the direct project members of the project." %}
    {% include note.html content="A user's license type also influences what the user can see and do on your site. A user's license type supersedes any role assignments. Ask your site administrator how many licenses of each kind are available for your users. For more information, [How Do TeamForge Licenses Work?][teamforgelicense]" %}

 5. Click **Add** and use the **Find a User** window to move your desired users into the **Selected Users** list.

    {% include tip.html content="You can search by full or partial user name or full name to find the right project members." %}

 6. Click **OK**.

The project members are now assigned the role.

### Handle a Role Request from a Project Member

A project member in Digital.ai TeamForge can ask to be granted a role. As the project administrator, it's up to you to approve or reject such requests.

When a Digital.ai TeamForge project member submits a request for a role in a project, the request is placed in the **User Membership** section of the **Project Administration** page, pending approval by a project administrator. The request is also displayed in the **Items Pending My Approval** section of each project administrator's **My Page**.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **User Membership**, then click the _Pending Requests_ tab.

 3. Under **Role Requests**, select the user whose role request you want to approve or reject.

    * Click **Approve** to approve the request and assign the role to the user.

    * Click **Reject** to deny the request.

    {% include tip.html content="To view the permissions granted via the role, click the role name, if required." %}
    {% include note.html content="Before approving or rejecting a role request, you can check the roles already assigned to the user by clicking the user name and selecting the _Roles_ tab." %}

The user receives an email notification when the request is approved or rejected.


### Assign a Global Project Role on Request

As a project administrator you can edit a requestable global project role for your project. You can update the settings to immediately assign the role to a project member on request.

 {% include note.html content="Note: Only site administrators or restricted site administrators with `Role-Edit` permission can edit global project role details. Project administrators can only edit requestable global project role's grant settings for their projects." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**.

 3. From the list of global project roles, click the requestable global project role you want to edit.

 4. On the **Edit Role** page, click **Edit**.

 5. Select the **Grant Automatically on Request** option and click **Save**. Selecting this option enables the project member requesting the role to be assigned the same immediately, without waiting for an approval.

The role is modified for your project.


### Assign Roles to a User Group

Enable multiple users to do something all at once by giving their group a role.

A user group can have any number of roles. Each member of the user group has all the access permissions allowed by all of the assigned roles, plus any permissions that may have been assigned by other methods, such as application permissions or individually assigned roles.

Roles and the associated permissions can be inherited. If your project is a subproject of any other project, you may have inherited some roles or user groups. You can assign any inherited role to any user group.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin** menu, click **Permissions**, then click the _Group-Role Matrix_ tab. Observe the user groups listed on the left and all the available roles (global, direct and inherited) on the right.

    {% capture usergrouprole %}
    User groups can be assigned global, direct and inherited roles. The inherited user groups have all the permissions that they have in the parent project. <br><br>
    {% include inline_image.html file="status-success-small.png" %}If you assign another inherited role to an inherited group, the members of that group get both the roles. <br><br>
    {% include inline_image.html file="status-success-small.png" %} If you assign a role to a user group in a project, that user group becomes a direct user group in that project.
    {% endcapture %}
    {% include callout.html type="primary" content=usergrouprole %}

 3. Select the roles you want for each user group and click **Save**.

    {% include restriction.html content="When you give a group access to a Wandisco Subversion repository, members of the group can view the  repository but cannot do repository actions, such as commit and update. You must assign those permissions to users individually." %}

The roles are now assigned to each user group.

### Assign User Groups to a Role

To manage permissions for a lot of groups or roles at once, try assigning user groups to roles.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**.

 3. To display existing global, direct or inherited roles, click the **Global project roles**, **Roles Created For a Project** or **Roles Inherited From Parent Project** option of **View**.

    {% include note.html content="If your project is a subproject of another project, you may have inherited some roles or user groups. The inherited role details like role name, description and the source project name are listed." %}

    You can assign direct user groups to a global/direct/inherited role.

 4. Click the name of the role that you want to assign to user groups.

 5. On the **Role Permissions** page, click the _Assigned Groups_ tab. The **Assigned Groups** page shows all user groups that are currently assigned the role.

    {% include tip.html content="You can assign the role only to the direct user groups of the project." %}

 6. Click **Add**.

 7. Type some of the group’s name in the **Name (search)** box and click **Find**.

 8. In the **Find a user group** window, select the user groups that you want to add, and click **Finish**.

    {% include restriction.html content="When you give a group access to a Wandisco Subversion repository, members of the group can view the repository but cannot do repository actions, such as commit and update. You must assign those permissions to users individually." %}

The user groups are now assigned the role.

### View Users and User Groups Assigned to a Role

Before adding a role to a project member or user groups, see all the users and user groups who are assigned that role through inheritance.

A user or user group can have any number of roles. Roles and the associated permissions can be inherited via project hierarchy or project groups.

 1. Click **Project Admin** from the **Project Home** menu.

 2. On the **Project Admin** menu, click **Permissions**.

 3. In the **View** drop-down, select **Global project roles** and from the results, a specific role.

 4. In the _Assigned Project Members_ tab, click the **View** drop-down and make a selection.

    * **Direct Members** displays the users who are directly assigned the role in the project.

    * **Inherited Members** displays the users who inherit the role from parent projects as well as project groups.

 5. In the _Assigned Groups_ tab, click the **View** drop-down and make a selection.

    * **Direct User Groups** displays the user groups that are directly assigned the role in the project.

    * **Inherited User Groups** displays the user groups that inherit the role from parent projects as well as project groups.

The roles are now assigned to each user group.

## Control Access by User Class

To avoid having to create and assign a lot of similar roles for individual users, give access to applications to whole classes of users whenever possible.

For each application (tasks, documents, file releases, trackers, and discussion forums), you can assign permissions globally based on user type.

For example, if you know that you want all project members to be able to view and submit to all project trackers, set the application's permissions to reflect this. You need to configure these settings only once.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin** page, configure your project access settings and click **Next**.

 3. On the **Edit Default Access Application Permissions** page, click the `+` symbol to expand the section for which you want to assign permissions.

 4. For each application and resource, choose a user type from the drop-down menus.

    * All users of the selected type will have the specified permissions: `view`, `submit/view`, or `post/view`.

    * For discussion forums and trackers, you can also specify submit or post permissions.

    {% include note.html content="You can specify access to top-level folders, but not to specific subfolders." %}

    {% include note.html content="If you want to control access to an application or resource that is not displayed on the **Edit Default Access Application Permissions** page, you can do so using role-based access control." %}

 5. Click **Finish**.

## Control Access by Project Type

Projects can be open only to project members, open to everyone in the world, or something in between.

By default, all new projects are created as private projects, accessible only to project members. Your system administrator can change the default access level for new projects.

 {% include important.html content="Users who do not have access to a project cannot see it on the Home page, in the **All Projects** list, or in search or reporting results." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**, then click the _DEFAULT ACCESS PERMISSIONS_ tab to see the project's current access setting.

 3. Click **Edit**.

 4. On the **Edit Default Access Permissions** page, select the kind of access you want to allow to your project.

    * **Private** - Project members only.

    * **Gated community** - Project members and unrestricted users.

    * **Public** - All users.

    {% include note.html content="If the option is not available, your system administrator has prohibited changing the access levels of projects on the site." %}

## Allow Users to See Other Users' Roles

You can enable some project members to view the roles assigned to other project members.

For example, if your project includes both core team members and consultants, you may want to restrict full visibility of user details to the core team members.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**.

 3. On the _ROLES_ tab, click the role you want to edit. For example, if you have divided project members into a "Core Team" role and a "Consultant" role, click the "Core Team" role.

 4. Under **Project Admin Permissions**, select **View User Membership**.

Now only project members who have the role you edited can see the roles held by other project members.

 {% include note.html content="They still can't see the actual permissions included in those roles, unless they have Project Admin status." %}

## Lock or Unlock a Project

To ensure that no changes occur in a project while you are collating or migrating project data, lock the project. You must have project administration permissions or be a site administrator to lock or unlock a project.

To lock or unlock a project in TeamForge, go to **Project Settings** and lock/unlock the project.

 {% include note.html content="A locked project does not allow any member (including project administrators and site administrators) to make any changes to the project. Besides that, a locked project can not be set as the parent project for any other project and tasks like adding, editing or deleting integrated applications are also not allowed." %}

 Click **PROJECT ADMIN** from the **Project Home** menu.

 The project is locked or unlocked as desired. The lock ( {% include inline_image.html file="Lockedproject.png" %}) icon appears on all the project pages while the project is locked.

  {% include note.html content="If a locked project has an integrated application, for example, project tracker, all the project tracker pages are also non-editable while the project is locked. The user who has access permissions for the integrated application can only view the pages." %}

## Control Access to Source Code

It's a good idea to make sure your source code can only be used by people who have business with it.

You can control which users can view or commit source code. You can make these distinctions at the repository level or at the path level within a repository.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Settings** page, click **Permissions**.

 3. Click the role whose access to source code you want to control.

    {% include tip.html content="If the appropriate role does not exist, you must create it first. See [Create a User Role][projectadmin-controllingprojectaccess.html#createuserrole]." %}

 4. On the **Edit Role** page, click **Source Code**.

 5. Under **Permissions for Specific Repositories**, select a repository in the project and specify this role's access to the repository as a whole.

    * To block users with this role from seeing this repository at all, select **No Access**.

    * To allow users with this role to see everything in the repository but not commit to it, select **View Only**.

    * To allow users with this role to commit to any path in the repository, select **View and Commit**.

 6. If you want to control access to a specific path within the repository for users with this role, select **Path-based Permissions** (PBP).

    See [Who can Access Source Code?][sourcecode-faqs.html#sourcecodefaq1] and [Wildcard-based access control and path-based permissions (PBP) in TeamForge](http://blogs.collab.net/teamforge/wildcard-access-control-and-path-based-permissions-in-teamforge) for more information.

     1. Click **Add**.

     2. Specify a path in the repository.

         {% include tip.html content="The path does not have to exist when you specify it. You can set a permission for a path that may be created later." %}

     3. Select **No Access**, **View Only**, or **View and Commit** for this path.

        {% capture sourcecodenote %}

        {% include inline_image.html file="status-success-small.png" %} If none of the available permissions (**View Only**, **View and Commit**, or **Path-based Permissions**) is selected for any repository, and none of the options under **Source Code Permissions** is selected, users with this role do not see the **Source Code** toolbar button. <br><br>

        {% include inline_image.html file="status-success-small.png" %} If two paths have different permissions, the permissions on the lower-level path take effect. For example, consider a role that has "No Access" set for the path /branches/version3/users, but has "View and Commit" access to `/branches/version3/users/vijay`. <br>
        
        {% include inline_image.html file="status-success-small.png" %} Users with this role can: <br><br>

             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{% include inline_image.html file="status-success-small.png" %} Check code in and out of the vijay directory.<br><br>
             &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{% include inline_image.html file="status-success-small.png" %} Click down through all the directories in that path, including users. <br><br> 

        {% include inline_image.html file="status-success-small.png" %}Users with this role cannot check files in and out of the users directory or monitor commits to users.

        {% endcapture %}
        {% include callout.html type="primary" content=sourcecodenote %}

      
 7. Click **Save**.

    {% include note.html content="You can also restrict the information that goes out with commit notification emails. See [Who can Access Source Code?][sourcecode-faqs.html#sourcecodefaq1]" %}

## Control HTML Headers in Hand-coded Project Pages

When a HTML page that you created in Microsoft Word or Frontpage looks strange, you may be able to fix it by suppressing HTML head content.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.
 
 2. On the **Project Settings** section, select **Show custom web page** and then select **Preserve HTML head content**.

 3. Click **Save**.

Pages created in Microsoft Word or Frontpage should render correctly.

## Allow Anonymous Subversion Checkouts

To grant anonymous checkout access while restricting write access to a Subversion repository, set the project's default access permissions to public, provide Source Code View permission to all users, and limit other permissions to specific user classes.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Permissions**, then the _DEFAULT ACCESS PERMISSIONS_ tab.

 3. Click **Edit**.

 4. Choose the **Public** project access option on the **Edit Default Access Permissions** page and click **Next**.

 5. Under **Application Permissions** on the **Edit Default Access Application Permissions** page, choose **Allow all Site Users and Guests** from the drop-down for Source Code View permission.

    {% include note.html content="You can give all users checkout access to all repositories or a specific repository." %}

 6. For other application permissions, choose a user class based on your access requirement.

Users can now check out from a repository without entering a password.


## Show or Hide an Application

To help users focus on the relevant parts of your project, choose which applications they can see in the Project Home menu.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu** page, click **Tools**.

 3. Select the applications that you want to be visible to users in your project, and click **Save**.


Only the application buttons you have set to **VISIBLE** appear in the Project Home menu of the project page.

 * Removing buttons from this menu does not remove the application from the site. Users with the appropriate permissions can still get to the hidden applications by other means, such as clicking a link in an email. The hidden application button will not appear.

 * When an application button is set to **Visible**, but a given user does not have permission to use that application, that user still cannot see the application button. For example, if a user has a role that does not permit access to any source code repositories, that user does not see the **Source Code** toolbar button, even if the button is enabled for the project.

 * If the Tasks tool is hidden for a project, the option to run reports on the Task tool is also hidden.

 * If you create a project template from a project that has hidden applications, any project you create from that template will have the same applications hidden.

## Limit User Posts to Discussions by Email

To help reduce the risk of spam or other mischief, you may need to limit the users who can post to your project's discussion forums by email.

To leverage the advantages of community collaboration, you should keep your forums as open as you can. However, some projects require tighter control over who can participate in discussions. TeamForge enables you to balance openness against privacy along a spectrum of choices.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. Click **Discussion Settings**.

 3. Set the value of **EMAIL POSTING** to one of these choices (listed from most restrictive to least restrictive).

<table>
<tr>
<th>This option...</th>
<th>has this effect</th>
</tr>
<tr>
<td>
<b>Allow only forum admins</b>
</td>
<td>
Only users with the "discussion admin" permission can post by email.
</td>
</tr>
<tr>
<td>
<b>Users with roles & permissions</b>
</td>
<td>
Only registered users with the "topic post" permission can post by email. This is the default. (For discussions marked as private, this is the least restrictive setting possible.)
</td>
</tr>
<tr>
<td>
<b>All logged in users</b>
</td>
<td>
All users who are registered on the site can post by email.
</td>
</tr>
<tr>
<td>
<b>Allow known email addresses only</b>
</td>
<td>
Users can post by email only if they have explicitly been added to the monitoring list. (This can include people who are not registered site users.)
</td>
</tr>
<tr>
<td>
<b>All site users and guests</b>
</td>
<td>
Anyone can post by email.
</td>
</tr>
</table>

If you select a value that's more liberal than the value your site administrator has set for the site as a whole, the site administrator's setting rules. For example, suppose the site administrator has provided that only users with the appropriate role ("Users with roles & permissions") can post by email. If your project requires extra security, you can choose to accept email only from forum administrators. However, you cannot accept email posts from a less restrictive category of users, such as "All logged in users."






{% include links.html %}