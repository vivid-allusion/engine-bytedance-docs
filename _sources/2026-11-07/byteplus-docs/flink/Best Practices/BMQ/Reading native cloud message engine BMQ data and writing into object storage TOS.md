---
title: "Reading native cloud message engine BMQ data and writing into object storage TOS"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Reading_native_cloud_message_engine_BMQ_data_and_writing_into_object_storage_TOS"
---

This article explains how to read real\-time data from a BMQ Topic using a simple Flink SQL task, and then write it into TOS.

<span id="43e6407f"></span>
## Process Introduction

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MzVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTM1IDY1Ij48ZGVmcy8+PGc+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Qk1RIFRvcGljPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VE9TIEJ1Y2tldDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDEyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZsaW5rIFNRTCBKb2I8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTMyIDI3LjcxIEwgMTY4LjMxIDI3LjcxIEwgMTY4LjMxIDIyIEwgMTkyIDMyIEwgMTY4LjMxIDQyIEwgMTY4LjMxIDM2LjI5IEwgMTMyIDM2LjI5IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM0MiAyNy43MSBMIDM3OC4zMSAyNy43MSBMIDM3OC4zMSAyMiBMIDQwMiAzMiBMIDM3OC4zMSA0MiBMIDM3OC4zMSAzNi4yOSBMIDM0MiAzNi4yOSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvc3ZnPg==" />


1. Prepare the BMQ Topic data source.

   You need to create a resource pool, Topic, and Consumer Group in the native cloud message engine console and obtain the resource pool access point address.

2. Prepare the TOS Bucket data destination.

   You need to create a storage bucket and folder in the object storage console.

3. Develop a Flink SQL task.

   Once you have prepared the data sources and destinations, you can develop SQL tasks on the BytePlus Flink console to read data from BMQ Topic and write it to TOS Bucket using simple code.


<span id="78e4a62b"></span>
## Prerequisites

To ensure network access security, the cloud product services used in this article all utilize internal network access, so BMQ resource pools and Flink resource pools must be in the same VPC within the same region.

