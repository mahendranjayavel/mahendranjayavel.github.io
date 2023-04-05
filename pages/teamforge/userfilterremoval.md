---
title: UserFilter Removal 
keywords: git, gerrit, scm, user filter
tags: [project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: May 11, 2020
permalink: userfilterremoval.html
folder: teamforge
summary: The `UserFilter` removal from the Quality Gates is a direct outcome of the removal of the `current_user` predicate from the open source Gerrit.
---

## What is a `UserFilter`?
`UserFilter` is one of building blocks for Quality Gates. It is one of the SubmitRule filters that determines whether a change qualifies for submission or not. SubmitRule with matching filters (or with no filters at all) are evaluated for submission. 

<!-- `UserFilter` is a part of SubmitRule which is a building block for Quality Gates. The SubmitRule is a rule that is evaluated to decide when a given change can be submitted. 
Only SubmitRule whose filters match (or have no filters) will be evaluated. `UserFilter` is one of the filters that can be used to decide which SubmitRule will be evaluated. -->

`UserFilter` has the following attributes:
* `CurrentUser`
* `CurrentUserGroup`
* `ignore Author/NonAuthor`
* `ignore Committer/NonCommiter`
* `ignore Owner/nonOwner`

For example, if you want to disable submit for a user, you can use a `UserFilter` with the `ignoreAuthor` attribute set to `true`. In such a case, the SubmitRule would not be satisfied if the user who is viewing the code review is the author of the latest patch set of that code change. In this case, the code change is not submittable by that user and the Submit button is disabled. This SubmitRule holds good in all other cases. 
 
## What are the reasons to remove `UserFilter` from the quality gates?

The `UserFilter` removal is a direct outcome of the removal of the [current_user](https://gerrit-review.googlesource.com/c/gerrit/+/143251) predicate from the open source Gerrit. It is not possible to implement the `UserFilter` without this predicate, as the quality gates would have no information about the current user any longer.

## Why was the current user predicate removed from open source Gerrit?

The current user predicate is removed because of the fact that the result of a submittability check should not depend on the user who is asking for it. For more information, [click here to follow the discussion on this topic](https://groups.google.com/forum/#!msg/repo-discuss/vW6XhUOkqik/Ea4pco6vlCQJ). 

Here are a few arguments that support the `UserFilter` removal:

* Using the current user predicate may produce some surprising results such as two different users being presented with completely different sets of required labels—or even different submit type.  If user A clicks submit, it might be **Always Merge**, but if user B clicks submit, it might be **Cherry-Pick**.
* Support for the `is:submittable` query. If the `current_user` predicate is used in the prolog rules, the '`submittable` field could vary on a user-to-user basis. So, it needs to be re-evaluated for every new request. Re-evaluating this field for every new request is not a good idea as this operation is quite costly.
* You can achieve equivalent results without using the `current_user` predicate.

## How can I check if I am affected by the `UserFilter` removal?

[Use this plugin](https://ctf.open.collab.net/sf/go/projects.sfdl/frs.collabnet_teamforge_git_integrat.20_1_workflow_readiness_checker) to check if you are affected.

## How to replace `UserFilter` from my Quality Gates?

Let’s consider the SubmitRule that mandates a user to be both the author and submitter of the change, for example. 

Here's the SubmitRule rule:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cn:GerritWorkflow enableVerification="true" enableCodeReview="true" description="Only the author can submit the change, others can still informally review and verify" name="Author only"  version="1" xsi:schemaLocation="http://www.collab.net/gerritworkflow gerritworkflow.xsd" xmlns:cn="http://www.collab.net/gerritworkflow" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<cn:SubmitRule displayName="Author-To-Submit" actionIfSatisfied="allow">
		<cn:UserFilter ignoreNonAuthor="true" />
   </cn:SubmitRule>
</cn:GerritWorkflow>
 ````

As you can see, the above rule uses a `UserFilter` with the `ignoreAuthor` attribute. Let's see how to have this done without the `UserFilter`. 

Let's first understand how the above rule works. 

This rule allows only the author to submit the change. No review is required, so the rule will be submittable for the author but not submittable for anyone else independent from the voting. That means that author is the only one who can decide if the rule can be submitted.

You can achieve this by requiring the author to give his approval (Verify +1) to make change submittable:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<cn:GerritWorkflow enableVerification="true" enableCodeReview="true" description="The change can only be submitted if the author has verified it, others can still informally review and verify" name="Author only" version="1" xsi:schemaLocation="http://www.collab.net/gerritworkflow gerritworkflow.xsd" xmlns:cn="http://www.collab.net/gerritworkflow" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<cn:SubmitRule displayName="Author-Verify-To-Submit" actionIfSatisfied="allow">
		<cn:VotingCondition value="1" votingCategory="Verified">
			<cn:VoteAuthorFilter ignoreAuthorVotes="false" ignoreNonAuthorVotes="true" />
		</cn:VotingCondition>
	</cn:SubmitRule>
</cn:GerritWorkflow>
 ````

As you can see, the above rule mandates the approval, but the only person whose vote will be considered is the author. So, we now have replaced the `UserFilter` with the `VotingCondition` and `VoteAuthorFilter` attributes. In other words, no one can submit without a vote from the author. Once the author gives a `Verified +1` vote, anyone who has the submit permission can submit the change.

On the other hand, what if you want only a specific person to submit? That’s also possible if you create a special Gerrit group and give only members of this group the right to submit.

## How to verify if you can upgrade to TeamForge—Git integration 20.1 or later? {#workflowreadiness}

Pre-requisites
: * SSH access to port 29418 of the Gerrit server.
: * User that is a member of the privileged Administrators group. This section uses the admin user for illustrative purposes.
: * The `plugins.allowRemoteAdmin` option enabled in the `/opt/collabnet/gerit/etc/gerrit.config` file. It is enabled by default. The following error occurs if not: `Fatal: Remote plugin administration is disabled`. If so, you must add the option to the `gerrit.config` file and restart Gerrit. 

1. Check your Gerrit version. 
   ```shell
   ssh -p 29418 amdin@<gerrit-host> gerrit version 
   ````

   Make sure you are either on Gerrit 2.14 or 2.15. 

2. [Download](https://ctf.open.collab.net/sf/go/projects.sfdl/frs.collabnet_teamforge_git_integrat.20_1_workflow_readiness_checker) the right version of the workflow readiness checker plugin for the version of Gerrit you have (2.14 or 2.15).
 
3. (Optional) Verify the list of installed plugins and make sure that the workflow readiness checker plugin is not installed already.
   ```shell
   ssh -p 29418 <gerrit-host> gerrit plugin ls 
   ````

4. Install the workflow readiness checker plugin. For example, run the following command if you have Gerrit 2.15.
   ```shell
   ssh -p 29418 admin@<gerrit-host> gerrit plugin install -n workflow-checker-2.15.jar - <workflow-checker-2.15.jar 
   ````

5. Verify the upgrade readiness and fix your setup, if required. 
   1. Go to: `https://<gerrit-host>/gerrit/plugins/workflow-checker/201readiness`
   2. Verify if your server is ready for the upgrade. 

      The following message appears if your server is ready for the upgrade. 
      ```shell
      Site is ready for upgrade to TeamForge 20.1 or higher.
      No usage of the deprecated UserFilter was detected. 
      ````

      If not, you may see a message that says your site is not ready. For example, the following message appears if the site is not ready for the upgrade. 
      {% include image.html file="201-userfilterremoval.png" %}

      If you see a similar message, you must edit the affected xml files and remove the `UserFilter` from them as discussed earlier. 

6. Once you have fixed all the XML files, verify the server readiness again by reloading the workflow readiness checker plugin.
   ```shell
   ssh -p 29418 admin@localhost gerrit plugin reload workflow-checker
   ````

7. Once you see the message that says the server is ready for an upgrade, you may uninstall the plugin.
   ```shell
   ssh -p 29418 admin@<gerrit-host> gerrit plugin rm workflow-checker  
   ````

8. Verify that the plugin has been uninstalled completely. 
   ```shell
   ssh -p 29418 <gerrit-host> gerrit plugin ls 
   ````

   Make sure the workflow-checker plugin is not on the list and you are ready for the upgrade.

{% include links.html %}