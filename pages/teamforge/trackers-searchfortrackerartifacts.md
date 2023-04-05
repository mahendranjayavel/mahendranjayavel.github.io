---
title: Find Tracker Artifacts
keywords: search, saved search, advanced search
tags: [project_member_tasks, trackers]
sidebar: teamforge_sidebar
permalink: trackers-searchfortrackerartifacts.html
folder: teamforge
last_updated: Jul 16, 2018
summary: If the filter returns too many results or not enough, try the search facility. The Tracker contains a comprehensive search system that enables you to find a specific artifact or set of artifacts quickly.
---

## Search for Tracker Artifacts

You can find tracker artifacts by supplying a keyword, an artifact ID, a date range or some other value. You can also search comments, attachments, and user-defined fields.

1. Click **Trackers** from the **Project Home** menu.
2. Set the scope of your search.
   * To search all the trackers in your project, click **Search Trackers**.
   * To search a specific tracker, click the tracker you want to search, then click **Search Tracker** in that tracker's list view.
3. In the _Tracker Search Criteria_ section, enter the keywords to search for.
   {% include note.html content="Wildcards are allowed." %}
4. Select the elements of the artifact to search. For example, to search for a keyword in the title and description fields, select the **Title** and **Description** check boxes. If you want to search all the text fields (including **Title**, **Description** and user-defined text fields), select the **All Text Fields** check box. 
5. To search for a keyword in the comments field, select **Include Comments**.
   
   When searching the tracker, you can now select one or more planning folders or teams from the respective fields on the **Search Tracker** page.

   {% include image.html file="searchtrackers-multiplePFvalues.png" %}

   {% include image.html file="searchtrackers-multipleteamvalues.png" %}

6. If you know the artifact's ID, enter that.
7. Click the calendar icon to select dates, if appropriate. You can also specify relative dates such as "Within the last 7 days".
8. Use as many of the remaining tracker search criteria as seems useful.
9. Click **Search**.

All tracker artifacts matching your search criteria are displayed.
 
{% include note.html content="If your search included multiple trackers. the icon next to each artifact in your search results can help you identify which tracker that artifact belongs to." %}

## Find your Own Artifacts
To narrow your scope, try searching only for artifacts assigned to or submitted by you.

1. Click **Trackers** from the **Project Home** menu.
2. On the list of project trackers, click the title of a tracker.
3. In the tracker artifact list view, click **Search Tracker**.
4. In the _Tracker Search Criteria_ section, select the **Use running search** options in the **Assigned To** or **Submitted By** fields.
5. Click **Search**.

All tracker artifacts matching your search criteria are displayed.

## Save a Search for Tracker Artifacts

To reuse a search that you devised for tracker artifacts, save the search criteria.

To be able to save your search, you must first select a tracker, and create and run your search.

1. In the _Tracker Search Results_ section, click **Save Search from Results**.
2. In the **Save Search As** page, enter a descriptive name for the search, and click **Save**.

The search appears under **My Saved Tracker Searches**. The name of the search, the tracker for which it was run, the criteria used, and a system-assigned ID are displayed.

## Share a Saved Tracker Search {#savedsearch}

To enable other users to use a search that you have devised, save it as a shared search.

To share your search with other users, you must be a tracker administrator.

1. In the _Tracker Search Results_ section, click **Save Search from Results**.
2. In the **Save Search As** page, enter a descriptive name for the search.
3. Select the **Shared Search** option.

The search appears under **Shared Tracker Searches**. The name of the search, the tracker for which it was run, the criteria used, the user who created the search, and a system-assigned ID are displayed.

## Run a Saved Search

To find artifacts in the current tracker or a different one in the project, run a saved search in the appropriate context.

1. Click **Trackers** from the **Project Home** menu.
2. On the list of project trackers, click the titile of a tracker.
3. In the tracker artifact list view, click **Search Tracker**.
4. Select the **Show My Searches Across Trackers** and **Show Shared Searches Across Trackers** options.
5. Expand the _My Saved Tracker Searches_ and _Shared Tracker Searches_ sections. The saved searches for all trackers in the project are displayed.
6. To run a search for the current tracker, click the **Search** or **Search Here** link below the search name in the required search. All artifacts in the current tracker, that match the search criteria, are displayed.
7. To run a search for a different tracker, click the **Search There** link below the tracker name in the required search. All artifacts that match the search criteria in the selected tracker, are displayed.

## Refine a Saved Search

Refine your saved searches and keep them updated.

To be able to refine (edit) a previously saved search, you must first run the search and click **Refine Search**.

1. Click **Trackers** from the **Project Home** menu.
2. Click **Search Trackers**.
3. Click **My Saved Tracker Searches**.
4. Click the **Search** link under the saved search (in **Saved Search Name** column) you want to refine. The saved search is run and results appear.
5. Click **Refine Search**. The Tracker Search Criteria for the saved search shows up.
6. Modify the search criteria and click **Save Search**. The _Save Search As_ dialog box appears.
7. Type a name and click **Save**. You may save the search with the same name, particularly if your have already shared the search with others. Otherwise, you can save the search with a new name too.

The search is saved with your new search criteria.

## Remove a Saved Search

To remove a saved search for tracker artifacts, delete it from the list of personal or shared searches.

 {% include note.html content="Only tracker administrators can remove a shared search." %}

 1. Click **Trackers** from the **Project Home** menu.
 2. On the list of project trackers, click the title of the tracker in which you want to delete a saved search.
 3. In the tracker artifact list view, click **Search Tracker**.
 4. Expand _My Saved Tracker Searches_ or _Shared Tracker Searches_ so that the available searches are displayed.
 5. Select a search and click **Delete**.
 6. Accept the confirmation message.

 The search is removed from the table where you deleted it.

 {% include links.html %}
