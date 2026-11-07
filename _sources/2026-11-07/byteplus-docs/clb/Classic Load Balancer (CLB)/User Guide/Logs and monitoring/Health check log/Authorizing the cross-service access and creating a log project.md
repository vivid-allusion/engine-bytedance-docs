---
title: "Authorizing the cross-service access and creating a log project"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Implementing-cross-service-authorization-and-creating-a-log-project"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Before using the Classic Load Balancer (CLB) health check log feature, you must authorize cross\-service access for CLB. This topic introduces the steps for cross\-service authorization and other related operations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have activated the Torch Log Service (TLS) and Torch Object Storage (TOS).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click Go to authorization.

5. Click Authorization to complete cross\-service authorization.

6. After authorization is complete, click Create log project, and the system automatically creates a log project named clb\-health\-check\-log.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a log project named clb\-health\-check\-log already exists in Torch Log Service (TLS), a default log project named clb\-health\-check\-log\-XXXX will be automatically created.   </div>
   

<span id=".55u45YWz5pON5L2c"></span>
## Related actions


<Tabs>
<Tab zoneid="RP2SKNf1ZM" title="Create log project">
<TabTitle>Create log project</TabTitle>

If the log project is deleted, follow the steps below to recreate it:


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click Create log project and the system automatically completes the creation process.


</Tab>
<Tab zoneid="IWuJfgZPe1" title="Delete log project">
<TabTitle>Delete log project</TabTitle>

Before deleting a log project, ensure it does not contain any log topics. Otherwise, first delete the log topic.


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Health check log.

4. Click Delete on the right side of the log project.

5. Click **Delete** to complete the action.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/CreateHealthCheckLogProject)

* [DescribeHealthCheckLogProjectAttributes](https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckLogProjectAttributes)

* [DeleteHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/DeleteHealthCheckLogProject)
