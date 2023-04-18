---
title: Export Tracker Artifacts
keywords: exporting tracker artifacts, how to export tracker artifacts
tags: [ctf_20.3, project_member_tasks, trackers, tracker_artifacts]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Oct 7, 2020
permalink: trackers-exportingtrackerartifacts.html
summary: To use the contents of artifacts from a tracker or a planning folder in other applications, export them to a CSV, XML, Excel or tab-delimited file.
---

Sometimes, it can be useful to look at the status of a project by sharing a spreadsheet using Microsoft Excel or Google Spreadsheets.

{% include tip.html content="You can also export tracker artifacts from a tracker report or a set of search results." %}

1. Click **Trackers** from the **Project Home** menu.
2. Click a tracker or planning folder. 

   In a tracker:
   * You can export a subset of the artifacts in the list view by setting up a filter. See [Tracker List Artifacts View](trackers-filteringtrackerartifacts.html#trackerartifacts).
   * You can select specific artifacts and export only those checked items.
   The current sort order in the list view is retained in the exported list of artifacts as well.
3. Click **Export**.
4. In the **Export Data** window, select an export format that you can import into the other application. For example, to use the data in a spreadsheet program, select `CSV`	or `Excel`.
   {% include image.html file="203-exporttags-01.png" caption="The Export Data dialog" %}
5. Move the fields you are interested in from the **AVAILABLE COLUMNS** list to the **SELECTED COLUMNS** list, then click **Export**.
   
   {% include note.html content="When you export tracker artifacts directly from a tracker, you can choose from all the fields in the tracker. When you export from a planning folder, only the standard fields provided by TeamForge can be exported. For more information on what you can do with different kinds of fields, see [What fields can I use in a tracker?][trackers-faqs.html#trackerfields]" %}

   * Export Associations in Trackers—you can export artifact associations from the following pages:
     * Tracker list view
     * Planning Folder list view
     * Tracker table report   

1. Artifacts are exported and the file is downloaded automatically.
   {% include tip.html content="Starting from TeamForge 16.10, while exporting tracker artifacts, artifacts are exported to one of the file formats such as Excel, CSV, Tab-delimited or XML (as selected by the user) and the file is downloaded automatically. To improve performance, the file download link, which you would have used in the past, is no longer available." %}

{% include links.html %}







