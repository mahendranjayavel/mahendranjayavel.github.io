---
title: Add Binaries to TeamForge Projects
keywords: add, binaries, repositories, nexus
tags: [installation, project_admin_tasks, binaries, integration, projects]
sidebar: teamforge_sidebar
permalink: iaf-binaries-add.html
last_updated: Jul 31, 2020
summary: When TeamForge Site Administrator has made the Binaries application available, Project Administrators can add it as one of their project tools.
---

We'll assume you have Project Admin rights in the project.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tools** to see the list of integrated applications available in the site.
3. Click **Add Tool**.
4. Select **Binaries** from the list of tools displayed.
   {% include note.html content="Make sure you select the **Binaries** base application (for which the deployment property `BaseApp` is set to `true`) and not any Nexus server that you may have." %}
5. Click **Save**.
   {% include image.html file="202-add-binary-to-projects.PNG" %}

   If a **Binaries** button appears along with the prefix as a tooltip when you mouse over the button, your job is done.

   {% include image.html file="202-add-binary-to-projects-02.PNG" %}

{% include links.html %}