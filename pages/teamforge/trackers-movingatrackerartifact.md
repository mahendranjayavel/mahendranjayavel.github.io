---
title: Move a Tracker Artifact (Cut and Paste)
keywords:  move a tracker artifact, cut, paste
tags: [project_member_tasks, trackers]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Dec 6, 2018
permalink: trackers-movingatrackerartifact.html
summary: As work proceeds on a tracker artifact, its focus may change. If this happens, it may be appropriate to move the artifact into a different tracker, or to a tracker in a different project.
---
To move a tracker artifact between projects, you must have either the tracker administration permission or tracker `View`, `Submit`, `Edit`, and `Delete` permissions in both the source and destination projects.

You can move one or more tracker artifacts in the same operation.

1. Click **Trackers** from the **Project Home** menu.
2. On the list of project trackers, click the title of the tracker containing the tracker artifact that you want to move.
3. Select the tracker artifact (or artifacts) that you want to move, and click **Cut**. Digital.ai TeamForge removes the tracker artifacts and places them on the clipboard.
4. Go to the tracker into which you want to paste the tracker artifacts.
   {% include note.html content="To move the tracker artifacts into another project, first find the destination project using your **Projects** menu." %}
5. Click **Paste**.
   * If all artifact assignees have the appropriate permissions in the destination tracker, the tracker artifacts are now moved.
   * If not, the **Paste Artifacts** window shows you the number of tracker artifacts that cannot be reassinged automatically.
6. Choose one of the following methods to reassign any unassigned tracker artifacts.
   * **Reassign Artifacts to**: Assigns all unassigned tracker artifacts to the project member you select.
   * **Myself**: Reassigns all unassigned tracker artifacts to you.
7. Click **Next**.

The tracker artifacts are now moved to the destination tracker. The details of the move are recorded in the **Change Log** tab of the **Artifact Details** page.
  * If the project members to whom the tracker artifacts are assigned have the appropriate permissions in the destination project, the tracker artifacts are automatically reassinged to the same project members. If not, you are offered several options for reassigning them.
  * If both trackers use the same user-defined fields and field values, values in these fields are retained.
  * If each tracker uses different user-defined fields or field values:
    * Values are set to the default value, if one was specified by the tracker administrator. Default values are mandatory for required fields.
    * Values are set to **None**, if no default value was specified by the tracker administrator.

{% include links.html %}