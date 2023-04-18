---
title: pebble-dep.xml 
keywords: authentication, pebble deployment configuration file
tags: [installation, upgrade, site-options.conf, config_files]
sidebar: teamforge_sidebar
permalink: pebble-dep-xml.html
last_updated: Feb 27, 2018
toc: false
summary: The pebble-dep.xml file, also known as the Pebble deployment configuration file, contains the data that Pebble needs to interact with the TeamForge site.
---

**A sample pebble-dep.xml file for the REST service type**

```shell
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE integrated-application 
  PUBLIC "-//CollabNet, Inc.//DTD Integrated Application Descriptor 1.0//EN"
  "http://schema.open.collab.net/sfee50/dtd/sf-pluggable-deploy-descriptor_1_0.dtd">
<integrated-application>
    <name>Pebble Blog</name>
    <baseurl>https://cu064.cloud.sp.collab.net:13001/pebble/index.jsp</baseurl>
    <gourl>https://cu064.cloud.sp.collab.net:13001/pebble/gourl/%p/%o</gourl>
    <endpoint>https://cu064.cloud.sp.collab.net:13001/pebble/services/rest/ctfapi</endpoint>
  <servicetype>REST</servicetype>
</integrated-application>
````

**A sample pebble-dep.xml file for the SOAP service type**

```shell
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE integrated-application 
  PUBLIC "-//CollabNet, Inc.//DTD Integrated Application Descriptor 1.0//EN"
  "http://schema.open.collab.net/sfee50/dtd/sf-pluggable-deploy-descriptor_1_0.dtd">
<integrated-application>
    <name>Pebble Blog</name>
    <baseurl>https://cu177.cloud.maa.collab.net:13001/pebble/index.jsp</baseurl>
    <gourl>https://cu177.cloud.maa.collab.net:13001/pebble/gourl/%p/%o</gourl>
<endpoint>https://cu177.cloud.maa.collab.net:13001/pebble/services/PebbleIntegrationService</endpoint>
    <servicetype>SOAP</servicetype>
</integrated-application>
````

{% include links.html %}