---
title: "Configure user group queue mapping"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Configure_user_group_queue_mapping"
---

The Volcano Engine E\-MapReduce (EMR) console allows you to visually manage YARN cluster queue resources, including adding, renaming, and deleting queues. You can also configure queue mappings based on user groups to ensure that tasks from specified user groups are submitted to designated queues according to rules.

<span id="d234998c"></span>
## Prerequisites


1. A cluster type that includes the YARN service and has an EMR version higher than 3.4.1 / 2.3.1 has been created. For details, see [Create a cluster](https://docs.byteplus.com/docs/E-MapReduce/105456).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about EMR software stack versions and specific services, please refer to the document <a href="https://docs.byteplus.com/docs/undefined/68da347242e561058e056938">EMR version overview</a>.</div>



2. The YARN scheduler must use Capacity Scheduler.


<span id="c0291552"></span>
## Add users and user groups


1. Log in to the [EMR console](https://console.volcengine.com/emr/).

2. Click **Resource Management \> Cluster Name** to enter the cluster details page.

3. Add users by following the steps below. For details, see [User Management](https://docs.byteplus.com/docs/E-MapReduce/105426).

* **Add user groups**

   On the cluster details page, click **User Management \> User Groups \> Add User Group.** 

* **Add users**

   On the cluster details page, click **User Management \> Regular Users \> Add User \> Manually Add User.** 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">New users must be added to the corresponding user groups.   </div>
   

<span id="22c7d32b"></span>
## Add a queue


1. Log in to the [EMR console](https://console.volcengine.com/emr).

2. In the right navigation bar, click **Cluster Management \> Cluster List \> Cluster Name** to enter the cluster details page.

3. On the cluster details page, click **Service Management \> YARN \> Queue Management** to enter the queue management page.

4. On the queue management page, click the **Add Queue** button on the right to add a new queue. Refer to [YARN Queue Management](https://docs.byteplus.com/docs/E-MapReduce/109542).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After adding a new queue, click <strong>Refresh Queue</strong> to activate the queue.</div>


<span id="9d83fb84"></span>
## Configure user group queue mapping

Use the queue mapping feature of the Capacity Scheduler. In the capacity\-scheduler.xml configuration file, use **yarn.scheduler.capacity.queue\-mappings** to configure the default queue rules for users or user groups to submit jobs, ensuring that jobs are forced to use the mappings specified in Queue Mappings.

On the cluster page, click **Service Management \> YARN \> Service Parameters \> capacity\-scheduler** to modify and locate the queue parameter configuration.

Here, two queue mappings are configured for developerQueue and qaQueue. Each queue uses `PlacementRule` for user\-to\-queue mapping, consistent with the visual configuration: in `capacity-scheduler.xml`, modify the following default configuration to `true`.

```Bash
  <property>
    <name>yarn.scheduler.capacity.queue-mappings-override.enable</name>
    <value>true</value>
  </property>
```


New queue configuration:

```Bash
<property>
    <name>yarn.scheduler.capacity.queue-mappings</name>
    <value>
        g:developer:developerQueue,g:qa:qaQueue
    </value> 
</property> 
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">There is no need to add the root. prefix to the new queue name; simply enter the queue name directly.</div>


* <div data-tips="true" data-tips-type="warning">If the queue name is entered incorrectly, YARN ResourceManager will fail to start and report an error.</div>



The value of yarn.scheduler.capacity.queue\-mappings follows these rules: `u:%user:queueA,g:%group:queueB`: `%user` is a placeholder representing the user's username; `%group` is the user's primary group. This rule means that if a job is submitted by a specified user group, it will be automatically submitted to the corresponding queue.

In the above configuration, jobs submitted by the developer group are directed to developerQueue, and jobs submitted by the qa group are directed to qaQueue.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After modifying the configuration, you must restart <strong>YARN ResourceManager</strong> , otherwise the configuration will not take effect.</div>


* <div data-tips="true" data-tips-type="warning">Queue mapping is highly flexible. It allows mapping based on username, user group, or even the application name used to submit the application.</div>


* <div data-tips="true" data-tips-type="warning">The configuration of <code>PlacementRule</code> is highly flexible. You can adjust the rules according to actual requirements to better fit your organizational structure.</div>


* <div data-tips="true" data-tips-type="warning">When troubleshooting errors, check the YARN ResourceManager logs to confirm that the mapping rules are effective.</div>



By following these steps, you can automatically submit jobs to different queues based on user groups, which helps better manage and separate resource usage for different projects or departments.

<span id="10d33f16"></span>
## Configuration validation

Log in to the cluster and use hadoop or spark\-sql to submit jobs. Submit YARN jobs with different users for quick validation.

Access the YARN ResourceManager UI page. For detailed instructions, refer to [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

You can view the jobs and queues submitted by users on the YARN ResourceManager UI page.

**Example**


1. Log in via ssh as user anfa. The anfa user belongs to the developer group. Submit a YARN job, such as spark\-sql \-\-master yarn.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d174a1e81dce4affaa493c9d16cee3b8~tplv-goo7wpa0wc-image.image" width="2258px" /></div>



2. Log in via ssh as user qa1. The qa1 user belongs to the qa group. Submit a YARN job, such as spark\-sql \-\-master yarn.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd66f5d2d38b414e90f46d6fff2615d4~tplv-goo7wpa0wc-image.image" width="1756px" /></div>



3. Observe the YARN ResourceManager UI page. At this point, the task submitted by anfa is in root.developerQueue, and the task submitted by qa1 is in root.qaQueue.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c1b7c38aca4ef6be2b272843767e80~tplv-goo7wpa0wc-image.image" width="3390px" /></div>



4. Jobs from different user groups have been submitted to their corresponding queues, and the configuration is effective.
