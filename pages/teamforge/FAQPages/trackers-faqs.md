---
title: FAQs on Trackers
keywords: FAQ, frequently asked questions
tags: [faq, trackers]
sidebar: teamforge_sidebar
permalink: trackers-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on Trackers.
---

## What fields can I use in a tracker? {#trackerfields}

You can use fields provided by TeamForge, and you can create your own custom fields. Most trackers use a mix of TeamForge-provided fields and user-defined fields.

### TeamForge-provided fields
Some fields are provided by TeamForge for all trackers.

   * **System-defined Fields** - Some TeamForge-provided fields are always present in every tracker. These are identified as "system-defined" fields in the field list.

     * The **Artifact ID**, **Title**, and **Description** fields are system-defined fields. They are always present and always come first when you view an artifact. 
     * Some system-defined fields can be reordered. For example, the **Assigned To** field is a system-defined field, so it is always present, but you can move it around in your tracker's display.

   * **Configurable Fields** - Some fields are available for any tracker, but can be modified in different ways. These are called "configurable" fields.

     * Any configurable field can be a required field. When a field is required, a user cannot submit an artifact without providing a value for the field. 
     * Some configurable fields can be disabled. When a field is disabled, TeamForge does not store data for it or include it in calculations. For example, the **Reported in Release** field is meant for tracking bugs, so you may want to disable it for a tracker that's for user stories. But the **Status** field is important for any tracker, so it can't be disabled.
     * For some configurable fields, you can specify whether users see the field when they submit an artifact.
     * Some configurable fields need values for users to choose from. You have to provide those choices.
     * You can set the width and height of configurable text fields.

### User-defined fields

