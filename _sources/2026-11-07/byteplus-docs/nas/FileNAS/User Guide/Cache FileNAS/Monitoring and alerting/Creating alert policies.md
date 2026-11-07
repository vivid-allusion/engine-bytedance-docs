---
title: "Creating alert policies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating_alarm_strategies"
---

Cache FileNAS supports alert functions. You can configure alert policies for key file system metrics based on business requirements to monitor resource usage and mitigate potential risks. This topic explains how to create an alert policy.

<span id="75a7934c"></span>
## Background information

BytePlus offers real\-time monitoring and alerts by integrating Cloud Monitor with FileNAS. Once you set an alert policy in Cloud Monitor, it will send alerts to contacts when the relevant file system's resource usage meets the trigger conditions. These alerts can help you manage your file systems more effectively. For more information, see [What is Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor).

<span id="98d8d99c"></span>
## Monitoring metrics

You can set alerts for the following Cache FileNAS\-related metrics, such as capacity utilization and NFSv4 write latency.


|**Dimension** |**Metric name** |**Description** |
|---|---|---|
|Capacity |Used capacity (MiB) |The capacity used in the file system. |
||Capacity Util (%) |The capacity utilization of the file system. The calculation formula is:<br><br>Capacity utilization = Used capacity / Total capacity of the file system. |
||Inode Util (%) |The inode (file count) usage of the file system. The calculation formula is:<br><br>Inode usage = Current file count / File count limit of the file system (default: 1 billion)<br><br>The current file count includes ordinary files and subdirectories within a directory. |
|Latency |NFSv4 read latency (μs) |The time delay between the file system receiving a request and successfully returning read data to the client via the NFSv4 protocol. |
||NFSv4 write latency (μs) |The time delay between the file system receiving a request and successfully writing data via the NFSv4 protocol. |
||NFSv3 read latency (μs) |The time delay between the file system receiving a request and successfully returning read data to the client via the NFSv3 protocol. |
||NFSv3 write latency (μs) |The time delay between the file system receiving a request and successfully writing data via the NFSv3 protocol. |
||NFS meta latency (μs) |The time delay between the file system receiving a request and completing metadata operations via the NFS protocol. |
||SMB meta latency (μs) |The time delay between the file system receiving a request and completing metadata operations via the SMB protocol. |
||SMB write latency (μs) |The time delay between the file system receiving a request and successfully writing data via the SMB protocol. |
||SMB read latency (μs) |The time delay between the file system receiving a request and successfully returning read data to the client via the SMB protocol. |
||DataFlow on\-demand loading latency (μs) |The time delay between when the client issues a request and when the file system returns the data in on\-demand loading mode. |
|Quota |Directory quota capacity Util (%) |The capacity utilization of the directory quota. The calculation formula is:<br><br>Directory quota capacity utilization = Used capacity / Capacity limit of the directory<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This metric is specific to restricted directory quotas. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/Managing_directory_quotas#ec5b9ecb">Restricted directory quota</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Log in to the <a href="https://console.byteplus.com/filenas/">FileNAS console</a>, click the target file system on the <strong>File System list</strong> page. Go to the <strong>Directory quota</strong> tab, and click <strong>Quota management</strong> in the <strong>Actions</strong> column for the target directory quota to view used capacity and capacity limit of that directory quota.</div><br> |
||Directory quota Inode Util (%) |The inode (file count) usage of the directory quota. The calculation formula is:<br><br>Directory quota inode usage = Current file count / File count limit of the directory<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This metric is specific to restricted directory quotas. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/Managing_directory_quotas#ec5b9ecb">Restricted directory quota</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Log in to the <a href="https://console.byteplus.com/filenas/">FileNAS console</a>, click the target file system on the <strong>File System list</strong> page. Go to the <strong>Directory quota</strong> tab, and click <strong>Quota management</strong> in the <strong>Actions</strong> column for the target directory quota to view current file count and file count limit of that directory quota.</div><br> |
|IOPS |NFSv4 read IOPS (Count/s) |The number of read requests that the file system handles per second via the NFSv4 protocol. |
||NFSv4 write IOPS (Count/s) |The number of write requests that the file system handles per second via the NFSv4 protocol. |
||NFSv3 read IOPS (Count/s) |The number of read requests that the file system handles per second via the NFSv3 protocol. |
||NFSv3 write IOPS (Count/s) |The number of write requests that the file system handles per second via the NFSv3 protocol. |
|QPS |NFS meta QPS |The number of metadata operations that the file system completes per second via the NFS protocol. |
||DataFlow import QPS (Count/s) |The number of files imported to the file system per second during DataFlow tasks. |
||DataFlow export QPS (Count/s) |The number of files exported from the file system per second during DataFlow tasks. |
||DataFlow evict QPS (Count/s) |The number of files evicted from the file system per second during DataFlow tasks. |
|Bandwidth |NFSv4 read bandwidth (B/s) |The amount of data that the file system reads and returns to the client per second via the NFSv4 protocol. |
||NFSv4 write bandwidth (B/s) |The amount of data that the client writes to the file system per second via the NFSv4 protocol. |
||NFSv3 read bandwidth (B/s) |The amount of data that the file system reads and returns to the client per second via the NFSv3 protocol. |
||NFSv3 write bandwidth (B/s) |The amount of data that the client writes to the file system per second via the NFSv3 protocol. |
||Dataflow import bandwidth (B/s) |The total number of bytes imported to the file system per second during DataFlow tasks. |
||DataFlow export bandwidth (B/s) |The total number of bytes exported from the file system per second during DataFlow tasks. |
||DataFlow on\-demand data loading bandwidth (B/s) |The amount of data transferred per second when accessing the file system in on\-demand loading mode. |
|Access point |Read IOPS (Count/s) |The number of read I/O operations completed per second. |
||Read bandwidth (B/s) |The total number of bytes read per second. |
||Read latency (μs) |The average time it takes to complete a read request. |
||Write IOPS (Count/s) |The number of write I/O operations completed per second. |
||Write bandwidth (B/s) |The total number of bytes written per second. |
||Write latency (μs) |The average time it takes to complete a write request. |


