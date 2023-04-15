---
title: HTML EMails for Tracker Artifacts
keywords: html emails
tags: [project_member_tasks, trackers, emails, documents]
sidebar: teamforge_sidebar
permalink: html-emails.html
last_updated: April 3, 2018
summary: From its 17.8 release, when you create or update an artifact, TeamForge sends HTML emails to users assigned to and users monitoring that artifact.
---

HTML emails are formatted emails that look like a newsletter that you receive from a web service. These emails are embellished with colors, graphics, table columns and links. In this way, HTML emails enhance the look and feel of the emails and override the simple and plain features of Text emails that only include text.

By default, the HTML email configured in TeamForge contains the artifact details such as artifact id, artifact title, description, assigned to, customer, priority, status, attachments, and so on. Details of the fields with null values are not shown in the email.

When you create an artifact, TeamForge sends an email that looks like:

 {% include image.html file="17-8-html-email-artifact-create.png" %}

The sections of the above email that are highlighted in red denote that they are links. You can click them to go to the respective destination page to which the link takes you through. For example, clicking the Artifact id and title of the artifact shown on the banner of the email takes you to the artifact details page. If you click the **Add Comment** link, you will get the following screen. This is typically your mail client in which you can enter your comments and send it. You will notice that the To and the Subject fields are autofilled already. You just need to provide your comments and hit the **Send** button. The comment that you add here gets appended to list of existing comments in the artifact details page.

 {% include image.html file="17-8-html-email-addcomments.png" %}

 The email sent when an artifact is updated contains the new and old values for fields such as Assigned To, Status, Priority, Planning Folder and so on. When you update an artifact, TeamForge sends an email that looks like:

  {% include image.html file="17-8-html-email-artifact-update.png" %}

  {% include note.html content="Outlook for Windows, Outlook for Mac, and Office 365 Web Client are the email clients that support the HTML email format." %}

{% include links.html %}
