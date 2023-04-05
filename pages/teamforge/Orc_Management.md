---
title: Activity Sources and Associations
keywords: EventQ, activity sources
tags: [eventq, install, upgrade]
sidebar: teamforge_sidebar
permalink: Orc_Management.html
last_updated: Jan 9, 2018
summary: EventQ provides a mechanism, allowing you to add relevant project tools to the TeamForge project context. This is accomplished through—sources—which represent light-weith integrations to external products. Add sources that populate activity streams with relevant activity data such as work item updates, commits, CI builds, and code reviews.
---

## What is a Source?

TeamForge is an open development platform with a strong notion associations. Within TeamForge, any two objects can be associated together, and when multiple associations are chained together, they create "traceability". But what about tools outside of TeamForge? EventQ provides just such a mechanism, allowing you to add relevant project tools to the TeamForge project context. This is accomplished through—sources—which represent light-weight integrations to external products. Once established, "sources" capture activity data from external tools, bringing them into the TeamForge project context and associations fabric.

* For work items, sources are issue trackers.
* For SCM commits, sources are defined as the code repository of interest.
* For CI builds, sources are "jobs" or "build configurations".
* For code reviews, sources are defined as the project or repository of interest.

## How do Sources work?

Whenever an "activity" occurs in a tool that has been setup as a project source, a special "adapter" sends notification of the activity to TeamForge EventQ. For example, if a specific Jenkins job is configured as a source, build information will be sent to TeamForge EventQ when that Jenkins job is executed. The resulting activity is mapped to the TeamForge project in question. A TeamForge project can have multiple sources, all sending their activity data to the TeamForge project.

## Associations

TeamForge EventQ creates associations between activities such as reviews, commits, builds, and work items.

Associations are relationships between activities like work items, commits, builds, and reviews. You can see associations for a particular activity on its TeamForge EventQ detail page or create a traceability graph of associations using the Trace associations button from an activity details page.
Most associations in TeamForge EventQ center around commits. That is, builds, work items, and reviews associate directly to commits, while a build-to-review association are implied through a common commit.

Builds are associated to commits by the underlying CI/build system. Typically, CI/build systems obtain source code from a target repository and build based on that specific revision of source code. TeamForge EventQ therefore relies on the CI/build system to report the associated revisions, which then get mapped as associations between commits and builds in TeamForge EventQ.

Reviews associate to commits in one of two ways, depending on the process being employed and the source code review product. 

When creating code reviews, note that the code review's repository URL must match the one specified while configuring the related SCM source. Otherwise, TeamForge EventQ will not be able to register associations between commits and reviews.

Work items can be directly associated to commits by referencing the work item artifact ID in the commit message. 

<!-- {% include reusables/sourceassociationkey.html %} -->

## Extensible Data Source (XDS) Overview {#xdsoverview}

EventQ can be configured to accept data from a wide range of sources through the Extensible Data Source (or XDS) feature. In addition to the stock activity APIs defined for commits, builds, reviews, and work items, the XDS feature enables you to create your own activity APIs by defining an "XDS Schema" that describes the expected activity message format for a particular tool or product domain in question. See [Extend TeamForge EventQ][extend_eventq] for more information.

