---
title: "Read the TLS log service data and write it to the Cloud Search Service, ESCloud"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Read_the_TLS_data"
---

The log service offers Kafka protocol consumption capabilities, allowing a log topic to be treated as a Kafka Topic, with each log entry corresponding to a Kafka message. You can use the Flink Kafka Connector to connect to the log service and consume the collected log data to downstream big data components or a Data Warehouse through Flink tasks.

This article demonstrates reading log data from the TLS topic using a Flink SQL task and then writing it to an ESCloud index.

<span id="318aac45"></span>
## Process Introduction

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTI1IDY1Ij48ZGVmcy8+PGc+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VExTIFRvcGljPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RVNDbG91ZCBJbmRleDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDAyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZsaW5rIFNRTCBKb2I8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTI3IDI2LjY0IEwgMTY5LjM2IDI2LjY0IEwgMTY5LjM2IDE5LjUgTCAxOTcgMzIgTCAxNjkuMzYgNDQuNSBMIDE2OS4zNiAzNy4zNiBMIDEyNyAzNy4zNiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzMjggMjYuNjQgTCAzNzAuMzYgMjYuNjQgTCAzNzAuMzYgMTkuNSBMIDM5OCAzMiBMIDM3MC4zNiA0NC41IEwgMzcwLjM2IDM3LjM2IEwgMzI4IDM3LjM2IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />


1. Prepare TLS topic data source.

   You need to create a log project in the log service console, then create a log topic and enable Kafka protocol consumption.

   You also need to obtain the project's access address, project ID, topic ID, and Kafka protocol topic ID, to fill in the information in the Flink SQL task and establish connectivity with TLS.

2. Prepare ESCloud Index as the data destination.

   You need to purchase an instance on the Cloud Search Service console and obtain the instance's access address.

3. Develop Flink SQL tasks.

   Once you have prepared the data source and destination, you can develop SQL tasks on the BytePlus Flink console. You need to create two tasks, one for producing messages and one for consuming messages.


<span id="7f342a7a"></span>
## Prerequisites

To ensure network access security, the cloud products and services used in this article use an internal network access mode, which requires TLS projects, Cloud Search Service instances, and Flink resource pools to be in the same VPC within the same region.

