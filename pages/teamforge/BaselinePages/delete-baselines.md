---
title: Delete Baselines
keywords: delete, baselines
tags: [baseline, ctf_20.1, role_based_access_control]
sidebar: teamforge_sidebar
last_updated: Apr 16, 2020
permalink: delete-baselines.html
folder: teamforge
summary: You can delete Open and Rejected (meta status) baselines as long as you have the DELETE/VIEW BASELINE permission assigned to you. You cannot delete approved baselines.
---
<!-- Artifact artf396075 : [Doc Task]artf395756 : A new permission "DELETE/VIEW BASELINE" should be available for selection to assign to a given role -->
Users with the DELETE/VIEW BASELINE permission can:

* View baselines
* Search for baselines
* Compare baselines
* Delete Open and Rejected (meta status) baselines. 

You can only delete baselines one-by-one from the **View Baseline** page.

To delete a baseline:
1. Select an Open or Rejected baseline to view it.
2. Click the **Delete this baseline** link on the **View Baseline** page. 
   {% include image.html file="201-deleteb-01.png" caption="Delete this baseline link" %}
   A confirmation message appears. 
3. You must type a reason to delete the baseline and click **Yes, I'm sure**.
   The comment/reason you type is stored in the database and is associated with the baseline you are trying to delete.
   {% include image.html file="201-deleteb-02.png" caption="Type a reason to delete the baseline" %}
   The baseline is deleted.

   An email notification is sent to the user that created the baseline, the users that acted (update, review or reject) on the baseline and the users that monitor the baseline.

{% include links.html %}


