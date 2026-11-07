---
title: "Create an instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance"
---

This topic describes the preparations and procedure for creating a Milvus for VectorDB instance.

## Prerequisites

* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* Access to other Volcengine services used by Milvus for VectorDB has been authorized. For details on cross\-service access authorization, see [Cross-service access authorization](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Cross-service_access_authorization).

* You understand the resources and specifications required for the instance to be created. For detailed information about resource estimation, see [Estimate resources](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Resource_estimation).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region where you want to create an instance.

3. On the **Instances** page, choose the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, then click **Create instance**.

   > **tip**

   * > A Dedicated instance uses dedicated computing resources and suits scenarios requiring high stability, large data volumes, or high request rates.

   * > A Serverless instance uses shared computing resources and fits scenarios like AI Agent, unstable traffic, low maintenance, or cost sensitivity. The first Serverless instance created within the same subnet will set up network resources such as NIC and DNS. Subsequent instances reuse the existing resources, enabling creation within 1 second.

   * > On\-Demand edition instances allocate computing resources as needed, suitable for scenarios with large traffic fluctuations, unstable loads, and flexible cost control requirements. Compared with Dedicated and Serverless editions, On\-Demand edition offers more flexible choices between resource usage and cost, suitable for scenarios with dynamic demands for resource specifications and usage costs.

4. On the **Create Dedicated instances**, **Create Serverless instance**, or **Create On\-Demand edition instance** page, complete the configurations below, then click **Confirm order**.

   **Create Dedicated instance**

