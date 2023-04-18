---
title: Find a User
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license, saml, ldap, authentication]
sidebar: teamforge_sidebar
permalink: findauser.html
last_updated: Apr 24, 2018
summary: To find a user, filter the list all Digital.ai TeamForge users on your site.
---

1. Go to **My Workspace > Admin**.
2. Click **USERS** from the **Projects** menu.
3. Specify the filter criteria in one or more filter fields (at the top of each column) and click **FILTER**.

   * You can find a filter field at the top of each column in most of the tables in the TeamForge application.
   * The filter field could be a text box or a drop-down list with multi-select check boxes.

     {% include image.html file="17-4-filtertables02.png" %}
   * You can type your filter criteria in the text boxes. The search text is case-insensitive.
   * You can also select the filter values from one or more drop-down lists. By default, you can only select up to 10 filter values in a drop-down list. However, you can set a value that suits your requirement for the FILTER_DROPDOWN_MAX_SELECTION token in the site-options.conf file to increase or decrease the count.
   * **Filter-as-you-type**: You can find the **Enter keywords** text box in all filter drop-down lists. As you type your filter keyword, instant search results are shown in the drop-down list. For example, in the following illustration, typing "R" instantly shows all statuses having the alphabet "R". The search text is case-insensitive.
     {% include image.html file="filtertables01.png" %}
   * Some search filters may not appear if your site administrator has not enabled them.
4. After filtering, if you want to clear the filters, click **FILTER** and select **Clear** from the drop-down list.

All users meeting your filter criteria are displayed.

{% include links.html %}