---
title: login-config.xml
keywords: authencation, login-config
tags: [installation, upgrade, site-options.conf, config_files, ldap, authentication]
sidebar: teamforge_sidebar
permalink: login-config.html
last_updated: Feb 16, 2018
toc: false
summary: This is the sample application-policy block that you can copy into your login-config.xml file to support LDAP authentication.
---

## Notes

Replace the default application-policy block of the login-config.xml file with this code, then make the modifications specified in [Set up LDAP integration for the TeamForge Site][ldap-authmanager.html#ldapforteamforge]. Option values that must be modified are highlighted in bold.

 * When the username is passed to the login module from TeamForge, it is translated into a DN for lookup on the LDAP server. The DN that is sent to the LDAP server is `<principalDNPrefix><username><principalDNSuffix>`.

 * In this example `application-policy` block, the username is stored in the People organizational unit in the `dev.sf.net` domain. This is represented as ,`ou=People,dc=dev,dc=sf,dc=net`

 * This example contains a single login-module section. If you are authenticating against multiple LDAP servers, include one `login-module` section per LDAP server, with the required option values modified appropriately for each one. If the same username exists in more than one LDAP server, the instance on the first LDAP server will be used.


## Sample Code

```shell
 <application-policy name="SourceForge">
   <authentication>
     <login-module code="org.jboss.security.auth.spi.LdapLoginModule" flag="sufficient" >
       <module-option name="allowEmptyPasswords">false</module-option>
       <module-option name="principalDNPrefix">uid=</module-option>
       <module-option name="principalDNSuffix">,ou=People,dc=dev,dc=sf,dc=net</module-option>
       <module-option name="java.naming.factory.initial">com.sun.jndi.ldap.LdapCtxFactory</module-option>
       <module-option name="java.naming.provider.url">ldap://util.dev.sf.net:389/</module-option>
       <module-option name="java.naming.security.authentication">simple</module-option>
     </login-module>
   </authentication>
 </application-policy>
```` 

## Sample Code for Active Directory Integration

Active Directory is not supported. However, these sample lines in the login-config.xml file may help you make it work for a simple AD setup, without complex directory structures requiring additional search parameters.

Set the values of `java.naming.provider.url`, `principalDNSuffix` and `rolesCtxDN` as appropriate to your site.

For more detailed instructions, see http://www.jboss.org/community/wiki/LdapLoginModule.

```shell
<login-module code="org.jboss.security.auth.spi.LdapLoginModule" flag="required" >
 <module-option name="java.naming.provider.url">ldaps://<server_name>:636/</module-option>
 <module-option name="allowEmptyPasswords">false</module-option>
 <module-option name="principalDNSuffix">@foo.bar.com</module-option>
 <module-option name="rolesCtxDN">dc=Foo,dc=Bar,dc=Com</module-option>
 <module-option name="matchOnUserDN">true</module-option>
 <module-option name="uidAttributeID">sAMAccountName</module-option>
 <module-option name="roleAttributeID">memberOf</module-option>
 <module-option name="roleAttributeIsDN">true</module-option>
 <module-option name="roleNameAttributeID">name</module-option>
</login-module>
````

{% include links.html %}