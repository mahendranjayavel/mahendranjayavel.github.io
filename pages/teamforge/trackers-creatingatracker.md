---
title: Set up Trackers
keywords: create tracker, work flow, workflow, clone, required fields, custom tracker fields, flex fields, auto assign, 
tags: [ctf_20.0, project_admin_tasks, trackers]
sidebar: teamforge_sidebar
permalink: trackers-creatingatracker.html
last_updated: Jan 28, 2020
layouts: "pagefaqs"
summary: A Tracker is a collection of related artifacts that describe work to be done or issues to be resolved. Every project should have one or more trackers. When you start a tracker, you decide which fields will be used, who will use them, and how they will use them.
---

## What is a Tracker?

A tracker is a collection of records that follow the development of a unit of work from conception through to completion. You can create a tracker to manage almost any kind of work that your project calls for.

In each TeamForge project, you can create any number of trackers. Each tracker tracks a different type of data.

For each tracker, you can define values for status, category, and other default fields. You can create your own fields to capture additional data that is specific to your project or organization. You can also create tracker workflows to specify the criteria necessary for users to change tracker status values.

Individual tracker entries are referred to as tracker artifacts. The role-based access control system enables you to control which project members are allowed to view, create, and edit tracker artifacts. Within a project or across the projects, a tracker can be cloned along with the workflow.

Summary information about the number and status of project tracker artifacts is provided on each project's **Tracker Summary** page. The Project Dashboard also provides an at-a-glance overview of the status of each project member's projects, including information on the number and status of the tasks and tracker artifacts in each project, and project overrun and underrun statistics.

## Create a Tracker

Create a tracker whenever you need to report and track bugs, feature requests, support requests, or any other type of issue where ownership, status, and activity must be managed.

Individual tracker entries are referred to as tracker artifacts. A tracker is a set of tracker items with a common purpose, such as bug reports, feature requests, or tasks.

1. Click **PROJECT ADMIN** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. Click **Create**.
4. On the **Create Tracker** page, provide a name and description for the tracker.
   {% include tip.html content="Descriptions help users learn how best to provide the information you want from them. To maximize your chances of getting useful data, make your description as informative as you can." %}
5. Select an icon that suggests the type of work the tracker is handling. This icon will appear with any artifact in this tracker, wherever it is viewed on the site. For example, if someone brings an artifact from this tracker into a planning folder, users of the planning folder can glance at the artifact's icon to see where it comes from.
6. Select the relevant unit from the **DISPLAY EFFORT IN** field. The units displayed here are configured based on the size of the artifacts in the tracker. Eg. Select the unit as **HOURS** for a tracker of small defects, **DAYS** for a tracker of tasks, and **WEEKS** for a tracker of epics.
   {% include note.html content="Configure the units at the project level and not at the planning folder level." %}
7. Select **INCLUDE FOREIGN CHILDREN** to include points and efforts from children artifacts across the projects in TeamForge.
   {% include note.html content="In a parent artifact, enabling CALCULATE POINTS field sums and rolls up the points from all its children artifacts within the project. In this total, if you want to include children artifacts from other projects across TeamForge, have the INCLUDE FOREIGN CHILDREN option enabled." %}
