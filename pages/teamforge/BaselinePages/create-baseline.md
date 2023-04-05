---
title: Create and View Baselines
keywords: creating baseline
tags: [baseline, ctf_18.2, ctf_18.3, ctf_19.0, ctf_19.2, ctf_19.3]
sidebar: teamforge_sidebar
last_updated: Oct 6, 2020
permalink: create-baseline.html
folder: teamforge
summary: Create a Baseline when you accomplish specific milestones in your project or when you release or deliver a product. You can create a Baseline from either a Baseline Definition or from the ground up.
---

{% include callout.html type="primary" content="**Prerequisite**: You must have **Create/View Baseline** permission to both create and view Baselines. **View Only** permission allows you to just view the Baselines." %}


## Save a Draft of Baselines

You can now save a draft of the baseline that's being created. Use the **Save as Draft** button in the **Create Baseline** page to save a draft of the baselines that are being created. 

Once saved, you can edit or delete draft baselines at a later point in time.

{% include image.html file="save-as-draft-button.png" caption="Save as Draft Button" %}

You can view the list of draft baselines by selecting **Draft** from the left navigation menu. The total number of draft baselines is shown next to the **Draft** option within parenthesis `()`.

{% include image.html file="draft-baselines.png" caption="List of Draft Baselines" %}

## Create Baselines {#baselinewithoutBDef}

To create a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baseline</a>:

1. Log on to TeamForge and select a project from **My Workspace**.
2. Click **Baselines** from the **Project Home** menu.
3. Click **New Baseline**.   
   {% include image.html file="baseline-new.png" %}
4. Enter values for the required fields such as **Title**, **Description** and **Category**.
   {% include image.html file="create-baseline.png" %}
5. Define the filter criteria.

   You can define the filter criteria for Trackers, Documents, Source Code Management, File Releases and Binaries. Select the following tabs to view the instructions.

   {% unless site.output == "pdf" %}
   {% include baseline/baseline-config-1.html %}
   {% endunless %}

   {% unless site.output == "web" %}
   {% include baseline/baseline-config-1-pdf.html %}
   {% endunless %}    

   <br>
   <div class="panel panel-info">
   <div class="panel-heading">Use an Existing Baseline Definition</div>
   <div class="panel-body" markdown="1">
   Instead of defining the filter criteria from the ground up, you can use the **Definition** drop-down list to select an existing <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline_definition}}">Baseline Definition</a> and create an <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baseline</a>. 

   Select a Baseline Definition from the **Definition** drop-down list. The selected Baseline Definition's filter criteria are auto-populated.

   Review the filter criteria and modify the filters, if required.
   </div>
   </div>

6. Select one or more <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.external_baselines}}">external baselines</a> from the **External Baselines** drop-down list.

   {% include image.html file="external-baselines.png" %}

   * You may click the selected external baselines to view them.
   * You can search for the external baselines that are not listed in the **External Baselines** drop-down list.
   * Only two selected external baselines can be shown at a time. To see the complete list of selected baseline definitions, click **+ More** in the **External Baselines** drop-down list.
   
7. Click **Preview to Create** to preview the Baseline. 

   <!-- Use this for web output -->
   {% unless site.output == "pdf" %}
   [![Preview Baseline](images/baseline-preview.png)](images/baseline-preview.png)
   {% endunless %}

   <!-- Use this for pdf output -->
   {% unless site.output == "web" %}
   {% include image.html file="baseline-preview.png" %}
   {% endunless %}

8. Click **Create Baseline** to save the Baseline.

   Once created, the new Baseline is added to the list of Baselines.

   {% include image.html file="baseline-list.png" %}
   
9. If required, click **Back** to edit the Baseline on the **Create Baseline** page.


**Refresh Baseline Status**

For a baseline including configuration items with large volume of data, there would be a delay in taking the snapshot of the configuration items. In such cases, a "Click to refresh" link is provided to refresh the status of the baseline being created.

{% include image.html file="refresh-baseline-status.png" caption="Click to refresh the baseline status" %}

