---
title: "Manually installing the O11yAgent collection add-on"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually"
---

This topic describes how to use an installation script or a batch job to install the O11yAgent collection add\-on for one or more Elastic Compute Service (ECS) instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The O11yAgent collection add\-on is a new\-generation pipeline used to collect and process observability data, which reduces the complexity of accessing observability systems in cloud environments and allows you to easily benefit more from observability data.

Compared with the cloud\-monitor\-agent add\-on, the O11yAgent collection add\-on provides the following benefits:


* Provides the graphical user interface (GUI) for add\-on installation and upgrade.

* Metrics will be added only based on the O11yAgent collection add\-on.


<span id=".6buR5bGP5a6J6KOF5o-S5Lu2"></span>
## Method 1: Install the add\-on by using the CLI

You can log in to the terminal interface of an ECS instance, download the add\-on installation script on the instance, and then install the O11yAgent add\-on.


<Tabs>
<Tab zoneid="XGVcj3bvEp" title="Installing the add-on on Linux ECS instances">
<TabTitle>Installing the add-on on Linux ECS instances</TabTitle>

<span id="xkfpd4W6"></span>
### Step 1: Obtain the add\-on installation script


1. Log in to the ECS instance by using ECS Terminal. For more details, refer to [Login method overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following commands to obtain region information and the installation script.


```Bash
region=$(wget -q -O - http://100.96.0.96/volcstack/latest/region_id);wget https://o11yagent-registry-${region}.tos-${region}.ivolces.com/scripts/o11yagentd/latest/o11yagentd_ecs.sh && chmod +x o11yagentd_ecs.sh
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">By default, the preceding commands are used to obtain and install the latest version of the collection add\-on. You can also set the <code>latest</code> parameter to a version number to install a specific version of the add\-on. For more details, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_Release_Notes">Add\-on release notes</a>.</div>


<span id="1hYRonV4"></span>
### Step 2: Install the add\-on


* The command for installing the add\-on on an ECS instance is as follows:


```Bash
./o11yagentd_ecs.sh --region ${region} --o11yagent.service_id o11yagent_ecs
```



* The command for installing the add\-on on a GPU ECS instance is as follows:


```Bash
./o11yagentd_ecs.sh --region ${region} --o11yagent.service_id o11yagent_hpc
```


<span id="isABkU2M"></span>
### Step 3: Check the result


1. Run the following command to check whether the add\-on is installed.

   ```bash
   o11yagentctl ps
   ```
   

   The following sample shows the expected result. You can view the process of the installed add\-on, and the `STATUS` of the add\-on is `online`, which indicates that the add\-on is installed and is working as expected.

   ```bash
   AGENT_ID                 NAME     PKG              STATUS      START_TIME
   ecs_i-ydmrej19***        o11yagent_ecs:3.23.0      online      2025-01-09 06:13:53.266884841 +0000 UTC
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to a delay in the update of <code>STATUS</code> for the add\-on, it is recommended to check the status of the add\-on multiple times.   </div>
   

1. Log in to the [Cloud Monitor console](https://console.byteplus.com//cloud-monitor). In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**. Click the name of the target ECS instance to go to the monitoring details page, where you can view the monitoring information of the ECS instance.





</Tab>
<Tab zoneid="vwaWCYghWA" title="Installing the add-on on Windows ECS instances">
<TabTitle>Installing the add-on on Windows ECS instances</TabTitle>

<span id="Ztnond36"></span>
### Step 1: Obtain the add\-on installation script


1. Log in to the ECS instance by using ECS Terminal. For more details, refer to [Login method overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Use the PowerShell CLI tool to run the following commands to obtain region information and the installation script.


```PowerShell
$region = Invoke-WebRequest -Uri "http://100.96.0.96/volcstack/latest/region_id" -UseBasicParsing -ErrorAction Stop | Select-Object -ExpandProperty Content

$downloadUrl = "https://o11yagent-registry-${region}.tos-${region}.ivolces.com/scripts/o11yagentd/latest/o11yagentd_ecs.ps1"

Invoke-WebRequest -Uri $downloadUrl -OutFile "o11yagentd_ecs.ps1" -UseBasicParsing -ErrorAction Stop -Verbose:$false
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">By default, the preceding commands are used to obtain and install the latest version of the collection add\-on. You can also set the <code>latest</code> parameter to a version number to install a specific version of the add\-on. For more details, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_Release_Notes">Add\-on release notes</a>.</div>


<span id="6v0wGVui"></span>
### Step 2: Install the add\-on


* The command for installing the add\-on on an ECS instance is as follows:


```PowerShell
./o11yagentd_ecs.ps1 --region ${region} --o11yagent.service_id o11yagent_ecs
```



* The command for installing the add\-on on a GPU ECS instance is as follows:


```PowerShell
./o11yagentd_ecs.ps1 --region ${region} --o11yagent.service_id o11yagent_hpc
```


<span id="MtpXwfUl"></span>
### Step 3: Check the result


1. Run the following command to check whether the add\-on is installed.

   ```bash
   o11yagentctl.exe ps
   ```
   

   The following sample shows the expected result. You can view the process of the installed add\-on, and the `STATUS` of the add\-on is `online`, which indicates that the add\-on is installed and is working as expected.

   ```bash
   AGENT_ID                 NAME     PKG              STATUS      START_TIME
   ecs_i-ydmrej19***        o11yagent_ecs:3.23.0      online      2025-01-09 06:13:53.266884841 +0000 UTC
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to a delay in the update of <code>STATUS</code> for the add\-on, it is recommended to check the status of the add\-on multiple times.   </div>
   

1. Log in to the [Cloud Monitor console](https://console.byteplus.com//cloud-monitor). In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**. Click the name of the target ECS instance to go to the monitoring details page, where you can view the monitoring information of the ECS instance.





</Tab>
</Tabs>


<span id=".5L2_55So5om56YeP5L2c5Lia5a6J6KOF5o-S5Lu2"></span>
## Method 2: Install the add\-on by using the cloud assistant Agent

The cloud assistant Agent is a native automated O&M tool developed by the platform. You can use a batch job to efficiently run O&M commands on single or multiple execution targets without passwords, login, and jump servers. You can use a batch job to quickly install the O11yAgent add\-on on multiple ECS instances.

<span id=".5q2l6aqk5LiA77ya5YmN572u5qOA5p-l"></span>
### Step 1: Check before installation


1. Log in to the [ECS console](https://console.byteplus.com/ecs).

2. In the left navigation bar, click **Maintenance & Monitoring \> Cloud Assistant**.

3. Click the **Public commands** tab and check whether the public command **Cloud Monitor ECS collection add\-on installation** exists.

4. Check whether the target ECS instance is installed with the batch job agent. Otherwise, the installation will fail, and the `CloudAssistantNotInstalled` message will appear. For the method of installing the batch job agent, refer to [Install Cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).


<span id=".5q2l6aqk5LqM77ya5Yib5bu65om56YeP5L2c5Lia"></span>
### Step 2: Create a batch job


1. On the **Public commands** tab, click **Create a job** in the **Cloud Monitor ECS collection add\-on installation** section to create an add\-on installation batch job.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The public command provides two versions of the Cloud Monitor ECS collection add\-on installation: Linux and Windows. Select an appropriate job for creation based on your business requirements.</div>



   * **Basic information**: Specify the basic information of the batch job.

   * **Execute command**: Specify the add\-on installation parameters.

      
      |Parameters |Required |Parameter Description |Parameter Type |Sample Value |
      |---|---|---|---|---|
      |site |No |The site to which the ECS instance belongs. Valid values:<br><br><br>* **volcengine**: BytePlus<br><br>* **byteplus**: BytePlus |The value is a string and must be 1 to 1,000 characters in length. |volcengine |
      |region |No |The ID of the region where the ECS instance is located. For more details, refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). |The value is a string and must be 1 to 1,000 characters in length. |cn\-beijing |
      |o11yagentd_version |No |The version number of the o11yagentd add\-on. The default value is `latest`, which indicates that the latest version of the add\-on is installed. You can also set the value to a version number to install a specific version of the add\-on. For more details, refer to [Add-on release notes](https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_Release_Notes). |The value is a string and must be 1 to 1,000 characters in length. |latest |
      |o11yagent_version |No |The version number of the o11yagent add\-on. The default value is `latest`, which indicates that the latest version of the add\-on is installed. You can also set the value to a version number to install a specific version of the add\-on. For more details, refer to [Add-on release notes](https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_Release_Notes). |The value is a string and must be 1 to 1,000 characters in length. |latest |
      |o11yagentd_control_plane_region |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the ECS instance and the o11yagentd control plane are deployed in different regions.</div><br> |Specify the ID of the region where the o11yagentd control plane is located. |The value is a string and must be 1 to 1,000 characters in length. |cn\-beijing |
      |o11yagentd_log_dir |No |The log path of the o11yagentd add\-on. |The value is a string and must be 1 to 1,000 characters in length. |/tmp/log |
      |o11yagentd_cpu_quota |No |The CPU upper limit of the o11yagentd add\-on. Unit: percentage of CPU core. For example:<br><br><br>* A value of 50 or 50% indicates 0.5 core.<br><br>* A value of 200 or 200% indicates 2 cores. |The value is a string and must be 1 to 1,000 characters in length. |50 |
      |o11yagentd_memory_max |No |The memory upper limit of the o11yagentd add\-on. Unit: bytes. For example:<br><br><br>* A value of 2048 indicates 2048 bytes.<br><br>* A value of 1024K or 1024k indicates 1024 KB.<br><br>* A value of 200M or 200m indicates 200 MB.<br><br>* A value of 1G or 1g indicates 1 GB. |The value is a string and must be 1 to 1,000 characters in length. |1024 |
      |o11yagent_total_cpu_quota |No |The total CPU upper limit of the o11yagent add\-on. Unit: percentage of CPU core. For example:<br><br><br>* A value of 50 or 50% indicates 0.5 core.<br><br>* A value of 200 or 200% indicates 2 cores. |The value is a string and must be 1 to 1,000 characters in length. |100 |
      |o11yagent_total_memory_max |No |The total memory upper limit of the o11yagent add\-on. Unit: bytes. For example:<br><br><br>* A value of 2048 indicates 2048 bytes.<br><br>* A value of 1024K or 1024k indicates 1024 KB.<br><br>* A value of 200M or 200m indicates 200 MB.<br><br>* A value of 1G or 1g indicates 1 GB. |The value is a string and must be 1 to 1,000 characters in length. |2048 |
      |o11yagent_cpu_quota |No |The CPU upper limit of the o11yagent add\-on. Unit: percentage of CPU core. For example:<br><br><br>* A value of 50 or 50% indicates 0.5 core.<br><br>* A value of 200 or 200% indicates 2 cores. |The value is a string and must be 1 to 1,000 characters in length. |100 |
      |o11yagent_memory_max |No |The memory upper limit of the o11yagent add\-on. Unit: bytes. For example:<br><br><br>* A value of 2048 indicates 2048 bytes.<br><br>* A value of 1024K or 1024k indicates 1024 KB.<br><br>* A value of 200M or 200m indicates 200 MB.<br><br>* A value of 1G or 1g indicates 1 GB. |The value is a string and must be 1 to 1,000 characters in length. |1024 |
      |instance_type |No |The type of the ECS instance. Valid values:<br><br><br>* **ecs**: the ECS instance<br><br>* **gpu**: the ECS instance of the heterogeneous computing type For more details, refer to [About instance specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |The value is a string and must be 1 to 1,000 characters in length. |ecs |
      |registry_address |No |The o11yagent output address. |The value is a string and must be 1 to 1,000 characters in length. |http://127.0.0.1 |
      

      * **Execute path**: Specify the job execution path, which is `/home` by default on ECS instances with Linux operating systems.

      * **Execute user**: Specify the executor of the job, which is `root` by default on ECS instances with Linux operating systems. You can select another executor to reduce risk.

      * **Timeout**: Specify the timeout for the job. When the command execution times out, the system will automatically terminate the task process.

   * **Execution mode**: Select the execution method of the job. Valid values:

      * **Execute immediately**: The job is executed immediately after the configuration is complete.

      * **Scheduled execution**: The job is executed at a specified point in time. If you select this option, you must specify a specific date and point in time when the job is executed.

      * **Periodic execution**: The job is periodically executed **by minute**, **by hour**, or **by day**. You can also specify the start time and end time for the periodic execution.

   * **Execute object**: Select the target ECS instance from the **Total** list to add it to the **Selected** list.

   * **Advanced configuration**: Specify the project to which the job belongs and labels.

2. Click **Create** to complete the configuration.


<span id=".5q2l6aqk5LiJ77ya57uT5p6c6aqM6K-B"></span>
### Step 3: Check the result


1. After the add\-on is installed, click the **Job management** tab and view the target job in the job list. If **Execution successful** is displayed in the **Status** column, it indicates the add\-on is installed on the ECS instance.

2. Log in to the [Cloud Monitor console](https://console.byteplus.com//cloud-monitor). In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**. Click the name of the target ECS instance to go to the monitoring details page, where you can view the monitoring information of the ECS instance.