"XDS Sources" can be added to your project through the "Custom" source type. Once added, XDS activities will be visible in the activity stream. XDS sources can also have associations just like any other source resulting in traceability between XDS and other activities, even between multiple XDS sources. For more information, see [Manage XDS Sources][Orc_Management.html#xdssources].

## Manage Build Sources {#buildsources}

Add build sources to bring automated build job results into the TeamForge project and traceability context.

Build sources bring build/CI data into EventQ for archival of metadata, participation in traceability, and activity reporting.

### Create or Find an Existing Tool to Group Your Build Source Under

1. From the desired project context, navigate to **Project Admin > Tools**.
2. Determine whether a **Tool** exists that represents a logical container for your desired source.
   For instance, if you are adding a Jenkins source, look for a tool representing the instance of Jenkins in question.
   1. If a tool exists already, click the tool’s title to edit the tool.
   2. If a tool does not exist, click **Add Tool**.

### Edit an Existing Build Source

1. To edit an existing build source, find the **Data Source** in the list of sources associated with the tool. 
   You can edit the display name or associate a different commit source for this build source. If you do not select a commit source, no associations will be drawn for the build activities coming from this build source. TeamForge displays a warning if a build source is not associated with a commit source. See [Manage Commit Sources][Orc_Management.html#commitsources].
2. Click **Update** to save your changes.
   {% include note.html content="While editing an existing source configuration, you can toggle a source from `Active` to `Inactive`, which will stop TeamForge from collecting data from that source; toggle back to `Active` to resume data collection from the source." %}

### Create a New Build Source

1. If this is a new tool, first select the **Tool Type** from the drop-down list. 
   For instance, if you’re adding a Jenkins tool instance, select **Jenkins**.
2. Select the **Include Traceability** check box. 
   A blank data source appears. If this is an existing tool with existing sources, click the **Data Source + (Add Source)** icon to add a new blank source.
   1. Provide a display name for the build source. This display name will help you differentiate the source in lists throughout the user interfaces. The display name can be up to 100 alphanumeric characters in length.
   2. Select a commit source. Select the commit source from the list of existing commit sources (or create a new one).
      {% capture cap1 %}
      {% include inline_image.html file="status-success-small.png" %} You must select a commit source from the list of existing commit sources to let TeamForge create associations between your build and commit activities.<br><br>
      {% include inline_image.html file="status-success-small.png" %} If you do not select a commit source, no associations will be drawn for the build activities coming from this build source. TeamForge displays a warning if a build source is not associated with a commit source. See [Manage Commit Sources][Orc_Management.html#commitsources] for more information about adding a commit source.<br><br>
      {% include inline_image.html file="status-success-small.png" %} For most source types, TeamForge generates a unique "source association key". The source association key uniquely identifies and helps route data from sources properly in TeamForge. You must supply this string while configuring adapters for most source types. You can copy the key by clicking on the small clipboard icon. No association key is necessary when you configure a TeamForge project code repository, though.
      {% endcapture %}
      {% include callout.html type="primary" content=cap1 %}
3. Click **Update**.
   
   TeamForge saves the new build source and activates it.


## Manage Review Sources {#reviewsources}

Add review sources to bring code reviews into the TeamForge project and traceability context.

Review sources bring code review data into EventQ for archival of meta data, participation in traceability, and activity reporting.

### Create or Find an Existing Tool to Group Your Review Source Under

1. From the desired project context, navigate to **Project Admin > Tools**.
2. Determine whether a tool exists that represents a logical container for your desired source. 
   For instance, if you are adding a Review Board source, look for a tool representing the instance of Review Board in question.
   1. If a tool exists already, click the tool’s title to edit the tool.
   2. If a tool does not exist, click **Add Tool**.

### Edit an Existing Review Source

1. To edit an existing review source, locate the **Data Source** in question on the **Edit Tool** screen. You can edit the display name or commit association prefix for this source.
2. Click **Update** to save your changes.
   
   {% include note.html content="While editing an existing source configuration, you can toggle a source from `Active` to `Inactive`, which will stop TeamForge from collecting data from that source; toggle back to `Active` to resume data collection from the source." %}

### Create a New Review Source

1. If this is a new tool, first select the **Tool Type** from the drop-down list. 
   For instance, if you’re adding a Review Board tool instance, select **Review Board**.
2. Select the **Include Traceability** check box. 
   A blank data source appears. If this is an existing tool with existing sources, click the **Data Source + (Add Source)** icon to add a new blank source.
   1. Provide a display name for the review source. This display name will help you differentiate the source in lists throughout the user interfaces. The display name can be up to 100 alphanumeric characters in length.
   2. Enter the Commit Association Prefix. This prefix is used to associate code commits with code reviews using the commit message. To associate a review with a code commit, you must enter the association prefix and review ID in the commit message in this format:
   ```shell
   [key:review_ID]
   ````
   Where key is any alphanumeric string. A commit association key may be up to 20 characters, including alphanumeric and underscore ("_") characters.
3. Click **Update**.
   
   TeamForge saves the new review source, and activates it.

## Manage Commit Sources {#commitsources}

Commit sources enable your external repositories to participate in traceability.

Commit sources bring commit data into TeamForge for archival of metadata, participation in traceability, and activity reporting.

{% include note.html content="TeamForge Project SCM repositories are added automatically as sources, both on upgrade and when new repositories are defined in the TeamForge project context." %}

### Create or Find an Existing Tool to Group Your Commit Source Under

1. From the desired project context, navigate to **Project Admin > Tools**.
2. Determine whether a tool exists that represents a logical container for your desired source.
   For instance, if you are adding a source to represent an external Git repository, look for a tool representing the Git server in question.
   1. If a tool exists already, click the tool’s title to edit the tool.
   2. If a tool does not exist, click **Add Tool**.

### Edit an Existing Commit Source

1. To edit an existing commit source, locate the **Data Source** in question on the **Edit Tool** screen. You can edit the display name for any commit source. Commit sources can be defined with one of two repository types:
   * **Project repositories**: housed within TeamForge projects.
   * **External repositories**: housed outside of TeamForge projects.
     
     {% include warning.html content="Once defined, you cannot switch the repository type. For external repositories, you can edit the repository URL. For project repositories, `Source Code view` permission is required and once selected and saved to a source, the project repository selection may not be altered. To work around this constraint, create a new source with a new repository and deactivate the old source." %}

2. Click **Update** to save your changes.

   {% include note.html content="While editing an existing source configuration, you can toggle a source from `Active` to `Inactive`, which will stop TeamForge from collecting data from that source; toggle back to `Active` to resume data collection from the source." %}

### Create a New Commit Source

1. If this is a new tool, first select the **Tool Type** from the drop-down list. 
   For instance, if you’re adding an external Git tool instance, select **External Git**.
2. Select the **Include Traceability** check box. A blank data source appears. If this is an existing tool with existing sources, click the **Data Source + (Add Source)** icon to add a new blank source.
   1. Provide a display name for the commit source. This display name will help you differentiate the source throughout the user interfaces where this source appears. The display name can be up to 100 alphanumeric characters in length.
   2. Select the repository type. Your source may be either a TeamForge project repository or an "external" repository.
      * **Project repositories**: housed within TeamForge projects.
      * **External repositories**: housed outside of TeamForge projects.
      {% include note.html content="Sources for Project repositories are created automatically.You need `Source Code View` permission to see available project repositories." %}
   3. For External repositories, enter your repository URL. This is likely the URI used to check out code or a WebDAV-enabled URL.
      * **For Subversion repositories**: run the `svn info` command inside the working copy and copy/paste the value of the "URL" field.
      * **For Git repositories**: run the `git remote show origin` inside the working tree and use the value of the "Fetch URL" field, without the "username@".

        For example, if your Subversion repository URL is set to https://forge.example.com/svn/repos/myproject, TeamForge EventQ collects messages from the "myproject" repository and all repositories under "myproject" such as https://forge.example.com/svn/repos/myproject/branches/mybranch.
3. Click **Update**.
   
   TeamForge saves the new commit source, and activates it.

   {% include note.html content="TeamForge EventQ displays all the defined sources for a step in the order in which they were defined." %}

## Manage Work Item Sources {#workitemsources}

Add work item sources to tickets, issues, defects and other work items to bring work items into the TeamForge project and traceability context.

Work item sources bring tracker data into TeamForge for archival of metadata, participation in traceability, and activity reporting.

{% include note.html content="TeamForge trackers are added automatically as sources, both on upgrade and when new trackers are defined in the TeamForge project context." %}

### Create or Find an Existing Tool to Group Your Work Item Source Under

1. From the desired project context, navigate to **Project Admin > Tools**.
2. Determine whether a tool exists that represents a logical container for your desired source.
   For instance, if you are adding a JIRA® source, look for a tool representing the instance of JIRA in question.
   1. If a tool exists already, click the tool’s title to edit the tool.
   2. If a tool does not exist, click **Add Tool**.

### Edit an Existing Work Item Source

1. To edit an existing work item source, locate the **Data Source** in question on the **Edit Tool** screen. You can edit the display name, while all other properties are system defined.

2. Click **Update** to save your changes.

   {% include note.html content="While editing an existing source configuration, you can toggle a source from `Active` to `Inactive`, which will stop TeamForge from collecting data from that source; toggle back to `Active` to resume data collection from the source." %}

### Create a New Work Item Source

1. If this is a new tool, first select the **Tool Type** from the drop-down list. 
   For instance, if you’re adding an external JIRA Tool instance, select the appropriate **Tool Type**.
2. Select the **Include Traceability** check box. A blank data source appears. If this is an existing tool with existing sources, click the **Data Source + (Add Source)** icon to add a new blank source.
   1. Provide a display name for the work item source. This display name will help you differentiate the source throughout the user interfaces where this source appears. The display name can be up to 100 alphanumeric characters in length.
3. Click **Update**.
   
   TeamForge EventQ saves the new work item source, and activates it.

## Manage XDS Sources {#xdssources}

Add Extensible Data Sources (XDS) to bring a wide variety of tools into the TeamForge project and traceability context.

XDS sources provide a means to integrate tools that do not fall under the stock activity classes (commit, build, review, and work item). You can add XDS sources to represent a wide range of tools and product domains.

### Create or Find an Existing Tool to Group Your XDS Source Under

1. From the desired project context, navigate to **Project Admin > Tools**.
2. Determine whether a tool exists that represents a logical container for your desired source. If you are adding a Chef™ source, look for a tool representing the Chef instance in question.
   1. If a tool exists already, click the tool’s title to edit the tool.
   2. If a tool does not exist, click **Add Tool**.

### Edit an Existing XDS Source

1. To edit an existing XDS source, locate the **Data Source** in question on the **Edit Tool** screen. You can edit the display name, look and feel, and tags. If you save an XDS source without defining the **Associated Source**, you may edit the XDS source later and add an **Associated Source**. Once the **Associated Source** has been defined it may not be altered.
2. Click **Update** to save your changes.

   {% include note.html content="While editing an existing source configuration, you can toggle a source from `Active` to `Inactive`, which will stop TeamForge from collecting data from that source; toggle back to `Active` to resume data collection from the source." %}

### Create a New XDS Source

1. If this is a new tool, first select the **Tool Type** from the drop-down list. 
   For instance, if you’re adding a Nexus tool instance, select the matching XDS Schema name from the drop-down list. Alternatively, select **Other** if no applicable choice exists yet.
2. Select the **Include Traceability** check box. A blank data source appears. If this is an existing tool with existing sources, click the **Data Source + (Add Source)** icon to add a new blank source.
   1. Provide a display name for the XDS source that is depicted on all TeamForge EventQ user interfaces. The display name can be up to 100 alphanumeric characters in length.
   2. Select an icon and set the icon background color to differentiate your source visually.
   3. Select an Associated Source.
      * Select a source from the list of existing sources. TeamForge EventQ associates activities from the XDS source to the selected source. For instance, if you want the XDS source in question to associate to builds from job XYZ, select the source corresponding to job XYZ in the **Associated Source** drop-down list.
      * If you do not select an associated source, no associations will be drawn to the activities coming from this XDS source.
   4. Add tags to the Source as a means to organize and categorize XDS Sources.
       Tags are particularly useful as filters for reporting via the Reporting API.

      {% include warning.html content="Tags are shared across the entire site. Exercise caution so that no superfluous tags are created which may make reporting more difficult." %}
3. Click **Update**.

   TeamForge EventQ saves the new custom source, and activates it.

{% include links.html %}