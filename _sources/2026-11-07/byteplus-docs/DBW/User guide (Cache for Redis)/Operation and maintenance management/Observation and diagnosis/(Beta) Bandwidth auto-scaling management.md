---
title: "(Beta) Bandwidth auto-scaling management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/automatic-bandwidth-scaling-management-for-redis"
---

The Database Workbench DBW provides a bandwidth auto\-scaling feature. When bandwidth usage reaches a threshold, the Redis instance's bandwidth automatically scales according to the configured scaling rules, helping you flexibly handle sudden traffic changes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Redis instance has been created and is in the **Running** state. For detailed steps, refer to [Create Instance](https://docs.byteplus.com/en/docs/redis/create-instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* This feature is currently in the invitation\-only testing phase. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact the technical support of Database Workbench DBW.

* Currently, only scaling up is supported; scaling down is not available.

* A maximum of 2000 bandwidth auto\-scaling rules can be created under a single account. A maximum of one bandwidth auto\-scaling rule can be created for a single instance.

* Instances with a node specification of 256MiB and no sharded cluster enabled do not support setting bandwidth auto\-scaling.

* Expanding bandwidth will not impact your business.

* Only instances created after May 25, 2023 support bandwidth modification. For instances created before May 25, 2023 that require shard bandwidth modification, you need to create a new instance and migrate data from the old instance to the new instance using tools like DTS, then use this feature on the new instance. For steps on migrating instances, refer to [Data Migration](https://docs.byteplus.com/en/docs/redis/data-migration).

* Instances accessing the Redis Enterprise Edition of the cache database are not currently supported. The Redis Enterprise Edition of the cache database is currently in the invitation\-only testing phase. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to request the service. For detailed information about the Redis Enterprise Edition of the cache database, refer to [What is the Redis Enterprise Edition of the cache database](https://docs.byteplus.com/en/docs/redis/about-redis).

* During the use of the bandwidth auto\-scaling feature, do not modify instance\-related configurations, as this may prevent the proper use of bandwidth auto\-scaling for instance expansion.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [DBW Console](https://console.byteplus.com/dbw).

2. In the top menu bar, select a region.

3. In the left navigation bar, select **Operations Management** \> **Observability and Diagnostics**.

4. In the upper\-right corner of the **Operations Observability** page, switch the instance type to **Redis Cache Database**.

5. On the **Bandwidth Auto\-Scaling** tab, click **Bandwidth Auto\-Scaling Configuration**.

6. In the **Bandwidth Auto\-Scaling Configuration** dialog, configure the following parameters.

   
   |**Parameters** |**Note** |
   |---|---|
   |**Automatic Bandwidth Expansion** |Click the **Enable** button to turn on the automatic bandwidth expansion feature. |
   |**Bandwidth Average Utilization Greater Than** |Set the threshold for triggering automatic bandwidth expansion on demand, in percentage, with a range of 70.00%~99.00%.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The system will take the larger value between the average inbound and outbound traffic usage as the average bandwidth usage.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Redis instances of different node specifications support various maximum bandwidth expansion values. Refer to <a href="https://docs.byteplus.com/en/docs/redis/modify-bandwidth#.5bim5a695L-u5pS56IyD5Zu0">Redis Instance Bandwidth Modification Range</a> for details.</div><br> |
   |**Observation Window** |Select the observation window time from the dropdown list, in minutes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, automatic bandwidth expansion: When <strong>the average bandwidth usage is greater than</strong> set to 70%, and the <strong>observation window</strong> is set to 5 minutes, it means that if the average bandwidth usage exceeds 70% within the 5\-minute observation window, the system will perform a bandwidth expansion operation on the instance.</div><br> |
   

7. Click **OK**.


&nbsp;
