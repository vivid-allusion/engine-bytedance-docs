---
title: "Data Operation and Maintenance Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Operation_and_Maintenance_Configuration"
---

Data operations and maintenance consists of five modules: task management, data connection, queue configuration, storage management, and synchronization configuration. This article introduces the operational procedures for each functional module of data operations and maintenance configuration.

<span id="72703c2f"></span>
# Functional overview

The data operations and maintenance configuration module is available in system management. Administrators can systematically manage multiple aspects, including task management, data connection, queue configuration, storage management, and synchronization configuration:


* Task management: In task management, administrators can establish dependency relationships for task execution statuses on third\-party platforms by creating HTTP APIs, ensuring the timely production of valid business data.

* Data connection: In data connection, administrators can configure different types of data connections for different projects. For example, in different projects, users can select different types of data connections; administrators and non\-administrators can also select different types of data connections.

* Queue configuration: Configure different queues for scheduled tasks and data backtracking tasks to reduce the impact of data backtracking on routine tasks.

* Storage management: View resource overview information and configure storage strategies, including enabling resource control switches, configuring project resource limits, and configuring resource over\-limit settings.

* Synchronization configuration: Set the upper limit for lifecycle and backtracking time.


<span id="8f52472c"></span>
# Common usage scenarios

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b25c607b3804c3a92c9f1dc815bc49c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>



* Enterprises hope to use third\-party APIs to configure dependency relationships, so that tasks are scheduled in an orderly manner based on node dependencies; that is, downstream nodes will only start running after upstream nodes have successfully run.

* In some projects, project administrators are allowed to use all types of data connections, while other users are not granted access to certain types of data connections.

* Managers within the company often need to review long\-term data, or planning and operations personnel frequently compare data from different stages, requiring frequent dataset retrospection.

* To avoid blocking operational resources and unnecessary overhead, the upper limits of lifecycle and retrospection time can be adjusted.


<span id="184b3541"></span>
# Feature overview

<span id="00b4d403"></span>
## Task management

This product provides users with flexible task scheduling dependency configuration capabilities. Scheduling dependencies typically refer to the upstream and downstream dependencies between periodic scheduling nodes during data synchronization or data development processes. By orchestrating task execution for upstream and downstream nodes based on their dependencies, downstream nodes will only start running after upstream nodes have successfully completed, ensuring the timely production of valid business data. The dependency configuration of this product offers two main approaches: automatic detection of upstream data output and custom dependency configuration.

**If a company already has a scheduling platform for relevant data development or data processing tasks, and it can be configured according to this product's API specifications, integration and linkage with this product can be achieved to establish task status dependencies for that scheduling platform.**  **If the company chooses to configure dependencies using a third\-party API, users must first perform API configuration in the task management module under system management**（**that is, the content introduced in this section**） **, and then complete the dependency configuration for task scheduling in the visual modeling and dataset dependency configuration modules.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dd73c3fb6ae4dc98c7f257ed2602333~tplv-goo7wpa0wc-image.image) </span>

The specific procedure is as follows:


