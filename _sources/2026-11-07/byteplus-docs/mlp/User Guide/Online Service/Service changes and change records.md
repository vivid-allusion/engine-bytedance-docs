---
title: "Service changes and change records"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Service_changes_and_change_records"
---

Machine Learning Platform supports dynamic capacity expansion and reduction, upgrade, transfer and rollback of services, and also saves the corresponding operation history for users to trace the update iteration process of services.

<span id="使用前提"></span>
# premise of use


1. There are \> = 1 services in [inference services].

2. The service status pending capacity expansion and reduction must be `in operation`.

3. The status of the service to be upgraded or transferred cannot be `stopped`.

4. The state of the service to be rolled back cannot be `stopped`, and the service has \> = 2 change records.

* Services that have private networks and subnets configured do not support rolling back to the unconfigured version.


<span id="操作步骤"></span>
# Procedure


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page.

2. On the service list page or enter the details page, click [capacity expansion and reduction] in the operation area and modify the number of instances according to the current business volume, and then the instances of the service will increase or decrease accordingly. At this time, the [change record] list of the details page will generate a change record of type `capacity expansion and reduction`.

3. In the service list or enter the details page, click 【···】\-【 Upgrade] in the operation area and modify the mirror/model/entry command/environment variables/listening port/health check/calculation specification/access configuration/queue as needed. The instance of the service will be updated on a rolling basis without affecting the online business. At this time, a record of type `upgrade service`will be generated in the [Change Record] list.

4. In the service list or enter the details page, click [transfer] in the operation area to re\-trigger the reallocation of the underlying resources, that is, redeployment, under the condition that the deployment configuration information remains unchanged. This feature is typically used for resource fragmentation cleanup and exception instance handling. If a single instance is abnormal, you can also [transfer] a single instance through the inference services details page \- the instance list page to achieve the effect of restarting an instance.

5. On the details page of the service, click [Change Record] to view all the change history so far. The key information is shown in the table below. Select a target version by comparing the change record and click [rollback to this version]. After the second confirmation, the instance of the service will be updated on a rolling basis without affecting the online business. The configuration of the new service is the same as that of the target version.



|**Parameter** |**Note** |
|---|---|
|Value Type |The type of change to the service. Including `creation service`, `capacity expansion and reduction`, `upgrade service`, `rollback service`, `transfer service`five types. |
|Description |Description information when the service is changed, used to explain the reason for the current change, its effect, etc. |
|Change of Person |The name of the user who initiated the change. |
|change details |* Shows the current configuration of the service.<br><br>* Shows the differences in the configuration between this record and the previous record. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64eca8b1a25349b58de68e26fc330e93~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02e212d60ad64e2f957a2ef1a5d15d84~tplv-goo7wpa0wc-image.image) </span>
