---
title: Check Out Code
keywords: check out code
tags: [ctf_19.3, project admin_tasks, project_member_tasks, source_code, git_gerrit, scm]
sidebar: teamforge_sidebar
last_updated: Oct 10, 2019
permalink: checkoutcode.html
folder: teamforge
summary: You can use the checkout command to check out the code from Subversion or GIT repository.
---

## Check out Subversion Code Anonymously

When you want to experiment with the code, you can do an anonymous checkout from the Subversion repository. The checkout command uses a unique system-created user called "guest" and works without authentication.

To make anonymous checkout possible, the project administrator must set public and repository view permission to "All Users." The checkout command differs based on whether a user is logged in or not.

* When you are not logged in, use this command to check out:

```shell
svn checkout --username guest <domain>/svn/repo URL name
````

* When you are logged in, use this command to check out:

```shell
 svn checkout --username <logged in_username><domain>/svn/repo URL name
````

## Check out GIT Code

Generally, GIT repositories can be accessed by more than one protocol. To support this, a **Protocol** drop-down list is available on the source code repositories page. This feature applies only to GIT repositories and so selecting a protocol determines the check out command for a GIT repository. This also gives the user an option to override the default protocol which is set while configuring the GIT integration server.

<!--artf391607-->
### Configurable Checkout Command for Git Repositories

Prior to TeamForge 19.3, by default, the checkout command/clone URL of a Git repository, included the SCP-based commit message hook for SSH protocol and cURL-based commit message hook for HTTP protocol.

From now on, you can modify the checkout command settings for both HTTPS and SSH protocols to include either the SCP-based or cURL-based commit message hook in their clone URL, using the two new parameters, **HTTPS HOOK FETCH COMMAND** and **SSH HOOK FETCH COMMAND** (**Admin > Integrations > \<Git <a href="#" data-toggle="tooltip" data-original-title="hostname refers to the server on which Git integration is hosted">hostname</a>\>** page). This setting applies across projects on your site.

{% include image.html file="git-fetch-commands.png" caption="\"HTTPS HOOK FETCH COMMAND\" and \"SSH HOOK FETCH COMMAND\" parameters" %} 

For instance, if you want the checkout command for HTTPS protocol to include SCP-based commit message hook, you can select the option _SCP_ from the **HTTPS HOOK FETCH COMMAND** parameter. 

{% include image.html file="git-clone-https-scp.png" caption="HTTPS clone URL with SCP-based commit message hook" %}

You can also include the cURL-based commit message hook in the HTTPS checkout command by selecting the _cURL_ option from **HTTPS HOOK FETCH COMMAND**.

{% include image.html file="git-clone-https-curl.png" caption="HTTPS checkout command with cURL-based commit message hook" %}

Similarly, you can select the option _cURL_ from the **SSH HOOK FETCH COMMAND** parameter to include the cURL-based commit message hook in the checkout command for SSH protocol, if required. 

{% include image.html file="git-clone-ssh-curl.png" caption="SSH checkout command with CURL-based commit message hook" %} 

You can select the _SCP_ option to get the SCP-based commit message hook included for SSH protocol.

{% include image.html file="git-clone-ssh-scp.png" caption="SSH clone URL with SCP-based commit message hook" %} 



{% include links.html %}
