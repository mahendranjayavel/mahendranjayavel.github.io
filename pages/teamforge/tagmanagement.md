---
title: Set up Tags
keywords: how to set up tags, how to manage tags
tags: [project_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Dec 24, 2019
toc:  no
permalink: tagmanagement.html
summary: Creating tags and tagging items such as documents, artifacts and so on can aid in classification, marking ownership of work items, marking items as milestones, releases and requirements, and so on. Project Administrators can set up tags to be used by project members in a project. However, project members with CREATE/EDIT permissions can create tags, if required.
---

Tags, once set up, can be used for tagging items such as Documents, Tracker Artifacts, and so on. To start with, TeamForge 17.1 supports tagging for Documents. Tagging will be extended for other objects in due course.

 {% include note.html content="While project members with CREATE/EDIT permissions can create new tags in a project, only project administrators can delete tags." %}

To set up tags,

 1. Select a project from **My Workspace** menu.

 2. Select **Project Home > Tags**.

 3. Type a tag title and click **Add Tag**.

    {% include note.html content="A tag can be of 36 characters in length and can contain both alphanumeric and special characters." %}
   
    {% include image.html file="tagmanagement01.png" %}

 4. Click a tag to edit the tag's title and description, edit the tag and click **Save**.

    {% include image.html file="tagmanagement03.png" %}

 5. To delete a tag, click the "X" mark of the tag. A confirmation message appears. Click **OK** to delete the tag.

    {% include warning.html content="When you delete a tag, all associations between the specific tag and TeamForge objects are removed. Exercise caution before deleting tags." %}

{% include links.html %}