---
title: Replicate a Subversion Repository
keywords: replicate, source code, repository
tags: [project admin_tasks, project_member_tasks, source_code, subversion, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Feb 14, 2019
permalink: replicatearepository.html
folder: teamforge
toc: no
summary: When a Subversion Edge replica has been successfully registered with a TeamForge SCM integration server, it is available to project administrators in projects using that server to house repositories. To replicate a Subversion repository, you need to add it to a replica server.
---

Before you can replicate a Subversion repository, an administrator must first add one or more replica servers. This involves converting a Subversion Edge server, and then approving the replica in TeamForge.

1. Click **SOURCE CODE** from the **Project Home** menu.

2. In the list of project repositories, select the one you want to replicate and click **Settings**.

3. Select the **Replicas** tab. The available replica servers are listed here. 
   
   Here's an example:

   {% include image.html file="editrepo1.png" %}

   If you don't see any available replica server listed here, it may be because none were created for this Subversion server, or there are pending replicas which haven't yet been approved by a TeamForge administrator.

 3. From the list of Available Replica Servers, click **Add** of one or more Replica Servers to have the server(s) replicate the selected repository.

 4. Click **Save**. Now the replica server is the hosting server for the repository.

    {% include image.html file="replicatesvnrepo.png" %} <br>
    Push a commit and verify if it's replicated on the Replica Servers.


#### Related Links
* [Replicate a Git Repository][setupgitreplica.html#replicategitrepo]


{% include links.html %}