8. Click **Create**. The new tracker appears at the bottom of your list of trackers.
9. If necessary, drag the tracker to a place in your tracker list that makes sense. The order you set here controls the order of every tracker list in your project.
10. You'll probably need some custom fields to capture information that's specific to your project. See [Create Custom Tracker Fields](#customfields).
11. To speed up the team's work, you may want to set up some rules for automatically reassigning artifacts when their contents change. See [Create a Tracker Workflow](#createatrackerworkflow).

## Create Custom Tracker Fields {#customfields}
To track data that is not captured by the default set of fields, create new fields that fit your project's purposes.

You can create the following user-defined fields in each tracker:
 * Up to 30 text entry fields.
 * Up to 30 date fields.
 * Up to 30 single-select fields.
 * An unlimited number of multiple-select fields.

   {% include caution.html content="Creating a large number of user fields and multiple-select fields may affect site's performance." %} 

### Create a Text Field
To let users type in data, create a text entry field.

A tracker can have up to 30 text fields.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. Click the tracker to which you want to add a text field.
4. On the _TRACKER FIELDS_ tab, click **Add Field**.
5. On the **Create Field** page, provide a name for the field.
6. Configure the shape of the field with the **Field Width** and **Field Height** fields.
7. To help users enter the right text values, select **Use Field Validation** and supply a regular expression that describes the appropriate values. This can help reduce errors and keep your team's data as meaningful as it can be. For more detailed instructions, see [Validate Text Entries in a Tracker Artifact](#validatetextentries).
8. Click **Save Field**. The new field is created.

### Create a "Select" Field
To let users choose values from a list that you define, create a "Select" field.

You can create up to 30 single-select fields and an unlimited number of multiple-select fields in a tracker.
 {% include caution.html content="Creating a large number of multiple-select and user fields may affect TeamForge's performance." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, click the tracker to which you want to add a "Select" field.
4. On the _TRACKER FIELDS_ tab, click **Add Field**.
5. On the **Create Field** page, provide a name for the field.
6. Use the **Input Type** drop-down to specify whether users will be able to select one value or more than one. If you're going to make this a required field, pick one of the values to be the default value. This value is applied to existing artifacts and artifacts that are moved from another tracker.
7. Decide whether users _must_ choose a value.
   * Required fields automatically appear on the **Create Artifact** page.
   {% include note.html content="If you make the field required, you must specify a default value. If you make a **User** field required, specify one or more default users. If you make a **Date** field required, the default is 'today'." %}
   * For optional fields, select **DISPLAY ON CREATE** if you want the field to appear when a user first creates an artifact.
   * To prevent the field from being used at all, select **DISABLED**. (By default, new fields are enabled.)
8. Use the **Values** section of the **Create Field** page to add more values for the user to choose from.
9. Keep adding values until you have the list of options you want, then click **Save Field**.

Manage Obsolete Single-select and Multi-select Custom Field Values
: It's not uncommon for single-select and multi-select custom field values to become obsolete over time. However, deleting a widely-used custom field value from a single-select or multi-select custom tracker field can undesirably affect existing artifacts that use that value. 
: To work around such a scenario, you can now hide the (obsolete) values of the single-select and multi-select custom fields from being shown on Tracker artifacts, mass artifact updates, planning folders, Planning Board, Task board, and Kanban Board. 
: A new check box, **Visible**, is now available (in the **Values** section) for single-select and multi-select field values (**Project Admin > Tracker Settings** page). Selecting and clearing this check box (while editing the tracker settings) shows and hides the values respectively.
: {% include image.html file="hide-ss-field-values.png" caption="\"Visible\" check box for single-select field values" %}
: {% include image.html file="hide-ms-field-values.png" caption="\"Visible\" check box for multi-select field values" %}

### Create a People-picker Field
To let users choose other users from a list, create a "people picker" field.

The **Assigned to** field is a people-picker field that is present in every tracker. An artifact can be assigned to only one user at a time. You can give yourself more flexibility by adding any number of custom people-picker fields.

For example, your QA team may want to assign a person to track progress on an artifact while it is assigned to a developer. You might create a people-picker called "QA monitor" to specify who that person should be.

In the people-picker fields you create, users can select multiple users.
 {% include caution.html content="Creating a huge number of user fields can slow down the site's performance." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, click the tracker to which you want to add a people-picker field.
4. On the _TRACKER FIELDS_ tab, click **Add Field**.
5. On the **Create Field** page, provide a name for the field.
6. On the **INPUT TYPE** drop-down list, select _Select User(s)_.
7. In the **DEFAULT FILTER** field, choose whether the list of people available in your new field will include members of this project or everyone who is registered on the site.
8. Configure the size of the field with the **FIELD WIDTH** field.
9. Click **Save Field**. The new field is created.

## Organize Tracker Fields
Most tracker artifacts ask the user for a lot of information. You can arrange the input fields in columns and rows to make it easier for users to find the fields they need.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of current trackers, click the tracker whose fields you want to organize. Click the _TRACKER FIELDS_ tab if it isn's already showing.
4. If some fields seem to be logically connected to each other, create a section to bring them together.
   1. Click **Add Separator** and select **Section**. Give the section a short but descriptive label.
   2. In the list of fields, drag your new "Section Separator" row to a position that makes sense.
   3. Drag the appropriate fields under the Section Separator that you just created.
5. Within a section, arrange fields logically into columns.
   1. Click **Add Separator** and select **Column**. Give the column a short but descriptive label.
   2. In the list of fields, drag your new "Column Separator" to a position that makes sense.
   3. Drag the appropriate fields under the Column Separator that you just created.
   4. Create as many columns as you need. Drag a column separator above another column separator to move it to the left in the artifact entry form. Drag it below to move it to the right.
6. Within a column, group fields into rows if appropriate.
   1. Click **Add Separator** and select **Row**. Give the row a short but descriptive label.
   2. In the list of fields, drag your new "Row Separator" to a position that makes sense, then drag the appropriate fields under the Row Separator.
   {% include note.html content="You can have rows and columns without sections." %}

## Enable or Disable Tracker Fields {#enabledisablefields}
If a tracker field is disabled, it does not appear on the Artifact page. Most fields can be disabled.

Disabled fields are accessible only to tracker administrators on the _TRACKER FIELDS_ tab.

You can enable or disable any field that is user-defined or configurable. However, you can't disable all configurable fields. For example, the **Status**, **Priority**, **Category**, and **Planning Folder** fields can't be disabled.

{% include note.html content="If your goal is to prevent users from entering data into a field when submitting an artifact, but still displayes the field on the **Edit Artifact** and **Tracker Search** pages, don' disable the field. Instead, clear the **DISPLAY ON SUBMIT** option on the **Edit Tracker Field** page."%}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of current trackers, click the tracker you want to configure.
4. On the _TRACKER FIELDS_ tab, select the fields you want to enable or disable.
   * Click **Disable** to remove them from the **Artifact** page.
   * Click **Enable** to allow them to be configured and displayed.
   {% include note.html content="Data in disabled fields is still searchable, but disabled fields do not appear as inputs on the **Search** pages." %}

## Configure Required Fields for a Tracker
If a field is set as required, users cannot create artifacts without completing it. Most tracker fields can be required or optional.

Each tracker can have its own required and optional fields. Required fields are marked with a blue asterisk (<span style="color:blue">*</span>) on the **Create Artifact** page.

{% include note.html content="When you make a field required, any field whose values depend on that fields values is also required. See [Help Users Select Options in a Tracker Artifact](#useroptions) for more information about dependednt field values." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of current trackers, click the one you want to configure.
4. On the _Tracker Fields_ tab, click the name of the field you want to set as required or optional. By default, only the **Title**, **Description**, and **Status** fields are set as required.
5. On the **Edit Field** page, select or clear the **Required** check box to make a field required or optional. Required fields automatically show up on the **Create Artifact** page.

   If you mark the user defined fields of type **Text Entry** or **Select User(s)** as **Required**, when creating or editing these fields on the **Tracker Settings** page, you can now save the configuration without providing a value for the **Default Value** field. This setting leaves the mandatory user defined fields (of **Text Entry** or **Select User(s)** type) on the **Create Artifact** page and the **View Artifact** page for the users to provide required values to these fields before creating or updating an artifact.

   {% include image.html file="mandatory_field_without_default_value.png" %}

   {% include note.html content="System-defined fields and the **Status** field are always required." %}
6. For optional fields, select or clear the **DISPLAY ON CREATE** option. This specifies whether the field will appear on the **Create Artifact** page.
7. Click **Save Field**.

## Configure Tracker "Select" Field Values {#configuretrackerfieldvalues}
To help users provide meaningful informatin, supply them with useful field values to choose from in the input fields in the tracker entry form.
 {% include tip.html content="Once a tracker has been created, you may create one or more user-defined single-select or multiple-select fields, add predefined values to the fields, remove values, if required, enable or disable fields, and change the default values for fields." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, click the name of the tracker that you want to configure.
4. On the _TRACKER FIELDS_ tab, click the name of the field whose values you want to edit.
5. On the **Edit Field** page, set up the field values you want users to see when they create a tracker artifact.
   * To define a new value, click **Add**.
   * To rename a value, edit the existing text. If you rename a value, the value is renamed in all existing artifacts.
   * To remove a value, check the box and click **Delete**. If you delete a value, the value is changed to **None** in all existing artifacts.
   * Select **DEFAULT VALUE** to set which option will be chosen if the user makes no selection. When you move a tracker artifact from one tracker to another, the default field value is the value that comes along.
   <div class="well well-sm" markdown="1">
   * When you edit the values of the **Status** field, you are also asked to describe what each value's status means, as shown in the **Values** section of the **Edit Field** page. This status meaning is used in Advanced Search to define which values are returned when searching for open or closed artifacts.
   * As always, when you create a new tracker, the default value for the '**Priority**' field is set as '4 - Low'. However, you can change the default value by editing this configurable single select field, '**Priority**'. You cannot delete or disable the **Priority** tracker field.
   * When you change the tracker fields, the values in the existing artifacts remain unchanged.
   </div>
6. Click **Move Up** or **Move Down** to order the list the way want it.
7. Click **Save Field**.

All values are now available in the selection menu for the field.

## Configure Tracker Units
You can estimate the value of efforts meaningfully in the form of units using the TeamForge tracker.

You can set any unit as the default for a tracker or planning folder and create any number of units. The default base unit is 'Hours' which you can rename, but not delete. You can also toggle between the burndown chart and effort values for any unit.
 {% include note.html content="You cannot enter decimal values in the **Conversion** field. Deleting a unit will cause all the associated artifacts to express effort in the form of the base unit." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. On the _UNITS_ tab, click **Add**.
4. On the **Add Unit** page, enter the **UNIT NAME** and **CONVERSION** value for the unit.
5. Click **Save**.

## Configure Default Tracker Columns 
When you're looking at the artifacts list in a tracker, a planning folder or a team, you can select the columns you want to see, either for this session or permanently.

You set your column preferences for each tracker, planning folder or team independently. If your project administrator has set default columns for the entire project, your individual column choices override those settings.

1. Click **Trackers** from the **Project Home** menu.
2. Select a tracker, planning folder or team and click **COLUMNS > Configure**.
   * If you've already saved a column configuration, click it and skip the rest of these steps.
   * To go back to the default column configuration, click **System (default)** and skip the rest of these steps.
   * To set up a new configuration, click **Configure**.
3. Choose your columns.
   1. Move the columns you want from **Available Columns** to **Selected Columns**. **Artifact ID: Title, Priority** and **Status** are required columns.
      {% include note.html content="Selecting more columns can increase the time required to load the listing page." %} 
   2. Remove any columns you don't need from **Selected Columns**.
   3. Use the move up and move down arrows to change the display order of the columns.
4. Apply your choices to your view of the tracker.
   * To use this arrangement this time only, click **Apply**. The next time you log in, you'll start with the default view again.
   * To save your column layout for repeated use, click **Apply and Save**, then give your arrangement a name. The next time you log in, you'll see the column arrangement you just selected. (If you've sorted the records in your view that sort order is saved too.)
     {% include tip.html content="If you are editing a column configuration that already exists, you can rename it by saving it under a new name." %}
5. To make the same set of columns appear every time you come to this tracker, planning folder or team, click **COLUMNS > Save** and from **Save Column Configuration** page, select **Make this my default view**.  
6. To make the same set of columns appear for every user the first time they see any tracker, planning folder or team in the project, click **COLUMNS > Save** and from **Save Column Configuration** page, select **Make this the default view for all project members**.

The project default configuration you set is now the default configuration for all project members, unless they have created their own personal default column configuration.

## Create a Tracker Workflow {#createatrackerworkflow}
To channel project member's work on tracker items, set up rules for how a tracker item can move forward.

Before creating a tracker workflow, see that these criteria are met:
 * You have a tracker to work with.
 * The tracker has a set of statuses defined, such as "In progress" and "Ready for QA".
 * Roles exist, and you can assign project members to them.

A workflow is a sequence of changes from one status to another. You can define status transitions for any combination of tracker statuses in the tracker.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, select a tracker.
4. Click the _WORKFLOW_ tab. The **Workflow** page lists all of your status values and the tracker workflow that you have configured.
5. On the **Workflow** page, click the status value for which you want to create a workflow.
6. On the **Edit Field Transition** page, select a status value from the **Create Transition to Status** drop-down menu.
7. Click **Add**. A new workflow is added. The **Any** workflow is changed to **Remaining Statuses**.
8. In the **ROLES** section, specify which users can make this changes. For example, only users with the QA Engineer role are allowed to change artifacts from **Open** to **Cannot Reproduce**.
9. Click the _Advanced Transition_ link.   
    {% include note.html content="For any new unsaved transition, an alert is shown asking you to save the transition so that you can it in the **Transition Status To** drop-down list. Click **OK** to configure already saved transitions or click **Cancel** and then click **Save and View** in the **Edit Field Transition** page to save the unsaved transitions." %}
    {% include image.html file="17-4-advanced-transition.png" %}
    1. Select the transitions workflow for which you want to apply Advanced Transition settings from the **Transition Status To** drop-down list.
    2. Select the **REQUIRED** check box against the fields for which the user _must_ provide values. For example, the user must assign the tracker item to someone and enter a comment.
       {% include note.html content="Fields whose values depend on a required parent field are automatically required. See [Help Users Select Options in a Tracker Artifact](#useroptions) for more information on parent and child fields." %} 
    3. Select or unselect the **Visible** check box for showing or hiding fields respectively for the selected status transition. 
    4. Select the values on the **AUTO POPULATE** column for the fields, which you want to get populated during the selected workflow transition.
       {% include image.html file="17-11-autopopulate.png" %}

    <div class="well well-sm" markdown="1">
    Points to note:
    * **Required** fields are always visible. 
    * Advanced Transition rules are applied when you create or edit artifacts in a tracker and only when edit artifacts in Planning, Task, and Kanban boards.
    * Hidden field values, if updated via SOAP/REST APIs, are ignored.
    </div>

10. Click **Save**.

The workflow is now saved. When a user submits or edits the status of a tracker artifact, he or she sees only the options that are allowed by the workflow. 

## Change a Tracker
A tracker's real-world uses often outgrow the name or description you gave it when you created it. When that happens, it is a good idea to update the tracker to reflect its changing role.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, click the tracker you want to edit, and click **Edit**.
4. On the **Edit Tracker** page, provide a new name or description for the tracker, and update the icon.
5. Update the units from **DISPLAY EFFORT IN** and click **Save**.
   {% include note.html content="These units are configured in the **Units** page at the project level, and not at the planning folder level." %}
6. Select **INCLUDE FOREIGN CHILDREN** to include points and efforts from children artifacts across the projects in TeamForge.
   {% include note.html content=" In a parent artifact, enabling **CALCULATE POINTS** field sums and rolls up the points from all its children artifacts within the project. In this total, if you want to include children artifacts from other projects across TeamForge, have the **INCLUDE FOREIGN CHILDREN** option enabled." %}
7. If necessary, drag the tracker to a place in your tracker list that makes sense. The order you set here controls the order of every tracker list in your project.

## Clone a Tracker
To save efforts in duplicating a tracker within the project and across the projects, choose cloning options available in TeamForge.

You can clone a tracker within a project along with the workflow. This can be done across the projects as well. If you are the Project Admin for the source and destination project, you can create new roles that are available in the destination project. However, the permissions associated with the role are not copied from the source project. A tracker admin cannot create new roles while cloning a tracker across projects.

1. Click **Project Admin** from the **Project Home** menu.
2. From the **Project Admin Menu**, click **Tracker Settings**.
3. Select **Clone External Tracker** from the drop-down list available in **Clone** button to clone a tracker from the source project.
   {% include note.html content="To clone a tracker within the project, you can select the tracker from the **Tracker Settings** page and click **Clone Tracker**." %}
4. On the **Cloning Tracker** page, name the new tracker and enter a suitable description.
5. Enter **SOURCE TRACKER ID** of the tracker available in the source project and click **Next**. The **Cloning External Tracker** page appears.
6. On the **Cloning External Tracker** page, name the new tracker and enter a suitable description.
7. Click **Create**. The cloned tracker appears at the bottom of your list of trackers.

## Auto Assign Tracker Artifacts 
You can configure the tracker to automatically assign newly submitted artifacts to specific project members.

You can assign artifacts to individuals based on the values in the **Category** or *Release** field.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings**.
3. From the list of existing trackers, click the tracker you want to configure.
4. On the _AUTO ASSIGNMENT_ tab, select **Auto Assign By Category** or **Auto Assign By Release**.
5. For each category or release value, choose a project member from the **AUTOMATICALLY ASSIGN TO** drop-down menu. This menu contains all project members with the tracker edit permission. Click the **Search** icon to display a list of project members to whom you can auto-assign artifacts. Choose `None` if you do not want artifacts with a specific value automatically assigned.
6. Click **Save**.

Whenever a new artifact is submitted with a value in the relevant field, the assignee receives an email notification and the artifact appears on the assignee's **My Page**.

## Help Users Select Options in a Tracker Artifact {#useroptions}
You can help users cope with complex information by guiding them to eligible values in single-select fields.

Any tracker that manages real-world information will quickly become very complex. Users can be confused by a proliferation of "Select" fields. Confusion can lead to inconsistent data, which makes your job harder.

You can help relieve the complexity by showing users their eligible options in a given field based on values they have already selected in another field. You can create overlapping sequences of dependent fields, with as many levels as you need.

This simplifies things for the user, but for the tracker administrator it can quickly get complicated. So let's look at an example.

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings** and create a tracker. For this example, let's call it the _Lunch Planning_ tracker.
3. Create a single-select field and call it **Lunch type**. (For this example, we'll ignore the built-in fields, such as **Status** and **Assigned to**. We're just working with fields that you create.)
4. Create some values for the **Lunch type** field. Let's call them Buffet, Picnic, and Banquet.

   Each type of lunch will make sense in some kinds of locations and not others. For example, you would not normally plan a banquet lunch in a park. We are now going to make it easy for users to avoid making such a mistake.
5. Create a single-select field called **Location type**, with Lunch type as the parent field, and give it some plausible values.
   1. Start by adding an option called Beach. In the **Parent Values** column, choose Picnic, because that's the kind of lunch you would have at the beach. (The **Parent Values** column lists all the values in the parent field you selected.)
   2. Add a `Restaurant`. In the **Parent Values** column, hold down the **Ctrl** key and choose `Banquet` and `Buffet`, because either of those could be held at a restaurant.
6. Create a single-select field called **Location**, with `Location Type` as the parent field, and give it some values to choose from.
   1. Start with an option called `Happy Food Restaurant`. In the **Parent Values** column, select `Restaurant`, because that's the type of location that Happy Food Restaurant is.
   2. Add another option, `Hanalei Cove`. Under **Parent Values**, select `Beach`.
7. Save your work and go to the tracker whose settings you have been editing. Try selecting from the interdependent values you have just created.

Observe that the value you choose in the **Lunch Type** field controls which values are available to you in the **Location Type** field, and that selecting a value in **Location Type** in turn controls the values that appear in the **Location** field.
 * When a user selects `Banquet` for a lunch type, they can select `Restaurant` but not `Beach` in the **Location Type** field. You will have less error correction to do, and users will avoid confusion.
 * When a user selects Picnic for their lunch type, the **Location Type** field offers only `Park` and `Beach`. Now you will not have to go through and clean up after users who mistakenly choose to plan a picnic at Happy Food Restaurant, and the doorman at Happy Food Restaurant will not have to turn away users who mistakenly show up with picnic baskets.   
 {% include important.html content="If you are used to defining your own Tracker fields, the ability to make field values depend on other values may change how your trackers work in ways you didn't anticipate. Keep these points in mind:" %}

 <div class="well well-sm" markdown="1">
 * Linking fields in this way doesn't modify existing data, but when users later modify fields that are linked, they will have to adhere to the relationships you set here. 
 * If a field has a parent, and that parent field also has a parent, the top-most parent field must have at least one value.
 * When a field has a parent field that is required, the child field's default value is set to None. If that required parent field is deselected, the child field no longer has to be required, but Required remains the default.
 * If you require a specific field value before an artifact can be placed in a given status, that field's children are subject to the same requirements. See [Create a Tracker Workflow](#createatrackerworkflow) for more about controlling what status an artifact can be in.
 * If you delete a field that contains values that another field's values depend on, the dependent field becomes a standard single-select field on its own.
 * When you cut and paste an artifact from one tracker to another, only those field values that also exist in the new tracker come along with the artifact. If those values aren't valid under the dependency rules of the new tracker, they are still brought along.
 </div>

## Validate Text Entries in a Tracker Artifact {#validatetextentries}

You can help users contribute useful information by testing their text entries against rules you configure.

Text fields can be error-prone because they invite free-form input. You can help users provide usable information by automatically rejecting values that don't match the needs of the tracker.

This simplifies things for the user, but for the tracker administrator it can be complicated. So let's look at an example.
  {% include note.html content="If your goal is to require users to enter some value, whatever the value is, don't use text field validation. Select the Required option instead." %}

1. Click **Project Admin** from the **Project Home** menu.
2. Click **Tracker Settings** and create a tracker. For this example, let's call it the _Bugs_ tracker. It will be used to record entomological specimens in a collection.
3. Create a text field and call it **Legs**. This is for users to record the number of legs each specimen displays.
4. Select **USE FIELD VALIDATION** and supply a validation rule that requires the user to enter a number. For example, if a given insect has six legs, you'll want the user to enter the numeral **6**, and not a string such as "six" or "several."

   Try this regular expression: `\d{1,3}`

   This rule requires the user to enter a number with one, two or three digits. Now, a user who means to record a centipede with 100 legs but enters 1000 by mistake will not be able to save the artifact until the error is corrected.

5. Enter a sample string to test your regular expression. Any part of the sample string that matches your regular expression appears under **Match Results**. If nothing appears, rework your regular expression until you get a match.
6. Create another text field and call it **Location**. This is where users will record the geographical spot where they collected the bug.
7. Select **Use Text Validation** and supply a validation rule that requires the user to enter a pair of geographical coordinates. For example, if a given insect was found outside CollabNet's California headquarters, you'll want the user to enter a string like `37.674689,-122.384652`, and not something like "Brisbane" or "Out on the lawn."
   
   Try this regular expression: `[-]?[0-9]*[.]{0,1}[0-9]{0,4}`

   This rule requires the user to enter two numbers, separated by a comma, in the general format of a pair of mapping coordinates.
     {% include note.html content="This particular regular expression does not guarantee that the coordinates are valid, just that they look like coordinates." %}
8. Save your work. In the tracker whose settings you have been editing, try entering a number greater than 999 in **Legs**, or a street address in **Location** The red **X** next to the field indicates that the text entry is incorrect. A green check indicates that the value meets the requirements.

Notice that any field in which you are validating text entries is identified by **Text Entry (with Field Validation)** when listed on the _TRACKER FIELDS_ tab.  

## Graphical Workflow Viewer for Trackers

You can now easily understand and interpret the tracker workflows meant for a specific user role with the help of a graphical workflow viewer.

The graphical representation of any workflow shows what the user with a specific role can do. However, the required fields, hidden fields, and auto populate fields set in the workflow are not shown in the graphical representation. To view the graphical representation of a workflow for a specific role:

1. Click **PROJECT ADMIN** from the **Project Home** menu.

2. Click **Tracker Settings**.

3. From the list of existing trackers, select a tracker.

4. Click the **WORKFLOW** tab.

5. On the **Workflow** page, click the **Graphic View** button. The following screen with the graphical view of the workflows for the selected role is shown.

   {% include image.html file="17-8-graphicalview.png" %}

This workflow is read-only and non-editable. The **Roles** drop-down list contains the user roles (as seen in the tabular view) for the which workflows have been configured, in addition to the default roles: `All users with create permission and All users with edit permission`.


{% include links.html %}