1. **Complete API configuration**

   Click "New API Task Dependency" to enter the API configuration form. Depending on the interfaces provided by the data source, multiple API dependencies can be configured.

   1. **Prerequisites**

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a35ec4393c4469beff4baa0d033782~tplv-goo7wpa0wc-image.image" width="2940px" />      </div>
      

      Please provide the following required information:

      * Data source type: Specifies the data source for which the API dependency is effective. The dependency interface can be called when using the selected data source.

      * Dependency name: The dependency name used to understand system integration.

      * Scope of effect: Controls the project space for API dependencies. You can select all projects or a single project from the dropdown menu.

      * Dependency description: Descriptive information used to understand or fill in the dependency configuration.

   2. **API configuration**

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfd8fd7c1c1b4008a62214e91bf7f299~tplv-goo7wpa0wc-image.image" width="2940px" />      </div>
      

      Configuration 1: URL

      The Key and Value in Params are automatically appended to the custom URL. The description section contains a sample URL.

      Configuration 2: Params

      * Request parameter description:

         The Key and Value in Params are automatically appended to the custom URL. The Key name can be customized, and the Value parameter format remains unchanged. The system can automatically pass in specific task parameters based on the parameter content. You can choose to use them as needed.

      * System parameter Params:

         
         |Parameters |Remarks |
         |---|---|
         |$ |Data source type, such as Hive\-jdbc, Maxcompute |
         |$ |The database name of the data source in the task |
         |$ |The table name of the data source in the task |
         |$ |Business date, that is, the specific date when the task is executed. In most cases, the business date is consistent with the partition date. |
         |$ |The partition value of the data source in the task |
         |$ |The task batch number, which is defined by both the business date (taskTime) and execution frequency. For daily granularity, the batch number is always 1. For hourly granularity, 1 to 24 batch numbers are generated sequentially according to the execution order. |
         

      * Custom parameters

         **Note: When adding a custom parameter, please enter this parameter when configuring the dependency.** 

         If the user's data scheduling platform cannot locate a specific instance using the system fields provided by this product, you can choose to add a custom parameter field, such as defining a task ID. Please enter the specific task ID or name when configuring the dependency, so that the dependency interface can locate the target parameter field.

   3. **Successful interface return structure**

      When the API interface call is successful, please define the structure of a successful response: The JSON structure returns {"status":"success"} or {'status':0}.

2. **Testing and saving**

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68fb44fcf3d847739876fd2bddd45e1b~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   **Test button**

   **Note:**  The API dependency can be saved only after the test passes connectivity. This test button only tests the interface call and does not check the content. You can enter any content for testing.

   * Clicking [Test] first checks whether the configuration items are complete. If not, the form will highlight prompts to complete the configuration.

   * The test button is available when highlighted. Click to open the test dialog for testing.

   * Different test dialogs and input methods are displayed based on the dependency method. The parameter format for the test date is fixed.

   * After the test passes, a success icon is displayed. If information is changed, you need to click Test again.

      **Save button**

   * If Test is not clicked or the test fails, the Save button is unavailable.

   * After testing: The Save button works. After saving, the page returns to the view page.

      **Cancel button**

      Click Cancel. A secondary confirmation dialog will appear: After cancellation, configuration or changes made will not be saved. Confirm cancellation.

3. **Subsequent actions**

   After completing the API configuration for your own scheduling system, you can select the configured dependencies in the dependency configuration of modules such as visual modeling and datasets. The specific steps are as follows:

   * When performing data output in visual modeling, you can configure dependencies. For details, see [2.2 Dependency configuration](https://docs.byteplus.com/docs/DataWind/109994#_2-2-%E4%BE%9D%E8%B5%96%E9%85%8D%E7%BD%AE).

   * In the synchronization settings of the dataset, you can configure dependencies. For details, see [Dependency configuration](https://docs.byteplus.com/docs/DataWind/110023#_3-1-4-%E4%BE%9D%E8%B5%96%E9%85%8D%E7%BD%AE).

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f83d289b4a534342bf12b7ce8adbc927~tplv-goo7wpa0wc-image.image" width="2940px" />      </div>
      


<span id="43214fdd"></span>
## Data connection

<span id="e7edd67e"></span>
### Type configuration

To enhance enterprise data security and achieve rigorous and flexible data management, the product allows differentiated configuration of data connection types. For example, project administrators can use all data connection types, while some data connection types are not available to other users.

**Operation steps:** 


1. In the left operation bar, select Data Connection and click Edit.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d29fb12ad97420eaedcbc0eeb661456~tplv-goo7wpa0wc-image.image) </span>

2. Select the applicable scope as All Projects or by project. If distinguishing by project, you can create a custom rule and select specific projects.

3. Set "Differentiated Rule" to "Yes", choose the rule type, and click the edit icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b8c35b742cb45009d4df65543c23835~tplv-goo7wpa0wc-image.image) </span>

4. Select the required data connection types, click OK, and complete the configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b85693f567144e7aa19ae5c75fb6d5b~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   


<span id="900ec8f5"></span>
### System configuration \- Meego data connection configuration