When none of the TeamForge-provided field captures exactly the information you need to track, you should create a field tailored to your own needs. Such fields are identified in the field list as "user-defined" fields. See [Create Custom Tracker Fields][trackers-creatingatracker.html#customfields] for details.
{{site.data.alerts.hr_shaded}}

## Can I limit the number of characters for fields in a tracker?

No, it is not possible in the current version of TeamForge.

Currently, while creating the tracker customer flex field of input type 'Text Entry', you cannot control the maximum number of characters to be allowed. There is 'Field Width' that takes values to control the size of the text field, but not to limit number of characters entered.
{{site.data.alerts.hr_shaded}}

## Not all my team members appear in the "assigned to" field. Why is that?

In order to appear in the Assigned To field, the user must belong to a role giving them edit/view permissions on the tracker.

## How does TeamForge automatically sum up effort estimates?

As you refine your agile project plan, you break down user stories into smaller stories, and eventually into tasks. TeamForge can watch the changing effort estimates all the way down the hierarchy, and give you a running total for each parent artifact and all its children.

**Example**

Imagine that you originally created a user story to describe the need for a "Shopping Cart" feature in your e-commerce application. You gave this story a rough effort estimate of 20 units, and entered that figure in the **Effort** field.

Upon further discussion, your project team recommends breaking the story down into three tasks:

 * Database (5 units)
 * Back End (15 units)
 * UI (8 units)

You create artifacts for those three tasks, identifying them as children of the user story artifact, and enter their respective effort estimates in the **Effort** field in each task artifact.

Back in the "Shopping Cart" story artifact, you select **Autosum effort** to indicate that effort number for this artifact should be rolled up from its children.

Now, rather than showing the manually entered number (20 units), your user story artifact shows the figure derived from adding the effort estimates for all three child artifacts (28 units).

### Double-counting?

Effort numbers are never "double-counted" when auto-summing is on. For example, if the sum for planning folder A would include effort for child C and parent P, and P has autosumming turned on, C's effort number is only counted once.

However, when auto-summing is off, the effort numbers from parent P and child C can both contribute to totals. So if a planning folder A includes parent P (autosum=off, effort=3) and child C (effort=5), then the pair contributes a total of 8 to A's total.

An artifact's effort number is calculated from the effort numbers of its immediate children artifacts only. This is true whether or not those children's numbers are themselves automatically derived.

 {% include note.html content="When a tracker is disabled, artifacts from that tracker do not contribute to the effort totals calculated for any planning folder they are in." %}

### Permissions

If you are a long-time user of TeamForge tracker features, be aware that autosumming can lead to some situations you haven't seen before. For example, picture these scenarios:

 * Artifact A is assigned to Sanil. He therefore has permission to edit that artifact, but he does not have permission to edit the artifact's parent, artifact B. Artifact B is assigned to Sergey, who has edit permission for both artifacts. Sergey turns on autosumming for artifact B. When Sanil updates his effort estimate for artifact A, the content of the **Effort** field in artifact B is updated as a result, even though only Sergey is explicitly authorized to change values in artifact B.

 * Connie creates artifacts X and Y, and declares both of them children of artifact Z. Then she assigns artifact Z to Thiru. Thiru now has edit permission for artifact Z. But he cannot edit artifact X or artifact Y, because he does not have access to the separate tracker where they live. When Thiru turns on autosumming for artifact Z, that artifact's **Effort** field includes the sum of artifacts X and Y, even though Thiru is not explicitly authorized to see any data from those artifacts. (In fact, he may not even know that artifacts X and Y exist.)
{{site.data.alerts.hr_shaded}}

## How do you measure "effort"?

Effort is a uniform span of time for measuring work on your product. Defining the unit of effort is an essential part of planning your work.

TeamForge shows you the effort that has been estimated, and actually expended, for each artifact on the tracker summary screen. Parent artifacts can automatically add up these effort figures from their child artifacts’ effort figures. The calculator icon indicates that the artifact’s effort is a sum of its child artifacts’ effort within the project. When the effort from children artifacts in projects across the TeamForge (foreign children) is included in calculations, the icon ( {% include inline_image.html file="Includeartifactsacrossprojects.png" %})  appears.

 {% include note.html content="When a tracker is disabled, artifacts from that tracker do not contribute to the effort totals calculated for any planning folder they are in." %}

The unit of effort should be something that makes sense in your environment. TeamForge does not require any particular unit. Your unit of effort might be hours per person, days, weeks, or something else. (If you are using a scrum-based project methodology, you may have opted to measure effort in relative terms, using points (story points), in which case you can leave the **Effort** fields blank.)

For example, some teams use the "ideal hour" as their standard unit of effort. To define an ideal hour, consider all the activities in a standard work day that must be done but don't directly contribute to development: installing and configuring tools, eating lunch, responding to email and instant messages, providing customer support, etc. For every hour of direct development work, how much time goes into these activities, on the average? If the answer is about a half hour, then your ideal hour is 1.5 clock hours.

Now consider a task that you judge to represent about four hours of direct development work. The value you'll enter in the **Effort** field is 6, because for each hour of direct development you'll need an extra half hour to make that development work possible.

In an environment with a lot of overhead -- for example, a group that relies on a very complex tool set -- your ideal hour might equal two clock hours, or perhaps much more. This is not in itself a problem: the point is not to suppress needed activities, but to plan realistically, in order to reduce the need for routine scheduling adjustments and to forecast more reliably.

(However, when units of effort seem radically out of line with reality, this may be a clue that something in the environment could be better optimized.)

For a quick view of the effort values you are working with, check the Planning Folder Summary page.

 * The estimated, remaining and actual values are listed for the planning folder as a whole.
 * The **Est** column shows the original estimated effort value for each artifact in the folder.
 * The **Rem** column shows the value remaining for each artifact after the latest update to the artifact.
 * The **Act** column shows the actual effort expended for each artifact, calculated after the work is done.

 {% include tip.html content="To make your tracking easier, consider having TeamForge automatically generate a running total of estimated effort for a whole hierarchy of user stories or tasks." %}

{% include links.html %}
