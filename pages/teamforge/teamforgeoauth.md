---
title: Use OAuth 2.0 for TeamForge User Authentication
keywords: OAuth 2.0, identity management, openid connect, oidc, grant types, authorization, authentication, single sign on, SSO
tags: [ctf_20.0, sso, authentication, site_admin_tasks, oauth, REST]
sidebar: teamforge_sidebar
permalink: teamforgeoauth.html
last_updated: Jan 11, 2020
summary: With the new TeamForge Identity Management built on OpenID Connect (OIDC) and OAuth 2.0 authorization frameworks, TeamForge can now act as an ID Provider (IdP). As an IdP, TeamForge can authorize a third-party client application to obtain limited access to its services either on behalf of a Resource Owner (user) or on behalf of the client application itself.
---
This topic discusses TeamForge OAuth architecture, scopes, supported authorization grant types, Federated Identity Management in TeamForge, and so on. This topic also discusses step by step how to add a client application that wants to access TeamForge's services.

## TeamForge OAuth Nomenclature {#oauthnomenclature}

{% include important.html content="It is assumed that you are familiar with the OAuth 2.0 and OpenID Connect frameworks, terms and concepts. It's recommended that you read [The OAuth 2.0 Authorization Framework RFC 6749](http://tools.ietf.org/html/rfc6749) and get familiar with **OAuth Roles**, **Protocol Flow**, **Access Tokens**, **Grant Types**, **Client Types** and so on before you proceed." %}

Here's a list of links and references for further reading.

