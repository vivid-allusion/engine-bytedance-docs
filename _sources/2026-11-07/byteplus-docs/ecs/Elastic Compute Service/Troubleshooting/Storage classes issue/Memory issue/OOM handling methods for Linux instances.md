---
title: "OOM handling methods for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/OOM_handling_methods_for_Linux_instances"
---

This topic describes how to troubleshoot OOM issues in a Linux instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first to improve fault tolerance and ensure data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Use the following information to troubleshoot instance OOM.

   
   |Information point |Method to obtain information |Description |
   |---|---|---|
   |OOM occurrence time and frequency |Linux system log |Log path is as follows:<br><br>```Plain Text```<br>```/var/log/messages```<br> |
   ||Business application log |Based on the OOM occurrence time, check the OOM cause in the application log of the target business. |
   |System load of Linux instance |[Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor) |It is recommended to use Cloud Monitor to view your instance load information. For details, refer to [Viewing Cloud Service Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor). |
   |Business load |Business application log |Based on the OOM occurrence time, check the OOM cause in the application log of the target business. |
   |Application log when OOM occurs |||
   

3. Select an appropriate handling method based on the actual OOM cause:

   * **Insufficient memory of the current Linux instance to support business operations**: You can upgrade the instance memory. For details, see [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Overview-2).

   * **Business application defects**: You can optimize the business code based on issues in the application logs of your business.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Here, the business refers to the third\-party business in a Linux instance. We recommend contacting the corresponding business provider to fix the issue.      </div>
