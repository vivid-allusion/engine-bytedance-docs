---
title: "Viewing GPU/RDMA monitor​ing data of instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data"
---

For GPU Compute Service (GPU), the BytePlus provides unique GPU monitoring and RDMA monitoring features to help you quickly view the graphics card and RDMA network information of your instances.

<span id="WdOxTThx"></span>
### Prerequisites

Check whether the instance has been installed with the O11yAgent collection plugin based on the ECS monitoring guide. If not, refer to [White-screen installation guide](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console) or [Manual plugin installation guide](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually) to complete the installation.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* Currently, only GPU supports this feature. For specification details, refer to [Heterogeneous Computing](https://docs.byteplus.com/en/docs/ecs/Heterogeneous-computing).

* You can also configure data exception alerts of the metric for GPU and RDMA by following the guidance of [Creating alarm policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For "Alarm object", select "Elastic Compute \> ECS".   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For "Subnamespace", select "GPU" or "RDMA".   </div>
   

* The frequency for collecting instance GPU/RDMA monitoring metrics is 60s, which means that GPU/RDMA monitoring metrics in an instance are collected every 60s.  


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top navigation bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Click the name of the target instance to go to the instance details page.

5. Select the "Monitoring" tab to view the instance data in the "GPU monitor" and "RDMA monitor" tabs.

   * GPU monitor

      On this page, you can view memory usage, GPU usage, GPU temperature, GPU Encoder Usage, GPU decoder usage, GPU memory usage, and other metrics.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only for instances with A100/A800 graphics cards and the number of graphics cards ≥ 2, you can view the metrics of "NVLink Inbound Total Bandwidth" and "Total bandwidth of NVLink outgoing direction".      </div>
      

   * RDMA monitor

      You can view "RDMA network inflow/outflow rate", "Number of packets sent/received by RDMA network", "RDMA network outgoing direction pause packet number", "Number of RDMA network incoming pause packets", and other metrics on this page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only for HPC\-optimized instances with the A100/A800 GPU graphics cards, you can view metrics of "Number of packets sent/received by RDMA network", "RDMA network outgoing direction pause packet number", "Number of RDMA network incoming pause packets", and "RDMA network outbound/incoming traffic pause time".      </div>
      

<span id=".55u45YWz5q2l6aqk"></span>
## Related operation

You can perform as follows:


* You can also [create alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for GPU and RDMA monitoring to quickly detect instances with exceptions and ensure their normal operations.

* Connect HPC\-optimized instances to VMP to achieve millisecond\-level monitoring of GPU/RDMA metrics. This provides technical assurance for stable operation and performance improvement of HPC workloads across multiple dimensions, including troubleshooting, resource optimization, and cost management. [Learn more](https://docs.byteplus.com/en/docs/vmp/GPU_RDMA-millisecond-level-monitoring-integration?lang=zh).


<span id="qFwVkeds"></span>
## FAQ

[How to resolve the issue of RDMA monitoring data being empty when I run container training tasks using the dedicated mode of the RDMA network interface?](https://docs.byteplus.com/en/docs/ecs/Monitoring-FAQs#9DtWp9nH)
