---
title: "Data Operation and Maintenance Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Operation_and_Maintenance_Configuration"
---

Data O&M consists of five modules: task management, data connections, queue configuration, storage management, and synchronization configuration. This document introduces the operational procedures for each functional module of data O&M configuration.

<span id="630e3c4c"></span>
# Overview

You can click the "System Management" button in the upper right corner to enter the system management page, where you can access the data O&M configuration module. Administrators can systematically manage multiple aspects, including task management, data connections, queue configuration, storage management, and synchronization configuration:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10c1711fe6624617bbefb668ff8ccaea~tplv-goo7wpa0wc-image.image) </span>


* Task management: In task management, administrators can establish dependencies on the execution status of tasks on third\-party platforms by using HTTP APIs, ensuring the timely production of valid business data.

* Data connections: In data connections, administrators can configure different types of data connections for different projects. For example, in different projects, the types of data connections available to users can vary; the types of data connections available to administrators and non\-administrators can also differ.

* Queue configuration: Configure different queues for scheduled tasks and data backtracking tasks to reduce the impact of data backtracking on routine tasks.

* Storage management: View resource overview information and configure storage policies, including a switch to enable resource control, project resource limit configuration, and over\-limit resource configuration.

* Synchronization configuration: Set upper limits for lifecycle and backtracking time.


<span id="f2da06c4"></span>
# Common use cases

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34e301179b04432c8a3046624488a4bf~tplv-goo7wpa0wc-image.image) </span>


* Enterprises want to use third\-party APIs to configure dependencies and orchestrate the orderly scheduling of upstream and downstream task nodes based on node dependencies. That is, downstream nodes will only start running after upstream nodes have successfully run.

* In some projects, project administrators are allowed to use all types of data connections, while certain types of data connections are not available to other users.

* Managers within the company often need to review long\-term data, or planning and operations personnel frequently compare data from different stages, requiring frequent dataset reviews.

* The aim is to avoid blocking operational resources and unnecessary overhead by adjusting the upper limits of lifecycle and retrospection time.


<span id="2da87d9a"></span>
# Feature overview

<span id="4b2af870"></span>
## Task management

This product provides users with flexible task scheduling dependency configuration features. Scheduling dependencies typically refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development processes. By configuring dependencies between nodes, tasks are scheduled so that upstream and downstream nodes run in sequence—that is, downstream nodes will only start running after upstream nodes have successfully executed, ensuring timely output of valid business data. The dependency configuration of this product offers two main approaches: automatic detection of upstream data output and custom dependency configuration.

**If an enterprise already has a scheduling platform for relevant data development or data processing tasks, and it can be configured according to this product's API specifications, integration and linkage with this product can be achieved to establish task status dependencies for the scheduling platform.**  **If the enterprise chooses to configure dependencies using third\-party APIs, the user must first configure the API in the task management module under system management**(**which is the content introduced in this section**) **, and then complete the dependency configuration for task scheduling in the visual modeling and dataset dependency configuration modules.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c134af8feeb54dad9f965ee7240205d1~tplv-goo7wpa0wc-image.image) </span>

The specific operation process is as follows:


1. **Complete API configuration**

   Click Create API task dependency to enter the API configuration form. Depending on the interfaces of the data source, multiple API dependencies can be configured.

   1. **Prerequisite operations**

      Please complete the following required information:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b79a31f76f3458b8c24ff08434707f4~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  * Data source type: Controls the data source for which the API dependency is effective; that is, the dependency interface can be called when using the selected data source.
  * Dependency name: Used to understand the dependency name for system integration.
  * Effective scope: Controls the project space for API dependencies. You can select all projects or a single project from the dropdown menu.
  * Dependency description: Used to provide descriptive information for understanding or entering the dependency configuration.