You can create a private network before creating cloud resources. For related documentation, please see [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

<span id="4718e14c"></span>
## Step One: Prepare BMQ Topic data source


1. Login to the [Cloud Native Messaging Engine Console](https://console.byteplus.com/bmq).

2. Select the target region on the top menu bar, then enter the target project from the **Project Management** page.

3. Create a resource pool.

   1. In the left navigation bar of the project, select **Resource Management** and then click **Create Resource Pool**.

   2. On the **create resource pool** page, set up basic information, resource configuration, network details, and Topic settings for the resource pool, then click **Next: Confirm Order**.

      
      |**Primary Configuration Item** |**Secondary Configuration Item** |**Description** |
      |---|---|---|
      |Basic Information |Resource Type |Default is **General Resource**. |
      ||Resource Mode |Defaults to **VCI mode**, which creates a BMQ resource pool on the generic resource\-VCI resource domain. |
      ||Billing Type |Select the billing type for the resource pool. Currently only supports **pay\-as\-you\-go**. |
      ||Resource Pool Name |Enter the resource pool name.<br><br><br>* Consisting of lowercase letters, numbers, and hyphens (\-).<br><br>* Length of 1~64 characters. |
      ||Regional and Availability Zone Deployment |The region has been selected and cannot be changed.<br><br>Based on the business's network latency, high availability disaster recovery requirements, choose **single availability zone** or **multiple availability zones**.<br><br><br>* Single availability zone: Choose an appropriate availability zone.<br><br>* Multiple availability zones: Multiple availability zones are selected by default. |
      ||Associated Project |Select the associated project from the dropdown list. |
      |Resource Configuration |Compute Specifications |Based on the estimated number of Topics, Consumer Groups, partitions, etc., required by the business scenario, select the appropriate resource pool specifications. |
      ||Storage Specifications |By default, CloudFS accelerated storage is used, with no additional configuration required. |
      |Network Information |Private Network |To ensure smooth access to the intranet, it is recommended to select a VPC located in the region of your existing cloud services. In the same VPC, subnets in different availability zones are interconnected.<br><br>If a private network has not been created yet, please refer to [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
      ||Subnet |Select the subnet from the drop\-down list. The system will automatically filter the available subnets based on your selected region, availability zone, and private network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the resource pool is deployed across multiple availability zones, subnets must be configured individually for each selected availability zone.</div><br> |
      ||Security Group |Select a security group from the dropdown list. |
      |Topic Configuration |Message Retention Duration |Set the default message retention duration for all Topics under this resource pool.<br><br><br>* The default is 72 hours and can be adjusted on an hourly basis.<br><br>* The supportable retention range is 1~336 hours (14 days). |
      

   3. On the **Order Details** page, confirm the resource pool configuration details, read and agree to the related product agreements, then click **Purchase Now**.

      After submitting the purchase order, you can return to the resource pool page. The purchased resource pool will display as **Initializing** and after initialization, it will display as **Running**.

4. Retrieve the endpoint address.

   1. On the **Resource Pool Management** page, click on the resource pool name to enter the resource pool details page.

   2. Under the **Service Access** tab on the resource pool details page, view and copy the user endpoint address of the resource pool.

5. Create Topic.

   1. In the left navigation bar of the resource pool details, select **Topic** and then click **Create Topic**.

   2. In the **Create Topic** dialog, set the name, number of partitions, message retention duration, and then click **Confirm**.

      
      |**Configuration** |**Description** |
      |---|---|
      |Topic Name |Enter the Topic name.<br><br>The name can consist only of lowercase letters, numbers, underscores (_), and hyphens (\-), and must be between 3 and 64 characters long. |
      |Description |Enter the description for the Topic. |
      |Number of partitions |Enter the number of partitions.<br><br>The default is 12, and the remaining available partitions are displayed below the input field. |
      |Message retention period |The retention period of data in the Topic.<br><br><br>* The default is to align with the global message retention period set by the resource pool, but it can also be adjusted on an hourly basis.<br><br>* The supported retention range is 1~336 hours (14 days). |
      

6. Create a Consumer Group.

   1. In the left sidebar of the resource pool details, select **Consumer Group**, then click **Create Group**.

   2. In the **Create Group** dialog, set the Group name and description, then click **Confirm**.

      
      |**Configuration** |**Description** |
      |---|---|
      |Group Name |Customize the Group Name.<br><br><br>* Consists of lowercase English letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length is 3~64 characters. |
      |Description |Enter description information. Not required. |
      


<span id="ad641064"></span>
## Step Two: Prepare the data destination TOS Bucket


1. Log in to the [Object Storage Console](https://console.byteplus.com/tos).

2. In the left sidebar, click on **Bucket List**, then click on **Create Bucket**.

3. On the **Create Storage** bucket page, set the bucket name, region, and bucket policy, and other key parameters, then click **Confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40c962071479472586263832ba464346~tplv-goo7wpa0wc-image.image" width="757px" /></div>


This section only introduces the required parameters for creating a storage bucket. For more information, please refer to [Create Storage Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


|**Configuration** |**Instructions** |
|---|---|
|Name |Customize the name of the storage bucket.<br><br><br>* It can consist only of numbers, hyphens (\-), and lowercase English letters, and must start and end with a number or letter.<br><br>* The length must be between 3 to 63 characters. |
|Region |Keep in the same region as the BMQ resource pool and Flink resource pool. |
|Bucket Policy |Set the bucket policy for the storage bucket, choosing a **private** policy here.<br><br>The strategy is outlined as follows:<br><br><br>* **Private**: The default setting. Only the bucket's owner and authorized accounts have read and write access to its contents. Recommended for use.<br><br>* **Public read**: Anyone can read from a bucket with public read permissions, which will also incur traffic costs.<br><br>* **Public read/write**: Anyone can read from and write to a bucket with public read/write permissions, which will also incur traffic costs. |



4. On the **File List** page of the bucket, click **Create Folder**, then set the folder name and click **Confirm**.

   Object Storage TOS stores files in a flat structure. To facilitate category management, you can create folders.


<span id="88aa9d17"></span>
## Step Three: Develop Flink SQL Jobs


1. Log in to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar, then enter the project from the **Project Management** page.

3. Create a resource pool.

   1. In the project's left navigation bar, select **Resource Management**, then click the **Resource Pool** tab, and click **Create Resource Pool**.

   2. On the **Create General Resource Pool** page, set up basic information, network information, storage parameters of the resource pool, and then click **Next: Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8645dbc677746099911712392f727e7~tplv-goo7wpa0wc-image.image" width="734px" /></div>


```Plain Text
  | | | | \
  |**Primary configuration option** |**Secondary configuration option** |**Description** |
  |---|---|---|
  | | | | \
  |Basic information |Resource type |Defaults to **general resources**. |
  |^^| | | \
  | |Resource Mode |Default is **VCI mode**, where Flink resource pools are deployed on the universal resource-VCI resource domain. |
  |^^| | | \
  | |Billing Type |\
  | |  |Flink resource pools deployed in the universal resource-VCI resource domain support both **pay-as-you-go** and **subscription-based** billing types; please choose as needed. |\
  | | |For billing details, please refer to [Pay-As-You-Go](/docs/flink/Pay-As-You-Go) and [Annual and Monthly Subscription](/docs/flink/Annual_and_Monthly_Subscription). |\
  | | |If you choose the subscription-based billing type, you also need to select **purchase duration**, and confirm if **automatic renewal** is needed. |
  |^^| | | \
  | |Resource Pool Name |Enter the name of the resource pool to be created. |\
  | | | |\
  | | |* Must be globally unique and cannot be an empty string. |\
  | | |* Length must be 1 to 63 characters. |\
  | | |* Supports lowercase English letters, numbers, and hyphens (-); the name must start and end with a letter or number. |
  |^^| | | \
  | |Regions and Availability Zones |* The region has been selected and cannot be changed. Maintain in the same region as BMQ resource pool and TOS Bucket. |\
  | | |* Choose an appropriate availability zone based on network latency and high availability requirements for your business. |
  |^^| | | \
  | |Associated Projects |Select the project to which the resource pool belongs from the drop-down list. |
  | | | | \
  |Resource Configuration |Compute Specifications |If you create a **subscription-based** billing type, you will need to manually configure resources for the Flink resource pool. The basic unit of resources is CU, where 1 CU means: 1 core CPU, 4 GB memory. |\
  | | |Set resource quantities based on actual needs. |
  | | | | \
  |Network Information |Private Network |Select a private network from the dropdown list. The resource pool needs to be within the same VPC as the BMQ. |
  |^^| | | \
  | |Subnet |\
  | |  |Select a subnet from the dropdown list. |\
  | | |The system will automatically filter available subnets based on the region, availability zone, and private network you select. |
  |^^| | | \
  | |Security Group |Select a security group from the dropdown list. |
  | | | | \
  |Storage Information |TOS Object Storage |Defaults to the TOS associated at product initialization and cannot be modified. |
```



3. On the **Details** page, review the configurations of the resource pool, read and check the Flink\-related agreements, then click **Purchase Now**.

   You can return to the resource pool list page to view the creation progress. Once created, it shows as **Running**.

4. Develop tasks.

   1. In the project's left navigation bar, select **Task Development \> Tasks**, then click the plus button to create a task.

   2. In the **Create Task** dialog, set the task name, type, folder, and engine version, then click **OK**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6cefe4de70443ea857a4b9778f4979~tplv-goo7wpa0wc-image.image" width="752px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecb7a8b4fd614b86855ef76766733d85~tplv-goo7wpa0wc-image.image" width="763px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Task Name |Customize the task name, such as “datagen-bmq-tos”. |\
  | |The character length of the name is limited to 1-48, supporting numbers, uppercase and lowercase English letters, underscores (_), hyphens (-), and periods (.), and it can only start and end with a number or letter. |
  | | | \
  |Task Type |Select **Flink Task > Flink Stream > SQL**. |
  | | | \
  |Current Folder |The system provides folder management functionality for categorizing tasks. You can directly choose the system's default **Data Development Folder**. |\
  | |If you have requirements for managing tasks in custom folders, please click the button to create a folder, then create the folder. |
  | | | \
  |Engine Version |Currently supports **Flink 1.11-byted** and **Flink 1.16-byted** versions. |\
  | |:::warning |\
  | |If you connect to BMQ resources via Kafka connector and use the Flink 1.16-byted engine version, you must set the `properties.enable.idempotence` parameter to **false** to disable idempotence; otherwise, the task will fail. |\
  | |::: |
  | | | \
  |Task Description |Enter a description of the task, generally describing its functionality. |
```



3. Write the business logic code for the SQL task in the task editing area.

   Here, you can directly copy and use the following code. The code connects a datagen connector that generates random numbers in real time and initially writes them to a BMQ Topic; it then reads data from BMQ Topic and outputs it to a TOS Bucket.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When reading and writing data to the BMQ Topic using the Kafka connector, if you are using the Flink 1.11 engine version, you can directly use the following Demo. When using the Flink 1.16 engine version, it is necessary to add the configuration <code><em>'properties.enable.idempotence'</em></code><code>=</code><code><em>'false'</em></code> to disable idempotence; otherwise, the task will fail to run.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Flink tasks use the Kafka connector to write data into the BMQ Topic. If there is insufficient throughput when writing data, you can increase the throughput by setting <strong>properties.batch_size</strong> and <strong>properties.linger_ms</strong>. For Kafka related parameters, please refer to <a href="https://docs.byteplus.com/docs/flink/Kafka_BMQ">Kafka/BMQ</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When writing files to TOS, use the filesystem connector. To quickly see the files written in the TOS Bucket, additional configurations are required. You can set the connector's <strong>sink.rolling\-policy.file\-size</strong>, <strong>sink.rolling\-policy.rollover\-interval</strong> parameters, and enable Checkpoint in the Flink parameters.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For filesystem connector parameters, please refer to <a href="https://docs.byteplus.com/docs/flink/Filesystem">Filesystem</a>; for detailed information about the filesystem connector's rolling strategy, please refer to the open\-source document <a href="https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/connectors/filesystem.html#rolling-policy">Filesystem\-Rolling Policy</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In a task, if a table is used as both source and sink, an error will occur during debugging <code>Table:xxx should not be both source and sink.</code>. It is recommended to directly verify the correctness of the SQL to ensure it is error\-free before going live.   </div>
   

   ```SQL
   CREATE TABLE orders (
     order_id BIGINT,
     order_product_id BIGINT,
     order_customer_id BIGINT,
     order_status VARCHAR,
     order_update_time AS LOCALTIMESTAMP
   ) WITH (
     'connector' = 'datagen',
     'rows-per-second' = '1',
     'fields.order_status.length' = '3',
     'fields.order_id.min' = '1',
     'fields.order_id.max' = '10000',
     'fields.order_product_id.min' = '1',
     'fields.order_product_id.max' = '100',
     'fields.order_customer_id.min' = '1',
     'fields.order_customer_id.max' = '1000'
   );
   
   
   CREATE TABLE bmq_table (
     order_id BIGINT,
     order_product_id BIGINT,
     order_customer_id BIGINT,
     order_status VARCHAR,
     order_update_time TIMESTAMP
   ) WITH (
     'connector' = 'kafka',
     --When accessing BMQ resources, use the kafka connector.
     'topic' = 'topic-b',
     --Topic name.
     'properties.bootstrap.servers' = 'bmq***bq5-1.xxx.byteplus.com:9092,bmq***bq5-2.xxx.byteplus.com:9092,bmq***bq5-3.xxx.byteplus.com:9092',
     --User access point address of BMQ resource pool, three addresses are separated by English commas.
     'properties.group.id' = 'group-b',
     --BMQ Consumer Group name, which needs to be created in advance, otherwise the Offset cannot be submitted normally.
     'scan.startup.mode' = 'earliest-offset',
     'scan.topic-partition-discovery.interval' = '120s',
     --The time interval for periodically scanning and discovering new Topics and Partitions.
     'format' = 'json'
   );
   
   
   INSERT INTO
     bmq_table
   SELECT
     *
   FROM
     orders;
   
   
   CREATE TABLE tos_sink (
     order_id BIGINT,
     order_product_id BIGINT,
     order_customer_id BIGINT,
     order_status VARCHAR,
     order_update_time TIMESTAMP
   ) WITH (
     'connector' = 'filesystem',
     --Use the filesystem connector when accessing TOS resources.
     'path' = 'tos://doc-**test/fl**le/',
     --tos path, consisting of Bucket name and folder name.
     'sink.rolling-policy.file-size' = '1M',
     --The maximum limit of file memory. When this value is reached, the file is closed and a new file is opened for writing.
     'sink.rolling-policy.rollover-interval' = '5 min',
     --The continuous writing time of the file. When this value is reached, the file is closed and a new file is opened for writing.
     'format' = 'json'
   );
   
   
   INSERT INTO
     tos_sink
   SELECT
     *
   FROM
     bmq_table;
   ```
   

4. Click the **Format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more elegant, tidy, and readable.

5. Above the code editing area, click the **Validate** button.

   The system will automatically verify the correctness of your SQL statements. If there are errors, please modify the SQL statements based on prompts. After validation, the system will display a message: `success`.

6. Above the code editing area, click **Parameter Configuration**, and then enable Checkpoint.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ca1b70b954a4411a85c5cded199f0cb~tplv-goo7wpa0wc-image.image" width="717px" /></div>



5. Start the task.

   1. In the **Task Development** section, find and click the target task, then at the top of the editing area, select the correct **Execution Method** and **Engine Version**, and then click **Go Live**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For Flink Stream type jobs, select <strong>STREAMING</strong> as the execution method; for Flink Batch type jobs, select <strong>BATCH</strong> as the execution method.      </div>
      

   2. In the **Task Launch Settings** dialog, select the runtime resource pool, set task priority and scheduling strategy, then click **OK**.

      The system will indicate that the task has been successfully launched, and you can go to the **Task Management** page to view it.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524e04a812e44a6eb9d179660c924013~tplv-goo7wpa0wc-image.image" width="734px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Runtime Resource Pool |Select the Flink resource pool for the task from the dropdown list. |
  | | | \
  |Task Priority |\
  | |The system default preset priority is L3. You can set the task priority as needed, the smaller the number, the higher the priority. |\
  | |Task priority determines the internal scheduling order of tasks, with tasks of higher priority being scheduled first, i.e., L3 is scheduled before L4. |
  | | | \
  |Scheduling Strategy |Configure the task scheduling strategy based on requirements. |\
  | | |\
  | |* GANG: Ensures all instances of a task are scheduled together, allocating resources only when the remaining resources meet the task’s normal operating requirements; no allocation is made if the needed resources are not met. |\
  | |   This strategy prevents the phenomenon where resources are allocated but the tasks cannot start, thus solving the resource deadlock issue. |\
  | |* DRF: Considers multidimensional resources to fairly distribute resources among all tasks in the resource pool, thereby enhancing utilization. |\
  | |   For example: With a remaining 10 cores and 40 GB of resources, Task A needs 10 cores and 20 GB; Task B needs 2 cores and 8 GB. If assigned to Task A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would instead allocate to Task B, leaving 8 cores and 32 GB available for subsequent tasks. |
  | | | \
  |Scheduling Duration |\
  | |When set to the GANG scheduling strategy, a scheduling duration needs to be set. |\
  | |If it exceeds the scheduling duration, the task will fail to schedule. If set to 0, it will keep retrying. |
```



3. In the project's left side navigation bar, select **Task Operations & Management \> Task Management**, then click the **Launch** button behind the target task.

4. In the **Launch Task** dialog, choose the task startup method, then click **OK**.

   The task launch will take some time, please be patient. After successful launch, the status will be **In Progress**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dd91778d5642978425aa6d276bbc33~tplv-goo7wpa0wc-image.image" width="716px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Startup mode |Please choose the startup method based on the actual situation: |\
  | | |\
  | |* Start from the latest state: Start with the latest Checkpoint or Savepoint. |\
  | |* Start from scratch: Start without using a Checkpoint or Savepoint. |\
  | |* Start from a specified snapshot: Start with the specified target snapshot (Savepoint). |\
  | | |\
  | |:::tip |\
  | |The task being launched for the first time can only start in a **brand new** mode. |\
  | |::: |
  | | | \
  |Parameter configuration |The task comes with parallelism on the development side, and resource configurations for Task Manager and Job Manager. Supports updating configurations and quick implementation when launching tasks. |\
  | |:::tip |\
  | |After updating the parameter settings and launching the task, a new task version will be added, and the latest configurations will be synchronized to the development side of the task. |\
  | |::: |\
  | | |\
  | |* Parallelism: Global concurrency of the task. |\
  | |* Single TaskManager CPU count: The number of CPU cores of a single TaskManager. |\
  | |* Single TaskManager memory size: The memory size occupied by a single TaskManager. |\
  | |* Single TaskManager slot count: The number of slots in a single TaskManager. |\
  | |* JobManager CPU count: The number of CPU cores of a single JobManager. |\
  | |* JobManager memory size: The memory size occupied by a single JobManager. |
  | | | \
  |More settings |When adding or modifying operators during task development changes, it may result in the task not being able to restore from snapshots. In this case, you may choose to enable the **allow partial operator state ignoring** feature to ensure the task runs smoothly. |\
  | |![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0930d87d01fb434f848a25d7194bed8d~tplv-goo7wpa0wc-image.image =1380x) |\
  | |:::warning |\
  | |* Only when selecting the **specified snapshot start** or **start from the latest state** mode is it supported to choose to ignore some operator states. |\
  | |* When you choose the **brand new start** mode, ignoring operator states is not supported. |\
  | |::: |
```


<span id="221342a9"></span>
## Result validation.

The code for the Flink SQL task is implemented to first write the random numbers generated in real\-time by the datagen connector into the BMQ Topic; then, it reads the BMQ Topic data and outputs it to the TOS Bucket.

Therefore, you can preview the data on the BMQ Topic side to verify whether the random data has been written correctly; you can also check in the TOS Bucket to see if the files have been written.

<span id="0af37702"></span>
### Preview BMQ Topic Data


1. Log in to [Cloud Native Message Engine Console](https://console.byteplus.com/bmq).

2. Select the target region from the top menu bar.

3. On the **Project Management** page, search for the target project by project name, then click on the project block to enter the project.

4. In the left navigation bar, select **Resource Management**, then click on the target resource pool name to enter the resource pool detail page.

5. In the resource pool detail, select **Topic** in the left navigation bar, then click on **Data Preview** behind the target Topic.

6. In the **Data Preview** dialog, select the data preview method, fill in the relevant information, then click **Preview Now**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Data Type |Currently only supports **Str** type. |
   |Data Preview |Select the method for data preview.<br><br><br>* **Based on Timestamp**: Preview information based on the timestamp of the production message.<br><br>* **Based on Offset**: Preview information based on the consumption offset. |
   |Partition |Select the partition for storing messages, both preview methods require this parameter to be set. |
   |Timing |When selecting the **time\-based** preview mode, you must set a specific timing. |
   |Relative Offset |When selecting the **position\-based** preview mode, a relative offset must be set. |
   

7. View the data preview results, then click **Close**.


<span id="ca51cc35"></span>
### View TOS Bucket files


1. Log in to the [Object Storage Console](https://console.byteplus.com/tos).

2. In the left navigation bar, select **Bucket List**, and then click on the target bucket name.

3. On the **File List** page, click on the target folder name to view the details of the written files.
