---
title: Use LDAP for TeamForge User Authentication
keywords: ldap, external authentication, identity management, single sign on, SSO
tags: [ctf_20.2, authentication, site_admin_tasks, sso, ldap]
sidebar: teamforge_sidebar
folder: teamforge
permalink: ldap-authentication.html
last_updated: Jul 13, 2020
summary: TeamForge supports integration with LDAP. Once integrated with LDAP servers, TeamForge can use LDAP credentials for user authentication.
---

<div class="well-lg well" markdown="1">
<b>LDAP (Lightweight Directory Access Protocol)</b> is an application layer protocol that works on top of the TCP/IP stack and accesses your directory service providers such as Active Directory for providing user authentication. For more information, see <a href="https://datatracker.ietf.org/doc/rfc2251/">RFC2251 - Light-weight Directory Access Protocol (v3)</a>.
</div>

## Enable LDAP as an IdP

This section walks you through the steps to enable LDAP as an IdP in TeamForge.

1. Log on to TeamForge as a Site Administrator.
2. Select **My Workspace > Admin**.
3. Select **Projects > Identity**.
4. Select the **Federation** tab.
5. Select the **Use Federated Login** check box and select _LDAP_ as the IdP from the drop-down list.
6. Click **Save**.
   {% include image.html file="ldap-idp.png" %}


## TeamForge-LDAP Authentication--Single LDAP Server Setup {#setupteamforgeforldap}

In this section, you can see the configuration required for setting up TeamForge for authentication using a single LDAP server.

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">

