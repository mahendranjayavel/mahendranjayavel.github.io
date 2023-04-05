---
title: Clone a Tracker Artifact
keywords: clone tracker artifacts
tags: [project_member_tasks, trackers]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Sep 20, 2017
permalink: trackers-cloneanartifact.html
summary: Save effort in duplicating a tracker artifact within the project and across projects by cloning artifacts in TeamForge.
---
You can now clone an artifact from one tracker to another within the project or across projects. For system defined mandatory fields, artifact data are copied from the source tracker to the target tracker as long as the fields are available on both the source and target trackers. Values for any conflicting fields are set to "None" otherwise.

1. Click **My Workspace** and select a project.
2. Select **Project Home** > **Trackers** and select the tracker that contains the artifact to be cloned.
3. Open the tracker you want to clone. The **View Artifact** page appears.
4. Click **Clone** ( {% include inline_image.html file="clone-artifact.png" %}).
   {% include image.html file="17-11-clonesourceartifact.png" %}
   
   The **Clone Artifact** dialog box appears.
5. Select the **Associate With Source Artifact** check box (selected by default) to create an association with the source artifact.
6. Select the **Include Attachments** check box to include attachments from the source artifact.
7. Select the **Create as child** check box to make the artifact being cloned as the child of the source or the original artifact from which it is being cloned.
8. Click **Select Tracker** drop-down list and select the target tracker.
You can either select a tracker from within the project in context or search and select a tracker from a different project. Use the **Search Projects** text box to find the project that has the target tracker and select the tracker. 

   **Selecting a project from within the same project**  
    {% include image.html file="1610_cloneartifact_01.png" %}

   **Selecting a cross project tracker where you want to clone the artifact** 
    {% include image.html file="1610_cloneartifact_02.png" %}

9. Click **Clone**. The **View Artifact** page appears. For system defined mandatory fields, artifact data are copied from the source tracker to the target trackers as long as the fields are available on both the source and target trackers. Values for any conflicting fields are set to "None" otherwise.
10. Update the fields, if required, and click **Save** or **Save and Close**. The artifact is cloned and saved in the target tracker.

{% include links.html %}