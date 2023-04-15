---
title: TeamForge-Git Integration
keywords: git, gerrit, integration
tags: [ctf_20.2, git_gerrit, integration, source_code, code_review]
sidebar: teamforge_sidebar
permalink: gitoverview.html
last_updated: Jul 13, 2020
summary: TeamForge supports integration with Git, a distributed version control tool powered by Gerrit.
---

Although Git is the world’s leading distributed version control system, the enterprise has been slow and tentative in its adoption. Concerned with security breaches, compliance violations and lack of governance, many organizations have chosen to take a "wait and see" approach. With TeamForge, Git is ready for the enterprise. TeamForge lets you realize all the benefits of Git while ensuring the security, governance and manageability your business demands. With TeamForge, you can even manage Git and Subversion together, within each individual project.

Gerrit is an open source code review system designed to work with Git. Gerrit supports various access control mechanisms. The TeamForge Git integration uses Gerrit as a vehicle to bring TeamForge project roles and permissions into Git.

{% include image.html file="teamforge-git-overview.png" %}


## Install or Upgrade TeamForge-Git Integration

You can install Git on the TeamForge Application Server or on a separate server dedicated for SCM. For more information about installing and upgrading Git, see TeamForge install and upgrade instructions.

## Git Integration Blog Posts
You can also read the [CollabNet blog posts on Git](http://blogs.collab.net/git) and follow the latest developments in the Digital.ai TeamForge-Git integration space.

## Add Git as a Linked Application

Once you have installed Git, you can add Git as a linked application on your TeamForge site.

{% capture cap1 %}
{% include inline_image.html file="status-success-small.png" %} In TeamForge 7.2 and later versions, installing Git for the first time creates a site-wide linked application automatically.<br><br>
<!-- {% include inline_image.html file="status-success-small.png" %} In TeamForge 8.0 and later versions, in addition to a site-wide linked application, a project-wide linked application is also created for projects in TeamForge that have at least one CVS repository.<br><br> -->
{% include inline_image.html file="status-success-small.png" %} However, this behavior can be controlled by the `teamforge.createTFProjectLinkedApps` Gerrit config (`gerrit.config`) property.
{% endcapture %}
{% include callout.html type="primary" content=cap1 %}

1. Set up the URL `http://<TEAMFORGEHOSTNAME>/gerrit/sso/`.
   {% include note.html content="The `/` at the end of the URL matters. Make sure you have it." %}
2. For instructions on setting up a site-wide linked application in TeamForge, see [Create a Site-wide Linked Application][externalapplications.html#linkedapps]. 
   
   Here's an example for Git:
   
   {% include image.html file="gerrit-linkedapp-80.png" %}
   
   A link for Git is added to the More menu in your TeamForge navigation bar.

   {% include image.html file="gerrit-linkedapp-80-1.png" %}

   Clicking **Git** displays the Git console in the main TeamForge window.

## Illustrations on TeamForge-Gerrit Communication

The following illustrations help you understand the communication flow between TeamForge and Gerrit in a single host and distributed environments.

### TeamForge and Git/Gerrit on a Single Host

{% include image.html file="tfgerritcomm01.png" %}

### TeamForge and Git/Gerrit in a Distributed Two-server Setup

{% include image.html file="tfgerritcomm02.png" %}

### TeamForge, Git/Gerrit and Replica Server in a Three-server Distributed Setup

{% include image.html file="tfgerritcomm03.png" %}

{% include links.html %}