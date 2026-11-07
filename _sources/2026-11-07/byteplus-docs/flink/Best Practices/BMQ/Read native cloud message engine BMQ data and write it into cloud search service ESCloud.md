---
title: "Read native cloud message engine BMQ data and write it into cloud search service ESCloud"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Read_native_cloud_message_engine_BMQ_data_and_write_it_into_cloud_search_service_ESCloud"
---

This article explains how to use a simple BytePlus Flink SQL task to read real\-time data from a BMQ Topic and then write it into an ESCloud Index.

<span id="40c1e24e"></span>
## Process Introduction

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTY1IDY1Ij48ZGVmcy8+PGc+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Qk1RIFRvcGljPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyMjIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAyMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RVNDbG91ZCBJbmRleDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDQyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZsaW5rIFNRTDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMzIgMjcuNzEgTCAxODAuNDEgMjcuNzEgTCAxODAuNDEgMjIgTCAyMTIgMzIgTCAxODAuNDEgNDIgTCAxODAuNDEgMzYuMjkgTCAxMzIgMzYuMjkgWiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzUyIDI3LjcxIEwgNDAwLjQxIDI3LjcxIEwgNDAwLjQxIDIyIEwgNDMyIDMyIEwgNDAwLjQxIDQyIEwgNDAwLjQxIDM2LjI5IEwgMzUyIDM2LjI5IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />


1. Prepare the data source BMQ Topic.

   You need to create a resource pool, Topic, and Consumer Group in the native cloud message engine console and obtain the resource pool access point address.

2. Prepare the data destination ESCloud Index.

   You need to purchase an instance in the cloud search service console and obtain the instance's access address. No need to manually create an Index, as the system's dynamic mapping capability will automatically create the index.

3. Develop Flink SQL tasks.

   Once you have prepared the data sources and destinations, you can develop SQL tasks on the BytePlus Flink console, achieving data reading from BMQ and writing to ESCloud through simple code logic.


<span id="fe3212c9"></span>
## Prerequisites

To ensure network access security, the cloud product services used in this article are accessed via an internal network, thus requiring the BMQ resource pool, cloud search service instance, and Flink resource pool to be in the same VPC within the same region.

