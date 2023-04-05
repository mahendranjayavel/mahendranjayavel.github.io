---
title: Manage Replicas
keywords: site admin scm tasks, scm, source control
tags: [site_admin_tasks, installation, upgrade, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: managereplicas.html
last_updated: Mar 1, 2018
summary: A replica server in TeamForge is a Subversion Edge server that replicates the content of an existing core SCM integration server.
---
A replica server in TeamForge is a Subversion Edge server that replicates the content of an existing core SCM integration server.

### Approve a Replica Server Request
When there is a request for a replica of a core SCM integration server, a TeamForge administrator must approve the request before the replica is created.

Replica requests from a TeamForge admin user or site administrator are automatically approved. Replicas requested by other users need approval by a TeamForge administrator.

1. Go to **My Workspace > Admin**.
2. Click **Integrations** from the **Projects** menu.
3. On the **SCM INTEGRATIONS** tab, click the **Pending SCM Replicas** tab.
4. From the list of pending SCM replica requests, select the SCM replicas that you want to approve.
5. Click **Approve** to approve the replica.
6. Click **Reject** to reject the replica and remove it from the list.
   
   When a replica is approved, it is listed in the SCM INTEGRATIONS tab beneath the master SVN server.

### Edit Replica Settings
As a TeamForge site administrator, you can configure replica settings for the polling frequency of the master, and repository initialization and synchronization events.

Replication events, such as creating new repositories and synching commits, are stored in a queue on the TeamForge Application Server. The replica server polls the TeamForge Application Server for new events and then processes those events on the replica server.

These events are divided into two separate pools:
* New repository initializations--this includes creating the repository and performing the initial synchronization of the content.
* All other events

When existing repositories are selected for replication, this can take a long time. It could take many hours or even days to fully replicate an entire repository across a WAN. These big events are processed in their own thread pool, so that other repositories which are already synchronized don't have to wait in line for them to finish.

For each pool, you can define how many simultaneous events will be processed. The higher the number, the greater the potential load on both the TeamForge replica server and the Subversion master. However, this can also decrease the wait time for a given commit to appear on the replica server.

1. Go to **My Workspace > Admin**.
2. Click **Integrations** from the **Projects** menu.
3. On the **SCM INTEGRATIONS** tab, click the name of the Subversion Edge replica you want to edit.
4. The **Edit System** page for the replica appears. Here's an example:
   {% include image.html file="editreplica_in_tf.png" %}
5. Change the replica name or description if required.
   {% include tip.html content="Including the geographic location would help users select a nearby replica." %}
6. Set the **Command polling interval** to define how frequently the replica polls the master looking for new events.

   The replica will process all new events when it polls. The default value for this setting is 60 seconds, but it can range from 5 to 1000000 seconds.
7. Set the **Maximum simultaneous new repository creations** to a low value.
   
   New repository initializations can take a long time and generate a lot of load. So you wouldn't want to allow too many of them to run at once. This value can range from 1 to 100, but we suggest you keep it at 3 or less.
8. Set the **Maximum simultaneous repository synchronizations** taking into account how many repositories you will be replicating and how many you think are likely to have commits occurring within the polling interval. 

   This value can range from 1 to 100. You may want to set this higher than the previous field, but we suggest you keep it at 10 or less. There's no reason to enter too high a number because you are merely specifying how many synchs can run at the exact same time -- and it never runs more than one per repository.
9. When you've made your changes, click **Save**.

### Remove a Replica
When you remove a replica from TeamForge, it is restored to a Subversion Edge server in standalone mode.

1. Go to **My Workspace > Admin**.
2. Click **Integrations** from the **Projects** menu.
3. In the **Edit System** page for the replica, click **Delete**.
   
   The replica is removed from TeamForge. The repositories that existed on the replica are deleted.

{% include links.html %}