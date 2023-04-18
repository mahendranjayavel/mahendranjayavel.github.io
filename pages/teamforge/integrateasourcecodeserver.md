---
title: Integrate a Source Code Server
keywords: site admin scm tasks, scm, source control
tags: [site_admin_tasks, installation, upgrade, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: integrateasourcecodeserver.html
toc: no
last_updated: Mar 1, 2018
summary: A site must have one or more servers to handle source code repositories and users. The source code server can be the same server as the application server or a separate server.
---
When you set up a managed software configuration management (SCM) server, you enable users to create, manage, and share repositories through Digital.ai TeamForge.
  {% include note.html content="The ability to add integration servers depends on the value of the [DISABLE_CREATE_INTEGRATION_SERVERS][siteoptiontokens.html#disable_create_integration_servers] flag in the `site-options.conf` file. You can add new integration servers when the flag is set to its default value of FALSE." %}

You can integrate more than one source code server of a given type. For example, you can have two or more Subversion servers on your site. Consult a system administrator about the requirements for setting this up.

  {% include tip.html content="If you use a source code solution other than Subversion, you can integrate it using the Digital.ai TeamForge SOAP APIs. This enables you to exchange commit data with any SCM application. Consult your Digital.ai TeamForge system administrator." %}

<!--   {% include note.html content="CVS servers that integrate with Digital.ai TeamForge must use the native UNIX/Linux authentication method, and not external authentication mechanisms such as NIS, NIS+, Winbind, Active Directory, or LDAP. TeamForge creates and manipulates local system accounts using the default `useradd`, `usermod`, `groupadd`, `groupdel`, and `userdel` commands. It expects to find any accounts or groups it create in `/etc/passwd` and `/etc/group`." %} -->

1. Go to **My Workspace > Admin**.
2. Click **Projects > INTEGRATIONS**.
3. On the **SCM INTEGRATIONS** page, click **Create**.
4. On the **Create Integration** page, write a name and description for the integration.
5. Choose the type of SCM server you want. 
   {% include note.html content="When you give a group access to a Wandisco Subversion repository, members of the group can view the repository but cannot do repository actions, such as commit and update. You must assign those permissions to users individually." %}
   {% include note.html content="The SCM Adapter option only works if you have created your own SCM integration using the Digital.ai TeamForge SOAP APIs." %}
6. Supply the host name for the **Soap Service Host**. This is the network address of the machine on which the integrated service such as Subversion is running.
   {% include note.html content="The default `localhost` will work only if the integration server is on the same server as the Digital.ai TeamForge server." %}
7. Leave the default values in the **SOAP Service Port** field.
8. Specify whether users will use SSL to connect to their repositories.
9. Change the **Repository Root** value if you want to store the repository on your server in a different location. The repository root is the top-level directory under which all source code repositories reside.
10. Select the **Requires Approval** check box if you want an administrator to approve all repositories created on the server. By default, unmanaged servers require approval for all repositories, because repositories must be created and integrated manually.
    {% include note.html content="By default, repositories created (or deleted) by site administrators and users with site-wide role (with Integrations, especially SCM INTEGRATIONS permission) need no approval." %}
11. Supply the URL by which your users will access the service. This will be of the form `http://<myscmserver.com>/integration/viewvc/viewvc.cgi`.
    {% include important.html content="If your system administrator has upgrade your site from SourceForge Enterprise Edition 4.4 or earlier, remove the port number in the SCM Viewer URL." %}
    <!-- {% include tip.html content="If you are working with a CVS server that uses Pserver authentication, ask your system administrator for the right URL." %} -->
12. The **Use Internal Code Browser** option is selected by default to allow the users to access the TeamForge code browser for a Subversion or Git server. For more information about this feature, see [Get the Code][getcode].
    {% capture codenote%}
    {% include inline_image.html file="status-success-small.png"%} Software requirements for using TeamForge code browser, if Subversion or Git is running on a separate server: Subversion Edge 5.1.0 and TeamForge - Git integration 8.4.4 or later. <br><br>
    {% include inline_image.html file="status-success-small.png"%} You need to specify the **SCM Viewer URL** (see step 11), the way you would for ViewVC or Gitweb. The 'http://' or 'https://', the host name and the port number (if any) need to be set correctly. As a minimum requirement, the URL should point to the root of the SCM http server and the domain name. <br><br>
    {% include inline_image.html file="status-success-small.png" %} If the SCM server is not the same as the TeamForge server, make sure you install SSL certificates or visit the URL for the site directly from your browser, and import and trust the certificate into the browser.
    {% endcapture %}
    {% include callout.html type="primary" content=codenote %}
13. Click **Save**. Digital.ai TeamForge attempts to validate the SCM viewer URL. If it cannot validate the URL, you can:
    * Correct it if you have entered it incorrectly.
    * Select **Save with errors** if the URL is different for an end user than it is for the Digital.ai TeamForge server; for example, if you have a firewall in place.

If you are adding a managed source code server, it is now added. All projects can now establish repositories on the server.
<!-- If you are adding an unmanager CVS server, all projects can now request repositories on the server. A Digital.ai TeamForge administrator must create and integrate them manually. -->

 <!-- {% include note.html content="Only CVS servers can run unmanaged." %} -->

{% include links.html %}