|**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Billing type |Select the instance billing type. Currently supported types are **pay\-as\-you\-go** and **subscription.** <br><br>> **tip**<br><br><br>> Subscription is a prepaid billing method, offering better discounts than pay\-as\-you\-go. We recommend that you use this billing method for long\-term users. For more information on billing types, see [Billing types](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Billing_methods).<br> |
   |Instance name |Set the instance name.<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Can only contain Chinese characters, letters, digits, hyphens (\-), and underscores (_).<br><br>* Length must be between 1 and 128 characters. |
   |Deployment mode |Select the instance deployment mode. Valid values are as follows:<br><br><br>* Single\-AZ deployment: reduces network latency and improves access speed.<br><br>* Two availability zones deployed: cross\-AZ deployment improves availability, with possible network latency of 2–3 ms.<br><br>* Three availability zones deployed: deployment across three availability zones further improves availability, with possible network latency of 2–3 ms. |
   |Availability zone |Select the availability zone based on your business requirements. The number of selected availability zones must match the deployment mode.<br><br>> **warning**<br><br><br>> After enabling multi\-AZ deployment in regions that support TOS multi\-AZ redundancy, the instance's TOS will automatically enable multi\-AZ redundant storage, which will increase storage costs accordingly. For more information, see [Multi\-AZ redundancy](https://docs.byteplus.com/en/docs/tos/Multi-az-redundancy).<br><br><br>For more information, see [Regions and availability zones](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Regions_and_availability_zones). |
   |Engine version |Select the engine version based on your business requirements.<br><br>> **tip**<br><br><br>> Milvus 3.0 version instances currently require whitelist access. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000255) for approval.</a\><br> |
   |**Specification configuration** ||
   |Service nodes<br><br> |Select the specifications and quantities for each service node.<br><br><br>* You can select different specifications for different nodes. For more information, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).<br><br>* The nodes included differ slightly between engine versions.<br><br>   * : Configure 1 to 3 Mix Coordinator nodes; configure 1 to 20 Proxy and Data Nodes. In Multi\-AZ deployment mode, the number must be a multiple of the availability zones.<br><br>   * Version 2.6 and 3.0: Configure 1 to 3 Mix Coordinator nodes; configure 1 to 50 Proxy and Streaming Nodes. In Multi\-AZ deployment mode, the number must be a multiple of the availability zones. |
   |Index/Compute node |* Select the node resource model.<br><br>   * CPU: both data nodes and compute nodes use CPU. Node resources have fine granularity, offering the lowest cost and best value in small to medium scenarios. Suitable for various general daily scenarios.<br><br>   * GPU: both Data Nodes and Compute nodes use GPUs. The highest full\-link performance in building and querying, its parallel computing architecture effectively accelerates building and reduces processing latency per query. Suitable for scenarios with large\-scale batch queries requiring high throughput, high concurrency, and low latency.<br><br>   * Blend mode: Data nodes use GPU, and compute nodes use CPU. Fast building speed with lower query costs, balancing performance and cost efficiency. Suitable for scenarios with large\-scale data building or low update frequency, large query scale, and cost sensitivity.<br><br>   > **warning**<br>   <br><br>   > Resource mode cannot be changed after instance creation. Handle with care.<br>   <br><br>* Select CU type for index and compute nodes. The CU type supports **Capacity** and **Performance**.<br><br>   > **tip**<br>   <br><br>   > CU type setting is supported only when **Resource mode** is set to **CPU**.<br>   <br><br>* Configure pooling, specification, and quantity for index nodes.<br><br>   > **tip**<br>   <br><br>   * > For pooling function details, see [Index node pooling function introduction](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Introduction_to_index_node_pooling).<br>   <br><br>   * > For detailed information about available specifications for index nodes, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).<br>   <br><br>   * > The number of index nodes supported for configuration varies depending on the selected **deployment mode**. The number of nodes must be a multiple of the number of availability zones. You can configure up to 20 index nodes and 200 compute nodes.<br>   <br><br>   * > Pooling is supported only when **Resource model** is set to **CPU**.<br>   <br><br>* Configure specification and quantity for compute nodes.<br><br>   > **tip**<br>   <br><br>   * > For more information about available specifications for compute nodes, see [Product specifications](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_specifications).<br>   <br><br>   * > The number of Compute nodes supported depends on the chosen **Deployment mode**. The number of nodes must be an integer multiple of the availability zone count. You can configure up to 20 index nodes and 200 compute nodes.<br>    |
   |Storage space |The Milvus for VectorDB version automatically creates a bucket in Volcengine Object Storage (TOS) to store data for the instance. Billing is hourly based on actual storage usage. |
   |**Network information** ||
   |Access method |Select the VPC and subnet used to access the instance.<br><br><br>* Currently, only access from sales regions is allowed.<br><br>* After an instance is created, the VPC cannot be changed.<br><br>* You can only select VPC resources from the project chosen before entering the instance creation page.<br><br>* To ensure smooth access to a Milvus instance, we recommend that you select a VPC from a region where existing cloud services reside.<br><br>* Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br>* The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Transport protocol |Select the transport protocol applicable to the instance. Valid values: **HTTP** and **HTTPS**.<br><br>> **warning**<br><br><br>> It is not recommended to modify the transport protocol after the instance is created.<br> |
   |**Administrator configuration** ||
   |User name |Set the account for logging on to the instance and visualization tool. The default value is root and cannot be changed. |
   |Password |Set the password for the root account. The password rules are as follows:<br><br><br>* Contain only uppercase letters, lowercase letters, digits, and the following special characters `_#!@$%^&*()+=-`.<br><br>* Must include at least three types from uppercase letters, lowercase letters, digits, and special characters.<br><br>* Length must be between 8 and 32 characters.<br><br>* Weak passwords are not allowed. |
   |Confirm password |Re\-enter the password to confirm.<br><br>> **warning**<br><br><br>> Remember this password. It is the only credential to access the instance.<br> |
   |**Advanced configurations** ||
   |Affiliated project |Select the project to which the Milvus instance belongs. You cannot switch the project when creating an instance. To switch, close the dialog and modify it in the top navigation bar.<br><br>> **tip**<br><br><br><br>* > A project is a resource management method provided by Volcengine that helps maintain resource isolation and data security. You can view resource usage bills by project for easier cost calculation of cloud resources.<br><br><br>* > If you select **All resources** as the project in the top navigation bar before entering the instance creation page, you can change the project of the instance on the instance creation page. If you select another project in the top navigation bar before entering the instance creation page, you cannot change the project of the instance on the instance creation page.<br> |
   |Tag (optional) |Adding tags to a Milvus instance helps with easier identification and management. You can click **Add a row** multiple times to add several tags. |
   |Delete protection |Configure delete protection for the instance. The delete protection feature prevents instances from being accidentally deleted. When this feature is enabled, instances cannot be deleted. This feature is disabled by default. |
   |**Billing information** ||
   |Purchase duration |Set the purchase duration of the subscription instance. Enjoy a 50% discount when the purchase duration is one year or longer. |
   |Automatic renewal |Set whether to enable automatic renewal on due; disabled by default. After you enable this feature, the platform automatically renews the instance monthly before it is due. You can also modify the renewal configuration. For details, refer to [Renewal management](https://console.byteplus.com/finance/renew/). |

   **Create Serverless instance**

|**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Billing type |Select the billing type for the instance; currently, Serverless instances only support **pay\-as\-you\-go billing**. |
   |Instance name |Set the instance name.<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Can only contain Chinese characters, letters, digits, hyphens (\-), and underscores (_).<br><br>* Length must be between 1 and 128 characters. |
   |Engine version |Select the engine version based on your business requirements. |
   |**Network information** ||
   |Access method |Select the VPC and subnet used to access the instance.<br><br><br>* Currently, only access from sales regions is allowed.<br><br>* After an instance is created, the VPC cannot be changed.<br><br>* You can only select VPC resources from the project chosen before entering the instance creation page.<br><br>* To ensure smooth access to a Milvus instance, we recommend that you select a VPC from a region where existing cloud services reside.<br><br>* Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br>* The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Transport protocol |Select the transport protocol applicable to the instance. Valid values: **HTTP** and **HTTPS**.<br><br>> **warning**<br><br><br>> It is not recommended to modify the transport protocol after the instance is created.<br> |
   |**Password configuration** ||
   |User name |Automatically generated after instance creation. Viewable on the details page. For detailed instructions, see [View instance information](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_information). |
   |Password |Set the password for the username. The password rules are as follows:<br><br><br>* Contain only uppercase letters, lowercase letters, digits, and the following special characters `_#!@$%^&*()+=-`.<br><br>* Must include at least three types from uppercase letters, lowercase letters, digits, and special characters.<br><br>* Length must be between 8 and 32 characters.<br><br>* Weak passwords are not allowed. |
   |Confirm password |Re\-enter the password to confirm.<br><br>> **warning**<br><br><br>> Remember this password. It is the only credential to access the instance.<br> |
   |**Advanced configurations** ||
   |Affiliated project |Select the project to which the Milvus instance belongs. You cannot change the project when creating a data source. To switch projects, close this dialog and modify it from the top navigation bar.<br><br>> **tip**<br><br><br><br>* > A project is a resource management method provided by Volcengine that helps maintain resource isolation and data security. You can view resource usage bills by project for easier cost calculation of cloud resources.<br><br><br>* > If you select **All resources** as the project in the top navigation bar before entering the instance creation page, you can change the project of the instance on the instance creation page. If you select another project in the top navigation bar before entering the instance creation page, you cannot change the project of the instance on the instance creation page.<br> |
   |Tag (optional) |Adding tags to a Milvus instance helps with easier identification and management. You can click **Add a row** multiple times to add several tags. |
   |Delete protection |Configure delete protection for the instance. The delete protection feature prevents instances from being accidentally deleted. When this feature is enabled, instances cannot be deleted. This feature is disabled by default. |

   **Create On-Demand instance**

|**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Instance name |Set the instance name.<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Can only contain Chinese characters, letters, digits, hyphens (\-), and underscores (_).<br><br>* Length must be between 1 and 128 characters. |
   |**Network information** ||
   |Access method |Select the VPC and subnet used to access the instance.<br><br><br>* Currently, only access from sales regions is allowed.<br><br>* After an instance is created, the VPC cannot be changed.<br><br>* You can only select VPC resources from the project chosen before entering the instance creation page.<br><br>* To ensure smooth access to a Milvus instance, we recommend that you select a VPC from a region where existing cloud services reside.<br><br>* Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br>* The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |**Password configuration** ||
   |User name |Automatically generated after instance creation. Viewable on the details page. |
   |Password |Set the password for the account. The password rules are as follows:<br><br><br>* Contain only uppercase letters, lowercase letters, digits, and the following special characters `_#!@$%^&*()+=-`.<br><br>* Must include at least three types from uppercase letters, lowercase letters, digits, and special characters.<br><br>* Length must be between 8 and 32 characters.<br><br>* Weak passwords are not allowed. |
   |Confirm password |Re\-enter the password to confirm.<br><br>> **warning**<br><br><br>> Remember this password. It is the only credential to access the instance.<br> |
   |**Advanced configurations** ||
   |Affiliated project |Select the project to which the Milvus instance belongs. You cannot switch the project when creating an instance. To switch, close the dialog and modify it in the top navigation bar.<br><br>> **tip**<br><br><br><br>* > A project is a resource management method provided by Volcengine that helps maintain resource isolation and data security. You can view resource usage bills by project for easier cost calculation of cloud resources.<br><br><br>* > If you select **All resources** as the project in the top navigation bar before entering the instance creation page, you can change the project of the instance on the instance creation page. If you select another project in the top navigation bar before entering the instance creation page, you cannot change the project of the instance on the instance creation page.<br> |
   |Tag (optional) |Adding tags to a Milvus instance helps with easier identification and management. You can click **Add a row** multiple times to add several tags. |
   |Delete protection |Configure delete protection for the instance. The delete protection feature prevents instances from being accidentally deleted. When this feature is enabled, instances cannot be deleted. This feature is disabled by default. |

5. On the **Confirm order** page, review the instance details, read and check the **Service\-Specific Terms for BytePlus Database Products and Services**, then click **Buy now** to complete the instance creation.

## What's next

[Connect to the instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Connect_to_the_instance)
