---
title: Change the scmviewer Password
keywords: site admin scm tasks, scm, source control
tags: [site_admin_tasks, installation, upgrade, integration, source_code, scm, git_gerrit]
sidebar: teamforge_sidebar
permalink: changethescmviewerpassword.html
last_updated: May 27, 2019
summary: It is recommended to change the scmviewer password after installing TeamForge.
---
Follow these steps to change the scmviewer password:
1. {% include installupgrade/stop_teamforge_178andLater.html %} 
2. Create an encrypted password using the [password_util.sh][passwordutil].
   ```shell
   /opt/collabnet/teamforge/runtime/scripts/password_util.sh -encrypt '<new_password_text>'
   ````
3. Set the encrypted password to the [SCM_USER_ENCRYPTED_PASSWORD][siteoptiontokens.html#SCM_USER_ENCRYPTED_PASSWORD] token in the `/opt/collabnet/teamforge/etc/site-options.conf` file.
4. {% include installupgrade/deploy_services_without_note.html %}

{% include links.html %}