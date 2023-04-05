---
title: Join a TeamForge Site
keywords: log into TeamForge, log in, log on
tags: [getting_started, users, license]
sidebar: teamforge_sidebar
permalink: getstarted-joinasite.html
last_updated: May 31, 2019
summary: To collaborate with others on a Digital.ai TeamForge site, start by getting a user account.
---

The process of joining a TeamForge site varies according to your site's setup. Here's what you should consider before you join a TeamForge site:
* Is user self-registration allowed on your site?
  User self-registration is, by default, disabled in TeamForge. However, TeamForge site administrators may choose to enable user self-registration. Such self-registered user accounts are later approved by the site administrator. For more information, see [DISABLE_USER_SELF_CREATION][siteoptiontokens.html#DISABLE_USER_SELF_CREATION] and [APPROVE_NEW_USER_ACCOUNTS][siteoptiontokens.html#APPROVE_NEW_USER_ACCOUNTS].
* How is your TeamForge site authenticating users?
  TeamForge supports user authentication both against its internal database and against other external authentication services such as LDAP, OAuth, and SAML. The account creation procedure varies according to the authentication setup. 

  Refer to the relevant instructions in this topic that suit your site's setup.

{% include note.html content="You need a license to use TeamForge. Your site administrator may have already assigned you a license. If you are self-registering, you'll be asked to choose the type of license you need when you create your account. For more information about TeamForge license, see [TeamForge License][teamforgelicense]." %}

## Sites that Use TeamForge's Internal Database Authentication

User self-registration is, by default, disabled in TeamForge. In such cases, user accounts can only be created by TeamForge administrators and users would get an email notification with a link to log on to TeamForge.

Follow these steps if your site uses TeamForge's internal database for authentication and if user self-registration is enabled.
1. Click **Create an Account** in the **New Users** section of the TeamForge home page.
2. On the **Create New Account** page, enter a username for your account.

   <div class="well well-sm" markdown="1">
      Your user name must meet these criteria:
      * User name is case sensitive.
      * Minimum number of characters as specified in the site-options.conf file.
      * No spaces.
      * Should have at least one letter.
      * The first character is a letter.
    </div>
3. Enter and confirm a password.
4. Fill in the rest of the fields and click **Create**.

   Your user account is now created, pending approval by a TeamForge site administrator. Once approved, you will get an email notification with a link to log on to TeamForge. 

3. Follow the link in the email to log on to TeamForge.

## Sites that Use LDAP Authentication

Follow these steps if your TeamForge site uses LDAP authentication. 
1. In the **Log Into TeamForge** section of the TeamForge home page, enter your corporate LDAP username and password.
      {% include tip.html content="In most cases, your username and password are the username and password with which you log in to your corporate network." %}
2. Click **Log In**.
3. On the **Create Account** page, re-enter your LDAP password.
4. Enter your full name and email address and click **Create**.
   {% include note.html content="The TeamForge Administrator receives an email notification to approve the new account that you've created. Once approved, you will get an email notification with a link to log on to TeamForge." %}
5. Follow the link in the email to log on to TeamForge.   

## Sites that Use SAML/SAML+LDAP Authentication

Follow these steps if your TeamForge site uses SAML or SAML+LDAP authentication.
1. In the **Log In to TeamForge** section of the TeamForge home page, click **Log In**. 
2. On the third-party Identity Provider's (IdP) login page, enter the username and password provided by your third-party IdP.
3. Click **Sign In**. 
4. On the **Create New Account** page, enter the password and other user details.
   {% include note.html content="Your user name and email address fields cannot be edited on the **Create New Account** page." %}
5. Click **Create**.
   {% include note.html content="The TeamForge Administrator receives an email notification to approve the new account that you've created. Once approved, you will get an email notification with a link to log on to TeamForge." %}
6. Follow the link in the email to log on to TeamForge.


{% include links.html %}