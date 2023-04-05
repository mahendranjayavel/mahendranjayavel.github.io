---
title: Baseline Settings
keywords: configure custom status, configure custom fields, set up workflow transitions
tags: [baseline, ctf_18.3]
sidebar: teamforge_sidebar
last_updated: Mar 4, 2020
permalink: baseline-settings.html
folder: teamforge
summary: As a baseline administrator, you can configure the custom attributes used in the baselines, configure the custom statuses, and manage workflow status transitions and field inclusions.
---

{% include callout.html type="primary" content="**Prerequisite**: You must have **Baseline Admin** permission to view/access the **Settings** menu." %}


## Manage Custom Attributes {#configurecustomattributes}

Custom attributes are user-defined attributes that a Baseline Administrator can configure for <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baselines</a>. You can add, edit, delete, and reorder custom attributes.

### Add Custom Attributes

You can add custom attributes as required. 

To add a new custom attribute:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.  

4. Click **Settings > Attributes** from the side navigation menu. 

   {% include note.html content="The **Attributes** page shows the list of both the system-defined attributes and custom attributes." %}

   {% include image.html file="custom-attributes.png" %}

5. Click the **+ Attribute** button.

6. Enter the **Field Name** and select the **Field Type**.

   {% include note.html content="When adding single-select (drop-down list) and multi-select (check box) fields, you need to provide at least 2 values to each of these fields. Otherwise, while saving, you will be prompted to provide the values." %}

7. **(This step is required only for single-select and multi-select fields):** Add at least two values. To add more values, click the **+ Add Value** button.

8. Select the **Required Field** check box to make the field mandatory.

9. Click **Save**.


### Edit Custom Attributes

You can edit the existing custom attributes, if required. When editing the single-select and multi-select fields, you can add more values to them. However, you cannot edit the field type. In other words, you can only edit the field name,  its values (applicable for single-select and multi-select fields), and select or clear the **Required Field** check box.

To edit any existing custom attribute/field:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.  

4. Click **Settings > Attributes** from the side navigation menu. 

5. click the edit ( {% include inline_image.html file="baseline-edit-icon.png" %}) icon against the custom attribute that you want to edit.
   
6. Change the field name and its corresponding value(s) (if applicable).

   {% include note.html content="You cannot edit the field type." %}

7. Select the **Required Field** check box (if not already selected) to make the field `mandatory`. Clear the check box to make the field `optional`.

8. Click **Save**.

### Delete Custom Attributes

You can delete any existing custom attribute, if required. However, you cannot delete the system-defined attributes. To delete an existing custom attribute, click the delete ( {% include inline_image.html file="baseline-delete-icon.png" %}) icon against the custom attribute that you want to delete.

### Reorder Custom Attributes

You can reorder both the system-defined and custom attributes, if required. To reorder a custom attribute, just drag the custom attribute and drop it anywhere within the list of custom attributes.

Based on the order appearing on the **Attributes** page, the attributes (fields) are shown when creating baselines and baseline definitions.


## Manage Custom Statuses {#configurecustomstatuses}

The status of a baseline changes at every stage of the baseline workflow. The baselines are categorized based on their statuses. You can create custom statuses based on your organizational requirements. However, the custom statuses are defined based on the system-defined status types. 

`Open`, `Approved`, and `Rejected` are the available status types. You can create more than one custom status for each status type. 

If a custom status has `Approved` or `Rejected` as its status type, then that custom status is considered as the terminal status.

{% include image.html file="baseline-admin-meta-status.png" %}

### Add Custom Statuses

To create a custom status:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.   

4. Click **Settings > Workflow** from the side navigation menu.
   
   {% include image.html file="baseline-admin-workflow.png" %}

5. Click the **+ Status** button on the **Workflow** page to add a new custom status.

   {% include image.html file="baseline-admin-status-button.png" %}

6. Enter the custom status name and select the system-defined status type.

   {% include image.html file="baseline-admin-custom-status.png" %}   

7. Click **Save**.

### Edit Custom Statuses

You can edit any existing custom status including the default custom status, if required. 

To edit an existing custom status, click the edit ( {% include inline_image.html file="baseline-edit-icon.png" %}) icon against the custom status that you want to edit.

{% include image.html file="edit-custom-status.png" %}

