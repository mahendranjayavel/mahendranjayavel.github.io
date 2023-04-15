---
title: Mass Configuration of Repository Policies Within a Project
keywords: mass configuration repository policies
tags: [ctf_19.1, project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Apr 30, 2019
permalink: mass-repo-policy-settings.html
folder: teamforge
summary: You may often want to apply a specific set of policies to more than one repository. You can just select multiple repositories within a project and apply your policies in one go.  
---
For mass configuration of repository policies&mdash;select the repositories, define the policies, review and apply the policy settings for selected repositories.

1. Click **SOURCE CODE** from the **Project Home** menu.
2. Select the **Repositories** tab.
3. Select all the repositories for which you want to set the policies and click **Settings**.
4. Use the toggle button to enable or disable the settings.
   <!-- Use this for web output -->
   {% unless site.output == "pdf" %}
   [![Mass Configuration of Repository Policies](images/19-1_mass-repo-policy-config.png)](images/19-1_mass-repo-policy-config.png)
   {% endunless %}

   <!-- Use this for pdf output -->
   {% unless site.output == "web" %}
   {% include image.html file="19-1_mass-repo-policy-config.png" %}
   {% endunless %}
5. Click **Review** to review the policy settings.
   {% include image.html file="review-mass-repo-policy-settings.png" %}
6. Click **Apply**.


{% include links.html %}