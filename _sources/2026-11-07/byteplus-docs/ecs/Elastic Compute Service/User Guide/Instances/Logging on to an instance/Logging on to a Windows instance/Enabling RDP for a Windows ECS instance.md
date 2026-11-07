---
title: "Enabling RDP for a Windows ECS instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enabling-RDP-for-a-Windows-ECS-instance"
---

The first time you log on to a Windows ECS instance, we recommend that you use a virtual network computing (VNC) system, enable Remote Desktop Protocol (RDP), then log on to the Windows ECS instance by using MSTSC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, RDP is enabled for ECS instances that are created from public images.</div>



1. Log on to the Windows ECS instance in the [ECS console](https://docs.byteplus.com/en/docs/49/%5Bhttps://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance%5D(https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance)).

2. Choose **This PC** \> **Properties** and click **Advanced system settings**.

3. Click the **Remote** tab. Confirm and select **Allow remote connections to this computer**. Select **Allow connections only from computers running Remote Desktop with Network Level Authentication (recommended)**  on demand.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e2cf3fd8d7c283dbf8c6c6d368c54d09.png) </span>
