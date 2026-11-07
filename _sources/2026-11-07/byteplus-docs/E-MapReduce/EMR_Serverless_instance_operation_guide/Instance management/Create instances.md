---
title: "Create instances"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_instances"
---

On the Serverless OLAP service page, you can quickly create a StarRocks/Doris instance. This allows you to rapidly obtain a fully managed, high\-performance instance environment without the need to build or maintain infrastructure yourself, enabling effortless large\-scale data analysis and queries.

<span id="_1-前提条件"></span>
# **prerequisites**

IAM cross\-service authorization has been completed:


* Log in to the [EMR Serverless OLAP console](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/list) with the primary account and complete service role creation[ServiceRoleForEMROLAP](https://docs.byteplus.com/docs/undefined/68da347242e561058e05696d) .

* To create an OLAP instance using a sub\-account, grant the corresponding sub\-account the EMROLAPFullAccess permission. See [Permission control in the management console: Grant permissions to IAM users](https://docs.byteplus.com/docs/E-MapReduce/si_permission_control).


<span id="_2-操作步骤"></span>
# procedure


1. After logging in to the EMR console, click ResourcesServerless on the left. On the EMR Serverless page, click “Create resource”\>"Serverless instance" in the upper right corner. On the instance creation page, complete the relevant instance configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8981d4c5de143299894fcad7e7ce29e~tplv-goo7wpa0wc-image.image) </span>

2. Configure instance parameters on the instance creation page. The description for each configuration item is as follows.

   1. Configure resource information.

      
      |Configuration item |Description |
      |---|---|
      |Region |The created cluster and corresponding resources will be deployed in the specified region and cannot be modified. |
      |Availability zone |The availability zone where the instance is located. Different regions support different availability zones. |
      |instance name |Custom instance name. |
      |Version |The version of the product software stack. The latest software version is selected by default. |
      |Instance series |Currently, the data warehouse edition and multi\-warehouse edition are supported.<br><br><br>* The Data Warehouse Edition currently defaults to the integrated storage and compute mode.<br><br>* The multi\-warehouse edition currently only supports the storage\-compute separation mode. Starting from StarRocks version 3.1, storage\-compute separation is supported. After enabling this mode, you must also configure TOS account information and address. Data from internal tables in StarRocks will be stored in TOS. |
      |Engine |The currently supported engine types and versions. It is strongly recommended to use the latest version of the corresponding engine. |
      |Project |By default, all VPC resources under all projects are selected. You can also select resources under the corresponding project. |
      |VPC |Use the dropdown to select your existing private network to connect the newly created cluster instance, or you can create a new VPC.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system will automatically create a managed security group under this VPC, which by default allows the IPv4 CIDR block of the subnet. No additional configuration is required.</div><br> |
      |Subnet |Use the dropdown to select a subnet in the availability zone under the corresponding VPC. If there is no available subnet, click [Create subnet](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/subnet) to create one. |
      

   2. Configure payment information.

      
      |Configuration item |Description |
      |---|---|
      |Payment method |* Subscription (recommended): Prepaid mode. Specify the payment duration. After expiration, you can release or renew. You can also enable the **Auto renewal** feature. The default renewal duration is one month. Enabling this feature reduces manual renewal management costs and prevents service interruption caused by forgetting to renew.<br><br>* Pay\-As\-You\-Go: A postpaid mode, meaning you pay after usage. Nodes can be released at any time. Charges are based on the actual usage duration, billed hourly. Suitable for short\-term testing tasks or flexible dynamic tasks. |
      |Billing duration |In Subscription mode, select the payment duration, such as 1 month, 3 months, 6 months, or 1 year. |
      |Auto\-renewal |After enabling, auto renewal will be performed 7 days before expiration, with a renewal duration of one month. |
      

   3. Configure instance specifications.

      
      |Configuration item |Description |
      |---|---|
      |High availability |Set whether to enable the high availability deployment switch. After enabling it, FE nodes will be deployed with 3 or 5 nodes to ensure high availability of the service. It is strongly recommended to enable high availability in production environments. |
      |Node |Configure the resource settings for FE nodes and BE nodes, including compute specifications and storage specifications. Compute specifications support standard types, such as 8 vCPU.<br><br><br>* FE nodes: Standard and memory types are supported. After selecting the appropriate type, you can choose the instance specifications and cloud disk specifications, and set the number of nodes.<br><br>* BE nodes:<br><br>   * Standard, memory, compute, and high\-performance types are supported. After selecting the appropriate type, you can choose the instance specifications and cloud disk specifications, and set the number of nodes.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only after enabling the high availability switch can the 'High\-performance' type be selected.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">High\-performance compute nodes are local physical disk servers. Local disks carry the risk of hardware failures causing business data loss. It is recommended to complete a full backup of core business data in advance.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Disk anomalies may cause business data to become unavailable, resulting in query failures in the Doris client.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Additionally, when performing maintenance operations on local disk nodes, BE instances within the node may trigger a restart, and associated business tasks will be interrupted. Please ensure that business clients have an automatic retry mechanism to avoid blocking business processes.      </div><br>      <br><br>   * In addition, BE nodes also support additional performance configuration, increasing data disk throughput:<br><br>      * Limits: When selecting the 'Extreme' type, SSD FlexPL data disk ≥ 500 GiB, or when selecting the 'Throughput' type, SSD TL0 data disk ≥ 100 GiB, only then can the additional performance configuration switch be enabled.<br><br>      * After the instance is created, additional performance can be adjusted during runtime. |
      

   4. Configure advanced settings.

      
      |Configuration item |Description |
      |---|---|
      |Project Management |The project to which the cluster instance belongs. By default, default (default project) is selected. To assign the newly created cluster instance to a new project, use the dropdown to select, or create a new project directly. |
      |Operations window |The permitted time range for operations such as maintenance and management. For example, 00:00 \- 06:00. |
      |Label |Optional configuration. You can add tags to the instance for easier resource management. Up to 20 tags can be added. |
      

3. Confirm the configuration information and fees, check the box to indicate you have read and agree to the service terms, and click **Create now**. For the Subscription payment mode, you must also confirm the order information and complete payment as prompted.

4. After creation is complete, return to the instance management page to view the created instance. When the instance **status** is **Running**, the instance has been successfully created.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac1b6df704bf4077be0f3fd6e86315df~tplv-goo7wpa0wc-image.image) </span>
