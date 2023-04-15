---
title: Project Templates - Install, Update, Enable and Disable
keywords: project, templates
tags: [installation, site_admin_tasks, upgrade, project_templates]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Apr 5, 2018
permalink: projecttemplates.html
summary: Provide sample projects to help users get started quickly. TeamForge comes with a sample template useful for agile development projects. Site administrators and project managers can use this template to jumpstart a project without a lot of manual setup steps.
---
Project templates are installed by default when you install TeamForge. TeamForge comes with a sample template useful for agile development projects. Site administrators and project managers can use this template to jumpstart a project without a lot of manual setup steps.

To install project templates using the TeamForge startup script, set the following tokens and restart the CollabNet services:

```shell
INSTALL_TEMPLATES=true    
REQUIRE_USER_PASSWORD_CHANGE=false 
````
{% capture tfsysadminnote %}
{% include inline_image.html file="status-success-small.png" %} If the project templates are already installed, you cannot re-install them using the TeamForge startup script. <br><br>
{% include inline_image.html file="status-success-small.png" %} You may choose to delete the sample project templates. After deleting the sample project templates, you must set the _INSTALL_TEMPLATES_ token to `false`. Otherwise, the project templates, if not found in the database, are installed automatically every time you restart the CollabNet services.
{% endcapture %}
{% include callout.html type="primary" content=tfsysadminnote %}

## Update a Project Template
To revise or correct an existing project template, overwrite it with a template of the same name.

* You must be a site administrator to overwrite an existing project template.
* Revise the project that will serve as the basis for the new project template.
  {% include tip.html content="You can disable a project template while you make changes to the project. To disable a project template, use the **My Workspace > Projects > Templates** page." %}

1. Select **PROJECT ADMIN** from the **Project Home** menu.
2. On the **Project Settings** page, click **Create Project Template**.
3. Select **Replace Existing Template** and choose the template you want to overwrite.
4. Provide the description for the template. (If you want to change the template name too, create a new template from the same project and disable the existing template.)
   {% include tip.html content="It's a good idea to use the description to note the changes from the previous version of the template." %}
5. Select the items you want to be available when new projects are created from this template.
6. The replacement project template is created. Its name and description appear on the **Template** tab of the **Projects** list, accessible from the navigation bar.

## Enable or Disable Project Templates
Site administrators or users with site-wide roles with project administration permissions can enable/disable project templates.

In TeamForge, enable a project template to make it available for use for creating new projects.

1. On **My Page**, click **Projects** and select the **PROJECT TEMPLATES** tab.
2. To make the project template available for use, select the template and click **Enable**.
3. To stop making the project template available for use, click **Disable**.
   {% include important.html content="You can create new projects only from the list of enabled project templates." %}
   * The Template Name field displays the name of the template using which the project was created. However, post upgrade to TeamForge 16.7 (or later), you will see the Template Name as "not available" for projects created in TeamForge 16.3 or earlier.
   * The Template Name field shows a hyphen (-) in cases where projects are created not from a template.
   * The template name is struck through in cases where the template used to create the project was deleted.
     {% include note.html content="Projects created using a template will now have the information about the template used for project creation." %}

<!-- Commenting out the following section about install-project-templates.py as the script has been deprecated per Hussain. -->
<!-- ## Install Project Templates Manually

In the TeamForge installation directory, run the `install-project-templates.py` script.

```shell
cd /opt/collabnet/teamforge/installer/
./install-project-templates.py -V
````

Use a site administrator user name and password. For a new site, both the user name and password are `admin`.

{% include tip.html content="On some servers, it may take a few seconds for the SOAP server to be ready after installation. If `install-project-templates.py` returns an error, wait briefly and then try running it again." %} -->


{% include links.html %}