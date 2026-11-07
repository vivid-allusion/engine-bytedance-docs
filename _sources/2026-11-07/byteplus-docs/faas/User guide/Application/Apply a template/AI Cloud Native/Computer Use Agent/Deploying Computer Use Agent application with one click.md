---
title: "Deploying Computer Use Agent application with one click"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Deploying_Computer_Use_Agent_application_with_one_click"
---

This article shows you how to use Function Service Application Center to deploy your own Computer Use Agent application with one click.

<span id="background-information"></span>
## Background information


* **Application introduction**

   Computer Use Agent is an intelligent agent service launched by the BytePlus based on ByteDance's Doubao large model, facing end users and AI application developers. The service has built\-in self\-developed out\-of\-the\-box MCP protocol\-driven Computer Use capabilities, supporting mouse control, keyboard control, and screenshot control, and other capabilities for Windows, Linux remote virtual computers. This service easily realizes remotely controlling end points (computers), completing work such as cutting and editing videos, creating PowerPoint slides, and operating and maintaining self\-media accounts, etc.

* **Runtime**

   Native Python 3.12, Native Node.js 20.x Runtime.

* **Associated cloud services**

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Using associated cloud services generates corresponding usage fees. For billing details, refer to the billing documentation of the associated cloud services.   </div>
   

   * Computer Use Agent backend

      * [Function Service](https://www.byteplus.com/en/product/faas): Provides a large model\-driven computer to automate the execution of tasks, real\-time viewing of desktops, and operating computer keyboard and mouse interfaces.

      * [API Gateway](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway): Expose the interface through the API Gateway.

      * [Elastic Compute Service](https://www.byteplus.com/en/product/ecs): Provides Computer instances that execute specific tasks output by the large model.

      * [Virtual Private Cloud](https://www.byteplus.com/en/product/vpc): Connect the network between Function Service and Computer instances.

      * [NAT gateway](https://www.byteplus.com/en/product/nat): Applications access the public network through the NAT gateway.

      * [Elastic IP](https://www.byteplus.com/en/product/eip): Applications need to associate the public network IP (EIP) to use the NAT gateway.

      * [Torch Log Service](https://www.byteplus.com/en/product/tls) (optional): Provides one\-stop services for logs\-like data.

      * [Cloud Monitor](https://www.byteplus.com/en/product/cloudmonitor) (optional): Support viewing function basic monitoring via cloud monitoring.

   * Computer Using Agent front end

      * [Function Service](https://www.byteplus.com/en/product/faas): Computer Use Agent interaction console.

      * [API Gateway](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway): Access the console through the API Gateway.


<span id="prerequisites"></span>
## Prerequisites


* All the cloud services associated with this application have been activated.

* Virtual Private Cloud (VPC), subnets, and security groups have been created in the regions where the applications are pending deployment. For detailed operations, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* IAM users need to ensure that they have authorized the **VeFaaSFullAccess**, **APIGFullAccess**, and **STSAssumeRoleAccess** policies. If any of the above policies is missing, contact the root user or the administrator for authorization. For specific operations, refer to [Editing a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-user).

* An API gateway instance of the Serverless gateway type has been created. For detailed operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* When using Function Service for the first time, make sure that the cross\-service authorization is completed. If authorization is not done, the console will pop up the cross\-service authorization page to guide you to complete authorization.


<span id="procedure"></span>
## Procedure


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar select **Application** \> **App Square**.

4. On the **App Square** page, select **Computer Use Agent** template, and click **Create applications**.

5. On the **Creating Applications** page, configure application parameters.

   * Basic information

      
      |**Parameter** |**Description** |
      |---|---|
      |Selected template |Displays the selected template. This scenario is a **Computer Use Agent**. |
      |Name |Customize the name of the application according to the naming rule prompted by the system. You can also directly use the application name automatically generated by the system. |
      |Description |Fill in the remarks information for the current application, which can also be empty. |
      |IAM role |The Application Center provides a system default role **ServerlessApplicationRole**, which contains permissions for partial cloud resources that the Application Center needs to access.<br><br><br>* If your user role does not contain this role, then this role will be automatically added.<br><br>* If your user role contains this role, then the system will automatically detect whether this role contains all the policies required for the current application. When any relevant policy is missing, the console will prompt the name of the policy that needs to be added, and add through clicking **Add Policy**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">IAM users need to ensure that the <strong>IAMReadOnlyAccess</strong> policy is authorized, otherwise you will not have the permission to obtain <strong>ServerlessApplicationRole</strong> role information.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If IAM users need to further add policies for the <strong>ServerlessApplicationRole</strong> role, you need to ensure that the <strong>IAMFullAccess</strong> policy is authorized.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">For more role\-related operations for IAM users, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3">IAM Documentation</a>.</div><br> |
      |Associated cloud services |Display the names, activation status, and activation purposes of all the cloud services that the current application needs to use.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For billing generated when using associated cloud services and requirements for account balance, refer to the relevant cloud product billing documents: <a href="https://docs.byteplus.com/en/docs/faas/Billing_overview">Function Service billing</a>, <a href="https://docs.byteplus.com/en/docs/apig/Billing_overview">API Gateway billing</a>, <a href="https://docs.byteplus.com/en/docs/vpc/Billing">Virtual Private Cloud billing</a>, <a href="https://docs.byteplus.com/en/docs/ecs/Billing-overview">Elastic Compute Service billing</a>, <a href="https://docs.byteplus.com/en/docs/tls/billable_items">Torch Log Service billing</a>, <a href="https://docs.byteplus.com/en/docs/natgateway/Billing-overview">NAT Gateway billing</a>, <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">Elastic IP Address billing</a>.</div><br> |
      

   * Resource allocation

      **Resource allocation** modules support the following two configuration methods:

      * **One\-click automatic configuration**: The system will automatically complete the basic configuration for you, and you only need to fill in the AK/SK information according to the use demand. When the AK/SK is not filled in, the application will create a Linux ECS instance by default, and you need to manage the instance in the ECS console; after filling in the AK/SK, managing the instance in the application is supported.

      * **Custom configuration**: You need to customize the configuration for the application parameters in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Basic information** ||
      |Region |Displays the region where the current application and its assoicated cloud resources are located. |
      |VPC |Select the VPC where you create Computer Use Agent application and cloud\-dependent resources. |
      |Subnet |Among the subnets under the selected VPC, select the subnet in which you expect to deploy Computer Use Agent. Only support selecting one subnet. |
      |Security group |Select a security group where you create Computer Use Agent application and cloud\-dependent resources. |
      |**Large Model Configuration** ||
      |API Key |Resource API Key for computers to use intelligent agent services. Support selecting from the list of the existing API Key under the current account, or you can also customize the API Key you enter. For obtaining method, refer to [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).<br><br>The environment variable Key (Env key) corresponding to the **Model Resource API Key** is: **ARK_API_KEY**. After creating the application, you can view or modify the model resource API Key through **ARK_API_KEY**. |
      |GUI Agent model |The doubao\-1.5\-thinking\-vision\-pro and doubao\-1.5\-ui\-tars\-250328 models are provided by default. The user can choose the model after the Computer Use Agent starts. |
      |**Agent Configuration** ||
      |API Access Key |Fill in the Access Key ID and Secret Access Key (AK/SK) information according to the use demands. When not filled in, the application will create a Linux ECS instance machine by default, and you need to manage the instance in the [ECS console](https://console.byteplus.com/ecs); after filling in AS/SK, managing ECS instances in the application is supported. |
      |**Access Configuration** ||
      |Gateway instance |Select the API Gateway instance of the Serverless type prepared in the prerequisites. API Gateway Trigger related resources, including services, Upstream, and routing, are automatically created under this instance. |
      

6. Click **Confirm** to start creating and deploying the application.

   The system will automatically jump to the application details page, and you can view the application deployment status and logs in real time.


<span id="result-validation"></span>
## Result validation


1. After the application deployment is successful, under the **Basic Information** module on the **Application Details** tab, click **Access Entry Point Details** to enter your own Computer Use Agent application interaction page.

2. On the Computer Use Agent application interaction page, select the operation system type you need and start the sandbox, enter the task, and view the remote computer operations, execution steps, and results driven by the large model in real time.
