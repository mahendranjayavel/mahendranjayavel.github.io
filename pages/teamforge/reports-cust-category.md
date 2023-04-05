---
title: Customize Reports
keywords: customize reports
tags: [ctf_20.0, project_member_tasks, license, customize, reports, datamart]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jan 11, 2020
permalink: reports-cust-category.html
summary: You can customize your reports by modifying the parameters in config.ini file. For example, some reports require a particular data source such as datamart and some require a particular license type such as ALM.
---

## Why do you customize a report?

You may want to hide or display reports depending on the availability of their data source or the type of license so that users do not see reports which they cannot run. For example, some reports require a particular data source such as datamart and some require a particular license type such as ALM.

Other use cases:

 * There are reports which require a data store (datamart) to be enabled.
 * There are many reports that do not apply to SCM users.

## How to Create Custom Reports?

1. Checkout the branding repository from 'look' project.

2. Create the folder structure: `/branding/cli/custom-reports/`. 

3. Create the folders `pkg` and `types` under`/branding/cli/custom-reports/`. 

4. Customize the report(s).

   1. Create a folder (`<report_name>`) under `pkg` (`/branding/cli/custom-reports/pkg/<report_name>`). For example, for the report **OpenByStatus**, the folder structure would be: `/branding/cli/custom-reports/pkg/OpenByStatus`. For sample reports, go to `/opt/collabnet/teamforge/var/cliserver/app/reports/pkg/`.

   2. Create the output folder under `/branding/cli/custom-reports/types/`. The output folder name should be similar to the value you provide for the **outputType** parameter in the `config.ini` file.  For example, if `outputType=bar`, the output folder structure would be `/branding/cli/custom-reports/types/bar`.

      Typically, the custom reports folder structure should look like this:

      {% include image.html file="custom-reports-folder-structure.png" %}

      where,

      * `/branding/cli/custom-reports/pkg/<report_name>/` contains

        *  **config.ini**&mdash;This file consists of the parameters required for a specific report. You can edit or delete the required parameters.
        * **sample.png**&mdash;This provides the thumbnail of the actual report at the bottom of the **Project Home > Reports > Select Report Type** page in TeamForge UI. Click the thumbnail of the custom report that you want to create.
        * **script**&mdash;This script contains the actual business logic that the customer has requested for. The result data from this script is consumed by the `/branding/cli/custom-reports/types/<outputType parameter in config.ini file>/script`. 

          {% include callout.html type="primary" content="**Limitation**: You should only use the variable name **results** while sending the result data from `/branding/cli/custom-reports/pkg/<report_name>/script` file to `/branding/cli/custom-reports/types/<outputType parameter in config.ini file>/script` file." %}

      * `/branding/cli/custom-reports/types/<outputType parameter in config.ini file>/` contains 

        * **script**&mdash;This script uses the result data obtained from the `/branding/cli/custom-reports/pkg/<report_name>/script` file. This script is generic and can be reused by different reports.
        * **template.html**&mdash;This file is used to present the report data in the form of HTML reports.

   3. Customize the `config.ini` file added to the `pkg` folder. For more information on how to customize this file, see [Modifying config.ini File][reports-cust-category.html#modifyconfigini].

5. Commit the files.

6. Repeat steps 4 through 6 to create as many custom reports as required.

7. Run the `syncreports.py` script to synchronize the cli report types configuration to TeamForge
database. 

   ```shell
   /opt/collabnet/teamforge/runtime/scripts/clireports/syncreports.py custom
   ````

   {% include note.html content="The **custom** argument type specification (see the above command) scans through the custom cli reports directory (typically the branding repository's working copy of **look** project) and parses the report
  configuration (`config.ini`) file in every report directory." %}

8. Log on to TeamForge.

9. Select any project and click **Project Home > Reports**. Click the **Create** button at the bottom of the page. You can see the custom report added at the end of the **Select Report Type** page.

To edit the report parameters, edit the `config.ini` file of a specific custom report and commit it. Changes will be updated in the report in the UI.

{% include note.html content="Make sure that you run the `syncreports.py` script every time you modify the `config.ini` file." %}

{% include note.html content="To change the object or type, see the keywords used in the config files of default reports and reuse it in the custom reports." %}

## Modifying config.ini File {#modifyconfigini}

You can customize your reports by modifying the parameters in `config.ini` file. For example, if you want to customize the "Average Size by Area/Group" report, modify the parameters in `opt/collabnet/teamforge/var/cliserver/app/reports/pkg/averageSizeByArea/config.ini` file. 

Further, you can also change a report's title, description or timeToLive duration of cached data and so on.

The following illustration shows a sample `config.ini` file.

 {% include image.html file="cliconfigini.png" %}

Here's a sample list of parameters you can modify:

<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td><b>title</b></td>
<td>Specifies the title of the report.</td>
</tr>
<tr>
<td><b>description</b></td>
<td>Specifies the description of the report.</td>
</tr>
<tr>
<td><b>almRequired</b></td>
<td markdown="1">
* If _almRequired_=`true`&mdash;The site should be in the ALM mode and the users should have an ALM license to operate the ALM reports.
* If _almRequired_=`false`&mdash;The site can be in either of the modes; both ALM and SCM licensed users can operate these reports.
</td>
</tr>
<tr>
<td><b>scmrequired</b></td>
<td markdown="1">
If _scmrequired_=`true`&mdash;Users should have Version Control license to operate SCM reports.
</td>
</tr>
<tr>
<td><b>eventsRequired</b></td>
<td markdown="1">
<!-- * If _eventsRequired_=`true`&mdash;EventQ's events data store should be installed. Users can operate these reports irrespective of the site mode and license type. -->
<!-- * If _eventsRequired_=`false`&mdash;Users cannot operate these reports irrespective of the site mode and license type. -->
</td>
</tr>
<tr>
<td><b>datamartRequired</b></td>
<td markdown="1">
* If _datamartRequired_=`true`&mdash;Datamart should be installed. Users can operate these reports irrespective of the site mode and license type.
* If _datamartRequired_=`false`&mdash;Users cannot operate these reports irrespective of the site mode and license type.
</td>
</tr>
<tr>
<td><b>category</b></td>
<td markdown="1">
You can change the category of a report by specifying it in `config.ini` file. For example, to change the category of a specific report from 'Agile' to 'Distribution', specify as:

**category**=_DistributionReports_

The default categories are namely:

* ActivityReports
* AgileReports
* DistributionReports
* TrendReports
</td>
</tr>
<tr>
<td><b>outputType</b></td>
<td markdown="1">
Specifies the output type of the report. Default output types are: 

* bar, 
* trendlines, 
* dualaxeslinecolumn, 
* stackedcolumns, 
* columndone, 
* burndown, 
* eventsDual, 
* area, and
* custom 

The parameters specific to the output type are also defined in the `config.ini` file.

</td>
</tr>
<tr>
<td><b>fields</b></td>
<td>Specifies the field objects that are included in the report. Parameters specific to these fields are also specified in the `config.ini` file.</td>
</tr>
<tr>
<td><b>timeToLive</b></td>
<td markdown="1">
* The `timeToLive` parameter sets the duration (in hours) after which the cached report data is invalidated and refreshed from the data source.
* The default `timeToLive` for reports that use operational database is <u>2 hours</u>. The cached report data invalidated and refreshed every 2 hours.
* The default `timeToLive` for reports that use datamart is <u>24 hours</u>. 
* You can change the `timeToLive` duration depending on your site's requirements. 
{% include note.html content="Shorter `timeToLive` duration can impact performance." %}
</td>
</tr>
<tr>
<td><b>label</b></td>
<td>Specifies the field name of the object. Example: Planning Folder ID, Tracker ID, Group By, and so on.</td>
</tr>
<tr>
<td><b>type</b></td>
<td markdown="1">
Specifies the type of the field. Default types are:
* wizard (drop-down list)(for Projects, Trackers, Planning Folders, Teams, and Repositories),
* radio, 
* checkbox,
* multidate,
* select (drop-down list), and
* text
* number
</td>
</tr>
<tr>
<td><b>object</b></td>
<td markdown="1">
Specifies TeamForge objects such as Trackers, Planning Folders, Projects, Teams, and Repositories. You must include the **object** parameter for all the fields for which you have specified the field type as `wizard`.
</td>
</tr>
<tr>
<td><b>max</b></td>
<td>Specifies the maximum number of options that you can select. If you set `max=1`, it acts as a single-select field. If you set `max=10`, you can select 10 values at a time (acts as a multi-select field). This parameter must be included for the fields having the type `wizard` or `select`.</td>
</tr>
<tr>
<td><b>required</b></td>
<td markdown="1">
Specifies whether the field is a mandatory or an optional field. Values are either `true` or `false`.
{% include callout.html type="primary" content="**Limitation**: To make a field optional, you must remove the **required** parameter for that field from the `config.ini` file. Unlikely, the field would behave as a mandatory field, if you just set the value to `false`." %}
</td>
</tr>
<tr>
<td><b>values</b></td>
<td markdown="1">Specifies the set of values for a field. For example, for a **Group By** field, the values can be `Priority`, `Priority & Category`, and so on.
</td>
</tr>
</table>


{% include links.html %}