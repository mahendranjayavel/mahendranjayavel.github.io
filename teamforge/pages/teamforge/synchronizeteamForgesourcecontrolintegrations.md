---
title: Synchronize TeamForge Source Control Integrations
keywords: site admin scm tasks, scm, source control
tags: [ctf_20.2, ctf_18.3, site_admin_tasks, installation, upgrade, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: synchronizeteamforgesourcecontrolintegrations.html
last_updated: Jul 13, 2020
summary: Any time you upgrade your TeamForge site or a source control application, you must ensure that your users can still access their source code.
---
1. Click **Admin** in the TeamForge navigation bar.
2. Select **Projects > Integrations**.
3. For each source control service you are supporting, verify that the right paths are specified.
   * **SOAP service host** should be `localhost` or the host name of the server on which you just installed TeamForge.
   * **Repository base URL** should be the URL for the top level of your source code server (which may be the same as your application server). For example, `http://<myscmbox>/svn/repos`
   * **SCM Viewer URL** should be the URL for the ViewVC application on your source control server. For example, `http://<myscmbox>/integration/viewvc/viewvc.cgi`
   {% include note.html content="If you want to turn on TeamForge code browser, specify the appropriate URL." %}
4. Select all your integrations and click **Synchronize Permissions**. This updates the permissions on your code repositories so that users can access them from the new site.
   {% include note.html content="By default, the DISABLE_CREATE_INTEGRATION_SERVERS token in the `site-options.conf` file is set to `false`, which allows users to create new external integrations. To restrict users from adding new integrations, set this token to `true` and recreate the runtime environment before making the site available to users." %}

   **Known Issue in TeamForge 18.3**
<!-- https://forge.collab.net/sf/go/artf315459#5 -->   

   Post upgrade to TeamForge 18.3, when you click **Synchronize Permissions**, <!-- CVS permissions are synchronized as expected. However,  -->one of the svn-internal repositories is assigned with the `root:HTTPD_GROUP` permission (erroneously). Fix this by running the following command:

   ```shell
   chown -R $(sed -ne 's/^HTTPD_USER=\(.*\)/\1/p' /opt/collabnet/teamforge/runtime/conf/runtime-options.conf):$(sed -ne 's/^HTTPD_GROUP=\(.*\)/\1/p' /opt/collabnet/teamforge/runtime/conf/runtime-options.conf) /opt/collabnet/teamforge/var/scm/sf-svnroot/*
   ````

{% include links.html %}