---
title: "Optimizing GPU clock configurations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Optimizing-the-GPU-clock-rate-configuration"
---

This topic primarily describes how to configure the clock of GPU resources in clusters in Vital Kubernetes Engine (VKE).

<span id=".6YCC55So5Zy65pmv"></span>
## Application scenarios

To achieve the highest performance of GPU resources, you can set the GPU clock based on your business requirements, control GPU power consumption and heat generation, and improve GPU stability.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

**GPU\-type** nodes exist in clusters, such as GPU Accelerated nodes and High Performance Computing Optimized nodes. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

<span id=".6YWN572u5ZG95Luk"></span>
## Procedure


1. Log in to the GPU node. For detailed operations, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. (Optional) View information about the GPU clock.

   ```Bash
   nvidia-smi -q -d CLOCK
   ```
   

3. Set the GPU to the maximum clock frequency, that is, lock the clock frequency, to achieve the highest performance of the GPU.

   ```Bash
   nvidia-smi -pm 1
   MCLOCKS=`nvidia-smi -i 0 --query-gpu=clocks.max.mem --format=csv,noheader,nounits`
   GCLOCKS=`nvidia-smi -i 0 --query-gpu=clocks.max.gr --format=csv,noheader,nounits`
   nvidia-smi -ac $MCLOCKS,$GCLOCKS
   nvidia-smi -lgc $GCLOCKS
   ```
   


<span id="MYgxUWUe"></span>
## Validating results

Run the following command to view the GPU clock frequency.

```Bash
nvidia-smi -q -d CLOCK
```


If the returned information shows that the clock frequency is set to the maximum value, GPU clock locking is configured.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84c54fd76972adcdc098481a1c8c25cf.png) </span>

You can also view the GPU clock rate on the cluster Prometheus monitoring dashboard. For detailed instructions, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f4469b79e6cec04f5bc05f6bd3f2cc5.png) </span>
