---
title: File Releases and Packages
keywords: releases and packages, file releases and packages, packages, file releases
tags: [ctf_20.1, ctf_19.3, ctf_19.2, file_releases, frs, associations]
folder: teamforge
last_updated: May 5, 2020
sidebar: teamforge_sidebar
permalink: releases.html
summary: You can publish the output of your project to selected audiences as packages and releases.
---

## What is a Release?

A release is a group of one or more files that are published as a unit.

Each release can have a maturity level attribute to describe its state of completeness. Maturity levels are predefined and include development build, alpha, beta, and general availability.

The TeamForge file release system enables users to publish files and groups of files to selected audiences. Using role-based access control, administrators can control which project members can access each package or release.

## Download a Release

Downloading a release brings all the release's files to your local machine in a single .zip file.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the release you want to download.
 3. On the **List Releases** page, click the title of the release.
 4. On the **View Release** page, click **Download Selected**.

TeamForge prepares the compressed file in .zip format. You are prompted to open or save the file.

TeamForge lets you track the number of downloads for each file under **File Releases> Package > Release** within the FRS module. This helps you understand the number of downloads and then take an informed decision on whether to retain or delete a file based on the number of downloads.

## Create a Package
A package is a folder into which one or more related releases are published.

For example, you might create a package to represent a product deliverable or major component. You can then create releases within the package for product builds or other groups of files.

 {% include note.html content="A package must exist before you create the releases and individual files that will go into the package." %}  

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click **Create**.
 3. On the **Create Package** page, provide a title and description for the package.
 4. Click **Save**.

The package is created. When you have created a package, you can publish a release into the package.

## Create a Release
A release is a group of one or more files that are published as a unit.

 {% include important.html content="Before creating a release, you must have a package into which you release will go." %}
 
 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package in which you want to create the release.
 3. On the **List Releases** page, click **Add**.
 4. On the **Create Release** page, provide a name and description for the release.
 5. Set the status of the release.

    * **Pending:** Releases with pending status are not visible in the drop-down list displayed when you set **Reported In Release** and **Fixed In Release** fields in an artifact. Use **Pending** status when you have created a release but have not yet finished adding files.
    * **Active:** Releases with active status are visible in the drop-down lists displayed when you set **Reported In Release** and **Fixed In Release** fields in an artifact.

 6. Identify the maturity level of this release.
 7. Click **Save**.

The release is created. You can begin adding files.

{% include tip.html content="To facilitate tracking, you may want to match this release to the planning folder that tracks the work that's going into the release. If you do that, the relevant work items will automatically appear on the _Planned Tracker Artifact_ tab. See [Create a Planning Folder][creatingplanningfolder]." %}  	

## Edit a Release {#editfilerelease}

You can edit a file release at any point in time, if required.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package which has the release that you want to edit.
 3. On the **List Releases** page, click the release that you want to edit.
 4. Click **Edit** on the release details page.
 5. On the **Edit Release** page, edit the fields as required.
    
    A new status **Obsolete**, is added to the **Status** drop-down list in TeamForge 19.2, to mark file releases that are no longer used. 

    {% include image.html file="file-release-obsolete-status.png"  caption="The new \"Obsolete\" status" %}

 6. Click **Save**.

### Audit/Change Log for File Releases

Similar to Tracker Artifacts and Documents, you can now track the changes specific to a file release from the **Change Log** tab introduced in TeamForge 19.3.

The following are tracked in the **Change Log** tab:

* Changes to the name, description, status, and maturity of a file release.

* When associations are added to or removed from a file release.

* When a file is added, updated, and deleted in a file release.

{% include image.html file="filerelease_changelog.png" url="http://docs.collab.net/teamforge221/images/filerelease_changelog.png" caption="\"Change Log\" tab that tracks changes to a file release" %}

## Add Files to a Release
After you have created a release, you can add one or more files. All files in a release are published as a unit.

Project members can download the entire release in a single .zip file, or download only selected files.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the release.
 3. On the **List Releases** page, click the title of the release.
 4. On the **View Release** page, click **Add**.
 5. On the **Add File** page, choose the desired file, then click **Save**. The file is added and you are returmed to the **View Release** page.
 6. Repeat the last two steps until all files are added.

After you have added your files, you might wish to change the status of the release from pending to active. This will allow users with appropriate permission to select the release when entering or updating an artifact. You can also change the maturity level if needed.

## Update Files in a Release
You can replace an existing file in a release with a new file.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the release.
 3. On the **List Releases** page, in the **Releases** section, click the title of the release containing the file that you want to update.
 4. On the **View Release** page, select the file you want to update, and click **Update**.
 5. In the **Update a File** page, go to the new file with which you want to replace the current file.
 6. Click **Save**.

This file is now updated.

