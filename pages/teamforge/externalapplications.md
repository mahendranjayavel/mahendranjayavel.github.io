---
title: Integrate or Link External Applications
keywords: integartions, linked applications
tags: [site_admin_tasks, integration, authentication]
sidebar: teamforge_sidebar
permalink: externalapplications.html
last_updated: Mar 15, 2018
summary: If your site's users need access to an application or web site that is not part of TeamForge, you can make it available by linking or integrating from within your TeamForge site.
---
## What is a linked application?
A linked application is an external application or site that users can get to from inside a TeamForge project.

You can use linked applications to incorporate these types of applications into your TeamForge project:

* Third party applications
* Internally developed applications
* Integrations developed using the TeamForge SOAP APIs
* Company intranet sites
* External websites

After you create a linked application, a button is added to your project navigation bar. Clicking the button displays the linked application in the main TeamForge project window (or in the case of a site-wide linked application, in a separate window).

{% include note.html content="You can create as many linked applications per project as you wish. However, because each linked application adds a button to the project navigation bar, creating a large number of linked applications can cause horizontal scrolling." %}

TeamForge administrators can also create site-wide linked applications that appear in all TeamForge projects.

## Create or Edit Linked Applications {#linkedapps}

To bring an external tool into your environment quickly and easily, set it up as a linked application. When you create a site-wide linked application, it appears in all projects on your TeamForge site. Site-wide linked applications are especially useful for incorporating corporate standard external applications, such as a company intranet sites, into your TeamForge installation.

### Create a Site-wide Linked Application {#sitewidelinkedapp}

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **INTEGRATIONS > SITE-WIDE LINKED APPLICATIONS**.
3. Click **Create**.
4. On the **Create Site-wide Linked Application** page, provide a name for the linked application. This name appears on the link in the TeamForge navigation bar.
5. Enter the server location or URL for the linked application.
6. Select whether you want to enable single sign-on for the linked application.
   * If you use single sign-on, access to the linked application is managed through the TeamForge authentication system. Users are not required to log into the linked application after they have logged into TeamForge.
   * If you do not use single sign-on, users will be required to log in to the linked application using its native authentication system.
7. Choose how you want the linked application to appear when a user clicks it.
   * **In the same window**: The linked application takes over the entire browser window, replacing whatever the user was looking at.
   * **In a new window**: The linked application launches in a separate browser window.
   * **In an iframe**: The linked application appears in a box in the same window, framed by the TeamForge site's header and navigation controls.
8. Click **Save**.
   
   A link for the site-wide linked application is added to your TeamForge navigation bar. Clicking the link displays the application in the main TeamForge window.

### Edit a Site-wide Linked Application

When the use patterns of a linked application change, you may need to change the way the application integrates with TeamForge.

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **INTEGRATIONS > SITE-WIDE LINKED APPLICATIONS**.
3. Click the name of the site-wide linked application that you want to edit.
4. On the Edit Site-wide Linked Application page, make the changes you need. You can edit these elements:
   * The name of the application.
   * The application's URL.
   * Whether the application uses single sign-on.
   * Whether the application is displayed in a new window, in the same window, or in an IFrame.
     {% include note.html content="You cannot change the application icon." %}
5. Click **Save**.

## What is an integrated application?
An integrated application is a stand-alone application that can seamlessly integrate into any TeamForge project.

You can use integrated applications to incorporate these types of applications into your TeamForge project:

* Third party applications
* Internally developed applications
* Integrations developed using the TeamForge SOAP APIs
* External websites

When you add an integrated application to your project, an icon is added to your project navigation bar. Clicking the icon displays the integrated application in the main TeamForge project window.

TeamForge site-administrators can register site-wide integrated applications that project administrators can opt to use across projects.

Site administrators or users with site-wide roles with the administration permissions for integrated applications can enable/disable integrated applications.

{% include tip.html content="Disabling an integrated application restricts it from being added to projects. However, disabling an integrated application does not affect the projects where the integrated application might already be in use." %}

After your site administrator registers an integrated application on the site level, on adding it to your project, an icon is added to your project navigation bar. Clicking the icon displays the integrated application in the main TeamForge project window.

{% include note.html content="You can register and integrate as many applications per project as you wish. However, because each integrated application adds an icon to the project navigation bar, creating a large number of integrated applications can cause horizontal scrolling." %}

## Create Integrated Applications {#integratedapps}

To make a tool comprehensively available to your users, set it up as an integrated application. 

Before you can make an integrated application available to Project Administrators, your system administrator must integrate the application with your site. This may involve modifying the application. How this is done depends in part on the application.

### Integrate an External Application into a TeamForge Site
When you integrate an external application into your TeamForge site, your site's project administrators can choose to include the integrated application alongside the built-in tools in their projects.

