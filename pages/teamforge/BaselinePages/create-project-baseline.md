---
title: Create and View Project Baselines
keywords: creating project baseline
tags: [baseline, ctf_18.3, ctf_19.0, ctf_19.3]
sidebar: teamforge_sidebar
last_updated: Feb 11, 2020
permalink: create-project-baseline.html
folder: teamforge
summary: A Project Baseline is a baseline created on a project at a given point in time. Once you have Project Baselines created, you can kick start new projects from Project Baselines and proceed from when and where the Project Baselines were created in the past. Project Baselines are typically created using Project Baseline Definitions, when you release or deliver a product. You can create as many Project Baselines as required.
---

{% capture projectbaselineprereq %}
**Prerequisites:**<br><br>
{% include inline_image.html file="status-success-small.png" %} You must have **Create Project Baseline** permission to create and view a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a>.<br>
{% include inline_image.html file="status-success-small.png" %} <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline_definition}}">Project Baseline Definition</a> is required before a Project Baseline is created.<br>
{% endcapture %}
{% include callout.html type="primary" content=projectbaselineprereq %}

{% capture projectbaseline %}
**Before you begin:**<br><br>
{% include inline_image.html file="status-success-small.png" %} The filter criteria for Trackers, Documents, Source Code Repositories, File Releases, and Binaries are fetched from the Project Baseline Definition.<br>
{% include inline_image.html file="status-success-small.png" %} Except for the filter criteria of Source Code Repositories, you cannot edit the filter criteria for other components such as Trackers, Documents, File Releases, and Binaries, while creating a Project Baseline.<br>
{% endcapture %}
{% include callout.html type="primary" content=projectbaseline %}

## Save a Draft of Project Baselines

You can now save a draft of the Project Baseline that's being created. Use the **Save as Draft** button in the **Create Project Baseline** page to save a draft of the baselines that are being created. 

Once saved, you can edit or delete draft Project Baselines at a later point in time.

{% include image.html file="save-as-draft-button.png" caption="Save as Draft Button" %}

You can view the list of draft baselines by selecting **Draft** from the left navigation menu. The total number of draft baselines is shown next to the **Draft** option within parenthesis `()`.

{% include image.html file="draft-baselines.png" caption="List of Draft Baselines" %}.

## Create a New Project Baseline

To create a new Project Baseline:

1. Log on to TeamForge and select a project from **My Workspace**.
2. Click **Baselines** from the **Project Home** menu.
3. Click the **Baseline Current Project** link on the baseline list view.   
4. Enter values for the required fields in the **Create Project Baseline** page.
   <!-- Use this for web output -->
   {% unless site.output == "pdf" %}
   [![Create Project Baseline](images/create-project-baseline.png)](images/create-project-baseline.png)
   {% endunless %}

   <!-- Use this for pdf output -->
   {% unless site.output == "web" %}
   {% include image.html file="create-project-baseline.png" %}
   {% endunless %}
5. Select one or more <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.external_baselines}}">external baselines</a> from the **External Baselines** drop-down list.

   {% include image.html file="external-baselines.png" %}

   Click the selected External Baseline to view it.

   You can search for the External Baselines that are not listed in the **External Baselines** drop-down list. Only two selected External Baselines can be shown at a time. To see the complete list of selected Baseline Definitions, click **+ More** in the **External Baselines** drop-down list.
6. Click **Preview to Create**.
7. Click **Create Baseline** on the **Preview Project Baseline** page.
   <!-- Use this for web output -->
   {% unless site.output == "pdf" %}
   [![Preview Project Baseline](images/preview-project-baseline.png)](images/preview-project-baseline.png)
   {% endunless %}

   <!-- Use this for pdf output -->
   {% unless site.output == "web" %}
   {% include image.html file="preview-project-baseline.png" %}
   {% endunless %}
8. If required, click **Back** to edit the baseline on the **Create Project Baseline** page.

**Refresh Baseline Status**

For a project baseline including configuration items with large volume of data, there would be a delay in taking the snapshot of the configuration items. In such cases, a "Click to refresh" link is provided to refresh the status of the baseline being created.

{% include image.html file="refresh-baseline-status.png" caption="Click to refresh the baseline status" %}

**Auto Refresh Baselines List Page**

The baselines list page is automatically refreshed every one minute until the baselines (with the status "Creation In Progress") in a specific project are created. You can continue to use the **Click to refresh** link to manually refresh the baseline(s).

