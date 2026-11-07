---
title: "Create a queue"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_a_queue"
---

Resource queues are logical units in EMR Serverless used to manage and isolate computing resources. They represent computing capacity and are also a billing concept. We allow users in Serverless to create public queues and dedicated hybrid heterogeneous queues. You can freely combine CPU and GPU resources to achieve seamless integration of data preprocessing (CPU\-intensive) and model inference (GPU\-intensive), significantly improving resource utilization. After queues are created, you can run various types of tasks such as Spark, Ray, and Presto. For queue billing information, please refer to [EMR Serverless billing overview](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To configure GPU resources, you can contact BytePlus technical support personnel by <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submitting a ticket</a>.</div>


<span id="e47f87b1"></span>
# prerequisites


* The EMR Serverless service has been enabled.

* 


<span id="5e9744e2"></span>
# Create a queue

<span id="bf2bdb11"></span>
## Create entry point


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario:

   1. Region: The created queue and corresponding resources will be deployed in the selected region and cannot be modified once created.

   2. Project: The default project is displayed.

3. Go to the create queue page.

   1. Method 1: In the overview interface, click Create resource \> Serverless queue.

   2. Method 2: In the left navigation bar, select Resources \> Serverless, and click the Create resource \> Serverless queue button in the upper left corner of the page.


<span id="ac838bcc"></span>
## Configure queue parameters

On the create queue page, complete the following configurations: Resource information, Payment information, resource queue configuration, metadata configuration, and other configurations.

<span id="e4e45a63"></span>
### Configure the queue type and payment information


|**Configuration items** |**Note** |
|---|---|
|Queue type |Select the queue type.<br><br><br>* public queue: After enabling EMR Serverless, the system will automatically assign you a 'public queue' resource. This resource is shared by all EMR Serverless users and is suitable for development and testing environments or small task clusters.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">public queueare system\-assigned public resources. Creating new public queues manually is not supported. After assignment, billing is based on actual usage; no charges are incurred if not used, and manual release is not required.   </div><br>   <br><br>* exclusive queue\-Subscription: You can choose to create a subscription\-based exclusive queue. This is your dedicated queue resource, ensuring isolation and security for critical tasks, and is suitable for production environments and critical tasks.<br><br>* exclusive queue\-Time\-based billing: EMR Serverless also supports dedicated queue resource types billed by time.<br><br>   * Exclusive queue – Pay\-as\-you\-go queue resources are billed hourly immediately after successful creation. Charges are incurred regardless of whether the queue resources are actually used during this period. Suitable for scenarios that require stable job execution for a short period. |
|Billing duration &Auto\-renewal<br><br>(Subscription exclusive queues require configuration) |* Billing duration: Select the purchase duration for the Subscription queue resources. Default value: 1 month.<br><br>* Auto\-renewal: Set whether to enable automatic renewal after the current Subscription queue resources expire. It is recommended to enable this option to avoid business impact due to resource expiration. After enabling:<br><br>   * The system will automatically deduct the fee from the account balance monthly before the resources expire, so manual payment is not required.<br><br>   * The automatic renewal period is fixed as "monthly"; that is, regardless of the Billing durationconfiguration duration of the queue resources, each subsequent automatic renewal will extend the duration by one month. |


<span id="c07f83fe"></span>
### Configure resource information


|**Configuration items** |**Note** |**Example** |
|---|---|---|
|Region |Select the geographic region where the resource is located. Resources in different regions cannot communicate with each other over the internal network. |North China 2 (Beijing) |
|Availability zone |Select the availability zone where the resource is located. You can select a single or multiple availability zones. Additional zones can be added during configuration, but removal is not allowed. Selecting multiple availability zones means you accept cross\-zone deployment, and underlying node resources may not be evenly distributed across each zone. When resources in a single availability zone are insufficient or a failure occurs, failover and disaster recovery can be achieved, but access response latency for the service may increase. We recommend using a multi\-availability zone solution for queues exceeding 3000 CU to ensure better resource supply. |Availability zone A |
|Internet connection |After enabling, Serverless Spark can connect to the target VPC network.<br><br>Enabling network connectivity requires additional configuration of the following parameters:<br><br><br>* VPC: Select the VPC under the current project.<br><br>* Security group: Select the security group under the VPC.<br><br>* Global cross\-VPC routing:<br><br>   * After enabling, all jobs will automatically bind to the queue VPC network (via auxiliary NIC). All jobs will consume subnet IPs, and during peak periods, jobs may fail due to insufficient subnet IPs.<br><br>   * If disabled, you can add the parameter `serverless.cross.vpc.access.enabled=true` at the job level to enable cross\-VPC access as needed.<br><br>   * For compute groups using external HMS as metadata, the queue VPC network will be bound by default (via auxiliary NIC), and this is not controlled by configuration. |Enable |


<span id="04bc478d"></span>
### Resource queue configuration


|**Configuration items** ||**Note** |**Example** |
|---|---|---|---|
|Queue name ||Name of the custom queue. May include letters, numbers, and underscores, with a maximum length of 99 characters. |emr_queue |
|CPU resource allocation |Instance type |Select the queue instance type specification.<br><br>CPU supports the following instance types:<br><br>Standard (1:4): 1 vCPU with 4 GiB memory.<br><br>Memory\-optimized (1:8): 1 vCPU with 8 GiB memory.<br><br>Compute\-optimized (1:2): 1 vCPU with 2 GiB memory. |Standard (1:4) |
||Pin |Set the fixed resource size for the queue. Unit: CU (Compute Unit). This portion of resources will be billed on an annual/monthly subscription basis.<br><br>Note: For requirements exceeding 50,048 CU, please apply via submit a ticket. |32 |
||Elastic |Set the upper limit of elastic resources that the queue can dynamically scale. Unit: CU. Elastic capacity is billed based on usage. The elastic portion of the queue must be less than or equal to 256 CU or the maximum limit (fixed CU count), and the input value must be a multiple of 32 CU.<br><br>Note: If elastic resources are not required, set to 0 CU. Currently, 1 CU is equivalent to 1 vCPU and 4 GiB memory. |0 |
|GPU resource allocation |Specification |Select GPU resource specifications. You can select one or more resource specifications from the list. Each instance specification corresponds to a certain amount of CPU, memory, and GPU. For example, emr.ini2.7xlarge includes 1 GPU\-NVIDIA A30, 28 vCPU, and 234 GiB memory.<br><br>Important: After the queue is created, adding or removing specifications is currently not supported. |emr.ini2.7xlarge |
||Quantity |Configure the number of instances for each specification. For example, configuring 2 emr.ini2.7xlarge instances includes 2 NVIDIA A30 GPUs, 56 vCPU, and 468 GiB memory. |2 |
||mGPU |The mGPU solution uses kernel virtualization technology to enable sharing of a single GPU card, flexibly allocating compute cores and GPU memory resources with strict isolation. After enabling mGPU, jobs in the queue can directly specify the use of certain cores and GPU memory capacity of a single GPU. In small model scenarios, this can significantly reduce usage costs and improve resource utilization. |Enable |
|EngineRuntime ||When selecting the Spark compute engine environment, you can choose the Spark version and the corresponding Java Runtime or Bolt Runtime.<br><br><br>* Java Runtime: Standard Java runtime.<br><br>* Bolt Runtime: BytePlusSelf\-developed native kernel acceleration engine that can improve the execution speed of Spark, Presto, and other jobs. For more details, see .<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This option only applies to Spark jobs in the default compute group within the queue. When creating other compute groups, you can still make your own selection.</div><br> |Spark 3.5 (Java Runtime) |


<span id="dd04a45c"></span>
### Metadata configuration


|**Configuration items** |**Note** |**Example** |
|---|---|---|
|LAS |When enabling an EMR Serverless queue, LAS must also be enabled as the metadata management service. |Enable |


<span id="828f3b48"></span>
### Other configurations


|**Configuration items** |**Note** |**Example** |
|---|---|---|
|Grant default permisison |Configure the default access permissions for the queue. After enabling, all accounts can use this queue by default, including viewing queue information, monitoring, and Submit Job to the queue. |Disable |
|Independent Shuffle Service |After enabling Independent Shuffle Service, you can select an existing Serverless RSS service to achieve better shuffle performance and workload isolation.<br><br>Independent Shuffle ServiceSupports RSS **Enable dual replicas** (enabled by default), which reduces shuffle retries through redundant storage and improves job stability.<br><br><br>* After it is enabled, capacity consumption and [fees](https://docs.volcengine.com/docs/6491/2486396?lang=zh) will increase accordingly.<br><br>* Public RSS enables dual replicas by default and users cannot disable it.<br><br>* For queues without dual replicas enabled, the job\-level parameter `spark.celeborn.client.push.replicate.enabled` remains effective. | |
|Extra cloud drive |When Extra cloud drive is disabled, each CPU node is equipped by default with one general purpose computing 512 GiB cloud disk.<br><br>Currently, Extra cloud drive is an allowlist feature. To use this feature, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to request activation.<br><br>To provide more local storage space for your jobs, you can enable Extra cloud drive to expand disk capacity, supporting larger intermediate data caches and more complex data processing tasks.<br><br><br>* Cloud disk type: The storage type of the cloud disk.<br><br>* Single disk capacity: The capacity of a single cloud disk per node after expansion. The value range is 513 GiB to 65,536 GiB. After the queue is created, the single disk capacity can only be increased, not decreased. Please choose carefully.<br><br>* Quantity: The number of cloud disks per CPU node. After the queue is created, the number of cloud disks per node cannot be changed. Please choose carefully.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Total cloud disk capacity per node = Number of cloud disks per node × Capacity per disk.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">general purpose computing Cloud disk billing starts from 513 GiB. If you select Elastic extreme speed typecloud disk, the free quota is 256 GiB, and billing starts from 257 GiB. For more information about billing and cloud disk types, see <a href="https://docs.byteplus.com/docs/undefined/6a1432d44246c9054ec5ab8f">Storage resources: Cloud disk pricing details</a>.</div><br> | |
|Tags |Add tags to resources for easier classification and management. You can select existing tags or create new tags. Note: Up to 20 tags can be added. | |


<span id="8fb68b8b"></span>
## View queue creation result


1. After filling in the configuration parameters, click Create now to complete the queue creation.

2. Go to Console \> Resources \> Serverless to view the created queue. When the queue status updates to Running, it means the creation was successful.


<span id="5226d615"></span>
# what's next


* After completing the creation of the EMR Serverless queue, you can start creating and running related jobs. For details, see [Create and submit jobs](https://docs.byteplus.com/docs/E-MapReduce/118293).

* After creating a dedicated queue, you can create compute groups within the queue to accelerate processing and isolate loads. See [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups) for details.
