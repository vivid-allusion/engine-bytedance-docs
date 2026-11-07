---
title: "Queue management: Fair Scheduler"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Yarn_Fair_Scheduler_configuration"
---

By default, EMR YARN uses Capacity Scheduler. To enable multiple queues to dynamically and fairly share cluster resources for business needs, you can switch to Fair Scheduler. This document describes how to enable Fair Scheduler and manually configure its parameters.

# Context

EMR YARN queues support two types of schedulers: Capacity Scheduler (default) and Fair Scheduler. These can meet resource allocation and scheduling requirements in different scenarios. The following introduces a comparison of the two schedulers.

|**Comparison dimensions** |**CapacityScheduler** |**FairScheduler** |
|---|---|---|
|**Core objectives** |Ensure each queue receives its preset capacity |Allow active queues or jobs to gradually obtain a fair share |
|**Resource allocation methods** |Mainly allocates resources by capacity ratio or absolute value, such as a queue occupying 30% |Mainly configures minimum/maximum resources and weights |
|**Idle resources** |Queues can temporarily borrow unused resources from other queues, but are limited by the maximum capacity |Idle resources are dynamically allocated to queues with tasks |
|**Resource contentions** |Emphasizes capacity guarantees and isolation between organizations |Emphasizes dynamic fairness when sharing clusters |
|**Preemption logics** |Can reclaim resources exceeding guaranteed shares through preemption mechanisms |Can trigger preemption when a queue remains below its fair share for an extended period |
|**Configuration files** |capacity\-scheduler.xml |fair\-scheduler.xml |
|**Typical scenarios** |Multiple departments and tenants, with relatively clear resource budgets and quotas |Multiple users sharing a cluster, with significant fluctuations in workload, aiming to reduce waiting time for small tasks |
|**Default EMR scenarios** |YARN in EMR uses this by default |Modify the scheduler configuration and deploy the Fair queue file. |

This document describes how to switch from the default Capacity Scheduler to Fair Scheduler, and how to configure queue resources and scheduling rules.

> **说明**

> For details on configuring queue resources and scheduling rules for the Capacity Scheduler, see [Queue management: Capacity Scheduler](https://docs.byteplus.com/docs/E-MapReduce/yarn_advanced_usage).

# Important and prerequisites

* Prerequisites

   * A cluster containing the YARN service has been created. For detailed steps, see [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

   * The EMR version is higher than 4.0.0. For information about the software stack version and included services, see [EMR version overview](https://docs.byteplus.com/docs/undefined/6a18f85809180105088064f4).

* Important notes

   * When switching schedulers, you must manually check and handle the compatibility of queue configurations and scheduling rules. Set minimum and maximum resource limits, weights, and other parameters reasonably according to the actual cluster resources and application requirements to avoid resource waste or excessive competition.

   * Before making changes to the queue structure, stop the relevant queues, apply the appropriate activation method, and verify the results of the changes.

   * Keep scheduling rules compatible with existing queue configurations, and ensure that the trigger times of two rules are at least 300 seconds apart.

   * Before using it in a production environment, it is recommended to fully test the effectiveness and stability of the Fair queue configuration in a test environment, then apply it to the production cluster. After making changes, check the execution results, application status, and resource monitoring, and retain operation logs.

# Switch to enable Fair Scheduler

1. Go to the EMR cluster details page and select **Service List \> YARN \> Service Parameters**.

2. Set `yarn.resourcemanager.scheduler.class` to `org.apache.hadoop.yarn.server.resourcemanager.scheduler.fair.FairScheduler`.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebceb464bac140f1bcd02d32efed788a~tplv-goo7wpa0wc-image.image)

3. Set `yarn.resourcemanager.scheduler.monitor.enable` to `false`.

4. Save the configuration, enter operation remarks, and then follow the console prompts to restart the service.

5. After the restart is complete, you can view the current scheduler type on the queue management page to confirm that the policy has been switched to Fair Scheduler. You can then configure queues and scheduling rules.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d22bf483c574b219848609908565267~tplv-goo7wpa0wc-image.image)

# Queue and scheduling configuration: UI operations

The EMR console provides visual YARN queue management capabilities, supporting operations such as adding queues, modifying queue configurations, adjusting queue hierarchy, and enabling or disabling queues.

Queue management includes the following two tabs:

* **Queue configuration**: Manage queue hierarchy and queue parameters.

* **Scheduling rules**: Automatically switch queue parameters at specified times, suitable for tidal scenarios such as ensuring online business during the day and allocating more resources to offline jobs at night.

## Queue configuration

### Add a sub\-queue

1. On the queue management page, in the Queue tab, click Add queue in the upper right corner, and configure queue parameters in the pop\-up sidebar.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf4ca291235c46baaec857c7392c5148~tplv-goo7wpa0wc-image.image)

   When adding a sub\-queue, the default parent queue is the root queue. You can click Add Queue as needed to add more sub\-queues to the root parent queue, and adjust parameters such as the queue name and weight for all sub\-queues. The core configuration parameters for sub\-queues are as follows.

   |Parameters |Note |
   |---|---|
   |weight |The relative resource allocation weight of each sub\-queue under the same parent queue. This does not represent task execution priority. When other conditions are the same, a higher weight results in a larger fair share. Actual resource usage is still subject to resource demand and resource upper and lower limits. |
   |minResources |The minimum resource share for the queue. When resources are insufficient and the queue has not reached its share, the scheduler prioritizes allocating available resources to it. If resources are already occupied by running applications, the queue is not guaranteed to immediately reach its share.<br><br>minResource supports the following three resource configuration methods:<br><br><br>* **Relative resources**: Enter an integer percentage.<br><br>* **Absolute resources**: Enter the number of vCPU cores and memory size, both as integers.<br><br>* **Resource percentage**: Enter the percentage of vCPU and memory, both as integers. |
   |maxResources |The upper limit of resources that can be allocated to the queue, also subject to the parent queue's resource upper limit.<br><br>maxResources supports the following three resource configuration methods:<br><br><br>* **Relative resources**: Enter an integer percentage.<br><br>* **Absolute resources**: Enter the number of vCPU cores and memory size, both as integers.<br><br>* **Resource percentage**: Enter the percentage of vCPU and memory, both as integers. |
   |maxRunningApps |The maximum number of applications running simultaneously in the queue. |
   |schedulingPolicy |Controls the resource allocation method within the queue:<br><br><br>* **DRF**: Allocates resources fairly based on the dominant resource, considering both CPU and memory.<br><br>* **FAIR**: Allocates resources based on fair share, primarily considering memory by default.<br><br>* **FIFO**: Prioritizes allocating resources to applications submitted earlier. This does not mean applications must execute serially. |
   |Operation remark |Add an operation note for the current scheduling rule. |

