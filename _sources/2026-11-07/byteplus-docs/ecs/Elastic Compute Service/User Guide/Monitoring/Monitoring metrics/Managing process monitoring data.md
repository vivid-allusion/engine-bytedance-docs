---
title: "Managing process monitoring data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics"
---

To help you understand process\-level information inside the instance operating system, BytePlus offers you the process monitoring feature. You can view the total number of active processes inside the instance and the TOP 5 processes by CPU consumption.

<span id=".5p-l55yL6L-b56iL55uR5o6n5pWw5o2u"></span>
## View process monitoring data

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Check whether the instance has been installed with the O11yAgent collection plugin based on the ECS monitoring guide. If not, refer to [White-screen installation guide](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console) or [Manual plugin installation guide](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually) to complete the installation.

<span id="FjnbGnmR"></span>
### Usage notes


* The collection frequency for process monitoring is 1 minute, which means that the relevant monitoring data of processes is collected every minute.

* After the instance starts, wait approximately 10 minutes and then view the relevant metric data within the instance.

* The CPU utilization result reflects the total utilization of multi\-core CPUs. If a process uses multiple CPUs, the CPU utilization may exceed 100%.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top navigation bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Click the name of the target instance,  Select the "Monitoring \> Process monitor" tab to view:

   * **Top process data**

      * Based on CPU consumption, the system shows monitoring data for the TOP 5 processes by default, such as "CPU utilization" and "memory consumption (%)".

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If the TOP 5 processes based on CPU consumption are not fixed, all processes that entered the TOP 5 list during the query time will be displayed. For example, if a process stayed in the TOP 5 for only one minute, it will still be displayed in the TOP list. A maximum of 20 entries are displayed.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If a process does not continuously appear in the TOP 5 during the query time range, the data points will be sparse and discontinuous. At a time with data points displayed, the process was among the TOP 5 processes with the highest CPU consumption. The density of the data points reflects the activity level of the process on the server.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If you need to view the "username" of a process, we recommend that you refer to the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console">White\-screen installation guide</a> or the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually">Manual plugin installation guide</a> to upgrade the plugin.         </div>
         

      * Click the name of the target process to view information of this process, such as CPU utilization and disk read/write count. For metric details, see the [process monitoring metrics](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics#.5p-l55yL6L-b56iL55uR5o6n5oyH5qCH).

   * **Process Count Monitoring:**  Displays the total number of processes running in the instance.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">After you install or upgrade the O11yAgent collection plugin, the instance will display the total number of all running system processes by default. Refer to the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console">White\-screen installation of O11yAgent collection plugin</a> or the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually">Manual installation of O11yAgent collection plugin</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The O11yAgent white\-screen installation and upgraded features are currently in Beta. If you need a trial, please contact your account manager to apply.      </div>
      


<span id=".55u45YWz5q2l6aqk"></span>
### Related operation

You can also [create an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for process monitoring in order to obtain whether the relevant processes of the Elastic Compute Service (ECS) are alive.

<span id=".5p-l55yL6L-b56iL55uR5o6n5oyH5qCH"></span>
## Process monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The monitoring frequency for process statistics is 1 minute, which means that the relevant monitoring data of processes is collected every minute.</div>



|Metric |Operating systems supported |Explanation |Unit |Description |
|---|---|---|---|---|
|ProcessCPUPct |Windows, Linux |CPU utilization of the process |% |When the process lifetime is not less than 30 seconds, it will generate a relatively accurate result. Otherwise, there might be a certain margin of error.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The CPU utilization result reflects the total utilization of multi\-core CPUs. If a process uses multiple CPUs, the CPU utilization may exceed 100%.</div><br> |
|ProcessMemPct |Windows, Linux |Memory usage percentage of the process |% |\- |
|ProcessIOWriteCount |Windows, Linux |The number of writes to the disk by the process |Count |\- |
|ProcessIOReadCount |Windows, Linux |The number of reads from the disk by the process |Count |\- |
|ProcessIOWriteBytes |Windows, Linux |The number of bytes written to the disk by the process |Bytes |\- |
|ProcessIOReadBytes |Windows, Linux |The number of bytes the process reads from the disk |Bytes |\- |
|ProcessVoluntaryCtxSwitches |Linux |The number of context switches voluntarily executed by the process |Count |\- |
|ProcessInvoluntaryCtxSwitches |Linux |Number of context switches involuntarily executed by the process |Count |\- |
|ProcessOpenFds |Windows, Linux |The number of file descriptors opened by the process |Count |\- |
|ProcessThreads |Windows, Linux |Number of threads used by the process |Count |\- |