**Known Issue**: The Baseline service may go down during the baseline creation or the package generation process, which may obstruct subsequent baseline operations. Restart the Baseline service (`teamforge stop -s teamforge-baseline` and `teamforge start -s teamforge-baseline`) to restore baseline operations.


## View Project Baseline {#viewprojectbaseline}

Once the <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a> is created, it will get added to the list of baselines. To view a Project Baseline, click any baseline with the category **Project Baseline** from the baseline list view.

### Create a Project from View Project Baseline Page {#createprojectfromPB}

You can create a new project in TeamForge from a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a>. 

{% capture createprojectfromviewpblpage %}
{% include inline_image.html file="status-success-small.png" %} Only users with a baseline license can create a project from a Project Baseline. <br>
{% include inline_image.html file="status-success-small.png" %} You can create a project only from an approved Project Baseline.<br>
{% include inline_image.html file="status-success-small.png" %} The same set of associations (related to Trackers, Documents, and File Releases) from the source project will be available in the carry over project created using the Project Baseline, provided that these associations were present when the source project was baselined.
{% endcapture %}
{% include callout.html type="primary" content=createprojectfromviewpblpage %}

To create a project from a Project Baseline:

{% include important.html content="Make sure that you've selected only the Nexus 3 binary repositories when creating the Project Baseline Definition. Projects created via the Project Baseline supports only Nexus 3 binary repositories. Nexus `Maven2` and `Raw` formatted Proxy, Hosted and Group types of repositories are only supported." %}

1. Select an approved Project Baseline from the baselines list view.

2. Click **Create New Project** on the **View Project Baseline** page.

   {% include image.html file="create-project-from-pbl.png" %}

3. You are redirected to the **Create New Project** page. Enter the values for the required fields on this page and click **Create**.

   {% include note.html content="The Project Baseline is prefilled in the **Project Baseline** drop-down list as you've been redirected from the **View Project Baseline** page of the Project Baseline in scope." %}

   {% include image.html file="pbl-in-create-project-page.png" %}

   If the selected project baseline includes the source code repository filter, a check box **Include Source code** is shown below the **Project Baseline** drop-down list.   

   Similarly, the check box **Include Binaries** is shown for project baselines that include the binary repository filter. For project baselines that include both the repository filters, both the **Include Source code** and **Include Binaries** check boxes are shown. Select the required check box to import the repository(s) to the new project.

   {% include image.html file="include_scm_binary_repos.png" caption="\"Include Source code\" and \"Include Binaries\" options" %}

{% include note.html content="From TeamForge 19.0 release, you can also create a project using the Project Baseline from the **Create New Project** page. For more information, see [Create a TeamForge Project][creatingaproject]. If you are a Site Administrator, see [Create and Manage Projects][createanewproject]." %}

#### References to External Baselines in Carry-over Project

When you create a new project from a project baseline that includes one or more external baseline(s), the new project or the carry-over project will have references to these external baselines. The new project created in this way will have a Tracker called **External Baselines**. This Tracker in turn will have artifact(s) created in the name of the external baseline(s) referenced from the Project Baseline of the source project. 

{% include image.html file="external-baseline-in-new-project.png" caption="\"External Baselines\" Tracker with artifacts" %}

The description of the artifact(s) in the **External Baselines** Tracker will include a link (in the format "baseline id:baseline name") to the external baseline.  

{% include image.html file="external-baseline-artifact.png" caption="Artifact in \"External Baselines\" Tracker" %}

Click the external baseline link in the artifact description to view the baseline from within its native project.

{% include image.html file="view-externalbaseline.png" caption="View External Baseline in its native project" %}

**Known Limitations** <br>

<!--artf317952-->
The following issues are found when a new project is created from a Project Baseline:

* IAF permissions added in the source project are not retained in the new (or target) project.

* **Grant Automatically on Request** setting, though configured in the source project, is not retained in the target project.

* As the publishing repository is not copied to the target project, the Source code path-based setting for publishing repository, though configured in the source project, is not retained in the target project.


<!--artf390774 - TeamForge 19.3-->
### Export Approved Project Baselines to Excel

{% include baseline/exporttoexcel.html %}  

You can now export the approved Project Baselines as excel reports using the "Export to Excel" option on the **View Baseline** page. 

