---
title: "Host application scaling"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Host_application_scaling"
---

Hosted applications support scaling hosts up or down as needed, enabling effective management of service status and resource utilization. This article explains how to increase or decrease the number of hosts for deploying an application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature is only supported for applications with a deployment type of <strong>host</strong>; applications with a deployment type of <strong>container</strong> do not support this feature at this time.</div>


* <div data-tips="true" data-tips-type="warning">Only host instances with status <strong>Normal</strong> can be added.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A managed application with **application deployment type** set to **host** has been created. For details about actions, see [Create and deploy managed applications (ECS)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, click the **environment** of the application hosted on the target host type.

3. Click **Scale**.

4. Select the target host instance and perform expansion or reduction actions.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After scaling is triggered, you can view the change log in **Change Records \> Details**.

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

<span id=".57yp5a655aSx6LSl"></span>
### Capacity reduction failed

Scale\-in failures may occur in some scenarios. In this case, please first disassociate the instances and applications that failed to scale in, and then manually remove the abnormal hosts.


1. View the hosts that failed to scale in from the change log.

2. In the instance list, **disassociate** the corresponding instance.

3. After successfully disassociating, manually remove the host as prompted.
