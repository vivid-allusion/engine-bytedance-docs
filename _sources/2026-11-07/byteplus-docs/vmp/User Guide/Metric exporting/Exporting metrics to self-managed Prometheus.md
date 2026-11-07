---
title: "Exporting metrics to self-managed Prometheus"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_self-managed_Prometheus"
---

Vital Managed Service for Prometheus (VMP) workspaces allow you to export data to self\-managed Prometheus. This topic describes how to export data from a workspace.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[Public beta]: This feature is currently in public beta.</div>


<span id="KLnRehKV"></span>
## Prerequisites


* A VMP workspace has been created. For more details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* A self\-managed Prometheus has been deployed in a public or private network environment, and the remote write URL and the authentication method of the self\-managed Prometheus have been obtained.


<span id="oSqKlvpW"></span>
## Limits

Only paid metrics can be exported. Free metrics (basic metrics stored for 15 days) are not supported for export. For more information, see [Billing Items](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

<span id="gQbwPEWl"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Export tasks**. On the page that appears, click **Create export tasks**.

4. Configure the task details and then click  ** Confirm**.

   
   |Parameter |Descriptions |
   |---|---|
   |Task name |Specify the name of the export task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
   |workspace |Select the workspace for which you want to export data. Only a common workspace can be selected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Workspaces with a storage duration of 15 days or less support exporting only custom and other metrics, but not basic metrics. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Metrics-Reference">Metric references</a>.</div><br> |
   |Project |The project to which the export task belongs. Project management is a resource management method that allows you to manage cloud resources in groups based on different businesses or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, while streamlining expense allocation and auditing for diverse cloud resources.  |
   |Tags |Labels are key\-value pairs attached to export tasks to identify them. They can be used with selectors to quickly filter target export tasks. A label is a key\-value pair that allows you to classify and aggregate cloud resources from different dimensions. You can use labels for resource authorization and bill splitting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can add up to 50 labels.</div><br> |
   |Data filtering |Filter metrics in the workspace by using metric labels, such as `job="prometheus"` or `__name__=~"job:.*"`. Regular expressions are supported. You can configure both **AND** rules and **OR** rules.<br><br><br>* **AND** rule: Metrics will be delivered only if they contain all specified labels.<br><br>* **OR** rule: Metrics will be delivered if they contain one of the specified labels.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must configure at least one data filtering rule.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After configuring the filter rules, click <strong>Query Test</strong> in the upper\-right corner to check the configuration results. If a configuration error exists or no data can be queried, an error message will be provided.</div><br> |
   |Data query offset |Set the backward offset from the export timestamp to define the time range for raw metric queries. The offset can be accurate down to minutes and seconds. When exporting metrics from the workspace, the system pulls the latest sample per the offset every minute. If you encounter high data latency, we recommend increasing this query offset. |
   |Export target |Select the target to which workspace data is delivered. In this topic, select **Self\-built Prometheus**. |
   |Network access method |Select the access method of self\-managed Prometheus. Valid values: **Public network access** and **Private network access**.<br><br><br>* If you select **Public network access**, you need to specify the **Address** parameter, which is the public remote write URL of your self\-managed Prometheus.<br><br>* If you select **Private network access**, you need to specify the following parameters:<br><br>   * **Virtual Private Cloud**: Select the Virtual Private Cloud (VPC) where the self\-hosted Prometheus is located.<br><br>   * **Subnet**: Select the subnet where the self\-built Prometheus is located.<br><br>   * **Address**: Specify the private remote write URL of the self\-hosted Prometheus. |
   |Authentication method |Select an authentication method for self\-hosted Prometheus. Available options include:<br><br><br>* **Basic auth**: Basic Auth is used for authentication. When you select this authentication method, you need to configure the username and password for the self\-managed Prometheus.<br><br>* **Bearer token**: **Bearer token** is used for authentication. When you select this authentication method, you need to configure an encrypted token value.<br><br>* **No authentication**: Do not use any authentication method. Access to the self\-managed Prometheus instance is anonymous. This option applies to internal secure networks where other network policies have implemented access control. |
   |Custom HTTP Header configuration |Configure custom HTTP headers. The HTTP header is in the format of header and value. The header can contain Chinese characters, letters, and special characters and must be 1 to 200 characters in length. |
   |Metric Relabel configuration |Configure metric relabeling. You can add labels to delivered metrics. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   


<span id="JS9SaogM"></span>
## Verifying results

<span id="XIQwlBUo"></span>
### View the export task

After the configuration is complete, you can view the status and details of the task. Check whether the export task runs as expected.


1. In the left navigation bar, click **Export tasks**. You can view the status of the task in the task list. When the task is in the **Running** state, it indicates that the export task works as expected.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can filter export tasks by <strong>workspace</strong> or <strong>name</strong> in the export task list to quickly find the corresponding export tasks.   </div>
   

2. After the export task is created, you can perform the following operation and maintenance operations:

   * Click the **name of the task** to go to the task details page, where you can view the details of the task.

   * Click **Edit** in the **Actions** column to edit the task.

   * Click **Suspend task** in the **Actions** column to suspend the task.

   * Click **Delete** in the **Actions** column to delete the task.


<span id="1pyGN726"></span>
### Check exported data

After you use the export task to deliver the data of a VMP workspace to the self\-managed Prometheus instance, you can view the corresponding data on the self\-managed Prometheus instance.

<span id="EgnMxpBP"></span>
## What to do next

On the export task details page, switch to the **Monitoring dashboard** tab and view the dashboards for both the raw metrics and exports to the target Prometheus instance. Here:


* The dashboard for raw metrics displays three metrics: the scrape QPS, the average number of raw metric samples pulled per second, and the average time consumed to pull raw metrics.

* The dashboard for exports to the target Prometheus instance displays three metrics: the number of requests for exporting data to the external Prometheus instance, the volume of data exported, and the latency of the export tasks.