```



2. **API configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ef2890e978e49d488a7d7de3be9694c~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  Configuration 1: URL
  The Key and Value in Params are automatically concatenated into the custom URL. The description section contains a sample URL.
  Configuration 2: Params
  * Request parameter description:
     The Key and Value in Params are automatically concatenated into the custom URL. The Key name can be customized, and the Value parameter format remains unchanged. The system can automatically pass specific task parameters based on the parameter content. You can choose to use these parameters as needed.
  * System parameter Params:
     
     | | | \
     |Parameters |Remarks |
     |---|---|
     | | | \
     |${dataSourceType} |Data source type, such as Hive-jdbc, Maxcompute, and more |
     | | | \
     |${dbName} |The database name of the data source in the task |
     | | | \
     |${tableName} |The table name of the data source in the task |
     | | | \
     |${taskTime} |Business date, that is, the specific date when the task is executed. Typically, the business date is consistent with the partition date. |
     | | | \
     |${partition} |The partition value of the data source in the task |
     | | | \
     |${batchNum} |Task batch number, defined jointly by the business date (taskTime) and execution frequency. For daily granularity, the batch number is always 1. For hourly granularity, batch numbers from 1 to 24 are generated in sequence based on execution order. |

  * Custom parameters
     **Note: When adding custom parameters, please enter the parameter when configuring the dependency.**
     If the user's data scheduling platform cannot locate a specific instance based on the system fields provided by this product, you can choose to add a custom parameter field, such as defining a task ID. Please enter the specific task ID or name when configuring the dependency so that the dependency interface can locate the target parameter field.
```



3. **Successful interface return structure**

   When the API interface call is successful, please define the structure for a successful return: JSON structure returns {"status":"success"} or {'status':0}.

4. **Testing and saving**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58f21a06965148f2a95ad2e11343b139~tplv-goo7wpa0wc-image.image) </span>

**Test button**

**Note:**  Click Test. The API dependency can only be saved after the connectivity test passes. This test button only tests the interface call and does not check the content. You can enter any content for testing.


* Click to first check whether the configuration items are complete. If incomplete, the form will highlight and prompt for completion.

* The test button is available when highlighted. Click to open the test popup for testing.

* Different test popups and input methods are displayed based on the dependency method. The parameter format for the test date is fixed.

* After passing the test, a success icon is displayed. If information changes, you need to click Test again.

   **Save button**

* If Test has not been clicked or the test fails, the Save button is unavailable.

* After testing: The save button works. After saving, the page returns to the display page.

   **Cancel button**

   Click Cancel. A secondary confirmation dialog appears: After cancellation, configuration or modification information will not be saved. Confirm cancellation.

3. **Subsequent operations**

   Once you have completed the API configuration for your own scheduling system, you can select the configured dependency interface in the dependency configuration of modules such as visual modeling and datasets. The specific steps are as follows:

   * When performing data output in visual modeling, you can configure dependencies. See [Data Output](https://docs.byteplus.com/docs/dataagent/Data_Output_).

      Operation path: Data preparation—Visual modeling—Edit—Output—Dependency configuration

   * In the synchronization settings of the dataset, you can configure dependencies. See [Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Setting).

      Operation path: Data preparation—Dataset—Edit—Synchronization settings—Dependency configuration


<span id="c1e29d6b"></span>
## Data connection

<span id="cc19193a"></span>
### Type configuration

To enhance enterprise data security and achieve rigorous and flexible data management, the product supports differentiated configuration for data connection types. For example: Project administrators are allowed to use all data connection types, while some data connection types are not available to other users.

**Operation steps:** 


1. Select Data connection from the left operation bar and click Edit.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acfb2524fc6a42f18ebf9677ff2ecac3~tplv-goo7wpa0wc-image.image) </span>


2. Select the scope of effectiveness as All projects or Distinguish by project. If distinguishing by project, you can create a custom rule and select specific projects.

3. Check "Differentiated rule" as "Yes", select the rule type, and click the edit icon.

4. Select the data connection types to be displayed, click Confirm, and complete the configuration.


