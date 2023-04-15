---
title: TeamForge Webhooks-based Event Broker Settings
keywords: webhooks, event broker
tags: [ctf_20.0, ctf_19.3, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: webhooks-event-broker-settings.html
last_updated: Feb 11, 2020  
summary: The TeamForge Webhooks-based Event Broker related settings are discussed in this page.
---

## Components

The TeamForge Webhooks-based Event Broker deployment consists of three components:

* the native binary,
* PostgreSQL database, and 
* the configuration file

## Configuration Parameters

<table>
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>WebrHost</td>
    <td>Hostname/IP of server where the TeamForge Webhooks-based Event Broker is running. This is used to dynamically send across the publishing endpoint for publishers.</td>
  </tr>
  <tr>
    <td>WebrPort</td>
    <td>Port number where the TeamForge Webhooks-based Event Broker will run.</td>
  </tr>
  <tr>
    <td>CertFile</td>
    <td>Certificate file. Mandatory as the TeamForge Webhooks-based Event Broker uses only secure HTTP.</td>
  </tr>
  <tr>
    <td>KeyFile</td>
    <td>Key file. Mandatory as the TeamForge Webhooks-based Event Broker uses only secure HTTP. Both the KeyFile and the CertFile should be present in the same directory where the TeamForge Webhooks-based Event Broker runs.</td>
  </tr>
  <tr>
    <td>WebrAdminUser</td>
    <td>The TeamForge Webhooks-based Event Broker administrative user name. There is only one admin user.</td> 
  </tr>
  <tr>
    <td>WebrAdminPassword</td>
    <td>The TeamForge Webhooks-based Event Broker admin user password. This is stored as an encrypted string and is decrypted at runtime by the TeamForge Webhooks-based Event Broker.</td>
  </tr>
  <tr>
    <td>DBServer</td>
    <td>The server where PostgreSQL instance is running.</td>
  </tr>
  <tr>
    <td>DBName</td>
    <td>The database name to which the TeamForge Webhooks-based Event Broker must connect. This is created automatically during installation and seeded with data.</td>
  </tr>
  <tr>
    <td>DBUser</td>
    <td>PostgreSQL username that the TeamForge Webhooks-based Event Broker server should use to connect to the database.</td>
  </tr>
  <tr>
    <td>DBPassword</td>
    <td>The TeamForge Webhooks-based Event Broker database password.</td>
  </tr>
  <tr>
    <td>MaxQueuedToSend</td>
    <td >This is used for TOPIC senders. This controls the number of messages each sender has to cache, while sending data. A higher number reduces database hits, while marginally increasing memory requirements. Default is 500. For more information on TOPIC senders, see <a href="http://docs.collab.net/teamforge221/topic-event-type.html">TOPIC Event Type</a>.
    </td>
  </tr>
  <tr>
    <td>TeamForgePlugin</td>
    <td>TeamForge plugin details are specified. This is used to authenticate with TeamForge for publishing data to TeamForge.</td>
  </tr>
  <tr>
    <td>TeamForgePlugin.Host</td>
    <td>TeamForge hostname</td>
  </tr>
  <tr>
    <td>TeamForgePlugin.Username</td>
    <td>TeamForge system username</td>
  </tr>
  <tr>
    <td>TeamForgePlugin.Password</td>
    <td>TeamForge system user password</td>
  </tr>
</table>

{% include note.html content="Inspection of the configuration file will reveal other configuration parameters as well. But
these pertain to the older v2 engine and are currently deprecated. These will be removed in the next release." %}

## Enhanced Logging

The TeamForge Webhooks-based Event Broker provides minimal logging by default. All exception conditions provide a trace in the service log. However, it is possible to turn on enhanced logging for debugging purposes. When a GET is executed on `host:port/v4/instrument/on`, enhanced logging is turned on. 

This provides a complete trace of all methods executed, entry and exit times of functions, payload values, subscription cache hits and values, and a host of other information.

Executing a GET on `host:port/v4/instrument/off` will turn off enhanced logging.

## Debugging Features

Invoking `host:port/debug` will show complete information on runtime debug. The dump can also be obtained using pprof tools. 

A sample screenshot is shown here:

{% include image.html file="webr-pprofs-sample.png" %}


Details related to the memory allocation, goroutines (processes) running, heap, CPU, and memory profile can be obtained on the running instance.


{{site.data.alerts.hr_shaded}}
#### Related Links

[Scripts and Filters in the TeamForge Webhooks-based Event Broker][scripts_filters]


{% include links.html %}