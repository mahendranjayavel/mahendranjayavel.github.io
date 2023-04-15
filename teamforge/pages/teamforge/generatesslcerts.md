---
title: Generate SSL certificates
keywords: SSL, certificates, self-signed certs, certs, security, secured socket layer, ssl
tags: [installation, upgrade, ssl, getting_started, security]
sidebar: teamforge_sidebar
permalink: generatesslcerts.html
last_updated: Oct 8, 2018
summary: To use HTTPS for web traffic, you will need to obtain a valid Apache SSL certificate.
---
When generating an Apache (mod_ssl) SSL certificate, you have two options:
* Purchase a SSL certificate from a certificate authority (CA). Searching the Web for "certificate authority" will present several choices.
* Generate a self-signed certificate. This option costs nothing and provides the same level of encryption as a certificate purchased from a certificate authority (CA). However, this option can be a mild annoyance to some users, because Internet Explorer (IE) issues a harmless warning each time a user visits a site that uses a self-signed certificate.

{% include important.html content="SSL is enabled by default and a self-signed certificate is auto-generated." %}

Regardless of which option you select, the process is almost identical.

1. Know the fully qualified domain name (FQDN) of the website for which you want to request a certificate. If you want to access your site through `https://www.example.com`, then the FQDN of your website is `www.example.com`.
   {% include callout.html type="primary" content="This is also known as your common name." %}
2. Generate the key with the SSL `genrsa` command.
   ```shell
   openssl genrsa -out www.example.com.key 1024
   ````

   This command generates a 1024 bit RSA private key and stores it in the file `www.example.com.key`.

   {% include tip.html content="Back up your www.example.com.key file, because without this file, your SSL certificate will not be valid." %} 
3. Generate the CSR with SSL `req` command.
   ```shell
   openssl req -new -key www.example.com.key -out www.example.com.csr
   ````
   This command will prompt you for the X.509 attributes of your certificate. Give the fully qualified domain name, such as `www.example.com`, when prompted for `Common Name`.
   {% include callout.html type="primary" content="Do not enter your personal name here. It is requesting a certificate for a webserver, so the `Common Name` has to match the FQDN of your website." %}
4. Generate a self-signed certificate.
   ```shell
   openssl x509 -req -days 370 -in www.example.com.csr -signkey www.example.com.key -out www.example.com.crt
   ````
   This command will generate a self-signed certificate in `www.example.com.crt`.

You will now have an RSA private key in `www.example.com.key`, a Certificate Signing Request in `www.example.com.csr`, and an SSL certificate in `www.example.com.crt`. The self-signed SSL certificate that you generated will be valid for 370 days.


{% include links.html %}