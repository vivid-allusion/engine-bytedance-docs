---
title: "GPU/RDMA millisecond-level monitoring integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/GPU_RDMA-millisecond-level-monitoring-integration"
---

VMP can be integrated with High Performance Computing Optimized ECS instances to provide millisecond\-level GPU/RDMA monitoring. This meets your business requirements for centralized monitoring of cloud GPU/RDMA resources and custom businesses. This topic describes the procedure for integrating GPU/RDMA millisecond\-level monitoring.

<span id="xYwckVug"></span>
## Background

Built on the GPU instance type, the High Performance Computing Optimized instance type integrates RDMA networks. This significantly improves network performance and increases acceleration ratios for large\-scale clusters. This instance type applies to scenarios such as high\-performance computing, AI, and machine learning. 

<span id="Bjgh7qhy"></span>
## Prerequisites


* The VMP service has been activated, and a VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The ECS service has been activated, and a High Performance Computing Optimized ECS instance has been created. For more details, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

* Cloud assistant Agent and the O11yAgent collection add\-on have been installed on the ECS instance. For more details, see [Installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) and [Installing the O11yAgent collection add-on by using the GUI](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console).

* A security group has been configured for the ECS instance. For more details, see [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

   * A security group has been created for the managed collector, and the subnet and port of the ECS instance have been allowed in the **outbound rule**.

   * Configure the security group to which the ECS belongs, and allow the security group used by the managed collector to access the corresponding port in the **inbound rule**.

* The VMP workspace and the target ECS instance must be deployed in the same region.


<span id="LnnRzD1C"></span>
## Procedure

<span id="7k5aU1jb"></span>
### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Access center \> Component**. On the page that appears, click **GPU/RDMA millisecond\-level Monitoring**.

4. (Optional) Service authorization.

   1. When you configure an ECS integration task for the first time, you need to grant permissions to allow VMP to access ECS and VPC. Click **Authorize** to configure service authorization.

   2. Click **Authorize Now** to authorize VMP to access other services.

5. Configure the collector deployment environment. Click **ECS environment** and select the associated ECS instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In this scenario, only High Performance Computing Optimized ECS instances that have cloud assistant Agent installed and are not associated with other GPU/RDMA millisecond\-level monitoring integration tasks can be selected.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_889eee700da3d0b5641f3235110d0057.png) </span>


6. Click **Create access task**. On the **Start access** tab, configure the details of the integration task. After the configuration is complete, click **Confirm**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f8bacf785ef57338f08d3571c3cdb1a.png) </span>


|Category |Parameter |Description |
|---|---|---|
|Basic information |Task name |Specify the name of the integration task. |
||workspace |Select a created VMP workspace to associate with the integration task. |
||Project |The project to which the instance belongs. ‌A project is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
||Tags |Labels of the instance. A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
|Scrape configuration |Metric scraping interval |Specify the interval at which the metrics of RDMA and GPM are collected. The value can be accurate to milliseconds. The default value is 100ms. |
||Metric selection |Select the metrics you want to collect based on your business requirements. |


<span id="TDZR0PnC"></span>
### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="gaBgiDSO"></span>
## Validate results

After the configuration is complete, you can view the status and details of the task. Check whether the integration task is running as expected.


1. In the left navigation bar, click **Access center \> Access task**.

2. Click the **ECS environment** tab **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5593bd63e7ef12624c70b8f7c6fc5c92.png) </span>


3. Click the task name to go to the task details page, where you can view detailed information about the task, as well as the cloud assistant Agent status and collection status of the ECS instance.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fb6faf639ac59a6a1ee12912892d026.png) </span>
