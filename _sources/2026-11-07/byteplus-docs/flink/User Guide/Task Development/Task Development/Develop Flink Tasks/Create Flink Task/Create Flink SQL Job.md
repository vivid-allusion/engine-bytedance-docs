---
title: "Create Flink SQL Job"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Flink_SQL_Job"
---

In the Flink console, you can create Flink SQL jobs by expressing your business logic through simple SQL statements, thus achieving business objectives.

<span id="83f2a1d5"></span>
## Prerequisites

Before you start developing SQL jobs, the following preparations should be completed:


* The project manager or project administrator (Project_Admin) has already created a Flink resource pool within the project. Please see [Create VCI resource pool](https://docs.byteplus.com/docs/flink/Create_VCI_resource_pool).

* Typically, developers (Project_Dev) are responsible for developing tasks. Please ensure that the operator has been added as a project member and associated with their role, please see [Add project members](https://docs.byteplus.com/docs/flink/Member_Management#a45bfca3).


<span id="4d6d755d"></span>
## Develop Flink Stream SQL Job


1. Log in to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left\-sided navigation bar, select **Project Management**, use the search box to perform a fuzzy search based on the project name, and then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Development**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder to directly create a task in that folder, or simply click on **Create** under **Flink SQL**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ed84302ae354d4c936bf442e7b00ff6~tplv-goo7wpa0wc-image.image) </span>


6. In the **Create** dialog, set the task name, task type, affiliated folder, engine version, and other parameters, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95b0a8cf88ec4b1fbfcc8686dadf5a4e~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name.<br><br>The length of the name should be between 1 and 48 characters. It supports numbers, uppercase and lowercase English letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Task Type |Select **Job Type \> SQL**. |
|Associated Folder |Select the target folder from the dropdown list.<br><br>The system by default has one **Data Development Folder**, but to manage tasks more conveniently, you can create additional folders.<br><br>For instructions on how to create a folder, see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders). |
|Engine Version |Currently supports BytePlus Flink 1.11\-byted (maintained), BytePlus Flink 1.16\-byted, and BytePlus Flink 1.17\-byted versions. Please select as needed. |
|Task Description |Enter the description of the task, which typically outlines the functionality implemented by the task. |



6. Edit the business logic code for the SQL task in the task editing area.

   After the task is created, the task code editing area opens by default, where you can write SQL code according to the actual business needs.

   Here is a test case that you can use directly.

   ```SQL
   CREATE TABLE datagen_source (
        siteid INT,
        citycode SMALLINT,
        username STRING,
        pv BIGINT
        )
   WITH (
     'connector' = 'datagen',
     'rows-per-second' = '2',                
     'fields.username.length' = '10',            
     'fields.siteid.max' = '10000',   
     'fields.siteid.min' = '1000'        
   );
   CREATE TABLE print_sink (
       siteid INT,
       citycode SMALLINT,
       username STRING,
       pv BIGINT
       )
   WITH (
        'connector' = 'print',
        'print-identifier' = 'out'            
   );
   insert into print_sink
   select * from datagen_source;
   ```
   

7. Click the **Format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more aesthetically pleasing, neat, and readable.

8. After completing the SQL task code editing, click the **Validate** button.

   The system automatically verifies the correctness of your SQL statements; if an error occurs, please modify the SQL statements according to the prompts. After the verification passes, the system will display `success`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3347643d85c4adfa22ea28cc2b4eae5~tplv-goo7wpa0wc-image.image) </span>

9. After editing and verifying the code, click the **save** button to save the task code.


<span id="e5e4a6a7"></span>
## Develop Flink Batch SQL tasks.


1. Log in to BytePlus Flink Console.

2. Select the target region from the top menu bar.

3. In the left sidebar, select **Project Management**, conduct a fuzzy search by project name in the search box, then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Development**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder, create a task directly in that folder, or simply click on **Create** under **Flink SQL**.

6. In the **Create** dialog, set the task name, task type, folder, engine version, and other parameters, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93d86f6d79fb437fa7f605772f49bf10~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name.<br><br>The length of the name is limited to 1\-48 characters, supporting numbers, upper and lower case letters, underscores (_), hyphens (\-), and periods (.); the name must start and end with a letter or a number. |
|Task Type |Select **Operation Templates \> Batch**. |
|Belonging Folder |Select the target folder from the dropdown list.<br><br>There is a default **Data Development Folder**, but for easier task management, you can freely create folders. For instructions on how to create a task folder, please see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders). |
|Engine Version |Currently supports Flink 1.11\-byted (maintenance), Flink 1.16\-byted, Flink 1.17\-byted versions; please choose as needed. |
|Task Description |Enter the task description, generally describing the functionality of the task. |



6. Edit the business logic code for the SQL job in the task editing area.

   After the task is created, the code editing area for the task opens by default, where you can write SQL code based on actual business needs.

   This provides a test case: read the content of an existing MySQL table, then print it using the Print connector.

   ```SQL
   create table mysql_source (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp,
       PRIMARY KEY (order_id) NOT ENFORCED
   ) WITH (
    'connector' = 'jdbc',
    'url'='jdbc:mysql://mysq***fb.rds.ibyteplus.com:3306/gts_autotest',
    'username' = '***test',
    'password' = 'Pw**45!',
    'table-name' = 'orders'
   );
   
   create table print_sink (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
   ) WITH (
     'connector' = 'print'
   );
   
   insert into print_sink
   select * from mysql_source;
   ```
   

7. Click the **Format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more beautiful, tidy, and readable.

8. After editing the SQL task code, click the **Verify** button.

   The system will automatically check the correctness of your SQL statements; if there is an error, please modify the SQL statement according to the prompt. After verification passes, the system indicates `success`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52d82a9e85ad402ca6e507f2f99a6e8e~tplv-goo7wpa0wc-image.image) </span>

9. After editing and verification, click the **Save** button to save the task code.
