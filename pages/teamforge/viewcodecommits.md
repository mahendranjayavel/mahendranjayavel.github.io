---
title: View Code Commits
keywords: view code commits
tags: [project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Apr 4, 2018
permalink: viewcodecommits.html
folder: teamforge
toc: no
summary: To stay up to date with code development on a project, browse the code commits made to each repository integrated into your TeamForge site.
---

For each code commit, you can view the list of files that were checked in, the version history of each file, and any associations with other TeamForge items, such as tracker artifacts or tasks.

 {% include note.html content="You can see only those paths in the repository that the repository administrator has given you access to." %}

1. Click **SOURCE CODE** from the **Project Home** menu.

2. From the list of project repositories, select the repository you want to look at, then click **View Commits**.

3. If you have internal code browser disabled (see [Integrate a Source Code Server][integrateasourcecodeserver]): The **Commits** section of the **Repository Details** page lists all the code commits in the repository. By default, it shows the commits made over the preceding seven days.

   a. Specify the filter criteria in **Commit Name**, **Committed By** or **Committed On** date ranges and click **FILTER**.

   b. After filtering, if you want to clear the filters, click **FILTER** and select **Clear** from the drop-down list.

   c. To view the details of a commit, click its title. The **Files** section of the **Commit Details** page lists all files that were checked in with the code commit, including the version number of each file and the last operation that was performed, such as modified, deleted, moved, copied, or added.

      * To view the file information, click the file name.

      * To view the latest version of the file, click the file version.

   d. To look at other items related to this commit, click the **ASSOCIATIONS** tab.


4. If you have the internal code browser enabled (see [Integrate a Source Code Server][integrateasourcecodeserver]): The **Changes** tab lists all the commits in the repository sorted by date.

   * Use the **Expand all** toggle button to expand or hide commit log messages for all the commits or selectively show or hide the commit log for the commit you are interested in.

   * You can also **browse repository from a specific commit** you are interested in.



{% include links.html %}