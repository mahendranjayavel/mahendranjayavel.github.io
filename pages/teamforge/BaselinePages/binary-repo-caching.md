---
title: Enable Caching for Baselines
keywords: binary, repositories, caching
tags: [baseline, ctf_20.2, site_admin_tasks, binaries]
sidebar: teamforge_sidebar
last_updated: Jun 22, 2020
permalink: binary-repo-caching.html
folder: BaselinePages
summary: You can enable caching for TeamForge Baselines in case you have a large number of binary (Nexus) repositories. Caching Nexus repositories enables fast loading of Nexus repositories when you try to create or modify the binary filter criteria for baselines or baseline definitions.
---

Loading a large number of Nexus repositories while creating baslines or baseline definitions can last for longer durations—typically slowing down the entire process itself. 

By enabling caching for Baselines (which is disabled by default) and setting up webhooks for the Nexus repositories, you can quickly load the list of Nexus repositories available to filter when you create or modify baselines or baseline definitions.

1. Run the following [adhoc database query][siteadmin-adhocquery] in TeamForge's WEBR data store to get the webhook endpoint URL for Nexus and keep it handy for later use.
   ```sql
   select 'https://{DomainName}/inbox/v4/Nexus.Repo.Updates/' || publisher_id from publisherv4 where publisher_name='Nexus';
   ````
2. Enable caching for baselines by setting the [BASELINE_CACHE_ENABLED][siteoptiontokens.html#BASELINE_CACHE_ENABLED] `site-options.conf` token.
   ```shell
   BASELINE_CACHE_ENABLED=true
   ````
3. {% include installupgrade/deploy_services_without_note.html %} 
4. Set up webhooks one-by-one for every Nexus repository that is linked to TeamForge.
   1. Log on to the Nexus server. 
   2. Go to **Server Administration and Configurations > System > Capabilities**. 
   3. Click **Create Capability**. 
   4. Select the **Webhook Repository** capability type. 
   5. Select the repository you want. 
   6. Select the `Asset` and `Component` event types. 
   7. Copy and paste the webhook endpoint URL for Nexus (see Step 1) in the `URL` field and click **Create Capability**. 

This concludes the process of enabling caching for Baselines and setting up the webhooks for Nexus repositories. 

{% include links.html %}