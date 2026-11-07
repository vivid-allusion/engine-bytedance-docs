---
title: "DaftJob jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DaftJob_jobs"
---

Daft is a Python\-native distributed data processing framework designed specifically for AI data pipelines, excelling at multimodal data processing and large\-scale feature extraction. To meet users' needs for multimodal data processing with Daft, EMR Serverless supports users in creating and running DaftJob, ready to use out of the box with no additional cluster management required. This article introduces the methods for creating and submitting DaftJob.

<span id="659f81fb"></span>
# Prerequisites


* An EMR Serverless queue has been created, and you have `Developer`/`Admin` permissions for the compute group. For detailed operations, refer to: [Create queues](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue), [Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions).

* A compute group has been created. DaftJob jobs run in the queue's **general compute group** or **Ray Cluster compute group configured with the daft image**. For details on compute group operations, see [Create and manage computing groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).


<span id="40b7536d"></span>
# **Submit Job**: via the console

<span id="e350aae5"></span>
## Preparation

Write the job code, package it as a ZIP file, and upload it to a TOS bucket in the same **region** as the current Serverless queue.

This article provides a complete job example. For details, see [Complete job example](https://docs.byteplus.com/docs/E-MapReduce/120652#3234ee07). For upload operations, see [Uploading objects](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

<span id="61105b41"></span>
## Submit Job


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the dropdown according to your scenario.

3. Click **Job center**\>**Job management** or **Job instance** to enter the **Create job** page

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c7122eb47b643ddb1be92e6ced5668b~tplv-goo7wpa0wc-image.image) </span>

