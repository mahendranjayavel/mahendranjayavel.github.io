---
title: TeamForge License
keywords: license, license types, ALM, SCM, Version Control, Collaboration, Trackers, license key, license info
tags: [ctf_21.1, ctf_20.0, getting_started, site_admin_tasks, license, ctf_18.2]
sidebar: teamforge_sidebar
permalink: teamforgelicense.html
last_updated: Jun 11, 2021
summary: When you purchase a TeamForge license, you get the right to assign licenses to a specified number of users.
---
## TeamForge License Framework {#licenseframework}
The TeamForge license framework has been revamped in TeamForge 21.1. 

TeamForge's license model consists of the following license types:
* ALM
* ALM Essentials
* SCM

Here's the list of changes to the TeamForge license model.

* The `Version Control`, `Collaboration`, and `Trackers` license types are no longer available in TeamForge 21.1 and later
* The `ALM` and `Baselines` license types are bundled together and are being offered as the new `ALM` license

When you migrate from TeamForge 21.0 or earlier to TeamForge 21.1 or later:
* Existing ALM licenses are migrated to the new ALM license (with Baselines)
* All other license types such as Baselines, Version Control, Tracker, and Collaboration are deleted

{% include callout.html type="primary" content="While TeamForge supports more selective tool options with these new license changes, there's no impact on customers, both new and existing, that require all the tools that TeamForge supports." %}

In addition to the tools offering, the Reporting framework is also controlled by the licenses you have. Meaning, you can view and generate reports based on the license types assigned to you. For example, you must have SCM license to view or generate SCM activity reports. Check with your Digital.ai representative if you aren't sure how many licenses or what kind of licenses you want/have.

The following table lists the license types and the tools that go with them (refer to the `Tools Availability Matrix` section at the end of this topic for a complete list of tools and functions).

<table>
<thead>
  <tr>
    <th>   <br>Features/Tools</th>
    <th>   <br>SCM</th>
    <th>   <br>ALM Essentials</th>
    <th>   <br>ALM</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>   <br>Source Code Management (SVN/GIT)   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>File Releases   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Discussions   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Integrations (Jira,   Jenkins, MicroFocus ALM, Nexus, ReviewBoard, TestLink)   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>CollabNet Desktops   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>LDAP/SAML support   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Trackers   </td>
    <td>   <br>   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Documents   </td>
    <td>   <br>   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Wiki   </td>
    <td>   <br>   </td>
    <td>   <br>   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <tr>
    <td>   <br>Baselines   </td>
    <td>   <br>   </td>
    <td>   <br>   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr>
  <!-- <tr>
    <td>   <br>Add-Ons (Authentication Manager, Undelete tool, Forklift)   </td>
    <td>   <br>   </td>
    <td>   <br>   </td>
    <td>   <br>{% include image.html file="status-success-small.png" %}   </td>
  </tr> -->
  <tr>
    <td>   <br>Reports   </td>
    <td>   <br>SCM Commits report</td>
    <td>   <br>Activity, Agile, and Table reports</td>
    <td>   <br>Distribution and Trend reports</td>
  </tr>  
  <tr>
    <td>   <br>24x7 Support</td>
    <td>   <br>Premium</td>
    <td>   <br>Premium</td>
    <td>   <br>Premium</td>
  </tr>
</tbody>
</table>

* Your license key contains a few important numbers:
  * The number of users eligible to use specific licenses such as `ALM`, `ALM Essentials`, and `SCM`.
  * The IP address of the machine that your site runs on.

    For example, if your organization has 80 users who will use only the source code management features, 100 users who will use TeamForge ALM Essentials features, and 100 users who need the TeamForge ALM features, your license key string may look like this:
    ````
    ALM_ESSENTIALS=100:ALM_PRO=100:SCM=80:12312023:supervillaininc:144.16.116.25.:302D02150080D7853DB3E5C6F67EABC65BD3AC17D4D35CB3Z00214141D70455B18583BF0A5000CA56B34817ADF8DBFI32353A6E657492617369633A38372E3139342E3136102E31322E
    ````
