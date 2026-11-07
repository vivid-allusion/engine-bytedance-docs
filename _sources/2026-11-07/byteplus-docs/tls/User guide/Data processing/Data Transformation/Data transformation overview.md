---
title: "Data transformation overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_transformation_overview"
---

Torch Log Service (TLS) offers a flexible and convenient data transformation feature. It allows you to cleanse and filter the collected log data, mask content, split data, and distribute data. This topic describes data transformation in multiple aspects, such as capabilities, limits, and how it works.

<span id="功能概述"></span>
## Feature overview

In scenarios such as big data and stream computing, it is often necessary to process various logs into structured data. For example, standardizing log content is required, such as performing field content extraction and format conversion on logs with chaotic formats. Besides, distributing logs to multiple downstream data processing systems for storage or computing is also required so that different business systems can use the logs. TLS supports a real\-time data transformation service that allows you to cleanse and filter log data, mask content, and split and distribute data. After you create a data transformation task, TLS creates a consumer group to extract log data in the source topic, then processes the log data one by one according to the specified transformation rules and Domain Specific Language (DSL) transformation function. After the data is transformed, TLS writes the data to the specified topic for subsequent log statistical analysis and data dump.

The data transformation feature supports multiple built\-in DSL transformation functions to meet multiple requirements such as data structuring and cleansing as well as data masking in various complex scenarios. For more information on supported transformation syntax, refer to [Data transformation syntax](https://docs.byteplus.com/docs/tls/data_transformation_syntax).

In addition, TLS supports the service log feature for data transformation, which allows you to view information such as the progress and running rate of a data transformation task. For more information, refer to [Service log fields](https://docs.byteplus.com/docs/tls/service_log_fields).

<span id="应用场景"></span>
## Use scenarios

The data transformation feature supports data processing capabilities in the following scenarios:


* Structuring: For log data that cannot be structured during log collection, you can collect it to the server, then perform complex structuring operations on it through the data transformation feature for subsequent SQL statistical analysis. Complex structuring operations include field extraction and format conversion. It is suitable for scenarios such as stream processing and data warehouse computing.

* Cleansing and filtering: TLS can filter complex and diverse log data in a unified manner, retaining core information that requires your focus. You can set a short retention period for log data to be filtered, which reduces costs and the volume of stored log data.

* Content masking: TLS can mask sensitive information contained in logs, such as mobile phone numbers, ID card numbers, and passwords in business logs.

* Data splitting and distribution: After unified log transformation, TLS splits a log into multiple pieces of data and outputs the data to different downstream systems respectively.


<span id="费用说明"></span>
## Precautions


* **Data load of units for concurrent operations**: The data load of units for concurrent operations affects the performance of data transformation.

   During a data transformation task, the data load of a single unit for concurrent operations depends on the amount of data stored in the shards of the corresponding source topic. Assume that data traffic is unevenly distributed among multiple shards when TLS writes log data to the source topic. In this case, hot spot units may appear during a data transformation task, causing transformation latency in certain shards.

   If log data in the source topic is written in **HashKey\-based shard\-oriented routing** mode, we recommend that you reasonably allocate write traffic to shards to ensure the data is evenly distributed in the shards. For more information on data write, refer to [PutLogs](https://docs.byteplus.com/docs/tls/api-putlogs).

* TLS writes transformed data to the target topic through the API action PutLogs. The data write rate is related to the number of shards in the target topic.

   When TLS writes the processing results to the target topic, you should meet the data write limits determined by the specification of the topic. If the number of shards in the target topic is small and the amount of data to be written is large, transformation latency may occur. We recommend that you evaluate the number of shards in the target topic based on the amount of data that you want to write to the topic or enable the auto shard splitting feature for the topic. For more information, refer to topics that describe basic resources and data read and write. For more information on how to enable auto shard splitting.

   When an error related to write limits on the target topic occurs during data transformation, TLS performs infinite retries to ensure data integrity. However, the progress of the transformation job is affected, causing latency in transformation on the current source shard.


<span id="使用限制"></span>
## Limits


|Limited Item |Description |
|---|---|
|Number of tasks |A maximum of 100 data transformation tasks can be created in each project, and a maximum of 30 data transformation tasks can be created in each topic. Tasks of all status displayed on the page are included.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Paused and completed tasks consume quota. If you confirm that these tasks are no longer used, we recommend that you clear the task list in a timely manner to reduce quota usage. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/manage_data_transformation_tasks">Managing data transformation tasks</a>.</div><br> |
|Number of target topics |In 1 data transformation task, a maximum of 20 different topics can be configured to store transformed data. |
|Execution preview |The execution preview feature of data transformation is used to debug data transformation code online. Note the following limits:<br><br><br>* Include up to 20 logs or test data entries in a single request. Otherwise, your preview request returns an error.<br><br>* In a single request, at most the first 100 transformation results can be returned. |


<span id="基本概念"></span>
## Terms


|Term |Description |
|---|---|
|ETL |Extract, Transform, and Load (ETL) refers to the process of extracting, converting, and loading data from a source business system to the target system. This process completes data integration, standardization, and unification. TLS can load log data from a specified source topic and output the results of data transformation to a specified target topic. |
|Events, data, and logs |In terms of the data transformation feature, events and data refer to log data. For example, 1 event corresponds to 1 log. The event retention function `e_keep` is used to reserve specific logs. |
|Source topic |In data transformation, a source topic represents the storage location of a log to be transformed. TLS consumes data from a source topic and performs data transformation.<br><br>You can set 1 source topic in 1 transformation task while you can add multiple data transformation tasks to 1 source topic. |
|Target topic |The topic to which transformed data is written is the target topic.<br><br>You can configure up to 20 target topics for 1 transformation task. |
|TLS DSL |TLS DSL is a Python\-like scripting language. TLS DSL is used to specify data processing logic in data transformation. TLS DSL supports more than 40 types of function syntax, thus meeting the requirements for data transformation in big data analysis scenarios and data warehouse\-based processing scenarios. For more information on the list of functions, refer to [Functions list](https://docs.byteplus.com/docs/tls/overview_of_functions). |
|Transformation rules |A transformation rule is the execution script of data transformation and a collection of logic code orchestrated through TLS DSL. |
|Transformation tasks |A transformation task is a unit for scheduling in data transformation. This type of task defines multiple configuration items such as a source topic, target topics, and transformation rules. |
