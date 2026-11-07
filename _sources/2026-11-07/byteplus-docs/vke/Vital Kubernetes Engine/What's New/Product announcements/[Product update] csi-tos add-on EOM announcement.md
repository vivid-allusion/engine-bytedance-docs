---
title: "[Product update] csi-tos add-on EOM announcement"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product_changes_csi-tos_add-on_EOM"
---

<span id="kYMNeqoL"></span>
## Change details

To stay focused on core service capabilities, improve overall service stability, security, and O&M efficiency, and align with architecture upgrade plans, VKE will stop allowing the csi\-tos add\-on to be enabled in clusters starting June 1, 2026 (UTC+8). The csi\-tos add\-on in existing clusters will continue to run normally. To prevent your business operations from being affected, we recommend that you adjust your business and migrate the add\-on in advance.

<span id="VvPpcZXf"></span>
## Impact

After the csi\-tos add\-on is officially taken offline, it cannot be installed in clusters.  


* Impact on the console: On the **Create PersistentVolume** and **Create PersistentVolumeClaim** pages, you can no longer select the S3FS access type.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f430a5c208940cd0711eec649603364.png) </span>

* Impact on the add\-on: On the **Addons** page of the VKE console, you will no longer be able to install or use the csi\-tos add\-on.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ec6971ac29d563901726c7026e4b91e.png) </span>


<span id="RRyLccCz"></span>
## Solution

To continue using TOS normally in your clusters, switch to the csi\-fsx add\-on as soon as possible. This add\-on provides the same features as the csi\-tos add\-on, delivering higher performance and availability. For the configuration method, see [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The csi\-fsx add\-on cannot be used on VCI. If you need to use TOS PVs on VCI, you can temporarily use the csi\-tos add\-on. The adaptation work is in progress. For details, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-Release-notes">VCI release notes</a>.</div>


We recommend that you plan the migration process based on your business scenario. If you encounter any issues during migration or need more technical support, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=1) at any time.
