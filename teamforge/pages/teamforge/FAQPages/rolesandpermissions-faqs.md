---
title: FAQs on Roles and Permissions in TeamForge 
keywords: FAQ, frequently asked questions
tags: [faq, role_based_access_control, projects]
sidebar: teamforge_sidebar
permalink: rolesandpermissions-faqs.html
last_updated: Jun 9, 2020
summary: These are some of the FAQs on the roles and permissions in TeamForge.
---


## Can I block a user's access to source code?

From time to time, you may need to prevent a user from using a source code repository.

SCM access can be withdrawn from a user by doing one of the following:

 * Change the user's access to specific paths in the repository. (Subversion only.)
 * Remove the role providing the desired source code permissions from the user.
 * Remove the user from the project.

How this works depends in part on whether the repository is managed by TeamForge. If the source control server that hosts the repository is managed by TeamForge, the user's access is removed immediately.

Both the project administrator and the user receive email notifications when the change is made.
{{site.data.alerts.hr_shaded}}

## Can I assign a role to all users of the site at once?

If you are a site administrator in Digital.ai TeamForge, you can assign a role to all the system users (non-site administrators) at one go.

Now, Digital.ai TeamForge provides a system created user group called "All Users", including all site users. All role assignments that can be made to a user group can be made even for the "All Users" user group.

 {% include note.html content="The `All Users` group members can not be manually added, edited, viewed or deleted. This group is automatically updated each time a user is added or deleted from the site." %}
{{site.data.alerts.hr_shaded}}

## Can I request a role?

If you are a project member in Digital.ai TeamForge, you can request a role in your project.

You can use the **Project Home > My Roles** page to request for a role. Your request is submitted to the project administrator for approval. You will receive an email notification when your request is either approved or denied.

 {% include note.html content="Based on your project administrator's discretion, some role requests may be granted immediately, while the other role requests may need approval." %}
{{site.data.alerts.hr_shaded}}

## Why don't I have access to the "Reported in Release" information in my artifact?

If you cannot see the "Reported in Release" information in your artifact, ask your project owner to add the role required to obtain access to this information.

Users with tracker artifact submit/view/edit permissions will not be able to see "Reported in Release" information in an artifact, as it is directly associated with the File Releases section.

You can request that the project owner add a role permission of View Only for All Packages in File releases for you to obtain access.
{{site.data.alerts.hr_shaded}}

## Who can access an application?

Application permissions help you minimize the need to create and assign many similar roles for individual users. Instead, you can permit or restrict access to individual applications within the project for whole classes of users.

Application permissions supplement role-based access control (RBAC.) For each application's concepts, documents, file releases, trackers, and discussion forums, you can assign permissions globally based on user type.

For example, if you know that you want all project members to be able to view and submit to all project trackers, you can specify this application permissions. You need to configure these settings only once. All current and future project members will be able to view and submit to all trackers without having the tracker view/submit permission assigned to them individually via a role.

Before you do this, you should have identified your project as private, gated community, or public. Configuring permissions is a finer-grained level of control that operates within this hierarchy of project types.

