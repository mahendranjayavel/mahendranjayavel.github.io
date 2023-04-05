---
title: Set up TeamForge for LDAP Authentication with Auth Manager
keywords: authorization, authentication, auth manager
tags: [license, authentication, ldap]
sidebar: teamforge_sidebar
permalink: ldap-authmanager.html
last_updated: Mar 15, 2018
summary: Follow these steps to convert your TeamForge installation to authenticate against your corporate OpenLDAP server.
---

## Set up LDAP Integration for TeamForge {#ldapforteamforge}

Follow these steps to convert your TeamForge installation to authenticate against your corporate OpenLDAP server.

{% include note.html content="Refer to the [Installation Requirements][requirements] for TeamForge for the supported OpenLDAP versions." %}

1. {% include installupgrade/stop_teamforge_178andLater.html %}
2. Edit the `site-options.conf` file.
   1. Enable TeamForge to use LDAP authentication by editing the `site-options.conf` file, for example, edit `/opt/collabnet/teamforge/etc/site-options.conf` file. Under **External User Authentication**, uncomment the line that follows and change its value to `true`.
   ```shell
   USE_EXTERNAL_USER_AUTHENTICATION=true
   ````
   2. Configure the `site-options` tokens.

      {% include note.html content="The values specified for the following tokens are only for illustration purpose." %}

      ```shell
      EXTERNAL_AUTHENTICATION_TYPE=ldap
      LDAP_DN_PREFIX=cn=
      LDAP_DN_SUFFIX=,cn=Users,dc=testldap,dc=qa,dc=collab,dc=net
      LDAP_SERVER_URL=ldap://testldap.qa.collab.net:3268
      ````
4. {% include installupgrade/deploy_services_with_note.html %}

## Turn off LDAP Authentication

During some maintenance operations, such as upgrades, you may need to turn off LDAP authentication.

 1. Open the `site-options.conf` file, the master configuration file that controls your TeamForge site.
    
    ```shell
    vi /opt/collabnet/teamforge/etc/site-options.conf
    ````

    {% include note.html content="`vi` is an example. Any *nix text editor will work." %}

 2. In the `site-options.conf` file, comment out these variables:

    * USE_EXTERNAL_USER_AUTHENTICATION
    * LOGIN_CONFIG_XML_FILE
    * MINIMUM_PASSWORD_LENGTH

 3. Recreate the runtime environment.

    ```shell
    ./install.sh -V -r -d /opt/collabnet/teamforge
    ````

 4. Review the variables you have changed, then save the `site-options.conf` file.

## Authenticate Users with LDAP Using Auth Manager

Use the Auth Manager to effectively manage and synchronize user profiles with LDAP.

There are a few limitations to the conventional method used to enable LDAP authentication. For example, when an external authentication source is configured using the conventional method, the template XML file needs to be copied and edited manually. The manual intervention may lead to ambiguities and it makes the process error-prone.

TeamForge makes the entire external authentication process easier with the Auth Manager add-on. It provides users the ability to create multiple profiles, manage profiles, and perform LDAP synchronization.

The Auth Manager allows you to:

 * import [login-config.xml][login-config] file.

 * maintain multiple profiles in LDAP servers.

 * manage each profile individually.

 * activate a profile without recreating runtime.

 * store files in the Integration Data Service (IDS) that survives an upgrade.

## Install Auth Manager

The Auth Manager add-on provides customers with a central authentication service the ability to integrate TeamForge with external authentication services such as LDAP, Active Directory, and Kerberos.

