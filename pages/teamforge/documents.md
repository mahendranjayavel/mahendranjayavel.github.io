---
title: Work with Your Documents
keywords: documents
tags: [ctf_22.0, project_member_tasks, documents, associations]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Apr 04, 2022
permalink: documents.html
summary: The Documents List page brings you document management functions to ensure a better document management experience.
---
<!-- Artifact artf394814 : Document v2.0 - Support for customers using Oracle DB -->
<!-- {% include important.html content="The new Documents List page is not tested with the Oracle database. Qualifying the new Documents List page on Oracle is planned for TeamForge 20.1 or later." %} -->

Here's a list of noteworthy features to the Documents List page.

## The Left Navigation Pane {#leftnav}

A new left navigation pane lets you quickly access your documents. The left navigation pane consists of the following menus.

* **All Folders**—A drop-down menu that shows the document folder tree. Clicking the **ALL Folders** menu, by default, lists the documents in the Root Folder. However, you can select any other folder from the drop-down menu to view the documents of that specific folder. The folder you last selected is persisted throughout the session to let you start from the same folder when you later visit the Documents List page.
* **Recent**—Lists the recently viewed/added documents.
* **Favorites**—Lists the favorite documents and document folders.
  {% include image.html file="documents-redesigned-menu.png" caption="Refurbished Documents Home Page Menu" %}
* **Tags**—A Tag Cloud, which is a group of tags added to the left navigation pane of the Documents List page. You can filter documents by tags.

## Concatenation of the Document Name and ID {#concatnameid}

Document name and ID are concatenated to better identify documents in the new Documents List page. The **Name** column shows the concatenated document name and ID. While document IDs are linkified, document names are plain text.

{% include image.html file="documents-name-id-separate.png" caption="Existing List View: Document Name and Document ID in separate columns" %}

{% include image.html file="documents-name-id-single.png" caption="Redesigned List View: Document Name and Document ID (link) shown under the \"Name\" column" %}

## Action Buttons Replaced by Action Icons {#actionicons}

The action buttons for performing operations such as monitoring, moving, and copying documents are replaced by action icons in the enhanced Documents List page. 

The **bell** icon represents the monitoring feature and the **more (...)** icon lists additional actions such as **New Folder**, **Rename**, **Move/Copy**, **Download**, and **Monitoring Users**. 

{% include image.html file="documents-action-icons.png" caption="Action Icons" %}

## Documents List Page Shows Both Folders and Files {#documentfoldersinlistpage}

Unlike the old Documents List page that shows only documents when you select a folder, the new Documents List page lists both folders and files (documents) when you select a folder from the left navigation pane.

{% include image.html file="documents-existing-list-page.png" caption="Old Documents List page showing just a list of documents" %}

{% include image.html file="documents-new-list-page.png" caption="The new Documents List page showing both document folders and documents" %}

## Create New Documents and Document Folders {#newbutton}

1. Browse and select a folder from the left pane where you want to have a new document or document folder created. 
2. Click **New** and select **Create Document** or **Create Folder** for creating a new document or a new folder respectively.
   
   {% include image.html file="202-newdocbutton.png" caption="Create new document/folder drop-down menu" %}

