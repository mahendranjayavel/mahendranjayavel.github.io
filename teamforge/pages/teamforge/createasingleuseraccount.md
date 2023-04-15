---
title: Create a Single User Account
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license, ldap, authentication, saml]
sidebar: teamforge_sidebar
permalink: createasingleuseraccount.html
last_updated: Feb 22, 2019
summary: To participate in a TeamForge site, a person must have a user account on that site. TeamForge administrators can create these user accounts. This topic applies to sites with no LDAP authentication.
---
{% capture cap1 %}
{% include inline_image.html file="status-success-small.png" %} If your TeamForge site uses LDAP authentication, TeamForge administrators cannot create new user accounts. On a site with LDAP authentication, each user must log into TeamForge using his or her LDAP credentials.
<br><br>
{% include inline_image.html file="status-success-small.png" %} On sites with LDAP/SAML/SAML+LDAP integrations, site administrators can designate select users that do not have a SAML or LDAP account as local users. Local users can log on to TeamForge using just the TeamForge credentials while bypassing the SAML/LDAP/SAML+LDAP authentication realms. A local user can also change and reset his password. For more information, see [ALLOW LOCAL USER][siteadmin-configuresiteviaui.html#allowlocaluser].
{% endcapture %}
{% include callout.html type="primary" content=cap1 %}

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. Click the drop-down arrow next to **Create** and click **Single User**.
4. On the **Create User** page, enter the field values appropriately.
   1. Enter a user name for the user.

      Your user name must meet these criteria:
      * User name is case-sensitive. However, to make usernames case-insentive set the site-options token [ALLOW_CASE_INSENSITIVE_LOGIN][siteoptiontokens.html#allowcaseinsensitivelogin] to `true`.
      * Minimum number of characters as specified in the site-options.conf file.
      * No spaces.
      * Should have at least one letter.
      * The first character is a letter.
   2. Enter and confirm a password for the user, if you prefer to set the user's password yourself.
      {% include tip.html content="To invite users to create their own password, leave the PASSWORD field blank. A password ticket email will be sent to users to let them create a password." %}
   3. Enter the **FULL NAME** and **EMAIL ADDRESS** of the user.
      {% include tip.html content="You can add more email addresses for the user after you finish creating their profile." %}
   4. Enter the user's organization.

      Organization can be a geographic designation, a corporate division, or whatever you want. It's advised to keep it consistent across your site.
   5. Select the language from the **LOCALE** drop-down list.
      {% include note.html content="TeamForge supports English, Chinese, Japanese and Korean languages." %}
   6. From the **TIME ZONE** drop-down list, select the preferred time zone for the user.
      {% include important.html content="Selecting the time zone overrides the default time zone set by the site options token, [DISPLAY_TIMEZONE][siteoptiontokens.html#displaytimezone]. It reflects in all the email notifications and TeamForge pages excluding integrated application pages." %}
   7. Choose the user's TeamForge LICENSE TYPE. 
      * You can assign users a combination of multiple license types such as ALM and SCM.
      {% include image.html file="createanuser_licensing.PNG" %}
   8. Choose a user type. You can choose only one user type for each user.
      * SITE ADMIN: Administrators have unlimited access to all the data in TeamForge.
      * RESTRICTED USER: Restricted users can only access projects of which they are members.
        {% include important.html content="If you do not select **RESTRICTED USER**, the user will be unrestricted and able to access all projects that have not been made private by a project administrator." %}
   9. To send a welcome message to the user, select **SEND WELCOME MESSAGE?**.
5. Click **Create**.
   
   The user account is created.

{% include links.html %}