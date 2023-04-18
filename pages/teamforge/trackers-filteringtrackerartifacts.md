---
title: Filter Tracker Artifacts
keywords: filter, sort, list artifacts
tags: [project_member_tasks, trackers, search_filter_sort, tracker_artifacts]
sidebar: teamforge_sidebar
permalink: trackers-filteringtrackerartifacts.html
folder: teamforge
last_updated: Feb 3, 2021
summary: When a large number of tracker artifacts makes it difficult to find the one you want, filter and sort the list to narrow down the possibilities.
---

## Configure Tracker Columns

When you're looking at the artifacts list in a tracker, a planning folder or a team, you can select the columns you want to see, either for this session or permanently.

You set your column preferences for each tracker, planning folder or team independently. If your project administrator has set default columns for the entire project, your individual column choices override those settings.

1. Click **Trackers** from the **Project Home** menu.
2. Select a tracker, planning folder or team and click **COLUMNS > Configure**.
   * If you've already saved a column configuration, click it and skip the rest of these steps.
   * To go back to the default column configuration, click **System (default)** and skip the rest of these steps.
   * To set up a new configuration, click **Configure**.
3. Choose your columns.
   1. Move the columns you want from **Available Columns** to **Selected Columns**. **Artifact ID: Title, Priority** and **Status** are required columns.
      {% include note.html content="Selecting more columns can increase the time required to load the listing page." %} 
   2. Remove any columns you don't need from **Selected Columns**.
   3. Use the move up and move down arrows to change the display order of the columns.
4. Apply your choices to your view of the tracker.
   * To use this arrangement this time only, click **Apply**. The next time you log in, you'll start with the default view again.
   * To save your column layout for repeated use, click **Apply and Save**, then give your arrangement a name. The next time you log in, you'll see the column arrangement you just selected. (If you've sorted the records in your view that sort order is saved too.)
     {% include tip.html content="If you are editing a column configuration that already exists, you can rename it by saving it under a new name." %}
5. To make the same set of columns appear every time you come to this tracker, planning foler or team, click **COLUMNS > Save** and from **Save Column Configuration** page, select **Make this my default view**.

## Tracker List Artifacts View {#trackerartifacts}

1. Click **Trackers** from the **Project Home** menu.
2. On the **Tracker Summary** page, click the title of the tracker in which you want to look at artifacts.
3. Specify the filter criteria in one or more filter fields (at the top of each column) and clic **FILTER**.
   * You can find a filter field at the top of each column in most of the tables in the TeamForge application.
   * The filter field could be a text box or a drop-down list with multi-select check boxes.
     {% include image.html file="filtertables02.png" %}
   * You can type your filter criteria in the text boxes. The search text is case-insensitive.
   * You can also select the filter values from on e or more drop-down lists. By default, you can only select up to 10 filter values in a drop-down list. However, you can set a value that suits your requirement for the `FILTER_DROPDOWN_MAX_SELECTION` token in the `site-options.conf` file to increase or decrease the count.
   * **Filter-as-you-type**: You can find the **Enter keywords** text box in all filter drop-down lists. As you type your filter keyword, instant search results are shown in the drop-down list. For example, in the following illustration, typing "R" instanstly shows all statuses having the alphabet "R". The search text is case-insensitive.
     {% include image.html file="filtertables01.png" %}
   * Some search filters may not appear if your site administrator has not enabled them.
4. After filtering, if you want to save a filter for future use:
   1. Click **FILTER** and select **Save** from the drop-down list. The **Save Filter As** window appears.
   2. Type a name for the filter in the **FILTER NAME** text box.
   3. Click **Save**. The filter is saved. You can view and select the saved filters at a later point in time by clicking the **Filter** drop-down list.
      {% include note.html content="You can save filters only in specific contexts. This feature may not be available in all the tables where you can filter table list items." %}
5. To delete save filters:
   1. Click **FILTER** and select **Delete** from the drop-down list. The **Select Filters To Be Deleted** window appears.
   2. Select one or more filters to delete.
      {% include tip.html content="Press and hold the **Ctrl** key to select more than one filter." %}    
   3. Click **Delete**. A message such as `2 tracker filter(s) have been deleted successfully.` is displayed if the process was successful.
6. After filtering, if you want to clear the filters, click **FILTER** and select **Clear** from the drop-down list.
7. Use the up-down arrow at the top of any column to sort your list by that column.
   * Your primary sort column is identified by a superscript **1** next to the up-down arrow, and your secondary and third-level sort columns, if any, are likewise marked.
   * Click the up-down arrow again to reverse the sort order.
   * You cannot sort the list by the following fields (columns)—`Reported in Release`, `Fixed in Release`, `Tags`, multi-select flex fields and user flex fields. 

## Planning Folder List Artifacts View

{% capture pflistartifacts %}
      {% include inline_image.html file="status-success-small.png" %} In the Planning Folder list view, you can filter only by **Priority**, **Artifact ID**, **Title**, **Assigned To** and **Team** columns.<br>
      {% include inline_image.html file="status-success-small.png" %} Though the artifacts are listed in a tree view (parent artifact with its child artifacts), the filter is applicable only for the parent artifacts and not their children. <br>
      {% include inline_image.html file="status-success-small.png" %} The filter is available only in the Sort mode and not in the Rank mode.<br>
      {% include inline_image.html file="status-success-small.png" %} The filter that you set is retained even after you navigate to other pages and return to this page.
{% endcapture %}
{% include callout.html type="primary" content=pflistartifacts %}

