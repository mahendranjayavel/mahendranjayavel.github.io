---
title: FAQs on Security
keywords: FAQ, frequently asked questions
tags: [faq, ldap, security, selinux, role_based_access_control, saml, ldap, oauth, ssl]
sidebar: teamforge_sidebar
permalink: security-faqs.html
last_updated: Jun 30, 2020
summary: These are some of the frequently asked questions on security.
---

## What are the implications of deprecating TLS protocol versions 1.0 and 1.1?
<!-- artf395000/[artf414563] TLS v1.0, 1.1 deprecation, implications for all previous CTF versions -->

In addition to security vulnerabilities, TLS protocol versions 1.0 and 1.1 do not support modern cryptographic algorithms. The software industry (including popular browsers such as Chrome, FireFox and so on) is set to deprecate the TLS protocol versions 1.0 and 1.1 by March 2020 and so is TeamForge. Customers are therefore advised to upgrade your sites to be able to negotiate with TLS 1.2 connections. Upgrade your clients to the latest version in case you face any SSL handshake issues while connecting to TeamForge.

With this move to deprecate TLS protocol versions 1.0 and 1.1, we must fix the `SSLProtocol` and `SSLCipherSuite` options in the `/etc/httpd/conf/httpd.conf` file and restart the Apache server.

```shell
SSLProtocol             all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
SSLCipherSuite          ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
````

Do this where you have Apache running. For example, TeamForge application server and Subversion servers have Apache.

You can also have this fixed permanently by setting up the `SSL_PROTOCOL` and `SSL_CIPHER_SUITE` `site-options.conf` tokens for TeamForge 18.1 and later.

```shell
SSL_PROTOCOL= all -SSLv3 -TLSv1 -TLSv1.1
SSL_CIPHER_SUITE=ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384

teamforge provision
````
{{site.data.alerts.hr_shaded}}

## What are the security features available in TeamForge?
TeamForge is equipped with a number of security features, which include:
* SELinux Support 
* SSL Support 
* Site option tokens to enforce password control policies
* Automatic password creation and encryption
* Password obfuscation
* Prevention of cross-site scripting
* Role Based Access Control (RBAC) and Path Based Permissions (PBP)
* Size restriction for document uploads
* Document safe download mode
* Incorrect login attempts-account lock feature
* SCM_DEFAULT_SHARED_SECRET to allow SCM Integrations to securely communicate with TeamForge
* Support for OAuth/LDAP/SAML
* Restrict domains for CSRF, Prohibit harmful file uploads
{{site.data.alerts.hr_shaded}}

## After switching to ADS authentication, why did the Create button disappear from the user admin section?

When using external authentication such as LDAP, creating users from within the application is disabled. All users must be created via LDAP.

See [login-config.xml][login-config] for more information.
{{site.data.alerts.hr_shaded}}

## Can I block project data from public search engines?

Yes, edit the robots.txt file to specify the pages or directories that should not be indexed by search engines.

If your site has some content that you may not want to be publicly searched for, or if some search engine hits are causing the site to slow down, you can make this change.

Only one robots.txt file can be created for a site. This file can contain a list of url patterns that should not be indexed, against the web crawler name.

The default robots.txt is available in the SITE_DIR/var folder. The robots.txt file is accessible without logging into Digital.ai TeamForge, via the `domain/robots.txt` URL. You can update and commit the robots.txt file into the branding root directory, and the system then places the file in the `SITE_DIR/var/overrides` folder.

 {% include tip.html content="You must have the commit permissions to create a robots.txt file under the branding repository in the Look Project." %}
{{site.data.alerts.hr_shaded}}

## How can I enforce strong passwords?

You can configure the application to reject passwords that do not meet your security criteria.

To enforce password requirements, place the following lines in `/opt/collabnet/teamforge/sourceforge_home/etc/sourceforge_configation.properties` file.

