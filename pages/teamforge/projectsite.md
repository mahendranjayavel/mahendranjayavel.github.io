---
title: Build Your Project Pages (Project Page Component, Publishing Repository)
keywords: build and assemble your project website
tags: [project_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Dec 27, 2017
permalink: projectsite.html
summary: Project members and other users need to know how to interact with your project. You can give them the information and tools they need by creating and maintaining a project website tailored to them. You can build your project home page from the ground up and assemble it from building blocks provided by TeamForge.
---

For quick, flexible site building, use the ready-made web page components that come with your TeamForge project site.

There are components for showing text, wiki pages, charts and graphs, and other purposes. These components make it easy to put together a sophisticated project site in little time.

## Create a Project Page

To provide information and functionality to people viewing your project, build one or more project pages.

1. Go to the page to which your new page will belong.
   {% include callout.html type="primary" content="Any project page can have sub-pages belonging to it. A page that belongs directly to the project home page is called a *top-level page*." %}
2. Click **Configure: On**.
3. Choose where your new page will fit in your project's structure.
   * To create a page just under the project home page, click **Add top-level page**. A top-level page's title is always visible in the navigation tree at left.
   * To create a page under the page you are on right now, click **Add sub-page**.
4. Give your new project page a title. Keep the title brief and descriptive.
5. Choose who can see this page.
   * Your choice will apply to all subpages that you create under this page.
   * To show this page to anyone with the necessary permissions, select Visible. For example, if you have defined a group of users who have access to your project, your new project page is visible only to those users. If your project is open to the public, anyone in the world can see it. Use this option when the information on this page is ready for a wide audience.
   * To show this page only to users with the project administrator role, select Hidden. Use this option if you are drafting content that you aren't ready to share yet, or want to share only with other project managers.
6. Click **Save**.
7. Click **Configure: Off**.

Now you are ready to build functionality into your project page with components such as text, news or tracker queries.


## Control Access to a Project Page

Before you put information or functionality on your project page, make sure it is accessible to the people it is intended for.

 {% include note.html content="This is only relevant if your page is not hidden. If you page is hidden, users who are not project administrators cannot see the page even if their role-based permissions would allow it." %}

1. Click **PROJECT ADMIN** from the **Project Home** menu.

2. On the **Project Settings** page, click **Permissions**.

3. Click the role to which you want to give access to your project page.

   {% include tip.html content="If the appropriate role does not exist, you must create it first." %}

4. On the **Edit Role** page, click **Project Pages**.

5. Under **Project Pages Permissions**, select the pages that users with this role can see and edit.

   * To enable users with this role to create, read, and modify all project pages, select the **Project Pages Admin** permission.

   * To allow users with this role to see pages but not edit them, select the appropriate page in the **View** section.

   * To allow users with this role to modify the contents of a text component project pages, select the appropriate pages in the **Edit Text Content** section.

   {% include note.html content="The project home page is always visible to any user who is authorzied to see the project." %}

## Reorder Project Pages

Facilitate your users' experience in your project by putting your project pages in an order that matches their needs.

1. Click **Configure: On**.

2. Select a project page and click **Edit Structure**.

3. Rearrange the structure of this page in any of these ways:

   * Select a page, and use **Cut** and **PastE** to place it in a different location.

     {% include note.html content="When you move a page, all of its sub-pages will also be moved." %}

   * Drag and drop a page to a different position.

   * Click **Add New Page** to add a sub-page to the current page.

   * Select one or more pages and click **Delete** to remove them.

4. Click **Save Changes**.

5. Click **Configure: Off**.


## Add Reports to a Project Page {#addreports}

Add one or more reports to your project home page to publish your project status to other project members. You can add only reports of type _Public_ to your project home page.

For more information about TeamForge reports, _Public_ and _Private_ reports, see [Reporting in TeamForge][\reports.html].

1. On the project page, click **Configure: On**.

2. Click **Add New Component**. The **Create Component** page appears.

3. Type a title for the report component.

4. Select **Reports** component type. A list of _Public_ reports for the project in context is shown.

5. Select **Visibility** and **Location**.

6. Select one or more _Public_ reports to add to the project page.

   * You can add up to thress reports per Reports component.

   * The _Public_ reports list may span over multiple pages if the number of reports exceeds **Page Size**. You can navigate through pages by clicking the page numbers at the bottom of the list.

   * However, you can change the **Page Size**.

     {% include image.html file="reports-page-size-dropdown.png" %}

7. If you would like to add reports from other project(s) of which you are a member, select the required project from the **Select Public Reports** drop-down list.

   {% include image.html file="selectpublicreportsforproject.png" %}

   The list of reports existing in the selected project is displayed from which you can select the relevant reports.

     {% include note.html content="Private reports and Table reports are not displayed in this list. You can add a maximum of three reports per Reports component." %}

8. Click **Save**.


The selected reports are added to the project page.


## Hide a Project Page

While you are preparing a project page, you may wish to keep it hidden.

You can hide a page from everyone except other project adminsitrators.

1. Click **Configure: On**.

2. Click **Edit Page Properties**.

3. For **Visibility**, select **Hidden** and click **Save**.

Now no one who does not have the Project Admin role can see the page, even if they have access to the project and to this page's parent page.

When you are finished building your page, don't forget to switch the page to "Visible" so that the intended users can see it.

## Rename a Project Page

As a page's focus evolves, it's a good idea to rename it to match its changing function.

1. Click **Configure: On**.

2. Click **Edit Page Properties**.

3. Change the **Title** as appropriate to its current function, and click **Save**.

4. Click **Configure: Off**.

## Create a Project Page Component {#createprojectpage}

Put information and resources in your users' hands with project page components.

For example, to let people know about important new developments, create a news component. To enable project members to find tracker items quickly, create a query component.

1. On the project page, click **Configure: On**.

2. Click **Add New Component**.

3. On the **Create Component** page, give your new component a title. Keep the title brief and descriptive.

4. Select one of the following component types that suits your need.

   * **Text** - Write free-form messages, reports or rants, in plain text or HTML.

   * **Reports** - Add various reports and charts to your project page.

   * **Documents** - Let project members exchange and review documents from the project page.

   * **Wiki PagE** - Open up your project page to two-way communication.

   * **Tracker Search Results** - Make saved search results available from the project page.

   * **Tracker Metrics** - Add charts about tracker metrics to your project page.

   * **Project News** - Maintain a journal or blog about your project, share information and make announcements.

   * **Project Statistics** - Show visual measures of your project activities on the project page.

   * **Subprojects** - Add a list of subprojects to your project page.

5. Choose who can see this component.

   * To show this component to anyone with the necessary permissions, select **Visible**.

   For example, if you have defined group of users who have access to trackers in your project, a query component will be visible only to those users. If your project's trackers are open to anyone, all users who view this project page will see the query component. Use this option when you are sure the component is ready for general use.

   * To keep this component under wraps until you are ready to show it, select **Hidden**.

   Now only users with the project administrator role can see this component. Use this option if you are drafting content that you aren't ready to share yet or want to share only with other project managers.

6. Select one of the locations, `Top of page` or `Bottom of page`, where the component shows up on the project page.

7. Depending on the component type you selected, set the properties of the component.

   <table>
     <tr><th>Component type</th><th>In the Properties of this component section...</th></tr>
    <tr><td><b>Text</b></td><td><ul><li>Type your free-form messages, rants or announcements in the text box.</li><li>Click <b>Save</b>.</li></ul></td></tr>

    <tr><td><b>Reports</b></td><td>For more information about adding reports, see <a href="projectsite.html#addreports">Add Reports to a Project Page</a> and <a href="reports.html">Reporting in TeamForge</a></td></tr>
    <tr><td><b>Documents</b></td><td><ul><li>Select a folder from the list to display its contents on the project page.</li><li>Click <b>Save</b>.</li></ul></td></tr>

    <tr><td><b>Wiki Page</b></td><td><ul><li>Type a title for the wiki page.</li><li>Click <b>Save</b>.</li></ul></td></tr>

    <tr><td><b>Tracker Search Results</b></td><td>Make sure one or more shared tracker searches are available to add to the project page. For more information about sharing saved tracker searches, see <a href="trackers-searchfortrackerartifacts.html#savedsearch">Share a Saved Tracker Search.</a><ul><li>Click <b>Add Saved Tracker Searches</b>.</li><li>Select one or more shared tracker searches from the <i>Select from Shared Tracker Searches</i> window.</li><li>Click <b>Add Selected</b>.</li><li>Select the number of rows of the search results to display from the <b>Display Rows</b> drop-down list.</li><li>Click <b>Save</b>.</li></ul></td></tr>    

    <tr><td><b>Tracker Metrics</b></td><td><ul><li>Select the number of charts from the drop-down list. You can add up to three tracker charts to your project page.</li>
   	<li>Select one of the chart types: <i>Burndown</i>, <i>Open by Priority</i> or <i>Open vs Closed</i>.</li>
    <li>Select a data source for your chart, a tracker or a planning folder.  </li>  
    <li>Click <b>Save</b>.</li></ul></td></tr>

    <tr><td><b>Subprojects</b></td><td><ul><li>Select the number of subprojects to be displayed on the project page.</li> 
    <li>Click <b>Save</b>.</li></ul></td></tr>

   </table>

## Edit a Project Page Component

You may want to make some changes to your project page component to make it more useful.

1. On the project page, click **Configure: On**.

2. In the title bar of the project page component you want to edit, click the edit icon {%  include inline_image.html file="editicon_component.png" %}.

3. Update the title as appropriate to its current functiona, if required.

4. Select the **Hidden** option for **VISIBILITY** to hide the page while you work on it. You can hide a page component from everyone except other project administrators.

5. Change the following settings depending upon the project page component that yor are editing.

   * For a _Sub-projects_ component, you can change the number of projects to be displayed.

   * For a **Documents** component, you can change the folder locaiton.

6. Click **Configure: Off**.

The project page component is displayed with modified content and/or settings.

## Reorder project page components

To make things easy for your project members, lay out your project components in a useful order.

1. On the project page, click **Configure: On**.

2. In the title bar of the project page component you want to move, click the up arrow {% include inline_image.html file="uparrow.png" %} or the down arrow {% include inline_image.html file="downarrow.png" %}.

3. Click **Configure: Off**.

## Hide a Project Page Component

While you are preparing a project page component, you may wish to keep it hidden.

You can hide a page component from everyone except other project administrators.

1. On the project page, clic =k **Configure: On**.

2. In the title bar of the project page component you want to hide, click the edit icon {% include inline_image.html file="editicon_component.png" %}

3. Select the **Hidden** option for **VISIBILITY**, and click **Save**.

4. Click **Configure: Off**.

Now no one who does have the Project Admin role can see the component, even if they have access to the project and to this page. Uses with the Project Admin role can see this component only when **Configure** is set to **On**.

## Rename a Project Page Component

As a page component's focus evolves, it's a good idea to rename it to match its changing function.

1. On the project page, click **Configure: On**.

2. In the title bar of the project page component you want to rename, click the edit button {% include inline_image.html file="editicon_component.png" %}.

3. Update the title as appropriate to its current function, and click **Save**.

4. Click **Configure: Off**.

## Delete a Project Page Component

When a component is no longer useful, remove it from the page to avoid distracting users.

1. On the project page, click **Configure: On**.

2. In the title bar of the project page component you want to delete, click the **Delete this Page** button.

3. Click **Configure: Off**.


## Create a Custom Project Home Page

To fully custom control your project website pages, build your own HTML and check it into the project's publishing repository. You can link to these pages as you would to any normal HTML page.

If you decide to hand-code your project hom page, the page works like any HTML page.

1. Click **PROJECT ADMIN** from the **Project Home** menu.

2. On the **Project Settings** page, select **Show custom web page** from **PROJECT HOME OPTIONS**.

   * **Show default project pages and components** is selected by default.

   * Site administrators can restrict public access to Publishing Repositories at the site level and you cannot view or modify **PROJECT HOME OPTIONS** in such case. See DISABLE_REMOTE_PUBLISHING site-options.conf variable for more information.

3. Add the `index.html` file to the `publishing/www` Subversion repository. The content of your index.html shows up immediately.

   {% include note.html content="When you switch to a hand-coded home page, you can still access any project pages you have created." %}

4. Click **Save**. Your cutome **Project Home** page is now active.

   {% include note.html content="If your project has any subprojects, the subprojects are also listed. To see them, make sure your `index.html` file exists and is in the right repository location." %}

## See What's in Your Publishing Repository

You can view the files in your TeamForge site's `publishing` repository through relative URLs.

For example:

 1. Endter the URL: `https://forge.collab.net/sf/projects/sampleproject/index.html` in the address bar to display contents of the `index.html` file. In this case, your `index.html` file must be in the `publishing` repository under the _www/sampleproject_ path. The contents of the `index.html` file are displayed in the **Project Home** page.

 2. Enter the URL: `https://forge.collab.net/sf/projects/sampleproject/roles/roledetails.html` in the address bar to display contents of the `roledetails.html` file. In this case, your `roledetails.html` file must be in the `publishing`repository under the _www/sampleproject/roles_ path. The contents of the `roledetails.html` file are displayed in the **Project Home** page.






  





{% include links.html %}