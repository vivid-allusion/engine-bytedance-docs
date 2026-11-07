---
title: "Viewing instances associated with key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-key-pairs-bound-to-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

Before you delete a key pair, you can view the instances that are associated with the key pair. This topic describes how to view the instances associated with a key pair.

Currently, you can only view instances that are in the same region as the key pair and whose status is **Running** or **Stopped**.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="ynm5v6O29H" title="On the key pair list page">
<TabTitle>On the key pair list page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the key pair is located. 

3. On the key pair list page, click the target key pair name to go to the details page, and then select the "Bound Instances" tab.

4. View the list of associated instances. You can filter instances by criteria, such as instance name, ID, and status. Click an instance name to view the instance details.


</Tab>
<Tab zoneid="k6IQmOEYTQ" title="On the instance details page">
<TabTitle>On the instance details page</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the target instance resides.

3. In the instance list, click the name of the target instance to go to the Overview tab.

4. View the key pair associated with the instance in the **Basic information** section.


</Tab>
</Tabs>
