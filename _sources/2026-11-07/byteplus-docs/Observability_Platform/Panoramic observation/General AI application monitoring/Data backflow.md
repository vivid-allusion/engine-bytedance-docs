---
title: "Data backflow"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Data_backflow"
---

In distributed system observability scenarios, trace data generated in online environments is key to identifying system performance bottlenecks, abnormal calls, and service dependencies. As capabilities such as intelligent diagnosis, performance analysis, and trace detection rules continue to iterate, large numbers of standardized, high\-quality trace samples are required for evaluation.

By exporting trace data in batches to evaluation sets, you can build a standardized and reusable trace sample library. You can then run evaluation experiments directly using trace samples from the evaluation sets. This supports scenarios such as trace diagnosis algorithm verification, detection rule optimization, anomaly detection evaluation, and fault case accumulation and reproduction. This process forms a closed loop from real online data to evaluation and verification, which improves the accuracy and reliability of diagnostic capabilities on the Observability Platform. This topic describes how to export AI trace data.

## Prerequisites

AI\-related applications have been integrated with Server\-side Monitoring and are reporting observability data normally. For details, see [AI scenario monitoring overview](https://docs.byteplus.com/en/docs/apmplus/Overview_of_AI_scenario_monitoring).

## Limits

* Currently, the data backflow feature is available only for AI\-related applications. Both the total exported data limit and the limit per export task are 100,000 records.

* You can use the data backflow feature to export only new data. Exporting historical data is temporarily not supported. To export historical data, see [Offline trace export](https://docs.byteplus.com/en/docs/apmplus/Span_export).

## Procedure

**Method 1: Create an export task manually**

1. Log in to the[ AI app monitoring](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis).

2. In the left navigation bar, select **Online Trace Export**.

3. Click ** Create export task** on the **Export Task** tab, and configure the parameters as needed. After completion, click **Confirm**.

   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Task name |Customize the name of the export task. |
   ||Overall data limit |Each export task supports exporting up to 100,000 records. You can adjust this value based on actual scenarios. |
   |Data filtering |Data filtering |The range of data to be exported. Supported filter parameters include: Span type, AI span type, Service name, Model name, Interface name, Status code, Actions, and Time consumption.<br><br>> **tip**<br><br><br><br>* > Multiple conditions can be configured for the same filter parameter. These conditions are evaluated based on OR logic. This indicates that data that meets all of the conditions is exported.<br><br><br>* > If multiple filter parameters are configured simultaneously, they apply based on AND logic. This indicates that only data that meets all specified parameters simultaneously is exported.<br> |
   |Time range |New data feed |The data export method. Currently, only exporting new data is supported. The export rules will be applied to newly generated trace data that meets the filter conditions. |
   ||Overall time range |Specify the total time range of the exported data based on actual scenarios. |
   ||Repeat frequency |The repeat frequency of the export task. You can specify a time period within the total range to run the export task daily or weekly.<br><br><br>* **Do not repeat**: If the execution frequency is not configured, all data within the total time range will be exported. For example, if the total time range is 2026\-03\-03 00:00:00 to 2026\-03\-05 00:00:00, all data meeting the requirements within this time range are exported.<br><br>* **Repeat by day**: Specify the daily execution frequency and per\-run data limit for the export task. Only data within the specified time period is exported. For example, if the total time range is 2026\-03\-03 00:00:00 to 2026\-03\-05 00:00:00 and the repeat frequency is 00:00:00 to 03:00:00 every day, only data meeting the requirements from 2026\-03\-03 00:00:00 to 03:00:00 and 2026\-03\-04 00:00:00 to 03:00:00 is exported.<br><br>* **Repeat by week**: Specify the execution frequency and per\-run data limit for the export task every week. Only data within the specified time period is exported.<br><br><br>> **warning**<br><br><br>> Both the total data limit and the limit per export task are 100,000 records. You can customize these limits. Data exceeding the upper limit will fail to be exported.<br> |
   |Export settings |Export platform |Exports trace data to the agent evaluation platform. |
   ||Data masking |* **On (default): ** Data masking is enabled. The Input and Output information in exported data is automatically masked to protect sensitive data.<br><br>* **Off:**  Data masking is disabled. You can export the complete Input and Output information for debugging and troubleshooting. |
   ||Target evaluation set |Select an existing evaluation set on the agent evaluation platform, or add a new evaluation set. When adding a new evaluation set, you need to customize the name of the target evaluation set. |
   ||Import method |The method used to import trace data to the agent evaluation platform. Currently, only appending data is supported. This indicates that data is appended to the existing data. |
   ||Field mapping |The field mapping relationships when data is imported to the agent evaluation platform. Sequentially select the trace span fields and the fields in the target evaluation set. |

###

**Method 2: Create an export task from a template**

Task templates are platform\-preset or user\-defined collections of export task configurations. When you create an export task from a task template, the system automatically populates parameters such as the task name, data filters, and field mappings. This reduces repetitive configuration and improves task creation efficiency.

1. Log in to the [AI app monitoring](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis).

2. In the left navigation bar, select **Online Trace Export**.

3. On the ** Task template** tab, click **Use template** on the target template card. The system automatically populates the parameters predefined in that template.

   > **tip**

   * > The platform provides multiple built\-in task templates that cover common scenarios, including LLM invocation errors, length truncation, high token consumption, Agent Run failures, and long execution times. You can also save an existing export task as a custom template for future reuse. For details, see [What to do next](https://docs.byteplus.com/en/docs/Observability_Platform/Data_backflow).

   * > You can quickly search for templates by template type, name, and description.

4. Configure the other parameters as needed. After completion, click **Confirm**. For parameter configuration descriptions, see [Method 1: Create an export task manually](https://docs.byteplus.com/en/docs/Observability_Platform/Data_backflow).

## What to do next

* After the export task is created, you are redirected to the task list. You can click the destination in the "**Export destination**" column of the target task to go to the target evaluation set and view the exported data details. You can also use the exported trace data to create an evaluation set to run evaluation experiments.

* The export tasks support the following basic actions.

   |Actions |Description |
   |---|---|
   |Pause/enable |Click ** Enable ** or **Pause** in the Actions column of the target task to manually pause or enable the task.<br><br>> **tip**<br><br><br>> **Pause**: takes effect only for tasks in the**In progress**state. **Enable**: takes effect only for tasks in the **Paused** state.<br> |
   |Copy |Click ** Copy** in the Actions column of a task to duplicate an existing export task, modify its configuration as needed, and quickly create a new export task. |
   |Save as template |Click ** Save as template** in the Actions column of the target task to save its configuration as a task template. The next time you create an export task from this template, the system automatically populates parameters such as the task name, data filters, and field mappings.<br><br>> **tip**<br><br><br>> Currently, you can only save an existing export task as a task template. You cannot create a blank task template directly.<br> |
   |Delete |Click **Delete** in the Actions column of the target task to delete an existing export task.<br><br>> **warning**<br><br><br>> Deleted tasks cannot be recovered. Proceed with caution.<br> |
