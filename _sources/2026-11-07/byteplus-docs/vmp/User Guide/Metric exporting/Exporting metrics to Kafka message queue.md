---
title: "Exporting metrics to Kafka message queue"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating_an_export_task"
---

You can export data from a Vital Managed Service for Prometheus (VMP) workspace to a Kafka instance to use message queues for consumption. This topic describes how to export data from a workspace.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[Public beta]: This feature is currently in public beta.</div>


<span id="5e81pM29"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Message Queue for Kafka has been activated, and a Kafka instance and topic have been created in the region where the current workspace is located. For more details, see [Creating instances](https://docs.byteplus.com/en/docs/kafka/creating-instance) and [Creating topics](https://docs.byteplus.com/en/docs/kafka/creating-topic).


<span id="sPIzkeqA"></span>
## Limits

Only paid metrics can be exported. Free metrics (basic metrics stored for 15 days) are not supported for export. For more information, see [Billing Items](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

<span id="sPIzkeqA"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Export task**. On the page that appears, click **Create export tasks**.

4. Configure the task details and then click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |Task name |Specify the name of the export task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
   |workspace |Select the workspace for which you want to export data. Only a common workspace can be selected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Workspaces with a storage duration of 15 days or less support exporting only custom and other metrics, but not basic metrics. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Metrics-Reference">Metric references</a>.</div><br> |
   |Project |The project to which the export task belongs. Project management is a resource management method that allows you to manage cloud resources in groups based on different businesses or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
   |Tags |Labels are key\-value pairs attached to export tasks to identify them. They can be used with selectors to quickly filter target export tasks. A tag is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use tags for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
   |data filtering |Filter metrics in the workspace by using metric labels, such as `job="prometheus"` or `__name__=~"job:.*"`. Regular expressions are supported. You can configure both **AND** rules and **OR** rules.<br><br><br>* **AND** rule: Metrics will be delivered only if they contain all specified labels.<br><br>* **OR** rule: Metrics will be delivered if they contain one of the specified labels.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must configure at least one data filtering rule.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After configuring the filter rules, click <strong>Query Test</strong> in the upper\-right corner to check the configuration results. If a configuration error occurs or no data can be queried, an error message will be provided.</div><br> |
   |Data query offset |Set the backward offset from the export timestamp to define the time range for raw metric queries. The offset can be accurate down to minutes and seconds. When exporting metrics from the workspace, the system queries the latest sample every minute based on the configured offset. If you encounter high data latency, we recommend increasing this query offset. |
   |Export target |Configure the destination for workspace data delivery. In this topic, **Kafka message queue** is selected as the destination. |
   |Kafka instance |Select the created Message Queue for Kafka instance. |
   |Kafka Topic |Select the created Topic of the Kafka instance. |
   |Metric Relabel configuration |Configure metric relabeling. You can add labels to delivered metrics. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   


<span id="monfx7vP"></span>
## Validate results

<span id="lisS9udf"></span>
### View the export task

After the configuration is complete, you can view the status and details of the task. Check whether the export task runs as expected.


1. In the left navigation bar, click **Export task**. You can view the status of the task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c32180bc26e3748d5a2a97c58a37659.png) </span>

After the export task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page, where you can view the details of the task.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the task.


<span id="iMUbfMIa"></span>
### Check exported data

After the data of the VMP workspace is delivered to the Kafka instance, you can view the corresponding data in the Message Queue for Kafka console.


1. Log in to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. Click **Instances** in the left navigation bar. On the new page, find the target instance in the instance list.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e1d0c153f7b07968476f36b5426b749.png) </span>

3. Click the instance name to go to the instance details page. Click the **Message query** tab and specify the **Topic**, **Partition**, and **Offset** parameters to query the data delivered from the VMP workspace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8da8ba731426ebb87010729f91b358c6.png) </span>


<span id="fmORG8HO"></span>
## What to do next

On the export task details page, switch to the **Monitoring dashboard** tab and view the dashboards for both the raw metrics and exports to Message Queue for Kafka. Here:


* The dashboard for raw metrics displays three metrics: the scrape QPS, the average number of raw metric samples pulled per second, and the average time consumed to pull raw metrics.

* The dashboard for exports to Message Queue for Kafka displays two metrics: the number of successful export tasks and the number of failed export tasks.
