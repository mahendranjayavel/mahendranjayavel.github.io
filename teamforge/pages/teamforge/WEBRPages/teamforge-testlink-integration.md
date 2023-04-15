---
title: TeamForge—TestLink Integration Using the TeamForge Webhooks-based Event Broker
keywords: webhooks, event broker
tags: [ctf_20.1, ctf_20.0, ctf_19.3, ctf_19.2, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: teamforge-testlink-integration.html
last_updated: Feb 16, 2020
summary: TeamForge's native Webhooks-based Event Broker replaces EventQ as the default event broker to support TeamForge integration with TestLink. EventQ-based TeamForge—Testlink integration is no longer supported.
---

TestLink is a web-based Test Management system that supports all the various components and processes involved in a testing process. Using TestLink, you can create test specifications, execute test cases, create custom reports, generate test plan metrics and so on.

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">

Before you begin with the installation and the configuration of the TeamForge—TestLink integration plugin, generate the TeamForge Webhook URL by running the [`create_webhook_event.py`][create_webhook_event_py] script. 

</div>
</div>

## TeamForge—TestLink Integration Overview {#testlinkoverview}

The TestLink integration plugin, `collabnet-testlink-1.0.5.tar`, if installed and configured, can notify the native TeamForge Webhooks-based Event Broker about the test cases and the test execution results.

The TeamForge—TestLink integration plugin, `collabnet-testlink-1.0.5.tar`, works only with the TestLink versions {{site.data.identifiers.testlink}}.

For more information about the installation requirements for TeamForge—TestLink integration, see:

* [TeamForge Installation Requirements][requirements]
* [TestLink Installation Requirements](https://github.com/TestLinkOpenSourceTRMS/testlink-code/blob/1.9.17/README.md)

{% capture cap1 %}
{% include inline_image.html file="status-success-small.png" %} Contact CollabNet for support on TeamForge—Testlink integration. For TestLink support, contact TestLink directly. [Click here](https://github.com/TestLinkOpenSourceTRMS/testlink-code/blob/testlink_1_9/BUYING_SUPPORT.TXT) for more information.<br><br>
{% include inline_image.html file="status-success-small.png" %} TeamForge 16.7 through TeamForge 19.1 support integration only with TestLink 1.9.15 and 1.9.16 using the `collabnet-testlink-1.0.2.tar` plugin.<br><br>
{% include inline_image.html file="status-success-small.png" %} TeamForge 19.2 supports integration with TestLink versions {{site.data.identifiers.testlink}} using the `collabnet-testlink-1.0.3.tar` plugin.<br><br>
{% include inline_image.html file="status-success-small.png" %} TeamForge 19.3 and later supports integration with TestLink versions {{site.data.identifiers.testlink}} using the `collabnet-testlink-1.0.5.tar` plugin.<br><br>
{% include inline_image.html file="status-success-small.png" %} If you are on earlier versions of TestLink, upgrade to one of the supported TestLink versions and integrate it with TeamForge. This integration does not provide backward compatibility (Data reliability and Migration) to older TeamForge—TestLink 1.9.11 integration that is based on TeamForge's Integrated Application Framework (IAF).<br><br>
{% include inline_image.html file="status-success-small.png" %} By default, only TeamForge Site Administrators can create test suites. If you want other users to create test suites, you must create a site-wide role in TeamForge, grant "CREATE/VIEW" access to "All Projects" for the role and assign this role to users.
{% endcapture %}
{% include callout.html type="primary" content=cap1 %}

TeamForge {{site.data.identifiers.teamforge}} supports integration with TestLink {{site.data.identifiers.testlink}} to track and synchronize requirement and defect tracker artifacts between these two systems.

The TeamForge—TestLink integration has two primary touch points:
* **Requirements** (TeamForge) to **Test Suites** (TestLink)
* **Test Case Run Failures** (TestLink) to **Defects** (TeamForge)

  {% include image.html file="TeamForge-Testlink.png" caption="TeamForge-TestLink Integration Workflow" %}

Here is a sample workflow to illustrate these touch points:

1. **Map TeamForge and TestLink projects**—The first step is to establish a project mapping between the intended TeamForge and TestLink projects. During mapping, in TestLink, you’ll be able to specify the TeamForge “Requirements” and “Defects” trackers for your project. These trackers will be used throughout the workflow.
2. **Create Requirements and Test Suites**—When a requirements tracker artifact is created in the TeamForge tracker specified in Step 1, you can choose to have a “Test Suite” created in TestLink. The Test Suite, once created, is associated with the requirements tracker artifact in TeamForge.

   {% include image.html file="Requirement-TestSuite.png" caption="TeamForge's Requirements Artifacts mapped with TestLink's Test Suites" %}

3. **Populate Test Suite with Test Cases**—Within TestLink, you can find and populate your Test Suite with Test Cases.
4. **Run Test Cases against Builds**—Once the Test Cases have been defined, you can run them against desired builds, tracking results in TestLink. Test Case runs are associated to the build/binary being tested for traceability purposes.
5. **Create Defects for failed Test Case runs**—If you encounter failing Test Case runs, you can simply click a button inside TestLink to create a defect in TeamForge. This is a “push button” defect that opens a new TeamForge window pre-populated with Test Case run failure data. An association will be created between the failing Test Case run and the new Defect.

   {% include image.html file="TCRun-Defect.png" %}

6. **Visualize Traceability**—Once this cycle is complete, you can view the associations chain between the requirements tracker artifact and the Test Suite, Test Case runs and any associated defects, the builds or binaries they exercised, the commits which triggered the build, and ultimately the requirements that started it all.

   {% include image.html file="Test-Traceability.png" %}

## Set up the TeamForge Application Server {#installconfiguretestlinkforwebr}

Follow these instructions to install the TestLink integration plugin on the TeamForge {{site.data.identifiers.teamforge}} Application Server.

1. Log on to the TeamForge Application Server.
2. If you have been having TeamForge—TestLink integrated earlier, delete the existing plugin JAR file (for example `collabnet-testlink-1.0.4.jar`) post upgrade to TeamForge {{site.data.identifiers.teamforge}}.
   1. Go to **My Workspace > Admin**. 
   2. Select **Projects > System Tools > Customizations**.
   3. Select the TestLink plugin JAR file (for example, `collabnet-testlink-1.0.4.jar`).
   4. Click **Delete**. A confirmation message is displayed.
   5. Click **OK**.
<!-- https://forge.collab.net/sf/go/artf394592#3 -->   
3. [Download](https://mvn.collab.net/nexus/content/repositories/testlink-integration/com/collabnet/collabnet-testlink/1.0.5/collabnet-testlink-1.0.5.jar) the `collabnet-testlink-1.0.5.jar` file.
4. Go to **My Workspace > Admin**.
5. Select **Projects > System Tools > Customizations** and click **Create**.
6. Click **Choose File** and select the `collabnet-testlink-1.0.5.jar` file.
7. Click **Add**.

## Set up the TestLink Server

1. Log on to the TestLink Server.

2. If you've been having TeamForge integrated with TestLink 1.9.16 or earlier:
   1. Upgrade your TestLink server to one of the supported TestLink versions {{site.data.identifiers.testlink}}. Follow the TestLink's official upgrade procedure.

      {% capture cap2 %}
      Make sure that you have the following RPMs available during TestLink installation: <br><br>
      {% include inline_image.html file="status-success-small.png" %} php-xml <br>
      {% include inline_image.html file="status-success-small.png" %} php-mbstring <br>
      {% include inline_image.html file="status-success-small.png" %} php-bcmath
      {% endcapture %}
      {% include callout.html type="primary" content=cap2 %}

   2. Remove the existing TeamForge—Testlink integration plugin.
   3. Uninstall the existing TeamForge—TestLink integration plugin.
      1. Delete the TeamForge project mapping.

         Before uninstalling the TeamForge—TestLink integration plugin, it is a best practice, but not mandatory, to delete the TeamForge project mapping in TestLink.

         {% include important.html content="While deleting the project mapping in TestLink, TeamForge custom sources turn inactive. The TestLink tool in TeamForge should be removed manually, if required." %}
      2. Click **TeamForge Setup**.
      3. Click **Delete**. A confirmation message is displayed.
      4. Click **OK**. The TeamForge project mapping is deleted.
      5. Click the **Plugins** icon from the toolbar.
         {% include image.html file="testlink01.png" %}
      6. Identify the TeamForge—TestLink integration plugin from the list of **Installed Plugins** and click **Uninstall**. 
      
3. If you are installing TestLink for the first time, just download and install one of the supported TestLink versions {{site.data.identifiers.testlink}} on the TestLink server.

4. Download the [collabnet-testlink-1.0.6.tar](https://mvn.collab.net/nexus/content/repositories/testlink-integration/com/collabnet/collabnet-testlink/1.0.6/collabnet-testlink-1.0.6.tar) plugin file to the `/tmp` directory and untar the file to `<testlink-installation-directory>/plugins` directory.

   ```shell
   cd <testlink-installation-directory>/plugins/
   tar -xvf /tmp/collabnet-testlink-1.0.6.tar
   ````
5. Log on to TestLink.

6. Click the **Plugins** icon from the toolbar.
   
   {% include image.html file="testlink01.png" %}

7. Identify the TeamForge—TestLink integration plugin from the list of Availabe Plugins and click **Install**. 

   The TeamForge—TestLink integration plugin is installed and shows up in the **Installed Plugins** section.

   {% include image.html file="201-testlinksso-01.png" %}

8. Go to **TestLink Home** and click the **TeamForge Webhook Setup** link.

    {% include image.html file="testlink03.png" %}

9. Enter the **Webhook URL** and click **Save**.

    {% include note.html content="You can generate the TeamForge Webhook URL by running the [`create_webhook_event.py`][create_webhook_event_py] script." %}  

    {% include image.html file="testlink04.png" %}

10. Click the **Home** icon from the toolbar.

11. Create a TestLink project.
    1. Click **Test Project Management** and click **Create**.
    2. Define project attributes such as the name, description, project prefix and so on. Click **Create**.
12. Go to the home page and click the **TeamForge Setup** link. This is where oyu create the mapping between the TeamForge and TestLink projects. 
    
    {% include image.html file="testlink-teamforgesetup01.png" %}

13. Enter the TeamForge **Project Home URL**, **Username**, **Password**, **Defect Tracker ID**, **Requirements Tracker ID** and click **Save**.

    {% include important.html content="It is assumed that you have a TeamForge project, requirements tracker and defect tracker created already. If not, create them first and then perform this step of setting up TeamForge in TestLink. Have the requirements and defect tracker ID handy while setting up TeamForge in TestLink." %}

    For more information on creating a TeamForge project and setting up trackers, see:
    * [Create a TeamForge Project][creatingaproject]
    * [Create a Tracker][trackers-creatingatracker.html#create-a-tracker]     

    {% include image.html file="testlink-teamforgesetup02.png" %}


    <!-- Artifact artf394592 : Documentation task for "Traceability between TeamForge Requirements tracker and Test Suite" -->
    
    Association Between the Requirements Artifact and the Test Suite
    : Once you create a mapping between the TeamForge and TestLink projects, three new fields show up on the TeamForge's Requirements and Defect trackers.
    : {% include image.html file="testlink18.png" caption="TestLink fields that show up when you map TeamForge—TestLink projects" %}
    : Select **Create** from the **Test Suite** drop-down list and type the TestLink project name to have a test suite created in TestLink whenever you create a new requirements artifact in TeamForge. The Test Suite so created is associated with the requirements tracker artifact as well.
    : Select the **Associations** tab and view the association between the requirements artifact and the test suite. 
    : {% include image.html file="testlink19.png" caption="Association between the requirements artifact and the test suite" %}

## Enable Single Sign-On (SSO) Between TeamForge and TestLink {#tlsso}

You can enable SSO between TeamForge and TestLink. Once you enable SSO, you cannot directly log on to TestLink. TestLink becomes one of the site-wide linked applications in TeamForge and you must log on to TeamForge to access TestLink. 

With SSO set up, TeamForge Administrator and non-admin users, from a role-mapping perspective, are mapped by default to the TestLink Administrator and Leader roles respectively.

1. Log on to the TestLink server. 
2. Add the following configuration tokens to the `<TestLink installation directory>/custom_config_inc.php` file.
   ```shell
   $tlCfg->authentication['SSO_enabled'] = true;
   $tlCfg->authentication['SSO_method'] = 'WEBSERVER_VAR';
   $tlCfg->authentication['SSO_uid_field'] = 'REMOTE_USER';
   $tlCfg->authentication['SSO_user_target_dbfield'] = 'login';
   $tlCfg->authentication['TeamForge_BASE_URL'] = 'https://<your TeamForge domain URL>';
   ````
3. Apply the `SSO_TL_patch.diff` patch file that comes with the plugin to the `<TestLink installation directory>/lib/functions/doAuthorize.php` file.
4. Log on to the TeamForge Application server. 
5. [Create a site-wide linked application][externalapplications.html#sitewidelinkedapp] for TestLink.
   For example, create a site-wide linked application using the following information. 
   ````
   Application Name: TestLink
   URL: http://testlink-domain/testlink-1.9.17/plugin.php?page=Teamforge/index.php
   Open Link In: New Window
   SSO Enabled: True
   ````
6. SSO is now enabled between TeamForge and TestLink and you can now access TestLink directly from the **My Workspace > More** TeamForge menu.
   {% include image.html file="201-testlinkss0-02.png" caption="TestLink as a site-wide linked application" %}
7. You can also access the TestLink application from within the TeamForge's defect association viewer.
   {% include image.html file="201-testlinksso-03.png" caption="TeamForge—Testlink SSO from the defect Association Viewer" %}



{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Webhooks-based Event Broker Overview][webhooks-event-broker-overview]
* [Install the TeamForge Webhooks-based Event Broker][install-webhooks-event-broker]
* [TeamForge-Jenkins Integration Using TeamForge Webhooks-based Event Broker][teamforge-jenkins-integration]
* [TeamForge-JIRA Integration Using TeamForge Webhooks-based Event Broker][teamforge-jira-integration]


{% include links.html %}



