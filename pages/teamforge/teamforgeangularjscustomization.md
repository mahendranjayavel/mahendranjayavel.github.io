---
title: AngularJS Customization in TeamForge
keywords: teamforge, extend, angularjs, customize, customization
tags: [ctf_20.1, extend_teamforge, customize, site_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforgeangularjscustomization.html
last_updated: May 5, 2020
layouts: "pagefaqs"
summary: You can customize TeamForge AngularJS pages using the APIs available. 
---

## Introduction
As part of the AngularJS customization, a robust API has been added that allows TeamForge customers to customize the look and feel and the behavior of TeamForge for their specific needs.

This works for both JSP pages and full AngularJS pages.
 - JSP page URLs would look like: `https://host-name-here/sf/`
 - Full AngularJS page URL would look like: `https://host-name-here/ctf/`
 
{% include warning.html content="The difference between JSP and AngularJs pages is that the JSP pages (i.e URLs with `/sf/`) are not SinglePage Application pages and reload in full on every server request." %}

For JSP pages, it is important to safeguard the customization code as the page reloads in full. This can be achieved by the follwing code snippet.

```js
var ctfModule = angular.module('saturn');

ctfModule.run(['browserService', 'customizationService', 
  function (browserService, customizationService){

  if (browserService.getLocationContainsAction('STRING_WITH_PART_OF_THE_URL_WE_WANT_TO_CUSTOMIZE')) {
      
    // Your actual customization code goes here

  }

}])
```

{% include warning.html content="Some of the TeamForge pages use Angular7 or later." %}

## API
The AngularJS framework defines a service called customizationService that is responsible for the definition of:
* Form Fields API
* Buttons API

### Form Fields API
Every html `<form>` in AngularJS pages is associated with a field set. For example, the login form is associated with the field set named "core_login". Doing a customization to this form will involve getting the field set named "core_login" and making the required modifications to it.

The customizationService service exposes the methods to interact with field sets.

* `createFieldSet(fieldSetName)`: Where fieldSetName is a String and returns a new FieldSet. 
* `getFieldSet(fieldSetName)`: Where fieldSetName is a String and returns a FieldSet if there is a FieldSet under this name or undefined if there is no FieldSet under this name.

#### The `FieldSet` Object
The FieldSet object exposes the methods.

* `addField(fieldName, fieldInfo)`: Adds a field to a FieldSet with given `fieldName` and `fieldInfo`. 
  Note that if a field with the same name is added twice, then the field will appear twice in the form. `fieldInfo` can be one of the following:
  * A JavaScript object, in this case it is expected that the object is the representation of the form field.
  * A function: A fully Angular injectable function that results in either a JavaScript object (that is the representation of the field) or An Angular promise (that results in the representation of the field when fulfilled).
* `removeField(fieldName)`: Removes a field from a FieldSet. 
* `interceptField(fieldName, fn)`: Intercepts a field that was previously added so it can be modified. 
  
  `fn` (function) is a fully injectable function. The local field will be used to inject the field as it was added (or previously intercepted).

  The `fn` returns
  * if its undefined then it is expected that `fn` modified the field object in-place. 
  * a new JavaScript object that will override the previous field information. 
  * an Angular promise that will resolve into the new field information.

* `reorderFields(fn)`: Reorders the fields within the given form.
  
  The `fn` (function) is a function that returns the order in which the fields should appear. The function `fn` can return
  * an array of the name of the fields in the order they need to be displayed.
  * a promise to an array with this same information. 


#### The field object#
Label properties
- label: The label text or i18n text
- tooltip: The tooltip for the label or the i18n tooltip for the label
- for: The property of the attribute `for` used for accessibility

Field information
- type: The type of the field, which can be one of the following—`text`, `email`, `email-list`, `picture`, `radio`, `textarea`, `include`, `checkbox`, `select`, `i18n-template`
- prepend: Defines a bootstrap prefix to text-like fields
- mobile: Configuration for mobile browsers
- placeholder: Defines a placeholder for text-like fields
- focus: If focus should be placed on this field when the field is first displayed
- postfix: A text, i18n text or template postfix
- postfixLocals: Local variables for the posfix (this is only useful when using a template)

Validation
- required: Defines if the field is required. The possible values are—`true`, `false` and `'noDisplay'`. The `'noDisplay'` option marks the field as required but does not show the star (*) at the end of the field
- maxLength: The max length of the field

Custom validation
- doChange: Function that gets called to validate a field, the function receives the value of the field and it is expected to return if the value is valid or not
- watchFunction (Advance use only): definition of the $watch function that will process the value that will be used to call the `doChange` function. This is only needed when there is a need for validations that involve multiple fields
- template (Advance use only): Template to show a custom validation checks

Display
- readOnly: If the field is readOnly
- hide: If the field should be hidden (in a strict sense, the field will not be displayed at all and not changed to a field of type `hidden`)

Properties specific to fields of type `picture`
- fileName: When editing the picture, property to be used to store the file name
- fileSize: When editing the picture, property to be used to store the file size
- fileType: When editing the picture, property to be used to store the file type
- dropZoneOutterClass: Class used on the outter element
- dropZoneInnerClass: Class used on the inner element
- dropZoneLabel: Label to be displayed when editing the picture
- iePreviewImage: IE does not support data URI images, so this image will be used as a placeholder when there is an image present
- imgClass: Class for the image
- noPhotoImg: Path to the image to be displayed when there is no image present

Properties specific to fields of type `email-list`
- keys: Number of emails in the list (when editing)

Properties specific to fields of type `radio`
- values: Values for the radio buttons

Properties specific to fields of type `textarea`
- size: Defines the size using a class on the textarea

Properties specific to fields of type `include`
- src: The path to the template to include

Properties specific to fields of type `i18n-template`
- description: The text or template to render
- locals: Locals on the template to render


### Buttons API

As part of the customization API, new button groups (group of buttons that work together) can be added, new buttons can be added and existing buttons can be intercepted.

The following code shows how to add a new button group.

```js
var ctfModule = angular.module('saturn');

ctfModule.run(['customizationService', function (customizationService) {

    //Create a button group and a set, then assing the group to the set, so they all work together
    var createSomeButtonGroups = customizationService.createButtonGroupSet('project_Some'),
    createSomeButtonGroup1 = customizationService.createButtonSet('project_Some/Group1');

    createSomeButtonGroups.addButtonGroup('group1', {group: 12, buttons: 'project_Some/Group1'});

    createSomeButtonGroup1.addButton('cancel', function () {
      return {type: 'link', href: '/sf/some/do/listSome/', label: {bundle: 'project', key: 'Some/button/cancel'} };
    });
    
    createSomeButtonGroup1.addButton('save', ['submitSomeFunctionHook', function (submitSomeFunctionHook) {
      return {type: 'button', 
                 click: submitSomeFunctionHook, 
                 disableOnInvalid: true, 
                 label: {bundle: 'project', key: 'Some/button/save'}};
    }]);
}]);
````

The following code snippet shows how to add a new button.

```js
var ctfModule = angular.module('saturn');

ctfModule.run(['customizationService', function (customizationService) {
    //Get the existing button set and add another button to it
    customizationService.getButtonSet('project_Some/Group1').addButton('exampleOfAddingNewButton',
    {type: 'link', href: '/sf/sfmain/do/someOtherUrl/', label: 'another label'});
}]);
````

The following code snippet shows how to intecept an existing button.
```javascript
var ctfModule = angular.module('saturn');

ctfModule.run(['customizationService', function (customizationService) {
    //Intercept an existing button and change its url
    customizationService.getButtonSet('project_Some/Group1').interceptButton('exampleOfAddingNewButton', function (button) {
        button.href = '/sf/sfmain/do/someOtherUrl/Updated'; 
    });
}]);
```

{% include links.html %}