---
title: FAQs on Git/Gerrit/History Protection 
keywords: FAQ, frequently asked questions
tags: [ctf_20.3, faq, git_gerrit, history_protection, code_review]
sidebar: teamforge_sidebar
permalink: gitgerrit-faqs.html
last_updated: Sep 17, 2020
summary: These are some of the frequently asked questions on TeamForge-Git integration, Git history protection and so on.
---
## Restore Git Replica Server by Bootstrapping {#restorereplica}
<!-- [artf415643] instructions for Git replica re-installation by DB bootstrap -->

You can restore your Git replica servers by bootstrapping the Gerrit database in case your servers are damaged beyond repair. To restore a damaged Git replica server:

1. Back up Git replica server's SSH keys from `/opt/collabnet/teamforge/var/scm/gerrit/hostkeys`. Back up the SSH keys to a safe location. The following command uses `/tmp`.
   ```shell
   cp -R /opt/collabnet/teamforge/var/scm/gerrit/hostkeys /tmp 
   ````
2. Stop the gerrit service.
   ```shell
   teamforge stop -s gerrit
   ````
3. Bootstrap the gerrit performance and gerrit databases.
   ```shell
   teamforge bootstrap -s gerrit-database-performance-postgres -y
   teamforge bootstrap -s gerrit-database-postgres -y
   ````
4. Bootstrap gerrit.
   ```shell
   teamforge bootstrap -s gerrit -y
   ````
