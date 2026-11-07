---
title: "Manual scaling"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manual_scaling"
---

Supports manually increasing or decreasing the number of application instances based on business needs to address periods of high and low demand.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you configure both an automatic scaling policy and manual scaling, the manual scaling configuration may be overridden by the automatic scaling policy and therefore may not take effect.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

Scaling policy configuration can be performed in two ways: manual scaling and automatic scaling.


* If scaling the application becomes urgent, for example, due to a sudden surge in traffic, you can choose to scale manually.

* When scaling the application is a non\-urgent requirement, for example, during periodic traffic peaks, you can select the automatic scaling method. For specific actions, see [automatic scaling](https://docs.byteplus.com/en/docs/cp/Auto_scaling).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Managed application created. For detailed instructions, see [Create a managed application](https://docs.byteplus.com/en/docs/cp/Managed_applications_K8s).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. On the application management page, select the target hosted application, click the application card, and go to the Basic Information tab.

2. Switch to the environment tab, and click **Manual Scaling**.

3. Set the target instance count in the pop\-up dialog box.

4. Click **OK** to start scaling the application.
