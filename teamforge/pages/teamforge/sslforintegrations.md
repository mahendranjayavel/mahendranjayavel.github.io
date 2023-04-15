---
title: Protect Integrations with SSL
keywords: SSL, integration, security
tags: [installation, ssl, security]
sidebar: teamforge_sidebar
permalink: sslforintegrations.html
last_updated: Apr 1, 2020
summary: If you have registered Secure Socket Layer (SSL) certificates, your site's users can use SSL when they set up an SCM integration server. You can also enable SSL to encrypt the data traffic between TeamForge Application and Database servers. 
---
## Register SSL Certificates

If you use certificates that are generated in-house, self-signed, or signed by a non-established Certificate Authority, they must be registered with each client system that will connect to the TeamForge server. Registration consists of importing custom certificates into the Java runtime's global keystore on each server.

{% include warning.html content="This affects any other Java applications on the server that use the same Java runtime." %}

1. Collect the server certificates from all servers. On RHEL, CentOS and other RedHat-based distributions, these are contained in `/etc/httpd/conf/ssl.crt/server.crt`.
   
   {% include important.html content="Be sure to use exactly this path, as there are other files with similar names, plus server certificates are not really secret, but some other files are. So, files must be copied (e.g., via scp) to the same directory, and renamed if necessary to avoid conflicts. It's recommended that you use the short server name of the corresponding server for this." %}
2. Locate the Java keystore. 
   
   This is `PATH_TO_JAVA/jre/lib/security/cacerts`. For example, this may be `/usr/local/j2sdk1.4.2_10/jre/lib/security/cacerts`.
3. Locate the Java keytool utility.

   This is `PATH_TO_JAVA/bin/keytool` For example, `/usr/local/j2sdk1.4.2_10/bin/keytool`.
4. Import each server certificate into the keystore.
   
   ```shell
   PATH_TO_JAVA/bin/keytool -import -keystore PATH_TO_JAVA/jre/lib/security/cacerts -file <server>.crt -alias <server>
   ````
   {% include note.html content="Any value is accepted for server in -alias <server>." %}
5. At the password prompt, use `changeit`. Confirm that you trust the certificate by typing yes.
6. Verify that all your certificates are added.
   ```shell
   PATH_TO_JAVA/bin/keytool -list -keystore PATH_TO_JAVA/jre/lib/security/cacerts |less
   ````
   {% include note.html content="The list will contain many more certificates. These are top-level CA certificates, provided with Java." %}
7. If you are running more than one separate server, repeat these steps for each server.
8. Restart TeamForge

From now on, you can select the **Use SSL** check box, if required, when creating an SCM integration.

## Encrypt Database Network Traffic (On Sites with Remote Database Servers) {#databasessl}

To prevent your data from being exposed in a readable format on the network, use the Secure Socket Layer (SSL) to encrypt the network traffic between the Application and the Database servers.

If you have a dedicated database server (operational database or datamart), encrypt the data traffic between the application and database servers and between the ETL and datamart servers.

{% include important.html content="The following steps are relevant for a distributed setup only." %}

1. {% include installupgrade/stop_teamforge_on_all_servers_distributed.html %}
2. If the operational database or datamart is running on a separate server, include the token [DATABASE_SSL=on][siteoptiontokens.html#DATABASE_SSL].
<!-- Artifact artf396404 : [DOC] Add tokens for DATABASE_SSL=on -->   
      
      In addition, set the following tokens with the location of the SSL cert and key files of the TeamForge PostgreSQL database server.
      ```shell
      POSTGRES_SSL_CERT_FILE=/var/ops/ssl/<dbserver.crt>
      POSTGRES_SSL_KEY_FILE=/var/ops/ssl/<dbserver.key>
      ````

      In case you have TeamForge Baselines, set the following tokens with the location of the cert and key files of the TeamForge Baselines PostgreSQL database server. 
      ```shell
      POSTGRES_BASELINE_SSL_CERT_FILE=/var/ops/ssl/<baselinedb-server.crt>
      POSTGRES_BASELINE_SSL_KEY_FILE=/var/ops/ssl/<baselinedb-server.key>
      ````      
      {% include note.html content="It is mandatory to include these tokens on all the servers." %}
      
3. {% include installupgrade/deploy_services_without_note.html %}
4. Verify that your PostgreSQL database is running in the SSL mode.
   1. Log on to the Database Server and run the following command:
      ```shell
      grep "ssl = " var/lib/pgsql/{{site.data.identifiers.postgres_short}}/data/postgresql.conf
      ````
      Observe:"ssl = on"

{% include links.html %}