---
title: Approve or Reject a Source Control Repository Request
keywords: site admin scm tasks, scm, source control
tags: [site_admin_tasks, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: approveorrejectasourcecontrolrepositoryrequest.html
last_updated: Mar 14, 2018
summary: When a user requests a source code repository on a source control server for which you have required approval, a TeamForge administrator must approve the request before the repository is created.
---

* When adding a source control server integration, you have the option to require TeamForge administrator approval for all repositories created on the server.
* When a user requests a source code repository on a managed SCM server, the repository is created automatically after it is approved by a TeamForge administrator.

{% include important.html content="Before approving a source code repository request for an unmanaged SCM server, a TeamForge administrator must create and integrate the repository manually." %}

1. Click **Admin** in the TeamForge navigation bar.
2. Click **Integrations** from the **Projects** menu.
3. Click the **PENDING SCM INTEGRATIONS** tab.
   {% include note.html content="Non-site administrators can now access the SCM Integrations tab if they have permission to manage SCM integrations." %}
4. From the list of pending SCM repository requests, select the SCM repositories that you want to approve.
5. Click **Approve** to approve the repository.
6. Click **Reject** to reject the project and remove it from the list.
   
   The person who requested the repository receives an email notification when the repository is approved or rejected. If you entered a comment, that also appears in the email notification.

{% include links.html %}