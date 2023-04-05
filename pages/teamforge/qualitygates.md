---
title: Quality Gates and Review Rules
keywords: quality gates, review rules
tags: [project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
folder: teamforge
permalink: qualitygates.html
last_updated: May 6, 2020
summary: This topic discusses quality gates and review rules from an administrator perspective. It also discusses some of the known issues with the project level `rules.pl` file and how to work around them. 
---

## Quality Gates in TeamForge

TeamForge Quality Gates are CollabNet specific xml files that define the conditions to be met before a commit can be merged into master (when code is ready to be pushed for production). Those xml files are stored in the `TF-Project/refs/meta/config/quality_gates` directory. TeamForge provides four predefined quality gates:

* ci_and_human_approval_required.xml
* no_approval_required.xml
* ci_approval_required.xml
* human_review_required.xml

Here is an example of a predefined quality gate xml file: `ci_approval_required.xml`

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<cn:GerritWorkflow xmlns:cn="http://www.collab.net/gerritworkflow" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" description="CI has to approve, +1 Verified allows to merge, -1 vetoes it." enableCodeReview="true" enableVerification="true" name="ci_approval_required" version="1" xsi:schemaLocation="http://www.collab.net/gerritworkflow gerritworkflow.xsd">
   <cn:SubmitRule actionIfSatisfied="allow" displayName="Verified-To-Merge">
      <cn:VotingCondition value="1" votingCategory="Verified"/>
   </cn:SubmitRule>
   <cn:SubmitRule actionIfSatisfied="block" displayName="Verified-Veto-Blocks-Merge">
      <cn:VotingCondition value="-1" votingCategory="Verified"/>
   </cn:SubmitRule>
</cn:GerritWorkflow>
````
These xml files are the building blocks for Review Rules.

## Review Rules in TeamForge

The following image shows the list of review rules that are available in TeamForge (the repository settings page).

{% include image.html file="201-qualitygates-01.png" %} 


The list of review rules can contain not only quality gates-based rules from `TF-Projects`, but also some repository specific policies. In other words, Review Rules can, but do not necessarily have to be defined using the quality gates. You can think of Quality Gates as a TeamForge-specific extension to Review Rules. 

In the above image, in addition to the four pre-defined rules based on quality gates, you can see two more global rules—`Global Rule 1` and `Global Rule 2`. Those are Review Rules that are based on custom quality gates, which are stored in the same place as the pre-defined quality gates—at `refs/meta/config` of `TF-Projects`.

The last rule—`Custom`—only applies to the given repository, and is defined in the `rules.pl` file of `refs/meta/config` branch of the current repository. It is visible only to this repository. That means, unlike the other Review Rules, it will not be shown in the **Review Rules** drop-down list of any other repository on this server.

## The Difference Between Review Rules and Quality Gates

Review Rules are stored in the `rules.pl` file of `refs/meta/config` branch in a given repository and represent the application of the given Quality Gates to this specific repository.

You can adjust it by modifying the `rules.pl` file and pushing it again to the `refs/meta/config` branch of this repository.

In a nutshell, the `rules.pl` file is generated from the Quality Gates and it looks like this:

```shell
submit_rule(Z):-cn:workflow(‘<XML of a given Quality Gates>’, Z).
````
It simply wraps Quality Gates into a prolog element.

The `rules.pl` file content is supposed to be a prolog program, which is used by Gerrit to determine the review rules. So, Gerrit expects prolog there. However, to simplify the review rules definition, CollabNet has introduced a building block called `cn:workflow` that takes the quality gates xml definition as an input, and generates a review rule out of it—so that customers are not required to implement their own review rules in prolog  any longer.

When you select a review rule from the TeamForge UI, a new `rules.pl` file is generated that is based on the selected quality gates. This file will be verified for correctness and then pushed to the `refs/meta/config` branch of the repository. At this moment, it becomes the actual review rules policy that is enforced by Gerrit on this repository.

An example `rules.pl` file:

```shell
submit_rule(Z):-cn:workflow('<?xml version="1.0" encoding="UTF-8" standalone="no"?><cn:GerritWorkflow xmlns:cn="http://www.collab.net/gerritworkflow" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" description="Merging is possible without any further approval." enableCodeReview="true" enableVerification="false" name="collabnet" version="1" xsi:schemaLocation="http://www.collab.net/gerritworkflow gerritworkflow.xsd"> <cn:SubmitRule actionIfSatisfied="allow" displayName="Merge-Always-Enabled"/> </cn:GerritWorkflow>', Z).
````

However, it is still possible to use a custom prolog `rule.pl` file if you want to. Such a file, does not have to be based on the quality gates xml. No need to use the `cn:workflow` element.


Here's an example for custom Gerrit prolog rule.

```shell
submit_rule(submit(CR, V)) :-    CR = label('Code-Review', ok(user(ID))),    V = label('Verified', ok(user(ID))).
````

Here's an example for custom xml based prolog rule.

```shell
submit_rule(Z):-cn:workflow('<?xml version="1.0" encoding="UTF-8" standalone="no"?><cn:GerritWorkflow xmlns:cn="http://www.collab.net/gerritworkflow" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" description="Merging is possible without any further approval." enableCodeReview="true" enableVerification="false" name="jenkins" version="1" xsi:schemaLocation="http://www.collab.net/gerritworkflow gerritworkflow.xsd"> <cn:SubmitRule actionIfSatisfied="allow" displayName="Merge-Always-Enabled"/> </cn:GerritWorkflow>', Z).
````

## Working with Project Review Rules

The `rules.pl` can be based on one of the predefined quality gates in `TF-Projects` `refs/meta/config` or can be totally new (Custom).

**Modifying the `rules.pl` File**

Repository specific submit rules are stored in the `rules.pl` file at `refs/meta/config` branch of the project. You must fetch and checkout the `refs/meta/config` branch. 

To create or edit the `rules.pl` file:

1. Fetch: `$ git fetch origin refs/meta/config:config`
2. Checkout: `$ git checkout config`
3. Edit or create the `rules.pl` file.
4. Git add: `$ git add rules.pl`
5. Commit: `$ git commit -m "My submit rules"`
6. Push: `$ git push origin HEAD:refs/meta/config`

Here's a list of example screenshots with information and error messages that could possibly show up when you use a custom `rules.pl` file. 

Example-1
: The following message appears when the review rule selected is valid and is not based on one of the predefined quality gates. 
: {% include image.html file="201-qualitygates-02.png" %}

Example-2
: A warning message when the review rule has an empty name attribute.
: {% include image.html file="201-qualitygates-03.png" %}

Example-3
: An error message that shows up when the current review rule has no name. 
: {% include image.html file="201-qualitygates-04.png" %}
: To fix this, check out the `rules.pl` file and provide a name and push it back to `refs/mets/config`.

Example-4
: A warning message that shows up when the `rules.pl` file of a specific repository has the same name as one of the predefined quality gates, but the submit rules are different. Such a `rule.pl` is still valid, but it is a good practice to have unique names. 
: {% include image.html file="201-qualitygates-05.png" %}

Example-5
: An error message when you use [UserFilter][userfilterremoval] (removed from Gerrit) in your `rule.pl` file. 
: {% include image.html file="201-qualitygates-06.png" %}
: To fix this, check out the `rule.pl` file, remove the `UserFilter` and push it back to the `refs/meta/config` branch of the project repository. 

## Quality Gates Location Change from TeamForge 20.0

The quality gates xml files were stored at `/opt/collabnet/gerrit/etc/quality_gates` directory in TeamForge 19.0 and earlier. 

However, with TeamForge 20.0 and later, the quality gates xml files have been moved to the `refs/meta/config` branch of the `TF-Projects` repository in Gerrit. This makes it simple as TeamForge administrators no longer need file system level access to the Gerrit server to add or remove rules. 

{% include note.html content="You cannot modify or delete predefined quality gates. However, you can add new ones." %}

Here's a [blog post](https://resources.collab.net/blogs/you-shall-not-pass-control-your-code-quality-gates-with-a-wizard-part-i) for further reference. 











{% include links.html %}