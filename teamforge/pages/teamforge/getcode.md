---
title: Get the Code
keywords: get the code
tags: [ctf_20.0, project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Jan 24, 2020
permalink: getcode.html
folder: teamforge
toc: no
summary: Browse TeamForge to find the code you want to work on, then check out the code.
---

You can view the contents of each file in a repository, plus additional information about each file such as revision history, comments, date and time of submission, and branch and tag information. You can also view differences (diffs) between any two files. You can also search for code in a repository using TeamForge Code Search.

{% include note.html content="You can see only those paths in the repository that the repository administrator has given you access to." %}

{% include note.html content="If you're getting code from a Subversion replica repository, the TeamForge account used while setting up the replica determines what's available to be checked out. This account could have been provided total access to the master repository, or restricted access using path-based permissions." %}

1. Click **SOURCE CODE** from the **Project Home** menu.

2. On the list of project repositories, click the name of the repository in which you want to view code. For each file, the revision number, time since check-in, author, and last log entry appear in the **Repository Browser**.

   * To view a file, or to view the diffs between two files, click the file name.

   * To view a specific version of the file, click **Download**.

   * To view the differences between two files, do either of these:

     * Click **[select for diffs]** next to each of the two files that you want to compare.

     * Enter the file revision numbers in the Diffs between boxes at the bottom of the page.

3. If you need to diff files, choose a display from the **Type of Diff** menu, then click **Get Diffs**. The differences between the two files are displayed.

4. Use your source control client to check out the code to your local machine.


## Internal Code Browser

For Subversion and Git repositories, you have the option to use the TeamForge code browser which is turned on by default while integrating the source code server. Fore more information, see Integrate a source code server.

On the list of project repositories, click the name of a Subversion or a Git repository in which you want to view code. On the top right of code browser, you can select the branch/tag (for Git) or specify the revision (for SVN) you want to browse.

   * **View:** This tab allows you to do the following:

     * Browse through the folder hierarchy of the repository and view the content of specific files. For any folder or file you are viewing within a branch (Git) or revision (SVN), you can obtain the commit information pertaining to its last update.
     * While viewing a single specific commit or a file, you can see the paths that were modified in that commit, the associations including JIRA such as builds, code reviews and so on for the specific commit and the differences between files in that commit.
     * While viewing a folder, if there is a file named `readme`, `readme.txt` or `readme.md` that file will automatically be rendered beneath the list of files in the folder. If the file contains markdown formatting, it will be rendered as rich text.
     * With the new linking capability, you can refer to a line of code or a range of lines in any revision of the file.

       {% include image.html file="SCM-link_to_line.png" %}

       {% include image.html file="SCM-link_to_range.png" %}

   * **Changes:** This tab lets you view all of the commits that touched a specific path you are browsing within a branch or revision. Click a commit to view its details.

   * **Graph:** This tab provides a graphical representation of the changes made including branching and merging of repositories.

   * **Branches (for Git):** This allows you to see all of the branches in the repository in their relation to the default (master) one. Using **Compare** Branch you can see the commits in the branch that do not exist in the default branch.

   * **Tags:** This tab lets you create Git tags and tag specific points in history as being important. Typically you can use this functionality to mark release points (v1.0, and so on) with an option to add Release Notes for the tagged revision. Once you create a tag, you can use it to download source code as a zip/tar file and view the tag information in Changes and Graph tabs.
  
      {% include image.html file="171_gittags01.png" %}
      {% include image.html file="171_tags01.png" %}
      {% include image.html file="171_tags02.png" %}

   * **Reviews:** This tab lists all the Open, Merged and Abandoned reviews, both Pull Requests and Gerrit single-commit reviews. Pull requests allow developers to collaborate with each other on a code change before merging it into another branch on a GIT repository. You can access this tab only when the repository owner has enabled this feature. For more information, see [Pull Request Step-by-Step][pullrequest.html#pullrequeststepbystep].

     * **Support for both Pull Requests and single-commit Gerrit Reviews:** Supports all types of code review policies, which include Pull Requests and single commit Gerrit Reviews.
        {% include image.html file="171_scm_01.png" %}
     * **Auto refresh when a Pull Request changes:** When a pull request changes, the page is automatically refreshed to reflect the changes.
     * **Comments to support @mentions:** Inline comments are parsed for @mentions and users called out via @mentions are added as reviewers.
     * **Open your Gerrit Reviews in Gerrit's user interface:** A new button has been added to let you open your Gerrit Reviews in Gerrit's user interface.
        {% include image.html file="167_scm02.png" %}
     * **Code commenting:** During code reviews, you can now add line comments in context while looking at the files in diff view. You can double-click to block a line/text and add a comment.
        {% include image.html file="167_commenting01.png" %}

        You can also reply to line comments.
        {% include image.html file="167_commenting02.png" %}

     * **Ability to diff the change against the Base or a previous Patch Set:** As part of the Gerrit review workflow, you now have the ability to diff the change against the Base or a previous Patch Set.
      * **Markdown support:** Markdown support for all .MD files: Render Markdown files when viewed through Code Browser.
        {% include image.html file="167_md.png" %}

        TeamForge uses Showdown—a bidirectional Markdown to HTML to Markdown converter written in Javascript. For more information, see the official [Showdown Documentation](https://github.com/showdownjs/showdown/wiki). Here's an abridged version of the [Markdown syntax documentation](https://sourceforge.net/p/teamforge/wiki/markdown_syntax/).
     * **Mass delete/resurrect options:** Mass delete/resurrect options in History Protect tab:
        {% include image.html file="167massdeleteresurrect.png" %}
        {% include image.html file="167_massdeleteresurrect01.png" %}
      
     * **Inline editing of files:** Quick changes to files, if required only to few files, can be done using the inline edit feature from within the code browser without having to clone an entire repository. Browse the repository, locate and open the file in the View tab, click **Edit** to open the file in the File Editor, make your changes, **Create code review** and **Publish** your changes for review.
        {% include image.html file="171_inlinedit01.png" %}

     * **Submit whole topic:** You can now bundle related changes (code reviews) by topic and submit the whole topic for review instead of just submitting changes one-by-one. Just open a review, click the **Set Topic** link and enter the topic name.
        {% include image.html file="171_submitwholetopic.png" %}


   * **Search:** This tab lets you search for code via TeamForge Code Search powered by Elasticsearch. You can search all files in a repository or narrow your scope to specific file types such as C, C++, C# and so on. Type your search keyword, select a file extension (optional) and click Search. For more information, see [Search Code][searchcode].
      {% include image.html file="codesearch01.png" %}

   * **Settings:** This tab lets you configure the repository settings.
   * **Download:** This tab allows you to download a copy of the required file.

{% include links.html %}
