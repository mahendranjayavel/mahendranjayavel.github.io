---
title: Lab Management 
keywords: FAQ, frequently asked questions
tags: [faq, lab_management]
sidebar: teamforge_sidebar
permalink: labmanagement-faqs.html
last_updated: Apr 2, 2018
summary: These are some of the frequently asked questions on Lab Management activities in TeamForge.
---

## Can I get more systems for my project?

If your project needs more systems allocated to it, you must contact your Domain Administrator to increase your limit and allocate new systems to your project.

Your Domain Administrator will usually be a known support contact in your organization.

If additional systems are available in other projects, your Domain Administrator will be able to re-allocate those resources to you. If there are no free systems available, and none that can be reassigned, the Domain Administrator will be able to request additional systems from CollabNet, and then assign them to your project.
{{site.data.alerts.hr_shaded}}

## What happens when I move a machine between projects?

When you move a machine from one project to another, the machine is not automatically rebuilt. It still runs the same profile and all the same software it was running in the original project.

There can be reasons for wanting to move a machine between projects without rebuilding it. For example, due to a reorganization, the same users and hosts may be providing the same service, but under a different department or project.

### Moving a machine does not reboot the machine or stop any running processes

If the old project was running processes on the machine that you do not want, you will have to stop them manually.

### Moving a machine changes the access rights on the machine, but does not end existing login sessions

Once the machine has changed projects, after a few minutes, the authentication will have changed so that users from the old project can no longer log in and users from the new project can now log in.

Existing user login sessions, however, are not terminated. Those users will not have root (UNIX) or Administrator (Windows) access any more.

### Moving a machine does not reset the contents of the "localadm" group.
The _localadm_ group is used to maintain a list of users on the system who are local administrators. This group is not emptied when a machine moves projects. It could contain users which you do not want as administrators on the host in the new project.
{{site.data.alerts.hr_shaded}}

## What is an audit log?

Every action performed by the user in the TeamForge Lab Management system is recorded in the Audit Log.

For example, when a host is rebuilt using a profile, these are some of the details captured in the Audit log:

 * The old profile.
 * The new profile.
 * How long it took to complete the rebuild process.
 {{site.data.alerts.hr_shaded}}

## What is the correct procedure for modifying a hosted Lab Manager profile?

All profile modifications must be done through the Lab Management UI, under **Administration > Manage Profiles**. Lab Manager profiles should not be directly modified and changes should not be committed to subversion.

To modify your profile, follow these steps:

 1. In the browser, login to https://mgr.cubit.domain.com/.
 2. Click on **Administration**.
 3. In the left pane, click on **Manage Profiles**.
 4. Click on the profile (your_profile_name).
 5. Click on the _Packages_ tab and choose your options.
{{site.data.alerts.hr_shaded}}

## What is port forwarding?

Use port forwarding to let TeamForge Lab Management hosts connect to machines on other networks.

While TeamForge Lab Management is a secure and isolated environment, occasionally there are valid reasons to let other traffic in and out of TeamForge Lab Management.

Port forwarding consists of routing traffic from one network port on one host to another (same or different) network port on another host.

