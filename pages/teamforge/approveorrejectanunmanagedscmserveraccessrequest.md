---
title: Approve or Reject an Unmanaged SCM Server Access Request
keywords: site admin tasks, scm, source control
tags: [ctf_20.2, site_admin_tasks, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: approveorrejectanunmanagedscmserveraccessrequest.html
last_updated: Jul 10, 2020
summary: When a user asks for access to an unmanaged SCM server, an administrator must approve or reject the request.
---

* When a project administrator assigns a role that provides SCM access to a project member, a TeamForge administrator must manually create the user account on the unmanaged SCM server. Because user creation on unmanaged SCM servers is not managed by TeamForge, TeamForge cannot verify that the user account has been created. A TeamForge administrator must confirm that he or she has created the account.
* Requests for SCM access removal are also submitted for approval by the TeamForge administrator.

When you get a repository access request on an unmanaged SCM server, log on to the server and create the requested user account on the unmanaged SCM server.

1. Log on to the TeamForge application server.
2. Go to **My Workspace > Admin**.
3. Click **Integrations** from the **Projects** menu.
4. Click the **SCM ACCESS REQUESTS** tab.
5. As the user account is created, select the repository access request from the **Repository Access Requests** section and click **Approve**. You may also click **Reject** to reject the repository access request.

   The user receives an email notification that the user account has been created and that the repository access request has been approved or rejected.

{% include links.html %}