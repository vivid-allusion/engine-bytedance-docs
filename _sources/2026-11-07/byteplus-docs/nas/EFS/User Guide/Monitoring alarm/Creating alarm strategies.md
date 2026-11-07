---
title: "Creating alarm strategies"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Creating_alarm_strategies"
---

EFS supports alert functions. You can configure alarm strategies for key file system metrics based on business requirements to monitor resource usage and mitigate potential risks. This topic explains how to create alarm strategies.

<span id="QwXtbtWr"></span>
## Background information

BytePlus offers real\-time monitoring and alerts by integrating Cloud Monitor with EFS. Once you set an alarm strategy in Cloud Monitor, it will send alerts to contacts when the relevant file system's resource usage meets the trigger conditions. These alerts can help you manage your file systems more effectively. For more information, see [What is Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor).

<span id="3sJZKQos"></span>
## Alarm metric description

You can set alerts for the following EFS\-related metrics, such as capacity utilization and NFSv4 write latency.


|**Subnamespace** |**Metric name** |**Description** |
|---|---|---|
|Capacity |Capacity utilization |The capacity utilization of a file system. The calculation formula is:<br><br>Capacity utilization = Used capacity / Total capacity of the target file system. |
||Inode utilization |The inode utilization for a file system is calculated using the following formula:<br><br>Inode utilization = Current file count (including regular files and subdirectories) / Default file limit (1 billion inodes) of the target file system.<br><br> |
|Latency |NFSv4 read latency |The time delay between the server receiving a request and successfully returning read data to the client in an NFSv4 file system. |
||NFSv4 write latency |The time delay between the server receiving a request and successfully writing data to an NFSv4 file system. |
||NFS meta latency |The time delay between the server receiving a request and completing metadata operations in an NFS file system. |
|Quota |Directory quota capacity utilization |Directory quota capacity utilization is calculated using the following formula:<br><br>Directory quota capacity utilization = Used capacity / Quota limit of the target directory<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The directory quota capacity utilization metric is only configurable for restricted directory quotas. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas#g8cS9Wsy">Enforcement directory quota</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Log in to the <a href="https://console.byteplus.com/efs">EFS console</a>, click the file system you want to check on the File System page. Go to the <strong>directory quota information</strong> tab to view used capacity and capacity limit of that directory quota.</div><br> |
||Directory quota Inode usage |Directory quota Inode usage is calculated using the following formula:<br><br>Directory quota Inode usage = Current file count / Quota limit of the target directory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The directory quota Inode usage metric is only configurable for restricted directory quotas. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas#g8cS9Wsy">Enforcement directory quota</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Log in to the <a href="https://console.byteplus.com/efs">EFS console</a>, click the file system you want to check on the File System page. Go to the <strong>directory quota information</strong> tab to view current file count and file count limit of that directory quota.</div><br> |


<span id="MA2UsXNk"></span>
## Steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section describes the steps to create an alarm strategy in the EFS console. Alternatively, you can log in to the <a href="https://console.byteplus.com/cloud-monitor/">Cloud Monitor console</a> to set up alarm strategies. For instructions, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.</div>



1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Monitoring alarm**.

6. On the **Monitoring alarm ** page, click **Create alert strategy** in the upper\-right corner.

7. Set the following parameters on the **Create alarm strategy** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This section outlines the key parameters for creating alarm strategies. For more information on additional parameters, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.   </div>
   

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Enter the name of the alarm strategy. |
      |Description |Describe the alarm strategy. |
      

   * **Alarm object**

      
      |**Parameter** |**Description** |
      |---|---|
      |Resource type |Select **Storage** \> **Elastic File Storage**. |
      |Subnamespace |Create alarm strategies based on **capacity**, **latency**, **Quota**, and other subnamespaces. |
      |Selection method |Methods for selecting resources include:<br><br><br>* **Manual selection**: Select resources manually.<br><br>* **Resource name**: Find resources by resource name.<br><br>* **Resource group**: Find resources by resource group. For more information, see [Creating a resource group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group). |
      |Resource name |When the **selection method** is set to **Resource name**, select the file system(s) for which you want to configure the alarm strategy. The options are explained below:<br><br><br>* **All resources**: The alarm strategy applies to all file systems in the specified region under the current account.<br><br>* **Specific resources**: The alarm strategy works for manually chosen file systems. |
      |Region |Select the region where the file system is located. |
      

   * **Alarm rules**

      
      |**Parameter** |**Description** |
      |---|---|
      |Metric type |**Single metric** or **Multiple metrics**. Select multiple metrics to monitor various resource metrics. |
      |Trigger condition |Set the monitored metrics, duration cycles, comparison logic, and alarm level for the alert. When the monitored resource metric meets the trigger conditions, the system will send an alert. For more information, see [Alarm metric description](https://docs.byteplus.com/en/docs/nas/efs_Creating_alarm_strategies#3sJZKQos).<br><br>For example, if the trigger condition is set to **average capacity utilization \> 60%, duration 60 cycles (1 cycle = 1 minute)** , the system checks resource metrics every minute. An alert triggers when the average capacity utilization of the file system exceeds 60% for 60 consecutive minutes. |
      |Mute for |To prevent alert fatigue, the system temporarily mutes notifications for a set time when a monitored resource triggers repeated alerts. |
      |Notify mode |Alert delivery strategies include:<br><br><br>* **Rule**: If a resource specified in an alarm rule triggers repeated alerts during the delivery period, only one alert will be sent.<br><br>* **Rule and resource**: If multiple resources specified in an alarm rule trigger repeated alerts during the delivery period, alerts are sent separately for each resource. If the monitored metric does not return to normal after the alert is sent, Cloud Monitor will send another alert. |
      |Alarm recovery notification |Users receive a recovery notification when the state of the alarm strategy returns to normal, and this alert is enabled by default. |
      

   * **Advanced Settings**

      
      |**Parameter** |**Description** |
      |---|---|
      |Project |Set the project for the alarm strategy. |
      

   * **Alarm way**

      
      |**Parameter** |**Description** |
      |---|---|
      |Alarm channel |Select one or more alarm channels, such as **Email**, **Telephone**, **SMS**, and **Webhook**. |
      |Alarm contact group |Choose the alarm contact group as the recipients of the alert. For steps on creating an alarm contact group, see [Creating contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <strong>Alarm contact group</strong> is only required if the <strong>Alarm channel</strong> is set to <strong>Email</strong>, <strong>Telephone</strong>, or <strong>SMS</strong>.</div><br> |
      |Webhook |Specify the webhook URL. For more information, see [Alarm callback usage notes](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Webhook</strong> URL is only required when the <strong>Webhook</strong> option is selected in <strong>Alarm channel</strong>.</div><br> |
      |Effective time |Set the effective time for the alarm strategy. The alarm strategy monitors resource data for trigger conditions only during the effective time. |
      

8. Click **Create**.
