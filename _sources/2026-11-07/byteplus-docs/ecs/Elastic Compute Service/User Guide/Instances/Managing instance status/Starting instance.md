---
title: "Starting instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Starting-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic introduces how to start one or more ECS instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Only ECS instances in the **Stopped** state can be started.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When an instance in the <strong>Running</strong> state is suspended due to overdue bills or expiration, its state changes to <strong>Stopped</strong>. After you settle the bill or renew the subscription, the instance automatically starts. However, the instance may fail to start. For example, due to insufficient inventory of <a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances#.6IqC55yB5YGc5py65ZCO6LWE5rqQ5oOF5Ya1">Economical Mode instances</a>, the instances that failed to start will still be released.</div>


<div data-tips="true" data-tips-type="warning">Therefore, verify whether the instance has started successfully. If it fails to start, manually start the instance by following the procedure in this topic.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, choose "Instances & Images \> Instances".

3. In the top menu bar, select the project and region to which the target instance belongs.

4. On the Instances page, click "Start" in the "Actions" column on the right side of the target instance.

5. In the pop\-up dialog box, confirm the instance name.

6. After confirming the information, click "Start" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Result

After you start an ECS instance, its state changes to **Starting**. After a short period of time, the state changes to **Running**.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [StartInstance - Starts an instance](https://docs.byteplus.com/en/docs/ecs/StartInstance)

* [StartInstances - Starts one or more instances](https://docs.byteplus.com/en/docs/ecs/StartInstances)
