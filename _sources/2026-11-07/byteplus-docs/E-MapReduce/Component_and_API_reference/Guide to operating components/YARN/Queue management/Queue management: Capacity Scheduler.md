---
title: "Queue management: Capacity Scheduler"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/yarn_advanced_usage"
---

YARN in EMR uses the Capacity Scheduler by default and provides a convenient graphical interface for queue management configuration. You can also use command\-line methods for more flexible queue configuration with the Capacity Scheduler. This document introduces the details of queue configuration for the Capacity Scheduler.

# Context

EMR YARN queues support two types of schedulers: Capacity Scheduler (default) and Fair Scheduler, which meet resource allocation and scheduling requirements in different scenarios. The comparison between the two schedulers is introduced below.

|**Comparison dimensions** |**CapacityScheduler** |**FairScheduler** |
|---|---|---|
|**Core objectives** |Ensure each queue receives its preset capacity |Allow active queues or jobs to gradually obtain a fair share |
|**Resource allocation methods** |Mainly allocates resources based on capacity ratio or absolute resources, for example, a queue occupying 30% |Mainly configures minimum/maximum resources and weights |
|**Idle resources** |Queues can temporarily borrow unused resources from other queues, but are limited by the maximum capacity |Idle resources are dynamically allocated to queues with tasks |
|**Resource contention** |Places more emphasis on capacity guarantees and isolation between organizations |Places more emphasis on dynamic fairness when sharing clusters |
|**Preemption logic** |Resources exceeding the guaranteed share can be reclaimed through the preemption mechanism |Preemption can be triggered when a queue remains below its fair share for an extended period |
|**Configuration files** |capacity\-scheduler.xml |fair\-scheduler.xml |
|**Typical scenarios** |Multiple departments and tenants, with relatively clear resource budgets and quotas |Multiple users sharing a cluster, with significant changes in task volume, aiming to reduce waiting time for small tasks |
|**Default EMR scenarios** |YARN in EMR uses this by default |Requires modifying the scheduler configuration and deploying the Fair queue file |

This document provides details on configuring queue resources and scheduling rules for the Capacity Scheduler. Currently, configuration is supported via the EMR console interface, or you can log in to the YARN server and configure through the configuration file.

> **说明**

> To use the Fair Scheduler, manually switch the scheduler to Fair Scheduler and configure it. For details, see [Queue management: Fair Scheduler](https://docs.byteplus.com/docs/E-MapReduce/Yarn_Fair_Scheduler_configuration).

# Important and prerequisites

* Prerequisites

   * A cluster containing the YARN service has been created. For detailed steps, see: [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

   * EMR version is higher than 4.0.0. For information about the software stack version and included services, see: [EMR version overview](https://docs.byteplus.com/docs/undefined/6a18f85809180105088064f4).

* Important notes

   * Before making changes to the queue structure, stop the relevant queues, process according to the applicable activation method, and verify the result of the change.

   * Maintain compatibility between scheduling rules and existing queue configurations, and ensure that the trigger times of any two rules are at least 300 seconds apart.

   * Complete validation in the test environment before use in the production environment. After making changes, check the execution result, application status, and resource monitoring, and retain the operation log.

# Queue and scheduling configuration: UI operations

The EMR console provides a visual YARN queue management feature, supporting operations such as adding queues, modifying queue configurations, adjusting queue hierarchy, and enabling or disabling queues.

Queue management includes the following two tabs:

* **Queue configuration**: Manage queue hierarchy and queue parameters.

* **Scheduling rules**: Automatically switch queue parameters at specified times, suitable for tidal scenarios such as ensuring online business during the day and allocating more resources to offline jobs at night.

## Access the queue management page

1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home), and in the left navigation bar, select **Cluster management \> EMR on ECS**. Click the name of the target cluster to enter the cluster details page, select the **Service list** tab, and click **YARN** in the service list.

2. On the YARN service page, click the **Queue management** tab to enter the queue management page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc5ba28bec474153a938c34cb4f5b6ca~tplv-goo7wpa0wc-image.image)

   * The **Queue configuration** tab displays all YARN queues of the current cluster in a tree structure. You can view the status, capacity, and hierarchy of the queues, and perform related management operations.

   * YARN queues are organized in a tree structure. All queues are subqueues of the root queue. EMR provides a preset root parent queue and a default subqueue named default. You can create additional subqueues as needed and allocate the capacity ratio of each subqueue and other parameters.

## Queue configuration

### Add a subqueue

1. In the Queue tab on the queue management page, click **Add queue** in the upper right corner, and configure the parameters of the queue in the pop\-up sidebar.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86a263158bc649c0b5b7584b35e6bb9b~tplv-goo7wpa0wc-image.image)

   When adding a new subqueue, the default parent queue is the root queue. You can click Add Queue as needed to add more subqueues to the root parent queue, and adjust the capacity ratio and other parameters of all subqueues. The core configuration parameters of the subqueues are as follows.

   |Parameters |Note |
   |---|---|
   |Capacity ratio |The capacity ratio of the queue. The sum of the capacity ratios of all sub\-queues under the same parent queue must be 100. |
   |Maximum capacity ratio |When idle resources are available, the queue is allowed to use resources exceeding its capacity ratio, up to the maximum capacity ratio. This value must not be less than the capacity ratio. |
   |Status |Controls whether the sub\-queue is enabled. |

