---
title: "Troubleshooting common issues with collection add-ons"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Plug-in_troubleshooting"
---

<span id="NcCW0hPU"></span>
## Missing general metrics

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The o11yagent add\-on comes in two variants: o11yagent_ecs and o11yagent_hpc. This topic provides an example on how to troubleshoot the o11yagent_ecs add\-on. When you troubleshoot the o11yagent_hpc add\-on, replace the process name in the following example with o11yagent_hpc.</div>


<span id="fSsQ1zT7"></span>
### Check whether the add\-on is installed


1. Log in to the Elastic Compute Service (ECS) instance by using ECS Terminal. For more details, refer to [Login method overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to check whether the o11yagent_ecs add\-on is installed.


```Bash
o11yagentctl ps
```


If the o11yagent_ecs add\-on is installed, the system will print the process information about the add\-on.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1d008558ba5121f2b4554dcd0c44dc4.png) </span>

View the values displayed in the `STATUS` and `START_TIME` columns. When the add\-on is running as expected, the status displayed in the `STATUS` column is `online`. The time displayed in the `START_TIME` column is approximately the time when the add\-on is installed. Convert the time based on the time zone.

If the system does not print the process information about the o11yagent_ecs add\-on or the value displayed in the` STATUS` column is not `online`, it indicates that the add\-on fails to be installed. Submit a ticket to address the issue.

<span id="MBwe0OEC"></span>
### View runtime logs

If o11yagent_ecs is installed, you need to check its runtime logs. The logs are stored in the `/var/log/o11yagent_ecs` directory.

```Bash
$ ls -al /var/log/o11yagent_ecs
```


The following sample code shows the expected result, in which two log files including o11yagent_core.log and o11yagent_plugin.log are displayed.

```Bash
total 129752
drwxr-xr-x  2 root root     4096 Apr 20 08:09 .
drwxr-xr-x 18 root root     4096 Apr 24 10:50 ..
-rw-r--r--  1 root root  2691188 Apr 24 10:56 o11yagent_core.log
-rw-r--r--  1 root root 17542449 Apr 24 11:00 o11yagent_plugin.LOG
```


Run the following command to check the o11yagent_plugin.log file and filter out error logs.

```Bash
cat /var/log/o11yagent_ecs/o11yagent_plugin.LOG | grep "ERR"
```


Submit a ticket and provide `AGENT_ID` and error logs for technical support.

If the o11yagent_plugin.log file does not exist, exceptions may occur on the o11yagent_ecs configuration file. Further check o11yagent_core.log. Then, submit a ticket and provide `AGENT_ID` and error information for technical support.

<span id="uQaE2bD0"></span>
## Missing GPU metrics


1. Check whether the monitoring add\-on is in a normal status. For more details, refer to the preceding **Missing general metrics** section.

2. If general metrics are obtained but only GPU metrics are missed, log in to the ECS instance and run the following command to check whether a GPU driver is installed on the ECS instance. Take NVIDIA GPU as an example.


```Bash
nvidia-smi
```


The following figure shows the expected result if the GPU driver is installed.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24aa75138db41d2d408dbdafe05a6350.png) </span>


3. Check whether the GPU driver is installed again. After the driver is installed again, you need to restart monitoring or the instance to obtain data as expected.

4. Check whether the version is outdated. You can upgrade the monitoring version.


<span id="fR9Ic7Xe"></span>
## GPU driver reinstallation fails due to the monitoring program occupying the GPUs

After you uninstall a GPU driver, you need to restart the operating system before you can reinstall the GPU driver. We recommend that you perform the following steps to reinstall the GPU driver.


1. Log in to the ECS instance by using ECS Terminal. Run the `reboot` command to reinstall the system.

2. Run the `o11yagentctl stop [agent id]` command to stop the cloud\-monitor\-agent add\-on.

3. Install the driver.

4. Run the `o11yagentctl start [agent id]` command to restart the cloud\-monitor\-agent add\-on.
