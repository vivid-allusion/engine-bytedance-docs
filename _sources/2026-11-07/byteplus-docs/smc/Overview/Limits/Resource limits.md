---
title: "Resource limits"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Limits"
---

This topic describes the limits to note when you use Server Migration Center (SMC), including platform account requirements, cloud product quotas, and configurations of source servers and target instances.

<span id=".6LSm5Y-36ZmQ5Yi2"></span>
## Account limits

SMC is a free service, but the migration process involves a small amount of ECS resource charges. For more information, see [Billing](https://docs.byteplus.com/en/docs/smc/Billing).

<span id=".6aKd5bqm6ZmQ5Yi2"></span>
## Quota limits


* The limits on Migration Source, Migration Job, and migration template quantities are shown in the table below.

   
   |Limit item |Upper limit |Changeable |
   |---|---|---|
   |Number of migration sources that can be registered |500 |Yes, if you need to increase the quota, contact your account manager to apply. |
   |Number of migration tasks that can be created |500 |Yes, if you need to increase the quota, contact your account manager to apply. |
   |Number of migration tasks that can be executed concurrently |30 |Yes, if you need to increase the quota, contact your account manager to apply. |
   |Number of migration templates that can be created |50 |No |
   

* The following table describes the resource quantity limits.

   
   |Limit item |Upper limit |Changeable |
   |---|---|---|
   |Volume capacity |* ESSD PL0: Maximum usage of 64TiB for each main account in a region.<br><br>* ESSD FlexPL: Maximum usage of 10TiB for each main account in a region. |Yes |
   |Number of VPCs (including the default VPC) that can be created per account per region<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For each task migrated to an Elastic Compute Service (ECS) image, a dedicated VPC is created by default.</div><br> |10 |Yes |
   |Maximum number of manual Snapshots that can be created per volume |10 |No |
   |Max. EIPs that can be applied for an account in a region |20 |Yes |
   |Number of security groups (including the default security group) that can be created per account per region |300 |Yes |
   |Max. key pairs for an account in a region |500 |No |
   


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can evaluate whether the resource quantity meets migration requirements before migration. For details, see <a href="https://docs.byteplus.com/en/docs/smc/Evaluate-the-number-of-cloud-resources-used-by-Migration-Jobs">Estimating the quantity of cloud resources used by migration tasks</a>.</div>


<span id=".6L-B56e76IyD5Zu0"></span>
## Migration scope

SMC only supports migrating data stored on the source server. Certain resource configurations (such as security groups and VPCs) will not be migrated.