To export a Project Baseline as an excel report, select the approved Project Baseline on the baseline list view and click the **Export to Excel** button on the **View Project Baseline** page.

{% include image.html file="export-appprojbaseline-to-excel.png" url="http://docs.collab.net/teamforge221/images/export-appprojbaseline-to-excel.png" caption="\"Export to Excel\" option for approved Project Baselines" %}

The name of the downloaded excel file has the format "[baseline_id]baseline_name". For instance, if you export the baseline "export_baseline" with the id "base1015", the name of the result excel file reads as "[base1015]export_baseline".

If the baseline name has a special character other than an underscore ("\_") or if the baseline has a space in its name, it will be replaced with an underscore ("\_") in the name of the downloaded excel file. For example, when the baseline "test baseline for export#1" is exported, the downloaded excel file name reads as "[base1033]test_baseline_for_export_1". 

The excel file has worksheets for each component included in the exported Project Baseline. Each worksheet has as many number of columns as the manifest fields for each component.
<!--artf390774 - TeamForge 19.3-->


## Monitor Project Baseline {#monitorprojectbaseline}

By default, you can start monitoring the <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.project_baseline}}">Project Baseline</a> as soon as you create it. If you are not already monitoring a Project Baseline (which you have not created), click the **Start Monitoring** icon ( {% include inline_image.html file="monitor-button.png" %}) to start monitoring the Project Baseline. To stop monitoring a Project Baseline, click the **Stop Monitoring** ( {% include inline_image.html file="monitored-button.png" %}) icon.


{% include links.html %}



<!--To view a baseline after it is created, click the baseline with the status **Approved** or **Rejected**.

{% include image.html file="view-baseline-1.png" %}-->.


<!--## Create a Project Baseline

A **Project Baseline** is typically a set of all item level baselines that are defined based on select categories. When you create a project baseline, a snapshot of all items comprised of the PBDef and the constituent BDefs is stored. 

To create a project baseline:

1. Log on to TeamForge and select a desired project.
2. Click **Baseline** from the **Project Home** menu to get to the baseline list view.
   {% include image.html file="baseline-list.png" %}
3. Click **Baseline Current Project** to create a project baseline.-->



<!--   * **Tracker Artifacts**

     1. Select the tracker type(s) from the **Tracker Type** drop-down list. These are the tracker types available in the project.
        {% include image.html file="baseline-tracker-type.png" %}

     2. Click **Add Filter(s)** and select the tracker type to set the required filters. The tracker type(s) that you have selected at step 1 are listed here.
        {% include image.html file="tracker-type-add-filter.png" %}       
        * _Attribute_ - Lists all the available attributes for the selected tracker type(s).
        * _Condition_ - Lists the conditions for the selected attribute type. 
        * _Value_ - Lists the values specific to the selected attribute type.
        
        Here's an example of how it appears after the filters are set. If you create the baseline at this point, it would create the baseline with completed user stories for the selected trackers.
         {% include image.html file="tracker-type-add-filter-2.png" %}

     3. Click **Add "AND" Condition** to concatenate more conditions to the filter criteria.
        {% include image.html file="baseline-tracker-type-add-condition.png" %}

     4. Repeat steps 2 and 3 until you've added the required filter criteria for Trackers.

     5. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.

     6. Select the planning folder. It is good enough that you select the parent/root planning folder to show all its child/sub folders. In this example, you can see all the sub folders of the root planning folder "Product 1".
        {% include image.html file="baseline-planning-folder-filter.png" %}

   If you want to see the list of artifacts in the tracker(s) selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **TRACKER/PLANNING FOLDER** section.

   You can narrow down the list by selecting the desired tracker and/or doing a keyword search in the preview pane.

   {% include image.html file="baseline-tracker-artifacts-preview.png" %}

   You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.

   
   * **Documents**

     1. Select the document folder path.

     2. Select the document version.

     3. Click **Add Filter(s)** to include the filter criteria.
        * _Attribute_ - Lists all the available attributes for documents.
        * _Condition_ - Lists the conditions for the selected attribute type. 
        * _Value_ - Lists the values specific to the selected attribute type.

     4. Click **Add "AND" Condition** to concatenate more conditions to the filter criteria.

     5. Repeat steps 3 and 4 until you've added the required filter criteria for Documents.
     
     6. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.

   If you want to see the list of documents in the document folder selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **DOCUMENTS** section.

   You can narrow down the list by selecting the desired document folder from its path in the preview pane.

   {% include image.html file="baseline-documents-preview.png" %}    

   You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.

   * **Source Code Management**

     1. Select the repository from the **Repo/Source Name** drop-down list. The repositories are grouped under the repository type which is either "Git" or "Subversion".

     2. Click **Add another Repo** to add more repository related filter criteria.

     3. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.


   * **File Release**

     Select the package or the release name from the **Package/Release Name** drop-down list.

     If you want to see the list of files in the releases selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **FILE RELEASE** section.

     You can narrow down the list by selecting the desired release in the preview pane.

     {% include image.html file="baseline-filerelease-preview.png" %}

     You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.


   * **Binaries**

     Select the server name or repository name from the **Server/Repository Name** drop-down list.-->

