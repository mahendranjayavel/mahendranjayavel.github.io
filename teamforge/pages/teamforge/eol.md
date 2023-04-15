---
title: Digital.ai's Product End-of-Life Policy
keywords: 
sidebar: teamforge_sidebar
permalink: eol.html
toc: no
last_updated: Mar 24, 2021
summary: This is Digital.ai's end-of-life policy to help customers better manage their end-of-life transition and to understand the role that Digital.ai can play in helping to migrate to alternative Digital.ai products, platforms and technologies.
---
Products reach the end of their life cycle for a number of reasons. These reasons may be due to market demands, technology innovation and development driving changes in the product, or the products simply mature over time and are replaced by functionally richer technology. While this is an established part of the overall product life cycle, Digital.ai recognizes that end-of-life milestones often prompt companies to review the way in which such end-of-support and end-of-life milestones impact the Digital.ai products or its supported platforms. With that in mind, we have set out below Digital.ai's end-of-life policy to help customers better manage their end-of-life transition and to understand the role that Digital.ai can play in helping to migrate to alternative Digital.ai products, platforms and technologies. The general policy guidelines are:

* As a general rule, Digital.ai will provide six months' notice and we would send out regular notifications to all our customers through our Digital.ai blog, product notifications and/or support newsletter.
* We would End-Of-Life support for our products, platforms and software with our new version of our product release.
* We would continue to provide support to our products, platforms and software for our earlier supported product version.
* You will need to ensure that you have a current and fully paid support contract with Digital.ai to receive notifications on end of life. Please contact your Account Manager regarding fees payable during the end-of-life period so that we can support you right through the end-of-life transition period.
* See the list of [Currently Supported Products](https://www.collab.net/support/supported-products) for more information.


<table class="table table-fixed">
<thead>
<tr>
<th class="col-sm-2">Products, Platforms and Software</th>
<th class="col-sm-2">Description</th>
<th class="col-sm-4">When?</th>
<th class="col-sm-4">Replacement Options</th>
</tr>
</thead>
<tbody>
<!-- Artifact artf418465 : Old Documents - EOL -->
<tr>
<td class="col-sm-2">Legacy Documents JSP Pages</td>
<td class="col-sm-2">No support for JSP based Documents pages</td>
<td class="col-sm-4">JSP based Documents Management pages are available in TeamForge 21.2 and earlier<br><br>JSP based Documents Management pages are not available in TeamForge 22.0 and later</td>
<td class="col-sm-4">Use the new Angular JS based Documents Management UIs.</td>
</tr>	
<!-- [artf417364] IE 11 EOL -->
<tr>
<td class="col-sm-2">Internet Explorer 11</td>
<td class="col-sm-2">No support for Internet Explorer 11</td>
<td class="col-sm-4">IE 11 supported by TeamForge 21.0 and earlier<br><br>IE 11 not supported by TeamForge 21.1 and later</td>
<td class="col-sm-4">As TeamForge supports the Edge browser, customers can move away from IE 11 in favor of the Edge browser.</td>
</tr>	
<tr>
<td class="col-sm-2">Site Activity Report</td>
<td class="col-sm-2">Deprecate Flash-based Site Activity Report</td>
<td class="col-sm-4">Flash-based <a href="http://docs.collab.net/teamforge201/monitorsite.html#siteactivityreport">Site Activity Report</a> is available in TeamForge 20.1 and earlier<br><br>Flash-based Site Activity Report is not available in TeamForge 20.2 and later</td>
<td class="col-sm-4">As <a href="https://theblog.adobe.com/adobe-flash-update/">Adobe Flash reaches its end of life by the end of 2020</a>, Flash-based TeamForge Site Activity Report is also being deprecated.</td>
</tr>  	
<tr>
<td class="col-sm-2"><code>UserFilter</code></td>
<td class="col-sm-2">Deprecate <code>UserFilter</code> (one of the Gerrit's SubmitRule filters)</td>
<td class="col-sm-4"><code>UserFilter</code> is supported in TeamForge 19.3 and earlier<br><br><code>UserFilter</code> is not supported from TeamForge 20.0 and later</td>
<td class="col-sm-4"><code>UserFilter</code> has been deprecated in TeamForge 20.0—Git integration. It is set to be removed completely in TeamForge 20.1.<br><br>{% include userfiltereol.html %} </td>
</tr>  	
<tr>
<td class="col-sm-2">CVS</td>
<td class="col-sm-2">No support for CVS</td>
<td class="col-sm-4">CVS supported in TeamForge 20.1 and earlier<br><br>CVS not supported from TeamForge 20.2 and later</td>
<td class="col-sm-4">Use other SCM tools like Git.</td>
</tr>  
<tr>
<td class="col-sm-2">EventQ</td>
<td class="col-sm-2">No support for EventQ</td>
<td class="col-sm-4">EventQ supported in TeamForge 19.3 and earlier<br><br>EventQ not supported from TeamForge 20.0 and later</td>
<td class="col-sm-4">Use the Webhooks-based Event Broker in place of EventQ.<br><br>{% include eventqeol.html %}</td>
</tr>
<tr>
<td class="col-sm-2">Nexus 2</td>
<td class="col-sm-2">No support for Nexus 2</td>
<td class="col-sm-4">Nexus 2 supported in TeamForge 19.1 and earlier<br><br>Nexus 2 not supported from TeamForge 19.2 and later</td>
<td class="col-sm-4">Upgrade to Nexus 3.</td>
</tr>
<tr>
<td class="col-sm-2">Chinese Korean and Japanese (CJK) locales</td>
<td class="col-sm-2">No support for CJK locales with TeamForge 17.1 and later</td>
<td class="col-sm-4">CJK supported in TeamForge 16.10 and earlier<br><br>CJK not supported from TeamForge 17.1 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">Crucible Plug-in</td>
<td class="col-sm-2">No support for Crucible plug-in</td>
<td class="col-sm-4">Supported in TeamForge 18.1 and earlier<br><br>Not supported from TeamForge 18.2 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">Artifactory versions later than v4.7</td>
<td class="col-sm-2">No support for Artifactory versions later than v4.7</td>
<td class="col-sm-4">Supported in TeamForge 18.1 and earlier<br><br>Not supported from TeamForge 18.2 and later</td>
<td class="col-sm-4">NA</td>
</tr>  
<tr>
<td class="col-sm-2">TeamCity</td>
<td class="col-sm-2">No support for TeamCity</td>
<td class="col-sm-4">Supported in TeamForge 18.1 and earlier<br><br>Not supported from TeamForge 18.2 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">Activity Stream</td>
<td class="col-sm-2">No support for EventQ Activity Stream</td>
<td class="col-sm-4">Supported in TeamForge 18.2 and earlier<br><br>Not supported from TeamForge 18.3 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">DLM 1.x</td>
<td class="col-sm-2">No support for DLM 1.x</td>
<td class="col-sm-4">Supported in TeamForge 17.4 and 17.8<br><br>Not supported from TeamForge 18.1 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">Old site-options.conf syntax</td>
<td class="col-sm-2">No support for older syntax for defining your HOST token (HOST_xxx)</td>
<td class="col-sm-4">Supported in TeamForge 17.11 and earlier<br><br>Not supported from TeamForge 18.1 and later</td>
<td class="col-sm-4">To ensure backward compatibility, TeamForge supported both old and new syntaxes for defining your HOST token. However, this backward compatibility will be available only with TeamForge 17.11 and earlier versions. It is recommended to adjust your site-options.conf in line with the new syntax (xxx:SERVICES) as support for older syntax would be dropped in TeamForge 18.1 release.</td>
</tr>
<tr>
<td class="col-sm-2">Unmanaged CVS servers</td>
<td class="col-sm-2">No support for unmanaged CVS integration servers</td>
<td class="col-sm-4">Supported in TeamForge 17.11 and earlier<br><br>Not supported from TeamForge 18.1 and later</td>
<td class="col-sm-4">During an upgrade, unmanaged CVS integration servers are "disabled" (converted to use the "generic adapter"). This is similar to how Perforce integration servers were disabled.</td>
</tr>
<tr>
<td class="col-sm-2">Running two PostgreSQL clusters on the same server</td>
<td class="col-sm-2">The ability to run two PostgreSQL clusters on the same server is deprecated</td>
<td class="col-sm-4">Supported in TeamForge 17.8 and earlier<br><br>Not supported from TeamForge 17.11 and later</td>
<td class="col-sm-4">Use same cluster for database and datamart or move datamart to a separate server (virtual machine).</td>
</tr>
<tr>
<td class="col-sm-2">RHEL/CentOS 6.x</td>
<td class="col-sm-2">No support for Red Hat Enterprise Linux/CentOS 6.x platform</td>
<td class="col-sm-4">Supported in TeamForge 20.3 and earlier<br><br>Not supported from TeamForge 21.0 and later.</td>
<td class="col-sm-4">Update to RHEL/CentOS 7.x or later.</td>
</tr>
<tr>
<td class="col-sm-2">Microsoft Project Integration</td>
<td class="col-sm-2">No support for MS Project integration</td>
<td class="col-sm-4">Supported in TeamForge 5.2–6.1<br><br>Not supported from TeamForge 6.2 and later</td>
<td class="col-sm-4">NA. Tasks component becomes obsolete from TeamForge 17.11.</td>
</tr>
<tr>
<td class="col-sm-2">Black Duck Code Sight</td>
<td class="col-sm-2">No support for Black Duck Code Sight</td>
<td class="col-sm-4">Supported in TeamForge 16.10 and earlier<br><br>Not supported from TeamForge 17.1 and later</td>
<td class="col-sm-4">Use TeamForge's native Code Search function powered by Elastic Search. Available in TeamForge 17.1 and later.</td>
</tr>
<tr>
<td class="col-sm-2">SSH tunneling</td>
<td class="col-sm-2">No support for SSH tunneling</td>
<td class="col-sm-4">Supported in TeamForge 16.7 and earlier<br><br>Not supported from TeamForge 16.10 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">VMware Player image</td>
<td class="col-sm-2">VMware Player appliance image is no longer available for TeamForge 16.7 and later</td>
<td class="col-sm-4">Available in TeamForge 16.3 and earlier<br><br>Not available from TeamForge 16.7 and later</td>
<td class="col-sm-4">TBD</td>
</tr>
<tr>
<td class="col-sm-2">Tasks component</td>
<td class="col-sm-2">No support for "Tasks" component</td>
<td class="col-sm-4">Supported in TeamForge 17.11 and earlier<br><br>Not supported from TeamForge 18.1 and later</td>
<td class="col-sm-4">Tasks component becomes obsolete from TeamForge 17.11 release. You may create a Tasks tracker, if required.</td>
</tr>
<tr>
<td class="col-sm-2">Berkeley DB backend for Subversion</td>
<td class="col-sm-2">No support for Berkeley DB</td>
<td class="col-sm-4">Supported in TeamForge 16.3 and earlier<br><br>Not supported from TeamForge 16.7 and later</td>
<td class="col-sm-4">All new Subversion repositories, by default, use the FSFS backend. Existing repositories must be converted.</td>
</tr>
<tr>
<td class="col-sm-2">TeamForge SOAP5.x</td>
<td class="col-sm-2">No support for SOAP5.x API support</td>
<td class="col-sm-2">Supported in TeamForge 16.7 and earlier<br><br>Not supported from TeamForge 16.10 and later</td>
<td class="col-sm-2">Use the latest TeamForge SOAP/REST APIs.</td>
</tr>
<tr>
<td class="col-sm-2">Project Tracker</td>
<td class="col-sm-2">No support for the Project Tracker component</td>
<td class="col-sm-4">Supported in TeamForge 16.7 and earlier<br><br>Not supported from TeamForge 16.10 and later</td>
<td class="col-sm-4">NA. Project Tracker becomes obsolete from TeamForge 16.10 release.</td>
</tr>
<tr>
<td class="col-sm-2">Advanced mode installation</td>
<td class="col-sm-2">No support for advanced mode installation</td>
<td class="col-sm-4">Supported in TeamForge 8.1 and earlier<br><br>Not supported from TeamForge 8.2 and later</td>
<td class="col-sm-4">NA. TeamForge 16.7 and later support dedicated installation only.</td>
</tr>
<tr>
<td class="col-sm-2">Perforce</td>
<td class="col-sm-2">No support for Perforce integration</td>
<td class="col-sm-4">Supported in TeamForge 8.1 and earlier<br><br>Not supported from TeamForge 8.2 and later</td>
<td class="col-sm-4">NA</td>
</tr>
<tr>
<td class="col-sm-2">TeamForge on SUSE</td>
<td class="col-sm-2">No support for SUSE</td>
<td class="col-sm-4">Supported in TeamForge 8.1 and earlier<br><br>Not supported from TeamForge 8.2 and later</td>
<td class="col-sm-4">Migrate to RHEL/CentOS platforms.</td>
</tr>
<tr>
<td class="col-sm-2">TeamForge SOAP4.x</td>
<td class="col-sm-2">No support for SOAP4.x API</td>
<td class="col-sm-4">Supported in TeamForge 7.2 and earlier<br><br>Not supported from TeamForge 8.0 and later</td>
<td class="col-sm-4">Customers can use the latest TeamForge SOAP/REST APIs.</td>
</tr>
<tr>
<td class="col-sm-2">TeamForge 32-bit</td>
<td class="col-sm-2">No support for 32-bit platform</td>
<td class="col-sm-4">Supported in TeamForge 7.2 and earlier<br><br>Not supported from TeamForge 8.0 and later</td>
<td class="col-sm-4">Move to 64-bit platform.</td>
</tr>
</tbody>
</table>



{% include links.html %}