---
title: Set up Webhooks for Repositories
keywords: webhooks for repositories
tags: [ctf_20.2, project_admin_tasks, webhooks]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jul 13, 2020
toc: no
permalink: webhooksforrepositories.html
summary: Webhooks can be configured both at a project level or for select repositories. Once set up, SCM events such as commit and merge are published to the Webhooks for other applications to consume.
---

Keep the Webhook URL (of the application that consumes TeamForge SCM event information) handy before you proceed with setting up Webhooks in TeamForge. You can set up Webhooks for Git and Subversion repositories.


## Create a Webhook

 1. Log on to TeamForge and select a project from the **My Workspace** menu.

 2. Click **SOURCE CODE** from the **Project Home** menu.

 3. Select a repository and select the **SETTINGS** tab.

 4. Select the **POLICIES** tab.

 5. Type the Webhook URL in the **WEBHOOK URLS** field, select an event type from the drop-down list and click **Add**.

    You have successfully created a webhook for the repository.

 6. Repeat steps 4 and 5 to add more webhooks, if required.

    {% include image.html file="1711-webhooks02.png" %}

   
{{site.data.alerts.hr_shaded}}
#### Related Links

* [Set up Webhooks for Tracker Artifacts][webhooksfortrackerartifacts]
* [Set up Webhooks for Projects][webhooksforprojects]



{% include links.html %}