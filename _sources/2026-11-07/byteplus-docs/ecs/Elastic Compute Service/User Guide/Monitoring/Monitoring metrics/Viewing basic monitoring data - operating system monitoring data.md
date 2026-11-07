---
title: "Viewing basic monitoring data/operating system monitoring data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data"
---

To allow you to view the monitoring data of basic performance metrics and operating system metrics for the running instances, the platform provides you with the basic monitoring and operating system monitoring functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"> view the operating system monitoring. If the O11yAgent collection plugin is not installed, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console">White\-screen installation guide</a> or <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually">Manual plugin installation guide</a> to install it.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Usage note


* The following describes how to view monitoring data for a single instance. You can also click the [Monitoring Dashboard](https://docs.byteplus.com/en/docs/cloudmonitor/Monitoring-dashboard) to view operating system monitoring statistics for multiple instances. This way, you can easily view the overall change trend and exceptions of a metric in different instances.

* The collection frequency for basic monitoring metrics is 30s, which means that basic monitoring metrics are collected every 30s.

* The collection frequency for operating system monitoring is 10s or 60s, which means that metrics of operating system monitoring are collected every 10s or 60s.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Default statistics cycles vary based on metric. The actual statistics cycles displayed in the console prevail.   </div>
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top navigation bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances". The Instances page appears.

4. Find the target instance through information such as instance name, ID, or tag.

   > You can also quickly view on the Instances page. For details, please refer to [Obtain monitoring data through the ECS console](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-monitoring-data).   
   

5. Select the "Monitoring" tab to view the "Basic monitor" and "Operating system monitor" data.

   * **Basic monitoring**: Click the "Basic monitor" tab, you can view basic performance metrics of an instance, including CPU, network, disk, and max connections.

      * Currently, only for the instance types listed in the following table, you can view the "Disk read and write bandwidth (B/s)" and "Disk read and write IOPS (Count/s)" metrics.

         
         |X86 Compute |Specification/type |
         |---|---|
         |General\-purpose |* [General-purpose g3i](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNp)<br><br>* [General-purpose g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNh) |
         |Compute\-optimized |* [Compute-optimized c3i](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNp)<br><br>* [Compute-optimized c3a](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNh) |
         |Memory\-optimized |* [Memory-optimized r3i](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#uvEC2ygI)<br><br>* [Memory-optimized r3a](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#qEWtPNM0) |
         

      * Max connections: the concurrent network connections of ECS.

         * Non\-HPC\-optimized: total number of TCP and UDP socket connections.

         * HPC\-optimized: total number of TCP, UDP, and RDMA connections.

   * **Operating system monitoring**: Click the "Operating system monitor" tab. There, you can view the operating system monitoring metrics of an instance, including the CPU, memory, disk, network, and network interface card.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If a disk of your instance is mounted, the metric legend is displayed in the format of <code>"Disk name" + ":" + "Space" + "Mount point directory"</code>. Example: "vda2: /". If the disk is not mounted, only the disk name is displayed. Rules for displaying disk\-related metric data:      </div>
      

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Data for the "disk usage", "disk free space", and "total disk capacity" metrics is displayed only for mounted disks.      </div>
      

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Data for the "disk read/write bandwidth", "disk read/write IOPS", and "disk I/O latency" metrics is displayed for all disks regardless of whether the disks are mounted.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If a disk of your instance is mounted but the mount point is not displayed, we recommend that you upgrade the plugin. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console#8e12498e">Performing a white\-screen upgrade of the O11yAgent collection plugin</a>.      </div>
      


<span id=".55u45YWz5q2l6aqk"></span>
## Relevant operations


* You can also [configure monitoring metrics for alerts](https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics) or [create an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for basic monitoring and operating system monitoring. This allows you to timely detect instance exceptions and improve O&M efficiency.

* You can also export CPU, memory, and disk usage data for all instance operating systems under the current account to a local file. This file can be used for offline issue diagnosis. For details, refer to [Exporting operating system data](https://docs.byteplus.com/en/docs/cloudmonitor/Basic-monitoring).


<span id="bK0T57tn"></span>
## FAQs


* ### Why can't I see any data under all metrics on the  **"Basic monitor" and "Operating system monitor" tabs**? <span id="T9TOVMei"></span>

   It may be because the Agent is not installed, outdated, or has encountered an exception. Perform troubleshooting by referring to [Troubleshooting common plugin issues](https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_troubleshooting).

* ### **Why can't I see any data under some metrics on the "Basic monitor" and "Operating system monitor" tabs?**  <span id="u4oXxrxM"></span>

   It may be because the Agent version is outdated. We recommend that you upgrade the O11yAgent plugin. For details, refer to [White-screen installation of O11yAgent collection plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console) or [Manual installation of O11yAgent collection plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually).
