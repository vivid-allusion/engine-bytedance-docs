---
title: "View and manage queues"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_and_manage_queues"
---

You can view the status of queues on the queue list page. For queues that have already been created, permission control, configuration modification, and other operations are currently supported. This document describes the different statuses of queues and the management operations supported.

# View queue status

The following section explains the main meanings of queue statuses and the management operations supported in each status.

|Queue status |Status note |Management operation: Subscription dedicated queue |Management operation: Public queue |
|---|---|---|---|
|Creating |The queue is being created. The next status will be running. The queue cannot provide services at this time. |No operation involved |No operation involved |
|Running |This status indicates that the queue has been created and is not expired, and is in a normal, available phase. |Change configuration<br><br>Authorize<br><br>Renew<br><br>Unsubscribe |Authorize<br><br>Unsubscribe |
|Stop serving due/Suspension of arrears |* Service suspension upon expiration: This status indicates that if the queue is not renewed within 2 hours after expiration, it cannot provide services. If the user does not renew the queue within 15 days, the queue will be released and resources will be reclaimed.<br><br>* Service suspension due to overdue payment: If payment is overdue (account balance is negative) for 2 hours and the debt is not paid, the public queue will be shown as suspended due to overdue payment. |Renew |No operation involved |
|Maturity release/Arrears release |* Release upon expiration: This status indicates that if the queue is not renewed within 15 days after expiration, its resources have been released and the queue must be reopened or created to be used again.<br><br>* Release due to overdue payment: If all debts are not paid within 7 \* 24 hours after overdue payment, resources will enter the reclamation state, releasing the EMR Serverless public queue, and the service will be unavailable. Released resources cannot be restored. To resume normal usage, settle outstanding payments and re\-enable the creation of public queues. |Delete |No operation involved |
|Pending payment |The EMR console will retain queues that have been configured but not paid for, marking them as pending payment. You can complete the payment during the order retention period. |Proceed to payment |No such status |
|Failed to create |If queue creation fails due to insufficient resources or other system issues, the queue will still be displayed and its status set to creation failed. |Delete |No such status |
|Changing |This status appears during the process of changing queue\-related configurations. |No operation involved |No such status |

# Queue management operations

## Modify queue

For running queues, on the queue details page, click Change Configuration in each section.

> **说明**

> Public queues do not support configuration modification.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08d8ca426e3a4e1f8a259654da7653a7~tplv-goo7wpa0wc-image.image)

### Basic information

|**Configuration item** |**Note** |
|---|---|
|Tag |Add tags to resources for easier classification and management. You can select existing tags or create new tags. Note: Up to 20 tags can be added. |

### Payment information

|**Configuration item** |**Note** |
|---|---|
|Auto\-renewal |You can change the queue's auto\-renewal attribute. It is recommended to enable this feature to avoid business disruption due to resource expiration. Once enabled, the system will automatically deduct the monthly fee from the account balance before the resource expires, eliminating the need for manual payment.<br><br>Note: The auto\-renewal feature uses a fixed monthly cycle, which is not affected by the initial purchase duration and is a globally unified rule. |

### Resource configuration

Three methods are supported: modifying existing specifications, adding new specifications, and removing specifications.

* Modify existing specifications: Change the quantity of existing specifications in the queue, including the number of CUs and the number of GPUs of different specifications.

* Add new specifications: Add CPU or GPU specifications within the original queue order period (existing specifications cannot be modified). The cost of new specifications will be charged according to the remaining period of the order.

* Remove specifications: Cancel a specific resource specification from the queue.

### Availability zone and network connection

|**Configuration item** |**Note** |
|---|---|
|Availability zone |You can add availability zone configurations to this queue, but removing availability zones is not allowed.<br><br>If availability zones are added to the queue with network connectivity enabled, you must also provide subnet information for the added availability zones. We recommend that after completing the queue's availability zone and network configuration, you also update compute groups that have separate network settings. |
|Internet connection |The network connection switch can be modified. Once enabled, a network connection from Serverless Spark to the target VPC can be established.<br><br>To enable network connectivity, additional parameters must be configured:<br><br><br>* Private network: Select the private network under the current project.<br><br>* Security group: Select the security group under the private network.<br><br>* Global cross\-VPC routing: After enabling, all jobs will automatically bind to the queue VPC network (via auxiliary NIC), and all jobs will consume subnet IPs. During peak job periods, insufficient subnet IPs may cause job failures. If disabled, you can add the parameter `serverless.cross.vpc.access.enabled=true` at the job level to enable cross\-VPC access as needed. For compute groups using external HMS as metadata, the queue VPC network (via auxiliary NIC) will be bound by default and is not controlled by configuration. |

