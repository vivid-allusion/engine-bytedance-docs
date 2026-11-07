---
title: "Create clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later"
---

Volcano Engine E\-MapReduce (EMR) is an enterprise\-grade big data analytics system for the open\-source Hadoop ecosystem. It is fully compatible with open\-source technologies and provides integration and management for ecosystem components such as Hadoop, Spark, Hive, Hudi, and Iceberg. For details, see [Guide to operating components](https://docs.byteplus.com/docs/E-MapReduce/Component_usage_guide). This document introduces the procedure and related configurations for creating a cluster in the EMR console.

<span id="34f8b4db"></span>
# **Prerequisites**


* After completing the relevant [Preparation](https://docs.byteplus.com/docs/E-MapReduce/118287)getting started steps, you must complete enterprise verification to create a cluster.


<span id="7b3a7437"></span>
# **Procedure**

<span id="b4e3539f"></span>
## Entry point for cluster creation


1. Log in to[E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). In the top menu bar, select the region and project space from the dropdown as appropriate:

   * Region: The created cluster and corresponding resources will be deployed in the selected region, and this cannot be changed after creation.

   * Project space: The system automatically creates a default project named **default**. From the upper right corner of the interface, go to **User \> Access Control \> Resource Project \>Project Management** to create or manage your project space. For details, see[Project configuration](https://docs.byteplus.com/docs/E-MapReduce/ecs-project_configuration).

2. On the Overview interface, click **Create resource \>on ECS cluster** to start creating a cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c28b8a625d40909aa428cd1eb086a4~tplv-goo7wpa0wc-image.image) </span>

   When creating a cluster for the first time, the system will prompt you to complete service authorization (ECS, VPC, EIP, and so on). After authorization, go to the upper right corner **User \> Access Control \> Role Management**, search for the keyword "EMR" in the search bar, and confirm that the "**ServiceRoleForEMR**" role exists, which indicates that EMR service authorization is complete.


<span id="41638f08"></span>
## Cluster configuration

After entering the cluster creation interface, complete the configuration steps for Software settings, Hardware settings, Other settings, Preview confirmation in sequence.

<span id="2147f1bc"></span>
### Software settings

<span id="07733acd"></span>
#### Region


|**Configuration item** |**Note** |
|---|---|
|Region |Region refers to different geographic regions where physical data centers are located, usually divided by the city where the physical data center is located. Private networks are completely isolated between different regions, ensuring maximum stability and fault tolerance between regions. Regions can communicate with each other via public IPs, or achieve private network connectivity through Cloud Enterprise Network and more. |


<span id="fdad33d8"></span>
#### Software configuration


|**Configuration item** |**Note** |
|---|---|
|Analytics scenarios |For data analytics scenarios, EMR already supports a variety of analytics scenarios such as **data lake** and **interactive analytics**. |
|Cluster type |For different analysis scenarios, EMR provides multiple cluster types. For more details, see [Cluster types](https://docs.byteplus.com/docs/E-MapReduce/Cluster_types).<br><br><br>* Data lake scenario:<br><br>   * Hadoop: A foundational framework for distributed big data, suitable for offline and real\-time analysis, as well as data lake architectures and various big data scenarios.<br><br>* Interactive analysis scenario:<br><br>   * Presto: An open\-source distributed query analysis engine based on MPP architecture, providing high\-performance data query services.<br><br>   * Trino: An open\-source distributed query analytics engine based on MPP architecture, supporting petabyte\-scale data query and analytics.<br><br>* Search scenarios:<br><br>   * OpenSearch: A distributed search and analytics engine that addresses users' needs for structured data exploration. |
|Product version |It is recommended to select the latest version of the EMR software stack. There are differences in the product versions supported by different cluster types. |
|Service High Availability |Select whether to enable high availability services for the cluster.<br><br>For example: When high availability is enabled, the Hadoop cluster will have three primary nodes to support high availability for ResourceManager and NameNode. High availability deployment is recommended for production environments.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, in real\-time computing scenarios, Kafka and Pulsar cluster types do not support enabling high availability mode for services.</div><br> |
|Required service |Default service components: The mandatory default services vary by cluster type. Later, you can start or stop services in the service list of the cluster . |
|Optional services |Select other component services based on actual needs. Selected components will automatically start the corresponding services. |
|Metadata selection |When the cluster includes components such as Hive, Ranger, and Airflow, metadata storage must be configured.<br><br><br>* External database: Only for use in test scenarios. The local MySQL database is deployed on a single node of the EMR cluster and cannot guarantee high availability, posing stability risks. For production scenarios, it is recommended to use an external database.<br><br>* External database: For clusters used in production environments, it is recommended to use a standalone RDS MySQL. You can choose the high availability version of RDS MySQL 5.7 from Volcano Engine, and select the external data source to connect to from the dropdown list. For detailed instructions, see [Metadata connections](https://docs.byteplus.com/docs/E-MapReduce/Metadata_connections).<br><br>* LAS: Use the AI Data Lake Service (LAS) to manage EMR metadata. Currently, only Hive metadata is supported. For detailed instructions, see Metadata Management. |
|Hive root path |If the Hadoop cluster type is selected, you must choose the Hive root path. Both local HDFS and object storage TOS are supported as storage path types.<br><br><br>* Enter the Hive root path information, which is the default Hive table location. This can be modified after the cluster is created. You can select either a local HDFS path or an object storage TOS path.<br><br>* If the TOS path type is selected, after clicking the button on the right, you can enter the TOS bucket name to search. If you have not created object storage, you can go to TOS Console to create it.<br><br>* You can also select TOS accelerator, which supports access to the TOS accelerator via the TOS single\-region access point.<br><br>   If you have already created an accelerator on TOS, you can also select the path of the corresponding TOS accelerator as the Hive root path to meet the requirements of low latency, fast response, and high throughput data transmission scenarios. For an introduction to the TOS accelerator, see: [TOS accelerator Overview](https://docs.byteplus.com/en/docs/tos/Overview11). |
|Cluster storage root path |Configure the default storage root path for the cluster, which is used to store job logs, temporary intermediate data, and other files generated within the cluster.<br><br>Supports local HDFS paths or TOS paths.<br><br>Limits: Only supported for Hadoop clusters and Custom clusters of EMR\-4.0.0 and above. |
|Spark Shuffle service |Specify the Shuffle service type used when executing Spark jobs. Different options correspond to different performance, stability, and operations and maintenance methods.<br><br>Click the options dropdown box. Available options:<br><br><br>* Spark External Shuffle。 This option is suitable for small and medium\-sized clusters and can be selected when the Shuffle volume is low.<br><br>* Celeborn service. This option is visible after enabling the Celeborn service in **Optional services**. Suitable for scenarios with large Shuffle volumes, high stability requirements, and the need for self\-managed Remote Shuffle Service.<br><br>* EMR Serverless RSS。<br><br>   * Integrates the EMR Serverless RSS service in the same region for EMR on ECS clusters. Suitable for scenarios with large Shuffle volumes, high stability requirements, and where operations and maintenance are not required and only Spark job development is the focus.<br><br>   * Limits: Only supported for Hadoop clusters and Custom clusters of EMR\-4.0.0 and above, and requires enabling **Spark 3.x** and disabling **kerberos authentication**. |


<span id="f8940625"></span>
#### Advanced settings


|**Configuration item** |**Note** |
|---|---|
|Custom configuration |Before creating the cluster, you can define the parameter configuration of cluster components using a JSON file and import the component configuration into the cluster.<br><br>The format for entering parameters is as follows: [{"serviceName": "xxx", "fileName": "xxx", "key": "xxx", "value": "xxx"}]<br><br><br>* serviceName: Service name, must be in all uppercase letters.<br><br>* fileName: File name. The actual file name for parameter passing, the suffix must be removed.<br><br>* key: Name of the configuration item.<br><br>* value: The specific value to set for this configuration item. |
|Kerberos authentication |After enabling, open\-source components in the cluster will start in Kerberos security mode. The Kerberos service can only be enabled when creating the cluster. It cannot be enabled or disabled after the cluster is created. For more information, refer to [Use Kerberos-authenticated clusters](https://docs.byteplus.com/docs/E-MapReduce/Use_a_Kerberos-authenticated_cluster). |
|Docker on YARN |After enabling, Docker can be used to run Spark and Flink tasks on the cluster. |
|External Ranger Audit Log |After this feature is enabled, audit logs such as Ranger authorization and other audit logs for the cluster will be stored in an external OpenSearch cluster or Volcano Engine Search Service, rather than the default EMR\-managed OpenSearch cluster. This is suitable for scenarios that require centralized log management, custom log retention policies, or integration with existing log platforms.<br><br><br>* OpenSearch source: Select the source type for the external OpenSearch cluster:<br><br>   * Self\-hosted OpenSearch cluster: An OpenSearch cluster deployed and maintained by the user.<br><br>   * Volcano Engine Search Service: A cloud search service managed by Volcano Engine.<br><br>* Cluster link: The access address for the external OpenSearch cluster, in the format `http(s)://<host>:<port>`, for example `https://opensearch.example.com:9200`. Ensure that the EMR cluster can communicate with this address over the network.<br><br>* Instance ID: The ID of the Volcano Engine\-managed cloud search service instance.<br><br>* User: The user for accessing the OpenSearch cluster or Volcano Engine Search Service.<br><br>* Password: The password for accessing the OpenSearch cluster or Volcano Engine Search Service.<br><br>* Index: The name of the index where Ranger audit logs are written in OpenSearch, that is, the logical namespace for storing log data. It is recommended to use a name that better identifies the service, such as emr\-ranger\-audit, to facilitate subsequent queries and management. |
|Release protection |After enabling release protection for the cluster, the release cluster operation cannot be performed, protecting your EMR cluster from accidental release.<br><br><br>* Limits: Only supported for Hadoop clusters and Custom clusters.<br><br>* To release a cluster, disable release protection on the **Cluster overview** page. |


After completing the software configuration, click **Next step** to set up cluster hardware.

<span id="060e89c5"></span>
### Hardware settings

<span id="7233cb73"></span>
#### Payment settings


|**Configuration item** |**Note** |
|---|---|
|Payment type |* Pay\-As\-You\-Go: A postpaid mode, where you pay after use. Nodes can be released at any time. Charges are based on the actual duration of activation, calculated in hours. Billing occurs once per hour. This mode is suitable for short\-term test tasks or flexible dynamic tasks.<br><br>* Subscription: Prepaid mode, pay for a specified duration. Upon expiration, you can choose to release or renew, or enable the **automatic renewal** feature to reduce manual renewal management costs and prevent EMR service interruption due to missed renewals.<br><br><br>For details, see [Billing overview](https://docs.byteplus.com/docs/undefined/6a18f83bc4cb0b050352f71e). |


<span id="632912e0"></span>
#### Availability zone


|**Configuration item** |**Note** |
|---|---|
|Availability zone |An availability zone is a physically isolated area within the same region, with independent power and network. Availability zones within the same region are interconnected via internal networks and have fault isolation capabilities. Supported availability zones vary by region. Refer to the console interface for specific information. |


<span id="10d98473"></span>
#### Network configuration


|**Configuration item** |**Note** |
|---|---|
|VPC |Select the private network for the region where the EMR cluster is located. It is recommended that EMR upstream and downstream systems be in the same private network.<br><br>If there is no available VPC, click [Create VPC](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc) to create a new one.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When selecting a specific project, ensure that the VPC is also under the corresponding resource project.</div><br> |
|Subnet |The subnet is used to assign a private IP address to the primary network interface of the instance. Network management can be performed via the network interface. Select the subnet of the corresponding availability zone under the VPC from the dropdown. If there is no available subnet, click [Create Subnet](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/subnet) to create one.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Subnets are distinguished by availability zones. Please select the subnet segment under the corresponding availability zone above.</div><br> |
|Security group |Select the security group rules to configure and control inbound and outbound traffic for cloud servers within the group. For details, see [Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).<br><br>You can select an existing security group from the dropdown. To create a new security group, click [Create Security Group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group) to go to the console to create one. |


<span id="82cd8148"></span>
#### Instance Settings


|**Configuration item** |**Note** |
|---|---|
|Custom deployment |After this feature is enabled, Hadoop high\-availability clusters and custom high\-availability clusters support modifying the number of Master nodes, within the range of 3 to 5. It also allows you to select which big data components to deploy on Master, Core, or Task nodes, enabling load isolation and reducing the load on certain nodes or node groups.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f282ff5671242fab449e3935887e710~tplv-goo7wpa0wc-image.image) </span> |
|Node |* The master instance is mainly responsible for deploying control processes such as ResourceManager and NameNode.<br><br>   * Number of master nodes: The default for a standard cluster is 1 node; Hadoop high\-availability clusters default to 3 nodes, and Presto and other high\-availability clusters default to 2 nodes.<br><br>   * You can select from four instance types: **Compute type,Local SSD type,General purpose,Memory type**. Choose the appropriate instance specifications as needed. For details on the differences between instance types, see [Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>   * System disk: Used to store the operating system running on the cloud server. Ultra\-fast SSD cloud disks are supported. The size can be adjusted as needed. Capacity range: 60–2048 GB.<br><br>   * Data disk: Used to store application data. Ultra\-fast SSD cloud disks are supported. The size can be adjusted as needed. Capacity range: 60–32768 GB.<br><br>      For details on cloud disk performance, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* Core instances: Primarily responsible for storing all data in the cluster. After the cluster is created, on\-demand scaling is also supported.<br><br>   * Number of Core instances: The default is 2, and can be adjusted as needed.<br><br>   * You can select from **Compute type,Local SSD type,General purpose,Memory type,Big data type,Enhanced networking, GPU instance type**—a total of seven instance types. Select the appropriate instance specification as needed. For details on the differences between instance types, see[Instance types and specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).<br><br>   * System disk: Used to store the operating system running on the cloud server. Ultra\-fast SSD cloud disks are supported. The size can be adjusted as needed. Capacity range: 60–2048 GB.<br><br>   * Data disk: Used to store application data. Ultra\-fast SSD cloud disks are supported. The size can be adjusted as needed. Capacity range: 60–32768 GB.<br><br>* Task instances: Do not store data and are mainly used to expand the cluster's computing capacity on demand. Not enabled by default. Add as needed, up to a maximum of 20 Task node groups.<br><br>* Public IP assignment: Supports enabling public IP assignment for Master, Core, and Task node groups. During cluster initialization, a public IP is automatically provisioned and assigned to the cluster node group. If public IP assignment is not enabled, the cluster cannot be accessed via public IP. |


After completing the hardware configuration, click **Next step** to configure other basic settings for the cluster.

<span id="2fd934f6"></span>
### Other settings

<span id="7ba525f8"></span>
#### basic information


|**Configuration item** |**Note** |
|---|---|
|Cluster name |Cluster name: Length must be between 1 and 64 characters. Only Chinese characters, letters, numbers, hyphens (\-), and underscores (_) are allowed. |
|Access credentials |This credential is used to remotely log in to the ECS machine of the cluster's Master node. You can choose to log in using a key pair or a password. |
|Key pair/Password |* Key pair: Select an existing key pair from the dropdown, or click [Create key pair](https://console.byteplus.com/ecs/region:ecs+ap-southeast-1/keyPair?projectName=default) to go to the console and create one. For details, see [Overview of key pair](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview).<br><br>* Password: Enter the login password for the cluster's Master node<br><br>   * The length must be between 8 and 30 characters.<br><br>   * The password can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must contain at least three of these types.<br><br>   * The following special characters are allowed: `~!@#$%^&\*()_\-+= \|<br><br>   * The password cannot start with “/” or “$6$”.<br><br>   * Do not set an overly simple password, or it may be vulnerable to malicious attacks by other users. It is recommended to use a key pair. |


<span id="eaf9d591"></span>
#### Advanced settings


|**Configuration item** |**Note** |
|---|---|
|Cluster script |To deploy and install third\-party components in an EMR cluster, you can run bootstrap operations before or after the deployment of EMR component services in the cluster to customize the cluster environment.<br><br>For details, see [Guided operations](https://docs.byteplus.com/docs/E-MapReduce/Guided_operations). |
|Cluster role |The IAM role provides resource permissions for ECS on the EMR cluster to call and access TOS. For details, see [Role authorization](https://docs.byteplus.com/docs/E-MapReduce/ecs_role_authorization). |
|Label |Tags consist of case\-sensitive key\-value pairs. The tags you set will be applied to all instances and cloud disks created in this session.<br><br>You can select existing tags, or directly enter and create new tags, then press Enter to confirm.<br><br>Tag management entry: [Tag management](https://console.byteplus.com/resourcemanager/tag/list). |
|Project of the cluster |To assign the newly created cluster to a new project, you can select from the dropdown menu, or go to [Create project](https://console.byteplus.com/iam/resourcemanage/project).<br><br>For details, see [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management). |


After completing other cluster settings, click **Next step** to preview and confirm the overall cluster configuration.

<span id="52a4a5a1"></span>
### Preview confirmation


|**Confirmation items** |**Description** |
|---|---|
|Cluster information |Provide and confirm the information for cluster creation settings, including **Cluster name,Metadata selection,Deployment region,Public IP** and more. |
|Payment type |Confirm the selected cluster payment type. |
|Software settings |Provide and confirm software information, including **Product version,Cluster type,Deployment options,**  required services, and optional services. |
|Network configuration |Confirm information including **Availability zone, VPC,Subnet** and **Security group**. |
|Instance configuration |Confirm the quantity, specifications, disk types, and number of Master, Core, and Task nodes. |
|Advanced settings |Confirm information for advanced cluster configurations, including \*\*Enable custom configuration,Guided operation,IAM user \*\* and more. |


After preview and confirmation, check the "[Special terms for Data Middle Platform products and services](https://docs.byteplus.com/docs/undefined/6a18f91f9a082404cc2e262c)" option in the lower right corner and click**Create now**. Complete the order payment step. Then go to**Resource Management \> on ECS** to view the created cluster. When the cluster status updates toRunning, it indicates successful creation.

<span id="278c1ac4"></span>
## Quick createCluster

Cluster creation also supports quick creation mode. In the cluster creation interface, select **Quick create** in the upper right corner:


1. Complete the configuration of relevant parameters such as **Software configuration,Payment settings,Availability Zone,Network configuration,Instance Settings,Basic information** and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18380a8c86084950b31665144a89a7c0~tplv-goo7wpa0wc-image.image) </span>

2. Check the service terms, click the **Create now** button to quickly create a cluster.


&nbsp;
