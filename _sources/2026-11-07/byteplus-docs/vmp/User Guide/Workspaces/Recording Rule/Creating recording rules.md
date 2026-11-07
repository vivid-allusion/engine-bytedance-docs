---
title: "Creating recording rules"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-a-recording-rule"
---

The recording rule helps you perform secondary aggregation of the collected data and store it as new data, providing you with a faster and more convenient way to store and query data. This topic describes how to create a recording rule.

Vital Managed Service for Prometheus (VMP) supports the recording rule configurations natively supported by Prometheus. For more details, see the [official documentation](https://prometheus.io/docs/practices/rules/).

<span id="c5bfbd06"></span>
## Prerequisites


* You have registered and activated VMP.

* A workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id="d55105b1"></span>
## Procedures


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. Click **Workspace** in the left navigation bar, find the workspace for which you want to create a recording rule in the workspace list, and then click the workspace name to go to the Overview page of the workspace.

3. Click **Recording Rules Management** on the left navigation bar.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e4119d1b9440b0b3554d01e606baf4b6.png) </span>

4. Click **New rule file** and configure the recording rule file.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8f798bccc5172279ff6365e9b3b2996.png) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify the name of the recording rule file.<br><br><br>* The name is in the string format and must be 1 to 100 characters in length.<br><br>* The name of the rule file must remain unique within the same workspace. |
   |Write target |The target workspace into which query data is written from the source workspace. You can select a target workspace in the same region as the current workspace. |
   |YAML configuration |Specify the details of the recording rule file. The sample format and description of the recording rule file are shown below.<br><br>```yaml```<br>```groups:```<br>```    - interval: 1m```<br>```      name: recording_rules```<br>```      rules:```<br>```        - expr: sum(irate(container_cpu_usage_seconds_total{image!=""}[5m])) by (pod) *100```<br>```          labels:```<br>```            team: operations```<br>```          record: pod:cpu:useage```<br><br><br>In the same group, rules cannot have the same name, PromQL query statement, and label.<br><br>The description of each parameter is shown as follows:<br><br><br>* interval: the execution cycle of the rule group. The interval must be no less than 5 seconds.<br><br>* name: the name of the rule group.<br><br>* rules: the rules. Each rule group can contain multiple rules.<br><br>* expr: the PromQL query statement for data query and aggregation used by the system.<br><br>* labels: the labels added to the newly aggregated data, which can be in the `<labelname>:<labelvalue>` format.<br><br>* record: the name of the rule, which must conform to the [Prometheus metric name specification](https://prometheus.io/docs/concepts/data_model/?spm=a2c4g.11186623.0.0.31d76d08fYaRsA#metric-names-and-labels). |
   |Description |Specify the description of the recording rule file. You can provide a detailed description of the metric aggregation for the rule file. |
   |Allow for query acceleration |The query acceleration switch. Query acceleration is disabled by default. If query acceleration is enabled, the query pre\-aggregation feature is available to automatically rewrite pre\-aggregation metrics used by queries according to the rules. |
   

5. Click **Confirm** to complete the configuration.
