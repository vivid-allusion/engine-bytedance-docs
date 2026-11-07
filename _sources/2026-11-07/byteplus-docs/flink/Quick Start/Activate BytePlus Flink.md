---
title: "Activate BytePlus Flink"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Activate_BytePlus_Flink"
---

Using BytePlus Flink requires creating a project, with isolated computing resources and independent development consoles for each project. This article explains the steps to activate a BytePlus Flink project and important considerations during the activation process.

<span id="920f24b0"></span>
## **1. Prerequisites**

Before starting, **ensure** the following preparations are complete:


|Steps |Actions |Description |
|---|---|---|
|1.1 |**Register a BytePlus platform account** |Refer to the [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) to complete account registration |
|1.2 |**Enable TOS object storage** |Search for the **TOS** service in the console and activate it. A dedicated Bucket will be automatically created when BytePlus Flink starts (used to store BytePlus Flink job JAR packages/logs) |
|1.3 |**Configure IAM permissions** |Grant the main account IAM permissions: `FlinkFullAccess`<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f98de658a00141aa81f2238d196c86e9~tplv-goo7wpa0wc-image.image) </span> |
|1.4 | **(Optional) Create VPC, subnet, security group, etc.**  |When activating the resource pool, select VPC, subnet, security group, and other network information. It is recommended to plan the network in advance. |


<span id="1016de1b"></span>
## **2. Activate BytePlus Flink service**

Enable the BytePlus Flink service


1. Log in to the cloud platform console and select **Data Analytics** \> **BytePlus Flink**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efa53ae99da044a998eaa07e23f8ac5f~tplv-goo7wpa0wc-image.image) </span>


2. For first\-time login to BytePlus Flink, use the main account to click **Authorize Now** and grant cross\-service access:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e68fea032429404784144e7197f9faed~tplv-goo7wpa0wc-image.image) </span>


3. Click **Initialization** to initialize the BytePlus Flink service:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29ba123130b04029b484cadac027c579~tplv-goo7wpa0wc-image.image) </span>


4. Confirm the service region (e.g., `Asia Pacific (Johor)`)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/768ce7b2aeec417eb90e3438cc0fbbd3~tplv-goo7wpa0wc-image.image) </span>


5. After confirmation, wait 3\-5 minutes for the service initialization to complete. If an error occurs during this period, it may be due to TOS service not being activated or lack of permissions. Please follow the prompts to take appropriate action. The image below indicates the service is successfully activated


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e61aac766ca9477d8608f922ee22b117~tplv-goo7wpa0wc-image.image) </span>

> ⚠️ *Note:* 

> 1. If the Flink page does not show the initialization prompt, check whether you have FlinkFullAccess permission. If not, contact the primary account for authorization.

> 2. *The TOS Bucket will be created automatically upon the first activation. Do not delete it manually.* 


<span id="1a8a537f"></span>
## **3. Create a project**

A project is the basic unit for job management


1. Go to **Flink Console** \> **Project Management**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeb7208e64fa451a9fb17e6d801e073c~tplv-goo7wpa0wc-image.image) </span>


2. Click **Import Project** and fill in the configuration:

   * **Project Name**: Select a project from existing IAM projects to import

   * **Description**: Describe the project's purpose (optional)

   * **Project manager**: Select an IAM user as the project owner, who will assign and manage permissions for subsequent users


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/638cc99f4d7a4ee280de22508dcea94f~tplv-goo7wpa0wc-image.image) </span>


3. Click **Confirm**, and the system will automatically import the project from IAM and generate a BytePlus Flink project:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dd63be5752045ceacba67ee61ce3621~tplv-goo7wpa0wc-image.image) </span>

<span id="2453c0e0"></span>
## **4. Purchase a resource pool**


1. Go to **BytePlus Flink Console** \> **Project Management**, then enter the target project


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2beb5a98a8547cc8b550bac2d683afa~tplv-goo7wpa0wc-image.image) </span>


2. Within the target project, navigate to **Compute** **Resource** \> **Resource Pools**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26b8f2c41f644b8992392499efb296da~tplv-goo7wpa0wc-image.image) </span>


3. Click **Create Resource Pool** and configure the parameters:

   * **Billing Type**: Pay\-as\-you\-go (recommended for testing) / Annual or monthly subscription

   * **Resource pool name**: required, resource pool identifier

   * **Region and availability zone**: select as needed; it is recommended to choose the availability zone where the VPC network is located

   * **Network information**: select private network, subnet, and security group; it is recommended to keep consistent with the VPC network of connected upstream and downstream resources

   * **TOS object storage**: Flink will select the default TOS bucket; please ensure do not delete this bucket


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b07ad1a0295b4f01b4dc55848b553e5d~tplv-goo7wpa0wc-image.image) </span>


4. Confirm the order and payment, then wait for the status to change to **Running** (about 2 minutes)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b2d5fddc16148b2a86c24466fea5936~tplv-goo7wpa0wc-image.image) </span>

<span id="caf43dd7"></span>
## **5. Follow\-up tasks**

After completing the basic environment setup, you can continue


|**Function** |**Operation entry** |
|---|---|
|View resource pool details |On the BytePlus Flink console, go to Resource Management \> Resource Pool to view resource pool details. Click the resource pool name to see its name, type, status, network information, DNS configuration, storage information, payment details, and more. |
|[Permission Overview](https://docs.byteplus.com/docs/flink/Permission_Overview) |IAM users, IAM roles, and others require IAM permissions (such as purchasing resource pools) and project permissions (such as job development and maintenance) to access the BytePlus Flink console. |
|[Import Project](https://docs.byteplus.com/docs/flink/Import_Project_From_BytePlus) |A project is the basic unit for managing BytePlus Flink tasks; all your configurations, tasks, and permissions are maintained within a single project. |
|Job development and maintenance management |Within the project space, select task development and task management to create, edit, delete, start, stop, restart jobs, and view logs, monitoring data, and job details.<br><br>You can refer to [Flink SQL tasks](https://docs.byteplus.com/docs/flink/Flink_SQL_tasks), [Flink CDC Tasks](https://docs.byteplus.com/docs/flink/Flink_CDC_Tasks), [Flink JAR Tasks](https://docs.byteplus.com/docs/flink/Flink_JAR_Tasks), [Flink Python tasks](https://docs.byteplus.com/docs/flink/Flink_Python_tasks), a for task development and maintenance management. |
|Resource management |You can manage the resource pool of the project space. Reference [Resource Pool Overview](https://docs.byteplus.com/docs/flink/Resource_Pool_Overview) |
|Release resources |You can click the delete button in the resource pool to release unused computing resources. Reference [Delete Resource Pool](https://docs.byteplus.com/docs/flink/Delete_Resource_Pool) |


<span id="a653a834"></span>
## **FAQ**


1. Why can't the service initialize after entering the Flink console?


**Answer**: check if you have FlinkFullAccess permission. Without this permission, you cannot view or perform the initialization service operations.


2. Why does the initialization service fail with a prompt that TOS service is not enabled?


**Answer**: BytePlus Flink relies on the TOS service to create Bucket buckets, so enabling the TOS service is required.