**Auto Refresh Baselines List Page**

The baselines list page is automatically refreshed every one minute until the baselines (with the status "Creation In Progress") in a specific project are created. You can continue to use the **Click to refresh** link to manually refresh the baseline(s).

## Create a New Baseline from Baseline Definition {#createbaselinefromBDef}

1. Log on to TeamForge and select a project from **My Workspace**.

2. Click **Baselines** from the **Project Home** menu. 

3. Click **Definitions** from the side navigation menu.

4. Select a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline_definition}}">Baseline Definition</a> from the list to view its details.

   {% include image.html file="view-baseline-def.png" %}

5. Click **Create Baseline** on the **View Baseline Definition** page to create a new Baseline. For more information, see [Create Baselines][create-baseline.html#baselinewithoutBDef].

For a baseline including configuration items with large volume of data, there would be a delay in taking the snapshot of the configuration items. In such cases, a "Click to refresh" link is provided to refresh the status of the baseline being created.

{% include image.html file="refresh-baseline-status.png" caption="Click to refresh the baseline status" %}

The next step is to review Baselines. Select a submitted Baseline to proceed with the baseline review. For more information, see [Review Baselines][baseline-review-approval-workflow].

## Create New Baselines from Approved Baselines {#createbaselinefromappbaselines}

You can now create a new Baseline from an approved Baseline.  

{% include important.html content="Project Baselines cannot be cloned." %}

To create a new Baseline from an approved Baseline, follow these steps:

1. Log on to TeamForge and select a project from **My Workspace**.

2. Click **Baselines** from the **Project Home** menu. 

3. Select an approved Baseline from the list of baselines.

4. Click **Create Baseline**. 

   {% include image.html file="create-baseline-from-appbaseline.png" caption="Create Baseline from Approved Baseline" %}

5. Enter the name and the description for the new Baseline.

   {% include note.html content="All but the name and the description fields are auto-filled with data from the source Baseline that’s being cloned." %}

6. Modify the fields and the filter criteria, if required.

7. Click **Preview to Create**.

8. Click **Create Baseline** on the **Preview Baseline** page.

The new Baseline is created.

## View the Baseline {#viewbaseline}

You can view a Baseline, after it is approved or rejected. In other words, you cannot edit the Baseline (both system-defined and custom fields) after its status changes to **Approved** or **Rejected**.

{% include image.html file="view-approved-baseline.png" %}

<!--artf390774 - TeamForge 19.3-->
### Export Approved Baselines to Excel

{% include baseline/exporttoexcel.html %}  

You can now export the approved Baselines as Excel reports using the "Export to Excel" option on the **View Baseline** page. 

To export a Baseline as an excel report, select the approved Baseline on the baseline list view and click the **Export to Excel** button on the **View Baseline** page.

{% include image.html file="export-appbaseline-to-excel.png" url="http://docs.collab.net/teamforge221/images/export-appbaseline-to-excel.png" caption="\"Export to Excel\" option for approved Baselines" %}

The name of the downloaded excel file has the format "[baseline_id]baseline_name". For instance, if you export the baseline "export_baseline" with the id "base1015", the name of the result excel file reads as "[base1015]export_baseline".

If the baseline name has a special character other than an underscore ("\_") or if the baseline has a space in its name, it will be replaced with an underscore ("\_") in the name of the downloaded excel file. For example, when the baseline "test baseline for export#1" is exported, the downloaded excel file name reads as "[base1033]test_baseline_for_export_1". 

The excel file has worksheets for each component included in the exported Baseline. Each worksheet has as many number of columns as the manifest fields for each component.
<!--artf390774 - TeamForge 19.3-->

## Monitor a Baseline {#monitoritemlevelbaseline}

<a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baselines</a> created by a user is monitored by the user by default. To monitor Baselines created by other users, click the **Start Monitoring** icon {% include inline_image.html file="monitor-button.png" %}. To stop monitoring a Baseline, click the **Stop Monitoring** {% include inline_image.html file="monitored-button.png" %} icon.


{% include links.html %}

