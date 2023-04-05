---
title: Edit a Project
keywords: edit project
tags: [project_admin_tasks, projects]
sidebar: teamforge_sidebar
folder: teamforge
permalink: project_edit.html
last_updated: Feb 7, 2018
summary: As a project administrator in TeamForge Lab Management, you can edit certain properties for your project.
---

 1. On the project home page for the project that you wish to edit, click **Edit Project**.

 2. Edit the following parameters:

    * **Project Summary** - A brief, one-line summary of the project.

    * **Project Description** - A more detailed explanation of the project.

    * **Project MOTD (Message of the Day)** - The Project MOTD is displayed to all users in your projects. This message also may display to users when they log in to client nodes in your project.

    * **Project-specific host allocation time limits** - In this section, project administrators can control how long users in their project can allocate hosts for. If you set this value to 0 (zero), there is no limit on the time a host can be allocated.

    If you reduce this value, users' hosts in your project may be deallocated. If deallocations will occur as a result of your lowering of the maximum allocation time, you will be warned which systems will be affected, and given a chance to change your mind.

    * **Delete this Project/Undelete this Project** - If your project is not deleted and has no hosts, you will be given the option to delete this project from TeamForge Lab Management. If your project is deleted, you will be given the option to undelete it.

     {% include note.html content="Only Domain Admins will be able to delete and undelete projects." %}

{% include links.html %}