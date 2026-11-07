---
title: "Create Flink CDC Job (Beta)"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Flink_CDC_Job"
---

BytePlus Flink's stream processing based on Flink CDC effectively accomplishes data ingestion from source to target through developing YAML jobs. This article will guide you through the operational steps for developing Flink CDC jobs.

<span id="2e169a57"></span>
## Prerequisites

The project administrator (Project_Admin) has already created the Flink resource pool within the project, please see [创建资源池](https://docs.byteplus.com/docs/flink/Create_Resource_Pool).

<span id="ac7316d3"></span>
## Develop Flink CDC Jobs


1. Log in to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. Select **Project Management** in the left navigation bar, then click on the project block to enter the project.

4. On the **Task Development** page, click the plus button to create a task.

   You can also choose a target folder to create tasks directly within it; or you can simply click on **Create** under **Flink CDC**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee173c8b75a249c082ba0388cf82dc42~tplv-goo7wpa0wc-image.image) </span>


5. In the **Create** dialog, set the job name, job type, storage location, engine version, and other parameters. After previewing the Change Data Capture task, if everything is correct, click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73bf1563e23a4a47932021a587f8828b~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Job name |Customize the job’s name.<br><br>The name must be 1\-48 characters long, supporting numerals, uppercase and lowercase letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a letter or numeral. |
|Job type |Select **job type \> Flink CDC**. |
|Template selection |Supports selecting types for data sources (Source) and data downstream (Sink).<br><br>The current data source supports MySQL.<br><br>The data downstream supports ByteHouse CDW, Kafka, Doris/StarRocks, Paimon, etc. |
|Data Routing |Add a routing module in the Change Data Capture template. Routing specifies the rules for matching a series of source tables and mapping them to a target table. The most typical application scenario is the merging of sub\-databases and sub\-tables, routing multiple upstream source tables to the same target table. |
|Data Transformation |Add a data transformation module in the Change Data Capture template. The transformation module helps users delete and expand data columns based on the data columns in the table. Additionally, it helps users filter out some unnecessary data during the synchronization process. |
|Storage Location |The system provides folder management functions to categorize and manage tasks. During the task development experience, you can directly select the existing system default **Data Development Folder**.<br><br>If you have requirements to manage tasks with custom folders, click the folder button to create a folder, and then create the folder. |
|Engine Version |We currently support Flink 1.16\-byted and Flink 1.17\-byted versions; please choose as needed. |
|Task Description |Enter a description statement for the task, generally describing the function implemented by the task. |



6. Edit the business logic code of the Change Data Capture task in the task editing area.

   Here is an example of a CDC YAML task code. The code means: Create a new MySQL type data source, synchronize all data tables under the app_db library to the Doris downstream. And perform some routing and field conversion on the data tables.

   ```YAML
   source:
        type: mysql
        hostname: localhost
        port: 3306
        username: root
        password: 123456
        tables: app_db.\.*
   
      sink:
        type: doris
        fenodes: 127.0.0.1:8030
        username: root
        password: ""
   
      transform:
        - source-table: adb.web_order01
          projection: \*, UPPER(product_name) as product_name
          filter: id > 10 AND order_id > 100
          description: project fields and filter
        - source-table: adb.web_order02
          projection: \*, UPPER(product_name) as product_name
          filter: id > 20 AND order_id > 200
          description: project fields and filter
   
      route:
        - source-table: app_db.orders
          sink-table: ods_db.ods_orders
        - source-table: app_db.shipments
          sink-table: ods_db.ods_shipments
        - source-table: app_db.products
          sink-table: ods_db.ods_products
   
      pipeline:
        name: Sync MySQL Database to Doris
        parallelism: 2
   ```
   

7. Refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources)uploading `mysql-connector-java` into the dependency file.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54b11d3b13e641328d89000be34fed90~tplv-goo7wpa0wc-image.image) </span>


8. After completing the CDC task code editing, click the **Verify** button.

   The system will automatically check the correctness of your YAML statements, and if there is an error, please modify the YAML statements according to the tips. After passing the verification, the system will display `success`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cd42561157f4f3f8f0f1422e0a88234~tplv-goo7wpa0wc-image.image) </span>

9. After editing and verifying the code, click the **save** button to save the task code.