The edited status is also shown in the workflow transition(s) associated with the status. For more information on the status transition workflow, see [Add Workflow for Status Transitions][baseline-settings.html#addstatustransitionworkflow].

### Delete Custom Statuses

You can delete any existing custom status, if required, except the default custom status. To delete an existing custom status, click the delete ( {% include inline_image.html file="baseline-delete-icon.png" %}) icon against the custom status that you want to delete.

{% include image.html file="delete-custom-status.png" %}

Be aware that deleting a status will also delete the workflow transition associated with the status.

### Reorder Custom Statuses

You can reorder the custom statuses as required. To reorder a custom status, just drag the custom status and drop it anywhere within the list of custom statuses.


## Manage Workflow Status Transitions {#addstatustransitionworkflow}

You can add the workflow status transitions based on the organizational requirements and associate the project user roles having baseline review permission with these status transitions. You can add one or more workflow status transition for every user role. 

To add a new workflow for status transition:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.   

4. Click **Settings > Workflow** from the side navigation menu.
   
   {% include image.html file="baseline-admin-workflow.png" %}

5. Click the **+ Transitions** button on the **Workflow** page to associate a project role with the status transitions.

   {% include image.html file="baseline-admin-add-transition.png" %}

6. Select the project role and the from and to statuses.

   {% include note.html content="The **From Status** drop-down list contains only the custom statuses with the status type _Open_." %}

   {% include image.html file="baseline-admin-transition.png" %}

   {% include note.html content="The status that is already added to the **To Status** drop-down list will not be available in the **From Status** drop-down list." %}

7. Click the **Add Transition** link to add more status transitions. 

8. Click **Save**.


## Manage Field Inclusions {#includeexcludefields}

Baseline manifest field configuration involves selecting the fields of Trackers and Documents that must be included when baselines are created or exported. The **Field Inclusions** setting lets you select the fields that you want to include in baselines. Such selected fields included as part of baselines are called the baseline manifest fields.

  {% include important.html content="Manifest field configuration is mandatory for baselining any newly created tracker." %}

### Include Fields from Trackers

To select the Tracker fields that you want to include in baselines:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.   

4. Click **Settings > Field Inclusions** from the side navigation menu.

   {% include image.html file="include-tracker-fields.png" %}

5. Select the **TRACKERS** tab, if not already selected.

   {% include note.html content="The **TRACKERS** tab is selected by default." %}   

6. Select the Tracker from the **Tracker** drop-down list.

7. Select a field from **All fields** list.

   The following mandatory Tracker fields are included in baselines by default—ArtifactId, Title, Status and Planning Folder.

8. Click the {% include inline_image.html file="include-button.png" %} button to move the selected field to the **Selected fields** list.

9. To exclude a field, select the field from the **Selected fields** list and click the {% include inline_image.html file="exclude-button.png" %} button to move the field back to the **All fields** list.

10. Repeat steps 7 and 8 to include all the fields you want.

11. Click **Save**.

### Include Fields from Documents

To include/add Document fields:

1. Log on to TeamForge as Baseline Administrator.

2. Select a project from **My Workspace**.

3. Click **Baselines** from the **Project Home** menu.   

4. Click **Settings > Field Inclusions** from the side navigation menu. 

   {% include image.html file="include-tracker-fields.png" %}

5. Select the **DOCUMENTS** tab.

   {% include note.html content="The **TRACKERS** tab is selected by default." %}   

   {% include image.html file="include-document-fields.png" %}

6. Select a field from **All fields** list.

7. Click the {% include inline_image.html file="include-button.png" %} button to move the selected field to **Selected fields** list.

      The following mandatory Document fields are included in baselines by default—DocumentId, Title, Version, and Status.

8. To exclude a field, select the field from the **Selected fields** list and click the {% include inline_image.html file="exclude-button.png" %} button to move the field back to the **All fields** list.

9. Repeat steps 6 and 7 to include all the fields you want.

10. Click **Save**.

### Reorder the Fields

You can reorder the fields added to the **Selected fields** list. To reorder a field within the **Selected fields** list, just drag the field and drop it anywhere within the list.

Based on the order set in the list of selected fields, the fields are shown on the preview window of Trackers and Documents and in the results of the **Compare Baselines** page. For example, if the **Category** field appears next to the **Status** field in the **Selected fields** list, both the fields appear on the preview window and the **Compare Baselines** page.

<!-- ### Exclude Fields from Selection

You can exclude/remove Tracker and Document fields (non-mandatory) added to the **Selected fields** list. Excluded field(s) will be moved back to the **All fields** list. You can always include the field(s) at any point in time.

To exclude/remove the Tracker or Document fields added to the **Selected fields** list:

1. Select the required field from **Selected fields** list.

2. Click the {% include inline_image.html file="exclude-button.png" %} button to move the selected field back to the **All fields** list.

{% include note.html content="You cannot exclude/remove the mandatory fields once they are added to the **Selected fields** list."%} -->


<!-- ### Which are the mandatory Tracker and Document fields? {#mandatoryfields}

When including the Tracker and Document fields, the following fields of Trackers and Documents must be added to the selected list of fields. If you don't add these fields, while saving your changes, you will be prompted to include those fields.

* **Mandatory Tracker Fields**&mdash;ArtifactId, Title, Status and Planning Folder

* **Mandatory Document Fields**&mdash;DocumentId, Title, Version, and Status
 -->


{% include links.html %}

