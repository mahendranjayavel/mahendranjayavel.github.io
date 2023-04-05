---
title: Source Code (SCM)
keywords: FAQ, frequently asked questions
tags: [ctf_20.2, faq, source_code, subversion]
sidebar: teamforge_sidebar
permalink: sourcecode-faqs.html
last_updated: Jul 13, 2020
summary: These are some of the frequently asked questions on SCM related activities in TeamForge.
---

## Git clone scp command fails with the `unknown option -- O` error. What should I do?

<!-- https://forge.collab.net/sf/go/artf422083 -->

The `git clone` scp command, which includes a new `-O` option, would fail with the following error if used with some of the older OpenSSH clients. 
  
`unknown option -- O`

Run the git clone scp command without the `-O` option. You can also upgrade your client if you want to run the git clone scp command with the `-O` option. 
{{site.data.alerts.hr_shaded}}

## What software configuration management tools are available in Digital.ai TeamForge ?

In Digital.ai TeamForge, users can browse the contents of a project's source code repositories and view detailed information about code commits, changed files, and associations with other Digital.ai TeamForge items.

Digital.ai TeamForge is not intended to replace your SCM tool. Code must be checked in using Subversion or GIT.
{{site.data.alerts.hr_shaded}}

## Who can Access Source Code? {#sourcecodefaq1}

Project administrators can give project members specific kinds of access to a whole Subversion repository or any path within that repository.

### Overview

You can specify access permissions for users with a given role at the repository level, or at the path level within a repository.

 * When you set a permission for a role on any directory in the repository, all directories and files under that directory get the same permission.
 * When you set a permission on an individual file in the repository, there is no effect on the permissions assigned to paths above the level of that file. (A file is just a path that ends with a file name.)

How you use path-based permissions will depend on whether you view permissions primarily as a way to grant access or as a way to restrict access.

**Full access, with exceptions**

 Give your company's own employees commit access to your whole source code base, while allowing developers from contracting firms to commit only to those parts of the code base that they are expected to work on.

**No access, with exceptions**

Assign all developers "No access" by default, then assign each type of developer access to certain directories and files according to their responsibilities.
 
 {% include note.html content="You can control access to a path or to an individual file. This is different from normal Subversion checkout and commit operations, which are performed on directories but not individual files." %}

### No Access
When you deny all access to a repository for a role, users with that role cannot see that the repository exists, except if:

 * The role has "View and Commit" access to some directory within the repository. In this case, users with this role can see the directories that contain the directory they have access to.

 * The user has another role that grants access to some part of the repository.

   {% include note.html content="An individual user can have multiple roles. When two roles have permissions that conflict with each other, the role with the more expansive permissions takes precedence." %}

### View Only

Users with a role that has "View Only" access to a path can browse the contents of the repository on the Web site or by connecting directly to the repository from a client, such as Tortoise, CollabNet Desktop for Eclipse, or CollabNet Desktop for Visual Studio.

### View and Commit

Users with a role that has "View and Commit" permission to a path can browse and download code, and can also check code into the repository.

### Wildcard-based Access Control and Path-based Permissions

