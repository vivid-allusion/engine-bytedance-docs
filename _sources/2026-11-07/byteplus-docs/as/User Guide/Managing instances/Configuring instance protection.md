---
title: "Configuring instance protection"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Setting-instance-scale-in-protection"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

You can enable protection for instances in a scaling group that you do not want to be automatically deleted or removed.


* When the scaling group scales in, instances with instance protection enabled will not be deleted or removed.

* The Auto Scaling health check feature does not check the status of instances with instance protection enabled.

* If the scaling group of an instance with instance protection enabled is configured with a load balancer, disabling protection for the instance will not affect its weight in the load balancer.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">By default, instance protection is disabled for instances automatically created by a scaling group and Pay\-as\-you\-go instances you manually added to the scaling group.</div>


* <div data-tips="true" data-tips-type="tip">After you manually remove an instance with instance protection enabled from a scaling group, instance protection becomes invalid.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you configure instance protection, confirm the items described in the following table.


|Project |Prerequisites |
|---|---|
|Instance |The instance must be in the **In service** status. |
|Scaling group |The scaling group must be in the **Enabled**, **Cooling** or **Stopped** status. |


<span id=".5byA5ZCv5a6e5L6L5L-d5oqk"></span>
## Enable instance protection


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select the "Switch to Protected" button on the right side of the instance for which you want to enable instance protection.

5. Click the "Confirm" button to complete the operation.


<span id=".5YWz6Zet5a6e5L6L5L-d5oqk"></span>
## Disable instance protection


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select the "Remove from Protected" button on the right side of the instance for which you want to disable instance protection.

5. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[SetInstancesProtection](https://docs.byteplus.com/en/docs/as/SetInstancesProtection)