* Once you have your LDAP server set up, you must configure the following `site-options.conf` tokens in TeamForge before integrating TeamForge with an LDAP server. Use your discretion and configure these tokens to suit your site's requirements.

  * [USE_EXTERNAL_USER_AUTHENTICATION][siteoptiontokens.html#USE_EXTERNAL_USER_AUTHENTICATION]=true
  * [APPROVE_NEW_USER_ACCOUNTS][siteoptiontokens.html#APPROVE_NEW_USER_ACCOUNTS]=false
  * [REQUIRE_PASSWORD_SECURITY][siteoptiontokens.html#REQUIRE_PASSWORD_SECURITY]=false
  <!-- * [LINUX_USERNAME_MODE_ENABLED][siteoptiontokens.html#LINUX_USERNAME_MODE_ENABLED]=true -->
  * [MINIMUM_PASSWORD_LENGTH][siteoptiontokens.html#MINIMUM_PASSWORD_LENGTH]=0
  * [PASSWORD_REQUIRES_MIXED_CASE][siteoptiontokens.html#PASSWORD_REQUIRES_MIXED_CASE]=false
  * [PASSWORD_REQUIRES_NON_ALPHANUM][siteoptiontokens.html#PASSWORD_REQUIRES_NON_ALPHANUM]=false
  * [PASSWORD_REQUIRES_NUMBER][siteoptiontokens.html#PASSWORD_REQUIRES_NUMBER]=false
  * [REQUIRE_USER_PASSWORD_CHANGE][siteoptiontokens.html#REQUIRE_USER_PASSWORD_CHANGE]=false

* In addition to the above tokens, configure the [ALLOW DATABASE AUTHENTICATION IF LDAP IS ENABLED][siteadmin-configuresiteviaui.html#allowdatabaseauthifldapenabled] parameter. To select this check box, select **My Workspace > Admin** and select **Projects > System Tools > Configure Application**. This parameter is listed in the **External Authentication** section. Select the ALLOW DATABASE AUTHENTICATION IF LDAP IS ENABLED check box to have LDAP credentials stored in TeamForge and have users authenticated via TeamForge every time a user logs in. This helps improve performance by optimizing the number of authentication calls between the TeamForge and LDAP servers.

  <!-- {% include important.html content="Selecting this option is mandatory for sites with internally managed CVS servers." %} -->

* If you have enabled database authentication, LDAP user credentials are stored when users login for the first time and continue to login using the locally stored LDAP credentials. However, you can restrict such indefinite usage of the stored LDAP credentials and force user re-authentication at regular intervals by setting up this configuration parameter. For example, setting a value of `24` would force user re-authentication (by the LDAP server) every 24 hours. For more information, see [FORCE RE-AUTHENTICATION WITH LDAP SERVER][siteadmin-configuresiteviaui.html#forcereauthwithldap].
</div>
</div>

1. Log on to TeamForge as a Site Administrator.

2. Select **My Workspace > Admin**.

3. Select **Projects > Identity**.

4. Select the **LDAP** tab. This tab lets you configure the TeamForge-LDAP integration.

   <!-- Use this for web output -->
   {% unless site.output == "pdf" %}
   [![LDAP Configuration](images/ldap-configuration.png)](images/ldap-configuration.png)
   {% endunless %}

   <!-- Use this for pdf output -->
   {% unless site.output == "web" %}
   {% include image.html file="ldap-configuration.png" %}
   {% endunless %}

   <br>
  
   <table>
   <tr>
   <th>Fields</th>
   <th>Description</th>
   </tr>
   <tr>
   <td>LDAP NAME</td>
   <td>Descriptive name for each LDAP configuration set.</td>
   </tr>
   <tr>
   <td>PROVIDER URL</td>
   <td>The string that encapsulates the IP address and port of a directory server.</td>
   </tr>
   <tr>
   <td rowspan="7">SECURITY AUTHENTICATION</td>
   <td rowspan="7" markdown="1">The authentication method used to bind to the LDAP server. There are 3 types of security authentication in LDAP:<br><br>

    * **Anonymous** - When a client sends a LDAP request without binding, then it is called an "anonymous client".<br>
    * **Simple** - In this type of authentication, the LDAP server sends the fully qualified DN (Distinguished Name) and the clear text password of the client.<br>
    * **SASL** - SASL (Simple Authentication and Security Layer) authentication provides a challenge response protocol to exchange data between the client and server for the authentication and establishment of security layer to carry out further communication.
      {% include note.html content="TeamForge supports only one of the authentication methods, which is **Simple**." %}
   </td>
   </tr>
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr>
   <td rowspan="3">SECURITY PRINCIPAL</td>
   <td rowspan="3">The distinguished name of the user to authenticate.<br><br>Example: "uid=admin,ou=accounts"</td>
   </tr>
   <tr></tr>
   <tr></tr>
   <tr>
   <td>SECURITY CREDENTIALS</td>
   <td>The password or other security credentials of the user to authenticate.</td>
   </tr>
   <tr>
   <td colspan="2" markdown="1"> 
   {% include note.html content="Select the `<<token_name>>` check box in the [Configure Your Site's Settings][siteadmin-configuresiteviaui] page to mandate the use of Security Principal and Security Credentials when a LDAP user tries to log on to TeamForge for the first time." %} 
   </td>
   </tr>
   <tr>
   <td rowspan="3">BASE DN</td>
   <td rowspan="3">The base distinguished name from where a server will search for users. This is a sequence of related distinguished names connected by commas and with the format "attribute=value". <br><br>Example: dc=help,dc=collab,dc=net</td>
   </tr>
   <tr></tr>
   <tr></tr>
   <tr>
   <td>USERNAME ATTRIBUTE</td>
   <td markdown="1">
   Attribute name to be used to match the username provided in the UI. <br><br>
   Example: sAMAccountName (for Active Directory). 
   {% include note.html content="Please contact LDAP administrator for more information." %}
   </td>
   </tr>
   <tr>
   <td>SEARCH TIMEOUT</td>
   <td>The read timeout in milliseconds for an LDAP operation. This is used to control the LDAP request made by a client in a timely manner, so that the client need not wait for a long time for the server to respond. For example, if the search timeout value is 5000 milliseconds, the LDAP service provider can abort the read timeout if the server does not respond within this 5 seconds.</td>
   </tr>
   <tr>
   <td rowspan="5">SEARCH SCOPE</td>
   <td rowspan="5" markdown="1">The starting point of an LDAP search and the depth from the base DN to the levels until which the search should occur. There are three types of search scope in an LDAP search: <br><br>
   * **OBJECT_SCOPE:** This limits the search scope only to the base object or base DN. <br><br>
   * **ONELEVEL_SCOPE:** This enables search only up to the immediate children objects under the base DN in a search tree.<br><br>
   * **SUBTREE_SCOPE:** This searches the entire subtree including the base DN. TeamForge recommends this as the default search scope in its LDAP configuration.
   </td>  
   </tr>  
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr></tr>
   <tr>
   <td>BASE FILTER</td>
   <td>The group DN in which the users are member of. Sets the LDAP default search filter for the users to search and load all users from the database of active user accounts belonging to a specific OU (organizational unit) provided in the search filter. This is an optional field. <br>
   <b>Example value</b>: <i>(&amp;(sAMAccountName={0})(objectCategory=account)(objectClass=user))</i></td>
   </tr>
   </table>

8. Click **Save**.

If you have issues with a specific LDAP setup, you can disable the LDAP authentication (Click **Disable**) to troubleshoot and fix the issues.

## TeamForge-LDAP Authentication--Multiple LDAP Servers Setup {#setupteamforgewithmultipleldap}

You can configure multiple LDAP servers for authentication with TeamForge 18.1 and later.  

1. Log on to TeamForge as a Site Administrator.

2. Select **My Workspace > Admin**.

3. Select **Projects > System Tools > Configure Application**.

4. Set the number of LDAP servers in the [LDAP CONFIGURATIONS MAXIMUM LIMIT][siteadmin-configuresiteviaui.html#ldapconfigmaxlimit] parameter (in **External Authentication** section).

5. Select **Projects > Identity**.

6. Select the **LDAP** tab.

7. Add as many LDAP servers as required (click the {% include inline_image.html file="ldap-add.png" %} icon) and configure individual LDAP servers as discussed in [Set up TeamForge for Single LDAP Server Authentication][ldap-authentication.html#setupteamforgeforldap]. 

   {% include image.html file="configure-multiple-ldaps.png" %}

8. Click **Save**.



{% include links.html %}