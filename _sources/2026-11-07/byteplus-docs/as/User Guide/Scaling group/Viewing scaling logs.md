---
title: "Viewing scaling logs"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Viewing-scaling-activities"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The Auto Scaling service records the results of scaling activities for each scaling group, including the conditions that triggered scaling, adjustment type, start/stop time, and execution result. It provides a channel for event recording and traceability.

Currently, the maximum retention period for scaling logs is 30 calendar days, and the maximum number of retained logs is 10,000. Log cleanup will be triggered when either of the two thresholds is reached.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Scaling log" tab.

4. You can filter logs by time. Click the "+" icon on the left side of a log entry to expand and view the instance ID created after a successful scaling activity, or the error code and error information for a failed scaling activity.


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DescribeScalingActivities](https://docs.byteplus.com/en/docs/as/DescribeScalingActivities)
