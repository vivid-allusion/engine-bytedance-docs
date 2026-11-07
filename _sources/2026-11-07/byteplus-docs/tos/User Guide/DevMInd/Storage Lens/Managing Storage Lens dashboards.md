---
title: "Managing Storage Lens dashboards"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Managing-Storage-Lens-dashboards"
---

This topic explains how to manage Storage Lens dashboards, including how to create and view a dashboard.

<span id="33FK7nri"></span>
## Prerequisites

You have enabled and authorized access to Cloudlens for TOS on the **Log analysis/Storage Lens** page.

<span id="ZVefgVLs"></span>
## Managing Storage Lens dashboards


<Tabs>
<Tab zoneid="JSt4E3HK9E" title="Create a Storage Lens dashboard">
<TabTitle>Create a Storage Lens dashboard</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the DevMind page, click **Storage Lens** in the left navigation pane.

4. On the **pivot dashboard** page, click **Create pivot dashboard** and configure the following parameters.

   
   |Section |Parameter |Description |
   |---|---|---|
   |Basic configuration |Kanban name |Enter a name for the dashboard. It cannot exceed 65 characters and must be unique across all dashboards. Once you create a dashboard, you cannot change its name. |
   ||Region |Select the region to which the dashboard metrics will be exported. Once you create a dashboard, you cannot change its region. |
   |Metric collection method |Metric collection method |Select what metrics you want the dashboard to collect. The retention period for this data is 15 months. The options are:<br><br><br>* **Free metrics**: This option collects basic metrics, such as storage usage and object count, and applies to all regions and buckets.<br><br>* **Advanced features**: In addition to basic metrics, this option collects activity metrics and supports data aggregation by prefix. However, it is only available for certain regions and buckets.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Advanced features are not currently supported.   </div><br>    |
   ||Filter metrics |This section displays the metrics that correspond to the collection methods you select, including:<br><br><br>* **Activity metrics**: Bytes uploaded and number of deleted bytes.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Activity metrics are only available when the <strong>advanced features</strong> option is selected.   </div><br>   <br><br>* **Summary metrics**: Total storage and total number of objects.<br><br>* **Cost optimization metrics**: Historical version bytes, number of historical version objects, number of unmerged multipart uploads bytes, and number of unmerged multipart uploads objects.<br><br>* **Data protection metrics**: Current version bytes and number of current version objects. |
   ||Prefix aggregation |This option is only available when **advanced features** is selected under **Metric collection method**.<br><br>Select this option to display storage metrics by prefix. This allows you to analyze storage usage by prefix. This option is disabled by default. |
   ||Prefix range |This option is only available when **advanced features** is selected under **Metric collection method** and **Prefix aggregation** is enabled.<br><br>Select this option to display metrics, such as total storage and object count, by prefix. Specifically:<br><br><br>* **Prefix Threshold (%)** : Select this option to aggregate prefixes that account for a certain percentage or more of the total storage usage.<br><br>   * **Prefix threshold**: The minimum prefix threshold size, which supports any integer ranging from 1 to 100. For example, a **prefix threshold** of 5 percent means that prefixes accounting for 5 percent or more of the bucket's total storage usage will be analyzed.<br><br>   * **Prefix depth**: The maximum number of levels up to which the prefixes are evaluated, which supports any integer ranging from 1 to 10. For example, a **prefix depth** of 2 indicates that statistics will be displayed and collected based on a two\-level directory structure.<br><br>   * **Prefix separator**: Enter the prefix delimiter character. You can use either a forward slash (/) or a custom delimiter. Custom delimiters support only a single character.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">FNS buckets support both forward slashes (/) and custom delimiters, while HNS buckets only support forward slashes (/) and do not support custom delimiters.      </div><br>      <br><br>* **Specify prefix**: Enter the prefix(es) that you would like the dashboard to evaluate.<br><br>   * You can specify up to 50 prefixes at once.<br><br>   * Only enter the prefix, not the bucket name. For example, to specify the "test" prefix in the "aaa" bucket, enter only "test".<br><br>   * Prefixes can contain Chinese characters, letters, numbers, and common symbols. Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed. |
   |Filter Bucket |Regions and buckets |Configure the dashboard scope. The options are:<br><br><br>* **Include regions and buckets**: Choose the region(s) and bucket(s) you want the dashboard to include.<br><br>* **Exclude regions and buckets**: Choose the region(s) and bucket(s) you want the dashboard to exclude. |
   ||Region |If you select **Include regions and buckets**, regions and buckets are linked. When a region is specified, only buckets within that region can be selected.<br><br>If you select **Exclude regions and buckets**, regions and buckets are independent of each other. When a region is specified, buckets both within and outside that region can be selected. The dashboard scope is based on the combined set of the selected regions and buckets. |
   ||Bucket |Select the bucket(s) that you want to include or exclude. |
   |Export metrics |Export metrics |Select whether to **export metrics**: If you select this option, TOS will automatically export dashboard data to a specified bucket daily. You can then use your own tools to perform statistical analyses on the exported data.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The first time you choose to <strong>export metrics</strong>, you must follow the instructions on the page to grant TOS read and write permissions to the target bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the target bucket has server\-side encryption enabled, you must also grant TOS access to Key Management Service.</div><br> |
   ||Output format |Select output format of your metrics export, either **CSV** or **Parquet**. |
   ||Target bucket |Select the bucket for exporting the metrics. The region of the bucket is determined by the region of the dashboard. To avoid metric data leakage, we recommend selecting a non\-public read/write bucket. |
   ||Metric prefix |Specify the prefix for storing the metrics export. For example, if you set the prefix to `datalens/`, your metrics export will be stored in the `datalens/` directory of the specified bucket. Follow these guidelines when specifying a prefix:<br><br><br>* Prefixes can contain Chinese characters, letters, numbers, and common symbols.<br><br>* Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed. |
   

