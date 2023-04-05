---
title: Integrate or Link External Applications to Projects
keywords: integartions, linked, applications, remove, link, external, add, tool, delete, tools, gourl, prefix, Go URLs, export
tags: [ctf_20.0, project_admin_tasks, integration, projects, authentication]
sidebar: teamforge_sidebar
folder: teamforge
permalink: externalapplicationsforprojects.html
last_updated: Dec 11, 2019
summary: You can make it easy for project members to use a wide variety of applications and sites from within TeamForge.
---

## Link an External Application

To make an application or site outside of Digital.ai TeamForge available in your project, create a linked application.

You can create as many linked applications per project as you need.

 {% include tip.html content="Some sites employ page code that disables this feature. For example, some Google apps automatically generate user login data and append it to their URLs, which prevents them from opening in an iFrame." %}

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Tools**. A list of all the applications in the project is displayed on the **Project Tools** section.

 3. Click **Add Tool**.

 4. On the **Add Tool** page, select the tool type as **Linked Application**. 

 5. Enter a name for the linked application. 

 6. Select **Show in Toolbar** check box.

    1. Enter the server location or URL for the linked application.

    2. Select the option in which the link should be opened.

    3. If you are a TeamForge administrator, select whether you want to use single sign on for the linked application.

       * By default, only site administrators can edit (turn on/off) single sign on (SSO) for linked applications. However, you can set the site options token ONLY_SITE_ADMIN_CAN_EDIT_SINGLE_SIGN_ON to `false` to have both site and project administrators turn SSO on and off. For more information, see [ONLY_SITE_ADMIN_CAN_EDIT_SINGLE_SIGN_ON][siteoptiontokens.html#sasinglesignon].

       * If you use single sign on, TeamForge users can automatically log into the linked application.

       * If you do not use single sign on, users must log into the linked application using its native authentication system.

    4. Click **Choose File** and select a `.gif`, `.jpg`, or `.png` file to serve as the new icon for the linked application.   Make the image 25 pixels wide and 20 pixels high. This icon appears with the application name in the **Project Home**   menu.

 7. Click **Save**.

 Now the linked application with the selected icon is shown in the **Project Home** menu. Click the respective linked application to open it on the same window or another window or in an IFrame as already defined.

## Edit a Linked External Application {#editlinkedexternalapp}

When the use patterns of a linked application change, you may need to change the way the application integrates with Digital.ai TeamForge.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. From the list of applications, click the application you want to edit. The **Edit Tool** page is displayed.

 3. Edit the name of the linked application, if required.

 4. Edit the linked application URL, if required.

 5. Enable or disable single sign on for the linked application. By default, only site administrators can edit (turn on/off) single sign on (SSO) for linked applications. However, you can set the site options token ONLY_SITE_ADMIN_CAN_EDIT_SINGLE_SIGN_ON to `false` to have both site and project administrators turn SSO on and off. For more information, see [ONLY_SITE_ADMIN_CAN_EDIT_SINGLE_SIGN_ON][siteoptiontokens.html#sasinglesignon].

 6. Click **Choose File** and select a `.gif`, `.jpg`, or `.png` file to serve as the new icon for the linked application.   Make the image 25 pixels wide and 20 pixels high. This icon appears with the application name in the **Project Home**   menu.

 7. Click **Update**.

## Integrate an External Application into Your Project {#integrateexternalapp}

To make an application or site outside of TeamForge available to your users seamlessly from inside your TeamForge project, bring it in as an integrated application.

If the application you want to use is not yet available for your project, ask your site administrator to set it up.

You can use as many integrated applications as you wish, after your site administrator has made them available.

 1. Click **PROJECT ADMIN** from the **Project Home** menu.

 2. On the **Project Admin Menu**, click **Tools**. The **Project Tools** section displays the list of all the current applications in the project.

 3. Click **Add Tool**.

 4. On the **Add New Tool** page, select the desired application. All the relevant paramters to configure the tool are displayed.

    1. If your site administrator has made it possible, specify a prefix for the resources created by the application you are setting up. A prefix enables TeamForge to provide handy links between objects managed by this application and other TeamForge objects. For example, if you are bringing in a blogging application:

       * You can connect a blog post with a TeamForge artifact using a special link called an "association."

       * For each blog post, you can give readers a simplified address, known as a "go URL."

       {% include note.html content="For project-level associations and go URLs the application's prefix is permanent after you save it." %}

    2. Set any other configuration parameters you need and save your changes.

       * Click **Save** to return to the Project Tools page.

An icon for the integrated application is added to your **Project Home** menu. Clicking it launches the application in the main TeamForge project window.

## How is an integrated application described? {#describeintegratedapp}

An integrated application is described using two XML files - a deployment configuration file and an application configuration file - that provide information to TeamForge about the configuration options exposed by the application.

In TeamForge version 6.1.1 and later, you have the ability to configure some integrated application settings using the user interface. You can also export these settings in XML format and make changes. To edit configuration settings, you would upload the XML file containing the updates.

**Integrated application settings**

 {% include note.html content="Some of the tags are internationalized so that the application will display languages based on the browser locale. See [Internationalize Your Integrated Application][languagelocalization] for more information." %}

**\<name\>**
This is the title of the integrated application. When the integrated application is added to a project, the button that appears on the project pages has this name. This name must be unique -- you cannot use it for any other integrated application on the same TeamForge server.

This tag is used in both deployment and application configuration files.

**\<adminurl\>**

When an application has an administration screen for configuring its parameters, this field contains that URL. It is optional.

This tag is used in the deployment configuration file.

**\<baseurl\>**

This is the URL to which a user will be directed on clicking the integrated application button in a project. 

This tag is used in the deployment configuration file.

**\<endpoint\>**

This is the SOAP endpoint for the integrated application. The endpoint contains the various methods exposed by the integrated application that are called during the lifecycle of TeamForge.

This tag is used in the deployment configuration file.

**\<gourl\>**

This indicates which URL must be used when an object id for an integrated application is specified (either via `Jump_to_id` or on the URL as `/sf/go/<objectid>`). This URL can support a couple of dynamic parameters.

 * %o - The object id entered by the user will be dynamically replaced here.

 * %p - The project id for the object entered will be dynamically replaced here.

For example, if the Go URL is http://go.tourl.com/tracking?id=%o and the object ID entered is XYZ123, then the URL will be replaced and redirected to http://go.tourl.com/tracking?id=XYZ123.

This tag is used in the deployment configuration file.

**\<category\>**

This is used to display the integrated application under a separate _Category_ tab. It is an optional parameter that is manually inserted based on the requirement. If the category is not defined, the integrated application appears under the _Generic_ tab.

This tag is used in the deployment configuration file.

**\<isbaseapp\>**

This validates whether the integrated application is a base application configured for the specified category. It is an optional parameter that is manually inserted based on the requirement.

This tag is used in the deployment configuration file.

**\<is-search-supported\>**

This validates whether the integrated application needs to be displayed as an object category in the drop-down list for search options in TeamForge such as **Jump to ID** and **Advanced Search**. It is an optional parameter that is manually inserted based on the requirement.

This tag is used in the application configuration file.

**\<config-parameters\>**

There can be any number of configuration parameters for an integrated application and they are displayed when associating the application to a project. These parameters are filled in by the project administrator and are available in the integrated application SOAP interface as configuration parameters. The integrated application gets a chance to validate these parameters and indicate back to TeamForge whether this project association is successful by passing in a "TRUE". It can return a "FALSE" if it doesn’t want this project association to succeed. Each configuration parameter is placed inside the "param" tag, which can contain multiple elements to describe the parameter.

 * **\<title\>**

   The internationalized title that appears for a project administrator to fill in while associating the integrated application to a project.

 * **\<name\>**

   The Java variable under which the value for this parameter will be available on the integrated application.

 * **\<description\>**

   The internationalized description that appears when a project administrator fills in or enters a configuration parameter.

 * **\<default value\>**

   The default value for the parameter that will appear in the user interface during the association of an integrated application to a project.

 * **\<display type\>**

   This is the type of display control used for the configuration parameter. We support "TEXT" for text fields, "CHECKBOX" for checkbox type controls, "RADIO" for radio buttons, and "SELECT" for select dropdowns. This field can also take an attribute that says what the value type for the field should be -- whether it should be an "Integer", "String" and so on. So if the field is expecting numbers, then entering "foo" as a value will throw a validation failure.

 * **\<option\>**

   If the display type is "RADIO" or "SELECT", then these fields contain the individual options available for the display controls. This will contain a "name" attribute that will be sent to the integrated application when that option is selected from the UI. The value of this option should be an internationalized field as it is the value visible to the user.

 * **\<editable\>**

   This specifies whether the configuration parameter should be editable once the integrated application is associated to a project. These configuration parameters are available when you add or edit an integrated project. If a parameter should not be "edited" post association, setting this to "false" will make it non-editable.

This tag is used in the application configuration file.

**\<description\>**

This is an internationalized string for the integrated application's description. It contains information for TeamForge project and site administrators to know what the application does.

This tag is used in the application configuration file.

**\<id-pattern\>**

When trying to link to an integrated application id, this regular expression gets used for mapping. By default (if no value is provided), it looks for alphanumerical characters; in case you need specific characters to be matched (for example, JIRA, which has hyphens in ids), this value is used.

This tag is used in the application configuration file.

**\<page-component\>**

These settings are used for Project Content Editors. The integrated application content can become part of the standard Page Component data that appears in project home pages. The settings indicate the type of information that will be available from the integration application.

 * **\<input-type\>**

   This is the input type control for an integrated app Page Component. We only support 2 types now. Either "select" so that the inputs can be shown from a "SELECT" dropdown and the users will be able to pick a value from there. Else, it can be a "text" where a simple "text" field will be entered for taking the user input.

 * **\<result-format\>**

   This is the format in which the output of Page Component is returned. This can be a "list" which indicates that it will be a Table like output. The integrated app will send the results in an XML format and the Integrated app framework converts this into a list of records. The other option is "html", where the output from the Integrated application is just displayed on the screen.

 * **\<page-component-description\>**

   The description that will appear when you add an Integrated application Page Component (Link to the page where " Add component" is available)

 * **\<page-component-title\>**

   The title that will appear when adding an Integrated application Page Component (Link to the page where "PCE Add component" is available)

This tag is used in the application configuration file.

**\<permissions\>**

This is a collection of permissions that are exposed by the integrated application. There could be any number of such permissions. These permissions will appear as a part of the project's roles (existing ones, as well as ones newly added) and can be assigned along with other tool permissions. You can map one of these permissions with a "dapMappedTo" attribute -- this indicates the permission to be used when a user logs in without authentication (for example, for public projects). Typically, this is the permission to read data so that it doesn’t need a login name; it varies from one application to another.

This tag is used in the application configuration file.

**\<prefix\>**

If the "require-per-project-prefix" attribute is false, the value of this tag is used for identifying the integrated application in Go URLs, associations, and linkifications. If the "require-per-project-prefix" attribute is true, the value is used only for the "Host" project. Each project must fill in its value as part of adding the integrated application. Click [here][externalapplicationsforprojects.html#integrateexternalapp] for steps to add integrated applications to a project.

This tag is used in the application configuration file. The prefix can contain alpha-numeric characters and cannot be more than six characters in length. For more information about prefix, see [How does an integrated application interact with other TeamForge tools?][externalapplicationsforprojects.html#integratedappinteractionwithTF]

**\<require-per-project-prefix\>**

An integrated application can indicate to TeamForge whether the object ids that it generates are uniquely identifiable across the entire application (if yes, the value for the attribute is "false") or whether they need to be project-specific (in this case, the value for the attribute is "true"). If an integrated application needs per-project prefix, you must enter the prefix value when the integrated application is added to a project.

This tag is used in the application configuration file.

**\<require-scm-integration\>**

This indicates whether SCM commits need to be vaildated. Some applications might have business rules which indicate that a commit can be made only if certain conditions are met. If the integrated application has any such rules, the value for the attribute should be "true". There are also a couple of methods to be implemented in the SOAP endpoint.

This tag is used in the application configuration file.

**\<require-page-component\>**

Some integrated applications choose not to expose details as Page Components. For those that don’t, set this tag to "false" and for those that do, set it to "true". If the value is "true", you must provide the "page-component-details" tags as well.

This tag is used in the application configuration file.

**\<servicetype\>**

TeamForge 6.1.0 and earlier releases supported only SOAP as the mechanism to talk from TeamForge to the integrated application. TeamForge 6.1.1 and later support REST calls. The servicetype tag indicates whether the protocol used for communication is REST or SOAP.

This tag is used in the deployment configuration file.

For examples of how these tags are used in the integration of the Pebble bogging application, see [pebble-dep.xml][pebble-dep-xml] and [pebble-app.xml][pebble-app-xml].

{% capture integratedappsnote %}
{% include inline_image.html file="status-success-small.png" %} The associations between Digital.ai TeamForge and an integrated application can be created only from Digital.ai TeamForge to the integrated application and not vice-versa. <br><br>
{% include inline_image.html file="status-success-small.png" %} To associate an object in an integrated application from within Digital.ai TeamForge, use the `[<prefix_objectid>]` format. Successful associations appear hyperlinked. <br><br>
{% include inline_image.html file="status-success-small.png" %} Each integrated application displays its prefix on moving the mouse over the application name in the tool bar.
{% endcapture %}
{% include callout.html type="primary" content=integratedappsnote %}

## How does an integrated application interact with other TeamForge tools? {#integratedappinteractionwithTF}

When you integrate an external application into your TeamForge site, the application can take full advantage of object IDs, links and Go URLs.

To look at how this works, we'll use the Pebble application as an example. Pebble is a blogging tool that you can quickly integrate with TeamForge.

### Object IDs

Integrated application object IDs are of the form "prefix_objectId". Object IDs uniquely identify a TeamForge object so that you can access and use it in different contexts. For example, to get to artifact `artf1234` quickly, you just enter `artf1234` in the Jump To ID box. In the Pebble tutorial application, the date of a blog post, in YYYYMMDD format, is used as the object ID.

A prefix is an alphanumeric string attached to the beginning of an object ID that TeamForge uses to manage object IDs from different tools. For example, in the Pebble app, `<prefix>_20100601` gets you a page showing all the blog posts in the project that were published on June 1, 2010.

In an object ID such as "prefix_objectId", the "prefix" is case-insensitive, whereas the "objectId" is case-sensitive. For example, the two object IDs, "PT_SC1" and "pt_SC1", refer to the same object in TeamForge. Whereas, the two object IDs, "PT_SC1" and "PT_sc1", refer to two different objects in TeamForge. Here, `PT` and `pt` are case-insensitive and the `SC1` and `sc1` are case-sensitive.

The prefix can either be the one specified when an integrated application is added to a project by project administrator, or the one in the XML Application configuration file depending on the "require-per-project-prefix" setting. The "require-per-project-prefix" setting can be true or false. If it is false, each project integration would not need to provide a project prefix; so the one provided in the XML application configuration file takes effect. If the "require-per-project-prefix" setting is true, a prefix needs to be provided by the user during every project association.

The amount of information the prefix carries depends on the kind of application you are integrating into your TeamForge site.

 * With applications that use object IDs, such as Project Tracker and JIRA, you can identify the project that the object belongs to from its object ID.

 * For applications that don't have uniquely identified objects, or don't have the notion of "project," such as MoinMoin or Review Board, you can choose a prefix that's specific to the project where the integrated tool is used.

#### Setting up Multiple Prefixes for Integrated Applications

At times, you may want to use more than one prefix for integrated applications. It is possible to have multiple prefixes set up for integrated applications. You must have the prefixes, separated by commas, included in the XML application configuration file and upload the file to your TeamForge site. For more information about uploading the application configuration file, see [Edit an integrated application][externalapplications.html#editanintegratedapplication].

Consider the following while setting up multiple prefixes for an integrated application:

 * Prefixes, once set up using the XML application configuration file, cannot be modified.

 * A prefix can be up to six alpha-numeric characters in length. However, the combined length of all the prefixes cannot exceed 128 alpha-numeric characters.

 * The "require-per-project-prefix" must be set to `false` in the application configuration file. In case it is set to true, an error message appears when you upload the application configuration file.

 * Do not use existing prefixes. You cannot upload an application configuration file consisting of one or more prefixes already in use in TeamForge.

### Go URLs

Go URLs allow a user to get to a particular object ID with a short, handy URL. To use this for Pebble, construct a URL like this: `https://mysite.com/sf/go/<prefix>_<date in format YYYYMMDD>`.

For example, if the Pebble tool in your project has the prefix PA, and you want to send someone all the blog posts published on app June 1, 2010, send them this link: https://mysite.com/sf/go/PA_20100601.

### Associations

The object ID can be used to associate objects with other TeamForge objects. For example, if you want to associate a document with the blogs published on June 1, 2010, go to the document's _Associations_ tab and add an association to `PA_20100601` as the object ID.

### Automatic Links

When you type text of the format `<prefix> _<date in YYYYMMDDD>` in any TeamForge text field, the text is converted to a link. When you click the link you see the blog posts for that date, if any.

## Export an Integrated Application

TeamForge site administrators can export an integrated application's variables in XML format and have them available for editing.

 1. Go to **My Workspace > Admin**.

 2. Click **INTEGRATED APPS** from the **Projects** menu.

 3. To export the integrated application, select the integrated application name.

 4. From the **View Integrated Application** page, click **Export**.


## Hide / Remove a Linked or Integrated Application from a Project

To stop making an application or site outside of TeamForge available to your users from inside your TeamForge projects seamlessly, hide or disintegrate an application.

{% include note.html content="You may have integrated several external applications per project to maximize the integrated applications feature's utility. However, because each integrated application adds an icon to the project navigation bar, a large number of integrated applications can cause horizontal scrolling. Consider removing the linked or integrated applications that are not in use." %}

1. Click **PROJECT ADMIN** from the **Project Home** menu.

2. On the **Project Admin Menu**, click **Tools**.

3. To hide an integrated application from the list of tools displayed, clear the **Visible** check box and click **Save**. The selected integrated application is hidden for the project. The icon of the hidden linked or integrated application disappears from your **Project Home** menu.

   {% include warning.html content="Hiding a linked or integrated application, hides all associations to the application too. It also hides the component type in the Project Home's **Create Component** page." %}

4. You can also click the **Delete** icon ( {% include inline_image.html file="deleteicon.png" %} ) to delete a linked or integrated application permanently from your project.
   
   {% include warning.html content="Deleting an integrated application (such as Review Board or Binaries) means a permanent removal of the application including all related integrated application data from your project. Exercise caution before deleting an integrated application. For example, deleting Review Board from a project will delete any and all review requests, reviews, diffs, or other data associated with the Subversion repositories in the project." %}
 


{% include links.html %}