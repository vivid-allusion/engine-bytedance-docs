---
title: "Instance management FAQ"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Instance-FAQs"
---

* Add instances

   * [How do I configure automatic scale-out for a scaling group?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5aaC5L2V6YWN572u5L2_5Ly457yp57uE6Ieq5Yqo5omp5a655a6e5L6L77yf)

   * [What are the restrictions when I manually add instances?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5omL5Yqo5re75Yqg5a6e5L6L5pe25pyJ5LuA5LmI6ZmQ5Yi26KaB5rGC77yf)

   * [Can Subscription instances be added?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5pSv5oyB5re75Yqg5YyF5bm05YyF5pyI5a6e5L6L5ZCX77yf)

   * [How do I troubleshoot the failure to add or create instances?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5peg5rOV5re75Yqg5oiW5Yib5bu65a6e5L6L77yM6K-l5aaC5L2V5o6S5p-l5Y6f5Zug77yf)

   * [Is the EIP assigned by a scaling group to an instance a newly automatically purchased one, or an existing unassociated EIP?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5Ly457yp57uE5Li65a6e5L6L5YiG6YWN55qE5YWs572RSVDvvIzmmK_oh6rliqjmlrDotK3vvIzov5jmmK_liIbphY3lt7LmnInkvYbmnKrnu5HlrprotYTmupDnmoTlhaznvZFJUO-8nw==)

   * [Can an instance be added to multiple scaling groups simultaneously?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5a6e5L6L5pSv5oyB5ZCM5pe25re75Yqg5Yiw5aSa5Liq5Ly457yp57uE5Lit5ZCX77yf)

* Manage instances

   * [How do I upgrade or downgrade configuration, associate a secondary network interface, or change the password for an instance created by a scaling group?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.6YCa6L-H5Ly457yp57uE5Yib5bu655qE5a6e5L6L77yM5aaC5L2V5a6M5oiQ5a6e5L6L5Y2H6ZmN6YWN44CB57uR5a6a6L6F5Yqp572R5Y2h44CB5L-u5pS55a-G56CB562J5pON5L2c77yf)

* Delete instances

   * [How do I configure automatic instance removal for a scaling group?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5aaC5L2V6YWN572u5L2_5Ly457yp57uE6Ieq5Yqo56e75Ye65a6e5L6L77yf)

   * [How do I delete instances in a scaling group?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5aaC5L2V5Yig6Zmk5Ly457yp57uE5Lit55qE5a6e5L6L77yf)

   * [How do I troubleshoot the failure to delete instances in the Auto Scaling console?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5peg5rOV5Zyo5by55oCn5Ly457yp5o6n5Yi25Y-w5Lit5Yig6Zmk5a6e5L6L77yM6K-l5aaC5L2V5o6S5p-l5Y6f5Zug77yf)

   * [How are instances to be deleted selected when a scaling group scales in?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5Ly457yp57uE5omn6KGM57yp5a656KGM5Li65pe277yM5aaC5L2V6YCJ5oup5b6F5Yig6Zmk55qE5a6e5L6L77yf)

   * [How do I prevent an instance from being deleted by automatic scale-in?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5aaC5L2V6Zi75q2i5a6e5L6L6KKr6Ieq5Yqo57yp5a656KGM5Li65Yig6Zmk77yf)

