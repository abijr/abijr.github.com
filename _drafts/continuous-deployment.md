---
layout: post
title:  "A Continuous Deployment Workflow"
date:   2015-05-03 17:31
categories: devOps
---

This is a workflow draft for the development and deployment of the myriad of services and applications used at Foxconn - Santa Teresa (my current workplace).

The Problem(s)
--------------
1. Most applications and web services are hand installed or developed directly in production servers. There is no easy way to deploy to production servers.

2. When applications/services crash, they crash... hard. No graceful failures, reason being that, there is only one instance of each application.

3. There is no testing environment. You publish your application/service, and cross your fingers hoping for the best.

Solution at a glance
--------------------
1. Use a configuration management (CM) tool to solve problem #1. With the CM tool configuration files, install and launch apps/services along with their dependencies. Simplifying and documenting the deployment process.

2. Use a service discovery system to allow more than one instance to be available at a time, allowing graceful failures and possibly load balancing and solving problem #2.

3. Finally, for problem #3, use a combination of solutions #1 and #2 to recreate the production environment (at a smaller scale) to allow the testing of applications and services.

The Workflow
------------
Here we find the steps to get an application running locally, deployed in a production setting.

**Environment Recreation:**
The developer will have to be in charge of allowing the recreation of the application development environment through the usage of the chosen CM tool's configuration files.

**Deployment:**
Once the developer thinks the application is ready for deployment to production, the developer himself or a system administrator will install the application to a new server node (if there are older instances of the same application the may keep running).

**Publication:**
After running tests (automated or not), the developer can choose to publish the node to the service discovery system. The now published application would now be accesible to users and other services.

Pros and Cons
-------------
**Pros**

* A more resilient infrastructure (most service discovery systems do load balancing and have failure detection).
* Easier and faster deployment process (run `$ my-cm-tool install`).
* Experimentation is encouraged, as new thigs can be tried without breaking stuff.
* Development in teams is easier, through the easily replicatable development environment.
* Services can be found without asking Caldiño[^1] for the IP.
* Background for cloud infraestructure usage is layed out.

**Cons**

* Learning curve for the tools (as small as it may be, it's still there).
* Maintenance of the service discovery and CM tool.
* Change in the way services and applications are currently accessed.

Tentative software
------------------
* [Consul](https://www.consul.io/): Distributed, highly available, DNS based, service discovery tool.
* [SkyDNS](https://github.com/skynetservices/skydns): Same as consul.
* [Salt](http://saltstack.com/community/): A new approach to infrastructure management by developing software that is easy enough to get running in seconds, scalable enough to manage tens of thousands of servers, and fast enough to control and communicate with them in milliseconds.
* [Ansible](http://www.ansible.com/home): Ansible is a powerful automation engine that makes systems and applications simple to deploy.

Conclusion
----------
This is actually simpler than I thought at first.

[^1]: Our Sysadmin