```shell
system.password.min-length=5
password.requiresNumber=true
password.requiresNonAlphaNum=true
password.requiresMixedCase=true
````

Once these lines are in place, restart TeamForge for them to take effect. The above example would require a password of at least 5 characters that must include at least one (1) mixed case letter, at least one (1) number, and at least one non-alphabetic character, e.g. Us3r!

{% include note.html content="These settings apply only to new passwords. Anyone in the system currently will be able to continue to use their existing, potentially weak, password. You should force all users to change their passwords after changing these." %}
{{site.data.alerts.hr_shaded}}

## How do I configure Subversion to authenticate against multiple LDAP domains?

For some configurations, a Subversion server may need to be authenticated against multiple LDAP domains. This is possible by modifying the Apache configuration.

This is now possible due to the mod_authn_alias module for Apache. The external link for the module contains multiple usage scenarios. You will need to confirm that your Apache has been compiled with the module enabled. (This is the case for CollabNet Subversion binary packages since 1.5.4). If it is compiled as a module, make sure it is enabled via the LoadModule directive in your Apache configuration.

Example for configuration usage for authentication against three LDAP servers :

```shell
<AuthnProviderAlias ldap ldap-US>
    AuthLDAPBindDN cn=ldapuser,o=company
    AuthLDAPBindPassword password
    AuthLDAPURL ldap://ldap-us.company.local/ou=Developers,o=company?sub?(objectClass=*)
</AuthnProviderAlias>

<AuthnProviderAlias ldap ldap-EU>
    AuthLDAPBindDN cn=ldapuser,o=company
    AuthLDAPBindPassword password
    AuthLDAPURL ldap://ldap-EU.company.local/ou=Developers,o=company?sub?(objectClass=*)
</AuthnProviderAlias>

<AuthnProviderAlias ldap ldap-IN>
    AuthLDAPBindDN cn=ldapuser,o=company
    AuthLDAPBindPassword password
    AuthLDAPURL ldap://ldap-in.company.local/ou=Developers,o=company?sub?(objectClass=*)
</AuthnProviderAlias>

<Location /svn>
    DAV svn
    SVNParentPath /opt/subversion/repos
    AuthType Basic
    AuthName "Subversion Repository"
    AuthBasicProvider ldap-US ldap-EU ldap-IN
    AuthzLDAPAuthoritative off
    Require valid-user
</Location>
````
{{site.data.alerts.hr_shaded}}

## How do I authenticate multiple LDAP via Apache?

If you need to add multiple OU= values in the LDAP url you must have separate LDAP urls and utilize AuthnProviderAlias to check both LDAP searches.

Use the following AuthnProviderAlias to check LDAP searches.

