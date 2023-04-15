---
title: Edit Baselines
keywords: Edit baselines
tags: [baseline, ctf_18.3]
sidebar: teamforge_sidebar
last_updated: Sep 23, 2019
permalink: edit-baseline.html
folder: teamforge
summary: You can edit the existing fields in a Baseline as long as the Baseline is in open status. A Baseline cannot be edited after it is approved or rejected.
---

{% include callout.html type="primary" content="**Prerequisite**: You must have **Create/View Baseline** permission to edit Baselines." %}

You can only edit the fields (both the system-defined fields and custom fields) in an <a href="#" data-toggle="tooltip" data-original-title="{{site.data.glossary.baseline}}">Baseline</a>. You cannot edit the filter criteria defined for Trackers, Documents, Source Code Repositories, File Releases, and Binaries (only Nexus binary repositories are supported) in the baseline.

1. Log on to TeamForge and select a project from **My Workspace**.

2. Click **Baselines** from the **Project Home** menu. 

3. Select a Baseline from the list of baselines to view its details.

4. Click the **Edit** icon on the **Review Baseline** page.

   {% include note.html content="As soon as a Baseline is created, it is ready to undergo the baseline review process. Once your Baseline is either approved or rejected during the review, the **View Baseline** page is shown." %} 

   {% include image.html file="edit-baseline-1.png" %}   

5. Modify the fields on the **Edit Baseline** page.

   {% include image.html file="edit-baseline.png" %}

6. Click **Save**.


{% include links.html %}