### Other configurations

|**Configuration item** |**Note** |
|---|---|
|Independent Shuffle Service |After enabling Independent Shuffle Service, you can select an existing Serverless RSS service to achieve better shuffle performance and workload isolation.<br><br>Independent Shuffle ServiceSupports RSS **enabling dual replicas** (enabled by default), which reduces shuffle retries through redundant storage and improves job stability.<br><br><br>* When enabled, capacity consumption and [costs](https://docs.volcengine.com/docs/6491/2486396?lang=zh) increase accordingly.<br><br>* For public RSS, dual replicas are enabled by default and cannot be disabled by users.<br><br>* For queues without dual replicas enabled, the job\-level parameter `spark.celeborn.client.push.replicate.enabled` remains effective. |
|Extra cloud drive |When Extra cloud drive is disabled, each CPU node is equipped with one general purpose computing 512 GiB cloud disk by default.<br><br>Currently, Extra cloud drive is an allowlist feature. To use this feature, you can [submit a ticket ](https://console.volcengine.com/workorder/create/)to request access.<br><br>To provide more local storage space for your jobs, enable Extra cloud drive to expand disk capacity, which supports larger intermediate data caching and more complex data processing tasks.<br><br><br>* Cloud disk type: The storage type of the cloud disk.<br><br>* Single disk capacity: The capacity of a single cloud disk per node after expansion. The value range is 513 GiB to 65,536 GiB. Single disk capacity can only be increased, not decreased. Please choose carefully.<br><br>* Quantity: The number of cloud disks per node. If Extra cloud drive is not enabled when creating the queue, each CPU node is assigned one cloud disk by default, and the number cannot be increased. If the quantity is specified when creating the queue, it cannot be changed later.<br><br><br>> **说明**<br><br><br><br>* > Total cloud disk capacity per node = number of cloud disks per node × single disk capacity<br><br><br>* > general purpose computing Cloud disk billing starts from 513 GiB. If you select Elastic extreme speed type cloud disk, the free quota is 256 GiB, and billing starts from 257 GiB. For details on billing and cloud disk types, see [Storage resources: Cloud disk pricing details](https://docs.byteplus.com/docs/undefined/6a1432d44246c9054ec5ab8f).<br> |
|job priority&Allow job preemption |You can enable or disable the job priorityswitch as needed. After enabling, you can set the priority for jobs within the general compute group. The value ranges from 0 to 10, with higher values indicating higher priority. When the queue is fully loaded, high\-priority jobs will run earlier than low\-priority jobs.<br><br><br>* After enabling, you can set the priority for jobs within the general compute group. The value ranges from 0 to 10 (default: 0), with higher values indicating higher priority. When the queue is fully loaded, high\-priority jobs will run earlier than low\-priority jobs.<br><br>* After enabling, you can also configure whether to enable the Allow job preemptionswitch, that is, whether to allow low\-priority (0–2) jobs in the general compute group to be preempted by higher\-priority (3–10) jobs for compute resources when the queue is fully loaded. By default, tasks with priority \>= 3 will preempt tasks with priority <= 2.<br><br>* Job priority values and preemption settings:<br><br>   ```SQL```<br>```   -- Set the job priority value```<br>```   set emr.job.priority = [0~10]```<br>```   ```<br>```   -- Set whether this job can be preempted by other jobs```<br>```   set job.preemption.enable = [true/false]```<br>```   ```<br>    |

### Kerberos authentication configuration

|**Configuration item** |**Note** |
|---|---|
|krb5.conf |You can configure the contents of the krb5.conf file in the queue details to access a Hive Metastore with Kerberos authentication enabled. Currently, this configuration is effective only for general computing groups (including the Default computing group). To change Kerberos authentication settings, refer to and . |

### GPU resource defragmentation

When GPU workloads are distributed across different nodes, resource fragmentation may occur, resulting in reduced overall GPU utilization. For example, even if the queue has enough available GPUs in total, jobs that require multiple GPUs on the same node may not be scheduled because the available GPUs are scattered too widely.

The GPU resource defragmentation feature stops and resubmits jobs that meet the defragmentation criteria to optimize the placement of GPU workloads, thereby reducing resource fragmentation, releasing contiguous available GPU resources, and improving resource utilization.

#### Notes

* **Defragmentation may interrupt, retry, or fail related jobs.**  Before you perform this operation, make sure your business can tolerate these impacts and check the automatic retry configuration of the jobs.

* Defragmentation is supported only for compute groups that are in the **Running** state and use GPU resources. Both full GPU card and GPU partition (mGPU) workloads are supported.

* The system does not migrate workloads that are already optimally placed. The defragmentation process does not change the configured node pool constraints and does not migrate jobs to mismatched node pools.

* Jobs that meet the defragmentation criteria are considered candidates only. If the system determines that a migration will not provide optimization benefits, or that the target node has insufficient capacity, the migration is not performed. Therefore, the system does not guarantee that all candidate jobs will be defragmented, or that the specified amount of contiguous GPU resources will be released after defragmentation.

#### Prerequisites

* **Target queue**: The target queue must use GPU resources.

* **User permissions**: Administrator permissions are required.

#### Procedure

1. Log in to the EMR console and navigate to the details page of the target GPU queue.

2. In the upper right corner of the page, click **GPU resource defragmentation**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7117e98228a84e2bae81a231fa483f40~tplv-goo7wpa0wc-image.image)

3. In the **GPU resource defragmentation** dialog box, select the defragmentation scope:

   * **All compute groups**: Defragment all compute groups in the queue.

   * **Manual selection**: Select one or more compute groups to defragment.

4. Optional: Set filter criteria in **Defragmentable Jobs.**  If no filter criteria are set, the system defragments all jobs that meet the criteria by default.

   |**Parameters** |**Note** |
   |---|---|
   |Automatic retry enabled |When selected, only jobs with automatic retry enabled are included in the defragmentation scope. |
   |Priority less than or equal to N |Set the priority threshold. Valid values range from 0 to 10. Only jobs with a priority no higher than this threshold are included in the defragmentation scope. Jobs without a configured priority are not matched. |
   |Or / And |Used to combine the two conditions. When **Or** is selected, a job needs to meet only one of the conditions. When **And** is selected, a job must meet both conditions. |

5. After you confirm the scope and conditions, click **Defragment Now**. To exit, click **Cancel**.

6. After you submit the defragmentation task, the button changes to **Defragmentation in Progress**. When the defragmentation process ends, a message at the top of the page shows **Defragmentation Completed**, and the button becomes available again. Note that the completion prompt indicates only that the defragmentation process has ended. It does not mean that the related jobs have resumed operation, or that the expected contiguous GPU resources have been released.

7. After the defragmentation is complete, check the status of the compute group and the results of job execution or retries. If any jobs fail, handle them promptly according to your business requirements.

# Renewal/cancellation/deletion

## Renew

For running queues and queues that have been stopped due to expiration, renewal operations are supported. Renewal can only maintain the original configuration of the queue and does not support configuration changes.

1. On the details page of the queue to be renewed, click Renew to enter the relevant page.

2. After adjusting the **renewal duration**, click "Proceed to payment". Once payment is complete, you can continue to use the renewed queue. At this time, the status of the queue that was stopped due to expiration will return to `Running`.

## Unsubscribe

### Cancel the entire queue

For running queues, the following two methods are available:

* Find the target queue on the queue list page and click Unsubscribe in the **Actions** column on the right.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc6c0ba609da42bf84a506cc3e814871~tplv-goo7wpa0wc-image.image)

   > **注意**

   * > When unsubscribing from a queue, the system will check the current running status of the queue owner, as well as the status of computing groups and jobs within the queue. You can check again whether the queue needs to be unsubscribed before proceeding, and then confirm the unsubscription in the interface.

   * > After unsubscribing from the queue, the computing groups under the queue will become unavailable and jobs will fail. Please proceed with caution.

* Go to the BytePlusofficial platform to cancel. For detailed instructions, refer to [Unsubscription Rules Description](https://www.volcengine.com/docs/6269/81013) and .

> **说明**

> After successful unsubscription, the queue will no longer be available and will not be visible in the console.

### Cancel a specific resource specification from the queue

To unsubscribe a specific resource specification in the queue, refer to the earlier section "Resource configuration" and directly delete the resource configuration on the queue details page.

## Delete

Queues that failed to be created or have been released upon expiration can be deleted. At this point, the queue resources have already been released, and deletion only removes the queue record.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/003f7517f73a41258cfde27b837d54f5~tplv-goo7wpa0wc-image.image)

# Permission management

## Authorization & default usage permissions

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cf182a919294f768fa855879c49b663~tplv-goo7wpa0wc-image.image)

* Queue permissions are used to restrict different users' permissions on different queues. Currently, two roles are supported: Developer and Admin. The primary account has Admin permissions by default, while queue permissions for sub\-accounts need to be granted. For details, see [Queue permissions](https://www.volcengine.com/docs/6491/1327414?lang=zh).

* You can also modify the default usage permissions of the queue.

   In the queue operations dropdown, you can select "Disable" or "Enable" to set the default usage permissions of the queue.
