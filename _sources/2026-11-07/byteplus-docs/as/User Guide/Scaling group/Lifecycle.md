---
title: "Lifecycle"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Lifecycle"
---

The lifecycle of a scaling group refers to all the states it undergoes from creation to deletion.

Appropriate planning and management of the lifecycle ensure that instances running in the scaling group can provide external services conveniently and efficiently.

<span id=".5Ly457yp57uE54q25oCB"></span>
## Scaling group status

During the lifecycle of a scaling group, it goes through several fixed states. The following table shows how each state is triggered.


|Status |Description |
|---|---|
|Creating |The state of the scaling group after you create it and before it enters the **Running** state. |
|Active |The state when the scaling group is running as expected. In this state, the scaling group can scale in or out as expected. |
|Disabled |After the scaling group completes the stop operation, it will enter the **Disabled** state. |
|Locked |After a manual or automatic scaling operation is performed on the scaling group, the scaling group enters the **Locked** state, indicating that new instances are being added or removed in the scaling group. |
|Cooling |After the scaling group performs scaling operations based on scaling rules, it enters the **Cooling** state. During the cooldown time, scaling operations triggered by scaling rules will not be accepted, but manual scaling, instance count check, and health check are not limited by the cooldown time. |
|Deleting |The scaling group is being deleted. Once this state ends, the scaling group will automatically disappear from the console page. |