You can create a private network before creating cloud resources. For related documentation, please see [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

<span id="adb0c1a7"></span>
## Step one: Prepare the TLS topic as the data source.

To consume TLS logs with a Flink SQL task, it's essential to first complete the necessary preparations related to TLS. For example, create a log project, set up a log topic, enable Kafka protocol consumption for the topic, and obtain the connection address needed for interacting with TLS.


1. Log in to the [log service console](https://console.byteplus.com/tls).

2. Select the target region in the top navigation bar.

3. Create a log project.

   1. In the left navigation bar, click **log project management**, then click **create a log project**.

   2. In the **create a log project** dialog box, set the project name and description, then click **confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bb33c8c7b324632bebe702b0f2187a4~tplv-goo7wpa0wc-image.image" width="728px" /></div>



4. Create a log topic.

   1. In the project details page, within the **log topics** section, click **create a log topic**.

   2. In the **create a log topic** dialog box, set key parameters such as **topic name**, **log storage duration**, **number of log partitions**, and then click **confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/631471d4a2934356a80c04bd95fdb8d6~tplv-goo7wpa0wc-image.image" width="726px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85560437f3a44c8393165ba37d4bf8fa~tplv-goo7wpa0wc-image.image" width="726px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Topic Name |Customize the name of the log topic. |
  | | | \
  |Log Storage Duration |The log retention time in the log service, logs exceeding the specified storage duration within this log topic will be automatically cleared. |\
  | |The unit is in days, defaulting to 30 days. The value range is from 1 to 3650, with 3650 days indicating permanent storage. |
  | | | \
  |Number of log partitions |The number of log partitions, with a default of creating 1 partition, can range from 1 to 10. Each partition provides a write capability of 5 MiB/s, 500 operations/s, and a read capability of 10 MiB/s, 100 operations/s. |\
  | |Once created, the modification of partition numbers is not supported. However, increasing the overall read and write capabilities of the log topic via automatic partition splitting is supported. |
  | | | \
  |Automatic partition splitting in logs |Whether to enable the automatic partition splitting feature. |\
  | | |\
  | |* (Default) Enabled: When the data volume written continuously exceeds the existing partition's service capability for 5 minutes, the log service automatically splits partitions according to the data volume to meet business needs, but the number of partitions after splitting cannot exceed the maximum allowed. New partitions created within the last 15 minutes will not automatically split. |\
  | |* Off: Automatic splitting of partitions is turned off. |
  | | | \
  |Maximum number of partitions |The maximum number of partitions, that is, the maximum number of all partitions after a partition is split. The value range is from 1 to 10, with the default being 10. |
  | | | \
  |Description |A simple description of the log topic. |
```



5. Activate Kafka protocol consumption.

   1. In the **log topic** section of the project detail page, click on the log topic name to enter the log topic details page.

   2. In the **Kafka protocol consumption** section on the log topic details page, check the **enable** option, then click **confirm** in the popup dialog box.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee3f56c9543440a4982464f75fd21b31~tplv-goo7wpa0wc-image.image" width="718px" /></div>



6. Obtain the endpoint address.

   1. In the **basic information** section of the log project detail page, view and copy the log project's ID, private network address, and log topic ID.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a6592480a74b73a302db3219bd9af0~tplv-goo7wpa0wc-image.image" width="718px" /></div>


```Plain Text
  * ① Log project ID: Used as the Kafka SASL username when consuming TLS logs with Kafka protocol.
  * ② Log project private network address: Used as the connection address for TLS log projects in Flink SQL tasks.
  * ③ Log topic ID: Used in Flink SQL tasks that produce messages, specifying the target topic for writing messages.
```



2. In the **Kafka protocol consumption** area on the log topic details page, view and copy the **Kafka protocol consumption topic ID**.

   * Kafka protocol consumption ID: Used in Flink SQL tasks that consume messages, specifying the target topic for reading messages.


<span id="4a568f60"></span>
## Step Two: Preparing Data Destination for ESCloud Index

To consume TLS logs using Flink SQL tasks, prepare a data write destination source; this article uses the ESCloud index. Please follow the steps below to create an instance and obtain the instance's access URL.


1. Log in to the [Cloud Search Service Console](https://console.byteplus.com/es).

2. Select the target region from the top navigation bar.

3. Create an instance.

   1. On the **Instance List** page, click **Create Instance**.

   2. On the **Create Instance** page, configure the instance name, availability zone version, node details, and access options, then click **Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50e09a72f3594708b7d7b99c57d30d20~tplv-goo7wpa0wc-image.image" width="718px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Explanation** |
  |---|---|
  | | | \
  |Instance name |Custom instance name, optional. If no instance name is set, a default name identical to the instance ID is generated. |\
  | |When customizing the instance name, the guidelines are as follows: |\
  | | |\
  | |* Cannot start with a number or a hyphen (-). |\
  | |* Can only include Chinese characters, numbers, letters, hyphens (-), and underscores (_). |\
  | |* Length must be within 1 to 128 characters. |
  | | | \
  |Availability Zone |Select the availability zone where the instance will be created. |
  | | | \
  |Version |Compatible with **6.7.1** and **7.10.2** Elasticsearch versions. |\
  | |As an example, version 7.10.2 is selected here. |
  | | | \
  |Deployment Node Types |Supports the following node types: |\
  | | |\
  | |* Data Node: By default, 3 data nodes with a storage specification of 100 GiB each are configured. |\
  | |* Dedicated Master Node: Choose whether to enable a dedicated master node, which is used to ensure instance stability. After enabling the dedicated master node, you need to select the configuration of node specifications. |\
  | |* Kibana Node: The system provides one free Kibana node with 1 core and 2 GiB, which cannot be modified. |
  | | | \
  |Data Node |Configure specifications for data nodes or dedicated master nodes. |\
  | | |\
  | |* Node Specifications: Different specifications include different numbers of CPU cores and memory. Please choose the appropriate node specifications based on your business needs. |\
  | |* Storage Type: Currently only supports ESSD-PL0. |\
  | |* Storage Specifications: Set the storage specifications, ranging from 20 to 10000 GiB. |\
  | |* Number of Nodes: Set the number of nodes based on your business needs. |\
  | | |\
  | |:::tip |\
  | |* When exclusive master nodes are not enabled: It is recommended to configure at least 3 data nodes in a production environment. Configuring 2 nodes carries the risk of split-brain, with the supported number of nodes ranging from 1 to 70. |\
  | |* When exclusive master nodes are enabled: The number of configurable data nodes ranges from 1 to 70, with no other restrictions; exclusive master nodes are fixed at 3. |\
  | |::: |
  | | | \
  |Access Methods |Supports three access modes: sales area access, internal storage network access, and public service area access. |\
  | | |\
  | |* Sales Area Access: Within a private network VPC, instances can be accessed. This document chooses this type of access. |\
  | |* Internal Storage Network Access: Default support for physical machine access, which cannot be modified. |\
  | |* Public Service Area Access: Machines located in the public service area can access. |
  | | | \
  |Private Network |When choosing **sales area access** to access the search service instance, it is necessary to select a specific VPC to access the instance. To ensure smooth access to the internal network, it is necessary to select the VPC consistent with the Flink resource pool. |
  | | | \
  |Subnet |The system will automatically filter available subnets based on the region, availability zone, and private network you select. |
  | | | \
  |Associated project |Select the project to which the cloud search instance belongs for easy resource management; this is optional. |
  | | | \
  |Username |The default is admin and cannot be changed. Used for logging in to the Kibana page and instance authentication. |
  | | | \
  |Login password |The password associated with the admin account must be set according to the rules and stored securely. |\
  | | |\
  | |* The password must include at least three of the following: uppercase letters, lowercase letters, numbers, and special characters. It should be 8 to 32 characters long. |\
  | |* Supports `_#!@$%^&*()+=-` special characters, and must not include spaces or Chinese characters. |
  | | | \
  |Confirm password |Enter the password from the previous step. |
  | | | \
  |Transfer protocol |Select the transfer protocol as **HTTP** or **HTTPS**. |\
  | |:::warning |\
  | |In Flink tasks, **instances that currently do not support HTTPS protocol** should select HTTP. If the HTTPS access address for ESCloud is configured in a Flink task, the task will fail. |\
  | |::: |
  | | | \
  |Delete protection |Choose whether to enable delete protection; it is disabled by default. |\
  | |The delete protection feature prevents accidental deletion of instances, so you cannot delete an instance while this option is enabled. |
  | | | \
  |Billing Type |Select the instance's billing type, supporting **pay-as-you-go** and **subscription**. For detailed information about billing, please see [Billing Overview](https://docs.byteplus.com/en/docs/cloudsearch/billing-overview). |
```



3. On the **Confirm Order** page, review the instance configuration details, read and check the relevant product agreement, then click **Buy Now** to complete the creation of the instance.

   After the instance is successfully purchased, you can click **Go to Console**, and the page will automatically redirect to the **Instance List** page, where you can conveniently view the newly created instance. An instance changes from **being created** to **running**, indicating that the instance has been created successfully.

4. Obtain the instance access address.

   1. On the **instance list** page, click on the instance name to enter the instance details page.

   2. In the **Instance Information** tab under the **Service Access** area, view and copy the instance access address.

      Flink SQL tasks require setting the instance address to access the instance.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d53a0295f374902ae3b003c53f91f4c~tplv-goo7wpa0wc-image.image" width="708px" /></div>



5. (Optional) You can also click on **Kibana Public Access Address** behind **Enable Public Access**, and then check the public IP to bind.

   Enable public access for Kibana to later log into the Kibana Web page and query data in the Index. If you don't have an available public IP, you can create one from the control panel. For related documentation, see [Apply for Public IP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="1584d1f8"></span>
## Step Three: Develop Flink SQL Tasks.

This document creates two independent Flink SQL tasks. One task is responsible for producing messages, writing random data to the TLS topic; the other handles message consumption, reading data from the TLS topic and writing it to the ESCloud Index.

<span id="f7d436ac"></span>
### Create Flink resource pool


1. Log in to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar, then enter the project from the **Project Management** page.

3. In the project's left navigation bar, select **Resource Management**, then click on the **Resource Pool** tab, followed by clicking on **Create Resource Pool**.

4. On the **Create General Resource Pool** page, set basic information for the resource pool, network information, storage information, and other parameters, then click **Next: Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/217107aa48e04d32ba1fb8f6565c3c03~tplv-goo7wpa0wc-image.image" width="754px" /></div>



|**Primary Configuration Item** |**Secondary Configuration Item** |**Description** |
|---|---|---|
|Basic Information |Resource Type |Default to **General Resource**. |
||Resource Mode |Default to **VCI Mode**, which deploys the Flink resource pool on the General Resource\-VCI resource domain. |
||Billing Type |Deploying Flink resource pool on the General Resource\-VCI resource domain supports **pay\-as\-you\-go** and **monthly and yearly subscription** billing types; please choose according to your needs.<br><br>If you need to understand the billing details, please refer to [Pay-As-You-Go](https://docs.byteplus.com/docs/flink/Pay-As-You-Go) and [Annual and Monthly Subscription](https://docs.byteplus.com/docs/flink/Annual_and_Monthly_Subscription).<br><br>If you choose a monthly or yearly subscription billing type, you must also select **purchase duration** and confirm if **automatic renewal** is needed. |
||Resource Pool Name |Enter the name of the resource pool to be created.<br><br><br>* Must be globally unique and cannot be an empty string.<br><br>* Length must be between 1 and 63 characters.<br><br>* Supports lowercase English letters, numbers, and hyphens (\-); the name must start and end with a letter or number. |
||Regions and availability zones |* The region has been selected and cannot be changed. In the same region as TLS and ESCloud.<br><br>* Choose an appropriate availability zone based on the network latency and high availability requirements of your business. |
||Associated project |Select the project the resource pool belongs to from the drop\-down list. |
|Resource configuration |Compute specifications |If you create a **subscription** billing type, you need to manually configure resources for the Flink resource pool, with the basic unit of resources being CU, where 1 CU means: 1 CPU core, 4 GB RAM.<br><br>Set the resource amount based on actual needs. |
|Network Information |Private Network |Select a private network from the dropdown list. Ensure it is in the same VPC as the log project and cloud search service instance. |
||Subnet |Select a subnet from the dropdown list.<br><br>The system will automatically filter available subnets based on your chosen region, availability zone, and private network. |
||Security Group |Select a security group from the dropdown list. |
|Storage Information |TOS Object Storage |Defaults to the TOS associated at product initialization and cannot be modified. |



5. On the **Details** page, review the resource pool configuration details, read and check the Flink\-related agreement, and then click **Buy Now**.

   You can return to the resource pool list page to view the creation progress. Once the creation is complete, it's displayed as **Running**.


<span id="e86e2839"></span>
### Development Task \- Produce Messages

Follow the steps below to develop and run a Flink SQL task responsible for writing random data into the TLS topic.


1. In the left sidebar of the project, select **Task Development \> Tasks**, then click the plus button to create a task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b91e39ba4db6451ab0118bf106316b05~tplv-goo7wpa0wc-image.image" width="758px" /></div>



2. In the **Create Task** dialog, set the task name, type, folder, and engine version, then click **OK**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb09a2bdd40e40239ecf30ef4f7afb53~tplv-goo7wpa0wc-image.image" width="748px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e9fa355ea8a4a50b97538763f04cf9f~tplv-goo7wpa0wc-image.image" width="706px" /></div>



|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name, such as "Datagen\-TLS9094".<br><br>The length of the name must be between 1 and 48 characters, supporting numbers, uppercase and lowercase letters, underscores (_), hyphens (\-), and periods (.). The name must start and end with a letter or a number. |
|Task Type |Select **Flink Task \> Flink Stream \> SQL**. |
|Current Folder |The system provides folder management features for categorizing tasks. You can directly select the default **Data Development Folder**.<br><br>If you need to manage tasks with your own folders, please click the folder button to create a folder. |
|Engine Version |Currently supports **Flink 1.11\-byted** and **Flink 1.16\-byted** versions.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In the Flink 1.16\-byted engine version using the Kafka connector, the <code>properties.enable.idempotence</code> parameter must be set to <strong>false</strong> to disable idempotence, otherwise the task will fail.</div><br> |
|Task Description |Enter a description of the task, typically describing the functionality it implements. |



3. In the task editing area, write the business logic code for the SQL task of **producing messages**.

   You can directly use the following code, just modify the TLS\-related information. The code implements writing randomly generated numbers by the Datagen connector into the TLS topic in real\-time.

   ```SQL
   create table orders_datagen (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time as localtimestamp
   ) WITH (
    'connector' = 'datagen',
    'rows-per-second'='1',
    'fields.order_status.length' = '3',
    'fields.order_id.min' = '1',
    'fields.order_id.max' = '10000',
    'fields.order_product_id.min' = '1',
    'fields.order_product_id.max' = '1000',
    'fields.order_customer_id.min' = '1',
    'fields.order_customer_id.max' = '1000'
   );
   
   
   create table kafka_table (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
   ) WITH (
     'connector' = 'kafka',
     'topic' = '88999d84-b*****a7e809edba7',       -- TLS Topic ID
     'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9094',  -- TLS log project access point address. When used as a message receiver, the port is fixed to 9094.
     'format' = 'json',
     'properties.enable.idempotence' = 'false',    -- Turn off idempotence
     'properties.security.protocol' = 'SASL_SSL',  -- SASL_SSL connection protocol ensures the security of log transmission
     'properties.sasl.mechanism' = 'PLAIN',
     'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="{SASL_user}" password="{SASL_password}";'    --Kafka SASL user name and password。
   );
   
   insert into kafka_table 
   select * from orders_datagen;
   ```
   

   * The code uses the Datagen connector to generate random data, simulating the log data that needs to be written. To learn more about this connector, please consult the [Datagen](https://docs.byteplus.com/docs/flink/Datagen) documentation.

   * The TLS log topic in the code uses the Kafka protocol to collect data; please fill in the TLS\-related information according to the table below.

      
      |**Configuration Option** |**Description** |
      |---|---|
      |connector |Specify the connector to be used.<br><br>TLS log topics collect logs via the Kafka protocol, thus it must be set to kafka. |
      |topic |Specify the target TLS topic for log writing, which is the topic ID. |
      |properties.bootstrap.servers |Specify the access address for the TLS log project in the format service address:port number, for example *tls\-ap\-southeast\-1.byteplus.com:9094*.<br><br><br>* Service address: The cloud product services used in this document are accessed through internal networks, so this address is set to the private network address of the log project.<br><br>* Port: Logs are written to the TLS topic, thus the fixed port is 9094. |
      |format |The format used for deserializing the message body (value) from Kafka. Here, it is set to json. |
      |properties.enable.idempotence |Whether to enable Kafka Client's transaction message capability, set to **false** here to disable transaction messages. |
      |properties.security.protocol |Uses the SASL_SSL connection protocol to ensure secure log transmission. |
      |properties.sasl.mechanism |Configure the SASL mechanism to PLAIN. |
      |properties.sasl.jaas.config |Configure JAAS.<br><br><br>* Username: Kafka SASL username. Configure as the ID for the log project.<br><br>* Password: Kafka SASL user password. Configure as the BytePlus Engine account key, format `${access-key-id}#${access-key-secret}`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">It is recommended to configure keys for sub\-users (IAM users) to reduce security risks.</div><br> |
      

4. Click the **Format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more attractive, tidy, and readable.

5. At the top of the code editing area, click the **Validate** button.

   The system will automatically verify the correctness of your SQL statements; if there are errors, please modify the SQL statements based on the prompts. After the verification passes, the system indicates **success**.

6. (Optional) Debug tasks.

   The validation function can only verify the correctness of SQL syntax, not completely avoid possible errors during code execution; it is advisable to debug your tasks before going live.

   1. In the **Task Development** section, select the target SQL task, then at the top of the editing area select the correct **execution mode** and **engine version**, and click the **Debug** button.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Choose the execution mode as <strong>STREAMING</strong> for Flink Stream type tasks; choose the execution mode as <strong>BATCH</strong> for Flink Batch type tasks.      </div>
      

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/242a87f09fcc46aa9c0801d4079b8ed4~tplv-goo7wpa0wc-image.image" width="714px" /></div>



2. In the **Debug Task** dialog, choose the **Use Online Data** debug type, then select the **Session Resource Pool**, and click **Confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcf6af3f76864917ac0c5a1954db856f~tplv-goo7wpa0wc-image.image" width="710px" /></div>



3. View the results of the task debugging, then click the red task stop button.

   The system returns to the task editing page, where you can view the task debugging results below the editing area. Once the task results meet expectations, please stop debugging promptly to avoid prolonged resource occupancy.

4. Launch task.

   1. In the task editing area, click the **Go Live** button above.

   2. In the **Task Go Live settings** dialog, select the Flink resource pool, set task priority, and scheduling policy, then click **OK**.

      The system will indicate that the task has successfully gone live, and you can go to the **Task Management** page to view it.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2578a736b16540008fad9808ba7dbabf~tplv-goo7wpa0wc-image.image" width="699px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Run resource pool |Select a Flink resource pool for the task to run from the dropdown menu. |
  | | | \
  |Task Priority |\
  | |The system's default preset priority is L3. You can set the task priority as needed; the smaller the number, the higher the priority. |\
  | |Task priority determines the internal scheduling order of tasks, with higher priority tasks being scheduled first, i.e., L3 is scheduled before L4. |
  | | | \
  |Scheduling Strategy |Configure the task scheduling strategy based on your needs: |\
  | | |\
  | |* GANG: Ensures that all instances of a task are scheduled together, meaning resources are allocated only when the remaining resources are sufficient to support the normal operation of the task; if not, resources are not allocated. |\
  | |   This strategy prevents the issue of resources being allocated but the task failing to start, thereby solving the problem of resource deadlock. |\
  | |* DRF: Considers multiple dimensions of resources to fairly distribute resources to various tasks within the resource pool, thereby enhancing utilization. |\
  | |   For example: With remaining resources of 10 cores and 40 GB, Task A requires 10 cores and 20 GB; Task B requires 2 cores and 8 GB. If assigned to A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would opt to assign to B, allowing the remaining 8 cores and 32 GB to be used for subsequent tasks. |
  | | | \
  |Scheduling Duration |\
  | |When set to GANG scheduling strategy, it's necessary to set the scheduling duration. |\
  | |If the scheduling duration is exceeded, the task will fail to schedule. If set to 0, it will keep retrying. |
```



3. In the project's left navigation bar, select **Task Operations & Management \> Task Management**, and then click the **Start** button behind the target task.

4. In the **Start Task** dialog, select the task start mode, then click **OK**.

   Starting the task will take some time, please be patient. After successful startup, the status is **Running**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12cf002541b7470b9925b913ad0f6479~tplv-goo7wpa0wc-image.image" width="708px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Startup Method |Please choose the task startup method based on the actual situation: |\
  | | |\
  | |* Start from the latest state: Initiate using the latest Checkpoint or Savepoint. |\
  | |* Fresh start: Initiate directly without using Checkpoint or Savepoint. |\
  | |* Start from a specified snapshot: Initiate using a targeted snapshot (Savepoint). |\
  | | |\
  | |:::tip |\
  | |The initial task launched must be in **entirely new startup** mode. |\
  | |::: |
  | | | \
  |Parameter Configuration |Task carries the parallelism, Task Manager, and Job Manager resource configuration on the development side. Supports updating your configuration and swiftly making it effective when starting tasks. |\
  | |:::tip |\
  | |After updating the parameter settings and starting the task, a new task version will be added, and the latest settings will be synchronized to the task development side. |\
  | |::: |\
  | | |\
  | |* Parallelism: Global concurrency of tasks. |\
  | |* Single TaskManager CPU count: The number of CPU cores per single TaskManager. |\
  | |* Single TaskManager memory size: The amount of memory occupied by a single TaskManager. |\
  | |* Number of Slots per TaskManager: The number of slots in a single TaskManager. |\
  | |* JobManager CPU Count: The number of CPU cores in a single JobManager. |\
  | |* JobManager Memory Size: The memory footprint of a single JobManager. |
  | | | \
  |More Settings |When adding or modifying operators during task development changes, it may prevent the task from recovering from snapshots. In this case, you can choose to enable the **Allow Ignoring Partial Operator States** feature to ensure the task runs smoothly. |\
  | |![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aac2567c34fa443cb08ff50621508483~tplv-goo7wpa0wc-image.image =1380x) |\
  | |:::warning |\
  | |* Only when selecting **specified snapshot startup** or **start from the latest state** options is it possible to check to ignore certain operator statuses. |\
  | |* When you choose the **fresh start** mode, ignoring operator state is not supported. |\
  | |::: |
```


<span id="1970fa77"></span>
### Development Task: Consume Messages

The development process for consuming messages is similar to that for producing messages. Please refer to the steps above to independently complete task development, debugging, running, etc., to achieve reading TLS topic data and writing to ESCloud Index.

This section only introduces precautions and provides sample code:


* When creating a task, the task name can be named `TLS9093-ESCloud`, and the engine version should still select **Flink 1.11\-byted**.

* Sample code for the task is as follows, please fill in the connection information for TLS and ESCloud according to the actual situation.

   ```SQL
   create table kafka_table (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
   ) WITH (
     'connector' = 'kafka',
     'topic' = 'out-8899**e809edba7',  -- Kafka protocol consumer topic ID for TLS topic
     'properties.bootstrap.servers' = 'tls-cn-beijing.byteplus.com:9093',  --TTLS log project access point address. The port is fixed at 9093
     'scan.startup.mode' = 'earliest-offset',
     'scan.topic-partition-discovery.interval' = '120s',   -- The interval for periodically scanning and discovering new topics and partitions
     'format' = 'json',
     'properties.security.protocol' = 'SASL_SSL',
     'properties.sasl.mechanism' = 'PLAIN',
     'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="{SASL_user}" password="{SASL_password}";'
   );      --Kafka SASL user name and password
   
   create table escloud_table (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
   ) WITH (
     'connector' = 'elasticsearch-7',  -- The connector version must be the same as the instance version to avoid incompatibility issues
     'hosts' = 'http://elasticsearch-g**m.escloud.byteplus.com:9200',     -- Instance address
     'index' = 'test_orders_3',    -- Index name. No need to create the index in advance, the instance will be created automatically
     'username' = 'admin',         -- Instance access user name
     'password'='cdq***56'         -- Instance access user password
   );
   
   insert into escloud_table
   select * from kafka_table;
   ```
   

   
   |**Purpose** |**Configuration Item** |**Description** |
   |---|---|---|
   |Connect to TLS Topics |connector |Specify the connector to use.<br><br>The purpose is to consume a TLS log topic as a Kafka Topic, so it must be set to kafka. |
   ||topic |Specify the target TLS topic for reading log data, valued as the Kafka protocol consumption topic ID. |
   ||properties.bootstrap.servers |Specify the access address of the TLS log project, formatted as `service address:port number`, such as `tls-cn-beijing.byteplus.com:9093`.<br><br><br>* Service address: The cloud product services used in this document all use internal network access, so this address is set to the private network address of the log project.<br><br>* Port: Read the log data from the TLS topic, thus the port is fixed at 9093. |
   ||scan.startup.mode |Startup mode when reading data. The value here is set to earliest\-offset, which means reading from the earliest partition in Kafka. |
   ||format |Format used to deserialize the Kafka message body (value). The setting here is json. |
   ||properties.security.protocol |Use the SASL_SSL connection protocol to ensure the security of log transmission. |
   ||properties.sasl.mechanism |Configure the SASL mechanism to PLAIN. |
   ||properties.sasl.jaas.config |Configure JAAS.<br><br><br>* Username: Kafka SASL username. Configure as the ID of the log project for the log service.<br><br>* Password: Kafka SASL user password. Should be configured as the BytePlus Engine account key, in the format `${access-key-id}#${access-key-secret}`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">It is recommended to set the keys as those of a sub\-user (IAM user) to reduce security risks.</div><br> |
   |Connect to ESCloud Index |connector |Specify the connector to be used.<br><br>Data needs to be written into the ESCloud Index, so here the connector chosen is `elasticsearch-7`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The version of the connector here needs to match the version of the cloud search service instance to avoid version conflicts.</div><br><br><br><div data-tips="true" data-tips-type="warning">The version of the cloud search service instance is <strong>7.10.2</strong>, and the corresponding connector version is <strong>elasticsearch\-7</strong>.</div><br> |
   ||hosts |Instance access address. |
   ||index |Index name for data entry.<br><br>There is no need to create the index in advance; the system will generate it automatically. |
   ||username |Instance access user. |
   ||password |Password of the instance access user. |
   


<span id="5f0ede34"></span>
## Result Verification

This article has created two tasks, one responsible for producing messages and the other for consuming messages. You can retrieve the data written on the TLS side to verify the production messages; you can also query the ESCloud Index on the Kibana Web page to verify the consumption of TLS logs.

<span id="e07b67b5"></span>
### Retrieve TLS Logs

Once the task responsible for producing messages is running normally, you can go to the log service console to retrieve the TLS logs, thereby determining if random data has been written.


1. Log in to the Log Service Console.

2. In the left navigation bar, click **Log Project Management**, then click on the name of the target log project.

3. In the log project's left navigation bar, select **Search & Analysis**, choose the log topic, then click on **Index Settings** on the right.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6c3d7c659b14502a65ad6a72ae4ff33~tplv-goo7wpa0wc-image.image" width="754px" /></div>



4. In the **Index Settings** panel, check the **Index Status** **Enable** checkbox, then check the **Full\-text Index** checkbox, and finally click **OK** at the bottom right.

   For more information about search and analysis, please refer to [Log Retrieval](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9f70af4ad954e66a19ccbe2d303c81b~tplv-goo7wpa0wc-image.image" width="752px" /></div>



5. On the **Search & Analysis** page, click the **Search & Analysis** button.

6. View the search and analysis results of the log topic, as well as the original logs.


<span id="a152dd1e"></span>
### Query ES Index data

Once the task of consuming information runs smoothly, you can log into the Kibana Web page to check if TLS log data is written in the index (`test_orders_3`).


1. Log in to the Cloud Search Service Console.

2. Select the target region in the top navigation bar.

3. On the **instances list** page, select the target instance, then click **Kibana** behind the instance.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b9b102e29d942d990fc3aa544b22ab6~tplv-goo7wpa0wc-image.image" width="764px" /></div>



4. On the Kibana login page, enter your username and password, click **Log In** to log into Kibana.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default username is admin, and the password is set during instance creation.   </div>
   

5. In Kibana Web page, select **Dev Tools** from the left navigation bar, then enter GET /test_orders_3/_search in the left code area of Console, an\*\*\*\*`GET /test_orders_3/_search in the left code area of Console`, and click the execute button.

   When a message similar to the following is returned, it indicates successful data retrieval from the TLS Topic and writing to the ES Index.

   ```SQL
   {
     "took" : 545,
     "timed_out" : false,
     "_shards" : {
       "total" : 1,
       "successful" : 1,
       "skipped" : 0,
       "failed" : 0
     },
     "hits" : {
       "total" : {
         "value" : 1410,
         "relation" : "eq"
       },
       "max_score" : 1.0,
       "hits" : [
         {
           "_index" : "test_orders_3",
           "_type" : "_doc",
           "_id" : "fBh-NYc**i2l",
           "_score" : 1.0,
           "_source" : {
             "order_id" : 9316,
             "order_product_id" : 956,
             "order_customer_id" : 798,
             "order_status" : "316",
             "order_update_time" : "2023-03-31 10:28:35.558"
           }
         },
         ......
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d3c7b3f69134da2a72308abb7d4db6a~tplv-goo7wpa0wc-image.image) </span>