| Term | Description |
|-------|-------------|
| OAUTH | [The OAuth 2.0 Authorization Framework RFC 6749](http://tools.ietf.org/html/rfc6749) |
| OIDC | [OpenID Connect Core 1.0](http://openid.net/specs/openid-connect-core-1_0.html) |
| BEARER TOKEN | [The OAuth 2.0 Authorization Framework: Bearer Token Usage RFC 6750](http://tools.ietf.org/html/rfc6750) |
| SAMLBEARER | [SAML 2.0 Bearer Assertion Profiles for OAuth 2.0](https://tools.ietf.org/html/draft-ietf-oauth-saml2-bearer-12) |
| JWE | [JSON Web Encryption (JWE)](https://tools.ietf.org/html/draft-ietf-jose-json-web-encryption-40) |
| JWS | [JSON Web Signature (JWS)](https://tools.ietf.org/html/draft-ietf-jose-json-web-signature-41) |
| JWT | [JSON Web Token (JWT)](https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32) |
| JWA | [JSON Web Algorithms (JWA)](https://tools.ietf.org/html/draft-ietf-jose-json-web-algorithms-40) |
| JWK | [JSON Web Key (JWK)](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-41) |

## TeamForge OAuth Overview

In the traditional client-server authentication model, client applications must have access to the Resource Owner's credentials in order to request and access protected resources on the Resource Server. Sharing Resource Owner's credentials such as user names and passwords to third party applications poses several problems, security being one of the major ones. 

Frameworks such as the OAuth 2.0 and OpenID Connect help in mitigating such security risks and hence TeamForge's authentication model has been rebuilt on top of OpenID Connect and OAuth 2.0 Authorization frameworks.

### TeamForge OAuth Roles
TeamForge OAuth authorization process involves interaction between four entities (roles) such as the user, IdP, SP and client application. The following table lists the roles that an entity can assume in the TeamForge OAuth setup.

| Entity/Role | OAuth Term | OIDC Term | SAML Term | Description |
|------|------------|-----------|-----------|-------------|
| User | Resource Owner | End-User | User | Human or machine that intends to access a resource of an SP.<br><br>Users are, in general, humans. If a machine acts as a user, it is called `Agent`. |
| Service Provider (SP) | Resource Server | Relying Party | Service Provider, Relying Party | Entity that demands authentication to grant access to some resource. <br><br>The SP trusts the IdP to perform the authentication on its behalf. |
| Client | Client | - | Browser | Application interacting with SP and IdP on the user’s behalf.|
| Identity Provider (IdP) | Authorization Server | Provider | Identity Provider, Asserting Party| Entity that proves, identifies and authenticates a user. |

### OAuth 2.0 Abstract Protocol Flow

The following illustration shows the OAuth 2.0 protocol flow.

{% include image.html file="oauth2.png" %}

* (A) The client application requests authorization from the Resource Owner. 
* (B) The Resource Owner responds to the client with a credential called `Authorization Grant`.
* (C) The client then redeems the `Authorization Grant` with the Authorization Server for a valid `Access Token` (D).
* (E) The client then reaches out to the Resource Server with the Access Token and gains access to the protected resource.

{% include callout.html type="primary" content="For more information about the OAuth 2.0 protocol flow, see [OAuth 2.0 Protocol Flow](https://tools.ietf.org/html/rfc6749#section-1.2)." %}

{% include callout.html type="primary" content="TeamForge can act both as an IdP and Service Provider and at times as a client too. The TeamForge Web Application is one of the system defined clients that use TeamForge IdP's OAuth services. For more information about system defined clients, see [System Defined Clients][teamforgeoauth.html#systemdefinedclients]." %}

## TeamForge API Authentication and Access Tokens

Both TeamForge REST and SOAP APIs use OAuth 2.0 access tokens for authentication. Clients can obtain access tokens from the token endpoint which is located at `/oauth/auth/token`.

### Access Tokens {#accesstokens}

The tokens used by the TeamForge API are Bearer Tokens as specified in [RFC 6750](https://tools.ietf.org/html/rfc6750). This means that it is possible and allowed to share tokens with multiple clients or to have clients pass tokens to intermediate services, which then delegate tokens to TeamForge. TeamForge tokens use the [JSON Web Token (JWT)](http://jwt.io) standard. However, clients should consider access tokens to be opaque in order to guarantee compatibility with future TeamForge versions. It is the client's responsibility to protect the access token against theft. This means that access tokens should only be transmitted over SSL-secured connections and should not be persisted.

### TeamForge OAuth Scopes {#teamforgescopes}

Scopes can be used to restrict which services a token can be used for. Limiting the number of scopes decreases the potential damage that could occur in case an access token is stolen, so it is advisable to restrict the number of scopes to a minimum.

TeamForge currently supports the following list of scopes.

| Scope | Description |
|---------|-------------|
| **urn:ctf:services:ctf** | Digital.ai TeamForge application services.  Use this scope to call the TeamForge REST API. |
| **urn:ctf:services:svn** | Subversion services. Use this to call the Subversion REST API. |
| **urn:ctf:services:gerrit** | Git/Gerrit services. Use this to call the Git REST API. |
| **urn:ctf:services:soap60** | SOAP60 services. Use this to call the TeamForge SOAP API. |

### Client ID and Client Secret

In order to use TeamForge's OAuth services, a client application must be registered with TeamForge. Upon registration, the client gets its client credentials: `Client ID` and `Client Secret`. For more information about how to get the Client ID and Client Secret, see [Add Clients][teamforgeoauth.html#addclients].

| Client ID | The Client ID is a unique identifier used by TeamForge to identify the client application and is used in building the Authorization URLs. |
| Client Secret | The Client Secret is a unique identifier used to authenticate the client application’s identity. |


### TeamForge OAuth Grant Types {#teamforgegranttypes}

When a client requests access token from an Authorization Server, it uses the Authorization Grant, which is a credential that represents the Resource Owner's authorization to access protected resources. Of the four standard grant types defined in [The OAuth 2.0 Authorization Framework RFC 6749](http://tools.ietf.org/html/rfc6749), TeamForge supports the following three grant types:

* [Authorization Code][teamforgeoauth.html#authorization_code] (`authorization_code`)
* [Resource Owner Password Credentials][teamforgeoauth.html#password] (`password`)
* [Client Credentials][teamforgeoauth.html#client_credentials] (`client_credentials`)

In addition, TeamForge supports the following custom grant type: 

* [Anonymous][teamforgeoauth.html#anonymous] (`rn:ctf:grant_type:anonymous`)

### TeamForge System Defined Grant Types {#systemdefinedgranttypes}
TeamForge also supports the following system defined grant types. However, these grant types are used by TeamForge's [system defined clients][teamforgeoauth.html#systemdefinedclients] to obtain access tokens and are therefore not supposed to be used for other custom clients.

* JSession (`urn:ctf:grant_type:jsession`)
* SCM Admin (`urn:ctf:grant_type:scmrequestkey:scmadmin`)
* SCM Viewer (`urn:ctf:grant_type:scmrequestkey:scmviewer`)
* Token (`urn:ctf:grant_type:token`)


## Authorization Code Grant Type (`authorization_code`) {#authorization_code}
The Authorization Code grant type can be used if the client intends to use TeamForge as its IdP. This grant type, if used by clients, provides an access token for a valid `authorization code`. This is a redirection based grant type and hence you must add one or more `Redirect URIs` while [adding clients][teamforgeoauth.html#addclients] that use this grant type. 

{% include note.html content="Inlcude a comma separated list of `Redirect URIs` in case you want to set up multiple URIs." %}

### How to get an authorization code?

Clients (Relying Party) must request the `authorization code` from TeamForge IdP URL (`/oauth/oidc/authorize`) with the following parameters:

````
scope = open_id (mandatory for OIDC clients)
response_type = code (mandatory for OIDC clients)
client_id = <Client ID generated while registering the client with TeamForge>
redirect_uri = <URL encoded Redirect URI>
````

After successful authorization, TeamForge IdP provides the `authorization code` to the redirect URI configured while [adding the client][teamforgeoauth.html#addclients]. Here's a sample OIDC response after a successful authorization:

```http
https://<your_redirect_uri>?code=<authorization_code>
````

Up on getting the `authorization code`, the client can redeem it with the Authorization Server to obtain an access token.

### Protocol Flow

{% include image.html file="oauth1.png" %}

### Usage Example to Obtain an Access Token

```curl
# Base URL of TeamForge site.
site_url="https://teamforge.example.com"

# Requested scope (all)
scope="urn:ctf:services:ctf urn:ctf:services:svn urn:ctf:services:gerrit urn:ctf:services:soap60"

# Client's authorization code
code=<your authorization code>

curl -d "grant_type=authorization_code&client_id=<your Client ID>&client_secret=<your Client Secret>&scope=$scope&code=$code" $site_url/oauth/auth/token
````

A successful response will return the HTTP 200 status code and the response body will contain something like this:

````
           {
             "access_token": "eyJraWQiOiIxIiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiJhZG1pbiIsImF1ZCI...",
             "token_type": "Bearer"
           }
````

In compliance with the Bearer Tokens specification (RFC 6750), TeamForge expects access tokens to be passed in the Authorization header:
````

            GET /resource HTTP/1.1
            Host: teamforge.example.com
            Authorization: Bearer SAksa921hjsi...

````           
The only exception to this is the SOAP API which expects the token to be passed as part of the SOAP request payload in accordance with the API documentation.

{% include callout.html type="primary" content="For more information, see [Authorization Code Grant Type](https://tools.ietf.org/html/rfc6749#section-4.1)." %}          


## Resource Owner Password Credentials Grant Type (`password`) {#password}

Clients can use the Resource Owner Password Credentials grant type to get an access token for a given username and password.

### Protocol Flow

{% include image.html file="oauth3.png" %}

### Usage Example to Obtain an Access Token

```curl
# Base URL of TeamForge site.
site_url="https://teamforge.example.com"

# TeamForge authentication credentials.
username="foo"
password="bar"

# Requested scope (all)
scope="urn:ctf:services:ctf urn:ctf:services:svn urn:ctf:services:gerrit urn:ctf:services:soap60"

curl -d "grant_type=password&client_id=<your Client ID>&scope=$scope&username=$username&password=$password" $site_url/oauth/auth/token
````

You can see from this example that it is sending an HTTP POST request to the `/oauth/auth/token` endpoint, and the content of the request body contains the following data:

* `grant_type=password`: Indicates you are providing username and password. 
* `client_id=<your Client ID>`: Client ID generated while adding the client.
* `scope= ...`: Space-separated list of requested scopes.
* `username=value&password=value`: The valid TeamForge user credentials.

{% include callout.html type="primary" content="For more information, see [Resource Owner Password Credentials Grant Type](https://tools.ietf.org/html/rfc6749#section-4.3)." %}

## Client Credentials Grant Type (`client_credentials`) {#client_credentials}

Clients can use the Client Credentials grant type to get an access token for a given Client ID and Client Secret. Use this grant type only for trusted and confidential clients.

{% include important.html content="Clients that use the Client Credentials grant type must be assigned with a valid TeamForge license in order for the clients to be able to access TeamForge resources as OAuth clients." %}

### Protocol Flow

{% include image.html file="oauth4.png" %}

### Usage Example to Obtain an Access Token

```curl
# Base URL of TeamForge site.
site_url="https://teamforge.example.com"

# Requested scope (all)
scope="urn:ctf:services:ctf urn:ctf:services:svn urn:ctf:services:gerrit urn:ctf:services:soap60"

curl -d "grant_type=client_credentials&client_id=<your Client ID>&client_secret=<your Client Secret>&scope=$scope" $site_url/oauth/auth/token
````

{% include callout.html type="primary" content="For more information, see [Client Credentials Grant Type](https://tools.ietf.org/html/rfc6749#section-4.4)." %}

## Anonymous Grant Type (`urn:ctf:grant_type:anonymous`) {#anonymous}

Use this grant type for clients that need to access TeamForge's public resources.

### Usage Example to Obtain an Access Token

```curl
# Base URL of TeamForge site.
site_url="https://teamforge.example.com"

# Requested scope (all)
scope="urn:ctf:services:ctf urn:ctf:services:svn urn:ctf:services:gerrit urn:ctf:services:soap60"

curl -d "grant_type=urn:ctf:grant_type:anonymous&client_id=<your Client ID>&client_secret=<your Client Secret>&scope=$scope" $site_url/oauth/auth/token
````

## Unsupported Grant Types

The following grant types are not supported by TeamForge.

* refresh_token
* urn:ietf:params:oauth-grant-type:saml2-bearer

## Federated Identity Management {#federatedlogin}

Federated Identity Management refers to the process of storing user credentials with an IdP (such as TeamForge, SAML and so on) and having the Service Provider (SP) rely on the IdP to validate user credentials when he/she tries to access its resources.

TeamForge supports federated identity. By default, federated login is disabled in TeamForge. Site Administrators must enable federated login and select an IdP.

1. Log on to TeamForge as a Site Administrator. 
2. Select **My Workspace > Admin**. 
3. Select **My Page > Identity**.
4. Select the **Federation** tab.
5. Select the **Use Federated Login** check box and select an IDP from the drop-down list.
   {% include image.html file="174_oauth_04.png" %}
6. Click **Save**.

### Logging into TeamForge in a Federated Login Setup
Once enabled, TeamForge Web Application, by virtue of being a system defined client application (see [System Defined Clients][teamforgeoauth.html#systemdefinedclients]), follows the OAuth authorization/authentication process to access TeamForge services on behalf of the Resource Owner (user).

1. Click **Login**.
   
   {% include image.html file="174_oauth_01.png" %}
   
   You are redirected to an authorization page.

   {% include image.html file="174_oauth_02.png" %}

2. Type the user name and password and click **Log In**. 

   You, as a Resource Owner, are then prompted to either allow or deny the client application (TeamForge Web Application) to access the resources on the Resource Server (TeamForge Application Server). 
   
   {% include image.html file="174_oauth_03.png" %}

3. Click **Allow** or **Deny** to allow or deny access respectively.


## System Defined Clients {#systemdefinedclients}
TeamForge OAuth consists of the following system defined clients: 
* TeamForge Web Applicaion Client (`ctfweb`)
* Code Browser Client (`codebrowser`)
* SOAP60 Client (`soap60-client`)
* SCM Client (`scm-client`)
* API Client (`api-client`)
* App Client (`app-client`)

These clients have been pre-defined as illustrated in the following table.

| System Defined Client | Grant Type | Services | Token Life Time (in seconds) |
|-----------------------|------------|----------|-----------------|
| ctfweb | authorization_code<br>urn:ctf:grant_type:jsession | soap60,ctf,gerrit,svn | 3600 |
| codebrowser | urn:ctf:grant_type:jsession | soap60,ctf,gerrit,svn | 3600 |
| soap60-client | password<br>urn:ctf:grant_type:anonymous | soap60 | 3600 |
| scm-client | urn:ctf:grant_type:scmrequestkey:scmviewer<br>urn:ctf:grant_type:scmrequestkey:scmadmin | soap60,ctf | 3600 |
| api-client | password | 	soap60,ctf,gerrit,svn | 3600 |
| app-client | urn:ctf:grant_type:token | soap60,ctf,gerrit,svn | 3600 |

{% capture systemclients %}
You cannot edit these system defined clients. The following error message shows up if you try to edit these clients.<br><br>
````
Error editing oauth client: System defined clients are not allowed to be modified.
````
{% endcapture %}
{% include callout.html type="primary" content=systemclients %}


## Add Clients {#addclients}

In order to use TeamForge's OAuth services, a client application must be registered with TeamForge. Upon registration, the client gets its client credentials: `Client ID` and `Client Secret`.

| Client ID | The Client ID is a unique identifier used by TeamForge to identify the client application and is used in building the Authorization URLs. |
| Client Secret | The Client Secret is a unique identifier used to authenticate the client application’s identity. |

To add a TeamForge OAuth client:

1. Log on to TeamForge as a Site Administrator. 
2. Select **Admin** from the **My Workspace** menu. 
3. Select **Identity** from the **Projects** menu. 
4. Click **Add Client** from the **OAuth** tab.

   The **Add Client** dialog box appears.

   {% include image.html file="174_addclient01.png" %}

5. Enter client information.

   The following parameters are required to register a client application with TeamForge:
   * **Client Application Name**: Type a name for your client.
   * **Redirect URIs**: Inlcude a comma separated list of `Redirect URIs` in case you want to set up multiple URIs. Redirect URIs are required only for clients that use the [**Authorization Code**][teamforgeoauth.html#authorization_code] grant type.
   * **Grant Type**: Select the client's grant type. 
   * **Services** (scopes): Select one or more TeamForge OAuth scopes.
   * **Token Life Time** (in seconds): Type the duration (in seconds) for which the token is valid.
   * **License Types**: Select a TeamForge license for the client. This is required only for clients that use the [**Client Credentials**][teamforgeoauth.html#client_credentials] grant type.
6. Click **Save**. Once the client is added successfully, a message containing the client's credentials is shown.
   {% include image.html file="174_oauth_05.png" %}

   {% include warning.html content="Once the client is added successfully, the `Client ID` and `Client Secret` are generated and shown in the message. You must copy and keep your `Client Secret` safe before closing the message as you cannot fetch your client secret later from anywhere else." %}
   

{% include links.html %}