Meego data connections require plugin credentials to be configured centrally. Only after verification is successful does the current environment support the Meego data connection type. Before connecting to a Meego data source, please configure the settings in System Settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bda9224b319499b9d905cc9a180afb1~tplv-goo7wpa0wc-image.image) </span>

**Operation steps**:

Open Data Connection \- System Configuration, click Edit, enter the Plugin ID and Plugin Password, and click Test Connection. Once the test is successful, click Save to connect to the Meego data source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9e05d3f73a84850aa3b145bb3e40cb5~tplv-goo7wpa0wc-image.image) </span>

**How to obtain the plugin ID and password**

After enabling the Lark office platform in DataWind, the user needs to create and publish a plugin in Meego, and then obtain the ID and password on the plugin information page.


1. **Enable the Lark office platform**

   * Go to the **System Configuration** page and enable the Lark office platform.

   * The user needs to bind their Lark account.

   * Add a sending channel.

2. **Create a Meego plugin**

   * Go to [Meego](https://project.feishu.cn/), click **Space Configuration \-\> Plugin Management \-\> Add Plugin**, and on the page, click **Create Plugin.**  in the upper right corner.

   * Click **Add Plugin** on the page, enter the plugin name, and click Confirm.

   * After creation, go to the plugin configuration page and first fill in the basic configuration information.

   * Go to Permission Management and obtain the permissions listed below.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a36d887edf874476a115ef00bf1ba3e8~tplv-goo7wpa0wc-image.image" width="330px" /></div>



3. **Publish the plugin**

   * For the plugin usage scope, select "Use within the enterprise"; for the installable space scope, select "All spaces".

   * Return to **Space Configuration \-\> Plugin Management** and add the plugin you just created.

   * After publishing successfully, return to the plugin basic information page and copy the Plugin ID and Plugin Secret, which are the plugin ID and password.


<span id="57cfb9fe"></span>
### System configuration \- third\-party data connections

Third\-party data connections must be enabled through a unified switch. After enabling, the current environment supports third\-party data connection types such as WeChat Official Account, Juliang Qianchuan, and Calendar. If the third\-party data connection switch is not enabled in system settings, users will not be able to see that the system supports third\-party data connections on the new data connection page of any project. (Applicable for self\-hosted deployments of version v2.74.0 and above)

**Operation steps**: Open Data Connection \- System Configuration \- Third\-Party Data Connection, click "Enable", and save.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07b4d234033b48aa885886d705259efc~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="775652a8"></span>
## Queue configuration

In System Management, click the System Configuration button, and select the Queue Configuration module from the left sidebar to manage queues. For a complete introduction, please refer to [Queue Configuration](https://docs.byteplus.com/docs/DataWind/109964).

<span id="efc5d424"></span>
## Storage management

When creating a new project, the system administrator can allocate specified storage resources to each project according to the settings. In the storage management interface, you can view resource overview information and configure storage policies, including the switch for enabling resource control, project resource limit configuration, and configuration for handling exceeded resource limits. In addition, you can also view and search usage details and other related information. The total amount of storage resources is generated or changed during deployment or upgrade. To make adjustments, contact the system administrator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cc7d3855d7e48d49bd7a2ecda99ab05~tplv-goo7wpa0wc-image.image) </span>

Administrators can set the default upper limit for project resources. Administrators can set unified project resource limits for all projects in Storage Policy \- Enable Resource Control, or set limits for individual projects in Usage Details. When project resources exceed the limit, creating new extraction tasks will be prohibited.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f05c3fdf69f419ebea67b83500c0419~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7736ee66aa074dd5930526ff32c9a8c7~tplv-goo7wpa0wc-image.image" width="2434px" /></div>


<span id="f0621fb5"></span>
## Synchronization configuration

System administrators can set the upper limits for data lifecycle and rollback time in Synchronization Configuration to preemptively restrict user behavior, reduce resource waste caused by human error, and avoid blocking operational resources and unnecessary overhead.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02fb1a8b6bdc4fb6a16bcaf71c7ba610~tplv-goo7wpa0wc-image.image) </span>
