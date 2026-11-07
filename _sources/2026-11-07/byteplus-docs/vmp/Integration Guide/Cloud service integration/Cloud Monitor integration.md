---
title: "Cloud Monitor integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services"
---

Vital Managed Service for Prometheus (VMP) can be integrated with Cloud Monitor to meet your business requirements for centralized monitoring of basic cloud resources, cloud services, and custom businesses. This topic describes how to integrate VMP with Cloud Monitor.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[Beta \- Apply for trial]</strong>: This feature can be used only after your account is added to the allowlist of Cloud Monitor. If you want to use it, contact your account manager to help you enable the Exporter feature of Cloud Monitor.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id="PRRMSCbe"></span>
### Solution introduction

Cloud Monitor is a one\-stop monitoring and alerting solution on the  cloud. It enables you to gather and visualize the resource status and monitoring metrics of various  cloud products, such as ECS, clusters, gateways, dedicated connections, and cloud storage. For more details, see [What is Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor)?

You can integrate Cloud Monitor with VMP to export real\-time cloud service monitoring data from Cloud Monitor to VMP and merge the data with business monitoring data in your clusters. This achieves centralized monitoring of business data and basic resource data. In addition, you can use Grafana, which is natively compatible with VMP, to build business\-related dashboards.

<span id="6YogYixq"></span>
### Supported cloud products

