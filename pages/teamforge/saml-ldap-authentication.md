---
title: Use Both SAML and LDAP for TeamForge User Authentication
keywords: saml,ldap, external authentication, identity management, single sign on, SSO, intermediate
tags: [ctf_20.2, sso, authentication, site_admin_tasks, saml, ldap]
sidebar: teamforge_sidebar
folder: teamforge
permalink: saml-ldap-authentication.html
last_updated: Jul 13, 2020
summary: By setting up the SAML+LDAP IdP, TeamForge users can reap the benefits of both SAML and LDAP authentication mechanisms in a unified manner. With SAML+LDAP authentication, while SAML enables TeamForge users to access web applications, the LDAP authentication supports user authentication required for CLI applications. For example, if a user performs a source code commit in Git/SVN repository, the user can get authenticated via LDAP.
---
To set up SAML+LDAP authentication, you must set up the SAML and LDAP configurations as discussed later in this topic and then select **SAML+LDAP** as the IdP.

**One E-mail Address--Multiple User Accounts: Intermediate Login Page**

In a SAML enabled and SAML+LDAP enabled environment, if you have multiple user accounts for the same email address, you will be redirected to an intermediate login page before the third party IdP for authentication. In this intermediate login page, you can see the list of accounts associated with your email address. Select one of the user accounts from the list, which would be the default user account used for authentication by the third party IdP for your subsequent logins. 

After you have set a default account, you are not taken to the intermediate login page the next time you log on. If you want to change or reset the default user account at any point in time, you can do so from the **My Settings > Edit User Information** page.

{% include image.html file="defaultuser-intermediatelogin.PNG" %}

 1. Set up SAML and LDAP integrations. See:

    * [Set up SAML][saml]
    * [Set up LDAP][ldap-authentication]

 2. Log on to TeamForge as a Site Administrator.

 3. Select **My Workspace > Admin**.

 4. Select **Projects > Identity**.

 5. Select the **Federation** tab.

 6. Select the **Use Federated Login** check box and select **SAML+LDAP** as the IdP from the drop-down list.

    {% include image.html file="saml-ldap.png" %}

 7. Click **Save**.


{% include links.html %}