4. Configure the parameters for the job.

   1. Configure the job **Basic information** and **Resource allocation**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/216bf15eb4ec45fcb00e1b417432a102~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameters** |**Note** |
      |---|---|
      |Job Name |The name of this job. Once created, it cannot be changed. |
      |Job types |The type of job to be created. |
      |Execution resources |EMR resources used to execute the job, divided into a resource type dropdown and a queue/computing group dropdown.<br><br>You can select specific resources and search by name or ID.<br><br>Only **general computing groups** or **Ray Cluster computing groups configured with daft images** are supported. |
      |Head |The head node is the management node responsible for job scheduling and task coordination. It does not participate in actual data computation. Each job has exactly one head node. |
      |Worker |The worker node is the execution node responsible for performing actual computation tasks. The number and specifications of worker nodes determine the computational performance of the job. |
      

   2. Configure **Job content.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf8d180ab81a4eb3ab1417b61f40232e~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameters** |**Note** |
      |---|---|
      |Image type |The source type of the image required to run the job. The following two types are supported:<br><br><br>* Built\-in image: Standard images preset by the system, matched according to job type.<br><br>* Volcano image repository: User\-uploaded custom images, suitable for scenarios requiring pre\-installed dependencies. |
      |Image |The specific image version used under the selected image type. |
      |Task master file |Select the main code file that has been uploaded to the TOS bucket in the same region as the current Serverless queue. |
      |Entry command |The entry command for submitting DaftJob, usually `python xxx.py`.<br><br>If there are parameters, add them to this command as well. |
      |environment variables |Environment variables are entered in the form of `key-value`. If you enter `APP_ENV` in the left input box of each row and `PRODUCTION` in the right input box, you can obtain it in the job as follows: `import os; var = os.getenv("APP_ENV")`. Here, `var` will be assigned the value `"PRODUCTION"`. |
      

   3. **Advanced settings。** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8337e780ddf14ddd9e4cf29265a53d26~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameters** |**Note** |
      |---|---|
      |GCS High Availability |When submitting DaftJob, you can use the toggle on the page to enable or disable GCS high availability.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are not familiar with GCS high availability, you can visit <a href="https://docs.ray.io/en/latest/ray-core/fault_tolerance/gcs.html">GCS Fault Tolerance</a> for related information.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you submit a RayJob through a RayCluster compute group, the GCS high availability configuration of the compute group will be automatically inherited, and no additional configuration is required.</div><br><br><br><br>If enabled, you need to fill in the following parameters:<br><br><br>* RedisURL: Specify the Redis instance used for GCS backup. After creating the instance in the Redis console, obtain the private domain name/port of the target instance from the instance list page.<br><br>* Password: Specify the Redis instance password. Set the password for the default account of the corresponding instance. |
      |Internet connection |Configure whether to enable the network connection. After enabling, you must set the corresponding VPC, subnet, and security group.<br><br>After configuration is complete, when subsequent jobs run, Ray's head/worker nodes can access services or resources within the enterprise VPC network through the VPC configured here. |
      |Custom parameters |Add custom job parameters based on the actual requirements of the job.<br><br>DaftJob supports the same custom parameters as RayJob. For details, see [Reference: Custom parameters supported by RayJob](https://docs.byteplus.com/docs/E-MapReduce/RayJob_jobs#7ca81722). |
      |Storage path mount |Set the storage paths that may need to be mounted for the current job. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |
      

5. After editing the job, click the **Create and run** button in the lower right corner to submit the job. You can also **create only** and manually trigger the job run later on the job list page.


<span id="3234ee07"></span>
## Complete job example

The following is a DaftJob example:


1. Prepare the data. Save the following content as `orders.csv` and upload the data to the TOS bucket.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa0568df7ea941eaa22a441eb3b6c974~tplv-goo7wpa0wc-image.image" name="orders.csv">orders.csv</Attachment>
   

2. Prepare the job code. Compress the following code as `demo. zip` and upload it to the TOS bucket.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/721cd6f6aa914035abed8e0ab02e4f37~tplv-goo7wpa0wc-image.image" name="demo.zip">demo.zip</Attachment>
   

&nbsp;

   Before use, modify the following locations according to your actual situation:

   1. Environment variables `TOS_ACCESS_KEY / TOS_SECRET_KEY`: Enter your AK/SK.

   2. `region_name` and `endpoint_url`: Modify according to the region where the TOS bucket is located (the example is Beijing). For details, see [TOS Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).

   3. `<your_bucket>` and `<your_path>` in `read_csv`: Replace with your actual bucket name and object path

      demo.py:

   ```Python
   import os
   import daft
   from daft import col
   from daft.io import IOConfig, S3Config
   
   # 1. Configure TOS: Modify according to the region where the bucket is located. AK/SK are read from environment variables
   # Use the S3-compatible interface of TOS; data is still stored in TOS
   io_config = IOConfig(
       s3=S3Config(
           region_name="cn-beijing",
           endpoint_url="https://tos-s3-cn-beijing.volces.com",
           key_id=os.environ["TOS_ACCESS_KEY"],      
           access_key=os.environ["TOS_SECRET_KEY"], 
           force_virtual_addressing=True,
       )
   )
   
   # 2. Read the order CSV from TOS. Important: Replace with your bucket name and file path
   df = daft.read_csv("s3://<your_bucket>/<your_path>/orders.csv", io_config=io_config)
   
   # 3. Filter paid orders and aggregate sales by category
   result = (
       df.where(col("status") == "paid")
       .with_column("revenue", col("price") * col("quantity"))
       .groupby("category")
       .agg(col("revenue").sum())
       .sort("revenue", desc=True)
   )
   
   # 4. Perform calculations and display results
   result.show()
   ```
   

3. Create and submit the job via the console, enter the **entry command** and add **environment variables:** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2d0689507f460d8534a6ea258ce5c5~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameters** |**Inputs** |
   |---|---|
   |Entry command |`python demo.py` |
   |Environment variables |* `TOS_ACCESS_KEY`<br><br>* `TOS_SECRET_KEY` |
   

4. View the job run results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd758c76a7d64661a4c7862e1f4e28db~tplv-goo7wpa0wc-image.image) </span>


&nbsp;

<span id="0c80161f"></span>
# View/run/delete jobs

After a job is created, you can view all created jobs on the job list page, manually trigger a job to run, or edit, modify, and delete jobs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1941ed94ade4f4cbbd2cde209b34c06~tplv-goo7wpa0wc-image.image) </span>

<span id="fdacf04e"></span>
# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.


<span id="bc7a6a9b"></span>
# Reference: Custom parameters supported by DaftJob

The custom parameters supported by DaftJob are consistent with those of RayJob. For details, see [Reference: Custom parameters supported by RayJob](https://docs.byteplus.com/docs/E-MapReduce/RayJob_jobs#7ca81722).
