---
title: "Scaling group FAQ"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Scaling-group-FAQs"
---

&nbsp;

<span id=".5by55oCn5Ly457yp5pyN5Yqh5pSv5oyB5ZOq5Lqb5Ly457yp6KGM5Li677yf"></span>
## What adjustments does the Auto Scaling service support?

The Auto Scaling service provides multiple adjustment types, such as manual scaling, scheduled scaling, periodic scaling, and alert\-based scaling, to meet the needs in various business scenarios. For more information, see [Adjustment types](https://docs.byteplus.com/en/docs/as/Adjustment-types).

<span id=".5Ly457yp57uE5LiA5a6a6KaB5pCt6YWN6LSf6L295Z2H6KGh44CB5YWs572RSVDkvb_nlKjlkJfvvJ8="></span>
## Is a scaling group required to be used with Load Balancer and EIP?

No, you can choose whether to use Load Balancer and EIP based on your business needs. For more information, see [Related cloud products](https://docs.byteplus.com/en/docs/as/Related-cloud-services).

<span id=".5Zyo5Ly457yp57uE5Lit6Ieq5Yqo5Yib5bu65oiW5omL5Yqo5re75Yqg55qE5a6e5L6L5Lya6Ieq5Yqo5ZCM5q2l5Yiw6LSf6L295Z2H6KGh44CBUkRT5pWw5o2u5bqT5Lit5ZCX77yf"></span>
## Are instances automatically created or manually added in a scaling group automatically synchronized to the load balancer and RDS database?

Yes. After a scaling group is associated with a load balancer and RDS database, when adjustments are performed, instances are automatically synchronized to the backend server group of the load balancer and the IP address allowlist group of the RDS database.

<span id=".5LuA5LmI5piv5Ya35Y205pe26Ze077yf"></span>
## What is cooldown time?

Cooldown time refers to the period allocated for cooling down after adjustments. The system initiates cooldown timing immediately upon the completion of each adjustment. During the cooldown time, adjustments triggered by scheduled, periodic, or alert\-based scaling rules will be rejected, but manual scaling, instance count checks, and health checks are not subject to the cooldown time restriction. For more information, see [Cooldown time](https://docs.byteplus.com/en/docs/as/Cooldown-period).

<span id=".5LuA5LmI5piv5pyf5pyb5a6e5L6L5pWw77yf"></span>
## What is the expected instance count?

You can specify an expected instance count to maintain a fixed number of instances in a scaling group. This ensures the instance count stays consistently fixed throughout the scaling group's operation. You can change the expected instance count at any time. For more information, see [Expected instance count](https://docs.byteplus.com/en/docs/as/Desire-instance-number-capacity).

<span id=".5ZCM5pe26K6-572u5LqG5omp57yp5a65562W55Wl5ZKM5a6e5L6L56e75Ye6562W55Wl77yM5Zyo56e75Ye65a6e5L6L5pe277yM5LyY5YWI5L2_55So5ZOq5Liq562W55Wl77yf"></span>
## If both the scaling policy and the instance removal policy are specified, which policy takes precedence when an instance needs to be removed from the scaling group?

Both the scaling policy and the instance removal policy are used to specify how the instances are removed when the scaling group automatically scales in.

When the two policies conflict, the scaling policy takes precedence. For more information, see [Removal policy types](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.56e75Ye6562W55Wl57G75Z6L).

<span id=".5ZCv55So5Ly457yp57uE5aSx6LSl77yM5aaC5L2V5o6S5p-l5Y6f5Zug77yf"></span>
## How do I troubleshoot the failure to enable a scaling group?

The scaling policy, subnet, and scaling configuration of a scaling group must meet the following requirements. Otherwise, the scaling group cannot be enabled as expected:


|Scaling Policy |Subnet and scaling configuration requirements |
|---|---|
|Priority policy |The instance type and image of the scaling configuration currently associated with the scaling group must be available in the availability zone corresponding to the highest\-priority subnet (that is, the first selected subnet). |
|Balanced distribution policy |The instance type and image of the scaling configuration currently associated with the scaling group must be available in the availability zones corresponding to all selected subnets. |


<span id=".5Li65LuA5LmI5Ly457yp57uE5omp5a655aSx6LSl77yf"></span>
## Why does the scale\-out of a scaling group fail?

When a scaling group scales out, it automatically creates instances and associates EIPs that match the scaling group. If the scale\-out fails, check in the Quota Center first to ensure there is sufficient quota to avoid failure due to insufficient quota.

<span id=".5YGc55So5Ly457yp57uE5ZCO5Lya5Yig6Zmk5a6e5L6L5ZCX77yf"></span>
## Will instances be deleted after a scaling group is disabled?

No. After a scaling group is disabled, the instances within the group are retained, and their status will not be modified.

<span id=".5Yig6Zmk5Ly457yp57uE5ZCO5Lya5Yig6Zmk5a6e5L6L5ZCX77yf"></span>
## Will instances be deleted after a scaling group is deleted?

Yes. After you delete a scaling group, instances that do not have instance protection enabled or whose lifecycle is managed by the scaling group will be automatically deleted, and related resources will be deleted synchronously. For instances that have instance protection enabled or whose lifecycle is not managed by the scaling group, they will only be removed when the scaling group is deleted, and the related resources and the association status will be retained.
