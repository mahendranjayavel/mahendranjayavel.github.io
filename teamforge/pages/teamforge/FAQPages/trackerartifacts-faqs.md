---
title: FAQs on Tracker Artifacts 
keywords: FAQ, frequently asked questions
tags: [faq, tracker_artifacts]
sidebar: teamforge_sidebar
permalink: trackerartifacts-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on Tracker Artifacts.
---

## Can I assign an artifact or a task to a group of users?

Unfortunately, this is not possible with the current implementation of groups in TeamForge.

As a workaround, you can create a new user account and set its email address to that of a mailing list that all group members are subscribed to. Then the submitting user can assign the artifact to this user account, and the mailing list will be notified. 
{{site.data.alerts.hr_shaded}}

## How do I create an artifact through email?

To create a tracker artifact using email, send an email message to `<tracker id>@<TeamForge server>`.

You can find the tracker id on the **Artifact List View** page. Fields are mapped as follows:

  * To: Tracker email address
  * Subject: Artifact title
  * Body: Artifact description
  * Attachments: Attachments
{{site.data.alerts.hr_shaded}}

## Why do the open tracker counts differ from when I filter on 'Open'?

The 'Open' category on the summary screen is based on the meta status 'Open'. It includes multiple statuses: Open, Fixed, and any other statuses that are defined as equivalent to Open by the Tracker admin for your project

For example, suppose the Tracker Summary block shows 21 open artifacts. However, when filtering on the 'Open' status, only five artifacts are displayed.

If you filter by 'All Open', you will see all 21 issues with statuses defined as Open. If you filter specifically by 'Open', you will see only the artifacts that specifically have the status 'Open'.
{{site.data.alerts.hr_shaded}}

## Is it possible to move an artifact from one tracker to another?

Yes, it is possible to move an artifact from one tracker to another tracker.

Simply use the **Cut** button to remove the artifact and then paste it to another artifact. You can also change the tracker type while editing the artifact using the **Edit Artifact** page. The destination tracker need not be in the same project, but if the tracker definitions differ, data could be lost.
{{site.data.alerts.hr_shaded}}

## What happens when a changed value makes a dependent field invalid?

When a user changes a field value on which the values of other fields depend, some dependednt values may need to be corrected.

This can happen if:

  * A parent value has been changed in such a way that its child values are inconsistent.
  * A text value has been changed in such a way that it no longer matches the regular expression that describes the acceptable values.

  {% include note.html content="Linking fields in dependent relationships does not modify existing data. However, when users later modify fields that are linked, they do have to adhere to the relationships among the fields." %}

### Changing Values

When a user changes the value of a field, and the value in another field becomes invalid as a result, the latter field (we call it the 'dependent' field) is reset to its default value the next time someone updates that artifact.

For example, picture a tracker called 'Interior decoration' in which, if the **Color Scheme** field is set to `Warm`, the **Carpet color** field can be set only to `Red`, `Orange` or `Yellow`. `Red` is the default value.

User 1 sets **Color Scheme** to `Warm` and **Carpet color** to `Yellow`.

User 2, after consulting the client, comes in and changes the color scheme to `Cool`. Now the allowed value of **Carpet color** are `Blue`, `Gray`, and `White`, with `Blue` as the default. But the actual value is still `Yellow`, which is now invalid. It's up to the user who is updating the artifact to choose a new color from the new set of valid colors. If the user doesn't make a choice, TeamForge automatically changes the value **Carpet color** to `Blue`, because that's the default value when **Color scheme** is set to `Cool`.

### Changing Dependency Rules

When you restructure a hierarchy of dependent values in a way that leaves invalid child fields in multiple artifacts, each of those artifacts must be fixed the first time a user edits it.

For example, in the artifact `room1`, User 1 has set the **Color scheme** field to `Warm` and the **Carpet color** field to `Red`. Suddenly User 2, the project manager, realizes that red is a terrible color for carpeting. User 2 changes the tracker settings so that **Carpet color** can be set only to `Orange`, `Yellow`, or `Maroon`.

The next time User 1 comes back to the `room1` artifact, TeamForge warns that the field value is in an inconsistent state.If the user tries to edit the specific field that is inconsistent, changes to the artifact cannot be saved until the user selects one of the new allowed values for that field.

### Changing Text Validation Rules

If you change the regular expression that governs what content is allowed in a text field, each affected field must be fixed the first time a user edits it.

For example, imagine that your 'Interior decoration' tracker includes a text field in which users can record the telephone number of a carpet installer. You set up a validation rule like `[(]\d\d\d[)]\s\d\d\d[-]\d\d\d\d` to ensure that only standard U.S.-format phone numbers can be entered. 

The tracker has been in use for a week when you realize that email would be a better way to communicate with carpet installers. You change the validation rule to something like `\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}\b`, to ensure that users will enter an email address.

The next time a user tries to update an artifact with a telephone number value in that field, TeamForge warns that the field value is in an inconsistent state. If the user tries to edit the specific field that is inconsistent, changes to the artifact cannot be saved until the user enters a value for that field that matches the new validation rule.

### Deleting a Parent Field

If you delete a field that contains values that another field's values depend on, the dependent field becomes a standard single-select field on its own. No correctionis needed.


### Changing 'requiredness'

 * When a field has a parent field that is required, the child field's default value is set to `None`. If that required parent field is deselected, the child field no longer has to be required, but `Required` remains the default.
 * If you require a specific field value before an artifact can be placed in a given status, that field's children are subject to the same requirements. See [Create a Tracker Workflow][trackers-creatingatracker.html#createatrackerworkflow] for more about controlling what status an artifact can be in.

{% include links.html %}