5. Click **Create pivot dashboard**.


</Tab>
<Tab zoneid="ISKEY05nkp" title="View a Storage Lens dashboard">
<TabTitle>View a Storage Lens dashboard</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Data is aggregated daily by account, region, bucket, and other dimensions. This information is intended for monitoring purposes only and should not be used for metering references.</div>


* <div data-tips="true" data-tips-type="tip">Only dashboards with <strong>advanced features</strong> enabled can display metrics by prefix.</div>


* <div data-tips="true" data-tips-type="tip">Storage Lens dashboards cannot display metrics for the current day.</div>


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the DevMind page, click **Storage Lens** in the left navigation pane.

4. On the **pivot dashboard** page, click the dashboard you want to check.

5. On the dashboard details page, set the filter conditions. These include **Region**, **Storage Class**, **Bucket, Prefix**, and **Date**. Multiple selections are supported.

   The dashboard will then display only metrics that meet the selected filter conditions.


</Tab>
<Tab zoneid="v6AwUauwik" title="Export metrics">
<TabTitle>Export metrics</TabTitle>

<span id="aph5WJIB"></span>
### Manual export


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, click **Storage Lens** in the left navigation pane.

4. On the **pivot dashboard** page, click the dashboard you want to check.

5. On the **Overview** tab, in the **Trends and Distributions** section, select a time range and click the download icon.

6. In the **Metrics export** dialog box, select the metrics you want to export, such as **Total storage**, **Upload Volume**, and **amount deleted**. Then, click **OK**.


<span id="8yQ8HraH"></span>
### Automatic export


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, click **Storage Lens** in the left navigation pane.

4. On the **pivot dashboard** page, click **Edit** in the **Actions** column of the dashboard you want to manage.

5. On the **Edit pivot dashboard** page, configure the parameters in the **Export metrics** section. For more information about the parameters, see Create a Storage Lens dashboard.

6. Once you have finished configuring, click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, enable <strong>Metrics export</strong> when creating a Storage Lens dashboard. For instructions, see <a href="https://docs.byteplus.com/docs/tos/Creating-storage-lens-dashboards">Creating Storage Lens dashboards</a>.   </div>
   


</Tab>
</Tabs>


<span id="jznrrfdc"></span>
## Other operations

On the **pivot dashboard** page, you can also perform the following operations on a dashboard.


|Operation |Description |
|---|---|
|View configuration |To view the configuration of a dashboard, click **View configuration** in the **Actions** column. |
|Edit |To edit a dashboard's configuration, click **Edit** in the **Actions** column. Note that you cannot change the **Kanban name** or **region**. |
|Delete |To delete a dashboard, click **Delete** in the **Actions** column. In the box that appears, confirm the deletion by clicking **Delete**. After you delete a dashboard:<br><br><br>* Immediate impact after deletion:<br><br>   * The dashboard will be removed from the dashboard list.<br><br>   * You will no longer be able to view the dashboard's daily metrics.<br><br>* Constraints for viewing historical data **:** <br><br>   * You can view the historical data of the deleted dashboard in the corresponding TLS topic if there are other dashboards in the same region. The historical data retention period is 15 months.<br><br>   * If there are no other dashboards in the same region, however, the associated TLS topic will be cleared, and the metric data will no longer be retained. |
|Search |To search for a dashboard, type its name or ID into the search box at the top of the page. |


&nbsp;

&nbsp;

<span id="AGCZtfKu"></span>
### 

&nbsp;
