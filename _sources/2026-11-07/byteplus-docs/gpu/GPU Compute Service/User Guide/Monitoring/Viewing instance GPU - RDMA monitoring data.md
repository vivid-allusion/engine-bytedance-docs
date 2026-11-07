---
title: "Viewing instance GPU/RDMA monitoring data"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Viewing-instance-GPU_RDMA-monitoring-data"
---

For GPU instances, BytePlus provides you with its unique GPU monitoring and RDMA monitoring, which can help you quickly understand the instance graphics card and RDMA network information.

<span id="instructions-for-use"></span>
## Instructions for use


* Only GPU instance is supported. For details, please refer to [Instance Types](https://docs.byteplus.com/en/docs/gpu/Instances).

* You can also configure GPU card and RDMA card indicator data exception alarms according to the [Create Alert Policy](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Resource type</strong> Please select <strong>Elastic Computing Service (ECS)</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Dimension</strong> Please select <strong>GPU</strong> or <strong>RDMA</strong>.   </div>
   


<span id="operation-steps"></span>
## Operation steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. Go to the instance list page, use one of the following methods to go to the monitor page.

   * Find the target instance and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_72648193f0b4d6e9b7adc0e3d02409e0.png) </span>in the **Monitor** column.

   * Click the name of the target instance to go to its details page, and click the **Monitor** tab.

3. View the instance data on the two tabs "GPU Monitoring" and "RDMA Monitoring".

   * GPU monitoring

      You can view indicator information such as video memory usage, GPU usage, and GPU temperature on this page.

   * RDMA monitoring

      On this page, you can view metrics such as "RDMA network inflow/outflow rate", "number of RDMA data packets received/sent", "number of suspended packets in/out of RDMA network".
