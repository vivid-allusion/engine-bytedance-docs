---
title: "Performance profiling"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Performance_profiling"
---

Performance profiling is an in\-depth performance analysis capability of infrastructure monitoring. It allows you to create profiling tasks for specified services and pods, analyzing CPU performance data collected from pods during a defined time window. Results are visualized via bar charts, flame graphs, and other formats to help rapidly pinpoint service performance bottlenecks.

<span id="LJZTcWtV"></span>
## Limits

Ensure that the "Continuous CPU Profiling" switch is enabled for the current workspace. For detailed instructions, see [Parameter management](https://docs.byteplus.com/en/docs/apmplus/parameter_management?lang=en).

<span id="3i2ZxIfu"></span>
## Create tasks

On the performance profiling page, you can create profiling tasks to collect and analyze CPU performance data for specified services and pods.


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **APM** \> **Infrastructure Monitoring** \> **Performance Profiling**.

3. On the **Performance Profiling** page, click **Create task**.

4. Refer to the table below to configure task parameters.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_70076c0bd78851ddb0505fea3cee2afa.png) </span>

   
   |**Parameters** |**Description** |
   |---|---|
   |Current workspace |The current workspace (the owning workspace of the performance profiling task). ‌This parameter is system\-populated and cannot be modified. |
   |Service |Select the target service for performance profiling. Only one service can be selected for each task. |
   |Pod |Select the pod instance whose performance data needs to be collected. The task will collect runtime CPU data for this pod. |
   |Start time |Set the task start time. By default, the task runs immediately. You can schedule the task to run at a specific future point in time. |
   |Collection Duration |Set the collection duration for performance data collection. The value range is 60 to 3600 seconds. |
   

5. Click **Confirm** to complete creation. The task is displayed in the task list and will perform collection and analysis based on the configured time period.


<span id="d4cGSjLU"></span>
## View analysis results

Find the task in the task list and click **View** in the Actions column to view task information, such as the task ID, workspace, service, pod, and status. After the task runs successfully, its details page displays the following analysis views to help you diagnose performance issues from different perspectives: **Time Series Analysis**, **Statistical Analysis**, and **Stack Analysis**.

<span id="Asgmc2AM"></span>
### Time series analysis

Time series analysis displays trend data for Pod CPU metrics during the collection period using chronological visualization. The following metrics are supported:


|**Metric** |**Description** |
|---|---|
|CPU utilization |The ratio of used CPU cores to total CPU cores. |
|CPU\-kernel state ratio |The ratio of CPU cores used by kernel\-mode functions to total used CPU cores. |
|CPU\-irqoff ratio |The ratio of CPU cores used in IRQOFF to the total number of used CPU cores. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8bad3e021358bdb76f61ce421807999c.png) </span>

On the **Time Series Analysis** page, you can perform the following operations:


   * Adjust the interactive time interval by setting the **time window size** in the upper\-right corner. If you select 1s, the granularity is a single time point.

   * Navigate adjacent time points or intervals of identical duration using the ⬅️ or ➡️ arrows on your keyboard.

   * Click a point on the ‌line chart timeline to select the corresponding time point or interval.

   * Click **Modify filter** to filter data by CPU\-related criteria, including stack trace keyword, podname, binary comm, pid, thread commm, cpuid, and cgroup.


<span id="CFBLmspU"></span>
### Statistical analysis

Statistical analysis summarizes CPU usage within the collection period from statistical dimensions, including **binary comm statistics**, **CPU core statistics**, and **Pod first pull up statistics**. The metrics are described as follows:


|**Metric** |**Description** |
|---|---|
|binary comm statistics |Includes CPU core statistics and PID quantity statistics and provides both bar charts and tables for comparison across different binary comms, facilitating quick identification of binaries with high CPU core usage or abnormal PID counts. |
|CPU core statistics |Displays the load status and kernel\-state ratio of different CPU cores. It supports selecting color\-mapped indicators, where darker colors indicate higher metric ratios. This information can be used to identify issues of excessive single\-core load. |
|POD first pull up statistics |Lists pod names that first appeared within the selected collection period. This information helps troubleshoot issues related to pod startup. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c6cbd6972eed8141550da05eef46d95.png) </span>

On the **Statistical Analysis** page, you can perform the following actions:


   * Click a graphical element with a mouse or touchpad to apply filters.

   * Click **Modify filter ** to filter data by CPU\-related criteria, including stack trace keyword, podname, binary comm, pid, thread commm, cpuid, and cgroup.

   * Click the **Apply to** button to apply the current filter to **time series analysis** or **stack analysis**.

   * Click **Modify** **to** adjust the filter criteria for CPU\-related targets.


<span id="MWsECg9y"></span>
### Stack analysis

Stack trace details analysis displays the function\-level CPU time distribution via a flame graph. Each layer of the flame graph represents a call stack level, where horizontal width indicates the relative CPU time consumed by the function. This helps identify high\-cost hotspot functions and their call paths. The available filters and display options are as follows:


|Serial number |Filter item |Description |
|---|---|---|
|1 |Search |Supports multi\-pattern function search. Enter keywords to highlight matching stack frames in green within the flame graph. |
|2 |Label Show |Metadata displayed for the bottom stack frame within the flame graph. By default, binary comm is shown. You can select items as needed, including podname, binary comm, pid, thread comm, cpuid, and cgroup. |
|3 |Filter |Click **Add filter to** filter data by CPU\-related conditions. |
|4 |View / Render / Direction<br><br> |Control the display format of top functions tables, flame graph direction, and toggle between flame graphs and function relationship diagrams. |
|5 |Config |Control the displayed information using options **only show kernel**, **ignore CPU information**, and **ignore address**. |
|6 |Download |Download collection results for offline analysis. You can download the top stack function data and the HTML file of the current flame graph. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_247b494706b09aebae702b592d9a4ba0.png) </span>

<span id="biirnpCC"></span>
## Retry tasks

When a task fails or collection results are unexpected, click ‌**Retry‌**  on the task details page. The system will ‌re\-run the task using the original configuration parameters‌, and the page will automatically refresh after completion.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aad4a17a3248977d3dd67b874f416b03.png) </span>

&nbsp;
