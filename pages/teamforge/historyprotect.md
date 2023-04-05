---
title: History Protection
keywords: history protect, protection, git, gerrit
tags: [git_gerrit, integration]
sidebar: teamforge_sidebar
permalink: historyprotect.html
last_updated: Aug 2, 2019
summary: History protection archives rewritten changes and keeps backups of deleted branches. If history changes occur, an immutable backup `ref` is created in the remote repository, notification emails are sent to all members of the Gerrit Administrators group, and an event is logged in the audit log.
---

History rewrites are non-fast-forward updates of remote refs and associated objects. History rewrites happen when a branch in a remote repository gets deleted, previously pushed commits get amended or filtered and forcefully re-pushed, or a remote branch/tag is pointed to an entirely different commit history.

History may get rewritten without leaving any trace of the previous state. Sometimes this behavior may be wanted — for example, in the case of removing code violating intellectual property, removing mistakenly committed large binary files or removing merged feature branches. The TeamForge-Git integration therefore does not disable the history rewrite feature, but instead enables it for SCM Administrators alone. However, since rewriting history might be easily abused and result in accidental data loss, we've introduced the History Protection feature as a safety net and necessity for ensuring proper audit compliance.

History protection archives rewritten changes and keeps backups of deleted branches. If history changes occur, an immutable backup `ref` is created in the remote repository, notification emails are sent to all members of the Gerrit Administrators group, and an event is logged in the audit log. The backed up `ref` can be restored into a new branch with any Git client (without needing physical file access to the Gerrit server). Gerrit site administrators can still decide to remove selected backup refs permanently.

{% unless site.output == "pdf" %}
<iframe width="700" height="700" src="videos/CTF72_HistoryProtection.swf" frameborder="0" allowfullscreen></iframe>
{% endunless %}

## Enable History Protection {#enablehistoryprotection}
History protection is enabled at the site level by default in TeamForge 17.4 and later versions. However, site administrators can disable history protection at the site level if need be, after which project administrators can choose to have history protection enabled or disabled for individual repositories.

To turn on/off history protection for an individual Git repository in a TeamForge project, select or clear the **Protect History** check box respectively while creating the repository. 

For an existing repository:
1. On the **Source Code** page, select the Git repository and click **Edit**.
2. Select the **Protect History** check box.
3. Click **Save**.

You can turn history protection on or off any time. However, your change will not be reflected in Gerrit immediately. It will be effective after the time that you defined as the regular refresh interval while installing the Git integration.

If you want your change to take effect immediately, do this right after you select or clear the **Protect History** check box: as a user with Source Code Admin permission, temporarily remove any user having a project role with any SCM permission, and then add that user back. This will trigger an immediate sync which will enable history protection. After that, the Gerrit Administrator will be able to see History Protection enabled in the Gerrit web interface (by logging in as a Gerrit Administrator and clicking the General link for the project with the name of the Git repository).

## History Protection Reports
Once history protection is turned on, any non-fast-forward push to a remote repository or deletion of a branch or tag on a remote repository is recorded and reported.

### Email Notifications
When history is rewritten, an email is sent to the Administrator group members in Gerrit.

{% include image.html file="tf-git-historyprotect-email.png" %}

{% include note.html content="The `Closure Templates (Soy)` have replaced the existing `Velocity Templates` used for history protection email notifications. For more information on the new Closure templates (Soy), see [Gerrit Code Review--Mail Templates](https://gerrit-documentation.storage.googleapis.com/Documentation/2.15/config-mail.html). 
" %}

### Gerrit Web Interface
Every history rewrite event is logged and stored in the Gerrit database and visible in the Gerrit web interface. As Gerrit Administrator, you can:
* See rewritten history from **Project > Rewritten History**.
  {% include image.html file="tf-git-rewrittenhistory-2.7.x.png" %}
* Restore history by clicking **Resurrect** and providing a name for the new branch.
  {% include image.html file="tf-git-resurrecthistory-2.7.x.png" %}
* Permanently remove a branch by clicking **Delete Permanently**.

### Git Command Line
You can use a standard Git client and run `git fetch && git ls-remote` for information on rewritten and deleted branches.
{% include image.html file="tf-git-fetchcommand.png" %}
You can view entries in `refs/rewrite` (for non-fast-forward pushes) and `refs/delete` using the Git `ls-remote` command only if read access is granted to `refs/*`. Gerrit will prevent any other action such as delete/force-update on those special `refs` for all users including administrators.

### Audit Log Entries
The following events are logged in `/opt/collabnet/gerrit/logs/gerrit.audit.log`:
* Remote branches are deleted.
* History is rewritten (non-fast-forward push).
* Backup branches are resurrected.
* Backup branches are permanently deleted.
* History Protection is turned on or off.

{{site.data.alerts.hr_shaded}}
#### Appendix
<!-- Use this for web output -->
{% unless site.output == "pdf" %}
* [History Protection FAQs][gitgerrit-faqs]
* [History Protection Slide Deck](pptsdocs/History_rewrite.pptx)
* [Git reflog vs History Protection](pptsdocs/Git_reflog_vs_History Protect.docx)
* [Gerrit Performance Cheat Sheet](pdf/Gerrit-Performance-Tuning-Cheat-Sheet.pdf)
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
* [History Protection FAQs][gitgerrit-faqs]
* [History Protection Slide Deck](https://docs.collab.net/teamforge203/pptsdocs/History_rewrite.pptx)
* [Git reflog vs History Protection](https://docs.collab.net/teamforge203/pptsdocs/Git_reflog_vs_History%20Protect.docx)
* [Gerrit Performance Cheat Sheet](https://docs.collab.net/teamforge203/pdf/Gerrit-Performance-Tuning-Cheat-Sheet.pdf)
{% endunless %}


{% include links.html %}