You can create rules that use wilcards to control access to specific paths in a repository. See [Wildcard-based Access Control and Path-based Permissions in TeamForge](http://blogs.collab.net/teamforge/wildcard-access-control-and-path-based-permissions-in-teamforge) for more background information about wildcard and path based permissions.

**Scenario 1**

Controlling access to a specific path in a branch using authz rules can be very time consuming and inefficient. Assume you have three branches, `[/branches/foo/build]`, `[/branches/bar/build]`, and `[/branches/baz/build]`. If you create `authz` rules, you may have to write a separate rule for every branch in the repository, let alone the fact that you need to write such rules for a branch you may create in the future.

```shell
[/branches/foo/build]
@build = rw
@dev = r
````

```shell
[/branches/bar/build]
@build = rw
@dev = r
````

```shell
[/branches/baz/build]
@build = rw
@dev = r
````
Instead, you can write a rule using wildcards such as:

```shell
/branches/*/build
````

Later, you can create and assign roles to users such as "build engineers" and "developers" with "read-write" and "read-only" access permissions respectively.


**Scenario 2**

In this scenario, assume that there is a particular file or folder pattern that needs access control in a repository. For example, you may want to restrict all users but release managers from modifying `.iso` files. It is impossible to define such a rule using the `authz` file.

With TeamForge, you can write a rule that partially uses wildcards in file or folder names such as:

```shell
/trunk/build/*.iso
````

This rule applies to all files and folders that end with .iso under the path `/trunk/build`.


**Scenario 3**

In this scenario, assume that you want to control access to a particular folder no matter where the folder is in a branch. For example, you may want to control access to the “build” folder wherever it is in a repository. You can write a rule using wildcards such as:

```shell
/**/build
````

The "**" matches any number of folder levels in a repository. For example, this rule applies to the following paths:

```shell
/trunk/build
/branches/feature1/build
/trunk/external_module/build
/build
````
In addition to these scenarios, you can use wildcards to create rules that suit your requirement. A few examples of how you can create wildcard-based rules:

* `/**/*.iso` - Match any .iso file anywhere in a repository.

* `/branches/RB*` - Match any branch if the name starts with RB.

* `/branches/*/*.txt` - Match all .txt files one level under any branch.

**Notes about path-based permissions**

If two paths have different permissions, the permissions on the lower-level path take effect. For example, consider a role that has "No Access" set for the path `/branches/version3/users`, but has "View and Commit" access to `/branches/version3/users/vijay`. A user with this role can:

 * Check code in and out of the vijay directory.
 * Click down through all the directories in that path, including `users`. (Directories that are not included in the user's permissions are not shown.)

Users with this role cannot:

 * Check files in and out of the users directory.
 * Monitor commits to users.
 * Execute Subversion copy, move or delete operations that involve resources in the users directory (or any other paths where the user has View Only or No Access).

### Commit Messages

When users monitor a repository, they receive commit announcements by email that include the resources that their role permits them to see.

Users with a "No Access" role on a repository cannot monitor that repository to receive commit messages by email.

By default, commit emails provide all the details about the commit that a logged-in user can view in the **Source Code** application. A repository owner can elect to have the notification emails omit most of the detail and provide only the commit ID and the committer's user name.

### Toolbar button

If none of the available permissions (**View Only**, **View and Commit**, or **Path-based Permissions**) is selected for any repository, and none of the options under **Source Code Permissions** is selected, users with this role do not see the **Source Code** toolbar button.
{{site.data.alerts.hr_shaded}}

<!-- ## I deleted the email that verifies my CVS password. How can I retrieve my password?

You can sync up your TeamForge login and CVS passwords by changing your password in TeamForge.

To change your password

 1. Log in and click on **My Workspace**.

 2. Click on **My Settings**.

 3. Click on **Change Password**.

 4. Enter your old password and new password.

 5. Click **Submit**.

 {% include note.html content="The old and new passwords can be the same if you do not wish to actually change it." %}
{{site.data.alerts.hr_shaded}} --> 

## Why don't the branding repo changes get rendered into UI?

It may be due to the property 'subversion_branding.repository_base' pointing to /sf-svnroot instead of the /svnroot directory, which is used by the scm-integration of the csfe installation.

First, check the location of the branding repository in subversion_branding.repository_base=/sf-svnroot' in `/opt/collabnet/teamforge/runtime/conf/sourceforge.properties`.

If it has to be /svnroot, then add an entry that states SUBVERSION_BRANDING_REPOSITORY_BASE=/svnroot

Then re-create a runtime and restart TeamForge.
{{site.data.alerts.hr_shaded}}

## Why do we have errors creating or altering repositories and adding or removing users?

The TeamForge SCM Integration server runs an instance of Tomcat and then launches TeamForge inside the Tomcat container.

If you are experiencing issues creating or altering repositories or adding and removing users from repository access, and the other TeamForge integration logs are not providing any clues, you may wish to review the Tomcat log at: `/opt/collabnet/teamforge/log/integration/catalina.out`.

Sometimes, OS-level errors will be flagged into this log and not others. In our experience, it is pretty rare to find something in this log that is not logged elsewhere.
{{site.data.alerts.hr_shaded}}

<!-- ## Why is the password and login shell changed for users on my cvs/svn server?

TeamForge uses local user accounts on the SCM server to provide access to CVS repositories via ssh.

If any local user accounts on the SCM server match user names within TeamForge they will be changed.

If you are planning to use CVS in the SCM server, you should ensure that the local accounts do not conflict with the TeamForge user accounts. Adding a prefix to the local user accounts (local_username) would be one way to resolve this and prevent the usernames from conflicting. Alternatively, if you are not using CVS repositories, the CVS integration can be removed altogether.
{{site.data.alerts.hr_shaded}} -->

## Why do I get a proxy timeout when I try to view certain SCM pages?

If you are getting a proxy timeout error when you try to view a SCM page, you may need to configure the Apache 2.2 Proxy Timeout to 300 or less in the httpd.conf file.

If you get the following error while attempting to view a SCM page in SFEE:

```shell
The proxy server received an invalid response from an upstream server.
The proxy server could not handle the request 
    GET /integration/viewcvs/viewcvs.cgi/ibe-rules/tags/phases/ibe-rules_09.02.0-Ph-200902_test_20090105/
Reason: Error reading from remote server     
```

Configure your Apache 2.2 Proxy Timeout to 300 or less in the `httpd.conf` file.
{{site.data.alerts.hr_shaded}}

<!-- ## What's the difference between a 'managed' and 'unmanaged' CVS server?

You can use TeamForge to control a CVS server, or you can run the CVS server stand-alone, or 'unmanaged'.

 {% include note.html content="Only CVS servers can run unmanaged. Subversion servers are managed by TeamForge." %}

### Managed Server

A _managed server_ gets its instructions from TeamForge to which it is integrated with. Use TeamForge for SCM tasks such as:

 * Creating repositories
 * Adding and removing users
 * Enabling or disabling user access to the repositories

Both new SCM servers and those with existing repositories can be managed by TeamForge.

### Unmanaged Server

On an _unmanaged CVS_ server, you use the CVS's own utilities to handle repository management, user management, and access permissions.

Add an unmanaged server if you know that all repository and user creation and management must be done manually. For example, set up an unmanaged CVS server when:

 * A corporate IT policy prohibits applications such as TeamForge from making any changes to the users or repositories on the corporation's CVS servers.
 * A CVS server has existing repositories that cannot be changed to adhere to TeamForge standards.
{{site.data.alerts.hr_shaded}} -->

## Subversion Replication in TeamForge

Here's some information on how replication could be useful in your TeamForge site and what to consider when you plan to set up a replica.

### Why replicate?

Typically, you would deploy a replica for one these reasons:

* **Projects in remote locations with lower bandwidth or higher latency want the performance of a "local" server**.

  Your company has a number of developers clustered together at a remote location. When you install a replica inside the LAN of these developers, they can greatly improve their Subversion performance and keep a lot of their traffic off the WAN. In this scenario, you would probably want a replica in each such location. Keep in mind that a replica can only be a proxy for one master -- so if your company has more than one Subversion master server, you may need more than one replica at each location.

* **You want to reduce the load on the master server**.

  For example, continuous integration tools can place a lot of load on the server and moving that load to a separate server can increase the response time for other users. In this scenario you probably only need to add one replica; you'd add it as close to the master as possible so that synchronization is quick. Of course the previous point can be a factor here. If the continuous integration server is at remote location, then you would want to put a replica near the continuous integration server.

### Rules for using a replica

To create a replica in TeamForge, you start with Subversion Edge. A Subversion Edge wizard lets you convert the server into a replica of a Subversion server in TeamForge.

When you configure the replica server, you provide the TeamForge username and password to use for the replica. These are the credentials the replica uses when it replicates Subversion content. This user must be added to projects and given permissions to the repositories being replicated. Those permissions also control what parts of the repository will be replicated. So if you have folders that should not ever live on remote servers, you can set up path-based permissions and that content will never be replicated to the server.

If you forget to set up permissions, the replication will fail. However, there's no real harm done, and once you fix the permissions, you can do it again.

The replica user can be a normal user account -- it does not have to be an Admin account. If the replica is set up and maintained by an Operations team, they might want to just use an Admin account so that project teams do not have to worry about adding the user to the project or setting up permissions.

Permissions for end users accessing those repositories will follow the normal TeamForge rules.
{{site.data.alerts.hr_shaded}}

<!-- ## How do I move an existing CVS repository into TeamForge?

You can import and manage an existing CVS repository with TeamForge.

Do the following to move an existing CVS repository:

 1. Stop CVS access to the old repo.

    ```shell
    chmod -x /usr/bin/cvs
    ````

 2. Tar the old repo.

    ```shell
    cd /cvsroot/old_repo
    tar zcvf /tmp/old_repo.tar.gz
    cd..
    mv old_repo /tmp
    ````

 3. Restore CVS access.

    ```shell
    chmod +x /usr/bin/cvs
    ````

 4. Transfer the repo to the TeamForge CVS server.

 5. Create the new repo from within TeamForge.

    1. Browse to your project

    2. Click the **Source Code** button

    3. Create your new repo

 6. Untar the old repo.
 
    ```shell
    cd /cvsroot/new_repo
    tar zxvf /tmp/old_repo.tar.gz
    ````

 7. To synchronize permissions, perform the following steps.

    * Login as a TeamForge site admin.

    * Click the **Admin** link.

    * Click the **Integrations** button.

    * Check the CVS integration you want.

    * Click the **Synchronize Permissions** button.

 8. Verify the new repo.

 9. Remove the old repo.

   ```shell
   /bin/rm -r /tmp/old_repo
   ````
{{site.data.alerts.hr_shaded}} -->

## How do I move an existing SVN repository into TeamForge?

If you have an existing SVN repo, you can manage it with TeamForge.

To move an existing the SVN repo, perform the following steps:

 1. Stop SVN access to the old repo.

 2. Dump the old repo.

    ```shell
    svnadmin dump /svnroot/old_repo > /tmp/old_repo.dmp o mv /svnroot/old_repo /tmp
    ````

 3. Restore SVN access.

 4. Transfer the repo to the TeamForge SVN server.

 5. Create the new repo from within TeamForge.

 6. Browse to your project and click the **Source Code** button, then create your new repo.

 7. Load the old repo.

    ```shell
    cat /tmp/old_repo.dmp|svnadmin load /svnroot new_repo
    ````

 8. To synchronize permissions, perform the following steps:

    1. Login as an TeamForge site admin.

    2. Click **Admin**.

    3. Click **Integrations**.

    4. Select the SVN integration you want.

    5. Click the **Synchronize Permissions** button.

 9. Verify the new repo.

 10. Remove the old repo.

     ```shell
     /bin/rm -r /tmp/old_rep
     ````
{{site.data.alerts.hr_shaded}}

## How do I enable Neon debugging in my Subversion client?

This is easliy done in a Linux environment by editing the existing servers text file. On Windows it is not easily done and not recommended.

On a Linux system, edit the `~/.subversion/servers` file by adding the line "neon-debug-mask = 130" (without quotes) to the [global] section of the file, making sure that you also un-comment the [global] line as well. Once Neon debugging is enabled, you should see much more output from each svn command.

Although Neon debugging is possible on Windows, it involves steps that are too complex for most end users to undertake, including compiling Windows binaries for the specific platform and manually handling any errors that arise during that process.

{% include links.html %}