2. After the configuration is complete, click Confirm to finish adding the subqueue.

### Queue modification and management

You can view the list of YARN queues on the queue management page. For subqueues, you can click the Modify button to edit and modify the capacity parameters, status, and so on of the queue. You can also add new subqueues to the root parent queue.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c0b0cec3ba34c53afe42e31b9ae0e28~tplv-goo7wpa0wc-image.image)

## Configure tidal scheduling rules

### Add a tidal scheduling rule

Tidal scheduling rules are suitable for scenarios where the cluster's resource requirements change periodically over time. You can configure scheduling rules for business peak and off\-peak periods. For example, increase the resource ratio of the analyst task queue at 8:00 AM, and adjust it to prioritize offline tasks at 8:00 PM. Tidal scheduling rules automatically switch the resource allocation strategy of YARN subqueues at specified times, reducing manual operations and improving the utilization of cluster resources and the resource assurance capability during business peak periods.

1. In the Schedule tab of the queue management page, click Add Rule in the upper right corner, and configure queue parameters in the pop\-up sidebar.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b87f21296244a3880dad35face677e~tplv-goo7wpa0wc-image.image)

   |Parameters |Note |
   |---|---|
   |Rule name |The name of the custom scheduling rule, used for subsequent queries and identification. |
   |Queue |Set the queues to which the current scheduling rule applies. You can select an existing sub\-queue from the drop\-down list and set the capacity ratio and maximum capacity ratio of the corresponding sub\-queue under the current scheduling rule.<br><br><br>* The sum of the capacity ratio values of all sub\-queues must be 100.<br><br>* The value of maximum capacity ratio must be greater than the value of capacity ratio. |
   |Crom expression |Use a Cron expression to set the scheduling execution cycle.<br><br><br>* A Cron expression typically consists of five fields, from left to right: minute (0–59), hour (0–23), day of month (1–31), month (1–12), and day of week (0–7, where both 0 and 7 represent Sunday, and 1 represents Monday).<br><br>* The following special symbols are supported: `*` means every value of the field matches; `,` is used to enumerate multiple values, such as 1,3,5; `-` indicates a range, such as 1\-5; `/` is used to specify increments, such as `*/10` for every 10 units.<br><br>* Some common examples: `0 8 * * 1` means 8:00 AM every Monday, `0 9 * * 1-5` means 9:00 AM every weekday, `*/15 9-18 * * 1-5` means every 15 minutes from 9:00 AM to 6:00 PM on weekdays, and `0 0 1 * *` means midnight on the first day of each month. |
   |Operation remark |Add an operation note for the current scheduling rule. |

2. After completing the configuration, click add to finish configuring the scheduling rule.

3. You can configure multiple scheduling rules as needed.

### Start, stop, and manage scheduling rules

You can view the list of added scheduling rules on the scheduling rule page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0d675268d7e40c189f31f10ddde7ba7~tplv-goo7wpa0wc-image.image)

* You can view the status of each scheduling rule, the capacity allocation of subqueues, and more.

* You can also set to stop or start the corresponding scheduling rule as needed, or edit or delete the corresponding scheduling rule.

# Queue and scheduling configuration: command\-line operations

## Basic queue settings