5. Deploy gerrit.
   ```shell
   teamforge deploy -s gerrit -y
   ````
6. Restore the SSH keys from `/tmp`.
   ```shell
   cp /tmp/hostkeys/* /opt/collabnet/teamforge/var/scm/gerrit/hostkeys
   ````
7. Set the right permissions to the SSH keys.
   ```shell
   chown -R gerrit:gerrit /opt/collabnet/teamforge/var/scm/gerrit/hostkeys/
   ````
8. Run the `teamforge migrate` command for the `gerrit` service.
   ```shell
   teamforge migrate -s gerrit -y
   ````
9. Start the gerrit service.
   ```shell
   teamforge start -s gerrit
   ````

{{site.data.alerts.hr_shaded}}
## Where can I find more information about Gerrit?
For more information on Gerrit, see the [Gerrit Community Documentation](https://gerrit-review.googlesource.com/Documentation/) page.
{{site.data.alerts.hr_shaded}}

## How can I log into Gerrit?
If your administrator has set up Gerrit as a linked application to Teamforge, you will automatically be logged into Gerrit (SSO) when you click its link. If not, access the URL `http(s)://<yourtfinstance>/scm integration server>/gerrit/` and provide your TeamForge credentials.
{{site.data.alerts.hr_shaded}}

## What are the Git protocols that work with the Git repositories managed by TeamForge?
The Git integration currently allows you to access a Git repository using SSH. That said, you must have generated an SSH key pair and uploaded the SSH public key to Teamforge in **My Settings > Authorized keys**.

Alternatively, you can use http(s) to clone and push to Git repositories. In this case, you can authenticate using your TeamForge user name and password.
{{site.data.alerts.hr_shaded}}

## How can I use http(s) for accessing Git repositories?
The clone URL for http(s) access follows this convention:
```git
git clone https://$USERNAME@<yourtfinstance/scm integration server>/gerrit/p/<TFreponame>
````
When you run the above command on your Git client, you will be asked to provide your credentials. Use the same credentials you use to log into TeamForge’s web interface.
{{site.data.alerts.hr_shaded}}

## How do I generate an SSH key pair?
You can generate an SSH key pair on a Unix machine by running the following shell command:
```shell
$ ssh-keygen -t rsa
````
You will be prompted to provide the location to store the key pair. The default is the home directory of the logged-in user.
{{site.data.alerts.hr_shaded}}

## After installing a Git client, I am able to clone a Git repository into my local work directory. However, I am not able to "push" anything to the remote repository in spite of having view and commit permissions. What should I do ?
Right after you clone, but before you commit any changes locally, you will need to configure Git if you haven't already.
````git
$ git config --global user.name "<TeamForge username>"
$ git config --global user.email "<email used in TeamForge for the user>"
````

You should now be able to push your changes.
{{site.data.alerts.hr_shaded}}

## Is a commit association created in TeamForge after I push my commit to a remote Git repository?
Yes, when you push a local commit to the remote repository, an association will get created if the commit message contains a reference to a TeamForge item such as a tracker artifact, wiki or document in square brackets, for example [artf1234].
{% include note.html content="A commit association will not be created if you push your commit to Gerrit's `review branch` (push for review). It will be created once the change is merged into the real branch." %}
{{site.data.alerts.hr_shaded}}

## What happens if the TeamForge site is down or there are some network problems--will the Git integration still work?
The Git integration still works, but with the following limitations:
* If the TeamForge site is down, users will not be able to see commit associations created in TeamForge, but still be able to push commits to a Git repository.
* If the Git integration is hosted in LOCAL mode, network-related problems would definitely prevent changes being pushed to a Git repository.
* If the Git integration is hosted in REMOTE mode, the synchronization of roles and permissions will be cached during the period when TeamForge is down; Git will function with the roles and permissions synched already.
{{site.data.alerts.hr_shaded}}

## What is a "Jumbo Push"?
In contrast to Subversion, Git has the concept of local commits that stay in the local environment of a user, and at some point, get pushed to a remote repository all at once. This push checks in changes from all commits into the remote repository. For each of those commits, a commit object appears in the TeamForge (Source Code component). So, one push can have an unlimited number of commits and thus commit objects in TeamForge. You can, however, define the threshold for a single push based on how many commits should generate a commit object. A push' containing commits beyond that threshold is called a "Jumbo Push"'.

You can configure the Jumbo Push threshold by updating the site option token, [GERRIT_GIT_PUSH_THRESHOLD][siteoptiontokens.html#gitpushthreshold] in the site-options.conf file. You have to run the post-installation script after rebuilding the runtime environment. When the Git and Teamforge are hosted on the same server, the runtime involves TeamForge downtime.
{{site.data.alerts.hr_shaded}}

## What objects and relationships are mapped between TeamForge and the Git integration?
See the README (APPENDIX, Relationship and Object mapping section) or [Mappings Between TeamForge and Gerrit][gitreference.html#tfgerritmapping].
{{site.data.alerts.hr_shaded}}

## When are the objects and relationships synchronized between TeamForge and the Git Integration?
TeamForge project roles, project role SCM permissions, global groups, SCM repositories, and global group/project role membership are synched in two ways:
* **Synchronously**: after a regular interval (configurable using the post-installation script).
* **Asynchronously**: whenever there is a change related to roles or permissions within Teamforge, it triggers the sync between TeamForge and the Git integration.

TeamForge repositories are only synched if there is at least one project role with SCM permissions present in the corresponding TeamForge project.

TeamForge users are provisioned in Gerrit whenever you:
* Change their authorized keys in TeamForge.
* Log into Gerrit by clicking the linked application link or using TeamForge user name and password
* Access GitWeb (web interface for a Git repository) by clicking a Git repository link in the TeamForge Source Code page
  
  {% include note.html content="Changes in Gerrit are not synched back to TeamForge." %}
{{site.data.alerts.hr_shaded}}

## Where can I find system logs for the Git integration?
You can find the logs under /opt/collabnet/gerrit/logs/.

### Can I bypass Gerrit and access a Git repository directly?
No, Gerrit is used to enforce TeamForge access permissions.
{{site.data.alerts.hr_shaded}}

## I deleted a TeamForge Git SCM repository but the corresponding Gerrit project does not get deleted. What's wrong?
1. Delete the Git repository in TeamForge.
2. Go to the Git repository project in Gerrit.
3. Go to **Projects > General** and delete the Gerrit project.

You can delete the repository even if there are open changes (repository is permanently deleted) with an option to preserve the repository, if required. Select **Preserve Repository** if required.
{{site.data.alerts.hr_shaded}}

## How can I import an existing Git repository into Gerrit? {#howtoimportgitrepo}
You can import an existing Git repository into Gerrit as a project admin from a local machine or as a System Admin from the server.

Option 1:

If you are a project admin, create a new repository and configure your account so that it has at least Delete/View SCM permissions for the one in TeamForge. Clone your existing repository and force push its content to the empty TeamForge repository:

```shell
git clone --mirror [url of repo to be imported]
cd reponame
git gc
git remote add dest [url_to empty TeamForge Git repository]
git push -f --tags dest refs/heads/*:refs/heads/*
````

Option 2:
If you are a site admin, create a new repository from the TeamForge UI and perform the following steps from the server as a Gerrit system user to import a repository from the source into TeamForge:

```shell
# su gerrit
$ cd /tmp
$ git clone --mirror [url of repo to be imported]
$ cd reponame.git
$ git gc
$ git remote add dest file:///gitroot/reponame.git/
$ git push -f --tags dest refs/heads/*:refs/heads/*
````

{% include note.html content="When importing a repository previously hosted on a different Gerrit server, do not push the review branches as Gerrit numerical change numbers are not globally unique and duplication will result in wrong email notifications and problems submitting open reviews." %}

**See Also**: [Import External Git Repositories into TeamForge from the Code Browser UI][import-git-repo].
{{site.data.alerts.hr_shaded}}


## Do we have default hook scripts available for Git in TeamForge?
Associating artifacts based on commit messages and blocking commits without a commit message is a core TeamForge mechanism that is supported by Git as well.
To add hook scripts, see [Gerrit Code Review--Hooks](https://gerrit-review.googlesource.com/Documentation/config-hooks.html).
{{site.data.alerts.hr_shaded}}


## Do we have email alerts for Git in TeamForge? If yes, where do we configure it?
Email alerts based on TeamForge commits is a core TeamForge feature, independent of the SCM involved. In addition, Gerrit sends out review emails using the SMTP server specified during installation (it defaults to the TeamForge SMTP server). The mail template is explained in [Gerrit Code Review--Mail Templates](https://gerrit-review.googlesource.com/Documentation/config-mail.html).
The [blog post](http://blogs.collab.net/teamforge/collabnet-gerrit-notifications-for-all-who-miss-the-good-ol-git-push-notifications) explains how to send information on Git pushes to Teamforge forums (which act as mailing lists too).
{{site.data.alerts.hr_shaded}}

## Do we have Role Based Access Control and Path Based Permissions for Git in TeamForge?
We support all SCM permission cluster options for TeamForge project roles, default access permissions, project admin permissions along with the site-wide roles and site admin permissions. However, path-based permissions are not relevant in Git since a Git commit always contains all files. If we did not ship certain files, this would result in a checksum error. Gerrit supports branch-based permissions though.

For more information on branch-based permissions, see [CollabNet’s blog post](http://blogs.collab.net/teamforge/managing-git-branch-level-permissions-with-teamforge-and-gerrit).
{{site.data.alerts.hr_shaded}}

## What is history protection?
History rewrites are non-fast-forward updates of remote refs and associated objects. History rewrites happen when a branch in a remote repository gets deleted, previously pushed commits get amended/tree filtered and forcefully re-pushed, or a remote branch/tag is pointed to an entirely different commit history.
{{site.data.alerts.hr_shaded}}

## Is it possible to turn on history protection for all Git repositories hosted on a Git integration server? If yes, how?

History protection is enabled by default in TeamForge 17.4 and later. However, site administrators can disable history protection at the site level if need be, after which project administrators can choose to have history protection enabled or disabled for individual repositories.

{% include important.html content="The GERRIT_FORCE_HISTORY_PROTECTION site-options token is no longer supported in TeamForge 17.4 and later. Remove this token from the `site-options.conf` file while upgrading to TeamForge 17.4 or later." %}
{{site.data.alerts.hr_shaded}}

## I've enabled Protect History for my TeamForge project's Git repository. Will this be effective immediately?
To enable history protection immediately, a TeamForge user with the Source Code Admin permission must do this right after selecting the **Protect History** check box: temporarily remove any user with a project role with any SCM permission, and then add that user back. This will trigger an immediate sync after which history will be protected for the Git repository. Otherwise, history protection will be enabled after a periodical sync.
{{site.data.alerts.hr_shaded}}

## Can I turn off history protection for any particular Git repository when it is enabled server-wide?
No, when history protection is enabled server-wide for the Git integration server, it cannot be turned off for a particular Git repository.
{{site.data.alerts.hr_shaded}}

## Where can I see the backup branches generated by history protection?
Backup branches are generated based on the type of History Rewrite. For a remote branch that is deleted, this is under `refs/delete`. For a non-fast-forward push, this is under `refs/rewrite` with the branch name containing the timestamp, original branch and the user who rewrote history, for example, `refs/delete/20121112042512-test--david`.
{{site.data.alerts.hr_shaded}}

## Who can resurrect or permanently delete backup branches?
A user who is a member of the Gerrit Administrator group can resurrect or permanently delete backup branches. By default, the TeamForge site administrator whose credentials are used for running the post-installation script is part of the Gerrit Administrator group.
{{site.data.alerts.hr_shaded}}

## Who can see backup branches?
By default, a TeamForge user with SCM View (or more) permission can see all backup branches by executing `git fetch && git ls-remote origin`. In Gerrit, the user must be part of a group which has at least read access for `refs/delete` and `refs/rewrite` for the given Gerrit project (TeamForge Git repository).
{{site.data.alerts.hr_shaded}}

## Are the backup branches under `refs/rewrite` and `refs/delete` protected from Git garbage collection which removes unreferenced objects?
Yes, objects in backup branches under `refs/rewrite` and `refs/deleted` are referenced and cannot be cleaned up by Git's garbage collection.
{{site.data.alerts.hr_shaded}}

## Do backup branches take up a lot of disk space on the Git server?
The backup branches on the Git server are mainly [Git objects](http://git-scm.com/book/en/Git-Internals-Git-Objects) that are compressed deltas of original file versions. Git regularly compresses these objects to save disk space.
{{site.data.alerts.hr_shaded}}

## What is the difference between History Protect and [Git reflog](http://www.kernel.org/pub/software/scm/git/docs/git-reflog.html)?
In Git, reflog records all activity on a branch, while History Protect only reports deleted branches/tags and history rewrites (non-fast-forward pushes) For more information, see Git reflog vs TeamForge-Git integration History ProtectGit reflog vs Perforce History Protect.
{{site.data.alerts.hr_shaded}}

## Which ports does the Git Integration use? My organization has a strict firewall policy, and I need to know which ports to make available for the Git integration.
The Git integration uses 3 ports: 9080,9081, and 29418. See the README file for more information. For the integration, Git integration uses 3 ports(9080,9081,29418 follow details in README) Only port 29418 should be exposed by the firewall.
{{site.data.alerts.hr_shaded}}

## I ran Gerrit manually (without the service script; now my secure `config` file is gone and Gerrit does not start up. What happened and how can I fix this?
If Gerrit is run with a different Unix user than `gerrit`, newly created and modified files may not belong to the `gerrit` user any longer. As a consequence, when you try to restart Gerrit using its services script (which switches to the gerrit user), Gerrit might not start up due to wrong file permissions. If Gerrit detects that the permissions of its secure config file have been tampered with, it even removes this file. You should, therefore, only run Gerrit using the service script provide, and reconfigure it by running the post-install script again. You can fix incorrect permissions by running the following (as sudo or root):

```shell
chown -R gerrit.gerrit /opt/collabnet/gerrit
````
{{site.data.alerts.hr_shaded}}

## I deleted the dedicated Teamforge Gerrit user account in TeamForge, and SCM permission synch is no longer working. How can I recover from this situation?

The easy, and recommended, approach is to ask CollabNet's Professional Services to undelete the TeamForge user in question.
Otherwise, you would have to create a new dedicated site admin user in TeamForge, shut down Gerrit, re-run the post-install script and provide the credentials of that user. Then, you would have to start Gerrit again, and log in with as that new user via the web interface. You will see that the user does not have any special admin permissions. If you still have a working user in Gerrit's administrator group, you could add the dedicated Gerrit user to that group using Gerrit's web interface. If not, you would have to manually add the new user to the Gerrit administrator group by shutting down Gerrit, removing all files from its caching directory, inserting the `user id` of the new user into Gerrit's Postgres `reviewdb DB` group/user membership table, and starting Gerrit again. Since this probably requires you to consult CollabNet's Professional Services as well, we strongly recommend the previous option (undeleting the previously removed user).
{{site.data.alerts.hr_shaded}}

## Why does the Registered Users group has StreamEvents capability in Git Integration v8.1.x by default?

* As Gerrit 2.7 Stream Events capability is required for user whose account has been used to monitor Gerrit Events on repositories hosted on Gerrit.
* As Jenkins [Gerrit Trigger plug-in](https://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Trigger) uses such a capability to monitor Gerrit events.
* If you have been using **Jenkins CI with Gerrit Trigger** plug-in to automatically verify code review request and already upgraded to TeamForge-Git Integration v8.1.x, the **Registered Users** group has been given this capability by default. Therefore, you do not need add this capability manually and your Jenkins CI with Gerrit Trigger continues to function as usual.
* In case you’re using **Jenkins CI with Gerrit Trigger** plug-in, you may remove the **Stream Events** capability as a user who is part of the **Gerrit Administrators** group.
  * To remove Stream Events:
    1. Log on to Gerrit web UI.
    2. Select the **Projects** tab.
    3. Select **All Projects > Access**.
    4. Click **Edit**.
    5. Delete the **Stream Events** drop-down list.
    6. Click **Save Changes**.
       {% include image.html file="removestreamevents01.PNG" %}
       {% include image.html file="removestreamevents02.PNG" %}
{{site.data.alerts.hr_shaded}}

## How do I use a replicated repository from the client? {#usereplicaongitclient}

You can start using a replicated repository either by cloning the repository from TeamForge or by modifying the existing repository.

#### Option 1: Clone repository from TeamForge

Clone the repository from the git replica using the clone URL provided by TeamForge. This is the easiest way as the clone URL contains all the necessary options.

1. Click on the replica of a git repository.

   {% include image.html file="git-replica.png" %}

2. Clone the replica using the clone URL provided by TeamForge. Here's an example of the Clone URL using SSH.

   {% include image.html file="clone-git-replica.png" %}

#### Option 2: Modify existing repository

If the repository is already available on the client (cloned from master), one can use it  and modify its `config` properties to use replica. 

Here's an example on modifying a repository that is cloned using SSH protocol.

1. Run this command to edit the Git `config` file.

   ```shell
   git config –-edit
   ````

2. Modify the following tokens.

   * The remote origin URL should point to the replica instead of `master`, so that the clone operation uses replica.

     ```shell
     [remote "origin"]
             url = ssh://<username>@<replica_server>:29418/<repo_name>
     ````

   * Wherever `master` is referenced in the command line, the replica should be used instead. This is achieved by using the token `insteadOf` as follows:

     ```shell
     [url "ssh://<replica_server>:29418"]
             insteadOf = ssh://<master_server>:29418
     [url "ssh://<username>@<replica_server>:29418"]
             insteadOf = ssh://<username>@<master_server>:29418
     ````

   * Finally, the push operation should go to `master` instead of replica.

     ```shell
     [url "ssh://<username>@<master_repo_name>:29418"]
             pushInsteadOf = ssh://<username>@<replica_server>:29418
     ````

In a similar manner, you can modify a repository that is cloned using HTTPS protocol.

## My Javamelody plugin does not display the graphs on standalone Gerrit server. What should I do?

This means that Javamelody is not able to find the required fonts. The easiest way to fix the problem is to install the *fontconfig* package on the Gerrit server:

```shell
yum install fontconfig
````

Restart your Gerrit server after installing *fontconfig* and verify that the Javamelody graphs are working properly.

{% include note.html content="The reason we haven't introduced a new dependency on the *fontconfig* is that Gerrit as such does not require it and we do not want to introduce a third party dependency to a Javamelody package that we do not own or manage. Besides, please note that the required fonts can be also installed without the *fontconfig* package." %}

## Gerrit cannot start as it is unable to obtain the list of repositories from TeamForge. What should I do?
<!-- https://forge.collab.net/sf/go/artf418923 -->
Gerrit fails to start when the SOAP call `ScmSoap.getRepositoryListForExternalSystem()` fails with the following error:

```
The specified path was invalid: projects.gerrit_git_integration/scm.gerritforge
```

**Solution**:

This is due to a corrupt `project_path` index of the project table. Run the following command to re-index.

```
reindex index project_path;
```
{% include links.html %}