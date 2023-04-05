---
title: Set up Hardware for your Team to Use
keywords: add lab management, set up hardware
tags: [project_admin_tasks, site_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: getstarted-cubit_getandlink.html
last_updated: Feb 7, 2018
summary: When you set up Lab Management, your team members can use TeamForge to access their own virtual machines for developing and testing.
---
1. Go to your **Lab Management** project.
2. Select **Project Admin** from the **Project Home** menu.
3. Click **Tools** from the Project Admin menu.
3. Click **Add Tool**.
4. Select **Other** from **Select Tool Type** drop-down list.
5. Enter the display name as **Lab Mgmt**.
6. Select the **Show in Toolbar** check box.
7. Enter the server location or URL of your Lab Management server.
8. If you are a TeamForge administrator, select whether you want to use single sign-on for the linked application.
   * If you use single sign-on, TeamForge manages authentication for Lab Management, and users don't have to log into Lab Management after they have logged into TeamForge.
   * If you do not use single sign-on, users must log into Lab Management using its native authentication system.
9. Click **Browse** and select the icon ( {% include inline_image.html file="LMserver.png" %}) for the linked application.
10. Click **Save**.

A **Lab Mgmt** button is added to your **Project Home** menu. Clicking it launches the application in the main TeamForge project window.

{% include links.html %}