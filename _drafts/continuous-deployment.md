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

2. When applications/services crash, they crash... hard. No graceful failures, reason being that there is only one instance of each application.

3. There is no testing environment. You publish your application/service, and cross your fingers hoping for the best.

Solution at a glance
--------------------
1. Use a configuration management (CM) tool to solve problem #1. With the CM tool configuration files, install and launch apps/services along with their dependencies. Simplifying and documenting the deployment process.

2. Use a service discovery system to allow more than one instance to be available at a time, allowing graceful failures and possibly load balancing and solving problem #2.

3. Finally, for problem #3, use a combination of solutions #1 and #2 to recreate the production environment (at a smaller scale) to allow the testing of applications and services.

The Workflow
------------
The developer will have to be in charge of allowing the recreation of the application development environment through the usage of the chosen CM tool's configuration files.

Once the developer thinks the application is ready for deployment to production, the developer himself or a system administrator will deploy the application to a new server node (if there are older instances of the same application the may keep running). After running tests (automated or not), the developer can choose to publish the node to the service discovery system. The now published application would now be accesible to users and other services.