The Auth Manager TeamForge add-on is available as an RPM file that you have to download and install. Contact CollabNet Support for more information.

 1. Log on to TeamForge as a root user.

 2. Extract the RPM file. Extracting creates the add-on directory at `/opt/collabnet/teamforge/add-ons`

 3. Navigate to the new add-ons directory.

    ```shell
    cd /opt/collabnet/teamforge/add-ons/ctf_authentication_manager
    ````

 4. Install the Auth Manager:

    ```shell
    ./install
    ````

 5. Choose to synchronize with LDAP for user data or make use of the user provided data, as required. For example, if you want to:

    * create a user profile quickly, use the data available in LDAP by enabling LDAP sync and running `hide.sh` script. It displays only the **Re-type password** field to the user.

    * create a user profile using the data provided by the user, disable LDAP and run the `show.sh` script. It displays all the fields that you expect the user to fill in and requires site administrator's approval. This is fairly a time-consuming process.

 6. Set up your site's master configuration file.

    ```shell
    vim /opt/collabnet/teamforge/etc/site-options.conf
    ````

    1. Set [_APPROVE_NEW_USER_ACCOUNTS_][siteoptiontokens.html#APPROVE_NEW_USER_ACCOUNTS] token as `false`.

       * **Hide fields** - To skip the approval process and create an user profile with the data available in LDAP, you have to enable LDAP Sync and run the `hide.sh` script after installation. It conceals all the fields on the **Create New User** page except the **Re-type password** field.

       * **Show fields** - To get the data from the user and not through the LDAP sync, you have to disable LDAP Sync run the `show.sh` script after installation. It shows all fields including **full name**, **email**, **locale string**, and **license type** on the **Create New User** page.

    2. Set [REQUIRE_PASSWORD_SECURITY][siteoptiontokens.html#REQUIRE_PASSWORD_SECURITY] as `false`.

    3. Set [PASSWORD_REQUIRES_NUMBER][siteoptiontokens.html#PASSWORD_REQUIRES_NUMBER] as `false`.

    4. Set [PASSWORD_REQUIRES_NON_ALPHANUM][siteoptiontokens.html#PASSWORD_REQUIRES_NON_ALPHANUM] as `false`.

    5. Set [USE_EXTERNAL_USER_AUTHENTICATION][siteoptiontokens.html#USE_EXTERNAL_USER_AUTHENTICATION] as `true`.

    6. Set [REQUIRE_USER_PASSWORD_CHANGE][siteoptiontokens.html#REQUIRE_USER_PASSWORD_CHANGE] as `false`.

    7. Set [MINIMUM_PASSWORD_LENGTH][siteoptiontokens.html#MINIMUM_PASSWORD_LENGTH] as `0`.

    8. Set [PASSWORD_REQUIRES_MIXED_CASE][siteoptiontokens.html#PASSWORD_REQUIRES_MIXED_CASE] as `false`.

 7. Protect Auth Manager with SSL, if preferred. Click [here][sslforintegrations] for more details.

 8. Provision services.
   
    ```shell
    teamforge provision
    ````
    {% capture provisionnote %}   
     TeamForge {{site.data.identifiers.teamforge}} installer expects the system locale to be `LANG=en_US.UTF-8`. TeamForge create runtime (`teamforge provision`) fails otherwise.
    {% endcapture %}
    {% include callout.html type="primary" content=provisionnote %}

 9. Start TeamForge.

    ```shell
    teamforge start
    ````

    {% capture installcompletionnote %}

    To ensure that the installation has been completed successfully and the external authentication functionality works do the following: <br><br>

    {% include inline_image.html file="status-success-small.png" %} Login to the TeamForge through UI as an admin user and check if the add-on is appearing as Auth Manager in the project navigation bar. Also, for fresh installation, an active **Default TeamForgeDatabase** profile appears under **Manage Existing Profiles**, by default, with the green status indicator. <br><br>
    {% include inline_image.html file="status-success-small.png" %} Alternatively, in the CLI, scrutinize the log files, for example, `/opt/collabnet/teamforge/log/apps/server.log`.
    {% endcapture %}
    {% include callout.html type="primary" content=installcompletionnote %}

## Configure Auth Manager in TeamForge

You can configure Auth Manager as a linked application in TeamForge.

As a result of this configuration, the Auth Manager appears in TeamForge's project navigation bar as a linked application.

 1. Log on to the TeamForge as a site administrator and go to the look project.

 2. Click **PROJECT ADMIN** from the **Project Home** menu.

 3. On the **Project Admin** Menu, click **Project Toolbar**. Then click **LINKED APPLICATIONS**. A list of all currently linked applications in the project is displayed.

 4. Click **Create**.

 5. On the **Create Linked Application** page, enter the name for the linked application as **AUTH MANAGER**.

 6. Enter the URL: `http://<host>/authenticationManager`.

 7. Enable Single Sign On (SSO) to allow TeamForge users to automatically log into the Auth Manager.

 8. Click **Save**. The application is linked to the TeamForge and the it appears as **AUTH MANAGER** in the project navigation bar.

## Manage Authentication Profiles

