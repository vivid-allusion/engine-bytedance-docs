---
title: "Create a data transformation task"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/create_a_data_transformation_task"
---

Torch Log Service (TLS) offers a flexible and convenient data transformation feature. It allows you to cleanse and filter the collected log data, mask content, split data, and distribute data. After a data transformation task is created, TLS automatically reads data from your source topic, transforms it according to a specified transformation rule, and writes it to different topics. This topic describes how to create a data transformation task in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Make sure the log data is collected. For more information on the procedure, refer to [Getting Started Overview](https://docs.byteplus.com/en/docs/tls/getting_started_overview).

* Make sure the source topic and the target topic are in the same Region. You cannot transform log data across regions.

* Before you create a data transformation task, refer to [Data transformation overview](https://docs.byteplus.com/en/docs/tls/data_transformation_overview) to know the description of and the limits to the feature.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Data transformation**.

4. Click **Create Data transformation task.** 

5. Specify the basic configuration for your data transformation task.

   1. Complete the basic configuration according to the following description, then click **Next step: Processing rule configuration**.

      
      |Parameter |Description |
      |---|---|
      |Task name |The name of the data transformation task. |
      |Description |The brief description of the data transformation task. |
      |Source project |The project where the log data to be transformed is located. |
      |Source topic |The topic where the log data to be transformed is located. |
      |Target topic |Information on the output targets. The targets mean the topics that store the transformed log data. You can specify up to 20 different topics. When you specify multiple topics, the system stores the data transformation results in multiple topics. Log Service supports both intra\-account and inter\-account processing. Each output target requires the following information:<br><br><br>* This account<br><br>   * Shipping type: Select **This account**.<br><br>   * Target name: Customize the name of the output target. Use the name to specify the output target in your data transformation rule.<br><br>   * Project: Specify the project where the transformed log data is located.<br><br>   * Topic: Specify the topic where the transformed log data is stored.<br><br>* Other accounts<br><br>   * Shipping type: Select **Other accounts**.<br><br>   * IAM role: When processing data across accounts, you must configure an IAM role. Specifically, enter the TRN of a custom role and authorize the processing task to assume this custom role to process data and then write it to the Log Service in another account.<br><br>      This custom role must have query and write permissions for the target topic. For instructions on creating and authorizing a role, see [Configure cross-account data transformation permissions](https://docs.byteplus.com/en/docs/tls/Authorization-for-transformation-across-accounts).<br><br>   * Target name: Customize the name of the output target. Use the name to specify the output target in your data transformation rule.<br><br>   * Topic ID: The log topic ID where the processed log data is stored.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Set the number of shards in your target topic appropriately based on that of shards in your source topic. Assume that the write traffic of the source log is large and the number of shards in the target topic is small. In this case, the task processing performance of data transformation may be affected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you specify multiple target topics, the data transformation results are written to the first specified topic by default. You can use the e_output function to distribute the processed data to different topics when you edit your transformation rules. For more information, refer to <a href="https://docs.byteplus.com/en/docs/tls/event_processing_functions">e_output function</a>.</div><br> |
      |Processing time frame |The time range of the data to be transformed.<br><br>Note: The value of this parameter specifies a time range within which log data is saved to the TLS server.<br><br><br>* All logs: Transform all the data saved in the specified topic. All historical log data and data constantly written to the topic are included.<br><br>* from certain time: Transform data collected after specified time. The data written subsequently is included. If you do not specify a point in time, all logs are transformed.<br><br>* Specify time range: Transform historical data within a specified time range.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The time range is a left\-closed and right\-open interval.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you do not specify the start time, TLS performs transformation from the earliest log. If you do not specify the end time, TLS constantly transforms written data.</div><br> |
      

   2. Write a transformation rule.

      Type a data transformation rule in the input box according to the prompts on the page. TLS supports various Domain Specific Language (DSL) syntax functions. You can click a function name on the tab for transforming functions to view syntax description and examples. You can also insert specified syntax within one click to quickly write a transformation rule. For more information on a list of supported syntax and functions, refer to [Functions list](https://docs.byteplus.com/en/docs/tls/overview_of_functions).

   3. Test the transformation rule.

      Use the log data in your source topic or the specified test data for testing according to the prompts on the page.

      * If the page prompts **DSL code compilation check failed**, the transformation statements are incorrect. Fix the syntax issue in a specified line by referring to the error message on the page, then test the rule again.

      * If the data transformation results are correct, click **Complete task**.

   4. In the pop\-up **task open immediately after creation** dialog box, choose whether to start the task immediately.

      * **Immediately enable**: Start the data transformation task immediately after completing the task configuration.

      * **Enter the suspended state** : After completing the configuration, the data transformation task is suspended, and the task needs to be started manually.

      * **Cancel** : Cancel the creation of a data transformation task.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Whether the data transformation task is stopped or complete, TLS does not delete the consumer group instances on which the task depends. We recommend that you clear the stopped and complete data transformation tasks and confirm the data transformation tasks that you no longer use in a timely manner. This way, you can reduce invalid consumer group instances.      </div>
      

<span id=".55u45YWz5pON5L2c"></span>
## Related operations


* After the data transformation task starts running, TLS records the execution status and progress of the task in a service log. You can view and analyze the relevant log data in the corresponding topic. For more information, refer to [Service log fields](https://docs.byteplus.com/en/docs/tls/service_log_fields).

* After a data transformation task is successfully created, you can modify or delete the task based on your business requirements. For more information, refer to [Manage data transformation tasks](https://docs.byteplus.com/en/docs/tls/manage_data_transformation_tasks)

* We recommend that you enable indexes for your target topic to help you query and analyze the processed data. For more information on the procedure, refer to [Configure indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).