* Instance health check

   * [What is the difference between the health check of Auto Scaling and the health check of Load Balancer?](https://docs.byteplus.com/en/docs/as/Instance-FAQs#.5by55oCn5Ly457yp55qE5YGl5bq35qOA5p-l5ZKM6LSf6L295Z2H6KGh55qE5YGl5bq35qOA5p-l5pyJ5LuA5LmI5Yy65Yir77yf)


<span id=".5re75Yqg5a6e5L6L"></span>
## Add instances

<span id=".5aaC5L2V6YWN572u5L2_5Ly457yp57uE6Ieq5Yqo5omp5a655a6e5L6L77yf"></span>
### How do I configure automatic scale\-out for a scaling group?

The health check or scaling rule feature can help you monitor the status of instances in a scaling group and automatically trigger scale\-out activities. For more information, see [Automatically scaling out instances](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically).

<span id=".5omL5Yqo5re75Yqg5a6e5L6L5pe25pyJ5LuA5LmI6ZmQ5Yi26KaB5rGC77yf"></span>
### What are the restrictions when I manually add instances?

Only the primary network interface of an instance can be added to a scaling group. Before you add an instance to a scaling group, you need to confirm the items described in the following table.


|Project |Prerequisites |
|---|---|
|Instance<br><br>Scaling group |* The instance must be in the same availability zone and VPC as the scaling group.<br><br>* The instance must be in the **Running** status.<br><br>* The instance must not already exist in other scaling groups.<br><br>   The scaling group must be in the **Running** or **Cooling** status. |


For more information, see [Manually adding instances](https://docs.byteplus.com/en/docs/as/Adding-instances-manually).

<span id=".5pSv5oyB5re75Yqg5YyF5bm05YyF5pyI5a6e5L6L5ZCX77yf"></span>
### Can Subscription instances be added?

Yes.

<span id=".5peg5rOV5re75Yqg5oiW5Yib5bu65a6e5L6L77yM6K-l5aaC5L2V5o6S5p-l5Y6f5Zug77yf"></span>
### How do I troubleshoot the failure to add or create instances?


* A single scaling group supports up to 300 instances at the same time. Confirm the current number of instances in the scaling group.

* Make sure that there are sufficient compute, storage, and network resources in the associated availability zone. Otherwise, instance creation may fail.

* Only instances of the same billing type can be added in a single operation. Otherwise, the entire addition will fail.

* The sum of the instance count or capacity that you want to add and the existing instance count or capacity in the scaling group must not exceed the maximum instance count or capacity of the scaling group or the expected instance count or capacity.

* A single instance can be added to only one scaling group. Make sure that the instance is not in other scaling groups.


<span id=".5Ly457yp57uE5Li65a6e5L6L5YiG6YWN55qE5YWs572RSVDvvIzmmK_oh6rliqjmlrDotK3vvIzov5jmmK_liIbphY3lt7LmnInkvYbmnKrnu5HlrprotYTmupDnmoTlhaznvZFJUO-8nw=="></span>
### Is the EIP assigned by a scaling group to an instance a newly automatically purchased one, or an existing unassociated EIP?

After an instance is added, the scaling group automatically purchases and assigns a new EIP based on the network configuration of the [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).

<span id=".5a6e5L6L5pSv5oyB5ZCM5pe25re75Yqg5Yiw5aSa5Liq5Ly457yp57uE5Lit5ZCX77yf"></span>
### Can an instance be added to multiple scaling groups simultaneously?

No.

<span id=".566h55CG5a6e5L6L"></span>
## Manage instances

<span id=".6YCa6L-H5Ly457yp57uE5Yib5bu655qE5a6e5L6L77yM5aaC5L2V5a6M5oiQ5a6e5L6L5Y2H6ZmN6YWN44CB57uR5a6a6L6F5Yqp572R5Y2h44CB5L-u5pS55a-G56CB562J5pON5L2c77yf"></span>
### How do I upgrade or downgrade configuration, associate a secondary network interface, or change the password for an instance created by a scaling group?

In the Auto Scaling console, only operations related to associating instances with a scaling group are supported. These operations include adding instances to a scaling group, enabling protection for instances, removing instances from a scaling group, and deleting instances. For regular operations such as modifying instance attributes and associating volumes/EIPs, there is no difference from instances created in the ECS console. You can perform and manage these operations in the [ECS console](https://console.byteplus.com/ecs/instance). For more information, see [ECS product documentation](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service).

<span id=".5Yig6Zmk5a6e5L6L"></span>
## Delete instances

<span id=".5aaC5L2V6YWN572u5L2_5Ly457yp57uE6Ieq5Yqo56e75Ye65a6e5L6L77yf"></span>
### How do I configure automatic instance removal for a scaling group?

The health check or scaling rule feature can help you monitor the anomalies of a scaling group and automatically trigger scale\-in activities. For more information, see [Automatically removing instances](https://docs.byteplus.com/en/docs/as/Removing-instances-manually).

<span id=".5aaC5L2V5Yig6Zmk5Ly457yp57uE5Lit55qE5a6e5L6L77yf"></span>
### How do I delete instances in a scaling group?


* Automatic deletion:

   * When the health check feature detects an anomaly or the scaling group scales in, instances whose lifecycle is managed by the scaling group are automatically deleted.

   * When the health check feature detects an anomaly or the scaling group scales in, instances whose lifecycle is not managed by the scaling group are only removed from the scaling group. If you want to delete such instances, you need to use the [ECS console](https://console.byteplus.com/ecs/instance).

* Manual deletion:

   * For instances without instance protection enabled, you can manually delete them from the scaling group.

   * Instances with instance protection enabled cannot be deleted from the scaling group. We recommend that you first [disable instance protection](https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection#.5YWz6Zet5a6e5L6L5L-d5oqk), and then [manually delete the instances](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).

   * For more information, see [Manually deleting instances](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).


<span id=".5peg5rOV5Zyo5by55oCn5Ly457yp5o6n5Yi25Y-w5Lit5Yig6Zmk5a6e5L6L77yM6K-l5aaC5L2V5o6S5p-l5Y6f5Zug77yf"></span>
### How do I troubleshoot the failure to delete instances in the Auto Scaling console?

Instances with instance protection enabled cannot be deleted from the scaling group. We recommend that you first [disable instance protection](https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection#.5YWz6Zet5a6e5L6L5L-d5oqk), and then [manually delete the instances](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually).

<span id=".5Ly457yp57uE5omn6KGM57yp5a656KGM5Li65pe277yM5aaC5L2V6YCJ5oup5b6F5Yig6Zmk55qE5a6e5L6L77yf"></span>
### How are instances to be deleted selected when a scaling group scales in?


* When you manually [remove](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically)/[delete](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually) instances, you can select the instances to delete based on your needs.

* For automatic scale\-in triggered by health checks, instance count checks, or scaling rules, the instances to delete are selected based on the [instance removal policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually) specified for the scaling group.


<span id=".5aaC5L2V6Zi75q2i5a6e5L6L6KKr6Ieq5Yqo57yp5a656KGM5Li65Yig6Zmk77yf"></span>
### How do I prevent an instance from being deleted by automatic scale\-in?

You can enable instance protection or standby status for the instance. Once instance protection or standby status is enabled, health check and scale\-in operations will be bypassed. For more information, see [Configuring instance protection](https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection) and [Setting instance to standby status](https://docs.byteplus.com/en/docs/as/Setting-instance-standby).

<span id=".5a6e5L6L5YGl5bq35qOA5p-l"></span>
## Instance health check

<span id=".5by55oCn5Ly457yp55qE5YGl5bq35qOA5p-l5ZKM6LSf6L295Z2H6KGh55qE5YGl5bq35qOA5p-l5pyJ5LuA5LmI5Yy65Yir77yf"></span>
### What is the difference between the health check of Auto Scaling and the health check of Load Balancer?

For more information, see [Instance health check](https://docs.byteplus.com/en/docs/as/Health-checks).