You can create a private network before creating cloud resources. For related documentation, please see [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

<span id="fbe6885e"></span>
## Step One: Prepare the BMQ Topic data source.


1. Log in to the [Cloud Native Messaging Engine Console](https://console.byteplus.com/bmq).

2. Select the target region from the top menu bar, then enter the target project from the **Project Management** page.

3. Create a resource pool.

   1. In the project's left navigation bar, select **Resource Management**, then click **Create Resource Pool**.

   2. On the **Create Resource Pool** page, set the basic information, resource configuration, network information, Topic configuration, and other key parameters, then click **Next: Confirm Order**.

      
      |**Primary configuration item** |**Secondary configuration item** |**Description** |
      |---|---|---|
      |Basic Information |Resource Type |Defaults to **general resources**. |
      ||Resource Mode |Default to **VCI mode**, which involves creating a BMQ resource pool on the general resources\-VCI resource domain. |
      ||Billing Type |Choose the type of resource pool billing. Currently only supports **pay\-as\-you\-go**. |
      ||Resource Pool Name |Enter the resource pool name.<br><br><br>* Consists of lowercase letters, numbers, and hyphens (\-).<br><br>* Length of 1 to 64 characters. |
      ||Deployment in regions and availability zones. |The region has been selected and cannot be changed.<br><br>Based on the requirements for network latency, high availability disaster recovery, select **single availability zone** or **multiple availability zones**.<br><br><br>* Single availability zone: Simply choose a suitable availability zone.<br><br>* Multiple availability zones: Multiple availability zones are selected by default. |
      ||Associated project. |Select the project that the resource pool belongs to from the dropdown list. |
      |Resource configuration. |Computing Specifications |Based on the business scenario, estimate the required number of Topics, Consumer Groups, and partitions, and select the appropriate resource pool specifications. |
      ||Storage Specifications |By default, CloudFS accelerated storage is used and no additional configuration is required. |
      |Network Information |Private Network |To ensure smooth access to the internal network, it is recommended to choose a VPC located in the region where existing cloud services operate. Within the same VPC, subnets across different availability zones are interconnected.<br><br>If a private network has not been created yet, please refer to [creating a private network](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
      ||Subnet |Select a subnet from the dropdown menu. The system automatically filters available subnets based on your selected region, availability zone, and private network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the resource pool is deployed across multiple availability zones, a subnet must be configured for each selected availability zone.</div><br> |
      ||Security Group |Select a security group from the dropdown menu. |
      |Topic Configuration |Message Retention Duration |Set the default message retention duration for all Topics under this resource pool.<br><br><br>* The default is 72 hours and can be adjusted on an hourly basis.<br><br>* The supported retention range is 1 to 336 hours (14 days). |
      

   3. On the **Order Details** page, confirm the resource pool configuration information, read and check the related product agreement, then click **Purchase Now**.

      After submitting the purchase order, you can return to the resource pool page. The purchased resource pool will be displayed as **Initializing**, and upon completion, it will be displayed as **Running**.

4. Obtain the access point address.

   1. On the **Resource Pool Management** page, click on the resource pool name to enter its details page.

   2. Under the **Service Access** tab on the resource pool details page, view and copy the user access point address of the resource pool.

5. Create Topic.

   1. In the left navigation bar of the resource pool details, select **Topic**, then click **Create Topic**.

   2. In the **Create Topic** dialog, set the name, number of partitions, message retention period, and then click **OK**.

      
      |**Configuration** |**Description** |
      |---|---|
      |Topic Name |Enter the topic name.<br><br>It must consist only of lowercase English letters, digits, underscores (_), and hyphens (\-), with a length of 3 to 64 characters. |
      |Description |Enter the description for the topic. |
      |Number of Partitions |Enter the number of partitions.<br><br>The default is 12, and the remaining number of available partitions is displayed under the input field. |
      |Message Retention Period |Data retention time in the Topic.<br><br><br>* By default, it aligns with the global message retention period set by the resource pool, but can also be adjusted independently by hourly increments.<br><br>* The supportable retention range is from 1 to 336 hours (14 days). |
      

6. Create a Consumer Group.

   1. In the resource pool details sidebar, select **Consumer Group**, and then click **Create Group**.

   2. In the **Create Group** dialog, set the Group name and description, and then click **OK**.

      
      |**Configuration** |**Description** |
      |---|---|
      |Group Name |Customize the Group name.<br><br><br>* Consists of lowercase English letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length is between 3 and 64 characters. |
      |Description |Enter description information. Not required. |
      


<span id="9a5423bb"></span>
## Step Two: Prepare data destination ESCloud Index.


1. Log in to the [Cloud Search Service Console](https://console.byteplus.com/es).

2. Select the target region in the top navigation bar.

3. Create an instance.

   1. On the **Instance List** page, click **Create Instance**.

   2. On the **Create Instance** page, set the instance name, availability zone, version, node details, and access methods, and then click **Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/974f2bfd10724f75a04cdb4f19b44b76~tplv-goo7wpa0wc-image.image" width="746px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Explanation** |
  |---|---|
  | | | \
  |Instance Name |Custom instance name, not required. If the instance name is not set, the default name will be the same as the instance ID. |\
  | |When custom setting an instance name, the value description is as follows: |\
  | | |\
  | |* Cannot start with a number or a hyphen (-). |\
  | |* Can only contain Chinese characters, numbers, letters, hyphens (-), and underscores (_). |\
  | |* The length must be within 1 to 128 characters. |
  | | | \
  |Available zone |Select the available zone where you want to create the instance. |
  | | | \
  |Version |Compatible with **6.7.1** and **7.10.2** Elasticsearch versions. |\
  | |Select version 7.10.2 as an example here. |
  | | | \
  |Deployment node type |Supports the following node types: |\
  | | |\
  | |* **Data node**: Default configuration includes 3 data nodes, each with a storage specification of 100 GiB. |\
  | |* **Dedicated Master Nodes**: Choose whether to enable dedicated master nodes, which are used to ensure instance stability. After enabling dedicated master nodes, you need to select the configuration specifications for the nodes. |\
  | |* **Kibana Node**: The system provides a free Kibana node with 1 core and 2 GiB, which cannot be modified. |
  | | | \
  |Node Details |Configure data nodes or dedicated master nodes specifications. |\
  | | |\
  | |* Node specifications: Different specifications include different numbers of CPU cores and memory. Choose the node specifications that suit your business needs. |\
  | |* Storage type: Currently only **ESSD-PL0** is supported. |\
  | |* Storage specifications: Set the storage specifications, ranging from 20 to 10,000 GiB. |\
  | |* Number of nodes: Set the number of nodes based on business requirements. |\
  | | |\
  | |:::tip |\
  | |* Without dedicated master nodes: It is recommended that production environments have at least 3 data nodes. Configuring 2 nodes poses a risk of split-brain, and the supported number of nodes ranges from 1 to 70. |\
  | |* With dedicated master nodes: The number of data nodes that can be configured ranges from 1 to 70, with no other restrictions; there are always 3 dedicated master nodes. |\
  | |::: |
  | | | \
  |Access Methods |Supports three types of access: sales area, storage intranet, and public service area. |\
  | | |\
  | |* Sales area access: Within the private network VPC, instances can be accessed, and this access method is chosen in this article. |\
  | |* Storage intranet access: Default support for physical machine access, cannot be modified. |\
  | |* Public service area access: Machines in the public service area can access. |
  | | | \
  |Private Network |When selecting **sales area access** for cloud search service instances, a specific VPC must be chosen to access the instance. To ensure smooth intranet access, it is necessary to select a VPC consistent with the existing BMQ resource pool. |\
  | |:::tip |\
  | |* Once an instance is created, the private network cannot be changed. |\
  | |* Within the same VPC, subnets in different availability zones are interconnected. |\
  | |::: |
  | | | \
  |Subnet |The system will automatically filter available subnets based on the region, availability zone, and private network you select. |
  | | | \
  |Project Ownership |Select the project that the cloud search instance belongs to for easier resource management; this is optional. |
  | | | \
  |Username |The default is admin, and it cannot be changed. Used for logging into the Kibana page, as well as instance authentication. |
  | | | \
  |Login Password |The password corresponding to the admin account, please set it according to the rules and store it securely. |\
  | | |\
  | |* The password must include at least three of the following: uppercase letters, lowercase letters, numbers, and special characters, with a length of 8 to 32 characters. |\
  | |* Supports special characters `_#!@$%^&*()+=-` and cannot include spaces or Chinese characters. |
  | | | \
  |Confirm Password |Enter the password you entered in the previous step. |
  | | | \
  |Transmission Protocol |Select the transmission protocol to either **HTTP** or **HTTPS**. |\
  | |:::warning |\
  | |In Flink tasks, **instances that currently do not support HTTPS transport protocol** are set to use HTTP. If an HTTPS access address for ES is configured in a Flink task, the task will fail. |\
  | |::: |
  | | | \
  |Delete Protection |Choose whether to enable delete protection; it is disabled by default. |\
  | |Delete protection is designed to prevent accidental deletion of instances; thus, you cannot delete instances while this option is enabled. |
  | | | \
  |Billing Type |Select the billing type for the instance, supporting **pay-as-you-go** and **annual and monthly subscription**. For detailed information about billing, please refer to [Billing Overview](https://docs.byteplus.com/en/docs/cloudsearch/billing-overview). |
```



3. On the **Confirm Order** page, review the instance configuration details, read and check the relevant product agreements, and then click **Purchase Now**.

   After successfully purchasing the instance, you can click **Go to Console**, and the page will automatically redirect to the **Instance List** page, making it easy to view the instance you just created. When an instance changes from **Creating** to **Running**, it indicates that the instance has been successfully created.

4. Obtain the instance access address.

   1. On the **Instance List** page, click on the instance name to enter the instance details page.

   2. In the Service Access area under the Instance In\*\*\*\* **Service Access area under the Instance Information** tab, view and copy the instance access address.

      Flink SQL tasks require this address to access the instance.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95d661c1375447d299d7efd4f4d183f8~tplv-goo7wpa0wc-image.image" width="730px" /></div>



3. You can also click **Enable Public Access** behind the **Kibana Public Access Address** and then select the public IP you need to bind.

   Enable public access for Kibana to subsequently log in to the Kibana Web page and query data in the Index. If you do not have an available public IP, you can go to the console to create one. For related documents, please refer to [Application for Public IP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id="a989e2b3"></span>
## Step Three: Develop Flink SQL Tasks


1. Log in to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar, then enter the project from the **Project Management** page.

3. Create a resource pool.

   1. In the left\-side navigation bar of the project, select **Resource Management**, then click on the **Resource Pool** tab, and finally click on **Create Resource Pool**.

   2. On the **Create General Resource Pool** page, set the basic information, network information, storage information, and other parameters for the resource pool, then click **Next: Confirm Order**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6a1c6d22cbf4c6a92b1ad42ec8eae71~tplv-goo7wpa0wc-image.image" width="738px" /></div>


```Plain Text
  | | | | \
  |**Primary Configuration Item** |**Secondary Configuration Item** |**Description** |
  |---|---|---|
  | | | | \
  |Basic Information |Resource Type |Default is **General Resource**. |
  |^^| | | \
  | |Resource Mode |Default is **VCI Mode**, meaning deploying Flink resource pool on a general resource-VCI resource domain. |
  |^^| | | \
  | |Billing Type |\
  | |  |In the Universal Resources - VCI Resource Domain, deploy Flink resource pools that support **pay-as-you-go** and **subscription** billing types; please select as needed. |\
  | | |If you need billing details, please refer to [Pay-As-You-Go](/docs/flink/Pay-As-You-Go) and [Annual and Monthly Subscription](/docs/flink/Annual_and_Monthly_Subscription). |\
  | | |If you choose the subscription billing type, you also need to select **purchase duration** and confirm whether **automatic renewal** is required. |
  |^^| | | \
  | |Resource Pool Name |Enter the name of the resource pool to be created. |\
  | | | |\
  | | |* Must be globally unique and cannot be an empty string. |\
  | | |* The length must be between 1 and 63 characters. |\
  | | |* Supports lowercase English letters, digits, and hyphens (-); and the name must start and end with a letter or digit. |
  |^^| | | \
  | |Region and Availability Zone |* The region is fixed and cannot be changed. Keep the BMQ resource pool and cloud search service instance in the same region. |\
  | | |* Choose a suitable availability zone based on the network latency, high availability, and other requirements of the business. |
  |^^| | | \
  | |Associated project |Select the project to which the resource pool belongs from the dropdown list. |
  | | | | \
  |Resource Configuration |Compute Specifications |If you create a **subscription-based** billing type, you need to manually configure resources for the Flink resource pool. The basic unit of resources is CU, where 1 CU means: 1 CPU core, 4 GB of memory. |\
  | | |Please set the amount of resources according to actual needs. |
  | | | | \
  |Network Information |Private Network |Select a private network from the dropdown list. It is necessary to keep BMQ resource pools and cloud search service instances within the same VPC. |
  |^^| | | \
  | |Subnet |\
  | |  |Select a subnet from the dropdown list. |\
  | | |The system will automatically filter the available subnets based on the region, availability zone, and private network you select. |
  |^^| | | \
  | |Security Group |Select a security group from the dropdown list. |
  | | | | \
  |Storage Information |TOS Object Storage |Defaults to the TOS associated at product initialization and cannot be modified. |
```



3. On the **Details** page, view the configuration details of the resource pool, read and check the Flink\-related agreements, then click **Purchase Now**.

   You can return to the resource pool list page to check the creation progress. Once the creation is complete, it will display as **Running**.

4. Development Task.

   1. In the left sidebar of the project, select **Task Development \> Tasks**, then click the plus button to create a task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75bce31de860456ab28bd6b8e7fdde02~tplv-goo7wpa0wc-image.image" width="746px" /></div>



2. In the **Create Task** dialog, set the task name, type, folder, and engine version, then click **OK**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a9db98c21f1417ba86b176fcffeb9bb~tplv-goo7wpa0wc-image.image" width="748px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/803b6aed01694bb29e67690d1b92272a~tplv-goo7wpa0wc-image.image" width="734px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Instructions** |
  |---|---|
  | | | \
  |Task Name |Customize the name of the task. |\
  | |The character length of the name is limited from 1 to 48, supporting numbers, upper and lower case letters, underscores (_), hyphens (-), and periods (.), and must start and end with a number or letter. |
  | | | \
  |Task Type |Select **Flink Task > Flink Stream > SQL**. |
  | | | \
  |Folder |The system provides folder management features for categorizing tasks. You can directly select the existing default **Data Development Folder**. |\
  | |If you have requirements to manage folders you create, please click the "create folder" button and then create the folder. |
  | | | \
  |Engine Version |Currently, we support **Flink 1.11-byted** and **Flink 1.16-byted** versions. |\
  | |:::warning |\
  | |If you connect to BMQ resources through the Kafka connector and are using the Flink 1.16-byted engine version, you must set the `properties.enable.idempotence` parameter to **false** to disable idempotence, otherwise the task will fail to run. |\
  | |::: |
  | | | \
  |Task Description |Enter the description of the task, which generally describes the functionality of the task. |
```



3. Write the business logic code for the SQL task in the task editing area.

   Here, you can directly copy and use the following code. The code implementation writes random numbers generated in real\-time by the datagen connector into the BMQ Topic first; then it reads data from the BMQ Topic and outputs it to the ESCloud Index.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When using the Kafka connector to read and write data to the BMQ Topic, if you use the Flink 1.11 engine version, you can directly use the following demo. If you use the Flink 1.16 engine version, you need to add the configuration (<code><em>'properties.enable.idempotence'</em></code><code>=</code><code><em>'false'</em></code>) to disable idempotence, otherwise the task will fail.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When writing data to Elasticsearch, if you use the elasticsearch\-7 connector, you can directly use the following demo. If you use the elasticsearch\-6 connector, you need to add a configuration (<code><em>'document-type'</em></code><code>=</code><code><em>'test'</em></code>) to specify the document type.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The version of the Elasticsearch connector used needs to match the version of the Cloud Search instance you created; otherwise, there may be a version incompatibility issue. The example code used the elasticsearch\-7 connector, so the corresponding Cloud Search instance version should be 7.10.2.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, ES instances supporting HTTPS transport protocol are temporarily not supported in Flink tasks.   </div>
   

   ```SQL
   CREATE TABLE orders_datagen (
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
     'fields.order_product_id.max' = '1000',
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
     'topic' = 'topic-a',
     --Topic name.
     'properties.bootstrap.servers' = 'bmq-****q5-1.xxxx.byteplus.com:9092',
     --Resource pool access point address.
     'properties.group.id' = 'group-a',
     --BMQ Consumer Group name. Need to be created in advance, otherwise the Offset cannot be submitted normally.
     'scan.startup.mode' = 'earliest-offset',
     'scan.topic-partition-discovery.interval' = '120s',
     --The time interval for regularly scanning and discovering new Topics and Partitions.
     'format' = 'json'
   );
   
   
   INSERT INTO
     bmq_table
   SELECT
     *
   FROM
     orders_datagen;
   
   
   CREATE TABLE escloud_table (
     order_id BIGINT,
     order_product_id BIGINT,
     order_customer_id BIGINT,
     order_status VARCHAR,
     order_update_time TIMESTAMP
   ) WITH (
     'connector' = 'elasticsearch-7',
     --Connector version, which needs to be the same as the instance version to avoid incompatibility issues.
     'hosts' = 'http://elasticsearch-pt8y***g3mi.escloud.bytepluse.com:9200',
     --Instance access address. ES instances using the HTTPS transport protocol are not currently supported in Flink tasks.
     'index' = 'test_orders',
     --Index name. No need to create an index in advance, the instance will be created automatically.
     'username' = 'admin',
     --Instance access user name.
     'password' = 'cd****456' --User password.
   );
   
   
   INSERT INTO
     escloud_table
   SELECT
     *
   FROM
     bmq_table;
   ```
   

4. Click the **Format** button, and the system will automatically adjust the SQL code format.

   The system will automatically beautify your SQL statements, making them more elegant, neat, and readable.

5. At the top of the code editing area, click the **Verify** button.

   The system will automatically validate the correctness of your SQL statements. If there are errors, please modify the SQL statements according to the prompts. After the inspection is passed, the system prompts `success`.

6. Start the task.

   1. In the task editing area, click the **Go Live** button above.

   2. In the **Task Launch Settings** dialog, select the runtime resource pool, set the task priority, and scheduling strategy, then click **Confirm**.

      The system will indicate that the task launch was successful, and you can go to the **Task Management** page to check.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3889e9630fd4579b43f93ed50708f46~tplv-goo7wpa0wc-image.image" width="716px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Resource Pool |Select the Flink resource pool for task operation from the dropdown list. |
  | | | \
  |Task Priority |\
  | |The default preset priority is L3. You can set task priority as needed; the smaller the number, the higher the priority. |\
  | |Task priority determines the internal scheduling order of tasks, with higher priority tasks being scheduled first, i.e., L3 before L4. |
  | | | \
  |Scheduling Strategy |Configure the task scheduling strategy based on the demands: |\
  | | |\
  | |* GANG: Ensures all instances of a task are scheduled together, allocating resources only when remaining resources meet the normal operational needs of the task; if not, resources are not allocated. |\
  | |   This strategy prevents the phenomenon where resources are allocated but the task cannot start, resolving resource deadlock issues. |\
  | |* DRF: Considers multi-dimensional resources to more fairly distribute resources among tasks within a resource pool, thus enhancing utilization. |\
  | |   For example: with remaining resources of 10 cores and 40 GB, Task A requires 10 cores and 20 GB; Task B needs 2 cores and 8 GB of resources. If allocated to Task A, the remaining 0 cores and 20 GB cannot be utilized; the DRF strategy would opt to allocate to Task B, leaving 8 cores and 32 GB available for subsequent tasks. |
  | | | \
  |Scheduling Duration |\
  | |When setting the GANG scheduling strategy, it is necessary to set the scheduling duration. |\
  | |If it exceeds the scheduling duration, the task will fail to schedule. If set to 0, it will keep retrying. |
```



3. In the project's left navigation bar, choose **Task Operations \> Task Management**, and then click the **Start** button behind the target task.

4. In the **Start Task** dialog, select the startup mode of the task, then click **Confirm**.

   Starting the task takes some time, please be patient. After a successful start, the status will be **In Progress**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92262e7c2d7941cfa9f6d66aa4c8317c~tplv-goo7wpa0wc-image.image" width="742px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Startup Mode |Please select the task startup mode based on the actual situation: |\
  | | |\
  | |* Start from the latest state: Start with the latest Checkpoint or Savepoint. |\
  | |* Start fresh: Start without using a Checkpoint or Savepoint. |\
  | |* Start from a specified snapshot: Launch by specifying the target snapshot (Savepoint). |\
  | | |\
  | |:::tip |\
  | |Tasks that are launched for the first time can only be started in a **fresh start** mode. |\
  | |::: |
  | | | \
  |Parameter Configuration |Task carries parallelism on the development side, and resource configuration for Task Manager and Job Manager. When launching tasks, it supports updating your configuration and taking effect quickly. |\
  | |:::tip |\
  | |After updating the parameter configuration and starting the task, a new task version will be added, and the latest configuration will be synchronized to the task development side. |\
  | |::: |\
  | | |\
  | |* Parallelism: global concurrency of tasks. |\
  | |* Single TaskManager CPU count: the number of CPU cores for a single TaskManager. |\
  | |* Single TaskManager memory size: the memory size occupied by a single TaskManager. |\
  | |* Single TaskManager slot count: the number of slots in a single TaskManager. |\
  | |* JobManager CPU count: the number of CPU cores for a single JobManager. |\
  | |* JobManager memory size: the memory size occupied by a single JobManager. |
  | | | \
  |More settings |When modifying or adding operators during task development, it may cause the task to be unable to recover from a snapshot. In this case, you can choose to enable the **Allow Ignoring Partial Operator States** feature to ensure the task runs smoothly |\
  | |![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02fd0b6e12f146d59aa14d8720f2392f~tplv-goo7wpa0wc-image.image =1380x) |\
  | |:::warning |\
  | |* Only when the launch methods **specified snapshot start** or **start from the latest state** are selected, is it supported to check ignoring the state of certain operators. |\
  | |* When you choose the **fresh start** mode, ignoring the operator state is not supported. |\
  | |::: |
```


<span id="d2081285"></span>
## Result verification.

You can log into the Kibana Web page to check if the randomly generated data has been successfully written into the index `test_orders`.


1. Log into Cloud Search Service Console.

2. Select the target region from the top navigation bar.

3. On the **Instance List** page, select the target instance and then click on **Kibana** behind the instance.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d9f0b5f6f8c4b539c945f77de4e2486~tplv-goo7wpa0wc-image.image" width="768px" /></div>



4. On the Kibana login page, enter your username and password, click on **Log In**, and log into Kibana.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The username is admin, and the password is the one set when the instance was created.   </div>
   

5. In the left navigation bar of the Kibana Web page, select **Dev Tools**, then in the code area to the left of **Console**, type `GET /test_orders/_search` and click the execute button.

   When a message similar to the following is returned, it indicates that data has been successfully read from the BMQ Topic and written into the ESCloud Index.

   ```SQL
   {
     "took" : 1125,
     "timed_out" : false,
     "_shards" : {
       "total" : 1,
       "successful" : 1,
       "skipped" : 0,
       "failed" : 0
     },
     "hits" : {
       "total" : {
         "value" : 2546,
         "relation" : "eq"
       },
       "max_score" : 1.0,
       "hits" : [
         {
           "_index" : "test_orders",
           "_type" : "_doc",
           "_id" : "sBiE2o****WUSExIw",
           "_score" : 1.0,
           "_source" : {
             "order_id" : 1967,
             "order_product_id" : 293,
             "order_customer_id" : 493,
             "order_status" : "3b5",
             "order_update_time" : "2023-03-13 18:21:44.248"
           }
         },
         ......
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c53883fa8bfe416893f267d977084d12~tplv-goo7wpa0wc-image.image) </span>
