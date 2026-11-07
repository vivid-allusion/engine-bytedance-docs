---
title: "Usage Guide"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Usage_Guide"
---

BytePlus Flink supports two types of task development: Flink SQL and Flink JAR. Please select the task type according to your actual needs. There are differences in the development process between SQL and JAR type tasks, please refer to the corresponding documentation.


|**Documentation** |**Description** |
|---|---|
|* [Create Flink SQL Job](https://docs.byteplus.com/docs/flink/Create_Flink_SQL_Job)<br><br>* [Create Flink JAR Jobs](https://docs.byteplus.com/docs/flink/Create_Flink_JAR_Jobs) |Guidance on how to create and develop tasks on the console. |
|[Debugging Flink Stream SQL Tasks](https://docs.byteplus.com/docs/flink/Debugging_Flink_Stream_SQL_Tasks) |Once task development is complete, you can debug the task, mitigate data risks, and improve development efficiency.<br><br>You can choose to debug with online data in the Session resource pool; alternatively, you can upload local CSV data files for offline debugging. |
|[Configure Flink Parameters](https://docs.byteplus.com/docs/flink/Configure_Flink_Parameters) |Guide on how to configure Flink\-related parameters, including resource configuration for Task Manager and Job Manager, as well as settings for Checkpoint, task failure restart policies, and dependency files. |
|[Launch Flink Task](https://docs.byteplus.com/docs/flink/Launch_Flink_Task) |After completing development and debugging, task developers can deploy the tasks to the production environment. Operations staff will formally initiate the task, which will then continuously run and output calculation results. |
|[Configure Upstream and Downstream Information](https://docs.byteplus.com/docs/undefined/67c910f742da8005e779a567) |You can configure the data source and destination for the task, and later view the data sources within the task details. |
|[变更引擎版本](https://docs.byteplus.com/docs/flink/Change_Engine_Version) |We currently primarily support BytePlus Flink versions 1.11\-byted and 1.16\-byted. In Flink SQL scenarios, free switching between the two versions is supported. |
|[Manage Task Versions](https://docs.byteplus.com/docs/flink/Manage_Task_Versions) |Once the task is launched, the system will record the task version, logging it with each operation.<br><br>On the task version page, you can compare the current version with historical versions, Rollback to a historical version, or delete historical versions. |