YARN queues are organized in a tree structure. All queues are subqueues of the root queue. The queue path indicates the hierarchical relationship between queues, and different levels are separated by `.`. All cluster resources are attached under the root queue. Subqueues can divide the resources of the parent queue according to the configuration (if no division is specified, they can share the parent queue's resources by default).

Queues can be set through the following configurations.

```Plain
<property>
  <name>yarn.scheduler.capacity.root.queues</name>
  <value>a,b,c</value>
  <description>The queues at this level (root is the root queue).
  </description>
</property>

<property>
  <name>yarn.scheduler.capacity.root.a.queues</name>
  <value>a1,a2</value> # 
  <description>The queues at the this level (root is the root queue).
  </description>
</property>

<property>
  <name>yarn.scheduler.capacity.root.b.queues</name>
  <value>b1,b2,b3</value> # root.b.b1,roor.b.b2,root.b.b3
  <description>The queues at the this level (root is the root queue).
  </description>
</property>
```

For each queue path, such as root.a.a1, you can configure the basic attributes of queue usage in the configuration file.

|Parameter |Note |
|---|---|
|yarn.scheduler.capacity..capacity |Queue capacity, a floating\-point number representing the minimum capacity of the queue (YARN guarantees that the queue can obtain this amount of resources). Once configured, ensure that the sum of all sub\-queues under the parent queue of this queue is exactly 100; otherwise, an error will occur. During operation, the resource usage of applications in this queue may exceed the configured minimum capacity (if there are idle resources in other sub\-queues, they can be temporarily used to improve resource utilization). |
|yarn.scheduler.capacity..maximum\-capacity |Maximum queue usage, a floating\-point number representing the maximum resources the queue can use. The valid configuration range is 0–100, or you can set \-1 to represent 100%. Ensure that the sum of all sub\-queues under the parent queue of this queue is greater than or equal to 100; otherwise, some resources may not be usable. |
|yarn.scheduler.capacity..maximum\-allocation\-vcores |The maximum number of vcores that applications in the queue can request. |
|yarn.scheduler.capacity..maximum\-allocation\-mb |The maximum memory size that applications in the queue can request. |
|yarn.scheduler.capacity..user\-settings..weight |The weight of queue resources allocated to each user. Users with a higher weight are more likely to obtain resources. |
|More parameters |Refer to the [open-source configuration parameter documentation](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html) for more information. |

In addition to configuring queue capacity proportionally, you can also use `yarn.scheduler.capacity.<queue-path>.capacity` and `yarn.scheduler.capacity.<queue-path>.max-capacity` to configure absolute capacity, such as `[memory=10240,vcores=12]`.

You can also configure to limit the number of jobs in the queue.

|Parameter |Note |
|---|---|
|yarn.scheduler.capacity.maximum\-applications |The maximum number of runnable jobs in the queue. This is a global configuration, with a default value of 10,000. If this number is reached, any further attempts to Submit Job to the same queue will be rejected. |
|yarn.scheduler.capacity..maximum\-applications |The maximum number of runnable jobs in a specific queue. |
|yarn.scheduler.capacity.maximum\-am\-resource\-percent |The maximum proportion of ApplicationMaster resources used in the queue. This is a global configuration. Valid values are between 0 and 1, with a default of 0.1. |
|yarn.scheduler.capacity..maximum\-am\-resource\-percent |The maximum proportion of ApplicationMaster resources used in a specific queue. |
|yarn.scheduler.capacity.max\-parallel\-apps |The maximum number of jobs that can run concurrently in the queue. This is a global configuration. Unlike maximum\-applications, jobs submitted after this number is reached are not rejected but remain in the ACCEPTED state and wait. |
|yarn.scheduler.capacity..max\-parallel\-apps |The maximum number of jobs that can run concurrently in a specific queue. |

For more basic queue settings, refer to the [open-source parameter configuration documentation](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html).

## Queue permission settings

YARN queues support setting specific access permissions for users. Access permissions for specific queues are divided into two types: Submit Job permission and queue management permission.

To enable queue permissions, set yarn.acl.enable to true in yarn\-site (if YARN enables Ranger permission control, this configuration defaults to true. In this case, it is recommended to use Ranger to manage YARN queue permissions and not to set it repeatedly).

You can specify that specific users have YARN admin operation permissions by setting yarn.admin.acl. The default is the yarn user. The logic for user settings is as follows:

* Separate multiple users with commas.

* If left empty, it means no user has this permission.

* You can use `*` to indicate that any user has this permission.

Set permissions for a specific queue:

|Parameters |Note |
|---|---|
|yarn.scheduler.capacity.root..acl_submit_applications |Set the users who have permission to Submit Job to this queue. |
|yarn.scheduler.capacity.root..acl_administer_queue |Set the users who have permission to administer this queue. |

## Preemption configuration

Yarn supports task preemption. Task preemption is divided into inter\-queue preemption and intra\-queue preemption, with inter\-queue preemption enabled by default. To configure preemption, enable the preemption feature in `yarn-site.xml` and make specific configurations in `capacity-scheduler.xml`.

* yarn\-site.xml

   |Parameters |Note |
   |---|---|
   |yarn.resourcemanager.scheduler.monitor.enable |Whether to enable the preemption feature. The default is false. |

* capacity\-scheduler.xml

   |Parameters |Note |
   |---|---|
   |yarn.resourcemanager.monitor.capacity.preemption.intra\-queue\-preemption.enabled |Whether to enable intra\-queue preemption. The default is false. |
   |yarn.resourcemanager.monitor.capacity.preemption.intra\-queue\-preemption.preemption\-order\-policy |The application sorting policy, which can be userlimit_first or priority_first. The former is user quota preemption, and the latter is priority preemption. The default is userlimit_first. |
   |yarn.scheduler.capacity..disable_preemption |Specifies that the queue cannot be preempted. By default, it inherits the value set by the parent queue. |
   |yarn.scheduler.capacity..intra\-queue\-preemption.disable_preemption |Specifies that the queue does not support intra\-queue preemption. By default, it inherits the value set by the parent queue. |
