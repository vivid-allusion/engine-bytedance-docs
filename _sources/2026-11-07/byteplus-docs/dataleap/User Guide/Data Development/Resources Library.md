---
title: "Resources Library"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/resources_library"
---

DataLeap supports visual creation of EMR, LAS, Flink, and generic engine resources. These resources can be used to create custom functions or be referenced by tasks such as Shell/Python, enhancing task development efficiency through resource references. This article will introduce you to the operations related to the Resources Library.

<span id="_1-概述"></span>
## 1 Use Cases

During task development, functions are often used. Before creating a function, you need to create resources in the **Data Development \> Task Development \> Resources Library**, bind engines according to the project bound to E\-MapReduce (EMR), Lakehouse analysis service (LAS), Stream Computing Flink Edition (Serverless Flink) or generic (Shell/Python) engines, and upload resource packages. Applicable to the following use scenarios:


* If you need to use resource files such as  **.Jar** in your code or functions, you can reference the uploaded resource files.

* If built\-in functions do not meet your needs, you can also create custom functions through resource packages. Additionally, you can define and create one or more functions based on resource files, referencing them during development for customized logic processing. The same resource can be reused by multiple functions.


<span id="_2-使用前提"></span>
## 2 Usage Restrictions


1. DataLeap products need to bind EMR Serverless Spark and Serverless Flink engines. See [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

2. Under the same engine type, it must not duplicate the name of an already successfully created resource.

3. Except for resources of **Generic** Engine types, other engine resources do not support the **Copy Resource** operation.

4. When using resources in EMR Serverless Spark Java/Python tasks, the current method still adopts direct configuration of TOS paths. Therefore, the resources created by the EMR Serverless Spark/Presto Engine in the resource library only serve for unified management purposes and are not yet supported for direct reference in tasks.


<span id="_3-功能介绍"></span>
## 3 Function Introduction

<span id="_3-1-新建资源"></span>
### 3.1 Create New Resource


1. Enter the **Resources Library** page.

   1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

   2. In the **Overview** interface, where joined projects are displayed, click on **Data Development** to enter the corresponding project.

   3. Click **Resources Library** in the left sidebar to enter.

2. Once inside the Resources Library, you can create new resources in any of the following two ways:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5553b78e2794cd7860ce7f44ce202e1~tplv-goo7wpa0wc-image.image) </span>

   You can also create a **New Subdirectory** folder under the corresponding engine instance to categorize and manage different types of resources.

3. Enter the **New Resource** interface and select the engine parameters you need to bind.

   
   |Parameters |Description |
   |---|---|
   |Related information ||
   |Engine Binding |Supports engine type bindings such as EMR Serverless Spark, EMR Serverless Presto, Serverless Flink, and Generic.<br><br>Among **Generic Engines**, resource types are available for Shell/Python tasks. |
   |Associated instance |Different engines bind to their respective associated instances.<br><br><br>* EMR Serverless Spark/Presto Engine: Default association with the instance at the time of project binding.<br><br>* Serverless Flink Engine: Default association with **Serverless Flink** instance at the time of project binding.<br><br>* Generic engines do not require binding to an engine instance. |
   |Save to |File path after resource upload. |
   |Basic Info ||
   |Resource Name |Enter the resource name, which can only consist of numbers, letters, underscores, hyphens, and periods, and must be within 255 characters.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Under the same engine type, the resource name cannot be duplicated with those that have been successfully created.</div><br> |
   |Description |Enter resource description information for easier management later. |
   |Resource Type |* Serverless Flink Engine type, resources support Jar, File types.<br><br>* Generic Engine types; resources support Jar, File, Zip types.<br><br>* EMR Serverless Spark/Presto Engine Type, only supports Jar resource type upload. |
   |Source of resources |* Stream Computing Flink, and Generic Engines support source methods of **Upload**.<br><br>* The EMR Serverless Spark/Presto Engine only supports resources originating from object storage (TOS) files, and specific TOS file paths need to be filled in below. |
   |Resource file |For resources of Jar, File, and Zip types, it is necessary to upload resource files, which can be done directly through Upload. Add resource files directly:<br><br><br>* Upload:<br><br>   * File names can only consist of numbers, letters, underscores, hyphens, and periods.<br><br>   * It is recommended that individual uploaded files are no larger than 300MB.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">In the same project, the same resource file cannot be uploaded multiple times, as this would result in a resource name already exists situation.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When referencing resources in task code, the resource file name must be used for referencing. For example, if the file name of resource A is <strong>resource.py</strong>, the code should use <code>import resource</code> to import it.</div><br> |
   |TOS document link |For EMR Serverless Spark/Presto Engine, you need to upload JAR resources to the TOS Bucket and fill in the TOS path information where the resources are uploaded, such as tos://bucket_name/spark\-test\-1.9.jar |
   

