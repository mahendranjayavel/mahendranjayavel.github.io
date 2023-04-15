---
title: Create a Source Code Repository
keywords: create, source code, repository
tags: [ctf_20.2, ctf_20.0, project_admin_tasks, project_member_tasks, source_code, git_gerrit, scm, ctf_19.2]
sidebar: teamforge_sidebar
last_updated: Jul 10, 2020
permalink: createasourcecoderepository.html
folder: teamforge
summary: Each project can have one or more source code repositories. Before you can create a source code repository, a site administrator must first add one or more SCM servers to the Digital.ai TeamForge environment.
---

1. Click **Source Code** in the project navigation bar.

2. In the list of the project repositories, click **Add**.

3. On the **Create** tab, choose the server on which you want to create the repository.

   {% include note.html content="The menu contains all of the SCM servers that the Digital.ai TeamForge administrators have added to the Digital.ai TeamForge environment." %}

   {% include image.html file="20.0-scm-settingstoggle.png" caption="The Create repo tab" %}   

   Configure Advanced Repository Settings During Repository Creation
   : The repository **Create** tab lets you create repositories by simply giving the repo a name and selecting the destination server. However, a **Settings** toggle button ia also available, which if selected, shows you all the advanced repository settings—thereby letting you configure the advanced repository settings at the time of repository creation itself. 
   : This toggle button is not selected by default. 
   : {% include image.html file="20.0-scm-settingstoggle.png" caption="The new Settings toggle button" %}
   : {% include image.html file="20.0-scm-settingstoggle01.png" caption="The Create repository tab with the Settings toggle button selected" %}

4. Select the **Settings** toggle button. 

5. Enter a name, display name, and description for the repository. If you plan to use an SCM server that requires approval for new repositories, use the **Description** field to provide your reason for asking to create this repository.

6. **This field is enabled only if you've chosen a Git server**. Choose a code review policy option from the **REPOSITORY CATEGORY** drop-down list. For more information on Gerrit code review policies, see [Control Your Code Review Policy][codereviewpolicy].

   {% include note.html content="From TeamForge 19.2, the review rules can only be configured from the **Settings > Policies** tab of the repository, after the repository has been created." %}

7. **This field is enabled only if you've chosen a Git server**. **PROTECT HISTORY** check box is selected by default. You can disable it, if required. For more information on history protection, see [History Protection][historyprotect].

8. **This field is enabled only if you've chosen a Git server**. Choose values from **GIT LFS ENABLED** and **MAX LFS OBJECT SIZE** drop-down lists. For more information, see [Set up LFS][setuplfs].

9. If you want each code commit to be associated with an artifact (or a task or some other work item) necessarily, select **Required on commit** option next to the **Association** field.

  {% include note.html content="A new rule has been added for enhanced commit governance. This rule enforces that the artifact and the commit must be in the same TeamForge project." %}
  {% include image.html file="SCM-same_project_association.png" %}

10. For security reasons, you may want to restrict email notifications to the essential information. If so, select **Hide Details in Monitoring Messages**.

11. To index the content of the repository and to make the repository content available in search results, select **Repository content will be available in search results**.

12. Click **Create Repository**.

Your request for a new repository is submitted. You will receive an email notification when your repository is created or if your request for a new repository is denied.

* If the SCM server that you chose does not require approval for new repositories, the repository is created.
* If the SCM server that you chose requires approval for new repositories, a Digital.ai TeamForge administrator must approve your repository before it is created.

<!-- {% include note.html content="For information about implications of TeamForge EventQ integration on SCM commits and associations, see [SCM Commits in TeamForge with EventQ Integration][eventq_overview.html#scmcommitsinTFeventqintegration]." %} -->


{{site.data.alerts.hr_shaded}}
#### Related Links

* [Import a Git Repository into TeamForge][import-git-repo]
* [Gerrit Code Review Policies][codereviewpolicy]
* [History Protection][historyprotect]
* [Set up LFS][setuplfs]




{% include links.html %}