<!---->

<!--* **Tracker Artifacts**

     1. Select the tracker type(s) from the **Tracker Type** drop-down list. These are the tracker types available in the project.
        {% include image.html file="baseline-tracker-type.png" %}

     2. Click **Add Filter(s)** and select the tracker type to set the required filters. The tracker type(s) that you have selected at step 1 are listed here.
        {% include image.html file="tracker-type-add-filter.png" %}       
        * _Attribute_ - Lists all the available attributes for the selected tracker type(s).
        * _Condition_ - Lists the conditions for the selected attribute type. 
        * _Value_ - Lists the values specific to the selected attribute type.
        
        Here's an example of how it appears after the filters are set. If you create the baseline at this point, it would create the baseline with completed user stories for the selected trackers.
         {% include image.html file="tracker-type-add-filter-2.png" %}

     3. Click **Add "AND" Condition** to concatenate more conditions to the filter criteria.
        {% include image.html file="baseline-tracker-type-add-condition.png" %}

     4. Repeat steps 2 and 3 until you've added the required filter criteria for Trackers.

     5. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.

     6. Select the planning folder. It is good enough that you select the parent/root planning folder to show all its child/sub folders. In this example, you can see all the sub folders of the root planning folder "Product 1".
        {% include image.html file="baseline-planning-folder-filter.png" %}

   If you want to see the list of artifacts in the tracker(s) selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **TRACKER/PLANNING FOLDER** section.

   You can narrow down the list by selecting the desired tracker and/or doing a keyword search in the preview pane.

   {% include image.html file="baseline-tracker-artifacts-preview.png" %}

   You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.

   
   * **Documents**

     1. Select the document folder path.

     2. Select the document version.

     3. Click **Add Filter(s)** to include the filter criteria.
        * _Attribute_ - Lists all the available attributes for documents.
        * _Condition_ - Lists the conditions for the selected attribute type. 
        * _Value_ - Lists the values specific to the selected attribute type.

     4. Click **Add "AND" Condition** to concatenate more conditions to the filter criteria.

     5. Repeat steps 3 and 4 until you've added the required filter criteria for Documents.
     
     6. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.

   If you want to see the list of documents in the document folder selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **DOCUMENTS** section.

   You can narrow down the list by selecting the desired document folder from its path in the preview pane.

   {% include image.html file="baseline-documents-preview.png" %}    

   You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.

   * **Source Code Management**

     1. Select the repository from the **Repo/Source Name** drop-down list. The repositories are grouped under the repository type which is either "Git" or "Subversion".

     2. Click **Add another Repo** to add more repository related filter criteria.

     3. Click the delete button ( {% include inline_image.html file="baseline-delete.png" %}) against the filter criteria that you want to delete.


   * **File Release**

     Select the package or the release name from the **Package/Release Name** drop-down list.

     If you want to see the list of files in the releases selected, click the view link ( {% include inline_image.html file="view-link.png" %}) in the **FILE RELEASE** section.

     You can narrow down the list by selecting the desired release in the preview pane.

     {% include image.html file="baseline-filerelease-preview.png" %}

     You can also do a keyword search by using the search ( {% include inline_image.html file="search-baseline-button.png" %}) on the preview pane.


   * **Binaries**

     Select the server name or repository name from the **Server/Repository Name** drop-down list.-->

<!--{% include note.html content="You can view the actual TeamForge objects (configuration items in terms of Baseline) from within TeamForge by clicking the respective links on the View Baseline page. However, TeamForge doesn’t show the objects, if you don’t have view permission." %}-->