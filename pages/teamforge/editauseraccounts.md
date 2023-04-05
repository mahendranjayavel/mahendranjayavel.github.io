---
title: Edit User Accounts
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license, saml, ldap, authentication]
sidebar: teamforge_sidebar
permalink: edituseraccounts.html
last_updated: Apr 4, 2019
summary: When a user has trouble accessing the site, you may need to reset the user's password or change the user's account status.
---
## Edit a User Account

{% capture cap2 %}
{% include inline_image.html file="status-success-small.png" %} If your TeamForge site uses LDAP for single-sign-on, passwords must be reset in the LDAP system, not on the Web administration pages. Ask your system administrator for help.<br><br>
{% include inline_image.html file="status-success-small.png" %} To avoid disasters, TeamForge makes it impossible to delete or deactivate the TeamForge admin account. You also can't remove the TeamForge admin flag or mark the admin user as a restricted user.<br><br>
{% include inline_image.html file="status-success-small.png" %} On sites with LDAP/SAML/SAML+LDAP integrations, site administrators can designate select users that do not have a SAML or LDAP account as local users. Local users can log on to TeamForge using just the TeamForge credentials while bypassing the SAML/LDAP/SAML+LDAP authentication realms. A local user can also change and reset his password. For more information, see [ALLOW LOCAL USER][siteadmin-configuresiteviaui.html#allowlocaluser].
{% endcapture %}
{% include callout.html type="primary" content=cap2 %}

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. On the **USERS** tab, click the name of the user whose account you want to edit.
4. On the **User Details** page, click **Edit**.
5. On the **Edit User Information** page, make your changes and click **Update**. You can specify up to a maximum of three alternate email addresses, if required.

## Act on Multiple User Accounts at Once
A TeamForge administrator can edit the status of multiple user accounts simultaneously.

For example, if you have multiple pending new accounts to approve, you can approve them in a batch instead of individually editing each account.

{% include note.html content="A pending user is a user who has requested an account but has not yet confirmed his or her email addresses." %}

{% capture cap3 %}
In the case of TeamForge admin accounts, you cannot make any of these edits:<br><br>
{% include inline_image.html file="status-success-small.png" %} Delete the account.<br>
{% include inline_image.html file="status-success-small.png" %} Change the account status to anything but active. <br>
{% include inline_image.html file="status-success-small.png" %} Remove the TeamForge admin flag. <br>
{% include inline_image.html file="status-success-small.png" %} Mark it as a restricted user. 
{% endcapture %}
{% include callout.html type="primary" content=cap3 %}

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. On the **Users** page, select the users whose status you want to edit.
4. Click the desired status change.
   * Delete - Deleted users are removed from all projects. All assigned items are removed from the user. Deleted users do not count against your TeamForge license count.
   * Disable - Disabled users cannot log in to TeamForge and do not receive notification messages, but they remain members of projects and selection lists.
   * Activate - Active users have full use of TeamForge, subject to RBAC permissions.

{% include links.html %}