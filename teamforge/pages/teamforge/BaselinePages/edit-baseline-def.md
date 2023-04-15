---
title: Edit Baseline Definitions
keywords: Edit baseline definition
tags: [baseline, ctf_18.3]
sidebar: teamforge_sidebar
last_updated: Feb 5, 2019
permalink: edit-baseline-def.html
folder: teamforge
summary: You can edit an existing Baseline Definition to add more filter criteria or modify the existing fields and filter criteria. 
---

{% include callout.html type="primary" content="**Prerequisite**: You must have **Create/View Baseline** permission to edit Baseline Definitions." %}


1. Log on to TeamForge and select a project from **My Workspace**.

2. Click **Baselines** from the **Project Home** menu. 

3. Click **Definitions** from the side navigation menu.

4. Select a <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline_definition}}">Baseline Definition</a> from the list of baseline definitions to view its details.

   {% include image.html file="view-baseline-def.png" %}

5. Click the **Edit** button on the **View Baseline Definition** page.

6. Modify the required fields and the filter criteria on the **Edit Baseline Definition** page.

   {% include image.html file="edit-baseline-def.png" %}

4. Click **Save**.



{% include links.html %}

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

     Select the server name or repository name from the **Server/Repository Name** drop-down list.

7. Click **Preview to Create** to see the preview of the baseline content. 

   {% include image.html file="baseline-preview.png" %}
   {% include note.html content="You can view the actual TeamForge objects (configuration items in terms of Baseline) from within TeamForge by clicking the respective links on the View Baseline page. However, TeamForge doesn’t show the objects, if you don’t have view permission." %}

8. Click **Save as Definition** to save the configuration as a baseline definition.

9. Click **Back** to get back to the **Create Baseline** page to edit the configuration.-->



<!---->

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

     Select the server name or repository name from the **Server/Repository Name** drop-down list.

6. Click **Preview to Create** to see the preview of the baseline content. 

   {% include image.html file="baseline-preview.png" %}
   {% include note.html content="You can view the actual TeamForge objects (configuration items in terms of Baseline) from within TeamForge by clicking the respective links on the View Baseline page. However, TeamForge doesn’t show the objects, if you don’t have view permission." %}

7. Click **Save as Definition** to save the configuration as a baseline definition.

8. Click **Back** to get back to the **Create Baseline** page to edit the configuration.




6. Click **Preview to Create** to see the preview of the baseline content. 

   {% include image.html file="baseline-preview.png" %}
   {% include note.html content="You can view the actual TeamForge objects (configuration items in terms of Baseline) from within TeamForge by clicking the respective links on the View Baseline page. However, TeamForge doesn’t show the objects, if you don’t have view permission." %}

7. Click **Save as Definition** to save the configuration as a baseline definition.

8. Click **Back** to get back to the **Create Baseline** page to edit the configuration.-->


<!--<div class="well well-lg">
<b>Baseline Definition</b> (<b>BDef</b>) specifies the selection criteria for the qualified configuration items in TeamForge that should accelerate baseline creation. Baseline Definition can be edited any time, if required.
</div>-->


<!--{% include note.html content="You can view the actual TeamForge objects (configuration items in terms of Baseline) from within TeamForge by clicking the respective links on the View Baseline page. However, TeamForge doesn’t show the objects, if you don’t have view permission." %}-->
