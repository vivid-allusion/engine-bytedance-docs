---
title: "How to resolve the failure in collecting monitoring data by Cloud-monitor-agent of ECS instances?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Resolve-the-issue-of-missing-monitoring-metrics"
---

This topic introduces how to troubleshoot the failure of viewing monitoring information of ECS instances caused by the Cloud Monitor plugin.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When the Cloud Monitor plugin is not installed, is outdated, or malfunctions, monitoring metrics of ECS instances may be missing. You can follow this topic to troubleshoot the issue and restore metric display.

<span id=".6Zeu6aKY56Gu6K6k"></span>
## Issue confirmation


1. Log in to the faulty ECS instance. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following command on the instance to confirm whether the Cloud Monitor plugin is installed.

   ```Plain Text
   systemctl list-units --type=service
   ```
   

   * If the Cloud Monitor plugin is installed, as shown in the picture below, follow the [troubleshooting](https://docs.byteplus.com/en/docs/ecs/Resolve-the-issue-of-missing-monitoring-metrics#.5pWF6Zqc5o6S5p-l) guide for further operations.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1107688790de23a5827eebac449f92ea.png) </span>

   * If the `cloud-monitor-agent` service is not found, complete the plugin installation.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For Windows operating system instances, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent?lang=zh&TagIDs=373#c3a69176">Install the plugin on Windows instances</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For Linux operating system instances, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent?lang=zh&TagIDs=373#u5GIs09l">Install the plugin on Linux instances</a>.      </div>
      


<span id=".5pWF6Zqc5o6S5p-l"></span>
## Troubleshooting

<span id=".5pON5L2c57O757uf55uR5o6n57y65aSx"></span>
### Missing operating system monitoring

If the monitoring metrics of your operating system are abnormal or missing, troubleshoot based on the following content.


1. Log in to the faulty ECS instance. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following command in the instance to view the running status of the Cloud Monitor plugin.

   ```Plain Text
   systemctl status cloud-monitor-agent   
   ```
   

   * If the service status of the Cloud Monitor plugin is **active(running)**  (normal operation), as shown in the picture below,  contact your account manager for technical support.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca3949bfbbc00ff224218bd35aaedf03.png) </span>

   * If the plugin is not in the **active(running)**  (normal operation) state as shown below, refer to [Installing the plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent) to update the cloud monitoring plugin.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_452333e277cf0aa40941d6b28241907a.png) </span>

3. Follow these steps to confirm the repair result:

   1. Execute the following command to confirm that the Cloud Monitor plugin is in the **active(running)**  status.

      ```Plain Text
      systemctl status cloud-monitor-agent   
      ```
      

   2. Execute the following command to verify whether the version of the Cloud Monitor plugin meets expectations.

      ```Apex
      LD_LIBRARY_PATH=/usr/local/cloud-monitor-agent/lib /usr/local/cloud-monitor-agent/cloud-monitor-agent version --config-file /usr/local/cloud-monitor-agent/config.yaml
      ```
      

   3. Log in to the [ECS console](https://console.byteplus.com/ecs/instance) to confirm whether the missing metrics of the faulty instance are now displayed correctly.

   4. If any result of the previous two steps is still abnormal,   contact your account manager for technical support.


<span id=".VENQ6L-e5o6l55uR5o6n57y65aSx"></span>
### Missing TCP connection monitoring

If metrics of TCP connection monitoring are abnormal or missing, troubleshoot as described in this section.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If TCP connection monitoring is enabled, the performance of the instance TCP bandwidth will be impacted to a certain extent.</div>


* <div data-tips="true" data-tips-type="warning">To avoid data collection failure caused by an in\-band monitoring component of an outdated version, we recommend upgrading the plugin as guided by the console prompts. Or, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent">Installing plugins</a>.</div>


1. Confirm whether the image used by the instance supports viewing TCP connection monitoring metrics. For the list of supported images, see [Usage instructions](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data#.5p-l55yLdGNw6L-e5o6l55uR5o6n5pWw5o2u).

2. If the image supports metric viewing, continue with the following troubleshooting.

3. Log in to the faulty ECS instance. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

4. Install the Cloud Monitor plugin with reference to [Installing plugins](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent). 

   > During plugin installation, the `systemctl daemon-reload` command is executed automatically. To avoid business interruptions, please do not perform any operations on the instance that may cause conflicts.   
   

5. Execute the following command to check whether the Cloud Monitor plugin service is running normally.

   ```Plain Text
   systemctl status cloud-monitor-agent
   ```
   

   Example of normal operation:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75f37df5c24a79ddc2f6c8e58c99cef0.png) </span>

6. Execute the following command to enable the TCP connection service.

   ```Plain Text
   sed -i 's/EBPF: true/EBPF: false/' /usr/local/cloud-monitor-agent/config.yaml
   ```
   

7. Execute the following command to restart the Cloud Monitor plugin service.

   ```Plain Text
   systemctl restart cloud-monitor-agent
   ```
   

8. When all steps are successfully performed, wait a few minutes. To obtain technical support when metrics are still missing,  contact your account manager.


<span id=".6L-b56iL55uR5o6n5oyH5qCH57y65aSx"></span>
### Missing process monitoring metrics

If only metrics of "Network bytes received/sent" and "Network packets received/sent" under process monitoring are missing, confirm:


* The keep\-alive time of the TCP connection exceeds 30s, and processes have performed network I/O.

* The operation flow matches the [process monitoring](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics) descriptions.
