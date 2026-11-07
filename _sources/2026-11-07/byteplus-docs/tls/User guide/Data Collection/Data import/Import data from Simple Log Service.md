---
title: "Import data from Simple Log Service"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Importing_data_from_sls"
---

BytePlus Torch Log Service (TLS) offers various cross\-service data migration solutions. It allows you to consume the log data collected within a specified time range and import structured log data from Simple Log Service (SLS) of Alibaba Cloud to BytePlus TLS.

<span id="背景信息"></span>
## Background

In scenarios such as cross\-service data migration, active/standby switchover, and log archiving, the log data collected from Alibaba Cloud SLS must be consumed and written into BytePlus TLS for query, analysis, consumption, or long\-term archiving. When importing logs from SLS, you use the consumption feature of consumer groups offered by SLS to enable BytePlus TLS to pull and consume log data from SLS, and call the PutLogs API action to upload the log data to BytePlus TLS. Then, data in the specified SLS Logstore is written into the specified TLS topic. When configuring an import task, specify a start position of log consumption. You can consume historical log data and consume new log data in real time.

When SLS is collecting logs, it adds certain reserved fields such as `__time__` to the original log data. These fields can be imported into BytePlus TLS. The fields `__time__` and `__source__` are imported by default, while some fields such as `__tag__:_pod_name_` must have their field names converted before importing. Other fields cannot be imported.

The following log fields can be imported:


|SLS Metadata Field |Corresponding Field in BytePlus TLS |
|---|---|
|`__time__` |`__time__` |
|`__source__` |`__source__` |
|`__tag__:_pod_name_` |`__pod_name__` |
|`__tag__:_container_name_` |`__container_name__` |
|`__tag__:_pod_uid_` |`__pod_uid__` |
|`__tag__:_container_source_` |`__container_source__` |
|`__tag__:_container_ip_` |`__container_ip__` |
|`__tag__:_namespace_` |`__namespace__` |
|`__tag__:_image_name_` |`__image_name__` |
|`__tag__:__path__` |`__path__` |
|`content` |`__content__` |


<span id="注意事项"></span>
## Precautions


* To ensure data security, we recommend that you use the AccessKey pair of an Alibaba Cloud RAM user for authentication when creating a log import task. The RAM user must be granted the permissions on the consumer group. For more information on how to create a permissions policy, refer to [Sample SLS RAM authorization policy](https://docs.byteplus.com/docs/tls/Importing_data_from_sls#sls-ram-%E6%8E%88%E6%9D%83%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B). For more information on how to grant permissions to a RAM user, refer to [RAM user authorization](https://www.alibabacloud.com/help/en/sls/create-a-ram-user-and-authorize-the-ram-user-to-access-log-service?spm=a2c63.p38356.0.0.51757034nA1Yxt). You can also create a custom RAM authorization policy according to your business requirements. For more information on the actions related to consumer groups, refer to [RAM user authorization](https://www.alibabacloud.com/help/en/sls/user-guide/use-consumer-groups-to-consume-data?spm=a2c63.p38356.0.0.6ed4592di3ubdO#section-yrp-xfr-7va).

* After a log import task is created, you cannot modify the data source and other configurations. In case of a configuration error, delete the configuration and create a new configuration.

* A TLS topic can only be associated with one SLS log import task. You cannot import log data from multiple Logstores to the same log topic.

* During log import, the data in the shards of an SLS Logstore does not consistent with the data in the shards of the destination TLS topic.

* After an SLS log import task is created, BytePlus TLS creates a consumer group on the SLS side for consuming log data. Do not modify or delete the consumer group on SLS. If you reset the consumer offset or delete the consumer group, issues such as repeated consumption or consumption failure will occur.


<span id="前提条件"></span>
## Before you begin


* Create a project and a Logstore in Alibaba Cloud SLS, and use the Logstore to store collected log data.

* Create a project and a topic in BytePlus TLS. The number of shards in the topic must be the same as the number of shards in the Logstore.

* The first time you use the log import or log shipping feature, you must grant read and write permissions to TLS to allow it to access the data source. If you do not grant the permissions to TLS before you use the feature, TLS guides you to perform the required operations when you create a log import task in the console. We recommend that you use the credentials of your BytePlus account to grant permissions. For more information, refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id="从-sls-导入日志"></span>
## Import log data from SLS

Perform the following steps to create an SLS log import task:

<span id="步骤一-初始配置"></span>
### Step 1: Configure the basic information


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **SLS log migration** pane, select **Alibaba Cloud SLS log migration**.

5. Configure the **Basic information**.

   
   |Parameter |Description |
   |---|---|
   |Basic information |The type of the log import task. The default value is **Cloud service log**. |
   |Project |The name of the destination TLS project that you want to use to store the log data imported from SLS. |
   |Topic name |The name of the destination TLS topic that you want to use to store the log data imported from SLS. |
   


<span id="步骤二-数据源配置"></span>
### Step 2: Configure a data source


1. Complete the data source configuration.

   
   |Parameter |Description |
   |---|---|
   |Task name |The name of the log import task. |
   |Data source |The data source from which you want to import log data. The default value is **Alibaba Cloud**. |
   |Network type |The type of network that you want to use to import log data. Both public networks and private networks are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to transmit data over a private network, contact sales.</div><br> |
   |Domain name |The domain name of Alibaba Cloud SLS. You can view it on the **Project Overview** page of the source project in the SLS console. |
   |Project |The name of the source project. |
   |Logstore |The name of the source Logstore. |
   |Consumer group |The name of the consumer group.<br><br>A Logstore can have up to 30 consumer groups, and each consumer group must have a unique name. |
   |key |The AccessKey ID and AccessKey Secret of your Alibaba Cloud account. BytePlus TLS uses the credentials of the specified account to authenticate with Alibaba Cloud SLS for reading and consuming log data from the specified project and Logstore.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the credentials of an RAM user for authentication. The RAM user must have the permissions on the specified consumer group. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Importing_data_from_sls#sls-ram-%E6%8E%88%E6%9D%83%E7%AD%96%E7%95%A5%E7%A4%BA%E4%BE%8B">Sample SLS RAM authorization policy</a>.</div><br> |
   |Consumption starting position |The start position of log consumption. Valid values:<br><br><br>* Earliest data: start consuming data from the earliest log data entry in the Logstore. This is the default value.<br><br>* Latest data: start consuming data from the latest log data entry in the Logstore.<br><br>* Custom point\-in\-time data: start consuming data from the specified time point. You can set a log retention period for log data stored in the Logstore, and the log entries whose retention periods exceed the specified period are automatically deleted. Therefore, you must make sure that the time point specified in this field falls into the time range determined by the log retention period, otherwise, the consumption configuration does not take effect. |
   |Consume in order |Specify whether to consume log data in sequence. The feature is enabled by default.<br><br><br>* Enabled: TLS consumes the log data in a shard in sequence. After a shard is split, TLS consumes the data in the original shard first, then consume the data in the shards split from the original shard simultaneously. After shards are merged, TLS consumes the data in the original shards first, then consume the data in the new merged shard.<br><br>* Disabled: TLS does not consume log data in sequence. That is, TLS starts consuming all data simultaneously and immediately consumes data from new shards generated by shard splitting or merging. In this case, log data is written into the BytePlus TLS topic in a disordered manner. |
   

2. Confirm the configurations, then click Next step.


<span id="步骤三-更新索引"></span>
### Step 3: Update indexes


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. The index feature is disabled by default. To query and analyze the collected log data, enable this feature.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2) to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a log import task is created, TLS immediately starts consuming log data from SLS and writes the data into the specified topic in real time. You can enable the indexing feature and configure indexes for implementing real\-time log query and analysis. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Configure-indexes-2">Configure indexes</a>.   </div>
   

