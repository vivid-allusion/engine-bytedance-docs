---
title: "Create microservices applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Create_microservices_applications"
---

Microservices applications can host container applications built with any language or framework. They provide two deployment methods: code package and container image deployment, support automatic scaling, offer Pay\-as\-you\-go billing, and are primarily used for microservices applications, MQ consumer services, and other fields. This article introduces how to create microservices applications.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The veFaaS is activated.

* Cross\-service authorization needs to be complete if you use veFaaS for the first time.

* Code has been locally developed. For details, refer to [Native runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime).

* Ensure that BytePlus Virtual Private Cloud has been activated, and that a Virtual Private Cloud, subnet, and security group have been created in the region where the function will be deployed. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Optional) To upload code via TOS, store the code zip package in TOS in advance. For details, see [TOS getting started](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* (Optional) To upload code via local or TOS, ensure that the code zip package is a non\-encrypted file and does not exceed 256 MiB.

* (Optional) The BytePlus Torch Log Service (TLS) has been activated. If you need to use a custom logging project to handle function logs, ensure that the project and topics have already been created. For details, see Creating log projects and Creating log topics.

* (Optional) To manage function resources via projects, create a project in advance. For details,  see [create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Microservices applications do not support the function online testing feature and do not support configuration of triggers.

* When using container image deployment:

   * Container images must be pushed to the BytePlus Container Registry in the same region as the function.

   * After the function is created, wait for image synchronization to complete before releasing the function.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Function \> Function management**, and on the **Function** page, click **Create function**.

4. On the Method page, click **Microservices Application Function** \> **Create Microservices Application Function**, and configure the parameters as described below.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Set the name of the microservices application. The name must be unique within the same account and cannot be modified after it is successfully created. |
      |Description |Description, can be left blank. |
      

   * **Function code**

      
      |**Parameter** |**Description** |
      |---|---|
      |Runtime |Select a runtime environment for the function code. Only **Native Runtime** is supported in this scenario. |
      |Deployment method |The following deployment methods are supported. Select as needed.<br><br><br>* **Image**: Deploy using a container image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Public images are contributed by community developers. veFaaS does not maintain them. For software usage issues, please provide feedback to the community.</div><br><br><br><br>   * **Container Registry**: Select the specific image to deploy from your BytePlus Container Registry. You can filter out a specific image by instance, namespace, and repository type (public or private).<br><br>      When you select an image from **Container Registry**, veFaaS automatically obtains the configurations of the image, including the **startup command** and **environment variables**. You can specify whether to apply the configurations of the selected image to the function****.<br><br>   * **Public image**: An out\-of\-the\-box preset image of veFaaS.<br><br>* **Code package**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The code Zip package must be an unencrypted file and cannot exceed 256 MiB.</div><br><br><br><br>   * **Function template**: Built\-in code templates provided by veFaaS, ready to use out of the box. Click **Code Preview** to view the resource files and code details included in the current template. Select the appropriate code template as needed.<br><br>   * **Local Upload Zip Package**: Upload a locally developed code Zip package.<br><br>   * **TOS Upload**: On the TOS upload panel, select the target Bucket and Zip file. |
      |Webserver mode |No. No HTTP Server is required, and no port needs to be exposed (set the port number Port to \-1). After successfully processing the request, the process exits actively or automatically after a timeout. |
      |Startup command |Enter the program's start command.<br><br><br>* When the deployment method is **image**: To specify a script file, use the absolute path and ensure the script has the appropriate executable permissions. If no script is specified, the `/opt/application/run.sh` script is executed by default.<br><br>* When the deployment method is **code package**: To specify a script file, use the relative path from the root directory of the code package and ensure the script has the appropriate executable permissions. If no script is specified, the `./run.sh` script in the root directory of the code package is executed by default. |
      

   * **Advanced settings**

      For details, see [Function Configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

5. Click **Create** to create the function.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Release the function's code and configuration online. For specific operations, see [Release Function](https://docs.byteplus.com/en/docs/faas/Release_function).
