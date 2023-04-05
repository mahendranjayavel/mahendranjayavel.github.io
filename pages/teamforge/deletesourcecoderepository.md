---
title: Delete a Source Code Repository
keywords: delete, source code, repository
tags: [ctf_20.2, project_admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Jul 10, 2020
toc: no
permalink: deletesourcecoderepository.html
folder: teamforge
summary: When you delete a repository, a request is submitted to the administrator for approval.
---

You need to have the required permission to delete SCM repositories.

1. Click **SOURCE CODE** from the **Project Home** menu.

2. In the list of the repositories, select the repository you want to delete and click **Delete**. The following confirmation message appears: `All SCM data in this repository will be lost. Are you sure you want to delete this repository?`

3. Click **OK** to delete.

Your request for deleting a repository is submitted. You will receive an email notification when your repository is deleted or if your request for deleting a repository is denied.

* If the SCM server that you chose does not require approval for deleting repositories, the repository is deleted right away.
* If the SCM server that you chose requires approval for deleting repositories, a Digital.ai TeamForge administrator must approve your request to delete a repository before it is deleted.

{% include links.html %}