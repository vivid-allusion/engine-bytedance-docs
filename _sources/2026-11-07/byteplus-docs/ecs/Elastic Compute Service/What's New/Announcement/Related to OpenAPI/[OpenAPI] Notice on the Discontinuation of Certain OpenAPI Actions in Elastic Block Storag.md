---
title: "[OpenAPI] Notice on the Discontinuation of Certain OpenAPI Actions in Elastic Block Storage (EBS) 2018-01-01 Version"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/2553744"
---

Dear valued customer, to provide you with more stable, secure, and feature\-complete services, BytePlus Elastic Block Storage (EBS) will officially discontinue support for certain OpenAPI actions in the **2018\-01\-01 version** on **July 20, 2026**.

<span id="bDbs9C2k"></span>
## Change time

**July 20, 2026**. Please refer to the console for the specific time.

<span id="OoreoVnA"></span>
## Involved OpenAPI actions:


* DeleteVolume

* ModifyVolume

* AttachVolume

* DeleteVolumes

* CreateVolume

* DetachVolume

* ExtendVolume

* InnerResetSystemVolume


After the discontinuation takes effect, the above actions will no longer be available. In addition, other OpenAPI actions in the 2018\-01\-01 version have also entered the maintenance phase. **We recommend that you migrate all related calls to the 2020\-04\-01 version** to ensure service stability and continued access to future capabilities.

For the corresponding actions in the 2020\-04\-01 version, see [Volume OpenAPI](https://docs.byteplus.com/en/docs/ecs/Createvolume?_vtm_=a106466.b106468.0_0.0_0.0.324_7637063494155814442&lang=en).

<span id="mfz4fM2Y"></span>
## Impact on you

If you are still calling any of the above actions in the 2018\-01\-01 version, related requests may fail after the discontinuation date, which could affect your business operations. If you have already migrated to the corresponding actions in the 2020\-04\-01 version, no action is required.
