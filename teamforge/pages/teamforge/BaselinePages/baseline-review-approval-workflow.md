---
title: Review Baselines
keywords: review project baseline, approval for project baseline
tags: [baseline, ctf_18.2, ctf_18.3]
sidebar: teamforge_sidebar
last_updated: Apr 12, 2019
permalink: baseline-review-approval-workflow.html
folder: teamforge
summary: A Baseline or a Project Baseline, once created can be reviewed. During the review cycle, the Baseline or the Project Baseline undergoes various status transitions as defined by the Baseline Administrator.
---

{% include callout.html type="primary" content="**Prerequisite**: You must have **Baseline Review** permission to review a Baseline or a Project Baseline." %}

## Baseline Review Process 

You can take an action on a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baseline</a> or a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a> that is submitted for review. The available actions are based on the workflow status transition associated with the user role. For more information on the workflow status transitions, see [Add Status Transition Workflow][baseline-settings.html#addstatustransitionworkflow].

You can edit a Baseline or a Project Baseline (only the baseline fields; not the filter criteria) as long as its custom status is having the status type `Open`. For more information on how to configure custom statuses, see [Configure Custom Statuses][baseline-settings.html#configurecustomstatuses]. 

You cannot edit a Baseline or a Project Baseline in a terminal status, that is, custom statuses that are assigned to the status type `Approved` or `Rejected`. 

You cannot re-submit a rejected Baseline or a Project Baseline. If a Baseline or Project Baseline is rejected, you can create a new Baseline or a Project Baseline and initiate the review process again. 

## Review a Baseline or a Project Baseline

1. Log on to TeamForge and select a project from the **My Workspace** menu.

2. Click **Baselines** from **Project Home** menu.

3. Select **Pending Review** on the left navigation menu.

   {% include image.html file="reviewpendingbaselines.png" caption="List of review pending baselines" %}

4. Click a Baseline or a Project Baseline on the **Pending Review Baselines** page.

   {% include image.html file="review-baseline.png" %}

5. Click the **Submit** drop-down button. This lists the custom statuses associated with the workflow transitions for your user role. For more information on how to add workflow transitions, see [Manage Status Transition Workflow][baseline-settings.html#addstatustransitionworkflow].

6. Select the required status and click **Submit**.

7. If you have selected a custom status whose status type is either **Approved** or **Rejected**, you are asked for the reason to approve or reject. However, while rejecting the Baseline or a Project Baseline, you must give a reason/comment for rejecting it.

## Add Comments {#addcomments}

You can add comments to a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baseline</a>. or a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a> during the review process.

To add comments to a baseline:

1. Select the Baseline or the Project Baseline, for which you want to add comment, from the list of baselines.

2. Enter the required comments in the text box in the **Comments** section and click the **Save** link (or press **Shift+Enter**).

   {% include image.html file="baseline-comments.png" %}

* **Show All** option

  **Show All** is the default option selected in the **Comments** section to show the comments and audit logs.

  {% include image.html file="baseline-comments-showall.png" %}

* **Comments Only** option

  To view only the comments, select the **Comments Only** option in the **Comments** section.

  {% include image.html file="baseline-comments-only.png" %}

## View Baseline {#viewbaseline}

You can view a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}"> Baseline</a> or <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a>, after it is approved or rejected. In other words, you cannot edit the baseline fields after the status of the Baseline or Project Baseline changes to **Approved** or **Rejected**.

{% include image.html file="view-approved-baseline.png" %}


{% include links.html %}


