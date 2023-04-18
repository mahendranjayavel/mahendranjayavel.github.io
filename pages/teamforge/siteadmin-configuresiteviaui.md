---
title: Configure Your Site's Settings
keywords: site options, site settings
tags: [ctf_20.3, ctf_19.2, site_admin_tasks, site-options.conf, authentication, ldap, saml, security, config_files]
last_updated: Sep 1, 2020
sidebar: teamforge_sidebar
folder: teamforge
permalink: siteadmin-configuresiteviaui.html
summary: Use the Configure Application tool to define your site level TeamForge settings.
---

The **Configure Application** tool, added in TeamForge 17.4, makes TeamForge site level settings configurable via the user interface. This comes in handy for site administrators, who otherwise would have to work with the `site-options.conf`file and then recreate the TeamForge runtime for site level configuration changes.

To modify your site settings, select **My Workspace > Admin** and select **Projects > System Tools > Configure Application**, modify the available site settings as required and click **Save**.

## Project
Project setting(s) that apply globally to all the projects in your TeamForge site:

### ALLOWED DOMAINS FOR CSRF

TeamForge administrators can now prevent CSRF by setting listing the domains that are allowed for CSRF.

The **ALLOWED DOMAINS FOR CSRF** parameter specifies the list of allowed domains to prevent users from performing any CSRF related activities. This list of domains is validated against the origin and the referer headers for any incoming requests into TeamForge. This is helpful while configuring TeamForge for cross-origin requests. The default value is `*` which allows all types of domains or URLs. Example URLs/domains: forge.collab.net, forge.collab.net/sf/sfmain/do/home.	

{% include image.html file="csrf-domains.png" %}

### NOTIFY ASSOCIATION AND DEPENDENCY UPDATES

Notification emails can be sent to all monitoring users when an association or dependency is added to an object. You can select the **NOTIFY ASSOCIATION AND DEPENDENCY UPDATES** check box to let TeamForge send notification emails to all monitoring users when an association or dependency is added. Clear this check box otherwise.	

### PROHIBITED FILE TYPES

You can restrict users from uploading specific file types. Add a list of comma-separated file extensions in this field to prevent those file types from being uploaded. For example, adding "exe,jar" prevents `.exe` and `.jar` files from being uploaded to TeamForge.

{% include note.html content="There are certain file upload restrictions already in place in TeamForge. For example, you can upload only an image file for a user's profile picture in the **My Settings** page. Such restrictions, by default, override the site level settings configured in the **Configure Application** page." %}

## Tracker {#trackersiteparams}
Tracker setting(s) that apply globally to all the trackers in your TeamForge site:

### MAXIMUM SIZE FOR SINGLE FILE ATTACHMENT {#maxfilesize}

Use this parameter to limit the size of a single file attachment (in Megabytes) to artifacts. You can specify the file size ranging from 1MB to 2048MB (2GB).

### MASS IMPORT ARTIFACTS LIMIT {#massimportartfslimit}

You can restrict the number of artifacts that can be mass-imported. Type the maximum number of artifacts that you want to allow via mass import in the **MASS IMPORT ARTIFACTS LIMIT** text box.	
## Lifecycle {#lifecycle}

Digital.ai VersionOne work item IDs, if used in your source code commit messages, are now automatically validated and associated with the actual Lifecycle work item.

This automatic work item association happens only if you have the following two parameters set up in TeamForge.

{% include image.html file="lifecycle-integration-params.png" %}

### LIFECYCLE API TOKEN

The API key used by TeamForge to talk to the Digital.ai VersionOne API.

### LIFECYCLE SERVER URL

The Digital.ai VersionOne server URL.

## External Authentication {#externalauthentication}

These settings are tied to any external authentication.

### ALLOW DATABASE AUTHENTICATION IF LDAP IS ENABLED {#allowdatabaseauthifldapenabled}

Select this check box to have LDAP credentials stored in TeamForge and have users authenticated via TeamForge every time a user logs in. This helps improve performance by optimizing the number of authentication calls between TeamForge and LDAP servers.

<!-- {% include important.html content="Enabling this parameter is mandatory for sites with internally managed CVS servers." %} -->

### ALLOW 'DIRECT LOGIN' FOR ALL

On sites with SAML or SAML+LDAP authentication, the site option, **ALLOW 'DIRECT LOGIN' FOR ALL**, comes in handy whenever you want to allow direct login (see [Direct Login to TeamForge][saml.html#directlogin]) for all the users regardless of the "Local User" setting (see [Enable Local User][siteadmin-configuresiteviaui.html#allowlocaluser]). 

If you enable the **ALLOW 'DIRECT LOGIN' FOR ALL** site option, users without a TeamForge account that try to login using the direct login URL are taken to the **Create TeamForge Account** page for account creation.

{% include image.html file="directlogin-for-saml-users.png" caption="ALLOW DIRECT LOGIN FOR ALL site option" %}

### ENABLE ACCOUNT MANAGEMENT {#enableacctmgmt}

Selecting the site parameter **ENABLE ACCOUNT MANAGEMENT** enables site administrators on sites with LDAP/SAML/SAML+LDAP integrations to create and edit user accounts and passwords.

### ENABLE LOCAL USER {#allowlocaluser}

In a SAML and/or LDAP enabled environment, site administrators can designate select users that do not have a SAML or LDAP account as local users. Local users can log on to TeamForge using just the TeamForge credentials while bypassing the SAML/LDAP/SAML+LDAP authentication realms. A local user can also change and reset his password.

When you select the **ENABLE LOCAL USER** site setting, the **Create User** and **Edit User Information** pages let site administrators to select the **Local User** check box while creating or editing user accounts. The list of users page also includes the **Local User** column. 

### ENABLE LDAP SELF REGISTRATION {#enableldapselfregistration}

If LDAP is enabled as an IdP in TeamForge Identity page, the site parameter **ENABLE LDAP SELF REGISTRATION** which is enabled by default, redirects those who try to log on to TeamForge without a user account, to the **Create TeamForge Account** page. To prevent the users from creating an account, the site administrators can disable this parameter. If the parameter is disabled, an error is thrown when users try to log on to TeamForge. 

### FORCE RE-AUTHENTICATION WITH LDAP SERVER {#forcereauthwithldap}

If you have enabled database authentication, LDAP user credentials are stored when users login for the first time and continue to login using the locally stored LDAP credentials. However, you can restrict such indefinite usage of the stored LDAP credentials and force user re-authentication at regular intervals by setting up this configuration parameter. For example, setting a value of `24` would force user re-authentication (by the LDAP server) every 24 hours.

### LDAP CONFIGURATIONS MAXIMUM LIMIT {#ldapconfigmaxlimit}

You can use this parameter to set the maximum number of LDAP configurations to be allowed on sites with multiple LDAP servers/directories. For example, if you set the value as 10, you can add only up to 10 LDAP configurations.

<!-- ## EventQ 

These are the settings related to EventQ.

### ACTIVITY STREAM AND REPORTS {#activitystream}

EventQ features such as the Activity Stream, EventQ based reports, and the Include Traceability check box (on the add/edit project tool page) are disabled in TeamForge 19.0 by default. If you have been using EventQ earlier and willing to use EventQ post upgrade to TeamForge 19.0, select this new site parameter **ACTIVITY STREAM AND REPORTS** to enable the Activity Stream, EventQ reports, and the Include Traceability check box. -->


<!--{% include image.html file="disable-activity-stream.png" %}-->

{% include links.html %}