The VMP Integration Center only allows you to export metrics from certain cloud services to Prometheus through Cloud Monitor. For details on supported cloud products, see [Supported cloud products](https://console.byteplus.com/cloud_monitor/exporter).

<span id="nitaoyUI"></span>
### Metric structure

In the exported data of Cloud Monitor, the metric name consists of `Namespace`, `SubNamespace`, and `MetricName`. For the values of each parameter, see [Cloud product metric queries](https://console.byteplus.com/cloud_monitor/docs).


* `Namespace` indicates the cloud service.

* `SubNamespace` indicates the sub\-category of metrics for a cloud service.

* `MetricName` indicates the metric name.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For example, when you export the metrics of ECS, <code>Namespace</code> is <code>VCM_ECS</code>, <code>SubNamespace</code> is <code>GPU</code>, and <code>MetricName</code> is <code>GpuTemperature</code>. The exported metric name is <code>GpuTemperature_GPU_VCM_ECS</code>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud Monitor has been activated, and the pay\-as\-you\-go billing method has been specified for Cloud Monitor.

* Relevant cloud services have been integrated with Cloud Monitor.

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YWN572u6ZuG5oiQ5Lu75Yqh"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click the name of the service to be integrated. This topic takes **Application Load Balancer (ALB)**  as an example.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you cannot find the service to be integrated in the integration center, you can click <strong>Cloud Monitoring (Batch Access)</strong> to try to integrate the target cloud service.   </div>
   

4. Check service authorization. The system will check whether permissions related to Cloud Monitor are granted. If related permissions are not granted or related features are disabled, grant permissions to access the service or enable features as prompted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f97dc9f5249c518a5c7a68c69fcb43fa.png) </span>

5. Click **Create integration task**, and click the **Start connecting** tab to specify the details of the integration task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a722d04ffe56dedfb859247990649288.png) </span>

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Configure the name of the integration task. |
   |workspace |Select a created VMP workspace. |
   |JobName |Specify the name of the Cloud Monitor collection task. It is used to distinguish the collection task from other collection tasks.<br><br>After integration, you can use the name to view the number of collected metrics on the [Resource consumption](https://docs.byteplus.com/en/docs/vmp/Resource-consumption) page. |
   |**Cloud Products selected** ||
   |Region |Select the region of the cloud service for which you want to collect metrics by using Cloud Monitor.<br><br>For some cloud services such as Cloud Enterprise Network (CEN) that are not deployed in regions, select **No region displayed**. |
   |Cloud Products selected |Select the cloud service for which you want to pull metrics from Cloud Monitor. |
   |**Acquisition Settings** ||
   |Acquisition interval |Configure the metric collection interval. |
   |Label export method |Configure the export method for cloud service metadata. Metadata mainly includes labels such as ProjectName and Name of cloud service instances.<br><br><br>* **Append to original metric**: Metadata will be appended to the original metric as a label. You can query metadata by using the original metrics.<br><br>* **Add as independent metric**: Metadata will be used as an independent metric. You can query metadata by using the `volc_resource_info` metric.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can export the metadata of only some cloud services, and metadata fields that can be exported vary based on different cloud services. For more details, see the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Feature_overview">documentation of Cloud Monitor</a>.</div><br> |
   |**Advanced Settings** ||
   |Instance export label key |Click **Add label key** to configure the  resource label to be exported when pulling product metrics from Cloud Monitor. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the label key list fails to be retrieved, check the GetTagKeys permission or network environment based on the error message and try again.</div><br> |
   |Metric Relabel configuration |Configure metric relabeling settings. You can add or replace labels in metrics during metric collection. For more details, see [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   |ProductConfig configuration |Configure metric filtering. You can filter collection objects by project, sub\-namespace, metric, and instance ID. For details, see the [ProductConfig configuration description](https://docs.byteplus.com/en/docs/88/22285#.55uR5o6n5L-h5oGv) section in this topic. |
   


<span id=".6I635Y-W55uR5o6n5aSn55uY"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view the examples of cloud service monitoring dashboards. Select the cloud service that you want to monitor from the **Cloud Products selected** list and click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e255cec73b9e1e03fcfe1bc22e564e5.png) </span>

<span id=".5p-l6K-i55uR5o6n5oyH5qCH"></span>
### Query metrics


1. Click the **Acquisition metric** tab.

2. Select the cloud service that you want to monitor from the **Cloud Products selected** list and select a sub\-category of metrics for the cloud service from the **SubNamespace** list. You can view the details of the metrics under that category.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f296bda69e2d7dbee433c6398d8adaa0.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more cloud service metrics, see <a href="https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric">Cloud Monitor metric queries</a>.</div>


<span id=".57uT5p6c6aqM6K-B"></span>
## What to do next

After the configuration is complete, you can view the integration task status and details to confirm whether Cloud Monitor is integrated with Prometheus. In addition, you can configure alert rules based on templates to promptly trigger alerts in case of exceptions.


1. In the left navigation bar, click **Integration Center \> Integration task**. On the page that appears, click the **Hosting environment** tab **.** 

2. In the task list, find the target task and click the task name to go to the details page of the task. On the details page, you can view the details and monitoring dashboards of the integration task.

   * Click the **Task information** tab and view the details of the integration task.

&nbsp;

   * Click the **Dashboard** tab and view the monitoring dashboards of the integration task. The dashboards include the number of cloud service instances, the number of cloud service metrics, total time taken for the last collection, and other dashboards.

&nbsp;

   * Click the **Alert template** tab to view the preset alert templates for the corresponding service. The tab displays information such as the template name, ID, version, type, description, number of associated alert rule groups, and time. Click **Apply template** in the **Actions** column that corresponds to the template to [create an alerting rule group](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups) based on the template.

&nbsp;


<span id=".55uR5o6n5L-h5oGv"></span>
## Advanced configuration

<span id="MeyPsRn4"></span>
### ProductConfig configuration description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you configure multiple filter conditions at the same time, the conditions are in an <strong>AND</strong> relationship. In this way, only objects or metrics that meet all conditions will be collected.</div>


```YAML
 #Only collect the metrics of resource objects in the specified project
ProjectName: [""]

 #Only collect the metrics in the specified sub-namespace
OnlyIncludeSubNamespaces: [""]

 #Exclude the metrics in the sub-namespace
ExcludeSubNamespaces: [""]

 #The metrics only need to be collected. <sub-namespace> indicates the sub-namespace of the cloud service.
OnlyIncludeMetrics:
  <subNamespace>: [""]

 # The excluded metric list. <sub-namespace> indicates the sub-namespace of the cloud service.
ExcludeMetrics: 
  <subNamespace>: [""]

 #Only collect the metrics of the specified instance IDs.
OnlyIncludeInstances: [""]

 #Exclude the metrics of instance IDs.
ExcludeInstances: [""]
```



|Parameter |Description |
|---|---|
|ProjectName |Filter collection objects by project. For example, if you set the `ProjectName parameter to ["default"]`, only objects in the `default` project are collected. |
|OnlyIncludeSubNamespaces |Filter collection metrics by cloud service sub\-namespace and only collect the metrics of the specified sub\-namespace.<br><br>**For example**, if you integrate VMP with ECS and set the `OnlyIncludeSubNamespaces parameter to ["GPU"]`, only GPU\-related metrics of ECS instances will be collected. To query the sub\-namespaces of cloud services, see [Cloud service metric query](https://console.byteplus.com/cloud_monitor/docs). |
|ExcludeSubNamespaces |Filter collection metrics by cloud service sub\-namespace and exclude the metrics of the specified sub\-namespace.<br><br>**For example**, if you integrate VMP with ECS and set the `OnlyIncludeSubNamespaces parameter to ["GPU"]`, it indicates that all metrics except for GPU\-related metrics for ECS instances will be collected. To query the sub\-namespaces of cloud services, see [Cloud service metric query](https://console.byteplus.com/cloud_monitor/docs). |
|OnlyIncludeMetrics |Configure the metrics that only need to be collected. `<sub-namespace>` indicates the subnamespace of the cloud service. To query the metrics of cloud services, see [Cloud service metric query](https://console.byteplus.com/cloud_monitor/docs).<br><br>**For example**, if you integrate VMP with ECS and configure the following code, it indicates that only CPU metrics with the sub\-namespace being `instance` and GPU metrics with the sub\-namespace being `GPU` will be collected.<br><br>```YAML```<br>```OnlyIncludeMetrics:```<br>```  Instance: ["CpuSystem","CPUUser","CpuOther"]```<br>```  GPU: ["GpuMemoryUsedSpace","GpuUsedUtilization"]```<br> |
|ExcludeMetrics |Configure metrics to be excluded. `<sub-namespace>` indicates the sub\-namespace of the cloud service. To query the metrics of cloud services, see [Cloud service metric query](https://console.byteplus.com/cloud_monitor/docs).<br><br>**For example**, if you integrate VMP with ECS and configure the following code, it indicates that CPU metrics with the sub\-namespace being `instance` and GPU metrics with the sub\-namespace being `GPU` will not be collected. All other metrics are collected.<br><br>```YAML```<br>```ExcludeMetrics:```<br>```  Instance: ["CpuSystem","CPUUser","CpuOther"]```<br>```  GPU: ["GpuMemoryUsedSpace","GpuUsedUtilization"]```<br> |
|OnlyIncludeInstances |Filter collection objects by cloud service instance ID and collect only the metrics of the specified instances.<br><br>**For example**, if you integrate VMP with ECS and set the `OnlyIncludeInstances parameter to ["i-ye3dvuypkws6ip***"]`, only the metrics of the specified ECS instance will be collected. |
|ExcludeInstances |Filter collection objects by cloud service instance ID and exclude the metrics of the specified instances.<br><br>**For example**, if you integrate VMP with ECS and set the `OnlyIncludeInstances parameter to ["i-ye3dvuypkws6ip***"]`, the metrics of the specified ECS instance will not be collected. |


<span id=".55uR5o6n5L-h5oGv"></span>
## Monitoring information

<span id=".5p-l6K-i5LqR5Lqn5ZOB5oyH5qCH"></span>
### Query cloud service metrics


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).  the 

2. In the top navigation bar, select the target region.

3. Click **Explore** in the left navigation bar to go to the Explore page.

4. Specify the **Workspace** parameter for which you want to query metrics in the upper\-right corner of the page, and enter a metric name, such as `CPUUser_Instance_VCM_ECS` of Cloud Monitor, in the **Query** field to check whether the corresponding metric can be queried as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f70eb15e2c12c655a561854228ceeea.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The metric names exported from Cloud Monitor are in the format of <code>MetricName_SubNamespace_Namespace</code>, such as <code>CPUUser_Instance_VCM_ECS</code>. For more details on the metrics of different cloud services, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics">Cloud service metrics</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use the <code>ResourceID</code> parameter for fine\-grained resource filtering and view the monitoring data of specific resources.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to use Grafana to build monitoring dashboards, you can integrate data from VMP into your own Grafana. For more details, see <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana in a VKE cluster and integrating Grafana with a workspace</a>.   </div>
   


<span id=".5p-l6K-i5LqR5Lqn5ZOB5a6e5L6L5YWD5L-h5oGv"></span>
### Query the metadata of cloud service instances

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can export the metadata of some cloud services, and the metadata fields vary based on different cloud services. For more details, see the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Feature_overview">documentation of Cloud Monitor</a>.</div>


* When you set the **Label export method** parameter to **Append to original metric**, you can view the original metrics of the cloud service on the **Explorer** page. The query result includes the metadata labels of the cloud service. In the following figure, you can view the metadata labels such as ProjectName, Name, Status, and AvailableZone in the original metric of ECS `CPUUser_Instance_VCM_ECS`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4030f83f765acd787b42d7713e417243.png) </span>

* When you set the **Label export method** parameter to **Add as independent metric**, you can view the metadata of cloud service instances by using the `volc_resource_info` metric.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b7e271f08e28511db517c9898d31700.png) </span>

   The following example shows how to use join operations to query the returned metadata of specific cloud service instances.

   ```Plain Text
   {Cloud Product Metrics} * on(ResourceID) group_left({Metadata Tags}) avg(volc_resource_info) by (ResourceID,{Metadata Tags})
   ```
   

   The following section shows an example.

   ```Plain Text
   CPUUser_Instance_VCM_ECS * on(ResourceID) group_left(Name,ProjectName) avg(volc_resource_info) by (ResourceID,Name,ProjectName)
   ```
   

   The following figure shows the expected result, in which you can view the metadata details returned by different cloud service instances.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_88983dacb22fb04461ab108536c7f9a7.png) </span>

* When you use the **instance export label key** feature to export the resource labels of cloud service instances, the system will automatically add the `tag_` prefix before the labels. For example, if the resource label is `ecs-label`, the exported metric label will be `tag_ecs_label`.


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

<span id=".5pCt5bu65LqR5Lqn5ZOB55uR5o6n5aSn55uY"></span>
### 

<span id="Y58TutH0"></span>
### Build a cloud service monitoring dashboard

You can build Grafana in a VKE cluster or an ECS instance, import the monitoring dashboard template that is obtained when you configure the integration task, and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id=".6YWN572u5LqR5Lqn5ZOB5ZGK6K2m"></span>
### Configure cloud service alerts

You can configure alerts in the alerting center of VMP. For more details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