3. If you are creating a new folder, type a name for the folder and click **Save**. To create a new document, see [Create a Document][documents.html#createdoc].

## Monitor and Unmonitor Document Folders and Documents {#monitorunmonitordocsfolders}

To monitor a document folder that you want, select the document folder from the left navigation pane and click the monitor icon (the grey bell icon {% include inline_image.html file="monitor-button.png" %}) from the list view.

The bell icon's color toggles between blue and grey when a folder is monitored and unmonitored respectively.
To unmonitor this document folder, click the monitor icon (the blue bell icon {% include inline_image.html file="monitored-button.png" %}).

{% include image.html file="unmonitored-document-folder.png" caption="Unmonitored document folder with grey bell icon" %}

{% include image.html file="monitored-document-folder.png" caption="Monitored document folder with blue bell icon" %}

In general, to monitor or unmonitor a document folder or document, select the required folder or the document from the list and click the monitor bell icon.

{% include note.html content="The monitor bell icon can be found with individual document folders and files so that you can choose to monitor or unmonitor document folders and files contextually." %}

{% include image.html file="unmonitored-folder-document.png" caption="In-context monitor icons for the individual document folders and documents" %} 

## Add a New Subfolder to a Document Folder {#moreactionsondocsfolders}

To add a new subfolder to a document folder:

1. Select a document folder from the **All Files** left navigation menu or from the list view.
2. Click the more icon ({% include inline_image.html file="documentslist-more-button.png" %}).
3. Select the **New Folder** option.
   {% include image.html file="documents-add-new-folder.png" caption="\"New Folder\" option" %}
4. Type a folder name and click **Save**.
   {% include image.html file="documents-newfolder-name.png" caption="New subfolder name" %}
   The new subfolder gets created and added to the list successfully.
   {% include image.html file="documents-newsubfolder.png" caption="Create new document folder" %}

## Rename Document Folders and Documents

To rename a document folder or a document:

1. Select the folder or document.
2. Click the more icon ({% include inline_image.html file="documentslist-more-button.png" %}).
3. Select **Rename**.
   {% include image.html file="rename-docs-folders.png" caption="The Rename menu" %}
4. Type a new name and click **Save** or press **Enter**.
   {% include image.html file="rename-doc-folder.png" caption="Renaming a document folder" %}
   {% include note.html content="You can rename a document either using the \"Rename\" option or by editing the document." %}
   {% include image.html file="document-renamed.png" caption="Renaming a document" %}

<!--artf392017 -->
## Move or Copy Documents and Document Folders {#movecopy}

While you can can move or copy documents to folders both within and across projects, you cannot move document folders from one project to another.

### Move or Copy a Single Document

To move or copy a single document:

1. Click the more icon ({% include inline_image.html file="documentslist-more-button.png" %}) of the document that you want to move.
2. Select **Move/Copy** from the menu.
   {% include image.html file="move-copy-documents.png" caption="\Move/Copy\ the selected document" %}
   
   The **Move/Copy** dialog box appears. By default, the **Move/Copy** dialog box has the current project and Root Folder selected. 
3. Select the project where you want the document copied or moved to from the drop-down list.
   {% include image.html file="documents-select-project.png" %}
   {% include image.html file="document-destination-project.png" caption="Select the target project" %}     
4. Select the folder where you want the document copied or moved to. You can also create new document folders if you want. Click **New Folder** and create a new document folder.
   {% include image.html file="documents-target-project-docfolder.png" caption="Select the document folder" %}
5. Click **Move** or **Copy** to move and copy the selected document respectively.

### Move or Copy Multiple Documents

To Move/Copy multiple documents at once:

1. Select the list of documents you want to move or copy from the list view. 
2. Select **Move/Copy** from the top-level menu.
   The **Move/Copy** dialog box appears.
3. Repeat steps 3, 4 and 5 to move or copy the selected documents. 

### Move a Single Document Folder

To move a single document folder to another document folder in the same project: 

1. Select the document folder from the Documents List page.
2. Select **Move/Copy** from the more icon ({% include inline_image.html file="documentslist-more-button.png" %}) of the document folder.
   The **Move** dialog box appears. By default, the Root Folder is selected. 
3. Select a folder from the tree view where you want to move the selected document. 
   {% include note.html content="To create a new folder, click the **New Folder** link." %}
   {% include image.html file="move-doc-folder.png" caption="Select the destination document folder" %}
4. Click **Move**.

### Move Multiple Document Folders

To move multiple document folders to another document folder in same project: 

1. Select the document folders from the list view and select **Move/Copy** from the more icon ({% include inline_image.html file="documentslist-more-button.png" %}) at the top of the Documents List page. 
2. Repeat steps 3 and 4 to have the selected folders moved. 

## Download Documents and Document Folders

To download the top-level document folder, any subfolders, and documents on the Documents List page, click the more icon ({% include inline_image.html file="documentslist-more-button.png" %}) of the document folder or document and select **Download** from the menu.

{% include image.html file="download-docs-folders.png" caption="\"Download\" a top-level folder" %}

The document folders are downloaded as TAR files. Spaces, if any, in the document folder name, are encoded with an underscore. For example, a document folder named `teamforge release 19.3`, when downloaded, becomes "teamforge_release_19.3".

When a document is downloaded, only the active version of the document is downloaded. The downloaded file name is in the format "\<document_id\>-\<active document version\>". For instance, for a document with the id "doc1796" and with two versions "Version 1" and "Version 2", of which "Version 1" is the active version, then the name of the downloaded document reads "doc1796-Version1".

You can download multiple documents and folders or both. In this case, the downloaded TAR file name reads as TeamForge[\"<UUID>\"] where `UUID` is the unique id.

To download multiple documents, multiple document folders, or a combination of both document folders and documents:

1. Select the required documents and/or document folders.

2. Click the more icon {% include inline_image.html file="documentslist-more-button.png" %} at the top of the Documents List page.

3. Click **Download**.

<!--artf392494-->
You can restrict downloads by both the file size and number. For more information, see the documentation for these `site-options.conf` tokens:

* [MAX_DOCUMENTS_DOWNLOAD_SIZE][siteoptiontokens.html#MAX_DOCUMENTS_DOWNLOAD_SIZE]
* [MAX_DOCUMENTS_DOWNLOAD_LIMIT][siteoptiontokens.html#MAX_DOCUMENTS_DOWNLOAD_LIMIT]

You can also track your downloads with the download progress indicator.

{% include image.html file="documents-download-inprogress.png" caption="Download Progress Indicator" %}

## Users Monitoring Document Folders and Documents

You can view the list of users monitoring a document folder or a document from the redesigned documents list page. While viewing the monitoring users, you can more users to the monitoring users list as well.

To view the list of users monitoring a document:

1. Go to **Project Home > Documents** page.

2. Click the **The New Documents** toggle button to go to the redesigned Documents List page.

3. Click the more icon ({% include inline_image.html file="documentslist-more-button.png" %}) against the required document folder or document.

4. Select the **Monitoring users** option.

   {% include note.html content="If you want to monitor the top-level or the root folder, use the more (...) icon next to the bell icon on top of the documents list page" %}

   {% include image.html file="documents-monitoring-user-icon.png" caption="\"Monitoring users\" option" %}

   {% include image.html file="documents-monitoring-users-list.png" caption="List of users monitoring the selected document or document folder" %}

5. Click **Add User** to add more users to the list.

6. Click the close button on the **Monitoring users** dialog.

The users now monitor the document or document folder.

If you're a site administrator or a document administrator, you can delete a user from the monitoring users list.

Click the delete icon against the user name that you want to delete from the list of monitoring users.

{% include image.html file="delete-user-from-monitoring-list.png" caption="Delete option" %}

Now the user no longer monitors the document or document folder.


## Mark Documents and Document Folders as Favorites {#favdocsandfolders}

You can star documents and document folders as favorites on the Documents List page. The documents and folders marked as favorites are added to the list of favorite documents and document folders. 

To mark documents or document folders as favorites:

1. Select **Project Home > Documents**.

2. Hover your mouse over a document or a document folder on the Documents List page and click the star icon {% include inline_image.html file="documents-favorites-icon.png" %} to mark it a favorite.

   {% include image.html file="set-single-doc-as-favorite.png" caption="Mark a document or document folder as favorite" %}

3. To mark multiple documents and document folders as favorites, select the documents and document folders and click the star icon at the top of the Document List page.

   {% include image.html file="set-multiple-docs-as-favorites.png" caption="Mark multiple documents and folders as favorites" %}

   Favorite documents and folders have a star showing up next to their names. Also, the grey star icon changes to blue star icon.

   {% include image.html file="docs-set-as-favorites.png" caption="Selected documents are set as favorites" %}

4. Select the **Favorites** left navigation menu to view the list of favorite documents and folders.

   {% include image.html file="documents-favorites-list.png" caption="List of favorite documents and folders" %}

<!--artf392685-->
## Lazy-loading of Document Folders and Documents {#listdocsfoldersonscroll}

Unlike the old Documents List page, the new page supports lazy-loading of documents and document folder as you scroll down the page. 

This optimizes the performance by not loading a large number of documents and document folders right away while keeping you waiting to do things.

{% include callout.html type="primary" content="**Known Issue**: As long as the contents of a document folder with a large number of documents/sub folders are being loaded, you cannot perform any other action on the new Documents List page." %}

<!--artf392861
## Sorting Document Folders and Documents {#sortdocsfolders}

You can sort the list of documents and document folders in either ascending or descending order. The documents and document folders can be sorted by their name, status, size, flex fields, last edited by, last edited on, and so on.

By default, the list of documents/document folders are sorted by their name/id in ascending order. This is indicated by an upward arrow next to the column name. 

{% include image.html file="sort-documents-folders.png" caption="Documents and folders sorted by name/id in ascending order" %}

To sort the list in descending order, click the upward arrow next to a column name. Once the list gets sorted in descending order, a downward arrow shows up next to the column name by which the list was sorted. -->

<!--artf391328-->
## Configure Default Document Columns {#docscolumnconfig}

The **Column Configuration** feature for Documents has been enhanced in the redesigned documents list page.

To configure the document columns:

1. Go to **Project Home > Documents** page.

2. Click the **The New Documents** toggle button to go to the redesigned Documents List page.

3. Click the **Column Configuration** icon ( {% include inline_image.html file="documents-column-config-icon.png" %}) on this page.

4. Select the **Column Configuration** option.

   {% include image.html file="document-column-configuration.png" caption="Column Configuration option" %}

5. Select the required user-defined (flex) field from the **All fields** list.

   {% include image.html file="documents-column-config-dialog.png" caption="Column Configuration Dialog" %}

6. Click the `>` button to move the selected field to **Selected fields** list. 

7. Repeat the steps 5 and 6 to add more fields to the list of selected fields.

   You can change the order of the fields added to the **Selected fields** list. To reorder the fields, click and drag the required field and drop it up or down any other field in the list.

   For instance, if you want to place the second item "MultiSelect1" field as the third item in the list, just click, drag, and drop it after the "Text1" field, which is the third item currently.

   {% include image.html file="documents-reorder-fields.png" caption="Reordering fields in \"Selected fields\" list" %}

8. Click **Apply & Save** to save the settings before it is applied on the documents list page.

   {% include note.html content="Click **Apply** to just apply the defined column configuration without saving it. However, if you do any other action on the page, " %}

   {% include image.html file="documents-apply-column-config.png" %}

9. Enter a name for the configuration.

   {% include image.html file="docs-save-column-config.png" %}

10. Select the **Make it Default** checkbox to set this as the default configuration.

11. Click **Save**.

    The saved configuration is listed under the **Column Configuration** and is applied successfully on the documents list page.

    {% include image.html file="documents-saved-column-config.png"  caption="Saved column configuration" %}

### Save an Applied Column Configuration

You can saved a defined configuration of document columns after applying it.

To apply and then save a column configuration:

1. Click the **Column Configuration** icon ( {% include inline_image.html file="documents-column-config-icon.png" %}) on the documents list page.

2. Select the **Column Configuration** option.

   {% include image.html file="document-column-configuration.png" caption="Column Configuration option" %}

3. Select the required user-defined (flex) field from the **All fields** list.

   {% include image.html file="documents-column-config-dialog.png" caption="Column Configuration Dialog" %}

4. Click the `>` button to move the selected field to **Selected fields** list. 

5. Repeat the steps 5 and 6 to add more fields to the list of selected fields.

   You can change the order of the fields added to the **Selected fields** list. To reorder the fields, click and drag the required field and drop it up or down any other field in the list.

   For instance, if you want to place the second item "MultiSelect1" field as the third item in the list, just click, drag, and drop it after the "Text1" field, which is the third item currently.

   {% include image.html file="documents-reorder-fields.png" caption="Reordering fields in \"Selected fields\" list" %}

6. Click **Apply**.

7. After the configuration is applied, repeat steps 1 and 2 to open the **Column Configuration** dialog.

8. Click **Apply & Save**.

9. Enter a name for the configuration.

   {% include image.html file="docs-save-column-config.png" %}

10. Select the **Make it Default** checkbox to set this as the default configuration.

11. Click **Save**.

The saved configuration is shown on the documents list page.

### Delete a Column Configuration

You can delete a saved column configuration, if required.

To delete a column configuration:

1. Click the **Column Configuration** icon ( {% include inline_image.html file="documents-column-config-icon.png" %}) on the documents list page.

2. Hover your mouse on the user-defined column configuration name for the delete icon to show up.

3. Click the delete icon.

   {% include image.html file="docs-delete-column-config.png" caption="Delete option" %}

4. Click **Confirm** to delete the configuration.

   {% include image.html file="docs-column-config-deleteconfirm.png" caption="Confirm deletion of column configuration" %}

   The selected column configuration is deleted successfully.

<!--artf391352-->
## Search Document Folders and Documents {#searchdocsfolders}

You can search for document folders and documents from the Documents List page. 

* You can search for a document or a document folder by its Name. 
* You can do a whole word search for documents and document folders with the keyword within double quotes.
* You can also do an advanced search for documents with a wide-range of parameters. 

To search for a document or a document folder:

1. Select the column configuration on which you want to search.

2. Click the search icon.

3. Type at least two characters of the search keyword in the search text box to view the search results as you type.

   Documents matching the search keyword are displayed.

   {% include image.html file="search-docs-folders.png" caption="Search for documents and document folders" %}

   {% include image.html file="doc-search-results.png" caption="Search results showing both documents and document folders" %}

<!-- ### @user and #status Simple Search
The Documents List page's search function supports @user and \#status simple search. 

@user
: Use the @user simple search to search for documents and document folders that are last edited by a specific user. Username predictions are shown as soon as you type `@` followed by at least two characters of the username in the Search text box.
: {% include image.html file="20.0-docsuments-01.png" caption="Username predictions as you type" %}
: {% include image.html file="20.0-docsuments-02.png" caption="@user search results" %}

\#status
: Use the \#status simple search to search for documents and document folders that are in a specific status. A list of available statuses to search for are shown as you type `#` in the Search text box.
: {% include image.html file="20.0-docsuments-03.png" caption="A list of available statuses shown as soon as you type `#`" %}
: {% include image.html file="20.0-docsuments-04.png" caption="#status search results" %} -->

### Whole Word Simple Search
<!-- Artifact artf396844 : [Doc Task] Document " Add double quotes feature in simple search" -->
The Documents List page's search function supports whole word search for documents and document folders.

Just include the search keyword within double quotes to do a whole word search. Document and document folder title is searched for a match when you do a whole word search.

{% include image.html file="201-wholewordsearch-01.png" caption="Whole word search within double quotes" %}

### Advanced Search {#advanced-search}
<!-- Artifact artf396422 : [Doc Task] - Advanced search in new list documents page -->

{% include image.html file="201-advanced-doc-search-01.png" caption="Advanced documents search options" %}

When you want to narrow down your search results with one or more documents you want, you would typically search with more than one of the following advanced search parameters.

Perform search in
: **Root Folder** or **Current Folder**. 
: Select the folder where you want to search for documents. 
: **Current Folder** is selected by default. 
: Click **Root Folder** to search the root folder (and subfolders). 

Search Inside
: **Name and Description**, **Documents** and  **All text fields**
: Select one or more of these check boxes to search. You must select at least one of these check boxes.
: You can search the name and description of documents, the document content, and all the text fields.

Version
: **Active** or **All**
: Select **Active** or **All** to search the active and all document versions respectively. 
: **Active** document versions are searched by default.
: Select **All** to search all document versions.

Tags
: Select one or more tags to search for documents that are tagged with the selected tags.
: Click **Add tag** and select one or more tags. 

Status
: Select one or more statuses to restrict your search to documents that are in one of the the selected statuses.

Date
: **Modified** or **Created**
: Select **Modified** or **Created** to search for documents that are modified or created on a particular date respectively. 
: Select one of the following options from the drop-down list to search for documents that are modified or created: **Today**, **Yesterday**, **Last 7 Days** and **Last 30 Days**. 
: **Any Date** is selected by default. 
: You can also select **Custom Date** from the drop-down list and select a custom date range from the **From** and **To** date fields. 
: {% include image.html file="201-advanced-doc-search-02.png" caption="Date-based search options" %}

Created/Modified by
: Select one or more users to search for documents created or modified by the selected users. 
: Click **Add user** and select one or more users from the drop-down list.

Custom Fields
: You can also include custom fields (single/multi select, user, and date fields) in your advanced documents search.

To perform an advanced documents search:
1. Click the search icon
2. Click the advanced search icon (the guitar icon).
3. Select the advanced search criteria. 
4. Click **Search**. The search results are displayed.
   {% include note.html content="Search results are restricted to a maximum of 500 documents. You must refine your search criteria in case your search results are not fetching you the documents you are looking for." %}
5. Repeat steps 2 through 4 to further refine your search criteria. 

## Recent Documents {#recentdocfiles}

You can see the list of recently added, modified, and viewed documents from the **Recent Files** page.

Select the **Recent Files** left navigation menu on the documents home page to view the list of documents that are recently added, modified, and viewed.

{% include image.html file="recent-document-files.png" caption="List of recently added, modified, and viewed documents" %}

## Tag Cloud
<!-- Artifact artf394065 : Doc Task for artf393339 : Tag clouds -->
Tags are another means of navigating/classifying your documents. While nothing has changed with the way you create or manage tags, Tag Cloud unlocks the potential of tags as a means of navigation/classification and brings tags to the forefront in the form of tag clouds.

A Tag Cloud is a group of tags added to the left navigation pane of the Documents List page. You can filter documents by tags.

{% include image.html file="tagclouds01.png" caption="Tag Cloud" %}

* The Tag Cloud shows the most recently used tags.
* Click a tag to list all the documents that are associated with that tag.
* Click **All Tags** to view all the tags in the Documents List page. 
* A tag in the tag cloud is visually distinguishable by its size and shade.
* The font size and shade of a tag indicates the number of documents associated with a tag. 
* A bigger font size and a darker shade means that more number of documents are associated with the tag.
* Tags in the Tag Cloud are sorted and listed—the tags list starts with the most recently used tags followed by the least recently used ones.

## Delete Documents and Document Folders {#deletedocuments}
<!-- Artifact artf395940 : [DOC TASK] Documents Delete operation from New UI -->

You can either delete documents and folders one-by-one or select multiple documents and folders and delete them. When documents and folders are deleted, an email notification is sent to notify users monitoring the documents and folders.

1. Select a folder from the **All Files** drop-down menu from the left navigation pane. 
2. To delete:
   * an individual document or folder, hover over any document or document folder, click the more icon and select **Delete** from the contextual menu.
     {% include image.html file="201-deletedocs-01.png" caption="Contextual menu to delete an individual document or folder" %}
   * multiple documents and folders, select the documents and folders you want to delete, click the more icon at the top of the Documents List page and select **Delete**.
     {% include image.html file="201-deletedocs-02.png" caption="Action menu at the top to delete multiple documents and folders" %}
   A confirmation message appears.
     {% include image.html file="201-deletedocs-03.png" caption="Confirmation message" %}   
4. Clik **Confirm** to delete the selected documents and folders.

**Also see**: [Hard-links Between Baselines and Configuration Items][baseline-overview.html#baselineshardlinks]


{% include links.html %}