Take great care when exposing network services running on TeamForge Lab Management hosts to the outside world. Acquaint yourself with your organization's security policies, or develop them if you don't already have them, and make sure all services that are exposed comply with these policies. Even better, work with CollabNet to establish access controls around the access to TeamForge Lab Management, so only authorized hosts from within your enterprise -- and trusted partners -- can access TeamForge Lab Management.

 {% include important.html content="CollabNet strongly recommends that any service that can yield a shell account on a TeamForge Lab Management node such as `SSH` not ever be port forwarded to outside the TeamForge Lab Management environment using this interface. <br><br>

 For CollabNet Hosted customers: CollabNet performs regular scans of its network, and if we see a dangerous or vulnerable network service configured, we may take any steps necessary to protect the overall security of the TeamForge Lab Management customer environment, including disabling the offending network service and the associated port forwarding." %}
{{site.data.alerts.hr_shaded}}

## What is involved in administrating profiles?

If you are a project admin in TeamForge Lab Management with profiles assigned to your project, or if you are a TeamForge Lab Management domain admin, it is important that you have an understanding of how to administer profiles.

 {% include important.html content="It is essential that you first have a solid understanding of how to retrieve and interpret profile details. Making changes to profiles without understanding the effects of what you are doing can cause disruption to your own project, and if the profile you are administering is a public profile, possibly many other projects that use this profile as well." %}

Profile definitions are versioned, which means the history of changes to profiles is preserved. This allows users to build with various versions of a profile, go back to earlier ones if a new one doesn't work for them, and upgrade to a newer version when available. As an administrator, you have the power to set descriptions on profiles and individual versions, block the use of certain versions, and so on.

Within the Profile Library, you can reach the Profile Admin page by selecting a profile in the Profile Library, and clicking on the _Admin_ tab.

Properties can be version-independent or version-dependent.

 * Version-independent properties are common across all profile versions. They do not vary, regardless of the profile's version. These are basically the settings that are configured when the profile is first being added to Lab Management with profiles assigned to your project, or if you are a TeamForge Lab Management. They are displayed at the top of the Profile Admin screen.

 * Version-dependent properties are associated with a particular version of a profile.

   {% include note.html content="These properties, when set, will apply to the version in question, as well as to any subsequent version. Setting the property on a later version will overwrite the property on earlier versions." %}

   These properties are displayed below the version-independent properties on the Profile Admin screen. Most of the properties that you can edit are version-dependent properties.

Only one version's properties are displayed at any given time for editing. To view multiple versions at the same time, use the Profile Details page.

## Version-independent properties

{% include note.html content="Some version-independent properties, set at profile creation time, cannot be changed." %}

There are three version-independent properties that you can change:

**Summary**

This is a brief summary of the profile. You can enter a more detailed description for each version in the properties section.

**Project**

The project that the profile belongs to. If you select "no project" using the "-" option, the profile will belong to the domain. The **Project** selection box is only available to domain admins.

**Is Public?**

This setting governs whether the profile is usable by all profiles, or just to members of this project.

### Version-dependent properties

There are many version-dependent properties that you can change for each profile. Some of these properties include:

* Those that specify hardware requirements needed to build this profile. This will make sure a profile is assigned to a host that can actually successfully be rebuilt with the profile.

* An option to specify whether the profile version can be used or not. Useful for marking a profile version "bad" so it cannot be inadvertently selected by users.

* The logo to associate with the profile version. This logo will be displayed in many locations throughout the system to easily identify profiles. Use the link to the Profile Logo Gallery to add and maintain logos.

  {% include note.html content="When working with these properties, be sure you are operating on the correct version!" %}

**Description**

A description for this version of the profile. Try to put some informative text here, so potential users of this profile will have some guidance as to what this version contains, or how it is different from other versions.

**Tag**

A symbolic name for a profile version. Tags can be used to make versions easier to remember, and can be moved around between profile versions, similar to a "tag" in Subversion. Valid characters for Tags are: letters A-Z, numbers 0-9, and underscores ; although a profile cannot be all numeric, and must contain at least one non-numeric character. The Tag HEAD is reserved, and always refers to the latest version -- buildable or not -- of the profile.
Tags are commonly used by project admins and other project leaders to instruct their users about the proper versions of profiles to use.

**Can new systems be built with this version of the profile? (also known as "Buildable").**

For any number of reasons, you may wish to restrict profiles so that one or more versions of that profile are not buildable. For example, you may wish to force your users to always use the latest version of your profile: this would be easily accomplished by making all the profile versions not buildable except the most recent. You can change the buildability of a version at any time.

**Icon**

You can choose from any of the available icons for your profile, although a profile icon is strictly optional. Icons are not private to your project, and are shared among the whole domain, so do not upload anything too secret (or naughty!).

**Buildable CPU Types**

The types of CPU that can be used to build the profile, for example, "Xeon" or "UltraSparc IV". Setting this property is strictly optional, even if the profile has CPU type restrictions.

**Buildable CPU Archs**

The CPU architectures that can be used to build the profile, for example, "x86_64" or "sun4v". Setting this property is strictly optional, even if the profile has CPU architecture restrictions.

**Buildable Number of CPUs**

The number of CPU's required to run the profile. Setting this property is strictly optional, even if the profile has restrictions around the number of CPU's it can use.

**Buildable Hardware Models**

Specific hardware models which are required to run the profile, for example, "PDP-11". Setting this property is strictly optional, even if the profile has hardware model restrictions.

**Size (in GB)**

The minimum hard disk size, in gigabytes (GB), required to install and run the profile.
{{site.data.alerts.hr_shaded}}

## Who controls which profiles can be used in a project?

As a project administrator, you can control which operating system profiles the users in your project can build hosts with.

TeamForge Lab Management's Profile Library gives ownership of profiles to individual projects, or to the entire domain. Profiles can either be public (available to all projects on the site) or private (available only to the project which owns the profile).

However, that fact that a profile is public, or belongs to the project, does not necessarily mean that it can be used to rebuild hosts. The profile must be specifically allowed for use in the project by a project administrator before it can be used to rebuild hosts.

Sometimes it is desirable not to restrict an entire profile, but only one or more versions of that profile. Individual versions of a profile can be prohibited by the project administrator of the project which owns the profile using the Profile Admin screen.

If the profile does not belong to your project, you cannot restrict the use of that profile at the individual version level: that decision is made at the discretion of the owners of the profile.

If you are the project administrator of the project which owns a profile, you can change the profile's public/private status at any time using the Profile Admin screen.

When you prohibit a profile from your project, this has no effect on hosts which are already built inside your project. They will continue to function normally running the profile they were already running. The owner of the system, however, will be unable to rebuild the system with its current profile, or any other profile which is not allowed in the project.

As a project administrator, you may wish to force your users to rebuild their systems once you have prohibited the use of a profile. On the Profile Summary page you can find a listing of all systems that are running each profile. This helps you track down systems running a profile that you have prohibited, and with your project administrator privileges, you can rebuild those systems with a profile of your choice.
{{site.data.alerts.hr_shaded}}

## How are my project systems being utilized?

Regardless of the number of hosts in a project, in practice it is common to find shortages of free hosts. At the same time, there are almost always hosts which are under-utilized or even completely idle, which could be re-allocated or consolidated.

Finding and reallocating these hosts allows more efficient use of your project infrastructure.

### Project-Level Analytics

The _Analytics_ tab in your project shows the following metrics. These metrics are the base available across all operating systems that TeamForge Lab Management supports.

 * Load Average
 * Processes
 * CPU
 * Logged-in Users

 {% include note.html content="More metrics, including host-specific and operating-system-specific metrics, are available for individual hosts when you click on the host name in the results table." %}

To see a metric, click the name of the metric. You can see these time ranges:

**Daily**

Approximately the past 24 hours

**Weekly**

Approximately the past 7 days

**Monthly**

Approximately the last 30 days

**Yearly**

Approximately the last 365 days

If a given host says "no value" in any of its columns, this means that TeamForge Lab Management has been unable to collect this data over the requested time interval. If the machine is up, and not collecting data, contact a TeamForge Lab Management administrator to investigate why data collection is not working properly. If the machine is currently down, or was down during the requested time range, you will not be able to get any performance data for those times. There is no way to retroactively "catch up" data if collection is not working properly.

The data used to build each graph and chart presented to you can be exported in CSV (Comma-Separated Value) format, suitable for opening in any spreadsheet application. This allows you to build your own visualizations of the data to complement the ones TeamForge Lab Management creates.

### Beating The System: Dealing With the Possibility of Users Generating "Fake" Load To Make Machines Seem Busier

Since we publish the metrics for determining how busy TeamForge Lab Management thinks machines are, it is possible for irresponsible users to generate automated jobs which simulate a busy machine, even if the machine is really not being used for anything.

We encourage all users and administrators of the project to make sure people in your projects understand that this type of behavior is not acceptable and may lead to loss of privileges or other actions against them. Presumably, if someone has a good reason for wanting to keep a machine, it is good for their project, and your organization if they do so.

As administrators, we strongly recommend you take the time to understand and listen to your users' concerns about how machines are allocated. You may just need more machines in your project, or you may be overzealous about de-allocating machines once they drop below a certain usage threshold. De-allocating machines that seem to be not busy may seem efficient, but if those machines took their users a long time to set up, that might be counterproductive. Perhaps you can reach a middle ground and use virtual machines, or a smaller virtual or physical machine, for that user.

Finally, we always recommend talking to your users and trying to understand how they are really using their machines. The statistics that TeamForge Lab Management gathers are a starting point for managing your software development and testing infrastructure, but not the final word.
{{site.data.alerts.hr_shaded}}

## What is host URL mapping?

Host URL Mapping in TeamForge Lab Management allows you to access web services running inside the TeamForge Lab Management environment from anywhere, using a simple and consistent URL, with optional SSL encryption services added on.

Host URL Mapping provides three major benefits:

 * Maintains a consistent URL even if the service is moved to a different TeamForge Lab Management node or different base URL.
 * Provides external access to resources that would otherwise be only accessible inside the TeamForge Lab Management environment. Because Host URL Mapping uses standard HTTP/HTTPS ports, you will not be blocked by firewalls that sometimes prevent port forwarding from working properly.
 * Allows you to transparently add SSL encryption to web services running inside your TeamForge Lab Management environment.

If your application mixes absolute and relative URL's, host URL mapping dynamically rewrites the absolute portions of your URLs to help ensure that your applications display properly when they are mapped. While not perfect, this feature has been tested with a number of web applications and found to be effective.

 {% include caution.html content="Take the utmost care when exposing web services running on TeamForge Lab Management hosts to the outside world. Acquaint yourself with your organization's security policies, or develop them if you don't already have one, and make sure that all services that are exposed comply with these policies. Even better, work with CollabNet to establish access controls around the access to TeamForge Lab Management, so only authorized hosts from within your enterprise and trusted partners can access TeamForge Lab Management." %}

CollabNet strongly recommends that any web service that you expose be password-protected, or otherwise require authentication to access.

CollabNet Hosted customers: CollabNet performs regular scans of its network, and if we see a dangerous or vulnerable web service configured, we may take any steps necessary to protect the overall security of the TeamForge Lab Management customer environment, including disabling the offending service and the associated URL mapping.

 {% include note.html content="While you can convert non-SSL URL's into SSL using Host URL Mapping, you cannot map SSL URL's. You can use Port Forwarding to expose SSL URL's outside of the TeamForge Lab Management environment, however." %}
{{site.data.alerts.hr_shaded}}

## Why doesn't URL mapping work for me?

My page doesn't look right. Images and graphics are wrong, or functionality doesn't work. The same page looks and works fine when viewed through Port Forwarding.

Host URL Mapper attempts to "clean up" HTML pages which pass through it in order to clean up absolute links. But it is not hard to construct an application that will slip through TeamForge Lab Management's filters and still not properly render all of its referenced objects inside of its pages. We make all reasonable attempts to clean up HTML, but not all applications can be properly rendered using Host URL Mapping. This is especially true for applications which make heavy use of Javascript, ActiveX, Java applets, and other types of rich client-side web programming.

To test this, use either a direct connection to the host (if available) or a port forwarded connection to the host to see if this behavior is present on the original version of the page. If the original page does not have this behavior, the first step is to verify the **Dynamic Rewriting** level is set to _More Aggressive_. If that does not work, please file a support request with CollabNet to evaluate the page.
{{site.data.alerts.hr_shaded}}

## How does host URL mapping compare with port forwarding?

URL mapping is good if you don't want your connection blocked, while port forwarding is good if you need non-HTTP services.

 * Port forwarding is a facility for making any TCP or UDP network service available outside the TeamForge Lab Management environment. Host URL mapping only allows you to expose HTTP-based services.

 * A major limitation of port forwarding is that many organizations' firewall security policies prohibit outgoing connections to arbitrary high ports. Because URL mappings all use standard HTTP/HTTPS ports 80 and 443, they will never be blocked. If you can access TeamForge Lab Management itelf, you will be able to access any application configured with host URL mapping.

 * Host URL mapping can automatically add SSL encryption to your web services that are not running SSL encryption. With port forwarding, if you want SSL encryption, you must set it up on each host.

 * Using host URL mapping, you can expose only a part of a server's URL space. With port forwarding, the entire URL space is visible.

 * Port forwarding does not need to rewrite links inside the HTML, so more web applications will work under port forwarding.
{{site.data.alerts.hr_shaded}}

## How are virtual guests different from physical machines?

Virtual guests work like physical hosts, with some important differences.

### Creating a new virtual guest

The process of creating a new virtual guest is very similar to the process of creating a new physical host, with the following differences:

 * You must select a virtual host -- a physical machine -- to run the virtual guest on. You cannot run a virtual guest inside of another virtual guest.

 * The virtual guest's project cannot be set independently of the virtual host, and the virtual guest will always be in the same project as its virtual host.

 * You are constrained, with hard limits, by the RAM and hard disk available on the virtual host. TeamForge Lab Management requires that each host have a minimum of 512MB of free RAM and 10GB of disk free.

 * Even if you are within the hard limits for RAM and hard disk space usage, you are still sharing other resources -- notably disk I/O bandwidth, network bandwidth, and CPU cycles -- with the host machine and any other guests already on the virtual host. Before creating a new virtual guest on a virtual host, we recommend carefully examining the virtual host's system performance to make sure it can handle the additional load. Of course, if you do find out later on that performance of your virtual guest is not as good as you would like, you can always migrate the virtual guest to another virtual host.

 * You are not as constrained on your selection of MAC address with virtual guests ; you can choose any available address in the allowed range. Valid values for MAC addresses for virtual guests in TeamForge Lab Management are 00:50:56:01:00:01 to 00:50:56:3F:FF:FF. Using anything outside of this range will either result in the host not being reachable on the network, or the host coming in conflict with another MAC address on the network.

 * You cannot specify the architecture or chip type for the virtual guest, since those properties are inherited from the parent.

 * You do not need to specify a Lights Out Management IP address for the virtual guest, since the IP address used to manage the guest is always the IP address of the virtual host.

### Disk size

While disk space is allocated to virtual guests at the time of virtual guest creation, it is not actually occupied on the host until it is needed by the guest. At the same time, TeamForge Lab Management does not keep an up-to-date count of exactly how much disk space is in use on the virtual host.

In practice, this means:

 * You will likely have more disk space on your host than your virtual guests would indicate. But it is also possible to have less space than your virtual guests would indicate. For example, let's say you have a 100GB disk on your host, with two virtual guests, each with a 40GB disk allocated. But if you're only using 5GB of that 40GB in each guest, the remaining 70GB in unallocated. But on the flip side, let's say you allocated those two virtual guests at 10GB each, but they were using a total of 90GB on your local disk to store files. TeamForge Lab Management would let you make this allocation, but your virtual machines would crash when you tried to put more than a combined 10GB on them both.

 * This translates into freedom in your management of disk space on the virtual hosts: you are free to temporarily "borrow" disk space from virtual guests that is not being currently used and use it for your virtual host.

 * Along with this freedom comes the responsibility of being vigilant about maintaining sufficient space on your virtual hosts to always have enough disk space for any guests on the system. Monitor your usage carefully using Analytics page for the host.

### Modifying hardware parameters of existing virtual guests

Some virtual guest hardware parameters can be modified after the virtual guest has been created.

**Changing disk size**

While changing the size of the disk is supported in TeamForge Lab Management, the change will not be reflected until you re-image your guest. And, in certain cases, it is possible for a change in the disk size of your guest to cause the guest to become unreachable, especially if you reduce the disk size. Therefore, we recommend that you change disk size on virtual guest only if you are going to immediately rebuild the guest.

**Changing RAM size**

Changing RAM size is a very low-risk operation. In order for the change to take effect, the virtual guest must be rebooted after the change is made in TeamForge Lab Management. Reducing the RAM available to your virtual guest can make the system run much slower.

 {% include note.html content="In between changing RAM size of the virtual guest and rebooting the virtual guest, you must wait approximately 5 minutes to insure your change is propagated." %}

**Changing the number of CPUs**

Virtual guests can support either one or two processors. Two CPUs for virtual guests are supported only if the virtual host has at least two CPUs. Like changing a virtual guest's RAM allocation, changing the number of CPUs in a virtual guest is a low-risk operation, and the virtual guest must be rebooted after the change has been made in TeamForge Lab Management.

 {% include note.html content="In between changing number of CPU's for the virtual guest and rebooting the virtual guest, you must wait approximately 5 minutes to insure your change is propagated." %}
{{site.data.alerts.hr_shaded}}

## What is involved in migrating a virtual guest?

When you migrate a virtual guest to a different host, there are a few things to keep in mind.

 * The user performing the migration must be a TeamForge Lab Management Domain Admin.

 * The current virtual host and guest, and the desired new virtual host, must all be in the same project. In other words, you cannot change both the project allocation and the parentage of a host in a single step.

 * The target virtual host must have enough RAM, disk, and CPU to accommodate the virtual guest you wish to migrate to it. The rules governing the RAM, disk and CPU needed are the same as if you were creating a new virtual guest on the host.

   TeamForge Lab Management calculates these values for you and presents you with a drop-down list of hosts that fulfill all these criteria. But if you are wondering why a host is not a valid potential new virtual host, see the host's current hardware parameters and allocations on the Host/Admin page for the virtual host.
 
 * If your TeamForge Lab Management installation is composed of more than one subnet, both the virtual guest being moved and the target virtual host must be on the same subnet. If you are not sure if your installation has more than one subnet, check with your local TeamForge Lab Management support contact.

 * Only one virtual guest at a time can be migrated to a given virtual host, although there is no limit on the number of virtual guests that can be moved from a given virtual host. The reason for this restriction is that moving a virtual guest to a host is a very I/O-intensive operation that will consume all available disk I/O on the destination host. Allowing more than one simultaneous move will not be any faster, and increases the risk of over system instability for the virtual host.

 * If more than one virtual guest migration to a given virtual host is started at the same time, they will complete serially. The exact order of the migrations may not correspond exactly to the order in which they were initiated and cannot be accurately predicted.

 * Occasionally, after the migration has completed successfully, the virtual guest will require an extra reboot to start up properly.
{{site.data.alerts.hr_shaded}}

## What's a good way to read log information?

To read log entries, download the log as a CSV file.

You can also filter the logs using the **Filter** option at the top of all audit log screens.

On any log page, you can click **Download all log entries in csv format** to download the corresponding CSV file.

{% include note.html content="The CSV file is formatted in Microsoft Excel format. If you import it into OpenOffice, set **Text Delimiter** to double quotes(\")." %}

{% include links.html %}