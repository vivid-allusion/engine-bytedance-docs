---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data_quality_overview"
---

The data quality rules is a data quality management platform for data and its production links, providing a complete set of data quality solutions for the development and use of data.

The data quality rules offers multiple functions, including monitoring fluctuations and triggering alarms for data volume and customized metrics, data profiling, and content comparison, ensuring data reliability and accuracy throughout the production and usage processes to prevent data distrust and decision errors caused by data quality issues.

<span id="_1-使用场景"></span>
## Use Cases

The data quality rules plays an important role in quality assurance throughout the entire data development process, detailed as follows:


* During task development

   Data profiling performs statistical analysis to help assess data quality and confirm data availability.

* During task release

   After task execution completes and partitioned data is generated, monitoring rules trigger quality checks.

* Quality exceptions are detected during the quality check process

   Determine whether to trip downstream tasks to prevent exception spread according to the configured strong and weak properties.

   * If the rule is strong, downstream tasks must wait for successful rule execution before continuing.

   * If the rule is weak, a failure alarm is sent but it does not affect downstream execution.

* Data comparison in the task modification process

   Task modification can use data comparison to evaluate the impact by comparing production and development data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cf006870ae840598e631fc9224c2b8b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
## Function Introduction

Data quality mainly includes four modules: data monitoring, data profiling, data comparison, and quality subscription.


* **Data Monitoring**

   Monitor data based on monitor rules, supporting both batch data monitoring and streaming data monitoring. Among them, batch data monitoring supports various configuration methods, including template rules, custom rules, and dual\-data\-source validation.

* **Data Profiling**

   approve full profiling or dynamic profiling to understand the complete data picture, identify potential issues, and comprehend data distribution.

* **Data Comparison**

   create data comparisons to quantify differences down to the field level between new and old data tables, accurately measure the impact of data changes, and provide references for data owners.

* **Duality Subscription**

   create quality subscriptions to receive daily quality report messages from the alarm bot.