* Your license key only works for the IP address (or range of addresses) of the hardware that your Digital.ai TeamForge is running on, as specified in your order form. If your site uses a separate server for its database or source code repositories, make sure your license key reflects the IP addresses of all the necessary servers. If any of these addresses change, ask your Digital.ai representative to generate a new key.
* When you create a user account, you can assign the user with available licenses.
* You can purchase a TeamForge license for as many years as you want. The validity period is encoded into your license when it is generated by your Digital.ai representative.
* How many users your site can support depends on the type of license. Check with your Digital.ai representative if you aren't sure what kind of licenses you have.
* Your license key is attached to the IP address of the server where your site runs. You can get a license key for a single IP address or for a range of IP addresses.
* Your service year starts the first time you log into your site, or the first time you create or edit any item on your site, such as a tracker artifact or a document. Whichever of these events comes first starts the clock.
* The expiration date of your license is shown on the License Info page. (Go to **My Workspace > Admin** and select **Projects > License Info**).
* When your service year expires, you can still see the project data on your site, but you cannot make any changes to it. However, you can still carry out some critical maintenance functions for your site:
  * Enter a new license key.
  * Disable or delete users.
  * Change user passwords.
  * Get forgotten user passwords.
* Except <a href="#" data-toggle="tooltip" data-original-title="Deleted users are removed from all projects. All assigned items are removed from the user. Deleted users do not count against your TeamForge license count">deleted users</a>, all  other users in TeamForge such as <a href="#" data-toggle="tooltip" data-original-title="Active users have full use of TeamForge, subject to RBAC permissions">active users</a>, <a href="#" data-toggle="tooltip" data-original-title="Users who are granted access to the requested account, but have not yet confirmed their email addresses">pending users</a>, <a href="#" data-toggle="tooltip" data-original-title="Users who cannot log into TeamForge and do not receive email notifications, but still remain the members of projects and selection lists">disabled users</a>, and <a href="#" data-toggle="tooltip" data-original-title="Expired users cannot log into TeamForge, but can use the forgot password link to create a new password">expired users</a> continue to consume licenses.

### Tools Availability Matrix {#toolsavailabilitymatrix}

