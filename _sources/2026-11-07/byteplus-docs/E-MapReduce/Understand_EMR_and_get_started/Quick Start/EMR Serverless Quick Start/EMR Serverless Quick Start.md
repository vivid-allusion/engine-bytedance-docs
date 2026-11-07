---
title: "EMR Serverless Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Quick_Start"
---

EMR Serverless provides fully managed multi\-engine services, including Spark, Ray, Presto, Doris, StarRocks, and more. You can quickly create and submit various engine jobs through the console. This document provides three common job examples. By following the step\-by\-step instructions, you can experience the entire process from job creation and submission to result viewing, helping you get started quickly.

<span id="c5a6db5b"></span>
# Basic concepts


* Job: A job is a complete data computing task. To submit a data computing task in EMR Serverless, users can submit a job in EMR. After job submission, the system automatically allocates computing resources based on the configuration, executes the computation, outputs the results, and releases the computing resources upon completion.

* queue(Queue): A queue is a computing resource pool provided by EMR Serverless, containing basic computing resources such as CPU and memory. It is required to run jobs. After users submit jobs, computing components such as Spark and Ray are scheduled and execute jobs within the queue, and the platform automatically allocates computing resources for the jobs.

   * EMR provides different types of computing resources as underlying support. You can select as needed: standard computing resources, memory\-enhanced CPU computing resources, compute\-enhanced CPU computing resources, and GPU\-accelerated computing resources (when purchasing GPU resources, you need to contact the Sales representative to reserve inventory).

   * EMR offers multiple queue types: public queue, dedicated queue–Subscription (elastic resources can be purchased as needed), and dedicated queue–hourly billing. This allows you to flexibly choose the appropriate resource type and billing mode based on different business scenarios, improving resource utilization and reducing costs.


<span id="33296105"></span>
# Prerequisites


* Before using EMR Serverless for the first time, please follow the [Preparation](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq)guide to complete Volcano Engine account registration, real\-name authentication, and EMR service activation. The EMR main account has extensive permissions. It is recommended to create sub\-users and grant permissions according to the principle of least privilege.

* queue is the resource pool required for running EMR Serverless jobs. When using EMR Serverless, you need to prepare the corresponding queue resources. This Quick Start uses the public queue.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The public queue is a shared queue resource automatically created for you after enabling EMR Serverless. In actual use, you can create other queue resources as needed. For operation details, see<a href="https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue">Create a queue</a>.   </div>
   

* When running a job, you typically need to upload the job code package to TOS (Torch Object Storage, object storage). The job will subsequently be run directly from TOS, so you need to prepare AK/SK credentials that can access the TOS service. Because the primary account key has extensive permissions, and only the key for accessing the TOS service is needed for this Quick Start, please create a sub\-account with only TOS operation permissions and use its key. For detailed procedures, see [Access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Code files for PySpark and RayJob jobs must be uploaded in advance to a TOS (object storage) bucket. During job execution, the system will read files from the specified path.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Spark SQL jobs can SQL EditorSubmit Job directly from the console without preparing TOS resources, so you can skip Preparation.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f681b54381c4f85814e832657ef237a~tplv-goo7wpa0wc-image.image) </span>


<span id="14d6e9a0"></span>
# Procedure

This document provides several demo jobs as examples to help you quickly get started with EMR Serverless.


* RayJob: Python job based on the Ray distributed framework.

* PySpark: Spark job written in Python.

* Spark SQL: Write SQL statements directly in SQL Editor to query and process data.


<span id="3ab4b0a5"></span>
## Preparation: Prepare job Demo

This Quick Start provides sample Demo files for the target jobs below. You can also use your own job code files, upload them to TOS, and reference them directly when creating jobs in EMR Serverless.


1. Obtain job Demo.

   
   |**Job types** |**Sample files** |Sample job code |
   |---|---|---|
   |RayJob |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b15ebf0a76c454f968a50c884aa3008~tplv-goo7wpa0wc-image.image" name="ray_job.zip">ray_job.zip</Attachment><br> |```Python```<br>```import ray```<br>```import time```<br>``````<br>```# Initialize Ray```<br>```ray.init()```<br>``````<br>```# Define a remote function```<br>```@ray.remote```<br>```def square(x):```<br>```    time.sleep(1)  # Simulate a time-consuming computation```<br>```    return x * x```<br>``````<br>```# Create a task list```<br>```numbers = [1, 2, 3, 4, 5]```<br>``````<br>```# Use Ray to compute square values in parallel```<br>```results = ray.get([square.remote(num) for num in numbers])```<br>``````<br>```# Output results```<br>```print("Squares:", results)```<br>``````<br>```# Shut down Ray```<br>```ray.shutdown()```<br> |
   |PySpark |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1238b019f19c49a7b2c01ebc6b07edff~tplv-goo7wpa0wc-image.image" name="py_job.py">py_job.py</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b97788e29844b87bcd432aa6024c6a5~tplv-goo7wpa0wc-image.image" name="models.py">models.py</Attachment><br> |py_job.py code:<br><br>```Python```<br>```"""```<br>```主入口脚本：Spark 作业测试```<br>```"""```<br>```from pyspark.sql import SparkSession```<br>```from pyspark.sql import functions as F```<br>```from pyspark.sql import types as T```<br>```from pyspark.sql import SQLContext```<br>```from models import Bean```<br>``````<br>```# Spark job name```<br>```job_name = 'py_job_test'```<br>``````<br>```# Initialize SparkSession```<br>```spark = SparkSession.builder.appName(job_name).getOrCreate()```<br>``````<br>```# Create a class instance, pass in a count value, and verify whether the Spark job can correctly import and use custom Python modules/classes```<br>```bean = Bean(20)```<br>```print(bean.count)```<br>``````<br>```# Execute an SQL query to test whether the Spark SQL engine is functioning properly```<br>```spark.sql("select 10000 as test_value").show(10)```<br>``````<br>```# Stop the Spark session```<br>```spark.stop()```<br><br><br>models.py code:<br><br>```Python```<br>```class Bean(object):```<br>```        count = 0```<br>```        def __init__(self, count):```<br>```                self.count = count```<br> |
   

