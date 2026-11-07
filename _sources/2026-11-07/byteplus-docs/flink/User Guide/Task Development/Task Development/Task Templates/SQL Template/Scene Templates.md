---
title: "Scene Templates"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Scene_Templates"
---

During the development process of Flink SQL tasks, developers often need to spend time and effort in coding. The console now provides rich scene templates for Flink CDC, which can be used directly for task development.

<span id="0ec86592"></span>
## View CDC Templates


1. Log in to [BytePlus Flink Console](https://console.volcengine.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management** and then click on the project block to enter the project.

4. In the left navigation of the project, select **Task Development \> Jupyter lab**.

5. On the **Template Management** page, select **SQL Templates \> Scene Templates** and view the templates.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23d1b30fd4794c5f90cd7bf2e4b7659e~tplv-goo7wpa0wc-image.image) </span>

6. View the template content, usage scenarios, and supported engine versions.

   
   |**Template Name** |**Use Case** |**Engine Version** |
   |---|---|---|
   |MongoDB CDC To BMQ |Scenario for writing MongoDB CDC to BMQ, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To ByteHouse\-CDW |Scenario for writing MongoDB CDC to ByteHouse\-CDW, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To ByteHouse\-CE |MongoDB CDC writes into ByteHouse\-CE scenario, please remember to replace specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To EMR\-Hive |MongoDB CDC writes into EMR\-Hive scenario, please remember to replace specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To EMR\-StarRocks |MongoDB CDC writes into EMR\-StarRocks scenario, please remember to replace specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To ES\-6 |MongoDB CDC writes into ES\-6 scenario, please remember to replace specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To ES\-7 |MongoDB CDC writing to ES\-7 scenario, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To HBASE\-1.4 |MongoDB CDC writing to HBASE\-1.4 scenario, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To HBASE\-2.2 |MongoDB CDC writing to HBASE\-2.2 scenario, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MongoDB CDC To Kafka |MongoDB CDC writes to Kafka scenario, please replace specific connection parameters |Flink 1.16\-volcano |
   |MySQL CDC To BMQ |MySQL CDC writes to BMQ scenario, please replace specific connection parameters. |Flink 1.16\-volcano |
   |MySQL CDC To ByteHouse\-CDW |MySQL CDC writes to ByteHouse\-CDW scenario, please replace specific connection parameters. |Flink 1.16\-volcano |
   |MySQL CDC To ByteHouse\-CE |MySQL CDC scenario writing into ByteHouse\-CE, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MySQL CDC To EMR\-Hive |MySQL CDC scenario writing into EMR\-Hive, please create the EMR\-Hive Catalog in advance. |Flink 1.16\-volcano |
   |MySQL CDC To EMR\-StarRocks |MySQL CDC scenario writing into EMR\-StarRocks, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MySQL CDC To ES\-6 |MySQL CDC scenario writing into ES\-6, please replace the specific connection parameters. |Flink 1.16\-volcano |
   |MySQL CDC To ES\-7 |Please replace specific connection parameters in the scenario where MySql CDC writes to ES\-7. |Flink 1.16\-volcano |
   |MySQL CDC To HBASE\-1.4 |Please replace specific connection parameters in the scenario where MySql CDC writes to HBASE. |Flink 1.16\-volcano |
   |MySQL CDC To HBASE\-2.2 |Please replace specific connection parameters in the scenario where MySql CDC writes to HBASE. |Flink 1.16\-volcano |
   |MySQL CDC To Kafka |MySQL Change Data Capture writes to Kafka; please remember to replace the specific connection parameters. |Flink 1.16\-volcano |