<table class="table">
<thead>
  <tr>
    <th>Tools</th>
    <th>SCM</th>
    <th>ALM Essentials</th>
    <th>ALM</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>File Releases</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Access Controls</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Project Work Spaces</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>User Management</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Flexible Process and Toolchain Templates</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Reusable Dashboards</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Categories and Groups</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Cross Project Visibility</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Cross Project Search</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Site-wide Administration</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Custom Branding and Custom Integrations</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Security Architecture</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Onsite and Hosted Provisioning</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Git/SVN Repository Management and Replication</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Code Review</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Build Automation</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Binary Repository Management</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Wiki and Discussion Forums</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>SVN Auto Updates</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>SVN Repository Backup and Monitoring</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Agile Task and Planning Boards</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Trackers</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Test Management</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Cross Project Reporting and Dashboards</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Document Management</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Baselines</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td colspan="4" align="center">Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td colspan="4">Activity Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td>SCM Commits (Datamart)</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Artifact Closed (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Artifact Created (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td colspan="4">Agile Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td>Burn Down Chart (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Committed vs Done vs Missed (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Cumulative Flowchart (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Release Burn Up Chart (Datamart)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td colspan="4">Table Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td>Tracker (Operational DB)</td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td colspan="4">Distribution Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td>Artifact Distribution Chart (Multiple Trackers) (Datamart)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Artifact Distribution Chart (SingleTracker) (Datamart)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Average Size by Area/Group (Operational DB)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Status Distribution by Area/Group (Operational DB)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Total Size by Area/Group (Operational DB)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Total Size by Tracker Type (Operational DB))</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td colspan="4">Trend Reports</td>
    <td style="display: none"></td>
    <td style="display: none"></td>
    <td style="display: none"></td>    
  </tr>
  <tr>
    <td>Artifact Open/Close (Datamart)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
  <tr>
    <td>Average Age Report (Datamart)</td>
    <td></td>
    <td></td>
    <td>{% include image.html file="status-success-small.png" %}</td>
  </tr>
</tbody>
</table>

## Supply Your TeamForge License Key via Teamforge User Interface {#supplylicenseui}

Your license key enables you to use Digital.ai TeamForge for the period of your contract.

Your license key will only work for the IP address of the machine that your Digital.ai TeamForge is running on, as specified in your order form.

{% include callout.html type="primary" content="These steps are for installing your license key via the web interface. If you prefer, you can install it as a text file instead. See [Supply your TeamForge License Key as a Text File][teamforgelicense.html#supplylicensetextfile]." %}

1. Locate the confirmation email you received from your Digital.ai representative when you purchased your contract.
2. Log into your site as a Site Administrator.
   {% include note.html content="A Site Administrator is different from the root user on the server that runs your TeamForgse site." %}
3. Click **Admin > License Info**.
   
   If you have entered a license before, the IP address and current licensed number of users on your site are listed on the License Key page. Verify that the IP address is the same as the one you entered in your order form.
4. Click **Enter License Key**.
5. Copy your new license key from the confirmation email and paste it into the Enter License Key field. 

   A license key string looks like this:
   ````
   ALM_ESSENTIALS=100:ALM_PRO=100:SCM=80:12312023:supervillaininc:144.16.116.25.:302D02150080D7853DB3E5C6F67EABC65BD3AC17D4D35CB3Z00214141D70455B18583BF0A5000CA56B34817ADF8DBFI32353A6E657492617369633A38372E3139342E3136102E31322E
   ````

   {% include important.html content="Save this license key in case you need to reinstall Digital.ai TeamForge." %}
6. Click **Save**.
7. Verify that the new value for Licensed Number of Users matches the total number of licensed users in your contract.

## Supply Your TeamForge License Key as a Text File {#supplylicensetextfile}
Your license key enables you to use Digital.ai TeamForge for the period of your contract.

Your license key will only work for the IP address of the machine that your Digital.ai TeamForge is running on.

{% include warning.html content="If you are upgrading from a site with a limited number of users to an enterprise-scale site, you must install your license key before starting Digital.ai TeamForge. Otherwise, your site could be rendered inoperable." %}

1. Locate the confirmation email you received from your Digital.ai representative when you purchased your contract.
2. Create a text file and copy-paste your license key from the confirmation email into it.
   
   For example, if your organization has 80 users who will use only the source code management features, 100 users who will use TeamForge ALM Essentials features, and 100 users who need the TeamForge ALM features, your license key string may look like this:
   ````
   ALM_ESSENTIALS=100:ALM_PRO=100:SCM=80:12312023:supervillaininc:144.16.116.25.:302D02150080D7853DB3E5C6F67EABC65BD3AC17D4D35CB3Z00214141D70455B18583BF0A5000CA56B34817ADF8DBFI32353A6E657492617369633A38372E3139342E3136102E31322E
   ````
   {% include note.html content="Save this license key in case you need to reinstall Digital.ai TeamForge." %}
3. Save the text file as `/opt/collabnet/teamforge/var/etc/sflicense.txt`
   {% include tip.html content="Save your license key somewhere remote too, in case you need to reinstall Digital.ai TeamForge and your `sflicense.txt` file is not accessible." %}
4. Make the license file usable by the application.
   ```shell
   chmod 0664 /opt/collabnet/teamforge/var/etc/sflicense.txt
   chown <APP_USER>:<APP_GROUP> /opt/collabnet/teamforge/var/etc/sflicense.txt
   ````
   Change the values of `<APP_USER>` and `<APP_GROUP>` with the values of `APP_USER` and `APP_GROUP` tokens respectively from the `/opt/collabnet/teamforge/runtime/conf/runtime-options.conf` file.


## View License Information
You can obtain a summary of the license information from the **License Info** page.

The **License Info** page provides you with all the basic information about the licenses you purchased for your TeamForge site. This includes details such as the number of TeamForge licenses you had obtained, how many you have used, expiration date and so on.

1. Go to **My Workspace > Admin**.
2. Select **LICENSE INFO** from the **Projects** menu.

{% include links.html %}