2. Create a TOS bucket and upload the job Demo to the TOS bucket.

   1. Log in to the [Object Storage Console](https://console.byteplus.com/tos), click **Bucket List** on the left side of the console, then in the bucket list interface, click **Create Bucket** in the upper left corner. On the **Create Bucket** page, enter the configuration parameters. See the table below for required parameter descriptions. Leave the others at their default values. For detailed parameter descriptions, see [Create Bucket](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1#.5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5qG2).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/761708b592b243df8b48095224d3d92b~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameters** |**Note** |**Example** |
      |---|---|---|
      |Name |Name of the bucket. Cannot be changed after creation. |abc |
      |Area |Region to which the bucket belongs. Must be in the same region as the EMR Serverless queue; otherwise, direct access is not possible. |North China 2 (Beijing) |
      |Bucket policy |Set the bucket\-level access control policy (Bucket Policy). It is recommended to set it to private. |Private |
      

   2. Upload the demo to the bucket. Click the name of the created bucket to enter the bucket details page, click **File List \> Upload File**, select the demo file, click **upload**. After the upload is complete, on the **File List** page, copy the folder path as a backup parameter. Example path: `tos://abc/doctest`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e7f2f17ee984425afd9798629c65732~tplv-goo7wpa0wc-image.image) </span>


<span id="4494c38d"></span>
## Go to the job entry page


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario:

   * Region: The created queue and corresponding resources will be deployed in the specified region and cannot be modified after creation.

   * Project: The default project is displayed.

3. Depending on the target job type, click the **SQL Editor** button to enter the Spark SQL submission page; click the **Create job** button to enter the RayJob or PySpark job creation page.

   
   |Method 1: On the overview page |Method 2: In the left navigation bar |
   |---|---|
   |Click Job center \> Job management or Job instance, then, in the upper right corner, click **Create job** or **SQL Editor**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/091d03d647384cf5bd226aa54be3e085~tplv-goo7wpa0wc-image.image) </span> |In the left navigation bar, select Serverless, click the queue name to go to the queue details page, then, in the upper right corner, click **Create job** or **SQL Editor**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b863578537674329bb0fb49274832b49~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="5b88685c"></span>
## Create and run a job

<span id="69d7bacd"></span>
### RayJob

On the Create job page, configure the job information. The required parameters for this Demo job are described in the table below. After completing the information configuration, click **Create and run** in the lower right corner to submit the PySpark job and run it in the queue resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92b55386f8c14ff7814ac62a26a11865~tplv-goo7wpa0wc-image.image) </span>


|**Parameters** |**Configuration instructions** |
|---|---|
|Job Name |Enter a custom name for this job. Cannot be changed after creation. |
|Job types |Select the type of job to create. This example selects RayJob. |
|Execution resources |EMR queue resources used to execute the job.<br><br><br>* Resource type dropdown: Select EMR Serverless<br><br>* Queue/project dropdown: For this example, select the default project named 'default'. |
|Image type |For this Quick Start, keep the default settings.<br><br>Each EMR Serverless job runs in a container. The image is the container's "operating system + dependency environment" package.<br><br><br>* Built\-in image: BytePlusprebuilt images provided, suitable for various job scenarios.<br><br>* Byteplus image repository: Images that are custom\-built by users and pushed to the image repository (VCR). |
|mirror image |Click the dropdown and select any image. |
|task master file |The core code file of the job is stored in the TOS bucket. When the platform starts the job, it will pull this file from TOS and execute the entry command. For this example, click the dropdown and select the job uploaded during Preparation, such as `tos://abc/doctest/ray_job.zip`. |
|Entry command |The actual Shell command executed after the job container starts, typically python xxx.py. If there are parameters, add them to this command.<br><br>For this example, enter `python ray_job.py`. |


<span id="dcbb79fa"></span>
### PySpark

