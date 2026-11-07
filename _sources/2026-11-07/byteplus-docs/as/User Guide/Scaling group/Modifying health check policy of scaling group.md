---
title: "Modifying health check policy of scaling group"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Modifying-the-health-check-policy-of-a-scaling-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

After you create a scaling group, you can modify the instance health check policy of the scaling group.

<span id=".5pON5L2c6K-05piO"></span>
## Usage notes


* When instance health check is enabled for a scaling group, each instance that joins the scaling group immediately has instance health check enabled. Instance health check monitors the running status of instances every 5 minutes. If an instance is in **Error** status, it is considered abnormal. The scaling group will automatically remove or delete abnormal instances. This effectively prevents business disruptions caused by failing to detect abnormal instances in a timely manner.

* When instance health check is disabled, the scaling group will not process abnormal instances.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Overview" tab.

4. Click the "Instance Health Check" button in the "Basic information" section and specify whether to enable instance health check.

5. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[ModifyScalingGroup](https://docs.byteplus.com/en/docs/as/ModifyScalingGroup)