<span id="f73d927b"></span>
### System configuration \- Meego data connection configuration

Meego data connection requires unified configuration of plugin credentials. Only after verification will the current environment support Meego data connection types. Before connecting to a Meego data source, please configure it in System settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82ba25816660428ba3be46794e445602~tplv-goo7wpa0wc-image.image) </span>

**Operation steps**:

Open Data connection \- System configuration, click Edit, enter the plugin ID and plugin password, and click Test connection. After the test is successful, click Save to connect to the Meego data source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc3ad079435d40b18f4ab4e179f1093b~tplv-goo7wpa0wc-image.image) </span>

**How to obtain the plugin ID and password**:

After enabling the Lark office platform in DataAgent, the user needs to create and publish a plugin in Meego, then obtain the ID and password on the plugin information page.


1. **Enable the Lark office platform**

   * Go to the **System Configuration** page and enable the Lark office platform.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc03824331ba40449cd9ea3a4c3af870~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  Configure the relevant parameters:
```



* The user needs to bind their Lark account.

* Add a sending channel.

* Configure the relevant parameters

2. **Create a Meego plugin**

   * Go to [Meego](https://project.feishu.cn/), click **Space Configuration \-\> Plugin Management \-\> Add Plugin**, then on the page, click **Create Plugin** in the upper right corner.

   * Click **Add Plugin** on the page, enter the plugin name, and click Confirm.

   * After creation, go to the plugin configuration page and first fill in the basic configuration information.

   * Go to Permission Management and obtain the permissions listed below.

3. **Publish the plugin**

   * For the plugin usage scope, select "Use within the company", and for the installable space scope, select "All spaces".

   * Return to **Space Configuration \- Plugin Management** and add the plugin you just created.

   * After successful publication, return to the plugin basic information page, copy the Plugin ID and Plugin Secret to obtain the plugin ID and password.


<span id="a6a887b7"></span>
### System configuration \- third\-party data connection

Third\-party data connections must be enabled through a unified switch. After enabling, the current environment supports third\-party data connection types such as WeChat Official Account, Ocean Engine, Calendar, and more. If the third\-party data connection switch is not enabled in the system settings, users will not see that the system supports third\-party data connections on the new data connection page of any project.

Operation steps: Open Data Connection \- System Configuration \- Third\-Party Data Connection, click "Enable", and save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/506adb92333c46308b5bfe2289e705cd~tplv-goo7wpa0wc-image.image) </span>

<span id="78b2342c"></span>
## Queue configuration

In System Management, click the System Configuration button, select the Queue Configuration module in the left sidebar to manage queues.

<span id="67e8bce9"></span>
## Storage management

When creating a new project, the system administrator can allocate specified storage resources to each project according to the settings. In the storage management interface, you can view resource overview information and configure storage policies, including the switch for enabling resource control, project resource limit configuration, and configuration for when resources exceed limits. Additionally, you can view and search usage details and many other details. The total amount of storage resources is generated or changed during deployment or upgrade. To adjust it, please contact the system administrator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3548017f2a104debb64c9ad9d5c6b2df~tplv-goo7wpa0wc-image.image) </span>

Administrators can set the default upper limit for project resources. Administrators can uniformly set project resource limits for all projects in Storage Policy \> Enable Resource Control, or set limits for a specific project in Usage Details. When project resources exceed the limit, creating new extraction tasks will be prohibited.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4680be9eae8b4beeafeb9527d55e90e6~tplv-goo7wpa0wc-image.image) </span>

<span id="1afaf470"></span>
## Synchronization configuration

System administrators can set the upper limit for data lifecycle and rollback period in synchronization configuration to proactively restrict user behavior, reduce resource waste caused by human error, and avoid blocking operational resources and unnecessary overhead.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ae5348632064792b0f0828655cb2e76~tplv-goo7wpa0wc-image.image) </span>