On the Create job page, configure the job information. The required parameters for this Demo job are described in the table below. After completing the information configuration, click **Create and run** in the lower right corner to submit the PySpark job and run it in the queue resource.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d808e48cffc24d218fe95529307851f7~tplv-goo7wpa0wc-image.image) </span>


|**Parameters** |**Configuration operations** |
|---|---|
|Job Name |The name of this job, which cannot be changed after creation. |
|Job types |The type of job to be created. For this example, select PySpark. |
|Execution resources |The EMR resources used to execute the job.<br><br><br>* Resource type dropdown: Select EMR Serverless<br><br>* Queue/project dropdown: For this example, select the default project named 'default'. |
|development model |For this example, select UI mode.<br><br><br>* UI: Submit job content through a visual interface.<br><br>* JSON: Submit job content in JSON format. |
|Python file |The core code file of the job is stored in the TOS bucket. When the platform starts the job, it will pull this file from TOS and execute the entry command. For this example, click the dropdown and select the job uploaded during Preparation, such as tos://abc/doctest/py_job.py. |
|Python dependencies |The models file required when executing the task file, stored in the TOS bucket. For this example, click the dropdown and select the models uploaded during Preparation, such as tos://abc/doctest/models.py. |
|Spark parameters |* Environment variables for Spark components.<br><br>* Enter the user's AK/SK here for TOS service authentication. The format is:<br><br>   * serverless.emr.access.key=AKL\*\*\*\*\*<br><br>   * serverless.emr.secret.key=WkR\*\*\*\*\* |


<span id="8912961d"></span>
### Spark SQL

After entering the **SQL Editor** page, submit the SQL statement in the workspace and click **Run**:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">EMR SQL Editoruses Spark SQL as the default execution engine, supports submitting SQL statements from the console to perform data queries, and the metadata service is provided by <a href="https://docs.byteplus.com/en/docs/Byteplus_LAS/What_is_AI_data_lake_service">LAS</a>.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f832b4f51f794da9a972aca55652dcec~tplv-goo7wpa0wc-image.image) </span>


1. Create a table in the database:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When entering the SQL Editorpage for the first time, the system will create a default Hive\-type Catalog for the user and a default database named default. The metadata service is provided byBytePlus LAS (AI Data Lake Service).   </div>
   

   ```SQL
   CREATE TABLE default.testtb
   (
       `id` INT,
       `name` STRING,
       `age` INT
   )
   ```
   

2. Write data to the data table:

   ```SQL
   INSERT INTO default.testtb VALUES(1, 'testyw',26), (2, '张三', 26), (3, '李四', 23)
   ```
   

3. Query table data:

   ```SQL
   SELECT * FROM default.testtb
   ```
   


<span id="b159cf23"></span>
## View job execution results


1. View job entry:

   On the console overview page, click **Job center**  **\>**  **Job management** or **Job instance** to view PySpark and RayJob jobs; Spark SQL jobs can only be viewed from the **Job center**\>**Job instance** page. Jobs can be filtered by **Instance name/ID**, **Job name/ID**, **Start time**, **Submitter**, or **Resource type**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acb1759a50e7494b8a975dfe42ad6584~tplv-goo7wpa0wc-image.image) </span>

2. View job details:

   Click the job name to enter the job details page, where you can view System log, Driver logs, query results, and other information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f75e925576943b1a0543d1c1bf1ba09~tplv-goo7wpa0wc-image.image) </span>


<span id="2f55348f"></span>
### RayJob

Please view the final output of the Demo job on the **Job Details \> Run Log** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e43b2c70fa4e97ab74e76fb2b8d861~tplv-goo7wpa0wc-image.image) </span>

<span id="88aa9f46"></span>
### PySpark

Please go to the **Job Details \> Driver Log** page, select the file named **stdout**, and view the execution result of the Demo job.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8784d7e159914799a01118aa9c6c97ee~tplv-goo7wpa0wc-image.image) </span>

<span id="6f74221c"></span>
### Spark SQL

Please view the query job execution result on the **Job Details \> Query Results** page or in the SQL Editor workspace under **Query Results** .


* **Job Details \> Query Results** page:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b92bf3f30ad24b9baff9ce05b13c744b~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7557803bbeb4ed5802d393f91f99bfa~tplv-goo7wpa0wc-image.image) </span>

* SQL Editor In the workspace under **Query Results** :

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b92a8bec3040457880bb8b77f607bd2b~tplv-goo7wpa0wc-image.image) </span>


<span id="25dacb8e"></span>
# More operations


* Typically, you can also use it in conjunction with DataLeap. The big data R&D governance suite (DataLeap) is a self\-developed, one\-stop big data platform solution by BytePlus, integrating real\-time and offline data integration, data development, intelligent operations and maintenance, data governance, and asset management capabilities. After connecting the EMR engine in DataLeap, you can create EMR Serverless jobs, query data, and more in DataLeap.

* When creating an EMR Serverless queue, you need to select a metadata service. Currently, you can choose BytePlusthe LAS Catalog service as the metadata service for EMR Serverless queue resources.
