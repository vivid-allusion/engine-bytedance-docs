---
title: "Using second-level monitoring feature"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Using_monitoring_by_seconds"
---

This topic describes how to configure and use the second\-level monitoring feature provided by BytePlus.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, please contact your account manager.</div>


<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

In Large Language Model (LLM) training scenarios, a hybrid approach integrating Tensor Parallelism (TP), Pipeline Parallelism (PP), and Data Parallelism (DP) is widely adopted to minimize communication overhead. TP primarily involves intra\-instance computation and communication, with relatively fixed implementations provided by NVIDIA. PP is a high\-frequency activity (operating at 40 ms intervals) with millisecond\-level single\-execution latency. DP is a low\-frequency activity (operating at 5s intervals) with 100 ms\-level single\-execution latency.

To help you resolve communication\-related issues more precisely and efficiently, BytePlus offers a second\-level monitoring feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Create a Vital Managed Service for Prometheus (VMP) in the same region as your cluster. For more information, see [Vital Managed Service for Prometheus](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus).


> Select an appropriate workspace type based on your actual needs.



* Execute the following command to check the version of the Cloud Monitor plugin and make sure that a version no lower than 3.16.0 is installed on the instance:

   ```Plain Text
   LD_LIBRARY_PATH=/usr/local/cloud-monitor-agent/lib /usr/local/cloud-monitor-agent/cloud-monitor-agent version --config-file /usr/local/cloud-monitor-agent/config.yaml
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the plugin is not installed or the version is too low, reinstall it. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent">Installing plugin</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your instance cluster is large in scale, use the cloud assistant feature to quickly install the plugin. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Batch-install-cloud-monitor-plugin">Batch installing Cloud Monitor plugin</a>.   </div>
   

* Make sure that Grafana is installed. For more information, see [Install Grafana](https://grafana.com/docs/grafana/latest/setup-grafana/installation/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5byA5ZCv56eS57qn55uR5o6n5Yqf6IO9"></span>
### Step 1: Enable the second\-level monitoring feature

<span id=".5L2_55So5om56YeP5L2c5Lia6YWN572u"></span>
#### Cloud assistant\-based configuration

When you enable the second\-level monitoring feature on large\-scale instances, you can use the cloud assistant feature to automatically complete the monitoring configuration in a batch.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enable the second\-level monitoring feature for non\-RDMA metrics, refer to the "Manual configuration" section below.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" to enter the job management page.

4. Select the "Custom commands" tab and click the "Create a custom command" button.

5. On the "Create a custom command" page, configure the following information to create a custom command.

   > This topic only describes the differentiated parameters. For the complete parameter description, see [Cloning to custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-public-command#.5YWL6ZqG5Yiw6Ieq5a6a5LmJ5ZG95Luk).   
   

   
   |Argument |Description |Sample value |
   |---|---|---|
   |Command type |Select "Python" for "Command type". BytePlus provides a Python script to help you complete the configuration quickly. |Python |
   |Command contents |Copy and paste the following content.<br><br>```Bash```<br>```#!/usr/bin/python```<br>```# -*- coding: utf-8 -*-```<br>```import json```<br>```import subprocess```<br>``````<br>```file_path = "/usr/local/cloud-monitor-agent/conf_plugin.json"  # Specify the file path```<br>```# Enter the new value.```<br>```enable={{enable}}```<br>```infoList='''{{user_password_url_list}}'''```<br>``````<br>```flag = False```<br>```if enable == 1:```<br>```   flag = True```<br>``````<br>```# Add a backslash before each double quote.```<br>```infoList = infoList.replace('"', '\"')```<br>``````<br>```# Read the file content and process it.```<br>```with open(file_path, "r") as file:```<br>```     data = json.load(file)```<br>``````<br>```# Modify the value.```<br>```data["PrometheusRdmaCounterCollectorEnabled"] = flag```<br>```data["PrometheusUserPasswordUrlList"] = infoList```<br>``````<br>```# Save the modified content to the file.```<br>```with open(file_path, "w") as file:```<br>```   json.dump(data, file, indent=4)```<br>``````<br>```subprocess.call(["systemctl", "daemon-reload"])```<br>```subprocess.call(["systemctl", "restart", "cloud-monitor-agent.service"])```<br> |\- |
   |Use argument |Select this option to use custom parameters. When this option is selected, custom parameters in the command content will be displayed automatically. |\- |
   

   Example:

6. If your instance does not have the cloud assistant Agent installed, perform the following steps to install it.

   * Batch installation in the console

      Click the "Agent management" tab, select the instances that require second\-level monitoring, and install the cloud assistant Agent.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can batch install the cloud assistant Agent on multiple instances in the console. After successful installation, you need to restart the instances for the configuration to take effect.      </div>
      

   * Install cloud assistant Agent by executing the scripts manually

      You can install the cloud assistant Agent in an instance by using the script provided by BytePlus.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After script\-based installation is complete, you do not need to restart the instance.      </div>
      

      * Installation​ through intranet

         Execute the following command in the instance to install the cloud assistant Agent through the BytePlus private network.

         ```Bash
         # Beijing Region
         sudo bash -c "$(curl http://assist-client-beijing.tos-cn-beijing.ivolces.com/install.sh)"
         
         # Shanghai Region
         sudo bash -c "$(curl http://assist-client-shanghai.tos-cn-shanghai.ivolces.com/install.sh)"
         
         # Guangzhou Region
         sudo bash -c "$(curl http://assist-client-guangzhou.tos-cn-guangzhou.ivolces.com/install.sh)"
         ```
         

          or 

         ```Bash
         # Beijing Region
         sudo bash -c "$(curl http://assist-client-beijing.tos-s3-cn-beijing.ivolces.com/install.sh)"
         
         # Shanghai Region
         sudo bash -c "$(curl http://assist-client-shanghai.tos-s3-cn-shanghai.ivolces.com/install.sh)"
         
         # Guangzhou Region
         sudo bash -c "$(curl http://assist-client-guangzhou.tos-s3-cn-guangzhou.ivolces.com/install.sh)"
         ```
         

      * Installation​ through internet

         If [an EIP is associated with your ECS instance](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), you can execute the following command to install the cloud assistant Agent through the Internet.

         ```Plain Text
         sudo bash -c "$(curl http://assist-client.tos-cn-beijing.volces.com/install.sh)"
         ```
         

          or 

         ```Plain Text
         sudo bash -c "$(curl http://assist-client.tos-s3-cn-beijing.volces.com/install.sh)"
         ```
         

