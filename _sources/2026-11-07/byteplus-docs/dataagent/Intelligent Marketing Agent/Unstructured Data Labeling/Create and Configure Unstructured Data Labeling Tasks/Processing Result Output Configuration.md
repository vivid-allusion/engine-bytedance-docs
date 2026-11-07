---
title: "Processing Result Output Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Processing_Result_Output_Configuration"
---

Data output refers to the process of data output and storage in the process of creating a visual modeling task. The current support is to output the marking results as VeCDP's dataset or VeCDP's label. Output as a dataset means that after completing the data input\-data processing, the task result needs to be saved in the form of a dataset for subsequent visualized query and display; Output as a label means that the data is output to the label system, and allows users to customize the data processing flow, and finally integrate the processing results into the label system. This article shows you how to configure the output of processed results.

<span id="a19ba20d"></span>
# Prerequisite


* [Data Preparation](https://docs.byteplus.com/docs/dataagent/Data_Preparation)

* [Task Creation](https://docs.byteplus.com/docs/dataagent/Task_Creation_)

* [Unstructured Data Processing Operators Configuration](https://docs.byteplus.com/docs/dataagent/Unstructured_Data_Processing_Operators_Configuration)


<span id="7f010f19"></span>
# Output as a Dataset

If the extraction results are used for analysis, the data can be output to the dataset, and output to Hive/ByteHouse is supported.


1. In the Visual Modeling Edit screen, click the Add Operator button, and in Output Type, click Select **Output \- Output** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c96cda7bfc134d01b93f0ab31109aa7c~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca052d2d7f0f4c1eb92fca7675ef6340~tplv-goo7wpa0wc-image.image) </span>

2. Configure the relevant parameters on the configuration page of the output dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52ac0092432e4e91a7fbe176ad5a3854~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |explain |
   |---|---|
   |Name/Description |Custom name and description. |
   |Open project |Configure to open a dataset to other projects, allowing dataset administrators to use it as a data source in visual modeling tasks for other projects. |
   |CDP application |Support CDP application marking, define the application scenarios of the dataset while outputting the dataset, automatically match different storage logic based on different scenarios, automatically constrain the format, and avoid repeated data extraction.<br><br>Note: Due to the special query logic in some applications downstream of CDP, please select the appropriate application scenario as needed.<br><br><br>* Common dataset: without special restrictions, it can be used as a data source to repeatedly participate in production processing in visual modeling, but it is impossible to register data archives or configure IDM.<br><br>* IDMapping graph configuration: used to configure IDMapping graph, only supports output Hive datasets, and generally requires partitioning to store the full amount of data every day.<br><br>* Data Archive \- Business Details/Behavioral Event Archive: Used to register details/behavioral data archives, this type of data set requires the main benchmark OneID field, and the system will automatically store the OneID field as a sharding key and cannot be changed. IDM operators can be added to the canvas process in advance to generate a benchmark ID (OneID) field, which generally requires partitioning and storing incremental data every day.<br><br>* Data Archive \- Subject Attribute Archive: A data archive used to register subject attributes. This type of data set requires the subject benchmark OneID field, and the system will automatically deduplicate according to the OneID field to ensure that the attribute value is unique. IDM operators can be added in the canvas process in advance to generate the benchmark ID (OneID) field. Generally, the full amount of data is required to be stored every day.<br><br>* Data Archive \- Business Dimension Archive: For registering business dimension data archives, the dimension primary key field is required for this type of dataset, and the system will store the full amount of data in each sharding node (server) and deduplicate the primary key field. It cannot be directly used in any other module of CDP. Generally, the partition is required to store the full amount of data every day.<br><br>* Data file \- session file: used to register session files, this type of data set requires a session id field, usually an incremental partition table. |
   |Type |You can choose ByteHouse or Hive.<br><br><br>* Hive: Requires data lifecycle (required) and partitioning (optional).<br><br>* ByteHouse: You need to select the cluster, sort key, sample field, table type, data lifecycle, and partition. |
   |Data lifecycle |The number of valid retention days extracted to the data in the system storage, the non\-partitioned table retains the data according to the data update time, and the date partition retains the data according to the partition date. The data outside the lifecycle is automatically cleared at 0 o'clock every day, and the default value is 7 days. |
   |Partition |Optional date or other values can be enumerated as a partition, the first\-level partition must be of type date, if there is no suitable field, you can choose "system default partition" (the value of the day, week, month level routine synchronization tasks is the day before the routine execution of the task, the value of the hour and minute level routine synchronization tasks is the day of the routine execution of the task, and the value of the manually run task is the business time selected at runtime), the second\-level partition can be selected as hours or other values can be enumerated as a partition (dynamic partitioning must be turned on in the advanced settings). |
   |Cluster |Select the cluster where the dataset is stored. |
   |Sort key |Setting the field that is most often used as a filter to the sort key makes the query faster. You can set multiple fields as sorting keys, with the first field having the greatest effect, and the rest decreasing in turn. It is recommended that there be no more than three. You cannot use a partition field as a sort key. |
   |Sample field |In the visualized query module, you can sample and query according to this field, and only fields of type int, float, and string are supported. |
   |Table type |You can choose a normal table or a bucketing table. A normal table is a conventional form of data storage, with a relatively simple and straightforward structure. The bucketing table divides data into different buckets according to specific rules to improve query performance. |
   

3. Dependency configuration: Data source dependency Through dependency configuration, it can be combined with the readiness status of upstream data to determine and start timing synchronization tasks. In the **dependency configuration**, for Hive and Bytehouse data sources, the system can automatically obtain the dependency information of the upstream configuration and display it. To modify or customize configuration dependencies, you can choose **a custom configuration**. For details, see [Dataset Output](https://docs.byteplus.com/docs/dataagent/Dataset_Output).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc97abb7532c4740a90e2a7f9d25696c~tplv-goo7wpa0wc-image.image) </span>

   Supports detection of dependencies on common data sources (Hive JDBC, Maxcompute). Fill in the dependency table, partition information, and dependency type. You can choose a reasonable dependence method according to the situation of the data table in the current task logic, and the system recommends [**task dependence \> system custom dependence \> data source partition detection dependence**] by default:

   * Task dependence: Establishes dependencies based on visual modeling of the output data table or dataset task state.

   * Data source partitioning detects dependencies: Establishes dependencies based on the partitioned data output of the data source.

   * System custom dependencies: create dependencies through system admin by creating dependency APIs, which are usually used to establish dependencies for tasks related to third\-party data platforms. The logic of the API is defined by system admin. For details, please consult system admin.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For non\-partitioned tables, the system is temporarily unable to recommend dependency system custom dependencies and data source partition probe dependencies.   </div>
   

4. Advanced configuration

   The dataset of the HIVE data source needs to select the run queue and the run priority in the queue. Select a queue, and the corresponding HIVE query will be executed on the specified queue before importing the dataset. Queue selection affects dataset synchronization time, but does not affect visualized query performance.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/969a7e68e9274275b966a4ceae73ee45~tplv-goo7wpa0wc-image.image) </span>

   Operating parameters: Support setting the operating parameters of dataset synchronization according to requirements to ensure successful synchronization or synchronization performance.


<span id="be57ac31"></span>
# Output as Label

If the extraction result needs to be used for the circle group, it can be output as a label. The data is exported to the labeling system, allowing users to customize the data processing flow, and finally the processing results are integrated into the labeling system.


1. In the visual modeling editing interface, click the Add operator button, and in Output Type, click Select **Output \- Output tab**.

2. Configure the relevant parameters on the configuration page of the output tag.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff899852c1df48adacc27349fbccd10c~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |parameter description |
   |---|---|
   |Subject |Select the principal configured in VeCDP, the target object for ID\-Mapping OneID |
   |Source ID type |The ID Code of a certain type of ID of the subject in the ID\-Mapping graph |
   |Corresponding field |Select the field in the data source corresponding to the ID\-Mapping source ID type as the data input |
   |Tag Configuration |After the label is submitted, the relevant label will be automatically built in the label system, and it will really take effect after saving the task. |
   |Label field |Select the field name that needs to be defined as a label, and special type fields such as Map are not supported for the time being. |
   |Label name |Define the label's understandable name, Chinese or English |
   |Label description |Define the descriptive information that the label can understand |
   |Online service |After opening, the tag can query relevant data in high\-speed OpenAPI to achieve high concurrency queries |
   |Advanced Configuration |Reasonable configuration of operating parameters can help improve the efficiency of the task, and the advanced parameters are only valid when there is a "data cleaning" operator in the front node or the output data set configuration "CDP reference ID field". |
   

3. ### Dependency configuration   <span id="dependency-configuration"></span>

   Data source dependency Through dependency configuration, timing synchronization tasks can be determined and initiated in combination with the readiness status of upstream data. In the **dependency configuration** , for Hive and Bytehouse data sources, the system can automatically obtain the dependency information of the upstream configuration and display it. To modify or customize configuration dependencies, you can choose **a custom configuration** . For details, see the [output label ](https://www.volcengine.com/docs/6356/1222756?lang=zh).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37d022323d9c40db82575952e52ff9d6~tplv-goo7wpa0wc-image.image) </span>

4. Advanced configuration.

   The dataset of the HIVE data source needs to select the run queue and the run priority in the queue. Select a queue, and the corresponding HIVE query will be executed on the specified queue before importing the dataset. Queue selection affects dataset synchronization time, but does not affect visualized query performance. Reasonable configuration of operating parameters can help improve the efficiency of the task, and the advanced parameters are only valid when there is a "data cleaning" operator in the front node or the output data set configuration "CDP reference ID field".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36b2b7393ec0451f8b51faddb682be24~tplv-goo7wpa0wc-image.image) </span>


<span id="fee55b00"></span>
# Output to External Storage

The marking result is exported to external storage. The processed data is exported to the data storage outside the system through visual modeling, so as to realize the construction of the output capability of data assets. See [External Output](https://docs.byteplus.com/docs/dataagent/External_Output_) for more information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If output is allowed, consult the owner of the data connection. If the system supports output, the switch can be turned on by contacting a Volcano Engine technician.</div>


Currently supported external storage:


|**data source** |**supported version** |**environment** |
|---|---|---|
|MaxCompute |1.20.2 |Private & SaaS |
|OceanBase Oracle / Mysql |1.20.2 |private department |
|Oracle |1.20.2 |private department |
|BytehouseCE |1.22.2 |Private & SaaS |
|MySQL |1.20.2 |private department |



1. In the visual modeling editing interface, click the Add operator button, and in Output Type, click Select **External Output.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/427e7ddd47e741478f521c5c4f92b890~tplv-goo7wpa0wc-image.image) </span>

2. Select Create a good data connection and fill in the **database & table information**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f692516f6fc4c8692a584272e4742ff~tplv-goo7wpa0wc-image.image) </span>


<span id="8c04e514"></span>
# Execute a Task


1. After the visual modeling task is configured, click **Test Execution,**  view the output in the **Test Execution Results** bar and tune.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e880589f2c46482189185f3a491c8a93~tplv-goo7wpa0wc-image.image) </span>

2. After the task debugging is completed, save the task configuration and click Return in the upper left corner to jump to the task details. Return to the Visual Modeling page and click **Run** of the current task to run it manually.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a48f494743424696b82aec7883e2660a~tplv-goo7wpa0wc-image.image) </span>


<span id="f0a658a0"></span>
# Next Steps

The above visual modeling output tasks are exported to datasets or labeled for BI Kanban analysis. For the analysis of the label and data set results for business logic verification, to ensure that the target expectations, if there is a problem, you can return to the large model application design steps for word optimization and other operations.