1. Click **Trackers** from the **Project Home** menu.
2. Click **Planning Folders**.
3. On the Summary page, click the planning folder in which you want to look at artifacts.
4. Specify the filter criteria in one or more filter fields (at the top of the filterable columns) and click **FILTER**.
   * The filter field could be a text box or a drop-down list with multi-select check boxes.
   * You can type your filter criteria in the text boxes. The search text is case-insensitive.
   * You can also select the filter values from on e or more drop-down lists. By default, you can only select up to 10 filter values in a drop-down list. However, you can set a value that suits your requirement for the `FILTER_DROPDOWN_MAX_SELECTION` token in the `site-options.conf` file to increase or decrease the count.
   * **Filter-as-you-type**: You can find the **Enter keywords** text box in all filter drop-down lists. As you type your filter keyword, instant search results are shown in the drop-down list. For example, in the following illustration, typing "R" instanstly shows all statuses having the alphabet "R". The search text is case-insensitive.
5. After filtering, if you want to clear the filters, click **FILTER** and select **Clear** from the drop-down list.
6. Use the up-down arrow at the top of any column to sort your list by that column.
   * Your primary sort column is identified by a superscript **1** next to the up-down arrow, and your secondary and third-level sort columns, if any, are likewise marked.
   * Click the up-down arrow again to reverse the sort order.
   * You cannot sort the list by the following fields (columns)—`Reported in Release`, `Fixed in Release`, `Tags`, multi-select flex fields and user flex fields. 


     **Filter by artifact status**
   
     In addition to the column-wise filter, you can also filter and view artifacts based on their status alone using the status drop-down list.
       {% include image.html file="17-4-filtertables04.png" %}
7. Select **All**, **Open only** or **Closed** from the drop-down list and all the relevant artifacts (including child artifacts) are displayed. For example, select **Open only** and all the artifacts with associated status values such as 'Under Construction', 'Open' and 'In Progress' are displayed.
   {% include note.html content="The statuses **All**, **Open only** and **Closed** are associated with user-defined status values while configuring a tracker field on the **Edit Tracker Field** page (**Project Admin > Tracker Settings**). For more information, see [Configure Tracker **Select** Field Values][trackers-creatingatracker.html#configuretrackerfieldvalues]." %}

## Teams List Artifacts View

* In the Teams list view, you can filter only by **Priority**, **Artifact ID**, **Assigned To** and **Planned For** columns.
* The filter that you set is retained even after you navigate to other pages and return to this page.
  {% include note.html content="The Sort and Rank modes are not available on the Teams list view." %}

**Filter by columns**

1. Click **Trackers** from the **Project Home** menu.
2. Click **Teams**.
3. On the Summary page, click the planning folder in which you want to look at artifacts.
4. Specify the filter criteria in one or more filter fields (at the top of the filterable columns) and click **FILTER**.
   * The filter field could be a text box or a drop-down list with multi-select check boxes.
   * You can type your filter criteria in the text boxes. The search text is case-insensitive.
   * You can also select the filter values from on e or more drop-down lists. By default, you can only select up to 10 filter values in a drop-down list. However, you can set a value that suits your requirement for the `FILTER_DROPDOWN_MAX_SELECTION` token in the `site-options.conf` file to increase or decrease the count.
   * **Filter-as-you-type**: You can find the **Enter keywords** text box in all filter drop-down lists. As you type your filter keyword, instant search results are shown in the drop-down list. For example, in the following illustration, typing "R" instanstly shows all statuses having the alphabet "R". The search text is case-insensitive.
5. After filtering, if you want to clear the filters, click **FILTER** and select **Clear** from the drop-down list.
6. Use the up-down arrow at the top of any column to sort your list by that column.
   * Your primary sort column is identified by a superscript **1** next to the up-down arrow, and your secondary and third-level sort columns, if any, are likewise marked.
   * Click the up-down arrow again to reverse the sort order.
   * You cannot sort the list by the following fields (columns)—`Reported in Release`, `Fixed in Release`, `Tags`, multi-select flex fields and user flex fields. 



   **Filter by artifact status**

   In addition to the column-wise filter, you can also filter and view artifacts based on their status alone using the status drop-down list.
   {% include image.html file="17-4-filtertables_team.png" %}
7. Select **All**, **Open only** or **Closed** from the drop-down list and all the relevant artifacts (including child 
   artifacts) are displayed. For example, select **
    only** and all the artifacts with associated status values such as 'Under Construction', 'Open' and 'In Progress' are displayed.
   {% include note.html content="The statuses **All**, **Open only** and **Closed** are associated with user-defined status values while configuring a tracker field on the **Edit Tracker Field** page (**Project Admin > Tracker Settings**). For more information, see [Configure Tracker **Select** Field Values][trackers-creatingatracker.html#configuretrackerfieldvalues]." %}    

   {% include links.html %}