When you have integrated the application, project administrators on your site can add it to their set of collaboration tools. Objects they create will share the core TeamForge features, such as authorization, authentication, go-urls, association, linkification, templating, Project Pages components, search, and source code management support.

1. Find the XML files that describes your integrated application.
2. Log into TeamForge as an admin user.
3. Go to **My Workspace > Admin**.
4. Click **INTEGRATED APPS** from the **Projects** menu.
5. Click **Create**.
6. Use the **Browse** window to find the configuration file you created, then click **Next**.
7. On the **Preview** page, review the parameters you set in the configuration file.
   {% include note.html content="You may have to revise one or more values to ensure they are valid." %}
8. Click **Save**.

The application is now available for all projects on your site. You can direct project administrators to these instructions to add it to their own project toolbars.

### Enable or Disable Integrated Applications
Site administrators can enable or disable integrated applications.

In TeamForge, enable an integrated application to make it available for use in the projects.
{% include tip.html content="You can also disable an integrated application to restrict it from being added to projects." %}
1. Go to **My Workspace > Admin**.
2. Click **INTEGRATED APPS** from the **Projects** menu.
3. To make the integrated application available for use, select the integrated application and click **Enable**.
4. To stop making the integrated application available for use, click **Disable**. The system asks for confirmation before disabling an integrated application. Click **OK** to disable the integrated application.
   
   A disabled integrated application can be re-enabled when there is a need to use that integrated application in a project.

### Remove a Tool (Integrated Application) from Project Admin Menu
To stop making an application or site outside of TeamForge available to your users from inside your TeamForge projects seamlessly, disintegrate an application.

{% include note.html content="You may have integrated several external applications per project to maximize the integrated applications feature's utility. However, because each integrated application adds an icon to the project navigation bar, a large number of integrated applications can cause horizontal scrolling. Consider removing the integrated applications that are not in use." %}
1. Click **PROJECT ADMIN** from the **Project Home** menu.
2. On the **Project Admin Menu**, click **Tools**.
3. To remove an integrated application from the list of tools displayed , clear the **Visible** check box and click **Save**. The selected integrated application is removed from the project.
   The icon of the removed integrated application disappears from your **Project Home** menu.

   {% include note.html content="Removing an integrated application, removes all associations to the integrated application too. Removing an integrated application, removes the component type in the **Project Home** **Create Component** page." %}

### Set Site-level Permissions for an Integrated Application
In TeamForge, as the site administrator you can set the site-level permissions for an integrated application.

The default access permissions are usually set using the configuring xml file for each integrated application. However, you may want to provide permission access at site-level for some of the users.
1. Go to **My Workspace > Admin**.
2. Click **INTEGRATED APPS** from the **Projects** menu.
3. Set the permissions for the integrated application and click **Submit**. The permissions are set for the selected integrated application.
   It is possible that an integrated application may be added to a project by a restricted user whose project administration permissions come from a global project role. In such a case, you could be left with no one authorized to administrate the integrated application. TeamForge handles that situation in one of two ways:
   * If one or more users with the "Founder project administrator" role is a member of the project, then the restricted user who did the integration gets that role too.
   * If there is no project member with the "Founder project administrator" role, the restricted user who did the integration gets a new administrator role called "\<integrated_application_name> Administrator."

### View Integrated Application Information
TeamForge site administrators, and users with site-wide roles and the IAF permission, can view information about an integrated application's configuration and other details.

1. Go to **My Workspace > Admin**.
2. Click **INTEGRATED APPS** from the **Projects** menu.
3. Click the name of the integrated application that you want to view. The default category tab, **GENERIC**, displays all the existing integrated applications associated with the site. You can have your integrated application displayed under a separate **CATEGORY** tab by defining it in the deployment configuration file.
   
   The configuration details of the integrated application are displayed.

### Edit an Integrated Application {#editanintegratedapplication}
TeamForge site administrators can update an integrated application's URLs (SOAP endpoint URL, administration URL, browser URL) and other parameters by uploading XML files containing the changes.

1. Go to **My Workspace > Admin**.
2. Click **INTEGRATED APPS** from the **Projects** menu.
3. Select the integrated application you want to edit.
4. Click **Edit**.
5. On the **Edit Integrated Application** page, make the changes you need. You can edit these elements:
   * The Deployment Configuration File.
   * The Application Configuration File.
6. Click **Browse** and select the files to attach.
7. Click **Next**.

### Export an Integrated Application
TeamForge site administrators can export an integrated application's variables in XML format and have them available for editing.

1. Go to **My Workspace > Admin**.
2. Click **INTEGRATED APPS** from the **Projects** menu.
3. To export the integrated application, select the integrated application name.
4. From the **View Integrated Application** page, click **Export**.
   
   The integrated application is exported.

{% include links.html %}