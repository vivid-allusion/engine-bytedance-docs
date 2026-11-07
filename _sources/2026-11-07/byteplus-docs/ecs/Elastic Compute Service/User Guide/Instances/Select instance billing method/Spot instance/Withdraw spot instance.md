---
title: "Withdraw spot instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reclaiming_spot_instance"
---

This article introduces the reclaim mechanism for spot instances and the situation after spot instances are reclaimed.

Spot instances have an interruption and reclaim mechanism. When instance inventory is insufficient or the market price exceeds your bid, the spot instance will be automatically released by the system. In addition, the following scenarios will also affect the normal operation of spot instances. Please exercise caution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Data cannot be recovered after a spot instance is released. Please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Spot_instances_overview#.5rOo5oSP5LqL6aG5">Precautions</a> to back up your data in advance.</div>


<span id=".5YGc5py65a-55oqi5Y2g5byP5a6e5L6L55qE5b2x5ZON"></span>
## The impact of shutdown on spot instances


|Stop mode |Can it be started again after stopping? |
|---|---|
|Normal Mode or Economical Mode |* If inventory resources are sufficient, the system can start normally.<br><br>* If inventory resources are insufficient, startup cannot proceed.<br><br><br>> For the enabling conditions of Economical Mode, refer to [Economical Mode Description](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances). |


<span id=".5qyg6LS55a-55oqi5Y2g5byP5a6e5L6L55qE5b2x5ZON"></span>
## Impact of overdue payments on spot instances


|arrears |Can normal use continue after an account becomes overdue |
|---|---|
|Overdue: ≤ 2 hours |* If inventory resources are sufficient and the bid is greater than or equal to the market price, they can be used.<br><br>* If inventory resources are insufficient or the bid is less than the market price, the resources will be reclaimed. |
|Overdue \> 2 hours |The instance's computing resources will be reclaimed. |


<span id=".6YeK5pS-5ZCO5oOF5Ya1"></span>
## Status after release

For information about other resources after a spot instance is released, refer to [Information about resources related to the instance after deletion](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances#.5Yig6Zmk5ZCO5a6e5L6L55u45YWz6LWE5rqQ5oOF5Ya1).
