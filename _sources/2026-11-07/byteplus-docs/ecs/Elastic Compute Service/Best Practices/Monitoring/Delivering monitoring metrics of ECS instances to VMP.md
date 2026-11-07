---
title: "Delivering monitoring metrics of ECS instances to VMP"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deliver_instance_monitoring_information_to_Entrusted_Prometheus_service"
---

This topic mainly describes how to deliver the monitoring metric information of ECS instances to Vital Managed Service for Prometheus (VMP).

<span id=".5LuA5LmI5piv5omY566hUHJvbWV0aGV1c-acjeWKoQ=="></span>
## What is VMP

Vital Managed Service for Prometheus (VMP) is a cloud\-native monitoring product of BytePlus. It supports maintenance\-free operation, high performance, high stability, and other features. You can quickly deliver the monitoring information of ECS instances into the VMP service to build your new\-generation, cloud\-native monitoring engine.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have enabled VMP service. For details, see [Getting started](https://docs.byteplus.com/en/docs/vmp/Quick-start).

* You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances), which meets the following requirements:

   * The ECS instance and VMP service reside in the same region.

   * The ECS instance has the following plugins installed:

      * Cloud Monitor plugin. If not installed, follow the guide for [installing an agent](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent) to complete the installation.

      * Cloud assistant plugin. If not installed, follow the [guide for installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) to complete the installation.

   * Security group: Allow inbound traffic for `TCP` port `9091`. For detailed operations, see [Managing security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L-u5pS55LqR55uR5o6n5o-S5Lu26YWN572u"></span>
### Step 1: Modify configurations of Cloud Monitor plugin


1. Log in to the [cloud assistant console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/invocations?tab=taskList).

2. Select the "Job management" tab, and click the "Create a job" button to enter the job creation page.

3. Enter the following job information as instructed.

   > This practice only describes necessary parameters. Other parameters remain at their default values. Adjust parameters based on your needs. For parameter details, refer to[ Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job#.5pON5L2c5q2l6aqk).   
   

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Job name |Set the job name. |Modify configurations of Cloud Monitor plugin |
   |Command type |Select "Manual input". |Manual input |
   |Command contents | |\- |
   |Object |Select ECS instances that meet the requirements for you to execute the job by instance name, project, tag, or other information. You can select multiple instances at one time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select up to 200 ECS instances.</div><br> |\- |
   

4. Click the "Confirm" button to complete the job creation.

5. After the job is created, the system automatically redirects you to the Job management page. The new job is then executed immediately.

6. You can follow the [guide for viewing job execution results](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results) to confirm whether the job has been successfully executed on each target instance.


<span id=".5q2l6aqk5LqM77ya5a6J6KOFR3JhZmFuYQ=="></span>
### Step 2: Install Grafana

You can install Grafana on a BytePlus ECS instance and view monitoring information on that instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To install Grafana, the instance is required to meet the following requirements:</div>



* <div data-tips="true" data-tips-type="warning">An EIP is associated with the instance. If not associated, follow the <a href="https://docs.byteplus.com/en/docs/ecs/associating-an-EIP">guide for associating EIPs</a> to complete the operation.</div>


* <div data-tips="true" data-tips-type="warning">To install and use Grafana, certain conditions are required to be met. For details, see <a href="https://grafana.com/docs/grafana/latest/setup-grafana/installation/">Installing Grafana</a>.</div>


* <div data-tips="true" data-tips-type="warning">Since Grafana uses port <code>3000</code> for communication by default, make sure that the security group of the instance with Grafana installed has allowed inbound traffic on <code>TCP</code> port <code>3000</code>. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules">Modifying security group rules</a>.</div>


1. Log in to the instance with Grafana to be installed. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-an-instance).

2. Execute the following commands to install Grafana.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this practice, Grafana 10.2.1 is installed on an Ubuntu instance. For Grafana download links for more operating systems and more Grafana versions, see <a href="https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1">Downloading Grafana</a>.   </div>
   

   ```Plain Text
   sudo apt-get update
   sudo apt-get install -y adduser libfontconfig1 musl
   wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.2.1_amd64.deb
   sudo dpkg -i grafana-enterprise_10.2.1_amd64.deb
   ```
   

3. After the installation is complete, you can execute the following command to check whether Grafana is started as expected.

   ```Plain Text
   systemctl status grafana-server
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_589f6daf64da558156fbf7a2970442b4.png) </span>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65bel5L2c5Yy6"></span>
### Step 3: Create a workspace


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the left\-side navigation pane, select "Workspace" to enter the workspace list page.

3. In the top menu bar, select a target region.

4. Click the "Create" button, and configure the workspace as follows.

   > This practice only describes necessary parameters. Other parameters remain at their default values. For detailed parameter descriptions, see [Creating a common workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).   
   

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Region |Deploy the workspace in the same region as the target instance. |China (Beijing) |
   |Workspace name |Specify the workspace name. Data in workspaces with different names is isolated from each other. |ECS2VMP |
   |Basic Auth |Enable the Basic Auth authentication feature.<br><br><br>* After this feature is enabled, the workspace supports authentication and authorization via **username/password** or **BytePlus AK/SK** for writing and querying data.<br><br>* To enable the Basic Auth authentication feature, the following information is required for authentication:<br><br>   * **username**: The username used for Basic Auth authentication.<br><br>   * **password**: The password used for Basic Auth authentication.<br><br>   * **Confirm password**: Re\-enter the password used for Basic Auth authentication to ensure the two entries are the same. |\- |
   |Workspace instance type |In this practice, **Standard Edition** is used. |Standard Edition |
   

5. After you confirm the configuration information, select the "I have read and agreed to Vital Managed Service for Prometheus Dedicated Service Terms" checkbox.

6. Click the "Create Now" button to complete the creation.


<span id=".5q2l6aqk5Zub77ya5Yib5bu66ZuG5oiQ5Lu75Yqh"></span>
### Step 4: Create an integration task


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top menu bar, select a target region.

3. In the left\-side navigation pane, select "Integration Center", and select the "Product Service" tab.

4. Click the "Create Integration Task" button in the "ECS instance" tab to enter the process for creating an integration task for the ECS instance.

   1. Based on the instructions, click the "To authorize" button.

   2. On the "Cross\-service access request" page, click the "Authorize now" button to authorize VMP to use ECS instance metrics.

   3. After authorization is completed, on the Create Integration Task page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d419339db6634f785d35472744f38229.png) </span> button on the right of the "To authorize" button to update the authorization result.

   4. Enter the following task information as instructed.

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Task name |Set the integration task name. Chinese, English uppercase and lowercase letters, numbers, and underscores `_` are supported. Value range: 1 ~ 40 characters. |ECS2VMP |
      |Workspace |Choose a created VMP workspace. |ECS2VMP |
      |ECS VPC |Select the VPC where the ECS instance resides. |vpc\-hs032xxxx |
      |Security group |Select the security group for the managed collector and allow the managed collector to access resources in your VPC. Multiple selection is supported. |sg\-os23sdaxxxx |
      |Subnet |Choose the VPC subnet for service discovery. Then, the system performs ECS service discovery under the selected subnet and monitors all ECS instances that meet the requirements. Multiple selection is supported. |sub\-2ds3xxxx |
      |Job configuration |Configure information such as the VMP collection interval, collection timeout period, collection protocol, and port number for collection metrics. For details, see [ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring). ||
      

   5. Click the "Confirm" button to complete the integration task creation.


<span id=".5q2l6aqk5LqU77ya6YWN572uR3JhZmFuYQ=="></span>
### Step 5: Configure Grafana


1. Enter the Grafana management page to log in.

   * Log in via the target instance

      If the target instance has GUI installed, you can access the Grafana management page on the instance.

      1. Log in to the target instance. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

      2. Visit the following link in the instance browser.

         ```Plain Text
         http://localhost:3000
         ```
         

      3. Enter the default username `admin` and password `admin`, and click the "Log in" button.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91a00d89f314259ef0896a070668e348.png) </span>

   * Log in remotely

      If the target instance does not have GUI installed, you can log in remotely from a server that has GUI installed and can access the Internet.

      1. Log in to the remote server.

      2. Visit the following link in the browser on the remote server.

         ```Plain Text
         http://< Public IP of the target instance >:3000
         ```
         

      3. Enter the default username `admin` and password `admin`, and click the "Log in" button for login.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91a00d89f314259ef0896a070668e348.png) </span>

2. Enter the new login password and click the "Submit" button to complete the password change.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93debd113e951468378f50fbfc380630.png) </span>

3. In the left\-side navigation pane of the Grafana home page, select "Connections \> Data sources".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_feddd2745006abdc8331ae464b8deaa2.png) </span>

4. On the "Data sources" page, click the "Add data source" button to add a data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e61cd84635e5d3fad9a2325f41055d1.png) </span>

5. On the "Add data source" page, click "Prometheus".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11b7ce8d6e4e427c52ff544d092268d8.png) </span>

6. After the data source is successfully added, on the "prometheus" page, configure information as follows.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Connection |Enter the `Query URL` of the VMP workspace in `Prometheus server URL *`. For detailed instructions, see [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL). ||
   |Authentication |Select "Basic authentication" and enter the `Basic Auth` information you entered for creating the workspace. ||
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ce15194d173dd739637f2b3f33f2521.png) </span>

7. Click the "Save & test" button at the bottom of the page.

   If the following output is displayed, the workspace is associated with Grafana.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e768dbe6887837dddc64f26effb9e43d.png) </span>

8.  **(Optional)**  Configure monitoring information panes (Panel).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Panels used in this section are for reference only. You can use them or <a href="https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/">customize monitoring panels</a> based on your needs.   </div>
   

   1. Download the file "ECS cluster monitoring dashboard \- 20240120.json".

      <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3a2cbc02a647d498431ad0b781568f2e.json" name="ECS cluster monitoring dashboard - 20240120.json">ECS cluster monitoring dashboard - 20240120.json</Attachment>
      

   2. In the left directory tree, select "Home" to return to the Grafana home page.

   3. Click the "+" button in the upper right corner, and then click the "Import dashboard" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d121500cd17be33fb5727ff0de62cd80.png) </span>

   4. On the "Import dashboard" page, click the "Upload dashboard JSON file" button, and select the downloaded JSON file of the ECS cluster monitoring dashboard from your local device.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e68e027f3c10f942ad2c48ae837b18e.png) </span>

   5. In the "VMP" module, select the Prometheus data source you created, and then click the "Import" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_100d4afbb621567bc49f78d996db0920.png) </span>

9. You can check the operation result in Grafana.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d953979f8dc2d507e13d36450f783026.png) </span>


<span id=".6ZmE5b2V"></span>
## Appendix

<span id=".5L-u5pS55LqR55uR5o6n5o-S5Lu25ZG95Luk"></span>
### Command for modifying Cloud Monitor plugin configurations

You can execute this command to modify Cloud Monitor plugin configurations of ECS instances, enable the VMP monitoring port, and restart the plugin.

```bash
#!/bin/bash
# set Prometheus = true
sed -i 's/Prometheus: false/Prometheus: true/w /dev/stdout' /usr/local/cloud-monitor-agent/config.yaml | grep -q .
# returns 0 when substitutions have been made, and 1 when no match is found or file not found
if [ $? -eq 0 ]; then
    systemctl restart cloud-monitor-agent
fi
```
