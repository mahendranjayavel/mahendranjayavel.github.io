---
title: Reference Information for AngularJS Customization
keywords: teamforge, custom, angularjs, customization
tags: [ctf_20.1, extend_teamforge, customize, site_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: angularjscustomizationreference.html
last_updated: May 5, 2020
summary: Some references to work with UI/AngularJS customizations.
---

## Suggested Tools
1. Any IDE that supports AngularJS : Inellij IDE or WebStorm or Visual Studio Code
2. Maven for packaging the code into jar file
3. Chrome Browser Devleoper Tools
4. Chrome Plugins
   * AngularJS Batarang
   * AngularJS Graph 

## The Final Jar File Structure Should Look Like

```shell
customization.jar
 |
 +-- META-INF
 |    +-- MANIFEST.MF
 +-- js/
 |    +-- <all-js-files-here>
 +-- css/
 |    +-- <all-css-files-here>
 +-- bundle/
      +-- images/
           +-- <all-image-files-here>
````

## Example MANIFEST.MF

```shell
Manifest-Version: 1.0
Built-By: janeDoe
Created-By: Apache Maven 3.5.2
Build-Jdk: 1.8.0_171
CTF-Customization-Name: ex01-logo-customization
CTF-Customizations-Enabled: True
CTF-CSS-Customization: css/customization.css
CTF-JS-Customization: js/custom.js
CTF-Bundle-Customization: bundle/
````



{% include links.html %}