```shell
LoadModule authn_alias_module 
modules/mod_authn_alias.so
                
<AuthnProviderAlias ldap ldap-alias1>
AuthLDAPBindDN cn=youruser,o=ctx
AuthLDAPBindPassword yourpassword
AuthLDAPURL ldap://ldap.host/o=ctx
</AuthnProviderAlias>
                
<AuthnProviderAlias ldap ldap-other-alias>
AuthLDAPBindDN cn=yourotheruser,o=dev
AuthLDAPBindPassword yourotherpassword
AuthLDAPURL ldap://other.ldap.host/o=dev?cn
</AuthnProviderAlias>
                
Alias /secure /webpages/secure
<Directory /webpages/secure>
Order deny,allow
Allow from all
                
AuthBasicProvider ldap-other-alias ldap-alias1
                
AuthType Basic
AuthName LDAP_Protected_Place
AuthzLDAPAuthoritative off
Require valid-user
</Directory>     
````  
{{site.data.alerts.hr_shaded}}

## Can the users be forced to change their passwords at first login?

Yes, as a site administrator you can configure the Digital.ai TeamForge site options to force the users to change their passwords at first login.

Setting the `REQUIRE_USER_PASSWORD_CHANGE` attribute as `true` in the `site-options.conf` file enforces password change on first login into Digital.ai TeamForge.

 {% include note.html content="You can not force password change on a user who had self-created the user account, or if a password-request had been raised for the user or if an administrator had reset the login password for that user." %}
{{site.data.alerts.hr_shaded}}

## Does TeamForge work with LDAP?

Yes, you can have your TeamForge installation authenticate against an LDAP server.

This is handy when users want to use a variety of different resources without having to maintain credentials for each one separately.

### Overview

Digital.ai TeamForge is a JBoss2 based application and relies on the JBoss JAAS service for user authentication. This enables a TeamForge site to authenticate users internally or externally.

### Internal User Authentication

Out of the box, TeamForge relies on its local database to manage user accounts. This includes username, password, full name, email address and a variety of other meta data values. Passwords are stored in the database using the standard MD5 Password hashing algorithm1. The database is only accessible by the application itself and a user with root access to the physical server. While running in this default configuration users are allowed to change their passwords in TeamForge, and any user with site administration privileges can create and approve new user accounts.


### External User Authentication

The JAAS service comes with several standard providers that allow TeamForge to be integrated with services such as LDAP, Active Directory and Kerberos. The JAAS service allows more than one source to be configured in the event several sources are needed.

 {% include note.html content="It is possible to use both types of authentication with a single TeamForge installation. See your CollabNet representative for details." %}

To ensure that you are not locked out of your site, the site administrator account is always validated by TeamForge, not by LDAP.

LDAP accounts must conform to the TeamForge rules for user names and passwords. For example:

 * If a password is used in LDAP that is shorter than the minimum allowable password length in TeamForge, you cannot create the user in TeamForge.

 * A user name that starts with a special character, such as an underscore, will not be accepted by TeamForge, even if it is valid in LDAP.

(For detailed TeamForge user name and password rules, see [Create a New User Account][createasingleuseraccount]).

### How is life different for the user under external authentication?

* When you turn external integration on, every user account (except the site administrator account) must have a matching LDAP entry to log in. This may require changing some existing accounts to match their corresponding LDAP records. (Accounts created after LDAP is in place are validated with the LDAP server when they are created, so you don't have to worry about this.)

* Every login attempt (Web UI and SOAP access) is passed to the external provider. This means that any changes to the user status in the external system take effect immediately. Users who have already logged in and have valid sessions are not affected.

* When TeamForge is using internal authentication, a site administrator can change a user's password. This is disabled for external authentication.

* Under external authentication, passwords can't be changed in the TeamForge web UI. Users have to use the interface provided by the third-party authentication source to change their password. Such password changes are available immediately to TeamForge for the next login attempt.

* Site administrators can no longer create user accounts. The end user must create their own account by logging into TeamForge just like a user who already has an account. At that point TeamForge detects that a new account needs to be created and presents the new user with a registration form, which requests the user's password n the external authentication system. On submit, TeamForge verifies the user account with the external system, and only if the username/password is verified does TeamForge create the new account.

* Once a new user has created their account, TeamForge can optionally be configured to put every new account in a pending status so that a site administrator can approve the new account. By default, new users will have immediate access to the system.

### LDAP for Source Control

LDAP is integrated into your TeamForge source control services.

For Subversion, the integration server queries TeamForge as needed.

### What can go wrong?

When TeamForge is configured to authenticate against an LDAP server and the LDAP server is down, all TeamForge authentication is disabled until the LDAP server is restored.

If a user does not exist on the LDAP server, or is deleted from the server, that user cannot log into TeamForge.
{{site.data.alerts.hr_shaded}}


## Why do I get the "Invalid command 'AuthLDAPAuthoritative'" error when I try to set LDAP for SVN users?

The invalid command `AuthLDAPAuthoritative` error may occur if you need to upgrade Apache from version 2.0 to 2.2.

CollabNet Subversion 1.5 is bundled with the latest version of Apache (currently 2.2.x). It includes the module mod_authnz_ldap and does not include mod_auth_ldap. Hence compatibility issues arise due to missing directives. Upgrade your Apache version to 2.2 if you get the following error when trying to install CollabNet SVN:

```shell
 bash-3.00# /etc/init.d/collabnet_subversion start
    Starting CollabNet Subversion:
    Syntax error on line 29 of 
        /etc/opt/CollabNet_Subversion/conf/collabnet_subversion_httpd.conf:
    Invalid command 'AuthLDAPAuthoritative', 
        perhaps misspelled or defined by a module not included in the server configuration
    FAILED 
