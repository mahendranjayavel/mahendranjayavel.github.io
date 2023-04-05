---
title: Create and Manage Project Categories
keywords: projects, project, approve, lock, unlock, create, rename, delete, templates, categories, parent, child, subproject
tags: [projects, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: manageprojectcategories.html
last_updated: Mar 2, 2018
summary: To help users navigate your site, help them sort projects into categories that make sense.
---
To help users navigate your site, help them sort projects into categories that make sense.

## Add a Project Category
When you set up project categories for your site, project administrators can use this taxonomy to organize their projects.

You can create any number of top-level categories and any number of sub-category levels.

1. Go to **My Workspace > Admin**.
2. Click **CATEGORIES** from the **Projects** menu.
3. In the **Project Categories** tree, find the location where you want to create the new category.
   * Highlighting **Project Categories** creates a new top-level category.
   * Highlighting any category creates a sub-category beneath it.
4. Click **New**.
5. In the **Create Category** page, write a name and description for the category.
6. Click **Save**.
   
   The category is created. It appears in the **Project Categories** navigation tree, and is available for use by all project administrators when categorizing their projects.

## Edit a Project Category
A project category's membership and function may change over time. If it does, you can update the category's name or description.

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **CATEGORIES**. The **Project Categories** tree displays the hierarchy of existing categories.
3. In the **Project Categories** tree, find the category that you want to edit.
4. Make the changes you need and click **Update**.

## Move a Project Category
You can reorganize projects by moving a project category to another place in the project category hierarchy.

You can move a project category in the following ways:
* From a top-level category to a sub-category.
* From a sub-category to a top-level category.
* From a sub-category to another sub-category.

When you move a project category, any sub-categories that it contains are also moved to the destination category.

1. Go to **My Workspace > Admin**.
2. Click **CATEGORIES** from the **Projects** menu.
3. On the **Edit Category** page, in the **Project Categories** section, click the project category you want to move.
4. On the **Edit** menu, click **Cut**.
5. Find the location to which you want to move the selected project category. You can move a project category either to the root category or into any other project category.
6. Select **Paste** from the **Edit** menu.
   
   The project category is now moved to the selected destination.

## Delete a Project Category
If you no longer need a project category, you should delete it.

When you delete a project category, all of its sub-categories are also deleted.

1. Go to **My Workspace > Admin**.
2. Click **CATEGORIES** from the **Projects** menu. The **Project Categories** tree displays the hierarchy of existing categories.
3. Using the document tree, find the project category that you want to delete.
4. Choose **Delete** from the **EDIT** menu.
   
   The project category and all of its sub-categories are deleted.

## Stop Using Project Categories
If you do not need to sort projects into categories, remove the ability to do so on your site.

By default, project categorization is disabled for new TeamForge installations.

{% include note.html content="Disabling project categorization does not delete categories you have already set up." %}

1. Go to **My Workspace > Admin**.
2. Click **CATEGORIES** from the **Projects** menu.
2. On the **Edit Category** page, select **Disabled** for **SITE-WIDE CATEGORIZATION** and click **Update**.
   
   Project categorization is disabled for your TeamForge site.

{% include links.html %}