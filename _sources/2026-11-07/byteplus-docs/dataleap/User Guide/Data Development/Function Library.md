---
title: "Function Library"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/function_library"
---

In the process of data development, the actual business often requires referencing functions to meet the computational demands of some scenarios. The platform provides a function library that supports searching, displaying, referencing, and custom creation of functions.

<span id="3702b19f"></span>
## 1 Overview

The Function Library page displays data in two parts: **Public functions** and **UDF**, with details on supported engine types as follows:


|Engine Type |Public Function |Custom Function |
|---|---|---|
|EMR Serverless Spark、EMR Serverless Presto |Supported (Batch) |Supported (Batch) |
|Serverless Flink Edition (Serverless Flink) |Not Supported |Supported (Real\-time) |
|ByteHouse Cloud Data Warehouse Edition |Supported (Offline) |Not supported |



* Public functions: Each engine provides built\-in, ready\-to\-use public functions, covering daily data cleaning, calculation, analysis scenarios, and direct invocation without the need for uploading a custom JAR package.

   * ByteHouse Cloud Data Warehouse Edition Public Functions: [ByteHouse Cloud Data Warehouse Edition Function Documentation](https://www.volcengine.com/docs/6517/102183)

* If the built\-in public functions provided by the engine do not meet your business scenario practice, you can create UDF (User Defined Functions), UDTF (User Defined Table\-Generating Functions), and UDAF (User Defined Aggregate Functions) by uploading resources such as JAR/File/Zip and using custom functions.


<span id="fd8889f6"></span>
## 2 Usage Restrictions


* DataLeap products require the activation of DataOps Development, Big Data Analytics, and Data Development Special Edition or Distributed Data Autonomy services before engines such as EMR and Serverless Flink Edition can be bound.

   For service activation, see [Launch service](https://docs.byteplus.com/docs/dataleap/overview#_1-1-%E5%BC%80%E9%80%9A%E6%9C%8D%E5%8A%A1); for engine binding, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

* Cluster types of ByteHouse Cloud Data Warehouse Edition do not support creating custom functions.

* EMR Serverless Spark and EMR Serverless Presto engines only support creating **batch** functions.

* Serverless Flink Edition only supports creating **streaming** functions.


<span id="_2-使用前提"></span>
## 3 Usage Prerequisites


* To create a custom function, you must first upload resources and then use these resources to create and operate the function. For methods of uploading resources, see details [Resources Library](https://docs.byteplus.com/docs/dataleap/resources_library).

* First, you must select the engine instance by binding it on the DataLeap Project Console through binding actions engine instance. For binding operations, see details [Configure Service Binding Information](https://docs.byteplus.com/docs/dataleap/create_project#54f5e209).


<span id="_3-功能介绍"></span>
## 4 Function Introduction

After uploading the engine\-specific resources to the Resource Library, you can visually create custom functions.

<span id="_3-1-新建函数"></span>
### 4.1 New Custom Function


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Enter a specific data development project and click on **Function Library** in the left navigation bar to access it.

3. In the custom function area, you can create a new function in the following ways:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee39467b372c4eebbf4c81cad8efd879~tplv-goo7wpa0wc-image.image) </span>

   You can also **create a new subdirectory** folder before creating a custom function to categorize and manage different functions by subdirectory.

4. Enter the function library, click  **+**  in the custom function section, and enter the new function creation page to create functions based on different binding engines.

   
   |Parameters |Description |
   |---|---|
   |Related information ||
   |Bind engine & associated instance |Supported selection of LAS, EMR (Hadoop cluster), Serverless Flink Edition, EMR Serverless Spark, EMR Serverless Presto, and automatically relate the engine instances added in the Project Console. Detailed Add operations see [Configure Service Binding Information](https://docs.byteplus.com/docs/dataleap/create_project#54f5e209). |
   |relational database |For the functions of EMR Serverless Spark and EMR Serverless Presto engines, select the already created LAS Catalog database information from the dropdown menu, and it should be associated with the database information. Additionally, when referencing the function, it needs to be called in the form of "Database name.Function name".<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When sub\-users reference a function, they should ensure they have the necessary permissions for the corresponding LAS Catalog database. If there are permission restrictions, you can apply for permissions through the Data Security Platform. See details <a href="https://docs.byteplus.com/docs/dataleap/Apply_Permission">Apply Permission</a>.</div><br> |
   |Save to |Directory where the function is saved. |
   |Basic Info ||
   |Function name |Enter the function name, allowed only with 2\-60 characters consisting of numbers, letters, and underscores, starting with a letter. |
   |Function class name |Define the class name of the function. |
   |Function description |Enter function description content for easy subsequent management. |
   |Function type |* Serverless Flink, EMR Serverless Spark, EMR Serverless Presto engines support UDF (User Defined Function), UDTF (User Defined Table Function), and UDAF (User Defined Aggregate Function) types. You can create as needed. |
   |Resource |Select a custom function you have created from the dropdown list, only Jar resources are supported. See details for creating new resources [Resources Library](https://docs.byteplus.com/docs/dataleap/resources_library). |
   |Input parameters |Description of input parameter types for the function. |
   |Output parameters |Description of output parameter types for the function. |
   |Use case |Example of function usage, to help other users know how to use the function. |
   |Data type |* EMR Serverless Spark, EMR Serverless Presto Engines only support the creation of **batch** functions.<br><br>* Serverless Flink engine only supports the creation of **streaming** functions. |
   

5. After filling in the parameters, click the **OK** button to create the function successfully.

6. You can preview built\-in and newly created function examples in the public or custom function section.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ceec05437d7a4b01b73bf4fd709b3a40~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-查找函数"></span>
### 4.2 Find Functions


1. Enter the **Function Library** page.

2. In the engine selection box, drop\-down to select engine types and instance types such as EMR (Hadoop), EMR Serverless Spark, EMR Serverless Presto, LAS, Serverless Flink Edition, ByteHouse Cloud Data Warehouse Edition, etc., for example, select EMR for engine type and emr\-xxx for instance type.

3. Select **Batch/Real\-time** data types, enter function name keywords for searching, and search results will be displayed categorized as public functions and custom functions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ByteHouse Cloud Data Warehouse Edition and EMR Serverless Spark/Presto Engine types only support viewing Batch Functions type.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e30a5daf63384e249961906535353f8e~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-3-查看引用函数"></span>
### 4.3 Reference Functions


1. Hovering the mouse over the **custom function** name will display function details.

2. Reference Function

   1. First, **task development \> Data development** interface, open the task editor interface.

   2. Switch to **Function Library**, and click the **Reference** function button to the right of the function name to directly insert the reference function statement into the editor. The following takes the Serverless Flink Edition real\-time function reference as an example:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7666dfbfa5914981be2666bcf7440b85~tplv-goo7wpa0wc-image.image) </span>

3. After the task references the function and has been submitted for release to the Operations Center, you can view the reference tasks and reference templates in the **Reference Record** on the right sidebar of the custom function.

   You can see tasks, template details, including Task ID, Task Name, Template Name, and Owner that have used the function. You can search for relevant referenced tasks in the search box by task name, template name, or owner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0f8c2c51d0a47e680af20275567abe9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-编辑函数"></span>
### 4.4 Edit Custom Function

Project members, by clicking the function name in the custom function library list, enter the edit interface where you can modify the configuration information of the custom function.


|Resource Bind Engine Type |Modifiable Parameters |Description |
|---|---|---|
|Serverless Flink, EMR Serverless Spark/Presto |Function Class Name |You can modify the class name of the defined function. |
||Function Description |Modifiable resource description for easy management later. |
||Function Type |* Serverless Flink, EMR Serverless Spark/Presto engines support modifying UDF, UDTF, UDAF types. |
||Resource |Can modify referenced resource files. |
||Input Parameters |Can modify the type description of the function input. |
||Output Parameters |You can modify the parameter type descriptions of the function output. |
||Use case |Supported updates to the use case. |


<span id="_3-5-删除函数"></span>
### 4.5 Delete Function

In the custom function list, click **Function Name \>**  on the right, click **More Actions \>** , then click **Delete**, and in the delete dialog, click the **Delete** button to delete the function.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the function is being used by an active task, the task must be taken offline before deleting the function.</div>


<span id="_3-6-移动函数"></span>
### 4.6 Move Function

Click **Function Name \>**  on the right, click **More Actions \>** , then click **Move**, to move the function to a different directory within the current project and under the current engine.
