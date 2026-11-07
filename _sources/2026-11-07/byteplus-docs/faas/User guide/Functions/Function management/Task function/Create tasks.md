---
title: "Create tasks"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_tasks"
---

Tasks help users host one\-off script tasks, for example, executing test scripts, data synchronization, data cleaning, GPU inference/training, and more. Serverless tasks respond to asynchronous invocation requests using task mode, track and save the status of each stage of the task, provide comprehensive task control and observability capabilities, and are suitable for long\-running tasks and compute\-intensive scenarios. This article introduces how to create a task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The veFaaS is activated.

* Cross\-service authorization needs to be complete if you use veFaaS for the first time.

* Code has been locally developed. For details, refer to [Native runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime).

* (Optional) To upload code via TOS, store the code Zip package in TOS in advance. For specific operations, see [TOS getting started](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* (Optional) To upload code locally or via TOS, ensure the code Zip package is a non\-encrypted file and does not exceed 256 MiB.

* (Optional) To access a Virtual Private Cloud (VPC), ensure BytePlus Virtual Private Cloud has been activated, and a Virtual Private Cloud, subnet, and security group have been created in the region where the function will be deployed. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Recommended) To view function logs, ensure Torch Log Service has been activated. If you need to use a custom logging project to handle function logs, ensure that the project and topics have already been created. For details, see Creating log projects and Creating log topics.

* (Optional) To manage function resources through projects, create a project in advance. For specific operations,   see [create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

When deploying with container images:


* Container images must be pushed to the BytePlus Container Registry in the same region as the function.

* After the function is created, wait for image synchronization to complete before releasing the function.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. Select **Function \> Function management** in the left navigation bar. On the **Function** page, click **Create function**.

4. On the creation method page, click **Task function** \> **Create task function**, and configure the parameters as described below.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Function name |Specify a custom name for the function. Function names cannot be repeated within the same account. After a function name is created, it cannot be modified. |
      |Description |Enter a description for the function. You can leave this field empty. |
      

   * **Function code**

      
      |**Parameter** |**Description** |
      |---|---|
      |Deployment method |The following deployment methods are supported. Please select as needed.<br><br><br>* **Image**: Deploy using container image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Public images are contributed by community developers. veFaaS does not maintain them. If you encounter software usage issues, please provide feedback to the community.</div><br><br><br><br>   * **Container Registry**: Select the specific image to deploy from your BytePlus Container Registry. You can filter out a specific image by instance, namespace, and repository type (public or private).<br><br>      When you select an image from **Container Registry**, veFaaS automatically obtains the configurations of the image, including the **startup command** and **environment variables**. You can specify whether to apply the configurations of the selected image to the function****.<br><br>   * **Public image**: An out\-of\-the\-box preset image of veFaaS.<br><br>* **Code package**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The code Zip package must be an unencrypted file and must not exceed 256 MiB.</div><br><br><br><br>   * **Function template**: Built\-in, ready\-to\-use code templates in veFaaS. Click **Code preview** to view the resource files and code details included in the current template. Select the appropriate code template as needed.<br><br>   * **Upload local Zip package**: Upload a locally developed code Zip package.<br><br>   * **TOS upload**: In the TOS upload panel, select the target Bucket and Zip file. |
      |Runtime |Select a runtime environment for the function code. This scenario only supports **Native runtime**. |
      |Webserver mode |No. Used to execute a user\-specified one\-off task script. The script does not need to include an HTTP Server and does not expose any ports (set the port number Port to \-1). After the task script finishes execution, it exits proactively. veFaaS determines whether the task succeeded based on whether the script exit code is 0. In the event of execution timeout, veFaaS will forcibly terminate the task process. |
      |Startup command |Enter the program's start command.<br><br><br>* When the deployment method is **image**: To specify a script file, use the absolute path and ensure the script has the required executable permission. If not entered, the `/opt/application/run.sh` script is executed by default.<br><br>* When the deployment method is **code package**: To specify a script file, use the relative path from the root directory of the code package and ensure the script has the required executable permission. If not entered, the `./run.sh` script in the root directory of the code package is executed by default. |
      

   * **Advanced settings**

      Asynchronous tasks are enabled by default and cannot be turned off. For more parameter details, see [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

4. Click **Create** to create the function.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Deploy the function's code and configuration online. For specific operations, see [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).
