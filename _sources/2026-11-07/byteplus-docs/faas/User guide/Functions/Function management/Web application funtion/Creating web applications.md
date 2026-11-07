---
title: "Creating web applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_Web_applications"
---

Web applications help users host native web framework applications, support popular frameworks based on various languages (such as Golang Gin) or custom container images for developing web programs, and enable migration of existing web applications. This article introduces how to create web applications.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The veFaaS is activated.

* Cross\-service authorization needs to be complete if you use veFaaS for the first time.

* Code development has been completed locally. For details, see [Native runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime) and [Native Python runtime](https://docs.byteplus.com/en/docs/faas/Native_Python_runtime).

* (Optional) To upload code via TOS, store the code zip package in TOS in advance. For specific operations, see [TOS getting started](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* (Optional) To upload code via local or TOS, ensure the code zip package is not encrypted and does not exceed 256 MiB.

* (Optional) To access Virtual Private Cloud (VPC), ensure BytePlus Virtual Private Cloud has been activated, and a Virtual Private Cloud, subnet, and security group have been created in the region where the function will be deployed. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), and [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Optional) The BytePlus Torch Log Service (TLS) has been activated. If you need to use a custom logging project to handle function logs, ensure that the project and topics have already been created. For details, see Creating log projects and Creating log topics.

* (Optional) To manage function resources by project, create a project in advance. For specific operations, see [Create project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

When using container image deployment:


* Container images must be pushed to the BytePlus Container Registry in the same region as the function.

* After the function is created, wait for image synchronization to complete before releasing the function.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Function \> Function management**, and on the **Function** page, click **Create function**.

4. On the creation method page, click **Web Application Function** \> **Create Web Application Function**, and configure the parameters as described below.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Function name |Specify a custom name for the function. Function names cannot be repeated within the same account. After a function name is created, it cannot be modified. |
      

   * **Function code**

      
      |**Parameter** |**Description** |
      |---|---|
      |Deployment method |The following deployment methods are supported. Select as needed.<br><br><br>* **Image**: Deployment via container image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Public images are contributed by community developers. veFaaS does not maintain them. For software usage issues, please provide feedback to the community.</div><br><br><br><br>   * **Container Registry**: Select the specific image to deploy from your BytePlus Container Registry. You can filter out a specific image by instance, namespace, and repository type (public or private).<br><br>      When you select an image from **Container Registry**, veFaaS automatically obtains the configurations of the image, including the **startup command** and **environment variables**. You can specify whether to apply the configurations of the selected image to the function****.<br><br>   * **Public image**: An out\-of\-the\-box preset image of veFaaS.<br><br>* **Code package**<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The code Zip package must be an unencrypted file and must not exceed 256 MiB.</div><br><br><br><br>   * **Function template**: Built\-in, ready\-to\-use code templates provided by veFaaS. Click **code preview** to view the resource files and code details included in the current template. Please select the appropriate code template as needed.<br><br>   * **Upload local Zip file**: Upload a locally developed Zip file.<br><br>   * **Upload via TOS**: In the TOS upload panel, select the target Bucket and Zip file. |
      |Runtime |Select a runtime environment for the function code. If the preset runtime does not meet your business requirements, you can build a runtime based on a custom image that matches your code's runtime environment and start method. For details about custom runtimes, see [Create a custom runtime](https://docs.byteplus.com/en/docs/faas/Create_a_custom_runtime). |
      |Webserver mode |Default value: Yes. You need to implement an HTTP server in the image or code and enable the server to listen on a port to process requests. |
      |Startup command |Enter the program's start command.<br><br><br>* When the deployment method is **image**: To specify a script file, use the absolute path and ensure the script has the appropriate executable permissions. If not entered, the `/opt/application/run.sh` script is executed by default.<br><br>* When the deployment method is **code package**: To specify a script file, use the relative path under the root directory of the code package and ensure the script has the appropriate executable permissions. If not entered, the `./run.sh` script under the root directory of the code package is executed by default. |
      |Listening port |Enter the port that the HTTP server listens on. The default port is 8000, and the valid range is [1024, 65535]. Please avoid using ports 9000, 9001, and 9990, which are occupied by services.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The enabled HTTP server needs to listen on <code>0.0.0.0:Port</code> or <code>*:Port</code>. Otherwise, a request timeout error will occur.</div><br> |
      

   * **Advanced settings**

      For details, see [function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

4. Click **Create** to create the function.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Deploy the function's code and configuration online. For specific operations, see [release function](https://docs.byteplus.com/en/docs/faas/Release_function).
