---
title: "Create an event function"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_event_functions"
---

To develop a program according to the interface defined by veFaaS, select an event function. This article introduces how to create an event function.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The veFaaS is activated.

* Cross\-service authorization needs to be complete if you use veFaaS for the first time.

* Local [code development](https://docs.byteplus.com/en/docs/faas/Code_development) has been completed.

* (Optional) To upload code via TOS, store the code Zip package in TOS in advance. For specific operations, see [getting started with TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* (Optional) To upload code locally or via TOS, ensure the code Zip package is a non\-encrypted file and does not exceed 256 MiB.

* (Optional) The BytePlus Virtual Private Cloud (VPC) service has been activated, and a VPC, subnets, and security groups have been created in the region where the function is to be deployed. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Optional) To view function logs, ensure BytePlus Torch Log Service has been activated. If you need to use a custom logging project to handle function logs, ensure that the project and topics have already been created. For details, see Creating log projects and Creating log topics.

* (Optional) To manage function resources by project, create a project in advance. For specific operations, see [create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Function \> Function management**, and on the **Function** page, click **create function**.

4. On the method selection page, click **event function** \> **create event function**, and configure parameters as described below.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Specify a custom name for the function. Function names cannot be repeated within the same account. After a function name is created, it cannot be modified. |
      |Description |Enter a description for the function. You can leave this field empty. |
      

   * **Function code**

      
      |**Parameter** |**Description** |
      |---|---|
      |Runtime |Select a runtime environment for the function code. Currently supports **Python**, **Golang**, and **Node.js**. |
      |Deployment method |The following deployment methods are supported. Select as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The code Zip package must be an unencrypted file and must not exceed 256 MiB in size.</div><br><br><br><br>* **Function template**: Built\-in, out\-of\-the\-box code template in veFaaS. Click **Code preview** to view the resource files and code details included in the current template. Select the appropriate code template as needed.<br><br>* **Upload local Zip package**: Upload a locally developed code Zip package.<br><br>* **TOS upload**: In the TOS upload panel, select the target Bucket and Zip file. |
      

   * **Advanced settings**

      For details, see [function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

5. Click **Create** to create the function.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Release the function's code and configuration online. For specific operations, see [release function](https://docs.byteplus.com/en/docs/faas/Release_function).