<span id="26e4e08a"></span>
## Steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section describes the steps to create an alert policy in the FileNAS console. Alternatively, you can log in to the <a href="https://console.byteplus.com/cloud-monitor/">Cloud Monitor console</a> to set up alert policies. For instructions, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.</div>



1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the file system you want to manage.

5. On the file system details page, click the **Monitoring alarm** tab.

6. Under the **Monitoring alarm** tab, click **Create an alert policy** at the top right corner.

7. On the **Create alert policy** page, configure the following parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This section outlines the key parameters for creating alert policies. For more information on additional parameters, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.   </div>
   

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |Basic information |Name |Enter a name for your alert policy. |
   ||Description |Provide additional information for your alert policy. |
   |Alert object |Resource type |Select **Storage** \> **Cache FileNAS**. |
   ||Dimension |The options include **Capacity**, **Latency**, and **Quota**. |
   ||Selection method |Methods for selecting resources include:<br><br><br>* **Manually select**: Select resources manually.<br><br>* **Resource name**: Find resources by resource name.<br><br>* **Object group**: Find resources by object group. For more information, see [Creating a resource group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group). |
   ||Region |If you select **Manually select** or **Resource name** for **Selection method**, specify the region where the file system resides. |
   ||Resources |If you select **Manually select** for **Selection method**, specify the file system(s) for which you want to configure alerts. Options:<br><br><br>* **All**: The alert policy applies to all file systems in the specified region under the current account.<br><br>* **Partial**: Manually select one or more resources. |
   ||Resource name |If you select **Resource name** for **Selection method**, specify the file system(s) for which you want to configure alerts. Options:<br><br><br>* **All resources**: The alert policy applies to all file systems in the specified region under the current account.<br><br>* **Partial resources**: The alert policy only applies to file systems that meet the specified conditions. |
   ||Object group |If you select **Object group** for **Selection method**, select an existing object group. |
   |Alert rules |Preset trigger condition |Currently, there are no preset trigger conditions available for Cache FileNAS file systems. |
   ||Metric type |**Single\-metric** or **Multi\-metric**. Select multiple metrics to monitor various resource metrics. |
   ||Trigger condition |Set the logic, duration cycles, and monitoring metrics for alerts. When a monitoring metric meets the trigger conditions, the system will send an alert. For more information, see [Monitoring metrics](https://docs.byteplus.com/en/docs/nas/Creating_alarm_strategies#98d8d99c). |
   ||Notification cycle |To prevent alert fatigue, the system temporarily mutes notifications for a set time when a monitored resource triggers repeated alerts. |
   ||Notification aggregation policy |Specify the rules for delivering alerts. Options:<br><br><br>* **Rule**: If a resource specified in an alert rule triggers repeated alerts during the delivery period, only one alert will be sent.<br><br>* **Rule and Resource**: If multiple resources specified in an alert rule trigger repeated alerts during the delivery period, alerts are sent separately for each resource. If the monitoring metric does not return to normal after the alert is sent, Cloud Monitor will send another alert. |
   ||Alert recovery notification |A recovery notification will be sent once the monitoring metric returns to normal. This option is enabled by default. |
   ||NoData alert |A no\-data alert will be triggered if the specified resource reports no data for n consecutive cycles. This alert is turned off by default. |
   |Advanced settings |Project |Set the project for your alert policy. |
   ||Tag |Click **Add tag** to add a tag to your alert policy. |
   |Alert method |Notification method |Select how you would like to receive alerts. Options:<br><br><br>* **Notification policy**: Select an existing notification policy. For more information, see [Creating a notification policy](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy).<br><br>* **Manually select**: Select one or more alert channels for your alert policy. |
   ||Alert channel |If you select **Manually select** for **Notification method**, choose one or more channels. The options include **Email**, **Phone**, **SMS, Alert callback**, and **Orchestration**. |
   ||Alert contact group |If you set **Alert channel** to **Email**, **Phone**, or **SMS**, select an alert contact group to receive alerts. For steps on creating an alert contact group, see [Creating contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group). |
   ||Webhook |If you select **Alert callback** for **Alert channel**, enter a callback URL. For more information, see [Alarm callback usage notes](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions). |
   ||Orchestration plan |If you select **Orchestration** for **Alert channel**, select an orchestration plan. |
   ||Effective period |Set the effective time period for the alert policy. The alert policy only monitors resource data for trigger conditions during the effective time period. |
   

8. After completing the settings, click **Create**.

   After creating an alert policy, you can view and manage it on the **Alert policy** page in Cloud Monitor.
