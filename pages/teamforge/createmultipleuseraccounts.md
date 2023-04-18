---
title: Create Multiple User Accounts
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license, authentication, ldap]
sidebar: teamforge_sidebar
permalink: createmultipleuseraccounts.html
last_updated: Feb 22, 2019
summary: To participate in a TeamForge site, a person must have a user account on that site. TeamForge administrators can provide access to multiple users by creating their accounts together.
---
{% include important.html content="If your TeamForge site uses LDAP authentication, TeamForge administrators cannot create new user accounts. On a site with LDAP authentication, each user must log into TeamForge using his or her LDAP user name and password." %}

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. Click the drop-down arrow next to **Create** and click **Multiple Users**.
4. Choose the user's TeamForge **LICENSE TYPE** on **Create Multiple Users** page.
  
   Multi select option is now enabled. Users can now use combination of license types such as ALM and SCM.

   {% include image.html file="multipleuser_licensing.PNG" %}

5. On the **Create Multiple Users** page, enter up to 25 lines like this, one user per line:
   ```shell
   username username@yourdomain.org name organization Restricted
   ````
   Usernames must meet these criteria:
   * 1 to 31 characters.
   * Only alphanumeric characters.
   * No spaces.
   * At least one letter.
   * The first character is a letter.

   In addition:
   * Organization field is optional.
   * To create an unrestricted user, omit **Restricted**. 
   * Restricted users can only access projects of which they are members, while unrestricted users can access all projects that have not been made private by a project administrator.
   * Use quotes around the full name or the organization information if it is more than a single word.
   * A maximum of twenty-five user accounts can be created at one time.
6. Click **Create**.
   
   The user accounts are created and password e-mails are sent to all the new users.

{% include links.html %}