---
title: Control Your Code Review Policy
keywords: code review, policy, git, gerrit
tags: [git_gerrit, integration, source_code, pull_request, scm, code_review]
sidebar: teamforge_sidebar
permalink: codereviewpolicy.html
last_updated: Feb 11, 2020
summary: You can control all Gerrit Code Review features directly from TeamForge by specifying a code review policy.
---
For more information on Gerrit Code Review, see the [Gerrit documentation](http://code.google.com/p/gerrit/).

The following code review policy options are supported:
* **No review**: All Gerrit review features are turned off and read/write access is enforced. This is the default option.
* **Mandatory** review: All code changes must be reviewed and read/write access is enforced.
* **Optional** review: The review feature is turned on but can be bypassed if necessary; read/write access is enforced.
* **Pull request** review: Pull requests allow developers to collaborate with each other on a code change before merging it into another branch on a Git repository. Using a pull request, you notify others about a feature or fix change that needs attention.
* **Custom**: Access rights must be set manually in the Gerrit web interface; they will not be overridden by TeamForge.
This specification is intended for advanced users who are familiar with Gerrit access rights and want to turn off “auto pilot”. 
* **User-defined** review: You can add your own categories, if you have access to the `TeamForgeGerritMappings.xml` file. For more information on adding a user-defined repository category, see [Creat a User-defined Repository Category][codereviewpolicy.html#adduserdefinedrepocat].

The following animation illustrates the detailed mapping between SCM permissions, repository policies, and Gerrit access rights.

{% include image.html file="Animated-GIF-Repository-Policies-Short.gif" caption="Mapping between SCM permissions, repository policies, and Gerrit access rights" %}

{% unless site.output == "pdf" %}
<iframe width="700" height="700" src="videos/CTF72_RBAC.swf" frameborder="0" allowfullscreen></iframe>
{% endunless %}

## Mandatory Code Reviews for Git Repositories

When a mandatory review is specified, every change pushed to the repository must pass through a review process before it can get committed (merged) to the repository.

{% include image.html file="mandatory-review-new.png" %}

{% include note.html content="Only TeamForge users with the **Source Code Admin** permission can bypass reviews." %}

Here's a list of permissions and what users with these permissions can do:
* No access: Users with no permissions cannot do anything.
* View only: Users with read permissions can read branches and push for reviews, and have -1 and +1 for reviews.
* Commit/View: Users with commit permissions can do everything read permissions would grant and in addition have -2, +2 for reviews. They can verify and submit permissions but have no right to bypass reviews.
* Delete/View: Users with delete permissions can do everything commit permissions would grant.
* Source Code Admin: Users with admin permissions can do everything delete permissions would grant and in addition push to and create any branch (bypassing review). They can rewrite history, forge the identity of the Gerrit server, and have the right to push tags, the right to upload merges, and the right to fine tune access rights in Gerrit for the Gerrit project involved.

## Optional Code Review for Git Repositories

When an optional review is specified, every change submitted to the repository can be pushed for code review or directly pushed to the repository bypassing review. This depends on the TeamForge user having the appropriate permissions — source code Delete/View or Commit/View permission for the former, or Source Code Admin permission for the latter.

{% include image.html file="optional-review-new.png" %}

Here's a list of permissions and what users with these permissions can do:

* No access: Users with no permissions cannot do anything.
* View only: Users with read permissions can read branches and push for reviews, and have -1 and +1 for reviews.
* Commit/View: Users with commit permissions can do everything read permissions would grant and in addition have -2, +2 for reviews. They can verify and submit permissions, push to/create any branch (bypassing review) and push tags.
* Delete/View: Users with delete permissions can do everything commit permissions would grant and in addition, have the right to rewrite history, upload merges and forge identity.
* Source Code Admin: Users with admin permissions can do everything delete permissions would grant and in addition push to/create any branch (bypassing review). They can rewrite history, forge the identity of the Git server, and have the right to push tags, the right to upload merges, and the right to fine tune access rights in Git for the Git project involved.

## No Code Review for Git Repositories

In TeamForge 8.0 and later, the **No review** policy is selected unless you choose some other policy.

{% include image.html file="default-review-new.png" %}

Here's a list of permissions and what users with these permissions can do:

* No access: Users with no permissions cannot do anything.
* View only: Users with read permissions can only read branches.
* Commit/View: Users with commit permissions can do everything read permissions would grant and in addition, push to/create any branch and push tags.
* Delete/View: Users with delete permissions can do everything commit permissions would grant and in addition, have the right to rewrite history, upload merges and forge identity.
* Source Code Admin: Users with admin permissions can do everything delete permissions would grant. In addition, they can forge the identity of the Gerrit server, and have the right to fine tune access rights in Git for the Git project involved.

## Pull Request Reviews for Git Repositories

Pull requests allow developers to collaborate with each other on a code change before merging it into another branch on a Git repository. Using a pull request, you notify others about a feature or fix change that needs attention.

{% include image.html file="pull-request-review.png" %}

From TeamForge 19.2, after a Git repository is created, the `master` branch is automatically added as the default protected branch for the **Pull request** repository category on the **Settings > Policies** tab of the repository.

{% include image.html file="default-protected-branch.png" caption="\"master\" added as default protected branch for the repository category \"Pull request\"" %}

For more information about pull requests, see [Pull Request][pullrequest].

## Custom Code Review for Git Repositories

When a custom code review is specified, users with the TeamForge Source Code Admin permission can directly fine tune permissions (access rights) in gerrit’s web interface. Those changes will not be overridden by TeamForge.

{% include image.html file="custom-review-new.png" %}

For information on manually defining access rights in the Gerrit web interface, see Update Git repository access permissions in Gerrit.

Here's a list of permissions and what users with these permissions can do:

* No access: Users with no permissions cannot do anything.
* View only: Users with read permissions cannot do anything unless added in Gerrit.
* Commit/View: Users with commit permissions cannot do anything unless added in Gerrit.
* Delete/View: Users with delete permissions cannot do anything unless added in Gerrit.
* Source Code Admin: Users with admin permissions have the right to fine tune access rights in Gerrit for the Gerrit project involved.

## User-defined Reviews for Git Repositories

Users can define their own code review policy.

{% include image.html file="user-defined-review.png" %}

### Create a User-defined Repository Category {#adduserdefinedrepocat}

You can add your own categories, if you have access to the `TeamForgeGerritMappings.xml` file.

To add a new user-defined repository category, follow these steps:

1. Create an empty Git repository, say `test-git-repo`.
   
   ```shell
   git init `test-git-repo`
   ````

2. Change to the directory `test-git-repo`.

   ```shell
   cd test-git-repo
   ````

3. Download the commits, files, and refs from the remote repository to your local repository.

   ```shell
   git fetch ssh://admin@<your_domain>:29418/TF-Projects refs/meta/config:meta-config
   ````

4. Check out the `TeamForgeGerritMappings.xml` file.

   ```shell
   git checkout meta-config
   ````

5. Open the `TeamForgeGerritMappings.xml` file in the editor. 

   ```shell
   vim TeamForgeGerritMappings.xml
   ````

   Add a new repository category, say "pull_request_new" to it.

   ```xml
   <RepoCategory name="pull_request_new" keepRightsAddedInGerrit="false">
        <ScmAdmin>
            <GerritRead value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCodeReview upperRange="2" lowerRange="-2" refPattern="refs/*" exclusive="false"/>
            <GerritVerify upperRange="1" lowerRange="-1" refPattern="refs/*" exclusive="false"/>
            <GerritSubmit value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPush forcePush="true" value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCreateReference value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritForgeAuthorIdentity value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritForgeCommitterIdentity value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritForgeServerIdentity value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritOwner value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritAbandon value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPushMerges value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritPush forcePush="false" value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritRebase value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPushAnnotatedTag forcePush="false" value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <GerritPushSignedTag value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <!-- protected branches-->
            <GerritPush forcePush="true" value="ALLOW" refPattern="refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
            <GerritSubmit value="ALLOW" refPattern="refs/for/refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
        </ScmAdmin>
        <ScmDeleteView>
            <GerritRead value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCodeReview upperRange="2" lowerRange="-2" refPattern="refs/*" exclusive="false"/>
            <GerritVerify upperRange="1" lowerRange="-1" refPattern="refs/*" exclusive="false"/>
            <GerritSubmit value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPush forcePush="true" value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCreateReference value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritForgeAuthorIdentity value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritForgeCommitterIdentity value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPushMerges value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritPush forcePush="false" value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritRebase value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPushAnnotatedTag forcePush="false" value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <GerritPushSignedTag value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <!-- protected branches-->
            <GerritPush forcePush="false" value="DENY" refPattern="refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
            <GerritSubmit value="DENY" refPattern="refs/for/refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
        </ScmDeleteView>
        <ScmCommitView>
            <GerritRead value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCodeReview upperRange="2" lowerRange="-2" refPattern="refs/*" exclusive="false"/>
            <GerritVerify upperRange="1" lowerRange="-1" refPattern="refs/*" exclusive="false"/>
            <GerritSubmit value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPush forcePush="false" value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCreateReference value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPush forcePush="false" value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritRebase value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritPushAnnotatedTag forcePush="false" value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <GerritPushSignedTag value="ALLOW" refPattern="refs/tags/*" exclusive="false"/>
            <GerritPushMerges value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <!-- protected branches-->
            <GerritPush forcePush="false" value="DENY" refPattern="refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
            <GerritSubmit value="DENY" refPattern="refs/for/refs/heads/{RepoParams/@protectedBranches}" exclusive="true"/>
        </ScmCommitView>
        <ScmViewOnly>
            <GerritRead value="ALLOW" refPattern="refs/*" exclusive="false"/>
            <GerritCodeReview upperRange="1" lowerRange="-1" refPattern="refs/*" exclusive="false"/>
            <GerritPushMerges value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritPush forcePush="false" value="ALLOW" refPattern="refs/for/refs/*" exclusive="false"/>
            <GerritRebase value="ALLOW" refPattern="refs/*" exclusive="false"/>
        </ScmViewOnly>
    </RepoCategory>
    ````

6. Run this command to add the changes to your local directory.

   ```shell
   git add TeamForgeGerritMappings.xml 
   ````
 
7. Commit the changes.

   ```shell
   git commit -m "add user-defined repo type 'pull_request_new'"
   ````

8. Check-in the changes to your remote repository.
   
   ```shell
   git push ssh://admin@<your-domain>:29418/TF-Projects meta-config:refs/meta/config
   ````
Now the user-defined category `Pull Request New` is added successfully.

{% include image.html file="user-defined-repo-category.png" caption="User-defined repository category \"Pull Request New\"" %}

The `master` branch becomes the default protected branch for repositories that belong to the user-defined repository category, provided that its name is prefixed with "Pull Request".

{% include image.html file="user-defined-pull-request-new.png" caption="User-defined repository category \"pull_request_new\" in `TeamForgeGerritMappings.xml` file" %}

{% include image.html file="user-defined-repo-category.png" caption="User-defined repository category \"pull_request_new\" shown as \"Pull Request New\" in the UI" %}

Once the repository is created, the `master` branch becomes a protected branch of the repository by default.

{% include image.html file="user_defined_pull_req_master.png" url="http://docs.collab.net/teamforge221/images/user_defined_pull_req_master.png" caption="\"master\" added as the default protected branch for user-defined repository category \"Pull Request New\"" %}


{{site.data.alerts.hr_shaded}}
#### Related Links
* [Review Code][pullrequest]

{% include links.html %}