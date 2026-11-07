---
title: "Create and deploy managed apps (non-Java tech stack)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_non-Java_stack"
---

This article describes how to create and deploy managed applications based on non\-Java technology stacks (for example, Node.js, Python, and so on) using host\-based deployment.

<span id="rhjYR9lK"></span>
## Prerequisites


* The required deployment files or deployment resources for the application to be deployed have been prepared.

   * Image deployment

      * CR repository image: The image for the application to be deployed has been uploaded to the container registry. For operation details, see [Push and Pull artifacts](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

      * Custom image: The address of the deployment image has been obtained, in the format `host/namespace/repo:tag`.

* The ECS instance to be deployed has been connected. For specific operations, see [Add ECS host group](https://docs.byteplus.com/en/docs/cp/Add_ECS_host_group#.5re75YqgLWVjcy3kuLvmnLrnu4Q=).


<span id="hSM8zAam"></span>
## Procedure


1. Log in to the Application Management page.

   1. Log in to the [Continuous Delivery Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **Workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the Application Management page, click **Create Application**.

3. On the Create Application page, select **Managed Application**, and fill in the relevant configuration information for the application as required.

   1. Fill in the **Application information**. After completion, click **Next: Environment configuration**.

      
      |Parameter |Description |
      |---|---|
      |App ID |Fill in the application ID as prompted on the interface. The App ID is the unique identifier for the App and cannot be changed after creation. |
      |App display name |Customize the display name of the App. |
      |App deployment type |In this scenario, select **Hosts**. |
      |App technology stack |This scenario only supports **Others**. |
      |Description |Enter notes for the current App. This field can be left blank. |
      |Member management |Quickly configure the members of the current App and assign different permissions to each member to meet the needs of multi\-role collaboration for App delivery.<br><br><br>* **Add members**: Add multiple members to the current App. Only users who have visible permissions in the current workspace can be selected. The system will, by default, add the BytePlus account (root user) and the App creator as administrators.<br><br>* **Permission**: The system has built\-in **administrator** and **Read\-only** roles. Each member can be assigned permissions for one or more roles.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Canceling the administrator permission of the root user is not allowed, and deleting the root user is not allowed.</div><br> |
      

   2. Fill in the **Environment configuration**. After completion, click **Next: Basic configuration**.

      
      |Parameter |Description |
      |---|---|
      |Host group |Select the host group to deploy. |
      |deployment resource |Select ECS instances to deploy in bulk. |
      |Environment ID |Set the unique identifier for the current environment. By default, `${App ID}-prod` is used, and customization is supported. Modification of the Environment ID is not supported after it is created successfully. |
      

   3. Fill in the **Basic configuration**. After completion, click **Next: Advanced settings**.

      
      |Parameter |Description |
      |---|---|
      |Deployment method |You can select **Image deployment**. |
      |Image deployment |Supported only when **Deployment method** is **image deployment**. Set the App image. Supports two methods: **CR Container Registry image** and **Custom images**. Please select as needed.<br><br><br>* **CR Container Registry image**: Select a container image from your BytePlus Container Registry. Select the **Region**, **Instance**, **Namespace**, **OCI Repository**, and **Tag** where the target image is located.<br><br>* **Custom images**: Directly enter the image address used by the App. The image address format is `host/namespace/repo:tag`. |
      |Version |Customize the version number of the App. You can click **Use timestamp for version number** on the right to automatically generate the version number. |
      |Package Update Strategy |Supports setting different release policies.<br><br><br>* Full: Deploy all ECS Hosts at once.<br><br>* Batch release: Deploy ECS Hosts in batches. Supports suspending deployment between two deployment batches. |
      

   4. (Optional) Fill in the **Advanced settings**.

      
      |Parameter |Description |
      |---|---|
      |Execution user |Users at the operating system level who execute deployment commands on the target Hosts, such as `root`, `admin`, and so on. Different execution users can be granted different resource management permissions. Specific execution users can be flexibly designated during deployment to ensure security and compliance. |
      |Start script |Scripts run before executing the App start command can be used to set environment variables, create temporary directories, or perform other preprocessing actions. If script execution fails, deployment will be aborted. |
      |Stop script |Scripts executed after deployment is complete can be used to clean up old artifact packages, temporary files, or perform other maintenance operations. If script execution fails, deployment will be aborted. |
      |Health check |After you enable health check, the platform uses the curl command to send an HTTP request. If the returned status code is 200, the health check passes.<br><br>It is recommended to enable health check to determine whether the App is deployed successfully.<br><br><br>* **Health check URL**: Enter the path for health check. For example: `http://127.0.0.1:8080`.<br><br>* **App wait time**: Set the timeout for health check. |
      

4. Click **Confirm** to start deploying the application. You can view the deployment progress of the application on the environment tab.


<span id="hfPorRNd"></span>
## Operation result

After the deployment is completed, the **Deployment status** will change to **Completed**. On the **List of instances** tab, click **Log** to view the host deployment log. You can confirm whether the application was deployed successfully by checking the health check results in the log.
