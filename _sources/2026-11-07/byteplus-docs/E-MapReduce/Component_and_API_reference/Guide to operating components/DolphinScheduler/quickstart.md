---
title: "quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ds_quickstart"
---

This article guides you through a series of DolphinScheduler prerequisite steps to help you understand how to use the service and related concepts.

<span id="_1-前提条件"></span>
## 1. prerequisites


1. To use the DolphinScheduler service, select the Volcano Engine E\-MapReduce (EMR) Hadoop cluster type version 3.1.0 / 2.1.0 or above. For details on different versions, see: [Version overview](https://docs.byteplus.com/docs/undefined/68da347242e561058e056938).

2. There are two ways to introduce the DolphinScheduler service into a cluster:

   * When creating an EMR Hadoop cluster, select the DolphinScheduler component service from the optional component list. For details, see [Create cluster](https://docs.byteplus.com/docs/E-MapReduce/105456).

   * For an already created EMR Hadoop cluster, you can add the DolphinScheduler service in **Cluster details \> Service list**. For details, see


[Add service](https://docs.byteplus.com/docs/E-MapReduce/105409#_2-%E6%B7%BB%E5%8A%A0%E6%9C%8D%E5%8A%A1).


3. For clusters with the DolphinScheduler service installed, you need to bind an Elastic Public IP to the ECS instance where the service is located and configure the service port (the default DolphinScheduler service port is **12345**) to access the DolphinScheduler Web UI. For details, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).


<span id="_2-登录认证"></span>
## 2. Login authentication

Accessing the DolphinScheduler Web UI requires you to provide login authentication information.

The EMR DolphinScheduler service uses OpenLDAP for login authentication and the default admin account as the service administrator. You can obtain the password for this user on the `master-1-1` machine in the cluster. The password text file is located at `/root/.emr/secret`.

<span id="_3-创建队列"></span>
## 3. Create queue

When executing tasks such as Spark or Flink, DolphinScheduler may need to specify a particular YARN queue.

Assuming the queue has already been created in YARN, further configuration is required in DolphinScheduler. Refer to the following steps to create a queue:


1. Go to the **DolphinScheduler cluster details \> Access link** page.

2. Click the **DolphinScheduler UI** access link, enter the obtained account and password information, and access the UI.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Prerequisites for using access links:</div>



1. <div data-tips="true" data-tips-type="tip">The ECS instance of the master\-1\-1 node in the DolphinScheduler cluster must be bound to an Elastic Public IP. See <a href="https://www.volcengine.com/docs/6401/68687">Bind Public IP</a> for details.</div>


2. <div data-tips="true" data-tips-type="tip">In <strong>Cluster Details \> Access Links \> Quick Configure Server Port</strong>, you must add the source address and corresponding port to the allowlist before you can continue accessing. See <a href="https://docs.byteplus.com/docs/E-MapReduce/105434">Access Links</a> for details.</div>


3. In the navigation bar, click to enter the **Security Center \> Yarn Queue Management** page.

4. Click the **Create queue** button, enter the queue name and queue value, then click the **Confirm** button to complete the creation.


<span id="_4-创建租户"></span>
## 4. Create tenant

A tenant maps to an operating system user, which is used by the Worker process to Submit Job. If the tenant name configured in the interface does not actually exist in the system, task execution will fail. Accounts with administrator privileges can create tenants through the DolphinScheduler Web UI. Perform the following steps in the Web UI:


1. In the navigation bar at the top of the interface, click to enter the **Security Center \> Tenant Management** page.

2. Click the **Create Tenant** button, enter the **Operating System Tenant** name, and click the **Confirm** button to complete tenant creation.

3. If the corresponding user does not exist in the operating system, you can create the user using the `User Management` feature provided by EMR. For details about the user management feature, refer to the [User Management](https://docs.byteplus.com/docs/E-MapReduce/105426) documentation.


<span id="_5-创建用户"></span>
## 5. Create users

Users of the DolphinScheduler service are divided into two types: administrators and regular users.


* Administrator: Has permission to operate all features, including the Security Center.

* Regular user: Can create projects and create, edit, and execute workflow definitions, as well as perform other operations.


EMR DolphinScheduler is integrated with the EMR OpenLDAP authentication system out of the box, so user creation must be performed through `User Management`.

When using DolphinScheduler, each user must be associated with a tenant, and workflow tasks submitted by the user are executed by the associated tenant at the operating system level.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When the tenant associated with a user changes from A to B, all resources under tenant A for that user will be copied to tenant B.</div>


<span id="4618d489"></span>
### 5.1. **User permission management method**

For an out\-of\-the\-box cluster without configuration, users created in User Management are granted regular user permissions by default.

DolphinScheduler determines which account has administrator privileges by configuring the value of `security_authentication_ldap_user_admin`. By pointing this configuration to a username that has not logged in before, and creating a user with the same name through `User Management` and logging in, that user will immediately have administrator privileges.

<span id="_6-告警配置"></span>
## 6. Alarm configuration

When starting a workflow, you can set alarm group parameters. DolphinScheduler will deliver various status information during workflow instance execution using the plugin method that is predefined in the alarm instance associated with the alarm group.

<span id="_6-1-创建告警组实例"></span>
### 6.1. Create alarm group instances

Before creating an alert group, you need to create an alert instance. Each alert instance is associated with a specific notification method, and an alert group can be associated with multiple alert instances at the same time to enable diversified alert notifications. The steps for creating an alert instance are as follows:


1. Click to enter the **Security Center \> Alert Instance Management** interface.

2. Click the **Create Alert Instance** button, enter the following information (using the Feishu plugin as an example), to complete the creation:

   
   |Configuration items |Note |
   |---|---|
   |Alarm instance name |Enter the alarm instance name information. |
   |Select plugin |Currently, more than ten alarm plugins are supported, including Script, WeChat, Email, Feishu, Http, and more. |
   |Alarm type |You can select the alarm type: success, failure, or all. |
   |Webhook |Enter the Webhook address corresponding to the plugin. |
   |Enable proxy |Determine whether the alarm instance needs to enable a proxy. If a proxy is enabled, the following information must be provided. |
   |Proxy |Enter the proxy address information. |
   |Port |Enter the proxy port number. |
   |User |Enter user credentials for authentication. |
   |Password |Enter the password information required for authentication. |
   

   Different plugins require different configuration information, depending on the actual interface. For details, see [Alert Plugin Guide](https://dolphinscheduler.apache.org/zh-cn/docs/3.1.3/guide/alert/alert_plugin_user_guide).


<span id="_6-2-创建告警组"></span>
### 6.2. Create alert group

DolphinScheduler uses alert groups to associate workflow tasks with specific alert instances. An alert group can be associated with multiple alert instances at the same time. The specific steps for creation are as follows:


1. Click to enter the **Security Center \> Alert Group Management** interface.

2. Click the **Create Alert Group** button, enter the following information, to complete the creation:

   
   |Configuration item |Note |
   |---|---|
   |Alert group name |Enter the alert group name. |
   |Alert group instance |Select from the alert group instances that have already been created. Multiple selections are supported. |
   |Description |Enter the alert group description to help with future management. |
   


<span id="_7-创建-worker-分组"></span>
## 7. Create worker group

DolphinScheduler supports grouping Worker nodes, and you need to specify a specific Worker node group when executing workflow tasks. DolphinScheduler defines and uses the default group. You can also customize Worker node groups as needed. The specific steps are as follows:


1. Click to enter the **Security Center \> Worker Group Management** interface.

2. Click the **Create Worker Group** button, enter the following information, to complete the creation:

   
   |Configuration item |Note |
   |---|---|
   |Group name |Enter the Worker group name. |
   |Worker address |Use the dropdown to select the Worker Server address of the current cluster. |
   


<span id="_8-创建环境"></span>
## 8. Create environment

Environment configuration is used for setting environment variables when Worker nodes run tasks. Each environment configuration is equivalent to a dolphinscheduler_env.sh file. Worker nodes use the predefined content in the dolphinscheduler_env.sh file by default. To modify it, follow the steps shown below:


1. Click to enter the **Security Center \> Environment Management** interface.

2. Click the **Create Environment** button, enter the following information, to complete the creation:

   
   |Configuration item |Note |
   |---|---|
   |Environment name |Enter the environment name. |
   |Environment configuration |The default environment is the content of the dolphinscheduler_env.sh file. You can modify the environment configuration according to your actual business scenario. |
   |Environment description |Enter the environment description to help with future environment management. |
   |Worker group |Use the dropdown to select from the Worker groups that have already been created. |
   

   Environment configuration reference:

   ```shell
   # JAVA_HOME, will use it to start DolphinScheduler server
   export JAVA_HOME=${JAVA_HOME:-/usr/lib/jvm/java-8-openjdk-velinux-amd64}
   
   # Tasks related configurations, need to change the configuration if you use the related tasks.
   export HADOOP_HOME=${HADOOP_HOME:-/usr/lib/emr/current/hadoop}
   export HADOOP_CONF_DIR=${HADOOP_CONF_DIR:-/etc/emr/hadoop/conf}
   export SPARK_HOME1=${SPARK_HOME:-/usr/lib/emr/current/spark}
   export HIVE_HOME=${HIVE_HOME:-/usr/lib/emr/current/hive}
   export FLINK_HOME=${FLINK_HOME:-/usr/lib/emr/current/flink}
   
   export PATH=$HADOOP_HOME/bin:$SPARK_HOME1/bin:$PYTHON_HOME/bin:$JAVA_HOME/bin:$HIVE_HOME/bin:$FLINK_HOME/bin:$PATH
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc6a1e704b9e3c35af8091103acd5ce2.png) </span>


<span id="_9-创建-token-令牌"></span>
## 9. Create token

All backend interfaces of DolphinScheduler require access authentication. Using tokens ensures security and also makes it more convenient for users to access backend interfaces. You can create and manage tokens through the DolphinScheduler Web UI by following these steps:


1. Click **Security Center \> Token Management** to enter the page.

2. Click the **Create Token** button, enter the following information to create the token:

   
   |Configuration item |Note |
   |---|---|
   |Expiration time |Set the token expiration time to effectively restrict interface calls. |
   |User |Select the user corresponding to the token to allow the user to manage it. |
   |Token |The token is generated proactively. You can use the **Refresh** button on the right to generate a new token. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Administrators can manage token information for all users, while regular users are only allowed to operate their own token information.   </div>
   

<span id="_10-编排工作流"></span>
## 10. Orchestrate workflows

After configuring the above information, you can assign accounts to regular users and allow them to start using DolphinScheduler to orchestrate and execute workflow tasks.

<span id="_10-1-创建项目"></span>
### 10.1 Create a project

Workflows are organized by project, so before creating a workflow, you need to select or create the appropriate project on the **Project Management** page:


1. Switch to the appropriate user account and re\-enter the DolphinScheduler Web UI.

2. In the top navigation bar, click **Project Management** to enter the page.

3. Click the **Create Project** button and configure the following project parameters:

   
   |Configuration item |Note |
   |---|---|
   |Project name |Enter the project name to help manage and differentiate between different workflows. |
   |Owner |The project is assigned by default to the currently logged\-in user. |
   |Project description |Enter the project description to help with future project management. |
   

4. After configuring the information, click the **OK** button to complete project creation.


<span id="_10-2-创建工作流定义"></span>
### 10.2 Create a workflow definition

Click the name of the created **project** to enter the project overview page. In the left sidebar, you can see the tabs for project overview, workflows, and tasks.

Click "**Workflow \> Workflow Definition \> Create Workflow**" to enter the workflow orchestration page. DolphinScheduler provides a wide variety of task types to support complex and diverse workflow orchestration scenarios. You can refer to the official [Task Types](https://dolphinscheduler.apache.org/zh-cn/docs/3.1.3/%E5%8A%9F%E8%83%BD%E4%BB%8B%E7%BB%8D_menu/%E4%BB%BB%E5%8A%A1%E7%B1%BB%E5%9E%8B_menu) documentation to learn about the specific parameter configurations for each task type.

You can drag and drop the corresponding task type into the editing area on the right. The workflow node is configured as follows (using the shell node configuration as an example):


|Parameter |Note |
|---|---|
|Node name |Enter the node name for the task type. |
|Run flag |Select the task run status. You can choose between **Normal** and **Forbidden**. If you check "Forbidden", the workflow will not execute this task. |
|Description |Enter the task description for the current node to help with future identification. |
|Task priority |Select the priority level for the current task, divided into five levels from HIGHEST to LOWEST. Select as needed based on your actual situation. When there are not enough worker threads, tasks with higher priority will be executed first in the queue. Tasks with the same priority are executed in a first\-in, first\-out order. |
|Worker grouping |Use the dropdown to select a worker group that has been successfully created. |
|Environment name |Configure the environment for task execution. Use the dropdown to select an environment name that has been successfully created. |
|Task group name |Manage the resources occupied by task instances through task groups to prevent excessive resource usage from affecting other components in the cluster. You can create task group information in **Resource Center \> Task Group Management**. See [Task Group Management](https://dolphinscheduler.apache.org/zh-cn/docs/3.1.3/guide/resource/task-group) for details. |
|Group priority |Set the priority of this task within the current task group to allow it to obtain resources first within the same group. |
|Retry count on failure |Specify the number of times the task will be resubmitted upon failure. This can be manually entered. |
|Retry interval on failure |Specify the interval between resubmitting the task after failure. This can be manually entered. |
|CPU quota |Allocate a specified CPU time quota for the task. Unit: percentage. The default value \-1 means no limit. For example, 100% represents full load for one CPU core, and 1600% for sixteen cores. |
|Maximum memory |Allocate a specified memory size for the task. If this limit is exceeded, OOM will be triggered and the task will be killed without automatic retry. Unit: MB. The default value \-1 means no limit. |
|Delayed execution time |Specify the delay time for task execution, in minutes. |
|Timeout alert |Configure timeout alerts and timeout failures. When the task exceeds the "**timeout duration**", an alert email will be sent and the task will fail. |
|Script |Edit the code for the corresponding task type. |
|Resources |Resource files required for task execution. |
|Custom parameters |Enter the custom parameter information required in the task script. |
|Preceding task |Set a predecessor (upstream) task for the current task to establish an upstream\-downstream dependency between tasks. |


After completing the configuration, click the **OK** button to complete the node configuration, and click the Save button in the upper right corner to set the workflow information and global parameters.

<span id="_10-3-运行工作流任务"></span>
### 10.3 Run workflow tasks


1. Publish the workflow:

   Workflow definitions that have been created can only be executed after they are published online. Click the **Publish** button in the action bar to publish the specific workflow online:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_143d74af97a41af13ae7a40f232b4dbe.png) </span>

2. Run workflow:

   For workflows that have been published online, you can click the **Run** button to trigger immediate execution, or click the **Schedule** button to configure the corresponding periodic scheduling rules.

   On the **Workflow \> Workflow Instance** page, you can view the workflow instance for this run and perform quick actions such as editing, rerunning, and more, as shown below:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73d1f34c500e8d8cadf59d28f88dea02.png) </span>

3. View logs:

   To view the execution history or log information of a task, click a node in the specific workflow instance to enter the node editing area, double\-click the task type, and in the upper right corner of the popup window you will see options for **View History** or **View Logs**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_674e709ea416a0b9ce004627b715bff4.png) </span>