```
{{site.data.alerts.hr_shaded}}

## How does TeamForge handle multiple redundant LDAP servers?

When configuring LDAP authentication for a TeamForge instance, there may be a business need for using multiple LDAP servers.

Follow the guidelines below for configuring.

The additional LDAP servers can be added to the `java.naming.provider.url` option in `login-config.xml`:

```shell
login-config.xml:
    <module-option name="java.naming.provider.url"> 
    ldap://primary/ ldap://secondary/</module-option>
````

Once the primary and secondary servers have been defined, they will be consulted in order of definition for every authentication request. First the primary, and if the primary fails, then the secondary. This prevents specifying multiple servers for round-robin handling of authentication, but it can still be used for redundancy needs.
{{site.data.alerts.hr_shaded}}

## What user activities are tracked?

In case of a data security compromise, a record of who is performing what activities will help resolve some of the security issues.

Typically web servers log every page (or URL) being accessed, including the IP address of the user, date and time of access, etc. These logs are very useful in tracking the source of any security violations that may occur.

Digital.ai TeamForge auditing tools are a powerful way to track unwanted and/or unauthorized changes within the system.
{{site.data.alerts.hr_shaded}}

### J2EE Architecture and Security

Digital.ai TeamForge is a J2EE application that employs three-tier architecture to provide a secure environment for mission-critical data.

In a multi-tier architecture, access to each tier is restricted to the tier above it, effectively securing the tiers behind the firewall. For example, while clients (users accessing the system through a web) access the web server, they neither have access to the application and backend servers nor are they aware of their existence.

Similarly, the web server itself does not have access to the backend servers (database, SCM, mail etc.)

Exceptions to this rule include:

 * Direct client access provided to the SCM servers. SCM servers are accessed across the firewall typically through SSH protocol, or HTTP or HTTPS (for Subversion). SCM server data is also accessible in a view only mode through the web interface.

 * Clients must have access to the mail server for posting messages to mailing lists.

 * Mail server must have access to deliver messages across the firewall.

Clients can also access the SOAP APIs through the web server. The web server in turn forwards SOAP requests to the application server for processing.
{{site.data.alerts.hr_shaded}}

## With self signed certificates in place, what is the recommended protocol (SSH or HTTPS) to use while cloning a Git repository from a TeamForge Git server running on RHEL/CentOS?

When using a self-signed certificate on a Teamforge Git server, you cannot clone a repository using the standard git client on RHEL/CentOS.

In RHEL/CentOS, the Linux certificates used by git and other tools are stored in the `/etc/pki/tls/certs/ca- bundle.trust.crt` file. This file is managed by the RPM package system. If a certificate is added to the ca-bundle.trust.crt file, Trusted Root Certification Authority updates are not installed automatically which in turn leaves the system vulnerable to potential attacks.

An alternative way for adding trusted certificates is available at http://stackoverflow.com/questions/9072376/configure-git-to-accept-a-particular-self-signed-server-certificate-for-a-partic. However, it appears that some tools do not read files outside of the main bundle.

Therefore, it is recommended to use SSH protocol while cloning a git repository from a TeamForge Git server running on RHEL/CentOS.
{{site.data.alerts.hr_shaded}}

## Do I have to use the password provided by administrator always?

No, you don't have to use the password provided by administrator beyond your first login into Digital.ai TeamForge.

The site administrator may have provided you with a user name and password after creating your user account in Digital.ai TeamForge. When you login using those credentials, you might be asked to change your password for security reasons. At this time, you can set a password of your choice.

{% include tip.html content="You will not be asked to change your password if you had created your own account, or if a password-request had been raised for you or if an administrator had reset your password." %}

{% include links.html %}