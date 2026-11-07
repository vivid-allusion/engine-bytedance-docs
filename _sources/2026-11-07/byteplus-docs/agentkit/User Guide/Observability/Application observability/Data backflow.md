---
title: "Data backflow"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Data_backflow"
---

In distributed system observability scenarios, the trace data generated in the production environment is a key basis for revealing system performance bottlenecks, abnormal calls, and service dependencies. As capabilities such as intelligent diagnosis, performance analysis, and trace detection rules continue to iterate, large numbers of standardized, high\-quality trace samples are required for evaluation.

By exporting trace data in batches to evaluation sets, you can build a standardized and reusable trace sample library. You can then run evaluation experiments directly using trace samples from the evaluation sets. This supports scenarios such as trace diagnosis algorithm verification, detection rule optimization, anomaly detection evaluation, and fault case accumulation and reproduction. This achieves a closed loop from real production data to evaluation verification and improves the accuracy and reliability of diagnostic capabilities on the Observability Platform. This topic describes how to export AI trace data.

<span id="QYsJPamU"></span>
## Limits


* Both the total data limit and the limit per export task are 100,000 records.

* The data backflow feature currently supports the backflow of new data only and does not support the backflow of historical data yet.


<span id="clWRAxTP"></span>
## Procedure


1. Log in the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left navigation pane, select **Observability \> Data reflow**.

3. Click **Create export task**, configure the parameters for the export task as needed, and then click **Confirm**.

   
   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Task name |Customize the name of the export task. |
   ||Overall data limit |Each export task supports exporting up to 100,000 records. You can adjust this value based on actual scenarios. |
   |Data filtering |Data filtering |The range of data to be exported. Supported filter parameters include: Span type, AI span type, Service name, Model name, Interface name, Status code, Actions, and Time consumption.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple conditions can be configured for the same filter parameter. These conditions are evaluated based on OR logic. This indicates that data that meets all of the conditions is exported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If multiple filter parameters are configured simultaneously, they apply based on AND logic. This indicates that only data that meets all specified parameters simultaneously is exported.</div><br> |
   |Time range |New data feed |The data export method. Currently, only exporting new data is supported. The export rules are applied to newly generated trace data that meets the filter conditions. |
   ||Overall time range |Specify the total time range of the exported data based on actual scenarios. |
   ||Repeat frequency |The repeat frequency of the export task. You can specify a time period within the total range to run the export task daily or weekly.<br><br><br>* **Do not repeat**: If the execution frequency is not configured, all data within the total time range is exported. For example, if the total time range is 2026\-03\-03 00:00:00 to 2026\-03\-05 00:00:00, all data meeting the requirements within this time range are exported.<br><br>* **Repeat by day**: Specify the daily execution frequency and per\-run data limit for the export task. Only data within the specified time period is exported. For example, if the total time range is 2026\-03\-03 00:00:00 to 2026\-03\-05 00:00:00 and the repeat frequency is 00:00:00 to 03:00:00 every day, only data meeting the requirements from 2026\-03\-03 00:00:00 to 03:00:00 and 2026\-03\-04 00:00:00 to 03:00:00 is exported.<br><br>* **Repeat by week**: Specify the execution frequency and per\-run data limit for the export task every week. Only data within the specified time period is exported.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Both the total data limit and the limit per export task are 100,000 records. You can customize these limits. Data exceeding the upper limit will fail to be exported.</div><br> |
   |Export settings |Export platform |Exports trace data to the agent evaluation platform. |
   ||Data masking |* **On (default): ** Data masking is enabled. The Input and Output information in exported data is automatically masked for sensitive data security.<br><br>* **Off: ** Data masking is disabled. You can export the complete Input and Output information for debugging and troubleshooting. |
   ||Target evaluation set |Select an existing evaluation set on the agent evaluation platform, or add a new evaluation set. When adding a new evaluation set, you need to customize the name of the target evaluation set. |
   ||Import method |The method used to import trace data to the agent evaluation platform. Currently, only appending data is supported. This indicates that data is appended to the existing data. |
   ||Field mapping |The field mapping relationships when data is imported to the agent evaluation platform. Sequentially select the trace span fields and the fields in the target evaluation set. |
   


<span id="JZq3pSkn"></span>
## What to do next


* After the export task is created, you are redirected to the task list. You can click the **destination ** in the "Export destination" column of the target task to go to the target evaluation set and view the exported data details. You can also use the exported trace data to create an evaluation set to run evaluation experiments.

* Export tasks support the following basic operations.

   
   |Item |Description |
   |---|---|
   |Pause/enable |Manually pause or enable an export task within the specified time range. |
   |Copy |Copy an existing export task and modify the configurations as needed to quickly create a new export task. |
   |Edit |Edit the configuration of an existing export task. The task will be executed based on the new configuration. |
   |Delete |Delete an existing export task.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted tasks cannot be recovered. Proceed with caution.</div><br> |