2. After completing the configuration, click Confirm to finish adding the sub\-queue.

### Queue modification and management

You can view the queue list of YARN queues on the queue management page. For sub\-queues, you can click the Modify button to edit and change the queue's weight, resource allocation logic, and more. You can also add new sub\-queues to the root parent queue.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0695cbc87b647f7a46f0d21e58aaee9~tplv-goo7wpa0wc-image.image)

## Configure scheduling rules

### Add scheduling rules

Tidal scheduling rules are suitable for scenarios where cluster resource requirements change periodically over time. You can configure scheduling rules for business peak and off\-peak periods respectively. For example, increase the resource share of the analyst task queue at 8:00 AM, and adjust to prioritize offline tasks at 8:00 PM. By using tidal scheduling rules, you can automatically switch the resource allocation strategy of YARN sub\-queues at specified times, reducing manual operations and improving cluster resource utilization and resource assurance during business peak periods.

1. On the queue management page, in the Queue tab, click Add rule in the upper right corner, and configure queue parameters in the pop\-up sidebar.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/531dd64253ee4382be3b042c21893ba9~tplv-goo7wpa0wc-image.image)

   |Parameters |Note |
   |---|---|
   |Rule name |The name of the custom scheduling rule, used for subsequent queries and identification. |
   |Queue |Set the queue to which the current scheduling rule applies. You can select an existing sub\-queue from the dropdown and configure the weight, resource classification logic, and more for the corresponding sub\-queue under the current scheduling rule. |
   |Cron expression |Set the scheduling execution cycle using a Cron expression.<br><br><br>* Cron expressions typically consist of five fields, listed from left to right as follows: minute (0–59), hour (0–23), day of the month (1–31), month (1–12), and day of the week (0–7, where both 0 and 7 represent Sunday, and 1 represents Monday).<br><br>* The following special symbols are supported: `*`matches every value in the field; `,`is used to enumerate multiple values, such as 1,3,5; `-`indicates a range, such as 1\-5; `/`sets the step value, for example, `*/10` means every 10 units.<br><br>* Some common examples: `0 8 * * 1`means 8:00 AM every Monday, `0 9 * * 1-5`means 9:00 AM every weekday, `*/15 9-18 * * 1-5` means every 15 minutes from 9:00 AM to 6:00 PM on weekdays, and `0 0 1 * *`means midnight on the first day of each month. |
   |Operation remark |Add an operation note for the current scheduling rule. |

2. After completing the configuration, click Add to finish configuring the scheduling rule.

3. You can configure multiple scheduling rules as needed.

