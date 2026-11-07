---
title: "Setting instance to standby status"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Setting-instance-standby"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If you want the instances in a scaling group to temporarily stop receiving business traffic for adjustments such as instance upgrades or plugin installations, you can temporarily set the instances to standby status. Instances in standby status:


* Standby instances will not be deleted or removed when the scaling group scales in.

* Auto Scaling health check does not check the status of standby instances.

* If the scaling group where the standby instances reside is configured with a load balancer, the load balancing weight of the instances will be set to zero and the instances will not receive business traffic.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you set an instance to the standby status, confirm the items described in the following table.


|Project |Prerequisites |
|---|---|
|Instance |The instance must be in the **In service** status. |
|Scaling group |The scaling group must be in the **Enabled** status. |


<span id=".5a6e5L6L6L2s5Li65aSH55So54q25oCB"></span>
## Switch an instance to standby status


1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select the target instance and click the "Switch to Standby" button at the bottom of the list.

5. Click the "Confirm" button to complete the operation.


<span id=".5a6e5L6L56e75Ye65aSH55So54q25oCB"></span>
## Remove an instance from standby status


1. Log in to the[ Auto Scaling console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select the target instance and click the "Remove from Standby" button at the bottom of the list.

5. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [EnterStandby - Sets an instance to standby status](https://docs.byteplus.com/en/docs/as/EnterStandby)

* [ExitStandby - Removes an instance from standby status](https://docs.byteplus.com/en/docs/as/ExitStandby)