TeamForge utilizes its own database to validate the user name and password and also supports external authentication sources such as LDAP, Active Directory, Kerberos and Master Password.

### Create a User Profile

You can create a profile that determines the authentication method and settings in TeamForge.

You need to have at least one user profile or more in active status before configuring the external authentication.

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Create Profile**.

    {% include note.html content="In the **Manage Existing Profiles** page, if you do not find the desired one in the list of existing authentication profiles, you can click **New Profile** and proceed." %}

 4. From the drop-down menu, select the type of the new authentication profile.

    * **LDAP** - It uses the user name and password provided by the user to bind to the LDAP. If the bind is successful, the user is authenticated. This is a simple method of authentication. Click [here](https://developer.jboss.org/wiki/LdapLoginModule?_sscc=t) for more information.

    * **LdapExtended** - It uses a service account to bind to the LDAP. Customizable filters are used to bind with the user and to validate authentication. Click [here](https://developer.jboss.org/wiki/LdapLoginModule?_sscc=t) for more information.

      {% include tip.html content="Use this module if the users are spread over LDAP or when a group membership is required to access TeamForge." %}

      {% include important.html content="You can use only the **LdapExtended** profile as a source for LDAP Sync." %}

    * **Active Directory** - It uses the user data configured through Microsoft's Active Directory. This is a simple method of authentication.

    * **Kerberos** - It uses MIT KRB5 authentication. Contact your network admin for the host configuration settings.

 5. Set the Jboss flag that determines the behaviour of the control flag with multiple login-modules.

    * **Sufficient** - The login-module is not required to succeed. If it does succeed, control immediately returns to the application (authentication does not proceed down the login-module list). If it fails, authentication continues down the login-module list.

    * **Optional** - The login-module is not required to succeed. If it succeeds or fails, authentication still continues to proceed down the login-module list.

    * **Required** - The login-module is required to succeed. If it succeeds or fails, authentication still continues to proceed down the login-module list.

 6. Enter the value for each module property listed for the chosen profile type.

 7. Click **Create**. The confirmation message, _The authentication profiles have been imported. Activate the profiles to apply to TeamForge authentication_, appears.

    {% include note.html content="The newly created profile is listed under Authentication Profiles in the Manage Existing Profile page. It is now inactive and the status indicator is yellow. You must activate the newly created user profile." %}

    {% include tip.html content="Before you create any profiles using Auth Manager, you may see an inactive auto-imported **TeamForgeDatabase** profile appearing under **Authentication Profiles**. It is recommended to delete the **Auto-imported UsernamePasswordInDatabaseLoginModule** after creating and activating your first profile. Because the subsequent login and authentication request pass only through the active profile(s)." %}

### Configure Master Password

With the Site Administrative privileges, you can generate a master password and use it along with any user name registered with the TeamForge.

You can create an authentication profile for master password users in Auth Manager. Impersonation is not supported in TeamForge but the master password feature facilitates any user in TeamForge, irrespective of the roles, to login as another user if they have a valid master password.

The Site Admin needs to generate the password through scripts and configure the authentication user profile using Auth Manager. It is important to have this configured for a web-based SSO system.

 1. On the commad-line interface, login to TeamForge as a root user to generate the master password.

 2. Navigate to the new add-ons directory.

    ```shell
    cd /opt/collabnet/teamforge/add-ons/ctf_authentication_manager
    ````

 3. Set the master password.

    ```shell
    ./mpasswd.sh
    ````

 4. Enter the password and re-enter when prompted for confirmation.

    {% include note.html content="Ensure that the password is masked while entering it. Also keep the master password confidential and share it with authenticated users on demand. It is a good practice to keep changing the master password frequently." %}

 5. Log on to the TeamForge as a site administrator and go to the **look** project.

 6. From the project navigation bar, click **AUTH MANAGER**.

 7. From the **Main Menu** pane on the left, click **Create Profile**.

    {% include note.html content="In the **Manage Existing Profiles** page, if you do not find the desired one in the list of existing authentication profiles, you can click **New Profile** and proceed." %}

 8. On the **Create Authentication Profile** page, select **MasterPassword** from the drop-down list.

 9. Enter an appropriate name for the new MasterPassword user profile.

 10. Set the Jboss flag that determines the behaviour of the control flag with multiple login-modules.

     * **Sufficient** - The login-module is not required to succeed. If it does succeed, control immediately returns to the application (authentication does not proceed down the login-module list). If it fails, authentication continues down the login-module list.

     * **Optional** - The login-module is not required to succeed. If it succeeds or fails, authentication still continues to proceed down the login-module list.

     * **Required** - The login-module is required to succeed. If it succeeds or fails, authentication still continues to proceed down the login-module list.

 11. Click **Create**. The confirmation message, _The authentication profiles have been imported. Activate the profiles to apply to TeamForge authentication_, appears.

     {% include note.html content="The newly created profile is listed under **Authentication Profiles** in the **Manage Existing Profile** page. It is now inactive and the status indicator is yellow. You must activate the newly created user profile." %}

     {% include tip.html content="Before you create any profiles using Auth Manager, you may see an inactive auto-imported **TeamForgeDatabase** profile appearing under **Authentication Profiles**. It is recommended to delete the **Auto-imported UsernamePasswordInDatabaseLoginModule** after creating and activating your first profile. Because the subsequent login and authentication request pass only through the active profile(s)." %}

### Upgrade a Profile

You can upgrade a legacy authentication profile by importing the corresponding configuration file for authentication.

You can upgrade an authentication profile that was used in TeamForge 6.2 or older versions. For each profile, you have to import and save the respective [login-config.xml][login-config] file. It imports all the user profiles automatically into the `standalone.xml` file which is later converted into `standalone-full.xml`. The `login-config.xml` and `standalone-full.xml` files are placed at the same location.

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Upgrade Legacy Config**.

 4. Select an option to upload your existing authentication configuration.

    1. **Detected Configuration Files** - The list of files detected in the default location.

    2. **Specify Server-based Configuration File** - Specify the location of the login-config.xml file in the TeamForge Server.

    3. **Upload Existing Configuration File** - Specify the legacy login-config.xml file saved in the local.

 5. Click **Save**. The confirmation message, _The authentication profiles have been imported. Activate the profiles to apply to TeamForge authentication_, appears.

    {% include note.html content="The newly created profile is listed under **Authentication Profiles** in the **Manage Existing Profile** page. It is now inactive and the status indicator is yellow. You must activate the newly created user profile." %}

### Reorder Profiles

You can set the order in which a user profile needs to be considered for authentication. On the **Manage Existing Profiles** page, you can manually reorder the list of authentication profiles.

For example, consider LDAP server 'A' that has 100 users profiles and LDAP server 'B' with just 15 users profiles. To reduce the network traffic effectively, you may arrange authentication profiles in such a away that the authentication requests pass through 'A' first and then through 'B'. When you enable reorder option, you can manually move the profiles back and forth within the list.

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Manage Existing Profiles**.

 4. Click **Enable Reorder**. You are now able to drag and drop profiles within the list.

 5. Reorder the list as required and click **Save Order**.

### Activate a Profile

To pass authentication requests through a profile, you must change the status of a profile to active. The status indicator is green for active profiles in .

By default, the status of a newly created profile is inactive. A profile creation process in is considered complete when you change the status from inactive to active. Activated profiles are automatically listed in the `standalone-full.xml` file.

You can activate a newly created profile or an existing profile that is currently inactive. The profiles that are listed in **Manage Existing Profiles** page with yellow status indicators are all inactive or deactivated. You can have multiple profiles in the active status and reorder them within the list, if required.

 {% include tip.html content="Before you create any profiles using Auth Manager, you may see an inactive auto-imported **TeamForgeDatabase** profile appearing under **Authentication Profiles**. It is recommended to delete the **Auto-imported UsernamePasswordInDatabaseLoginModule** after creating and activating your first profile. Because the subsequent login and authentication request pass only through the active profile(s)." %}

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Manage Existing Profiles**.

 4. To activate all the profiles listed in the **Manage Existing Profiles** page atonce, click **Activate All**.

 5. To activate a particular profile in the **Manage Existing Profiles** page, click the profile name that needs to be activated. The profile details are displayed.

    {% include note.html content="Ensure that the current status of the profile is inactive and marked yellow." %}

 6. Click **Activate**.

    {% include note.html content="This button is visible only if the current status of the profile is inactive; scroll down to see this." %}

 7. On the confirmation window, click **OK** to proceed. The profile is activated now and the status turns green.

### Deactivate a Profile

At any point in time, you can deactivate an active profile in . The status indicator is yellow for inactive profiles in .

You may decide to deactivate a profile when you encounter issues with LDAP. If you are half way through the configuration setup and you do not want the profile to be acive for user authentication, you can deactivate it. Or If you want to troubleshoot and identify if the issue encounted prevails in the particluar LDAP server, you can deactivate the authentication profile.

The profiles that are listed in **Manage Existing Profiles** page with yellow status indicators are all inactive or deactivated. By default, the status of a newly created profile is inactive. You can have multiple profiles in the inactive status and reorder them within the list, if required. Deactivated profiles are automatically removed from the `standalone-full.xml` file.

 {% include important.html content="The deactivated profile remains in the Integrated Data Space (IDS) and you can reterive the same profile by activating it. The deactivated profile is permanently removed from the application only when it is deleted." %}

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Manage Existing Profiles**.

 4. To deactivate all the profiles listed in the **Manage Existing Profiles** page, click **Deactivate All**.

 5. To deactivate a particular profile in the **Manage Existing Profiles** page, click the profile name that needs to be deactivated. The profile details are displayed.

    {% include note.html content="Ensure that the current status of the profile is active and marked green." %}

 6. Click **Deactivate**.

    {% include note.html content="This button is visible only if the current status of the profile is active; scroll down to see this." %}

 7. On the confirmation window, click **OK** to proceed. The profile is deactivated now and the status turns yellow.

### Delete a Profile

You can delete an inactive profile from the permanently.

You can delete only deactivated profiles. If you do not want to have a profile in your authentication profile list, you need to deactivate it first and then delete it totally from the system.

 {% include important.html content="A deactivated profile remains in the Integrated Data space (IDS) until you perform deletion. To remove it completely from the system, delete the deactivated profile." %}

 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Manage Existing Profiles**.

 4. Click the profile that you want to delete. The profile details are displayed.

 5. Ensure that the current status of the profile is inactive.

    {% include note.html content="The profile status is marked yellow if inactive." %}
 
 6. Click **Delete**.

    {% include note.html content="This button is visible only if the current status of the profile is inactive." %}

 7. On the confirmation window, click **OK** to proceed. The profile has been deleted.

## Configure LDAP Sync

Perform LDAP Sync to update TeamForge with the user data available in the LDAP server. You can use an extended LDAP profile as a source for LDAP sync.

LDAP Sync, basically searches in the LDAP server for the user data configured in a login-module. Then it fetches the user data to the TeamForge and performs synchronization. You have options to selectively include login-modules for the LDAP Sync. For example, you have two LDAP accounts, out of which only one needs to be considered for LDAP sync. You need to turn off the LDAP account that you do not want to include in LDAP Sync.

The extended LDAP profile needs to have Bind DN, Bind Credentials, Base Filter, and Base DN values for the synchronization. The Base DN, which is not available in other simple LDAP authentications, makes the synchronization possible in **ExtendedLDAP** profile.

 {% include important.html content="Provide the site admin user name and obfuscated site admin password explicitly in `/opt/collabnet/teamforge/var/etc/soap-provider.properties` and do not provide ADMIN account credentials. " %}

 1. Log on to the TeamForge as a site administrator and go to the look project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **Manage Existing Profiles**.

 4. Select your desired profile that needs to have the LDAP Sync enabled.

 5. Click **Edit**.

 6. Select _true_ from the **Use As LDAP Sync Source** drop-down list to consider the selected profile for the synchronization.

 7. From the **Main Menu** pane on the left, click **LDAP Sync**.

 8. Click **Global Settings** and enable LDAP sync by selecting _true_ from the drop-down list.

 9. Click **Group Sync Settings** and do the following to synchronize groups:

    1. Select _true_ form the **Enable Group Sync** drop-down list to enable the LDAP/AD group synchronization.

    2. Enter appropriate value in **Group Job Cron Interval** to set the time interval for running group synchronization. For example, click [here](http://www.quartz-scheduler.org/documentation/quartz-1.x/tutorials/crontrigger).

    3. Enter the attribute in **Group Search Filter Expression**, to specify LDAP/AD expression for testing.

    4. Enter the search text with '*' at the end in **Group Search Filter Arguments** to synchronize with groups within the search results that have a particular prefix.

       {% include tip.html content="To include all the groups in synchronization, just enter '*'." %}

       **Example:** `CTF*`, `TF*` or `*`

 10. Click **User and User Data Sync Settings** and do the following to synchronize user status and attributes:

     1. Select _true_ form the **Enable User Data Sync** drop-down list to enable synchronization of user data.

     2. Enter appropriate value in the **User Data Sync Cron Interval** to set the time interval for group synchronizations. For examples, click [here](http://www.quartz-scheduler.org/documentation/quartz-1.x/tutorials/crontrigger).

     3. Enter the search text with '*' at the beginning in **User Search Filter Arguments** to synchronize with groups within the search results that have a particular prefix.

        {% include tip.html content="To include all the groups in synchronization, just enter '*'." %}

        **Example:** `CTF*`, `TF*` or `*`

     4. Select _true_ from the **Enable LDAP Status Sync** drop-down. It enables the LDAP Sync for the user status. If the user account is disabled in LDAP/AD, it flags and then disables the user account in TeamForge.

     5. Enter the number of days in **User Grace Period** beyond which the user account is disabled in TeamForge, if the user is not existing in LDAP.

     6. Select _false_ from the **Enable User Disable Action** drop-down list. It specifies if the user who has not logged into TeamForge for the specified period, needs to be disabled in TeamForge.

     7. Enter the number of days in **User Disable Interval (Days)** beyond which the user account is disabled in TeamForge, if the user has not logged into TeamForge for the specified period.

     8. Select _true_ from the **Enable User Delete Action** drop-down list to enable the deletion of a disabled user account based on the delete interval.

     9. Enter the number of days in the **User Delete Interval (Days)** drop-down list beyond which the user account is deleted from TeamForge. It is mandatory to have **Enable LDAP Status Sync** or **Enable User Disable Action** enabled.

        * When **Enable LDAP Status Sync** is _true_, users that do not exist in Active Directory are deleted after the 'delete' and 'grace' intervals from the flagged date. However, users that are existing in Active Directory cannot be disabled or deleted.

        * When **Enable User Disable Action** is _true_, users are deleted, irrespective of their existence in Active Directory, after the 'disable' and 'delete' intervals. It is calculated from the last login date.

        * When both **Enable LDAP Status Sync** and **Enable User Disable Action** are set to _true_, users that are not existing in Active Directory are deleted after the 'grace' and 'delete' intervals from the flagged date. And the users that are existing in the Active Directory are deleted after the 'disable' and 'delete' intervals from the last login date.

      10. Select _true_ from the **Enable User Membership Action** drop-down list to include user's LDAP/AD group membership in the synchronization. This needs to be enabled when the **Enable Group Sync** is set to _true_.

      11. Select _true_ from the **Allow User Re-enabling** drop-down list to re-enable LDAP active users that have pending or disabled status in TeamForge.

      12. Enter the user names in **Excluded Usernames** to skip the respective users accounts during synchronization.

      13. Enter the email address in **Default Email Address** that needs to be associated with the TeamForge user account. It is used as the default email address when the email field is found null or empty.

      14. Enter the number of user batches in **Split Users for LDAP Sync** to perform the synchronization.

          {% include note.html content="The user batch number entered splits the existing number of users into batches and then performs synchronization. Entering '0' or '1' considers all the existing users for the synchronization. Whereas entering '7' splits the existing users into seven batches and completes synchronization on the seventh run." %}

 11. Click to expand **Mail and Reporting Settings** and do the following:

     1. Select _true_ in **Enable User Email Reports** drop-down list to enable the email notification and reporting.

     2. Enter the SMTP host to mail through. If you are using the TeamForge James mail server, enter `localhost` in **Mail Transport Host**.

     3. Enter the email address of the recipient in **Mail To** that is usually a TeamForge Discussion Forum or a Tracker.

     4. Enter the email address of the sender in **Mail From** that is usually a TeamForge Discussion Forum or Tracker. The sender should be a valid TeamForge user.

     5. Enter any optional email address in **Mail CC** that needs a carbon copy of the email.

     6. Enter the subject line for the email in **Mail Subject**.

     7. Enter the user name in **Mail Username** that authenticates connection to the SMTP servers, if required. Its optional to fill in this field.

     8. Enter the password in **Mail Password** that is required to connect to SMTP servers, if required. Its optional to fill in this field.

 12. To save and apply all the changes you made to the profile, click **Save**.

 13. To run the LDAP Sync once (on an ad hoc basis), click **Run Once**.

 14. Click **Stop** and **Start** buttons to reinitiate the synchronization service.

## Configure Selective Sync

The Selective sync, otherwise known as single user sync, is similar to the LDAP sync that is performed only for a particular user and not for the users in the entire directory server. The Site Admin can perform synchronization for a selective user on the three selective attributes: full name, email, and organization.

The single user sync is helpful when you encounter inconsistencies or discrepancies in the LDAP behaviour. Some of the common scenarios include network delay, LDAP disconnectivity, and failure of authenticating a valid user.

In cases where the LDAP is not completely reliable, you can consider performing selective sync. For example:

 * While performing LDAP sync for a huge site that has thousands of users, there are chances that a handful of users are not synchronized and found missing in the report. Just for users that are missed out, you can synchronize the full name, email, and organization of individual users.

 * When the default (dummy) email is used to create a profile, the user may not receive any email notifications. In this case, the Site Admin can update only the email address of the user and perform single user sync. It saves the time spent on LDAP sync that scans through the entire directory server for a single user's email update.

   {% include note.html content="You cannot perform selective sync on users that are disabled and deleted. Single user sync is not applicable for the 'ADMIN' user." %}


 1. Log on to the TeamForge as a site administrator and go to the **look** project.

 2. From the project navigation bar, click **AUTH MANAGER**.

 3. From the **Main Menu** pane on the left, click **LDAP Sync**.

 4. Select _true_ form the **Enable Group Sync** drop-down list under **Global Settings > Group Sync Settings**. It enables the LDAP/AD group synchronization.

 5. Select _true_ form the **Enable User Data Sync** drop-down list under **Global Settings > User** and **User Data Sync Settings**. It enables synchronization of the user data.

 6. To save and apply all the changes you made to the profile, click **Save**.

 7. Go to **My Workspace > Admin**.

 8. On the site administration navigation bar, click **USERS**.

 9. On the _USERS_ tab, click the name of the user whose account you want to edit.

 10. On the **User Details** page, click **EDIT**.

 11. On the **Edit User Information** page, make your changes to the full name of the user, email address and organization.

 12. Click **Sync User Info** to synchronize the modified user data with the authentication source.

     {% include important.html content="Selective Sync is limited to full name, email, and organization of the user. If you have issues with other attributes of a user profile, try LDAP sync through **Auth Manager**." %}

## Uninstall Auth Manager

You can remove the Auth Manager completely from the TeamForge. Unlike other linked applications in TeamForge, you need not run the default installer to uninstall the athis add-on.

Before uninstaling, use the Auth Manager GUI to remove all the authentication profiles except the TeamForgeDatabase profile.

 1. Login to TeamForge as a root user.

 2. Navigate to the new add-ons directory.

    ```shell
    cd /opt/collabnet/teamforge/add-ons/ctf_authentication_manager
    ````

 3. Uninstall the **AUTH MANAGER**.

    ```shell
    ./uninstall.sh
    ````

 4. Provision services.

    ```shell
    teamforge provision
    ````

    {% capture provisionnote1 %}
    TeamForge {{site.data.identifiers.teamforge}} installer expects the system locale to be LANG=en_US.UTF-8. TeamForge "provision" command fails otherwise.
    {% endcapture %}
    {% include callout.html type="primary" content=provisionnote1 %}

 5. Start TeamForge.

    ```shell
    teamforge start
    ````

## Field Description for Auth Manager

The credential store and identity manager properties that are required to create an authentication profile in the Auth Manager are described here.

<table>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>allowEmptyPasswords</td>
<td>A flag indicating if empty (length 0) passwords should be passed to the LDAP server. An empty password is treated as an anonymous login by some LDAP servers and this may not be a desirable feature. Set this to false to reject empty passwords or true to have the LDAP server validate the empty password. The default is `true`.</td>
</tr>
<tr>
<td>baseCtxDN</td>
<td>It defines the fixed DN of the context to search for user roles. Consider that this is not the Distinguished Name of where the actual roles are located but the DN of where the objects containing the user roles are located (that is, for active directory, this is the DN with the user account).</td>
</tr>
<tr>
<td>baseFilter</td>
<td> It defines the search filter used to locate the context of the user to authenticate. The input username/userDN as obtained from the login module callback substitutes the {0} expression. This substitution behavior comes from the standard DirContext?.search(Name, String, Object[], SearchControls? cons) method. An common example search filter is "(uid={0}).</td>
</tr>
<tr>
<td>bindCredential</td>
<td>It defines the bindDN password. The password can be encrypted if the jaasSecurityDomain is specified.</td>
</tr>
<tr>
<td>bindDN</td>
<td>It defines the DN used to bind to the LDAP server. This is a DN with read/search permissions to the defined baseCtxDN and rolesCtxDN.</td>
</tr>
<tr>
<td>java.naming.factory.initial</td>
<td>The classname of the InitialContextFactory implementation. This defaults to the Sun LDAP provider implementation com.sun.jndi.ldap.LdapCtxFactory.</td>
</tr>
<tr>
<td>java.naming.provider.url</td>
<td>This property specifies the host name and port of the DNS server used by the initial DNS context, as well the initial context's domain name.</td>
</tr>
<tr>
<td>java.naming.referral</td>
<td>It indicates the service providers how to handle referrals.</td>
</tr>
<tr>
<td>java.naming.security.authentication</td>
<td>Specifies the authentication mechanism and the security level to use. This defaults to simple
java.security.krb5.kdc  It defines the host name on which the Active Directory server runs.</td>
</tr>
<tr>
<td>java.security.krb5.realm</td>
<td>It defines the Microsoft domain in which the Active Directory server runs.</td>
</tr>
<tr>
<td>principalDNPrefix</td>
<td>A prefix to add to the username to form the user distinguished name.</td>
</tr>
<tr>
<td>principalDNSuffix</td>
<td>A suffix to add to the username when forming the user distinguished name. This is useful if you prompt a user for a username and you don't want the user to have to enter the fully distinguished name.</td>
</tr>
<tr>
<td>roleAttributeID</td>
<td>It defines the role attribute of the context that corresponds to the name of the role. If the roleAttributeIsDN property is set to true, this property is the DN of the context to query for the roleNameAttributeID attribute. If the roleAttributeIsDN property is set to false, this property is the attribute name of the role name.</td>
</tr>
<tr>
<td>roleAttributeIsDN</td>
<td>It defines if the role attribute contains the fully distinguished name of a role object or the role name. If false, the role name is taken from the value of the user's role attribute. If true, the role attribute represents the distinguished name of a role object. The role name is taken from the value of the roleNameAttributeId attribute of the corresponding object. In certain directory schemas (for example, Microsoft Active Directory), role (group)attributes in the user object are stored as DNs to role objects and not as simple names. In such case, set this property to true. The default value of this property is false.</td>
</tr>
<tr>
<td>roleFilter</td>
<td>It defines a search filter used to locate the roles associated with the authenticated user. The input username/userDN as obtained from the login module callback substitutes the {0} expression in the filter definition. The authenticated userDN substitutes the {1} in the filter definition. An example search filter that matches the input username is (member={0}). An alternative that matches the authenticated userDN is (member={1}). <b>If you omit the roleFilter attribute, the role search will use the UserDN as the DN to obtain the roleAttributeID value</b>.</td>
</tr>
<tr>
<td>roleNameAttributeID</td>
<td> It defines the role attribute of the context which corresponds to the name of the role. If the roleAttributeIsDN property is set to true, this property is used to find the name attribute of the role object. If the roleAttributeIsDN property is set to false, this property is ignored.</td>
</tr>
<tr>
<td>rolesCtxDN</td>
<td>The fixed DN of the context to search for user roles. Consider that this is not the Distinguished Name of where the actual roles are; rather, this is the DN of where the objects containing the user roles are (e.g. for active directory, this is the DN where the user account is).</td>
</tr>
<tr>
<td>searchScope</td>
<td>Sets the search scope to one of the following (the default value is SUBTREE_SCOPE): 
<ul>
<li>OBJECT_SCOPE - searches the named roles context only.</li>
<li>ONELEVEL_SCOPE - searches directly in the named roles context.</li>
<li>SUBTREE_SCOPE - searches only the object if the role context is not a DirContext?. If the roles context is a DirContext?, the subtree rooted at the named object and the named object itself are searched.</li>
</ul>
</td>
</tr>
<tr>
<td>searchTimeLimit</td>
<td>It defines the timeout for the user and role searches in milliseconds (defaults to 10000, that is 10 seconds).</td>
</tr>
</table>


{% include links.html %}