4. After configuring the parameters, click the **OK** button to successfully create the resource.


<span id="_3-2-查找资源"></span>
### 3.2 Find Resources


1. Enter the Resources Library.

2. In the upper left corner, choose from engine types and instance types such as LAS, EMR, EMR Serverless Spark/Presto, Stream Computing Flink Edition, Generic, etc. For example, if the engine type is EMR, select an associated instance ID like emr\-xxx.

3. In the search input box, type the resource name/owner keywords to search.


<span id="_3-3-查看编辑资源"></span>
### 3.3 View and Edit Resources


1. When you hover the mouse over the resource name: details such as resource type, creator, creation time, and last modified time can be displayed.

2. When you click on the resource name: resource details can be displayed and you may edit parts of the resource configuration information, including the following:

   
   |Editable Parameters |Description |
   |---|---|
   |Resource Description |Editable Resource Description for Easier Future Management. |
   |Owner |Editable Resource Owner. |
   |Resource File |Serverless Flink, Generic Engine Modification:<br><br><br>1. Click the **Delete** button on the right.<br><br>2. Click the **Upload** button to upload a new resource file again.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the Serverless Flink engine, if you delete an old resource file and then re\-upload a resource with the same name, the old resource file in Flink will not actually be deleted.</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, the names of new and old resource files will be incremented according to the sequence identifier, and the old resource file will still be used to execute the task before the task is manually restarted or when the system automatically restarts, which can avoid the failure of historical tasks. However, after the task is resubmitted and manually restarted, the new resource file will be used to execute the task.</div><br><br><br><div data-tips="true" data-tips-type="tip">Under the Flink engine, the versions of new and old resource files used for different tasks can currently be distinguished by checking the names of resource files in the task execution logs.</div><br> |
   |TOS file link |EMR Serverless Spark/Presto Engine can modify TOS file links. |
   


<span id="08f3d309"></span>
### 3.4 Copy Resources

**EMR**, **Generic** engine types support the copy operation, which allows copying of created resources directly to **EMR** or **Generic** engine types, with detailed operating instructions as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Other engines do not currently support copying resource actions.</div>



1. In the resource list, click **Resource Name\>**  on the right **More Actions\>**  click **Copy** button to perform resource copying.

2. In the popup window, you can choose to copy the original resource to a specified EMR or Generic engine, and specify the target resource name, target resource storage directory, and other information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e7c9e57c3724d03baba79b8cefc2394~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-删除资源"></span>
### 3.5 Delete Resources

In the resource list, click **Resource Name\>**  on the right **More Actions\>**  click **Delete,**  in the delete popup click **Delete** button to delete the resource file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the resource has been referenced by a function or a task, there will be a prompt about the dependent function or task; the reference must be removed before deleting the resource.</div>


<span id="_3-5-移动资源"></span>
### 3.6 Move Resources

Click **Resource Name\>**  on the right **More Actions\>**  click **Move**, you can move resources to other directories under the current engine in the current project.

<span id="_3-6-引用记录"></span>
### 3.7 Reference Records

Open resource details, click the right sidebar **Reference Record,**  the list displays details of tasks or functions related to the resource used. You can search for related referenced tasks or functions in the search box based on the task name or owner.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Resources under the EMR Serverless Spark/Presto Engine:</div>



* <div data-tips="true" data-tips-type="tip">Since resources are still used in tasks in the form of configuring TOS paths, there are currently no records related to tasks for EMR Serverless Spark/Presto engine resources.</div>


   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95085c9d1d46473fa2b4149a9267ce36~tplv-goo7wpa0wc-image.image" width="1708px" />   </div>
   

* <div data-tips="true" data-tips-type="tip">Since custom creation of EMR Serverless Spark/Presto engine\-related UDF functions is not supported currently, there are also no function\-related records for resources.</div>


* Reference task: Task ID, Task name, Owner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/329e31e3f86f4a07b2a87dff703e15c4~tplv-goo7wpa0wc-image.image) </span>
