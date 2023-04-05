---
title: External Authentication Overview
keywords: external authentication, saml, ldap 
tags: [ctf_20.2, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: identityinfo.html
last_updated: Jul 13, 2020
summary: TeamForge enables user authentication both against its internal database and against other external authentication services such as LDAP, OAuth, and SAML. This section provides information on how to set up TeamForge for authenticating its users against these services.  
---
TeamForge supports the following identity management frameworks: 

* [OAuth 2.0 Authorization Framework][teamforgeoauth]

  With the new TeamForge Identity Management built on OpenID Connect (OIDC) and OAuth 2.0 authorization frameworks, TeamForge can now act as an ID Provider (IdP). As an IdP, TeamForge can authorize a third-party client application to obtain limited access to its services either on behalf of a Resource Owner (user) or on behalf of the client application itself.
* [SAML][saml]

  SAML is an XML-based open standard developed by OASIS Security Services Technical Committee. It defines a framework to perform web browser SSO using secure tokens for exchaning security information between web applications.
* [LDAP][ldap-authentication]

  LDAP (Lightweight Directory Access Protocol) is an application protocol that works on a layer on top of the TCP/IP stack and accesses your directory service providers such as Active Directory for providing user authentication. For more details on LDAP, see [RFC2251 - Light-weight Directory Access Protocol (v3)](https://datatracker.ietf.org/doc/rfc2251/).
* [SAML+LDAP][saml-ldap-authentication]

  With SAML+LDAP IdP, the TeamForge users can reap the benefits of both SAML and LDAP authentication mechanisms in a unified manner. With SAML+LDAP authentication, while SAML enables TeamForge users to access web applications, the LDAP authentication supports user authentication required for CLI applications. For example, if a user performs a source code commit in Git/SVN repository, the user can get authenticated via LDAP.

{% include links.html %}