## Delete Files from a Release
If a file is no longer needed, it's a good idea to delete it from the release.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the desired release.
 3. On the **List Releases** page, in the **Releases** section, click the title of the release containing the file that you want to delete.
 4. On the **View Release** page, choose the file you want to delete, and click **Delete**.

The file is deleted.

## Update Release Attributes
As your release matures, you should update its maturity level and status.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the release.
 3. On the **List Releases** page, in the **Releases** section, click the title of the release containing the file that you want to delete.
 4. On the **View Release** page, click **Edit**.
 5. On the **Edit Release** page, choose a new status for the release. A release can be in Active or Pending status.
 6. Select the maturity level of this release from the **Maturity** field.
 7. Click **Save**.

<!--artf315781-TeamForge 19.0-->
## View a Baseline from View Release page {#baselinesfromviewreleasepage}

A new tab **Baselines** is added to the **View Release** page to list the baseline(s) with which the release in scope is associated. The **Baselines** tab is visible only to users with baseline license and package view permission. Click the baseline id to view the associated baseline.

{% include image.html file="release_baselines_tab.png" %}
<!--artf315781-TeamForge 19.0-->

## Change a Package's Name or Description
When the purpose or the audience for a package shifts, you may want to rename the package or describe it differently.

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, select the package you want to edit, and click **Edit**.
 3. On the **Edit Package** page, provide the new name or description.
 4. To make it easier for users to download the package, select **Show Download Link in Project List**. This makes the download link show up in the project's entry in the Project Categories system, if the project has been put in one or more categories. See [Categorize a Project][projectadmin-categorizingaproject].
 5. Click **Save**.

## Associate a Release with other items
If a file release is related to other TeamForge items, such as documents, tasks, tracker artifacts, integrated application objects, or new items, you can connect the file release to the other item by creating an association.

Creating associations between items helps you define relationships, track dependencies, and enforce workflow rules. Some example uses of file release associations include:

 * Associate a release with a requirements document.
 * Associate a beta release with a task related to managing the beta program.
 * Associate a release with tracker artifacts representing bugs fixed in the release.
 
 {% include note.html content="You can also associate tracker artifacts such as bugs and feature requests with the related file releases. You do this as part of working with the tracker." %}

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the package containing the release with which you want to create an association.
 3. On the **List Releases** page, click the name of the release.
 4. On the **View Release** page, click the _Associations_ tab and click **Add**.
 5. In the **Add Association Wizard** window, select the items with which you want to associate the artifact:
    * **Enter Item ID:** If you know the item's ID, you can enter it directly.
      {% include note.html content="To associate an object in an integrated application from within TeamForge, use the `[<prefix_objectid>]` format. Each integrated application displays its prefix on moving the mouse over the application name in the tool bar." %}
    * **Add from Recently Viewed:** Select one of the last ten items you looked at during this session.
    * **Add from Recently Edited:** Select one of the last ten items you changed.
 6. Click **Next**.
 7. You may add a comment in the **Association Comment** text box.
 8. Save your work.
    * Click **Finish and Add Another** to add additional associations.
    * Click **FInish** to return to the **Details** page.
      {% include note.html content="When an association is added to or removed from TeamFOrge objects such as tracker artifacts, tasks, documents, discussions, and file releases, a notification mail is sent to users monitoring these objects. An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui]." %}
 9. Click the _Associations_ tab to view a graphical representation of all the associated items. Through the Association Viewer, you can choose to view associations in the form of a list or flip over to the Trace view to explore the layers of associations (including parent/child dependencies) laid out in a timeline. You can scroll across the Trace view by dragging the mouse over the association layer or use the 'Previous' and 'Next' arrows to view all the objects as events in a timeline. <br>
 
 While the _Associations_ tab shows the count of the total number of associations, you can only view the most recent 500 associations when you click the _Associations_ tab in case the artifact has more than 500 associations. You can, however, browser through the **Association Viewer** to view older associations.

## Delete a Package
If you no longer need a package, you can delete it.

Deleting a package deletes all of the releases and files within it.

 {% include important.html content="Delete a package only if you are sure that you no longer need any of the releases and files within it." %}

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, choose the package that you want to delete.
 3. Click **Delete**.

The package and all of the releases and files withi it are now deleted.

**Also see**: [Hard-links Between Baselines and Configuration Items][baseline-overview.html#baselineshardlinks]

## Delete a Release
If you no longer need a release, you can delete it. Deleting a release deletes all of the files within it.

 {% include important.html content="Delete a release only if you are sure that you no longer need any of the files within it." %}

 1. Click **File Releases** from the **Project Home** menu.
 2. On the **File Release Summary** page, click the title of the containing the release that you want to delete.
 3. On the **List Releases** page, in the **Releases** section, select the release that you want to delete, and click **Delete**.

The release and all of the files within it are now deleted.


{% include links.html %}