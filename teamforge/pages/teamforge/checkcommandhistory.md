---
title: Check Command History
keywords: check command history
tags: [project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Mar 5, 2019
permalink: checkcommandhistory.html
folder: teamforge
toc: no
summary: Recent command history for a replica server or a specific repository allows you to check for errors and see whether there are pending commands.
---

* Maybe a repository revision is not showing up. You can check for errors to know it's not just because the repository is still synchronizing.
* You can also check if there are commands waiting in the queue -- you'd be able to see whether the repository is truly in sync.
* To check the command history for a replica repository, follow these steps:

  1. Click **SOURCE CODE** from the **Project Home** menu.

  2. In the list of repositories, click the icon for the one you're interested in. You'll see repository details and command history. Here's an example:

     {% include image.html file="repocommandhistory.png" %}

     {% include tip.html content=" You can also check command history by clicking on the **Status** icon in the **Edit Repository** page." %}

 * You need to be a TeamForge administrator to check the command history across a replica server.

   1. On the site administration navigation bar, click **INTEGRATIONS**.

   2. On the **SCM INTEGRATIONS** page, click the name of the replica server you're interested in. The **Edit System** page displays the command history.

{% include links.html %}
