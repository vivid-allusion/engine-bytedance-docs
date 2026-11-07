---
title: "Viewing performance monitoring"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Viewing-performance-monitoring"
---

The Byteplus Cloud Monitor provides performance monitoring for file storage PFS. This topic introduces the monitoring item descriptions related to PFS and the operation steps to view performance monitoring.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

[CloudMonitor](https://console.byteplus.com/auth/login?redirectURI=%2Fcloud-monitor%2Foverview) has been activated.

<span id=".55uR5o6n6aG56K-05piO"></span>
## Cloud Monitor metrics

For information on monitoring items related to PFS, please refer to [PFS Monitor metrics](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric&namespace=VCM_vePFS).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">This topic only introduces the operation steps for viewing performance monitoring on the PFS console. You can also view the corresponding information on the <a href="https://console.byteplus.com/auth/login?redirectURI=%2Fcloud-monitor%2Foverview">CloudMonitor</a> console. For specific steps, please refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-operating-system-monitoring-data">Viewing operating system monitoring data</a>.</div>



1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. On the Instance List page, click on the target file system name.

4. On the instance details page, click **Monitoring alarm** and then click monitoring tab you want to query to view the corresponding information.Monitoring tab description as follows.

   
   |Monitoring tab |Monitoring items |
   |---|---|
   |Storage |* **TotalStorage**<br><br>* **UsedStorage**<br><br>* **TotalInode**<br><br>* **UsedInode**<br><br>* **StorageUtil**<br><br>* **InodeUtil** |
   |Bandwidth |* **ReadBandwidth**<br><br>* **WriteBandwidth** |
   |IOPS |* **ReadIops**<br><br>* **WriteIops** |
   |delay information |* **read delay**<br><br>* **write delay** |
   |protocol service |* **ProtocolServiceBandwidth**<br><br>* **ProtocolServiceIops**<br><br>* **ProtocolServiceLatency** |
   |Fileset |* **Fileset Used Capacity**<br><br>* **Fileset Total Capacity**<br><br>* **Fileset Capacity Used Ratio** |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select the specific time period for the query or choose a specific date for the query in the upper left corner of the tab.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click the fullscreen button in the top right corner of the chart to view the corresponding statistics in fullscreen mode.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click on <strong>View more metrics</strong> at the top right of the page, and the page will automatically redirect to the <a href="https://console.byteplus.com/auth/login?redirectURI=%2Fcloud-monitor%2Foverview">CloudMonitor</a> console to view more monitoring information for PFS.   </div>
   


<span id=".55u45YWz5pON5L2c"></span>
## Related operations

You can set up alarm strategy based on the monitoring items supported by PFS to promptly grasp any abnormal situations of instances. For detailed instructions, please refer to the [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
