---
title: Customize TeamForge
keywords: customize, customization jar, custom event handler
tags: [installation, upgrade, site_admin_tasks, project_admin_tasks, projects, customize, branding, postgres]
sidebar: teamforge_sidebar
permalink: customize.html
last_updated: Aug 6, 2020
summary: You can redesign some aspects of your site to suit your organization's needs and preferences.
---

These instructions support only some basic types of customization. Almost infinite varieties of customization are possible. To get into specific customization options in more detail, search or post a question on the TeamForge [discussion forum](http://forums.open.collab.net/ds/viewForumSummary.do?dsForumId=736) or talk to your CollabNet representative.

## Customize TeamForge Using a Custom `.jar` File

You can customize your TeamForge site by building a maven project and uploading the customization jar file that extends or customizes TeamForge.

Maven projects are built and packaged to generate TeamForge customization jar and `MANIFEST.MF` files. The generated customization jar file is then uploaded to TeamForge. When you upload a customization jar, it is processed and if it has a custom event, it is registered. Later, if it has customizations, they are cached by the customization mechanism for a cost-free access at every request. Cached customizations are then served by the following three servlets:

<div class="tg-wrap">
<table width="100%">
<tr>
<th width="60%">Servlet</th>
<th width="40%">Description</th>
</tr>
<tr>
<td markdown="1">/ctf/api/main/js-customization
</td>
<td markdown="1">Retrieves all the Javascript customizations.
</td>
</tr>
<tr>
<td markdown="1">/ctf/api/main/css-customization
</td>
<td markdown="1">Retrieves all the CSS customizations.
</td>
</tr>
<tr>
<td markdown="1">/ctf/js/modules/customization-\<customization-name>/\<resource-name>;
</td>
<td markdown="1">Resolves the resource relative to the main folder configured for the given customization name.
</td>
</tr>
</table>
</div>

The customization mechanism provides access to all the enabled customizations in the cache.

A customization jar can contain:
* Custom events
* Javascript customizations
* CSS customizations
* Custom bundles

{% include image.html file="jarfilestructure.png" caption="Sample jar File Structure" %}

Here's a [sample customization jar file](http://docs.collab.net/downloads/sample-customization-jar-file.jar).

While custom events are configured through an `events.xml` file in the `META-INF` folder in the jar file, Javascript, CSS and custom bundles are configured through `META-INF/MANIFEST.MF` entries.

Here's a list of `META-INF/MANIFEST.MF` entries:

<div class="tg-wrap">
<table width="100%">
<tr>
<th width="35%">MANIFEST.MF entries</th>
<th width="65%">Description</th>
</tr>
<tr>
<td markdown="1">CTF-Customizations-Enabled
</td>
<td markdown="1">The entry to enable or disable a customization. This entry applies to custom event and customizations.
* Custom event and customizations are applied if this entry is set to `True` (default value).
* Custom event and customizations are not applied if this entry is set to `False`.
</td>
</tr>
<tr>
<td markdown="1">CTF-Customization-Name
</td>
<td markdown="1">The entry to set the name of the customization to be used for getting bundles.
</td>
</tr>
<tr>
<td markdown="1">CTF-Customizations-Priority
</td>
<td markdown="1">The entry to set the priority for customizations. Allows you to specify the `priority` of the customization. Customizations are sorted by the servlets based on the `priority`. Customizations with low priority are included at the end. The priority value could be from 1 to 100, 100 being the default value.
</td>
</tr>
<tr>
<td markdown="1">CTF-JS-Customization
</td>
<td markdown="1">Path to a Javascript file.
</td>
</tr>
<tr>
<td markdown="1">CTF-CSS-Customization
</td>
<td markdown="1">Path to CSS stylesheet.
</td>
</tr>
<tr>
<td markdown="1">CTF-Bundle-Customization
</td>
<td markdown="1">Path to the main bundles directory.
</td>
</tr>
</table>
</div>

### An Illustration of How to Add a CSS Customization

1. Build a customization project.
   
   Maven project structure that includes a custom stylesheet file as a resource:
   ```css
	css-customization% find -type f
	./pom.xml
	./src/main/resources/custom/custom.css
	css-customization %
	````
	```css
	css-customization % cat src/main/resources/custom/custom.css 
	div.core-footer {
	    background-image:url('/ctf/js/modules/customization-mybundles/img/footer.png');
	}
	css-customization %
	````

	The `pom.xml` descriptor, uses the packaging plugin for setting the needed `MANIFEST.MF` properties:

   ```xml
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	  <modelVersion>4.0.0</modelVersion>

	  <groupId>com.ctf.customizations.samples</groupId>
	  <artifactId>css-customization</artifactId>
	  <version>1.0-SNAPSHOT</version>
	  <packaging>jar</packaging>
	...
	  <build>
	    <plugins>
	      <plugin>
	      <groupId>org.apache.maven.plugins</groupId>
	      <artifactId>maven-jar-plugin</artifactId>
	      <version>2.4</version>
	        <configuration>
	          <archive>
	            <manifestEntries>
	              <CTF-Customizations-Enabled>True</CTF-Customizations-Enabled>
	              <CTF-Customization-Name>mystyles</CTF-Customization-Name>
	              <CTF-CSS-Customization>custom/custom.css</CTF-CSS-Customization>
	            </manifestEntries>
	          </archive>
	        </configuration>
	      </plugin>
	    </plugins>
	  </build>
	...
	</project>
	````
2. Package the Maven project.
   ```shell
	css-customization % mvn package
	[INFO] Scanning for projects...
	...
	[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ stylesheet ---
	[INFO] Building jar: /home/matias/workspaces/ctf/css-customization/target/mystyles.jar
	[INFO] ------------------------------------------------------------------------
	[INFO] BUILD SUCCESS
	[INFO] ------------------------------------------------------------------------
	[INFO] Total time: 2.959s
	[INFO] Finished at: Wed May 21 20:26:28 ART 2014
	[INFO] Final Memory: 8M/105M
	[INFO] ------------------------------------------------------------------------
	css-customization %
	````
	
	Generated jar:
	```shell
	css-customization % jar tvf target/mystyles.jar
	   207 Wed May 21 20:26:28 ART 2014 META-INF/MANIFEST.MF
	    17 Wed May 21 20:26:26 ART 2014 custom/custom.css
	  1092 Wed May 21 20:16:06 ART 2014 META-INF/maven/com.ctf.customizations.samples/css-customization/pom.xml
	   132 Wed May 21 20:26:28 ART 2014 META-INF/maven/com.ctf.customizations.samples/css-customization/pom.properties
	css-customization %
	````

	Generated `MANIFEST.MF`:
	```shell
	Manifest-Version: 1.0
	Built-By: matias
	Build-Jdk: 1.7.0_55
	CTF-Customization-Name: mystyles
	CTF-CSS-Customization: custom/custom.css
	CTF-Customizations-Enabled: True
	Created-By: Apache Maven 3.0.4
	Archiver-Version: Plexus Archiver
	````
3. Upload the generated jar file as a custom event so that your customization is applied to TeamForge pages.
   1. Log on to TeamForge as a site administrator.
   2. Select **My Workspace > Admin**.
   3. Select **Projects > System Tools > Customizations** and click **Create**.
   4. Click **Choose File**, select the customization jar file and click **Add**.
4. Enable, disable, delete or download a customization.
   1. Select **My Workspace > Admin**.
   2. Select **Projects > System Tools > Customizations**.
   3. Select one or more customizations (check boxes) you want to enable or disable and click **Enable** or **Disable**.
   4. Select one or more customizations (check boxes) you want to delete and click **Delete**.
   5. Select one or more customizations (check boxes) you want to download and click **Download**.


## Customize a Page, Picture, Text String, or Other Elements on Your Site {#customizeanything}

Follow these general instructions to customize a page, picture, text string, or other element on your site.

{% include important.html content="Custom branding changes can be overridden when your site is upgraded to a new version. You may have to reapply any look-and-feel modifications after an upgrade." %}

1. Download the sample branding files. Choose one of these files:
   * [Basic branding package](https://docs.collab.net/teamforge221/downloads/branding-bundle-basic-22.1.411.zip): Contains the files you need to do most of your branding tasks. Safest to use this file if you are doing your own branding.
   * [Advanced branding package](https://docs.collab.net/teamforge221/downloads/branding-bundle-advanced-22.1.411.zip): Contains all the files that can be customized. For use when someone from CollabNet is helping you with your branding.

   {% include note.html content="It is important that you have the most recent version of this archive as a starting point. Check that the version number at the top of the `readme.txt` file in your copy of the branding package is the same as your version of the application. If it is not the same, check www.collab.net to see if there is a more recent version." %}
2. In the `look` project, check out the branding repository.
3. Copy the default version of the appropriate file from the branding zip file to the equivalent directory in your local copy of the branding repository.
4. Change the file to produce the results you want. For example:
   * To change a logo on your site's home page, overwrite the `home.gif` file with a new file of the same name.
   * To change a logo on a project home page, overwrite the `project.gif` file with a new file of the same name.
	 <div class="panel panel-info">
	 <div class="panel-heading">Logo Change Guidelines</div>
	 <div class="panel-body" markdown="1">
	  * The logo can be of any format—PNG, Gif, JPEG, and SVG. However, use a transparent logo file such as SVG. JPEG files, for example, are not transparent.
	  * The logo can be of any size, but choose the aspect ratio appropriately. However, the logo width should be at least 100px.
	 </div>
	 </div>
5. Commit the changed files into your site’s branding repository.
   {% include important.html content="Your branding repository does not have to contain all the files that are in the sample branding zip file, but the structure of your repository must be an exact mirror of the structure of the sample file set." %}

## Customize the Home Page of Your Site {#customizehomepage}
To change the content of your site's main page, replace the `home.vm` file or add either `domain_home.html` or `DomainHome.html.html` file to the `html` folder in the branding repository.

{% include note.html content="For the general steps for changing the look and feel of a page, see [Customize a Page, Picture, Text String, or Other Elements on Your Site][customize.html#customizeanything]." %}

The `\branding\templates\sfmain\home.vm` template controls the look, feel and structure of the standard home page. The default version allows users to log in and sign up for new user accounts, if Digital.ai TeamForge is configured to allow user self-creation.

If the `DomainHome.html.html` or `domain_home.html` file is checked into the branding repository, the contents of the file are displayed as the site home page.

{% include tip.html content="If both `DomainHome.html.html` and `domain_home.html` files exist in the repository, the contents of the `DomainHome.html.html` are displayed." %}

Edit the home.vm template to produce the page you want. You can change these objects on the site home page:

<div class="tg-wrap">
<table width="100%">
<tr>
<th width="30%">Object</th>
<th width="70%">Description</th>
</tr>
<tr>
<td markdown="1">siteNews
</td>
<td markdown="1">The html block that shows site news.
* The `siteNews` html block itself is not customizable.
* By uncommenting this `siteNews` object and commenting out `communityNews` object, site news can be displayed across all projects in the site.
* In addition to enabling the `siteNews` html block, you must set [ENABLE_SITE_NEWS][siteoptiontokens.html#enablesitenews] token to `true` if you want site news published on your site's home page.
</td>
</tr>
<tr>
<td markdown="1">communityNews
</td>
<td markdown="1">The html block that shows community news.
By uncommenting this object, and commenting out `siteNews` object, community news (news from the look project) can be displayed across all projects in the site.
</td>
</tr>
<tr>
<td markdown="1">mostActiveProjects
</td>
<td markdown="1">The html block that shows the most active projects. The html block itself is not customizable.
</td>
</tr>
<tr>
<td markdown="1">displayActivityGraph
</td>
<td markdown="1">A flag that indicates that the activity graph should be displayed.
</td>
</tr>
<tr>
<td markdown="1">displayTeamForgeLinks
</td>
<td markdown="1">A flag that indicates that Digital.ai TeamForge quick links should be displayed.
</td>
</tr>
</table>
</div>

## Customize the Home Page of Projects
To change the default main pages of the projects on your site, edit the `project_home.vm` file.

{% include note.html content="For the general steps for changing the look and feel of a page, see [Customize a Page, Picture, Text String, or Other Elements on Your Site][customize.html#customizeanything]." %}

Edit the `project_home.vm` template to produce the project page you want. You can change these objects on the project home page:

<div class="tg-wrap">
<table width="100%">
<tr>
<th width="30%">Object</th>
<th width="70%">Description</th>
</tr>
<tr>
<td markdown="1">projectData
</td>
<td markdown="1">The object that contains the information about the project. It implements the interface `com.collabnet.ce.customization.IProjectData`.
</td>
</tr>
<tr>
<td markdown="1">adminList
</td>
<td markdown="1">The list of project administrators. Each object of the list implements the interface `com.collabnet.customization.IUserRow`.
</td>
</tr>
<tr>
<td markdown="1">memberList
</td>
<td markdown="1">The list of project members. Each object of the list implements the interface `com.collabnet.customation.IUserRow`.
</td>
</tr>
<tr>
<td markdown="1">projectMember
</td>
<td markdown="1">A flag that indicates that the user is a member of the project.
</td>
</tr>
<tr>
<td markdown="1">joinProjectButton
</td>
<td markdown="1">The button that contains the link to the Join Project page. It returns a `com.collabnet.ce.customization.widgets.Button`.
</td>
</tr>
<tr>
<td markdown="1">useCustomHomePage
</td>
<td markdown="1">A flag that indicates that the page shows the Wiki Home page instead of the standard Home page.
</td>
</tr>
<tr>
<td markdown="1">customHomePage
</td>
<td markdown="1">The html that displays as the Project Home page.
</td>
</tr>
<tr>
<td markdown="1">editCustomHomePageButton
</td>
<td markdown="1">The button that is used to edit the custom Home page. It returns a `com.collabnet.ce.customization.widgets.Button`.
</td>
</tr>
<tr>
<td markdown="1">projectAdmin
</td>
<td markdown="1">A flag that indicates whether or not the current user is a Project Admin.
</td>
</tr>
<tr>
<td markdown="1">useCustomProjectLogo
</td>
<td markdown="1">A flag that indicates that the Wiki project logo image will be used instead of the standard project logo.
</td>
</tr>
<tr>
<td markdown="1">customLogoPathString
</td>
<td markdown="1">The url from where the custom project logo image can be loaded.
</td>
</tr>
</table>
</div>

## Change Your Site's Outgoing Emails
When you site sends out automated emails, the text of the emails can be customized to fit your site's specific needs.

{% include note.html content="Before customizing your site, download the branding files. See [Customize a Page, Picture, Text String, or Other Elements on Your Site][customize.html#customizeanything]." %}

You control screen labels and messages by overriding the resource bundle keys that specify the text strings that appear in Velocity macros and JSPs.

1. In your local copy of the branding repository, create a directory called templates/mail.
2. In the `templates/mail` directory, create a file containing the custom content for an email that the system sends out.
   
   Give the file the same name as the equivalent sample email file in the branding files package. For example, to override the email that is sent out to new members of the site, name the file `templates/mail/user_welcome.vm`. Use Velocity syntax to identify the parts of the email, like this:
   ```shell
	##subject
	Welcome to our TeamForge site!
	##subject
	##body
	Here is the content that I want to appear in emails coming from my site...
	##body
	````

	{% include note.html content="To customize a template in a specific language, identify the locale as an extension to the file name. For example, to create a user welcome file in Japanese, name the file `templates/mail/user_welcome_ja.vm`" %}
3. Commit your new and changed files into the repository.

<!--
## Add a Custom Event Handler to Your TeamForge Site
An event handler is a program that watches for events on a TeamForge site and communicates them to another system. You can add your own event handlers to the set that are built into TeamForge.

For example, some of your site's members may be using TeamForge alongside a legacy issue tracking system. You may want to write an event handler that listens to the `Artifact Create` event on your TeamForge site and sends the details about any newly created artifact to the legacy system through a webservice.

1. Create your custom event handler and package it as a .jar file.
2. Check with your system administrator that the [ENABLE_UI_FOR_CUSTOM_EVENT_HANDLERS][siteoptiontokens.html#enableuiforcustomeventhandlers] token in the site configuration file is set to `true`.
3. Go to **My Workspace > Admin**.
4. Click **SYSTEM TOOLS** from the **Projects** menu.
5. Click **Customizations**.
6. Click **Create** and use the **Browse** control to locate your `.jar` file.
7. Click **Add**.
   {% include note.html content="If the system reports `Error Parsing Event Jar File`, debug your event handler until the error message no longer appears." %}

   Your `.jar` file is uploaded to your TeamForge site and the event cache is cleared. All the events you specified in your event handler are now captured and sent to the external web service.-->

## Customize Your Apache Configuration
The following instructions illustrate how you can include custom configuration to Apache and disable the same if not required.

1. Create `conf.d/httpd/httpd.conf.d` under `/opt/collabnet/teamforge/etc/` directory.
2. Include `custom.conf` under `/opt/collabnet/teamforge/etc/conf.d/httpd/httpd.conf.d/`.
3. {% include installupgrade/deploy_services_without_note.html %}
   
   The following warning message is displayed, which you can ignore.

   ```shell
   Custom configuration found in /opt/collabnet/teamforge/etc/conf.d/httpd/httpd.conf.d has been applied. Please be informed that such configuration may impact the reliability of TeamForge.
   ````

   The following line is added to `/etc/httpd/conf/httpd.conf`:
   ```shell
   Include /opt/collabnet/teamforge/etc/conf.d/httpd/httpd.conf.d/
   ````
4. Run the `httpd -e info` command to know the Apache configuration/syntax errors, if any.

### Remove Custom Apache Configuration
1. To remove custom configuration:
   ```shell
   cd /opt/collabnet/teamforge/etc/conf.d/
   mv httpd/ httpd_old
   ````
2. {% include installupgrade/deploy_services_without_note.html %}


## Customize Your PostgreSQL Configuration
The following instructions illustrate how you can include custom configuration to PostgreSQL and disable the same if not required.

1. Create `conf.d/pgsql/pg_hba.conf.d/` under `/opt/collabnet/teamforge/etc/` directory.
   
   If the reporting service is running on a separate port (see [Create a Single Cluster for Both Database and Datamart][movedbdmintoonepginstance]), create `conf.d/reports-pgsql/pg_hba.conf.d/` under `/opt/collabnet/teamforge/etc/`.
2. Include `custom.conf` under `/opt/collabnet/teamforge/etc/conf.d/pgsql/pg_hba.conf.d/`.
   
   If the reporting service is running on a separate port, include `custom.conf` under `/opt/collabnet/teamforge/etc/conf.d/reports-pgsql/pg_hba.conf.d/`
3. {% include installupgrade/deploy_services_without_note.html %}
   
   The following warning message is displayed, which you can ignore.
   ```shell
   Custom configuration found in /opt/collabnet/teamforge/etc/conf.d/pgsql/pg_hba.conf.d has been applied. Please be aware of that such configuration may impact the reliability of TeamForge.
   ````
   If the reporting service is running on a separate port:
   ```shell
   Custom configuration found in /opt/collabnet/teamforge/etc/conf.d/reports-pgsql/pg_hba.conf.d has been applied. Please be aware of that such configuration may impact the reliability of TeamForge.
   ````

   Configuration settings from `custom.conf` are included in `/var/lib/pgsql/{{site.data.identifiers.postgres_short}}/data/pg_hba.conf`.

   If the reporting service is running on a separate port, configuration settings from `custom.conf` are included in `/var/lib/pgsql/{{site.data.identifiers.postgres_short}}/reports/pg_hba.conf`.

4. Check the `postgresql.log` file for any syntax errors: `/opt/collabnet/teamforge/log/pgsql/postgresql.log`.

### Remove Custom PostgreSQL Configuration
1. To remove custom configuration:
   ```shell
   cd /opt/collabnet/teamforge/etc/conf.d/
   mv pgsql pgsql_old
   ````

   If the reporting service is running on a separate port:
   ```shell
   cd /opt/collabnet/teamforge/etc/conf.d/
   mv reports-pgsql reports-pgsql_old
   ````
2. {% include installupgrade/deploy_services_without_note.html %}

{% include links.html %}