<span id="查看日志导入任务"></span>
## View a log import task

After a log import task is created, you can view the basic information and data source information on the details page of the import task. You can also view the consumption status of each shard in the Alibaba Cloud SLS console.

<span id="查看任务信息"></span>
### View task information


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **SLS log migration** pane, Click the name of the log import task to view its basic information.

   n the details page of the log import task, you can view the basic information such as the task name, destination topic, and import status, as well as the data source information such as the data source, consumer group, and network type.

   The following values can be displayed in the **Status** field:

   
   |Status |Description |
   |---|---|
   |Running |The log import task is running normally. |
   |SLS resource does not exist |The project or Logstore is deleted from SLS. In this case, the data consumption process stops and cannot be resumed. To restart data consumption, you must create a new log import task. |
   |SLS authentication failed |The SLS account or permissions are invalid. For example, overdue payments exist in the account or the permissions for SLS log import are revoked from the account. After the account or permissions are restored, consumption resumes. |
   |SLS unknown exception |The SLS server is exceptional. After the server is restored, the operation resumes. |
   |TLS resource does not exist |The TLS project or topic is deleted. In this case, the data consumption process stops and cannot be resumed. To restart data consumption, you must create a new log import task. |
   |TLS authentication failed |The BytePlus TLS account or permissions are invalid. For example, overdue payments exist in the account or the permissions for SLS log import are revoked from the account. After the account or permissions are restored, consumption resumes. |
   


<span id="查看消费状态与监控信息"></span>
### View consumption status and monitoring information

The Alibaba Cloud SLS console displays real\-time consumption statuses. You can view the consumption progress through the following methods:

View the data consumption progress of each shard on the **Consumer Group Status** page. For more information, refer to [View the status of a consumer group in the Simple Log Service console](https://www.alibabacloud.com/help/en/sls/user-guide/use-consumer-groups-to-consume-data?spm=a2c63.p38356.0.0.201a4cd9CQBinD#section-91r-j3o-o2g).

<span id="删除日志导入任务"></span>
## Delete a log import task

If a data import task encounters faults or exceptions, delete the import task and create a new task to import the data. If all existing log data has been imported or you no longer need to import log data into BytePlus TLS, delete the log import task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Deleting a log import task does not affect the log data that has been imported.</div>


* <div data-tips="true" data-tips-type="tip">Once a log import task is deleted, it cannot be restored. Proceed with caution.</div>


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. On the **SLS log migration** tab, find the log import task that you want to delete, then click **Delete** in the **Action** column.

5. In the pop\-up window, confirm the information about the task to be deleted, then click **OK**.


<span id="sls-ram-授权策略示例"></span>
## Sample SLS RAM authorization policy

To use a RAM user to authenticate with Alibaba Cloud SLS for reading and consuming log data, you must grant the RAM user the required permissions on the consumer group. The recommended authorization policy is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>${projectName}</code> and <code>${logstoreName}</code> must be replaced with the actual project name and Logstore name.</div>


```json
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "log:GetCursorOrData",
        "log:GetLogStore"
      ],
      "Resource": "acs:log:*:*:project/${projectName}/logstore/${logstoreName}"
    },
    {
      "Effect": "Allow",
      "Action": [
        "log:CreateConsumerGroup",
        "log:ListConsumerGroup",
        "log:ConsumerGroupUpdateCheckPoint",
        "log:ConsumerGroupHeartBeat",
        "log:UpdateConsumerGroup",
        "log:GetConsumerGroupCheckPoint"
      ],
      "Resource": "acs:log:*:*:project/${projectName}/logstore/${logstoreName}/consumergroup/*"
    }
  ]
}
```
