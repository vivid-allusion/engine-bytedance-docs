---
title: "Use JDBC or MySQL-CDC data sources"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources"
---

MySQL is a widely used open\-source relational database management system that supports efficient data storage and retrieval, commonly used in web applications and data analysis scenarios. Flink provides two common MySQL data access methods. First, the Flink JDBC Connector supports querying and writing results for batch or small\-scale data via JDBC connections to MySQL databases. Conversely, the MySQL CDC (Change Data Capture) Connector can capture real\-time changes in MySQL databases and stream them into Flink, suitable for real\-time data synchronization and more complex analysis scenarios.

<span id="29c2d632"></span>
# Prerequisites


1. To ensure network access security, the cloud product services used in this article all employ internal network access methods, hence MySQL and Flink resource pools must be located in the same VPC within the same region. You can create a private network before setting up cloud resources. For related documentation, please see [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* Based on compliance requirements, if MySQL\-related functionalities are needed, users must upload the MySQL driver themselves. Please proceed to the [MySQL official site](https://downloads.mysql.com/archives/c-j/) to download version 8.0.27, and upload it to the development dependencies file.


<span id="ba64d279"></span>
# Step One: Download the MySQL Driver


1. Go to the [MySQL official site](https://downloads.mysql.com/archives/c-j/), select the MySQL driver version 8.0.27, and choose "**Platform Independent**" for the operating system.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e48951382fa549be9a244f100bb8461d~tplv-goo7wpa0wc-image.image) </span>


2. Select the TAR or ZIP package, then click the Download button to download. Extract the files and find the mysql\-connector\-java\-8.0.27.jar file.

3. Upload the extracted JAR package to the file management module.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/516ab26ebc17487db9a44bcf4192292f~tplv-goo7wpa0wc-image.image" width="591px" /></div>


<span id="d6063af7"></span>
# Step Two: Develop SQL Tasks


1. Login to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, and then click on the project block to enter the project.

4. Click the plus button on the **task development** page to create a task.

   You can also select the target folder and create a task directly within that folder; or simply click on **Flink Task** under **BytePlus Flink**.

5. In the **create task** dialog, set task name, task type, parent folder, engine version, and other parameters, then click **confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d503ead21d54181a8c7ca39749fdb7e~tplv-goo7wpa0wc-image.image" width="588px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fe5dd02d09d4df49e7915904e333293~tplv-goo7wpa0wc-image.image" width="574px" /></div>



|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name.<br><br>The length of the name must be between 1 and 48 characters, supporting numbers, upper and lower case letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Task Type |Select **BytePlus Flink \> Flink Stream \> SQL**.<br><br>If you need to experience the development process of a JAR task, please see [开发JAR 作业](https://docs.byteplus.com/docs/flink/Flink_JAR_Tasks). |
|Related Folder |The system provides folder management functionality for categorizing and managing tasks. During the task development experience, you can directly select the default **data development folder** in the system.<br><br>If you have requirements for managing tasks with custom\-built folders, please click the folder button to create a folder. |
|Engine version |We currently support BytePlus Flink 1.11\-byted, BytePlus Flink 1.16\-byted, and BytePlus Flink 1.17\-byted versions; please choose as needed. |
|Task Description |Enter the description of the task, which typically explains the functionality implemented by the task. |



6. Edit the business logic code of the SQL task in the task editing area.

   Here is an example SQL task code. The code means: create a new `*MySQL-cdc*` source table, fetch real\-time change data from MySQL, and write the change data to a downstream Kafka.

   ```SQL
   create table orders_source (
     _id varchar,
     order_id bigint,
     order_product_id bigint,
     order_customer_id bigint,
     order_status varchar,
     order_update_time timestamp(3),
     PRIMARY KEY (_id) NOT ENFORCED
   ) WITH (
    'connector' = 'mysql-cdc',
    'hostname' = 'localhost',
    'port' = '3306',
    'username' = 'root',
    'password' = '*******',
    'database-name' = 'mydb',
    'table-name' = 'orders'
   );
   
   
   create table kafka_sink (
     _id varchar,
     order_id bigint,
     order_product_id bigint,
     order_customer_id bigint,
     order_status varchar,
     order_update_time timestamp,
     PRIMARY KEY (_id) NOT ENFORCED
   ) WITH (
     'connector' = 'upsert-kafka',
     'topic' = 'topic-test',
     'properties.bootstrap.servers' = 'xxx',
     'properties.group.id' = 'xxx',
     'properties.enable.idempotence' = 'false',
     'key.format' = 'json',
     'value.format' = 'json'
   );
   
   
   INSERT INTO kafka_sink
   SELECT
     *
   FROM
     orders_source;
   ```
   

7. Click the **format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more elegant, tidy, and readable.

8. After editing the SQL task code, click the **verify** button.

   The system will automatically verify the correctness of your SQL statements, and if there is an error, please modify the SQL statements based on the prompts given. After the inspection passes, the system displays `success`.

9. After editing and validating the code, click the **save** button to save the task code.


<span id="f3ea2891"></span>
# Step Three: Upload the MySQL Driver


1. Click the parameter configuration button on the right side of the editor, and select the JAR resource uploaded in "**Step One**" from the dependency files.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e483d5436cef427eb23921ea886e4460~tplv-goo7wpa0wc-image.image" width="574px" /></div>


After successful uploading, you can proceed with SQL debugging, job deployment, startup, and other functions as per the normal process.

<span id="a3cc3cb0"></span>
# Important Notes

If the above MySQL driver is not uploaded, the following error may occur, with the key error message shown as follows:

```Plain
Caused by: java.lang.IllegalArgumentException: JDBC-Class not found. - com.mysql.jdbc.Driver
```


Here is a specific screenshot:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c67f38677ad94c75b1d14127b71b74fe~tplv-goo7wpa0wc-image.image) </span>

Troubleshooting Method:


1. Check whether the MySQL driver has been successfully uploaded and attached to the SQL dependency files.

2. After confirming that steps one to three have been completed according to the document, restarting the task should resolve the issue.