### Start, stop, and manage scheduling rules

You can view the list of added scheduling rules on the scheduling rules page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec8cce4c2d044923ab5b9deb1af334e4~tplv-goo7wpa0wc-image.image)

* You can view the status of each scheduling rule, the capacity allocation of sub\-queues, and more.

* You can also stop or start, edit, or delete the corresponding scheduling rules as needed.

# Queue and scheduling configuration: command\-line operations

When you need to use parameters not covered by the console, such as configuring user\-to\-queue mapping or setting the queue preemption policy, refer to the following manual configuration methods.

## Step 1: Create a Fair queue configuration file

1. Log in to the server node running YARN.

2. Use a text editor (such as vi or nano) to create a new configuration file, for example, fair\-scheduler.xml.

3. In the configuration file, first define the root queue, which is the parent queue of all other queues.

   ```XML
   <allocations><queue name="root"><minResources>10000 mb,0 vcores</minResources><maxResources>40000 mb,4 vcores</maxResources><weight>1.0</weight><schedulingPolicy>fair</schedulingPolicy></queue></allocations>
   ```

   This defines the minimum resources (10,000 MB of memory and 0 virtual cores), maximum resources (40,000 MB of memory and 4 virtual cores), weight (1.0), and the scheduling policy as fair for the root queue.

## Step 2: Modify configuration parameters

You can set more configuration parameters in the configuration file. The following are configuration examples for some typical scenarios.

### Add sub\-queues

You can add multiple sub\-queues within the root queue. For example, add two sub\-queues, queue1 and queue2:

```XML
<queue name="queue1"><minResources>5000 mb,0 vcores</minResources><maxResources>20000 mb,2 vcores</maxResources><weight>2.0</weight><schedulingPolicy>fair</schedulingPolicy></queue><queue name="queue2"><minResources>3000 mb,0 vcores</minResources><maxResources>15000 mb,1 vcores</maxResources><weight>1.5</weight><schedulingPolicy>fair</schedulingPolicy></queue>
```

Each sub\-queue has its own minimum and maximum resource limits, weight, and scheduling policy. The weight determines the relative importance of the queue in resource allocation.

### Configure user\-to\-queue mapping

To assign applications from specific users to specific queues, configure user\-to\-queue mapping. For example, assign applications from user1 to queue1 and applications from user2 to queue2:

```XML
<user name="user1"><queue>queue1</queue></user><user name="user2"><queue>queue2</queue></user>
```

### (Optional) Set the queue preemption policy

To allow a queue to preempt resources from other queues when resources are insufficient, configure the preemption policy. For example, allow queue1 to preempt resources from other queues when resources are insufficient:

1. Set `yarn.resourcemanager.scheduler.monitor.enable` to true.

2. Modify the preemption policy

   ```XML
   <queue name="queue1"><minResources>5000 mb,0 vcores</minResources><maxResources>20000 mb,2 vcores</maxResources><weight>2.0</weight><schedulingPolicy>fair</schedulingPolicy><queueMaxAMShare>0.5</queueMaxAMShare><fairSharePreemptionTimeout>60000</fairSharePreemptionTimeout><fairSharePreemptionThreshold>0.5</fairSharePreemptionThreshold></queue>
   ```

   Here, queueMaxAMShare indicates the maximum resource allocation ratio for applications in the queue, fairSharePreemptionTimeout specifies the preemption timeout (in milliseconds), and fairSharePreemptionThreshold indicates the preemption threshold.

## Step 3: Save and deploy the configuration file

1. Save the fair\-scheduler.xml configuration file.

2. Copy the configuration file to Yarn's configuration directory, typically the $HADOOP_HOME/etc/hadoop/ directory.

3. In Yarn's configuration file yarn\-site.xml, add or modify the following properties to specify the use of the Fair Scheduler and the configuration file path (these can be modified in Component Management \- Service Management \- Yarn \- Configuration Files).

   ```XML
   <property><name>yarn.resourcemanager.scheduler.class</name><value>org.apache.hadoop.yarn.server.resourcemanager.scheduler.fair.FairScheduler</value></property><property><name>yarn.scheduler.fair.allocation.file</name><value>/path/to/fair-scheduler.xml</value></property>
   ```

   Ensure that /path/to/fair\-scheduler.xml is replaced with the actual configuration file path.

## Step 4: Restart the Yarn service

In the corresponding EMR cluster, restart the Resource Manager and all Node Managers in Component Management \- Service Management \- Yarn.

## Step 5: Verify the configuration

Submit several applications to the Yarn cluster and check whether resources are allocated according to the Fair queue configuration. You can use Yarn's command\-line tools (such as yarn application \-list and more) to view the running status and resource allocation of applications.
