---
title: Manage Statuses for a Planning Folder
keywords: manage statuses for a planning folder
tags: [project_admin_tasks, planning_folder]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Apr 25, 2018
toc:  no
permalink: planningfolderstatus.html
summary: To help team members understand how to work with a planning folder, create statuses for it that correspond to the planning folder's life cycle.
---

When you have created a planning folder status, you can apply it to any planning folder in your project.

For example, at a given moment you might have one planning folder in "Under development" status, while another is in "Finished" status and another is in "Preliminary scoping" status.

 {% include tip.html content="You may also want to move the planning folder to a relative position in the planning folder list that communicates where it stands in the order of work." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. Click **Planning Folder Settings**.

 3. Under **Statuses**, click **Add**.

 4. Configure your new planning folder status.

    1. Give the status an unambiguous name that other will find easy to understand.

    2. Specify whether the status counts as active or inactive or freeze. Project members may want to exclude inactive planning folders from their view, to avoid overload.

       {% include note.html content="_Freeze_ is the new status added to the **Active/Inactive** drop-down list in TeamForge 18.1. If you have selected the status of a planning folder to _Freeze_, you cannot be able to move any artifact into or out of this planning folder. However, you can update any artifact within this planning folder." %}

       {% include image.html file="planningfolder-status-freeze.png" %}

    3. Select which value is the default value for new planning folders and planning folders that originated in earlier TeamForge versions.

    4. Arrange your planning folder statuses in the order that makes sense for you.


  
{% include links.html %}