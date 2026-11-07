---
title: "Shell"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/shell"
---

DataLeap supports the Shell task type, which allows for the referencing of resources, the configuration of parameters, and the editing of Shell scripts to meet your business scenario needs. This article will introduce the Shell task configuration description.

<span id="993ba454"></span>
## 1 Usage limitations


* When a Shell task needs to access private network services or resources, it must do so through the **dedicated compute resource group**. The Shell task interface does not support modifying network configurations individually.

* In the task execution settings, if you need to use a custom image to run tasks, you must install Python 3 in the custom image to ensure proper operation.

* When configuring upstream dependencies for Shell tasks, the **dependency recommendation** feature in scheduling properties is not supported. Upstream dependencies can only be added by **manual addition**. For details, see [Task scheduling depends on](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies).

* The SSH settings entry in task execution settings is currently restricted to whitelisted users. If you need to use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2hvbWU%3D) to contact us for activation.

* Debug log data in the data development interface is retained for 15 days. You can view the details of the corresponding debug logs within 15 days.


<span id="_2-前提条件"></span>
## **2 Prerequisites**


* When a sub\-user logs in to create a task, if the sub\-user manually selects the network environment, they must have the VPCReadOnlyAccess or VPCFullAccess permission policy for the private network. A sub\-user may request that the main account should add the corresponding permission policy to [Access Control](https://console.byteplus.com/iam/identitymanage/user). For details, see [Access Control](https://docs.byteplus.com/en/docs/vpc/IAM-Overview).

* To access a remote ECS host and execute scripts in ECS through a Shell task, you must first configure the SSH data source. For details, see [Configure SSH Datasource](https://docs.byteplus.com/docs/undefined/689ab4f7dd0ea1051cb44a55).


<span id="_3-1-创建任务"></span>
## **3 Create the task**


1. Log in to the [DataLeap tenant console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/overview?)

2. Enter the Data Development interface within a specific project and click **New Task** button to create a new task.

3. Select **Data Development \> Generic \> Shell** task type consecutively.

4. Fill in the basic task info, click **Confirm** button, and complete the task creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Task name information only allows characters, letters, numbers, underscores, hyphens, [], 【】, (), and Chinese characters, and must be within 127 characters.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aba4605430c47efb9e4b2a9f607ccb3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-编辑使用"></span>
## **4 Edit Usage**

After the task is created successfully, enter the code development editing interface.

<span id="_3-2-1-开发代码编辑"></span>
### 4.1 Code Development Editing


1. Supported languages: Shell Bash, as shown below:

   ```shell
   echo "Hello World !"
   ```
   

2. Parameters: Supported time parameters ${date}, ${hour}, etc., see [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252).

   ```shell
   echo ${date}
   ```
   


<span id="_3-2-2-网络配置（可选）"></span>
### 4.2 Network Configuration (Optional)

When tasks access public networks, private networks (VPC) resources, or image repository addresses with network access restrictions in scripts, you need to configure the network by selecting a private network, subnet, and security group information that can communicate with your resources.

The following two methods are available:


* You can manually select the network information such as the private network (VPC), subnet, and security group where the task resources and data sources are located.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a sub\-user logs in to create a task, if they manually select the network environment, they need usage permissions for services related to Private Network. At this time, the main account should, in <a href="https://console.byteplus.com/iam/identitymanage/user">Access Control</a>, add VPCReadOnlyAccess or VPCFullAccess permissions for the sub\-user. See details in <a href="https://docs.byteplus.com/en/docs/vpc/IAM-Overview">Access Control</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43f2cd8ad0e44b0db4dab6f209838ab7~tplv-goo7wpa0wc-image.image) </span>

* Or, when the project is bound to an **Exclusive Computing Resource Group**, you can also access resources and services under the private network by using the [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group) to achieve network intercommunication.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e2c4aa9adcf4a1ca6280e3485f08149~tplv-goo7wpa0wc-image.image) </span>

   You can [enable public network](https://docs.byteplus.com/en/docs/natgateway/Internet-NAT-Gateway-Getting-Started) access for the VPC of the Exclusive Computing Resource Group or align its VPC information with the VPC where your resources are located. If they do not match, you can also use [CEN](https://docs.byteplus.com/en/docs/cen/Getting-Started-Overview) to facilitate network intercommunication.

   After selecting **Exclusive Computing Resource Group**, the network configuration information here all comes from the Exclusive Computing Resource Group data. It is not currently supported to modify directly on the network configuration interface. You can configure the corresponding private network information when creating an Exclusive Computing Resource Group, [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group) See details.


<span id="_3-2-3-任务产出数据登记"></span>
### 4.3 Task Output Data Registration

Output data registration is used to record the data lineage of tasks and does not impact the logic of the code. It is strongly recommended to complete this if a Shell task contains output from specific database and table data, in order to maintain the data lineage relationship of the task in the future.


1. Engine type: Choose the data engine category based on actual conditions, such as EMR (EMR Hadoop, EMR Doris, EMR StarRocks Engine), ByteHouse, EMR Serverless Spark, EMR Serverless StarRocks, Default (no registration), etc.

2. Associated instance: Select the instance information under the corresponding engine.

3. Data type: Select the data type produced under the corresponding engine type.

4. Database table: Select the detailed name information of the database and table produced under the corresponding engine.


<span id="_3-2-4-执行设置"></span>
### 4.4 Execution Settings


1. Click to enter the right sidebar **Execution Settings** window.

2. Select computing resource group: Supported to choose common computing resource group, [Exclusive Computing Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group).

3. Image address:

   Supports custom images. It is recommended to use BytePlus image repository, dataleap\-{region}.cr.bytepluses.com/studio/spark:online, where the {region} value should be replaced with the actual region, such as johor\-ap\-southeast\-1.

   Complete example: Johor region: dataleap\-johor\-ap\-southeast\-1.cr.bytepluses.com/studio/spark:online

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you fill in the image repository address (such as a third\-party image repository) which needs to be accessed through the public network or a specified private network (VPC), you need to achieve inter\-network connectivity using the above <a href="https://docs.byteplus.com/docs/dataleap/shell#_3-2-2-%E7%BD%91%E7%BB%9C%E9%85%8D%E7%BD%AE%EF%BC%88%E5%8F%AF%E9%80%89%EF%BC%89">4.2 Network Configuration (Optional)</a>. You may try the following solutions:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enable your image repository address and the VPC address you configured to have <strong>public network</strong> access capability;   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The VPC where your image repository is located and the VPC you configured needs to be consistent, or connectivity can be achieved through <a href="https://docs.byteplus.com/en/docs/cen/Getting-Started-Overview">CEN</a>.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The basic image address contains only the most basic Linux and Python commands. In simple scenarios, you could also base on the basic image address and supplement some Dependencies.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Basic image address, Johor region: <code>dataleap-johor-ap-southeast-1.cr.bytepluses.com/studio/runtime_light:online</code>   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your custom image file contains encrypted files and you wish the image file to be used only for specific tasks, you can create a private image type and add private image configuration information such as <strong>mirror warehouse address, username, and password</strong> to the <strong>exclusive computing resource group</strong>, accessed through the <strong>exclusive computing resource group</strong>. For instructions on modifying resource group image configurations, see details <a href="https://docs.byteplus.com/docs/dataleap/exclusive_computing_resource_group">Exclusive Computing Resource Group Management</a>.   </div>
   

   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to manually fill in the <strong>OCI artifact repository</strong> with the specific image version's <strong>network address</strong> information, based on the actual image address entered. If the filling is omitted, the default basic image address will be accessed.   </div>
   

4. Resource configuration: Resources can be configured according to actual demand, using CU as the unit, with the default configuration being 1CU (1CU = 1Core 4GB); more specifications are available in the dropdown selection.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Specifications of 0.25CU and 0.5CU are only supported by the Exclusive Computing Resource Group.   </div>
   

5. Resource selection:

   Shell tasks support the use of **generic resources** in task editing, enhancing data development efficiency through access to Jar, File, Zip, and other types of resources.

   In the **Resource selection** dropdown, select the resources needed for the task. If no resources have been created yet, you can also click the **Create Resource** button to go to the resource library and create new ones. See details on creating resources at [Resources Library](https://docs.byteplus.com/docs/undefined/682aa9fee638492ec7c94266).


<span id="_3-2-5-任务模板"></span>
### 4.5 Task Template

By clicking the **Task Template** button, you can choose whether to use task templates for quick and convenient code template logic reuse. In the popup, select the Shell task template, choose the appropriate version number, and enter replacement parameters to complete reuse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc0b10dcdc5e4af2883e54213d744ca0~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">When using task templates, the image address in the interface editor and execution settings <strong>cannot be edited again.</strong> If the current task template code does not match your current business scenario logic, you can modify or create a new version of the task template to reuse in different business scenarios.</div>


2. <div data-tips="true" data-tips-type="warning">When modifying templates, pay attention to references by other tasks, operating instructions can be seen in <a href="https://docs.byteplus.com/docs/undefined/682aa78f5743da0516029455">Task Template</a>。</div>



<span id="9eb8b872"></span>
## 5 Subsequent Actions

After editing the task, you can configure the [scheduling settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings) of the node as needed, and then save, debug the task, and commit it for release. For detailed submission release instructions, see [4.1 Submit Batch Task](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-1-%E7%A6%BB%E7%BA%BF%E4%BB%BB%E5%8A%A1%E6%8F%90%E4%BA%A4).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When debugging, if you directly use online data, proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days. You can view the corresponding debug log details within 15 days.</div>


* <div data-tips="true" data-tips-type="warning">This task type supports sending message notifications to the initiator of the debug after a debug execution is either successful or failed. Based on your business needs, you can go to <strong>Project Console \> Configuration information \> message notification settings</strong> to choose whether to enable notifications for <strong>Execution Successful</strong> or <strong>Failed</strong>. Default notification method is <strong>Email</strong>. Debug initiators must bind the corresponding <strong>Security Email</strong> information in BytePlus "Account management" in advance.</div>



<span id="81185be4"></span>
## 6 FAQ

<span id="4e839f24"></span>
### Q1. What is the reason for the inconsistency between the execution time in the container and the collection time in the DataLeap log?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8be66a3bcd24041a8eac6e7b0300ce1~tplv-goo7wpa0wc-image.image) </span>


* Problem Description:

   In Shell tasks that involve running Java scripts and printing Java\-related logs, there is an inconsistency between the time printed in the logs and the current time.

* Cause of Problem and Solution:

   The default environment inside the container for Shell tasks is in the UTC+0 time zone, so the time displayed when printing logs inside the container is in the UTC+0 time zone. You can add a command in the Shell script to modify the container's time zone to align the log time inside the container with the DataLeap log collection time. To modify the command, see the example: `timedatectl set-timezone "Asia/Shanghai"`


<span id="8b4aa1d7"></span>
### Q2. How to resolve empty network information in Shell tasks migrated from other platforms?


* Problem description:

   When migrating Shell tasks from other platforms to the DataLeap platform, an **exclusive computing resource group** was used, but the network configuration information was empty, which caused the task to be unable to execute normally.

* Solution:

   Task migration causes the network to become unassociated. On the right side of the task, in **Execution settings**  **\- Computing resource group**, switch to the corresponding **Exclusive computing resource group**. After rebinding, the network will be associated with the corresponding resource group information, resolving the issue of empty network information.
