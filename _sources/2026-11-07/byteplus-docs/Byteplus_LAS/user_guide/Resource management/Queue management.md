---
title: "Queue management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/queue_manage"
---

When developing and scheduling data processing tasks on LAS, you rely on the computing resources provided by queues. You can run tasks on already created EMR Serverless queue resources (recommended), or, according to business needs, plan resource requirements and purchase and enable AI Data Lake queues as needed. This document provides details and instructions for using queue resources.

<span id="e75d2379"></span>
# Overview

LAS requires queue resources in the following typical scenarios:


* Data processing task scheduling: Supports computing engines such as Daft and Ray for multimodal data processing.

* Environment deployment: Used for development machines and online service deployment, enabling rapid setup of data processing environments and services.


Currently, LAS computing queues are divided into two types: "dedicated queues" and regular "computing queues". A comparison is provided below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">On January 8, 2026, AI Data Lake optimized the application strategy for queue resources, unifying queue resources as "compute queues" that can be flexibly applied to task scheduling and environment deployment scenarios. The distinction between "general queues" and "compute queues" is no longer made, and support is provided for using EMR Serverless queues as exclusive queues for LAS, for use with LAS development machines and tasks.</div>



|Comparison items |Exclusive queue (recommended) |Compute queue |
|---|---|---|
|Queue resource source |Essentially an EMR Serverless queue. |Compute queue provided by LAS. |
|Queue characteristics |* Unified as the `Min/Max` model.<br><br>   * `Min`: Reserved resources to ensure core computing power, billed annually or monthly.<br><br>   * `Max`: Elastic resource upper limit, billed by usage.<br><br>* GPU resources support configuration of machine types and number of GPU cards, and support scenarios with mixed GPU/CPU queues and combinations of multiple GPU models.<br><br>* You can allocate queue resources based on the resource requirements of different tasks, and create multiple compute groups with different resource quotas under a queue, making it easier for different tasks to select resources as needed. When executing LAS tasks, you can select the "general compute group." |* Scenarios that mix GPU queues with single\-model GPU combinations are not supported.<br><br>* The billing method is "annual/monthly subscription." |
|Availability zone |Supports creating and deploying resources across multiple availability zones, providing cross\-zone disaster recovery capabilities. |Typically, a single availability zone is bound during creation. |
|Monitoring and alerting |Fully aligned and integrated with the BytePlus **Cloud Monitoring** dashboard, offering a wide range of metrics covering queues, compute groups, and job dimensions, including GPU monitoring. |LAS has built\-in monitoring; some metrics require manual configuration. |
|Permissions/IAM |Unified use of the IAM+EMR Serverless **Developer / Admin** role system, supporting permission management for individual queues. |LAS uses an independent permission system and does not support queue\-level permission management. |
|Project/Tag billing |Leveraging the integration capabilities of EMR Serverless and BytePlus global Project/Tag, enabling out\-of\-the\-box billing and resource grouping. |LAS requires separate integration with Project/Tag. |
|Usage scenarios and recommendations |* Can be flexibly applied to task scheduling and environment deployment scenarios; exclusive queues (EMR Serverless queues) are recommended.<br><br>* LAS queues will not receive new feature updates in the future. It is recommended to release LAS queues and use exclusive queues, or purchase exclusive queues after the queue expires. ||


<span id="1cba1147"></span>
# Dedicated queue (EMR Serverless queue)

The dedicated queue is essentially an EMR Serverless queue:


* Queue creation and management: See .

* You can allocate queue resources based on the resource requirements of different tasks. Multiple computing groups with different resource quotas can be created under a queue, allowing flexible selection for different tasks. Currently, when executing LAS tasks, the "general computing group" can be selected. For details, see .

* Queue monitoring: See .


<span id="1af60964"></span>
# Computing queue (LAS queue)

<span id="843fe7cb"></span>
## Create a new queue

You can create a resource queue by following the steps below. For billing information, see [Billing instructions](https://docs.byteplus.com/docs/Byteplus_LAS/Billing_instructions).


1. Log in to \*\*LAS Console \> \*\*Resource management  **\>**  Queue management  **\>**  Compute queue \*\*\*\* page, click Create compute queue \*\*\*\* , and then configure queue resource parameters on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3124ce5046174ecfa907d60576e745b9~tplv-goo7wpa0wc-image.image) </span>

2. Configure Resource information.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Availability zone |Select which availability zone in the current region to enable queue resources. |
   |Network connection |Select whether to enable the network connection switch. After enabling, the Serverless queue can connect to the target VPC network. After enabling, you also need to configure:<br><br><br>* Select the VPC network, subnet, and security group to connect.<br><br>* Select whether to enable Global Cross\-VPC Routing. After enabling, all jobs will automatically bind to the queue's VPC network. |
   

3. Configure payment information.

   The current queue resources support the "annual/monthly subscription" billing method. For details, see [Billing instructions](https://docs.byteplus.com/docs/Byteplus_LAS/Billing_instructions).

4. Configure queue resource settings, select resource type and machine type.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Queue name |Custom queue name |
   |CPU model |* CPU types supported: standard (1:4), memory\-optimized (1:8), compute\-optimized (1:2) |
   |fixed & elasticity CU |Configure the fixed CU count and elastic CU count for the corresponding CPU resources as prompted on the interface. |
   

5. Other configurations.

   
   |Parameters |Configuration description |
   |---|---|
   |permission to use is granted by default |Choose whether to enable default authorization based on actual requirements. After enabling it, by default, all accounts can directly use the queue, including viewing queue information, monitoring, and submitting jobs to the queue. |
   |Label |Tags are composed of case\-sensitive key\-value pairs. The tags you set will be applied to the queue you are creating. |
   

6. After confirming the configuration, review and check the "I agree to the AI Data Lake Service LAS Service Terms" option in the lower right corner, click **Create**, complete the order payment step, and then go to Resource management  **\>**  Queue management  **\>**  Compute queue to view the created resources.


<span id="c42c4c86"></span>
## Queue scaling

When the compute queue specifications are insufficient or exceed application requirements, you can change the instance specifications, supporting both upgrades and downgrades.

<span id="64c843fa"></span>
### Limitations

Only changes to resource specifications are supported; changes to machine types are not supported, such as changing from a standard CPU type to a compute\-optimized type.

<span id="3ea406f5"></span>
### Operation steps


1. Log in to the **LAS Console**, and in the left navigation bar, click Resource Management to enter the Resource management page.

2. In the Resource management list, click the Configuration change of the target resource queue to open the configuration change dialog box, where you can adjust the size of the resource specifications or the number of GPU cards as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79617d3e926d4e33a6a520e80ad7736c~tplv-goo7wpa0wc-image.image) </span>

3. After clicking **Confirm**, the configuration change will begin.


<span id="32aece2c"></span>
## Queue monitoring

For compute queue and general queue instances that have been created, LAS AI provides monitoring functionality, allowing you to conveniently obtain queue usage information.

Specific monitoring information can be viewed via the following path: On the resource list page, click the target resource name to enter the details page, then access it through the Queue monitoring tab in the sidebar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9be533babae84664b8bbfc89a91975c6~tplv-goo7wpa0wc-image.image) </span>


* You can filter the monitoring time range in the monitoring interface.

* Currently, basic monitoring metrics for queue resource usage are provided. The tooltip buttons after each metric contain corresponding metric definitions.
