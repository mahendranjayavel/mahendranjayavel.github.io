---
title: Provision a Continuous Integration Server from a Lab Management Cloud
keywords: allow hosts from public clouds
tags: [project_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: provisionCIserver.html
last_updated: Feb 7, 2018
summary: The Lab Management Cloud plugin enables Hudson and Jenkins to automatically create slaves from Lab Management clouds.
---

## Install the Lab Management Cloud Plugin for Hudson and Jenkins

Get the plugin from **openCollabNet** and upload it using the **Plugin Manager**.

 1. Download the `labmanagement.hpi` file from **openCollabNet**. (Please check back later for availability.)

 2. In the Hudson or Jenkins Plugin Manager page, click the _Advanced_ tab.

 3. In the Upload Plugin section, browse to the location where you saved the `.hpi` file and click **Upload**.


In the Plugin Manager's _Installed_ tab, you should see the Lab Management Cloud plugin enabled.


## Configure the Lab Management Cloud Plugin for Hudson and Jenkins

When you add a new cloud, you set up templates specifying details such as the host type and profile for the nodes that will be provisioned from this cloud.

 1. In the Cloud section of the Hudson or Jenkins configuration page, click **Add a new cloud** and select **CollabNet Lab Management**.

    Lab Management options are displayed. Here's an example:

    {% include image.html file="lm_configurehudsonplugin.png" %}

 2. Enter the URL of the Lab Management Manager node. For example, https://mgr.cloud.sp.collab.net/.

 3. Provide the user name and password. This user must have access to the Lab Management project where new hosts will be allocated.

 4. Enter the user's API key for the Lab Management web service.

    {% include tip.html content="Copy and paste the key from the user's Lab Management home page." %}

 5. Click **Test Connection** to make sure that the options you provided are valid.

 6. Specify the Lab Management project where new hosts will be added.

 7. Select a Cloud from which new hosts will be allocated. You can find the list of valid cloud names in the Lab Management Manager interface. For example:

    {% include image.html file="lm_cloudlist.png" %}

 8. Click **Add Template** to create a template that Hudson will start.

    1. Specify a name that characterizes the template. The **name** is used to identify the template and is displayed in various parts of the Hudson interface.

    2. For **Host Type**, select the type of hardware you want for the node.

    3. For **Size**, select the amount of resources -- memory, CPU, and disk -- assigned to this template. You can find the exact amount of resources for each size in the Lab Management Manager's **Clouds > Allocate From Cloud** page. For example:

       {% include image.html file="lm_cloudallocate.png" %}

    4. For **Profile**, select the Lab Management profile to be used for the template.

    5. Provide a list of **labels** separated by white spaces.

       {% include note.html content="The names and labels you provide for the templates are used to specify which jobs will use this cloud." %}

    6. Enter a value for **# of Executors**. This controls the number of concurrent builds that Hudson or Jenkins can perform. So the value affects the overall system load that might be incurred. A good value to start with is the number of processors on your system.

       When using Hudson or Jenkins in the master/slave mode, setting this value to 0 would prevent the master from doing any building on its own. Slaves may not have zero executors, but may be temporarily disabled using the button on the slave's status page.

 9. Click **Save**.

In the **Manage Nodes** page, you'll see an option to provision a node from Lab Management.

 {% include image.html file="lm_configurehudsonplugin1.png" %}

## Run a Hudson or Jenkins Job on a Host Provisioned from Lab Management Cloud

When you run a job on a host provisioned from a Lab Management cloud, use a template you defined earlier.

 1. In the Hudson or Jenkins configuration page for the job, provide a name and description.

 2. Select the **Restrict where this project can be run** option to tie the job to the Lab Management cloud.

 3. Enter a label expression. To always run this job on a specific node, just specify its name. However, when several nodes could be available and you don't want to tie the job to a specific one, enter an expression based on the name and label values of a Lab Management cloud template you configured earlier.

    {% include image.html file="lm_configurejob1.png" %}

 4. Specify any other options you want and click **Save**.

 When a node is no longer used, it will be brought down and released.




{% include links.html %}
