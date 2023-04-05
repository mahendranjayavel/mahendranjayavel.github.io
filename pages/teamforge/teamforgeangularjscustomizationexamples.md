---
title: AngularJS Customization Examples
keywords: teamforge, extend, angularjs, customize, customization, example
tags: [ctf_20.1, extend_teamforge, customize, site_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforgeangularjscustomizationexamples.html
last_updated: Mar 5, 2019
layouts: "pagefaqs"
summary: Here are some examples to cover the basic AngularJS customization use cases. 
---


## Introduction

Here you can find examples that use JavaScript/AngularJS, CSS, and images to customize the UI.

The examples provide the location of the jar file that you can download and alter it to your specific use case. Also, you can use the jar file **as-is** in your test/stage TeamForge instance to see it in action.

You can disable the customization by disabling the custom event handler.

{% include note.html content="The example customization jars discussed in here are intended for illustrative purposes only." %}

## Basics

Before you begin:
 1. Identify the URL of the page that you want to customize.
    * If the URL starts with `<host>/ctf/...`, then you need the `ctf` module.
    * If the URL starts with `<host>/sf/...`, then you need the `saturn` module.
 2. For JSP pages, as you are targetting a specific page for customization, make sure you put the safety net around your js customization code.
 
    ```javascript
     var ctfModule = angular.module('saturn');

     ctfModule.run(['browserService', 'customizationService', 
       function (browserService, customizationService){

         if (browserService.getLocationContainsAction('STRING_WITH_PART_OF_THE_URL_WE_WANT_TO_CUSTOMIZE')) {
      
           // Your actual customization code goes here

         }

     }])
    ````
 
## Customization Example—Customize Images
This example illustrates how to replace an image and a small bit of CSS (to do the replacement). 

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[Download](downloads/ex01-logo-customization.jar) the customization JAR file.
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
[Download](https://docs.collab.net/teamforge203/downloads/ex01-logo-customization.jar) the customization JAR file.
{% endunless %}

## Customization Example—JavaScript Alert

This example illustrates:
* the way to include custom JavaScript.
* that the custom JavaScript runs at the end.
* that custom JavaScript runs on **every** page.

As the custom JavaScript runs on every page, you need to safeguard it to execute **only** on the page you intend to customize.

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[Download](downloads/downloads/ex02-basic-javascript-alert.jar) the customization JAR file.
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
[Download](https://docs.collab.net/teamforge202/downloads/ex02-basic-javascript-alert.jar) the customization JAR file.
{% endunless %}

# Customization Example—AngularJS Availability Check

This example checks if the AngularJS is available and prints a message in the browser console. A nomral message if the AngularJS is enabled. If not, an error.

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[Download](downloads/downloads/ex03-angular-availability-check.jar) the customization JAR file.
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
[Download](https://docs.collab.net/teamforge202/downloads/ex03-angular-availability-check.jar) the customization JAR file.
{% endunless %}

# Customization Example—Remove a Button in a Full AngularJS Page

This example illustrates:
* how to hook into angular in a full AngularJS page.
* how to use safety check to do customization only on the page we intend.
* how to remove the **Delete** button from the **Project > Reports** page.

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[Download](downloads/downloads/ex04-custom-service-remove-button.jar) the customization JAR file.
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
[Download](https://docs.collab.net/teamforge202/downloads/ex04-custom-service-remove-button.jar) the customization JAR file.
{% endunless %} 

{% include links.html %}