7. Create a cloud assistant task to configure the second\-level monitoring feature on the target instance.

   1. Select the "Job management" tab and click the "Create a job" button.

   2. On the "Create a job" page, fill in the information in the following table.

      > This topic only describes the differentiated parameters. For the complete parameter description, see [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).      
      

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Job name |Set the job name. |Configure the second\-level monitoring feature |
      |Command type |Select "Custom commands". |Custom commands |
      |Command |Select the custom command you created in Step 4. |Configure second\-level monitoring |
      |Parameter​ |The parameters for second\-level monitoring.<br><br><br>* enable: Required. Whether to enable the second\-level monitoring feature for RDMA metrics. Valid values:<br><br>   * `0`: Disable.<br><br>   * `1`: Enable.<br><br>* user_password_url_list: Required. Format: `[{"user":"xxx","passwd":"xxx","url":"http://write.prometheus-cn-beijing.ivolces.com/workspaces/xxx"}]`. Where:<br><br>   * user: Enter the VMP username.<br><br>   * passwd: Enter the VMP login password for the corresponding user.<br><br>   * url: Enter the Remote Write URL. For more information, see [Obtaining Remote Write and Query addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). |\- |
      |Execute object |Select the instance for which you want to configure second\-level monitoring based on information such as the instance name, project, or tag. |\- |
      

   3. Click the "Confirm" button to complete the job creation.

   4. After the job is created, the system automatically redirects you to the Job management page. The new job then executes automatically based on its execution method.

   5. You can view the execution status and results of the job on each instance by following the instructions in [Viewing job execution results](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results).


<span id=".5omL5Yqo6YWN572u"></span>
#### Manual configuration

If you only need to use the second\-level monitoring feature on a few instances or need to enable second\-level monitoring for non\-RDMA metrics, you can manually configure the second\-level monitoring feature according to the instructions in this section.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to open the /usr/local/cloud\-monitor\-agent/conf_plugin.json configuration file.

   ```Plain Text
   vi /usr/local/cloud-monitor-agent/conf_plugin.json
   ```
   

3. Press the `i` key to enter edit mode and modify the following parameters.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8618ca13f72c50851075b6f8c2b02744.png) </span>

   Parameter descriptions:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |PrometheusRdmaCounterCollectorEnabled |Whether to enable second\-level monitoring for RDMA metrics. Valid values:<br><br><br>* true: Enable<br><br>* false: Disable. |true |
   |PrometheusNormalCollectorEnabled |Whether to enable second\-level monitoring for non\-RDMA metrics. Valid values:<br><br><br>* true: Enable<br><br>* false: Disable<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot configure the collection interval. The default collection interval is 30s.</div><br> |true |
   |PrometheusUserPasswordUrlList |The Basic Auth settings for the VMP workspace. Multiple workspaces are supported. Format: `[{"user":"xxx","passwd":"xxx","url":"http://write.prometheus-cn-beijing.ivolces.com/workspaces/xxx"}]`.<br><br><br>* user: Enter the VMP username.<br><br>* passwd: Enter the VMP login password for the corresponding user.<br><br>* url: Enter the Remote Write URL. For more information, see [Obtaining Remote Write and Query addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). |\- |
   

4. Execute the following command to restart the Cloud Monitor service.

   ```Plain Text
   systemctl restart cloud-monitor-agent.service
   ```
   


<span id=".5q2l6aqk5LqM77ya6YWN572uR3JhZmFuYQ=="></span>
### Step 2: Configure Grafana


1. Log in to Grafana.

2. Click the "Toggle menu" button in the upper left corner, and then select "Connections \> Data Sources" from the directory tree on the left.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3fa6a63b33f83a1e2953a846bb61b525.png) </span>

3. Click the "Add data source" button, and search for and add Prometheus.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_be90a1a4bec0dbe347f34f6c09ca49c3.png) </span>

4. On the "Settings" tab, configure the VMP data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_084e150e44e68d68438a5d4bdb80bb7b.png) </span>

   Parameter descriptions:

   
   |Parameter |Description |
   |---|---|
   |Prometheus server URL |Enter the query URL. For more information, see [Obtaining Remote Write and Query addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). |
   |Basic auth |Enable this feature to use VMP authentication information. |
   |User |Enter the VMP username. |
   |Password |Enter the VMP login password for the corresponding user. |
   

5. After the configuration is complete, click the "Save & test" button at the bottom of the page.

6. Select "Dashboards" from the directory tree on the left, and choose "Import" from the "New" drop\-down list on the right.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a615be94c31befc7e88c804e576aff3a.png) </span>

7. Select the BytePlus second\-level monitoring JSON file, and click the "import" button to import the file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not have the BytePlus second\-level monitoring JSON file, contact your account manager to obtain it.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3fa1d69eafa8f1d63f75d07996c704e1.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_272c000cccd551d941c710aa2d3ae9c5.png) </span>

8. After the file is imported, you can view BytePlus instance second\-level monitoring data directly in Grafana.