Some applications may be invisible to some users based on the roles you assign. If you give a user a role that does not grant access to a particular application, that user cannot see the button for that application in the Web interface. (However, if that user also has some other role that does grant access to that application, the user can see the application button.

 {% include note.html content="A user's license type also influences what the user can see and do on your site. A user's license type supersedes any role assignments. Ask your site administrator how many licenses of each kind are available for your users. For more information, see [How do TeamForge Licenses Work?][teamforgelicense.html#licenseframework]." %}


### Exceptions

* If a user has an SCM license, that user can see only the tools that support the core source control functions of the site. The Tracker, Documents, and Tasks tools are not visible.
* If a user has any level of permission on a tracker or a task folder, that user can see the **Reports** button.
* If a user has tracker administration permission on any tracker, or task administration in any task folder, that user can see the **Project Admin** button.

### User Classes

These are the classes of users to which you can assign application permissions:

<table>
<tr>
<th>User Class</th>
<th>Description</th>
</tr>
<tr>
<td>
	All users with Role Permissions
</td>
<td>
	Only project members with appropriate RBAC permissions.
</td>
</tr>
<tr>
<td>
	All project members
</td>
<td>
	All project members.
</td>
</tr>
<tr>
<td>
	All project members and unrestricted users
</td>
<td>
	All unrestricted users, whether or not they are project members, plus all project members.
</td>
</tr>
<tr>
<td>
	All logged-in users
</td>
<td>
	All restricted and unrestricted users (all logged-in users,) whether or not they are project members.
</td>
</tr>
<tr>
<td>
	All users
</td>
<td>
	All users, whether or not they are logged in or have Digital.ai TeamForge accounts.
</td>
</tr>
</table>

### Restrictions by type of site

On some types of sites, you can't assign application permissions to certain classes of users. In such cases, you must use role-based access control (RBAC) permissions.

 * On a private site, you cannot set application permissions for these classes of users:

   * All project members and unrestricted users
   * All logged-in users
   * All users

 * On a "Gated Community" site, you cannot set application permissions for these classes of users:

   * All logged-in users
   * All users
{{site.data.alerts.hr_shaded}}

## Can I delete an item if I have 'Administer' permission?

No. You cannot delete an item if you have the administer permission.

The administer permission does not allow you to delete an item. You can create, edit, submit, and view items if you have the administer permission. For deletion, you must have the delete permission.
{{site.data.alerts.hr_shaded}}

## Can I disable creation of user accounts?

As of TeamForge 4.1 SP3, it is possible to disable the creation of new accounts by users so that only a 'site admin' can create new users.

To enable this mode of operations, simply add the following line to `/opt/collabnet/teamforge/sourceforge_home/etc/sourceforge_configuration.properties`:

```shell
sf.disableUserSelfCreation=true
````

Once this line is in place, restart TeamForge for it to take effect.
{{site.data.alerts.hr_shaded}}

## Why do I see the project home page though I lack the necessary permission?

This has been set so that when users are provided access to a project, they do not see an empty page.

Irrespective of whether the view permission on project pages is checked, users will be able to see the contents in the project home page.
{{site.data.alerts.hr_shaded}}

## Why do you need the authentication and authorization plugin for Hudson?

The Authentication and Authorization plugin allows you to set up your Hudson installation to authenticate against a CollabNet server and specify access control for CollabNet users.

 {% include note.html content="Authentication and authorization are independent actions. You could set up your Hudson installation to authenticate against a SourceForge or TeamForge site, but not use that CollabNet site for authorizing users. Authorization is available only with Digital.ai TeamForge 5.2, but authentication is possible with earlier CollabNet SourceForge Enterprise versions as well." %}

### Authentication

Authentication determines user names and passwords. You establish user credentials when you enable your Hudson site to use the CollabNet security realm.

### Authorization

Authorization determines what users can do on the Hudson site.

Your Hudson server can be shared between many CollabNet projects, and you can grant TeamForge users permissions at the site level. You specify site-level permissions when you configure the site to use a CollabNet server for authorization.

A job on your Hudson server may be involved with more than one TeamForge project. For example, a job that builds software can pull in source code from multiple project repositories. For the purpose of authorization, however, each job is associated with one CollabNet project, and you can give users project-level roles.

When your Hudson site is set up to use CollabNet authorization, TeamForge project administrators can assign these roles to project members:

 * Hudson Build/Cancel
 * Hudson Configure
 * Hudson Delete
 * Hudson Promote
 * Hudson Read

Users get the highest permissions they are entitled to. For example, if a user is part of a group that has administration permissions for the Hudson site, that supersedes any Hudson-related role the user might be assigned within a specific CollabNet project.
{{site.data.alerts.hr_shaded}}

## Can I control user access to an integrated application?

TeamForge can integrate the permissions scheme of a separate application into the TeamForge role-based access control system.

To look at how this works, we'll use the Pebble blogging tool as an example. Pebble is an application that you can quickly integrate with TeamForge.

Pebble brings with it a set of pre-determined roles that you can assign to project users. The roles are defined in the XML application configuration file.

**Blog Reader**

You can only read blogs and make comments, the comments are sent for moderation.

**Blog contributor**

You can add blog posts, but they will be sent for moderation.

**Blog publisher**

You can add blog posts, moderate comments and blog posts.

**Blog owner**

You can do all that a Blog publisher does as well as change the blog properties and security options.

Any site user with one or more of these roles can see the **Pebble Blog** button in their project toolbar. Clicking that button allows them to operate Pebble according to their access rights.

 {% include note.html content="Note: Site Administrators don't need any specific permissions; they have all permissions on all projects on the site." %}
{{site.data.alerts.hr_shaded}}

## How does inheritance work?

Site or project administrators can create hierarchical relationships between projects so that one project can inherit members, roles and permissions from a parent project.

When you define users, user groups and roles with specific permissions in one project, they can be inherited in one or more subprojects. This helps you avoid duplicating the effort of defining users, user groups and roles across projects.

You can still, if required, create roles specifically for this project and add direct members to any project. The direct members can be assigned inherited roles. The inherited members can be made direct members and/or assigned direct/inherited roles too.

While inheriting roles, only the permissions associated with all (top-level) folders are inherited.

In a subproject, you can select the inherited project members from the **Assigned to** lists or from the user picker, as the case may be. Inherited users may not be part of these lists if their role inheritance was prevented in the parent project.

 {% include note.html content="At the time of role creation, you can choose to allow or disallow the role inheritance into private subprojects." %}
{{site.data.alerts.hr_shaded}}

## How does inheritance work for project groups?

Site or project administrators can create project groups and add member projects to the group, to manage several projects as a single unit.

Moreover, hierarchical relationships may exist between projects so that one project can inherit members, roles and permissions from its parent project.

Quite like a project can inherit roles and permissions from its parent project; projects can inherit only permissions via the project group.

Project Groups permissions when granted to users via site-wide roles, also allows the users to access project groups in all cases. Prevent inheritance option for roles does not apply in those cases.

The project in which a user gets permissions through role assignment in project groups appears on the **My Workspace > Projects > All Projects** page.

The roles created specifically for a project group are not made available as inherited roles in the group's member projects for assignment. Project group roles can only be assigned directly in the project group context. These roles are not requestable.
{{site.data.alerts.hr_shaded}}

## Can I create new user accounts as "unrestricted"?

You can make all new accounts be "unrestricted" by default instead of the more secure "restricted."

This is controlled by the _USER_ACCOUNT_RESTRICTED_ variable in the `site-options.conf` file. Change that value to `false` and restart runtime.

 {% include note.html content="This does not change any existing accounts. If someone was restricted before this flag was turned on, they remain restricted until the site admin edits their account." %}
{{site.data.alerts.hr_shaded}} 

## Why can't Oracle connect to my TeamForge installation?

The simplest way to correct this is to overwrite the `.jar` included with TeamForge with the one from $ORACLE_HOME.

TeamForge uses the thick Oracle JDBC driver, which has two parts. One of these is provided by TeamForge, the other is in $ORACLE_HOME. If these two components are incompatible, TeamForge will be unable to make a connection to the database.

Follow these steps to overwrite the `.jar` included with TeamForge with the one from $ORACLE_HOME:

```shell
cp $ORACLE_HOME/jdbc/lib/ojdbc14.jar 
        /opt/collabnet/teamforge/jboss/jboss-3.2.6/server/default/lib/
````

A restart of the application will be required to use the `new.jar`.
{{site.data.alerts.hr_shaded}} 

## Why can't I move these artifacts into this planning folder?

To avoid confusion, you must observe a few basic rules when you assign artifacts to planning folders.

When an artifact in a planning folder has a child artifact, the child artifact can only be assigned to the same planning folder as the parent artifact, or a sub-folder of that folder. For example:

 * Before you assign an artifact to a planning folder, make sure the artifact and all its children are assigned to a single planning folder and its sub-folders.

 * Don't assign an artifact to a planning folder that is above the artifact's parent artifact in the planning folder hierarchy.

 * Before promoting a planning folder to a higher level in the hierarchy, make sure its member artifacts (and its members' parent artifacts) are all assigned to the same planning folder or a sub-folder of it.

An artifact can only be assigned to a planning folder in its own project.

As a best practice, consider instead creating a matching artifact in this project and associate the two artifacts.

Before you assign an artifact to a planning folder, be sure you have permission to edit every artifact affected by the move.
{{site.data.alerts.hr_shaded}}


## Who can access a project?

You control access to your Digital.ai TeamForge project by a combination of project settings, membership rules and user restrictions.
{{site.data.alerts.hr_shaded}}

## Who should I allow access into my project?

To decide how to control access to your project, think about what the project is for and who will be using it.

Consider these elements:

* The project's access setting.

A project can be public, private, or gated community.

 {% include note.html content="The site administrator can change the default project access permissions." %}

* The project's membership.
* Each site user's user type.
* Each site user's license type.
* Each TeamForge user's user type.
* Any parent projects from which members, user groups or roles are inherited.
* Any subprojects that inherit members, user groups or roles from this project.

### User type

Users can be restricted or unrestricted.

 * Restricted users can access only public projects and projects of which they are members.
 * Unrestricted users can access all projects except private projects of which they are not members.

### License type

Users can have an ALM license or an SCM license.

 * An ALM license enables the user who holds it to use the full range of TeamForge features: both the core source-code management tools and the extended application life cycle management functionality.
 * An SCM license enables the user who holds it to use the core TeamForge source-code management tools.

License type supersedes user type. For example, if you give a user an SCM license, and then declare that user an unrestricted user, the user can see only the core source code management tools in any project they can access.

### Project access setting

A project can be private, gated, or public.

* **Private** - Private projects can only be accessed by project members. Private projects do not appear on the Home page, in the **All Projects** list, or in search or reporting results to users who are not project members.

  Create a private project when you want to strictly limit project access.

* **Gated** - Gated community projects can be accessed by project members and by unrestricted users. As with private projects, gated projects are not visible to users who are not allowed to access them.

  Create a gated community project when you want to exclude restricted users, but do not need to exclude other, unrestricted users. For example, your organization might wish to designate all contractors or outsourced staff as restricted users. They will not be able to see any gated community projects, but all of your full-time, regular staff will have access.

* **Public** - Public projects can be accessed by all users.

  Create a public project when you have no need to restrict access.

  361:The following table shows which user types can access projects with each project access setting.
{% include note.html content="Project access is not the same as project membership. Project access allows a user to see the project in the **All Projects** list, visit the project home page, and browse selected project data. A restricted user may be able to access a project without being a project member." %}

This table shows which user types can access projects with each project access setting.

<table>
<tr>
<th>Project access type</th>
<th>Project member (Unrestriced user)</th>
<th>Project member (Restricted user)</th>
<th>Non-project member (Unrestricted user)</th>
<th>Non-project member (Restricted user) </th>
</tr>
<tr>
<td>
	Private
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
<td>
	No
</td>
<td>
	No
</td>
</tr>
<tr>
<td>
	Gated
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
<td>
	No
</td>
</tr>
<tr>
<td>
	Public
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
<td>
	Yes
</td>
</tr>
</table>
{{site.data.alerts.hr_shaded}}

## How do I give read-only anonymous access to svn repository?

Set the default access permissions of the project to public and allow Source Code to view permission for all or specific repositories to All users while restricting other permissions.

To give read-only anonymous access to SVN repository within a project while still restricting write access, you could set the default access permissions of the project to public with Source Code view permission open to all users, while restricting other permissions to specific user classes.

The steps to set this up are as follows:

 1. Click **Project Admin** from **Project Home** menu.

 2. Click **Permissions** in the left navigation menu.

 3. Click on _Default Access Permissions_ tab.

 4. Set **Project Access Permissions** as _Public_.

 5. Under **Application Permissions**, choose **All users** from the drop-down for Source Code View permission.

 6. For other application permissions, choose a user class based on your access requirement.

 {% include note.html content="In Step 5 above, it is possible for you to choose whether you want to give View access to All users for all repositories or a specific repository." %}
{{site.data.alerts.hr_shaded}}

## Can I ensure that only site admins can create projects?

You can do this using Velocity.

Create `/opt/collabnet/teamforge/sourceforge_home/templates/body_footer.vm` and populate it with this:

```shell
#set($superUser = ${PAGE_INFO.isSuperUser()}) 
#if($superUser == false) 
<script>
if(document.getElementById("createProject") != null){ 
var e = document.getElementById("createProject").parentNode.parentNode; 
while (e.firstchild) { 
e.removeChild(e.firstChild); 
} 
} 
</script>
#end
````

Save the file, and TeamForge will start hiding the button for non-site admins immediately.
{{site.data.alerts.hr_shaded}}

## How do user roles work?

Project administrators can define specific access permissions for individual project members. They do this by using global project roles and/or creating roles and assigning the roles to project members.

Under role-based access control (RBAC), permissions are not assigned directly to an individual user. Instead, each user has the permissions that are attached to any role that is assigned to that user.

A project member can be assigned multiple roles.

In Digital.ai TeamForge, site or project administrators assign roles to the site users or project members. Besides this, a project member can submit a role request to the project administrator. The project administrator can approve or reject such requests.

When you define users, user groups and roles with specific permissions in one project, they can be inherited in one or more subprojects. This helps you avoid duplicating the effort of defining users, user groups and roles across projects.

 {% include note.html content="Permissions are cumulative. If a project member is assigned a role that provides a specific permission, and another role that does not, the user has that permission." %}

A role defines these things:

 * The applications that project members with that role can and cannot access.
 * The resources on which project members with that role can use the applications.
 * The actions that project members can take in each application and on each resource.

 {% include note.html content="If a user has an SCM license, that user can see only the tools that support the core source control functions of the site, even if the user has a role that would otherwise grant access to other resources." %}

When a user's roles do not include access to an application or resource, that application or resource is not visible to that user. For example, imagine that you are assigning roles to Jason, a software developer. Jason needs to check source code in and out in order to fix bugs, develop features and create software releases. However, Jason does not need access to the wiki. If you set up Jason's roles according to those requirements, Jason's experience is like this:

 * On any page in the project site, Jason can see and click the **Trackers**, **Source Code**, and **File Releases** buttons along the top of his screen.
 * Jason does not see the **Wiki** button.
 * If someone sends Jason a link to a page in the Wiki application and Jason clicks the link, he gets an error message. (The message does not specify whether the page exists or not.)
 * When he accesses the project directly from Eclipse or Visual Studio, Jason can expand the project node and browse the **Trackers**, **Source Code**, and **File Releases** nodes, but not the **Wiki** node.

   {% include note.html content="A user's license type also influences what the user can see and do on your site. A user's license type supersedes any role assignments. Ask your site administrator how many licenses of each kind are available for your users. For more information, see [How do TeamForge licenses work?][teamforgelicense.html#licenseframework]." %}

### Applications

An application is a collection of related features designed to enable a user to collaborate on particular kinds of tasks. For example, the Documents application helps users create documents, share in document reviews, and publish documents, among other things.

In the Web interface, each application is represented by a button in the navigation bar at the top of any project page. A given user can see the buttons corresponding to applications they have access to by virtue of the roles assigned to them.

Applications are also known as "tools."

### Resources

 * The tracker application might contain a bugs tracker and a feature request tracker. These are the tracker resources.
 * A project can contain multiple SCM repositories. These are the SCM resources.

### Permissions

**View**

Allows users to view and download items, but not to create or edit items, administer folders, or edit application settings.

**Create or Submit**

Allows users to create new items, but not to edit items, administer folders, or edit application settings. Users with the create or submit permission also have the view permission.

**Edit**

Allows users to edit items, but not to administer folders or edit application settings. Users with the edit permission also have the view permissions.

**Administer**

Allows users to create and edit items, administer folders, and edit application settings. Users with the administer permission also have the edit, create or submit, and view permissions. To delete items, the user needs to have the delete permission.

**Delete**

Allows users to delete items, but not to administer folders or edit application settings. Users with the delete permission also have view permissions. Without the delete permission, users with the administer permission are not allowed to delete items.
{{site.data.alerts.hr_shaded}}

### How does Digital.ai TeamForge help protect data access?

Access to data must be strictly controlled to meet the security requirements of the enterprise. Strict data access control is achieved through a combination of firewalls, authentication, and authorization.

#### Firewalls and Network Configuration

A firewall provides the first level of protection by restricting access to the private network from the Internet. Sophisticated firewall configuration can provide strong security for all enterprise resources.

All Digital.ai TeamForge application server nor the backend servers should ever be exposed to the Internet.

The Digital.ai TeamForge application to function effectively, the following conditions must be met.

 * Across the firewall, clients (users) must have access to:

   * The web server through a secure protocol such as HTTPS (port 443). The web server typically handles both the browser requests as well as the SOAP requests and forwards them to the Digital.ai TeamForge application server.

   * Send mail to Digital.ai TeamForge mail server via SMTP (port 25).

   * The SCM server through a secure protocol such as SSH (port 22).

 * The web server must have access to the application server (typically port 8080).

   {% include note.html content="This port is not exposed outside the firewall." %}

 * The web server must have access to the SCM server for repository browsing functionality.

 * The application server must have access to the backend (SCM, database, mail, etc.) servers.

 * The SCM server must be able to access Digital.ai TeamForge for commit notifications.

 * The mail server must be able to deliver messages across the firewall.


### Authentication and Authorization

To secure sensitive data, Digital.ai TeamForge provides access control tools to restrict unauthenticated and non-member access.

User authentication is supported through verification of username and password during login. Project administrators can completely restrict access to authenticated members by marking projects as gated communities or private. A gated community is only accessible to unrestricted users, while a private project is only accessible to its members.
{{site.data.alerts.hr_shaded}}

## How does Digital.ai TeamForge help protect my data?

Sensitive data must be protected from illegal access at various points in the system. Key areas where security is typically compromised include data transmission and data storage.

### Data Transmission

Network traffic is not encrypted by default. The HTTP protocol (non-SSL) does not protect data during transmission. HTTPS provides Strong Encryption using the Secure Socket Layer and Transport Layer Security protocols (SSL/TLS).

 {% include note.html content="The web server employed by a Digital.ai TeamForge installation must be reconfigured to employ the HTTPS protocol." %}

No Support for TLS Protocol Versions 1.0 and 1.1
<!-- artf395000 -->
: In addition to security vulnerabilities, TLS protocol versions 1.0 and 1.1 do not support modern cryptographic algorithms. The software industry (including popular browsers such as Chrome, FireFox and so on) is set to deprecate the TLS protocol versions 1.0 and 1.1 by March 2020 and so is TeamForge. Customers are therefore advised to upgrade your sites to be able to negotiate with TLS 1.2 connections. Upgrade your clients to the latest version in case you face any SSL handshake issues while connecting to TeamForge.

### Data Storage

Sensitive data, such as credit card numbers, financial information, etc., must be stored securely. Usually this is done by encryption. In the context of an application, like Digital.ai TeamForge, passwords are stored as cryptographic hash, using SHA family of algorithms, to guarantee adequate data protection.

SHA-512 message digest algorithm defines a one-way hash function that is used to maintain data integrity through creation of a digest from data input. The one-way hash function is designed in such a way that it is hard to reverse the process, that is, to find a string that hashes to a given value. SHA-512 is currently a standard, Internet Engineering Task Force (IETF) Request for Comments (RFC) 6234. According to the standard, it is “computationally infeasible” that any two messages that have been input to the SHA-512 algorithm could have as the output the same message digest, or that a false message could be created through apprehension of the message digest.
{{site.data.alerts.hr_shaded}}


## How do site administrator roles work?

Site administrators are default site managers who can create additional site administrators and delegate few site administrative tasks to them.

They can also allow some Digital.ai TeamForge users to use one or more Digital.ai TeamForge tools across several projects, by creating site-wide roles with specific project permissions, minus site administrative permissions. They can also provide ready-to-use roles as global project roles, creating uniformity across the site.

In Digital.ai TeamForge, site or project administrators assign roles to the site users or project members. Besides this, a project member can submit a role request to the project administrator. The project administrator can approve or reject such requests.

A role defines these things:

 * The applications that project members with that role can and cannot access.
 * The resources on which project members with that role can use the applications.
 * The actions that project members can take in each application and on each resource.

When a user's roles do not include access to an application or resource, that application or resource is not visible to that user. For example, imagine that you are assigning roles to Jason, a software developer. Jason needs to check source code in and out in order to fix bugs, develop features and create software releases. However, Jason does not need access to project wiki. If you set up Jason's roles according to those requirements, Jason's experience is like this:

 * On any page in the project site, Jason can see and click the **Trackers**, **Source Code**, and **File Releases** buttons along the top of his screen.
 * Jason does not see the **Wiki** button.
 * If someone sends Jason a link to a page in the Wiki application and Jason clicks the link, he gets an error message. (The message does not specify whether the page exists or not.)
 * When he accesses the project directly from Eclipse or Visual Studio, Jason can expand the project node and browse the **Trackers**, **Source Code**, and **File Releases** nodes, but not the **Wiki** node.

### Applications

An application is a collection of related features designed to enable a user to perform tasks and collaborate with other users. For example, the Documents application helps users create documents, share in document reviews, and publish documents, among other things.

In the Web interface, each application is represented by a button in the navigation bar at the top of any project page. A given user can see the buttons corresponding to applications they have access to by virtue of the roles assigned to them.

Applications are also known as "tools."

### Resources

 * The tracker application might contain a bugs tracker and a feature request tracker. These are the tracker resources.

 * A project can contain multiple SCM repositories. These are the SCM resources.

#### Site Administration Responsibilities

The additional site administrators can be granted administrative rights for any of the site administrator responsibilities related to the following:

 * Projects (includes project templates)
 * Project Groups
 * Users
 * Groups
 * Roles
 * Categories
 * System Tools
 * Integrated Applications

### Site Administration Permissions

**View Only**

Allows users to view and download items, but not to create or edit items, administer or edit application settings.

**Create or Submit**

Allows users to create or submit and edit items, but not to administer or edit application settings. Users with the create or submit permission also have the edit and view permissions.

**Edit**

Allows users to edit items, but not to administer items or edit application settings. Users with the edit permission also have the create / submit and view permissions.

**Administer**

Allows users to create, edit and administer items plus edit application settings, if required. Users with the administer permission also have the edit, create or submit, and view permissions. To delete items, the user needs to have the delete permission.

**Delete**

Allows users to delete items, but not to administer items or edit application settings. Users with the delete permission also have view permissions. Without the delete permission, users with the administer permission are not allowed to delete items.
{{site.data.alerts.hr_shaded}}

## Which role is assigned to me?

There are several ways in which you could have been assigned certain roles in Digital.ai TeamForge. Your access to the projects depends largely on the permissions granted to you via your roles.

You could have been granted access to any Digital.ai TeamForge project in any of the following ways:

* Through site-wide roles (assigned directly to the user)
* Through global project roles (assigned directly or inherited via another project, either individually or as a group member)
* Through project roles (assigned directly or inherited via another project, either individually or as a group member)
* Through permission inheritance (via project hierarchy)

There are two ways you can check which roles are assigned to you in any of your projects:

 {% include note.html content="If you are a site administrator, you can view any user's access rights to the system." %}

To view the roles assigned directly to you:

Use the **My Workspace > My Page > Projects** page and click the _My Projects_ tab.

 {% include note.html content="You can click the role to view the folder-level permissions assigned to you in a project." %}

To view all the roles assigned to you:

Use the **My Workspace > My Page > My Settings** page and click the _Roles_ tab.

You can select `Roles Created For a Project`, `Roles Inherited From a Parent Project` or `Site-wide roles` to view the corresponding roles assigned to you.

{% include note.html content="A global project role that has been assigned to you in a project where you are a direct member will be listed as a directly assigned role." %}

{% include note.html content="You can click the role to view the folder-level permissions assigned to you." %}

### Related Links
* [Control Project Access - Create a Role Based Access Control (RBAC)][projectadmin-controllingprojectaccess]
{{site.data.alerts.hr_shaded}}

## Who can access project planning information?

A project manager should consider carefully who is able to change the project plan.

You can specify the people who can change the product plan based on their roles in the project. Only users with the role you select can view, create, modify, and delete artifacts in the planning folder hierarchy, and populate those artifacts with content.

Every project must strike its own unique balance between openness and control. These broad guidelines may help you decide how to set up the appropriate roles for your project.

 * Err on the side of visibility. Most of the time you will want all project members to at least see the contents of all planning folders. This helps developers avoid duplicating their efforts, and it can enable team members to volunteer their help to each other when appropriate.

   However, occasionally you may want to hide all or part of the planning folder hierarchy from selected people. For example, when you bring on a contract developer for a short period, you may want to restrict that person's view to the specific artifacts they are working on directly.

 * Limit the number of people who can modify or populate planning folders. In many cases, only the project manager really needs to do this.

   However, it may make sense to allow some people with a direct stake in the project to modify some folders. For example, if you are working with a product owner, it might be useful for that person to be assigning artifacts to future planning folders while your team is working on the current one.
{{site.data.alerts.hr_shaded}}

## Who can see a project page?

A user can see a given project page if the page is not hidden and the user's role includes permission to see the page.

{% include note.html content="When a page is hidden, it is only visible to users with the Project Admin role, and then only when the user has clicked **Configure: On**." %}

If a person can see your project, they can see the project home page and any of its subpages. To see any other page, they must be assigned permission explicitly.

Permissions determine two kinds of access:

 * Anyone with access to the project can see the project homepage.

 * Users whose role includes permission to see a given top-level project page can see all the subpages of that page.

Subpages inherit their permission setting from the top level page they belong to.
{{site.data.alerts.hr_shaded}}

## Who can see a project page component?

To see a given project page component, you must have permission to see both the project page where the component is and the tool that the component represents.

Your ability to see and edit the contents of a project page component is controlled by your permissions with regard to the tool the component represents.

For example:

 * If you have permission to create documents in a selected folder in the Document Manager tool, you have that same permission when viewing that folder in a Documents component on a project page.
 * If you do not have permission to view a folder in the Document Manager tool, you cannot see a document component that contains that folder on a project page.

 {% include note.html content="Users with the Project Admin role can see project page components even if they do not have access to the related tool." %}
{{site.data.alerts.hr_shaded}}

## As a project admin, why don't I have permissions to the wiki?

Most likely, your site was installed before TeamForge contained the wiki component.

When the wiki was added to TeamForge, it was decided that there was no way for us to know the security requirements at customer sites, so permissions for the new wiki component were not assigned to project admins by default. As a project admin, you can alter any existing role to grant this permission, or create a new role for this permission and then assign to the appropriate project members as needed.


{% include links.html %}