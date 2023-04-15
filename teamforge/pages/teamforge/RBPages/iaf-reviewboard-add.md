---
title: Add Review Board to TeamForge Projects
keywords: add, review board, exclude, repositories, synchronize, subversion, tool, prefix
tags: [installation, project_admin_tasks, review_board, integration, projects, subversion]
sidebar: teamforge_sidebar
permalink: iaf-reviewboard-add.html
last_updated: Apr 5, 2018
summary: When TeamForge Site Administrator has made the Review Board application available, Project Administrators can add it as one of their project tools.
---
When you add Review Board to your project, it works just like the other TeamForge tools, authorization, authentication, go-urls, association, linkification and source code management support.

For this example, we'll call your project "testproject" and we'll assume you have Project Admin rights in that project.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tools** to see the list of integrated applications available in the site.
3. Click **Add Tool**.
4. Select **Review Board** from the list of tools displayed. 

   Set the values that make sense for your TeamForge installation, then click **Save**.

   <table class="table" markdown="1">
   <thead>
   <th>Option</th>
   <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td markdown="1">**Prefix**
   </td>
   <td markdown="1">Specify a unique alphanumeric string that will identify this tool throughout the site.

   For example, suppose you set your prefix to `ZZ`. Entering `ZZ_1` in the `Jump to ID` redirect you to review request id 1 of the "testproject" project. Another may also add Review Board as a tool, with a prefix of `YY`.Jumping to `YY_1` will redirect to review request id 1 of that project.
   {% include note.html content="The tool prefix cannot be changed after you have set it." %}
   </td>
   </tr>
   <tr>
   <td markdown="1">**Exclude Repositories**
   </td>
   <td markdown="1">Use a comma to separate the directory names of the repositories that you want to exclude from syncing with Review Board. To include all repositories, enter "None".
   {% include important.html content="You must sync repositories with Review Board (select **Synchronize Repositories** check box) to have the repositories listed in this **Exclude Repositories** text box excluded." %}
   </td>
   </tr>
   <tr>
   <td markdown="1">**Synchronize Repositories**
   </td>
   <td markdown="1">Synchronize TeamForge Subversion repositories with Review Board.
   {% include note.html content="Select this check box every time you want to sync repositories to Review Board. When you add Review Board to your project with this check box selected, the SVN repositories are synced once and the check box is cleared. For any new repositories you create, you must edit the Review Board (**Project Admin > Project Toolbar > Edit Integrated Application**) and sync new repositories with Review Board by selecting this check box." %}
   </td>
   </tr>
   </tbody>
   </table>
	
   If a Review Board button appears along with the prefix as a tooltip when you mouse over the button, your job is done.

{% include links.html %}