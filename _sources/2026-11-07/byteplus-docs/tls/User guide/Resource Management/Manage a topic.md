---
title: "Manage a topic"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Managing_topics"
---

In Torch Log Service (TLS), a topic is the basic unit for log management. For example, you can collect, store, query, and analyze logs based on topics. This topic describes the basic operations for managing topics, such as creating, modifying, and deleting topics.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin

Create a project in the TLS console. For more information, refer to [Manage a project](https://docs.byteplus.com/docs/tls/Managing_projects).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 200 topics can be created in a project.

* If the read and write capabilities of a topic shard are insufficient for handling the requests, new data fails to write into the shard. We recommend that you enable the automatic sharding feature.


<span id=".5Yib5bu65pel5b-X5Li76aKY"></span>
## Create a topic


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**.

4. Select the target project, then click the project name.

5. In the **Topic** area, click **Create topic**.

6. Proceed to configure the topic.

   1. Configure the basic settings.

      
      |Parameter |Description |
      |---|---|
      |Topic name |Specify a name for the topic. |
      |Log storage period |Specify a period for which log data is retained in TLS. Once the specified period is reached, the expired log data in the topic is automatically deleted.<br><br>Unit: days. Default value: 30. Valid values: 1 to 3650. The value 3650 means that log data is permanently stored. |
      |Record extranet IP |Specify whether to enable the feature of recording public IP addresses. The feature is enabled by default. Once enabled, TLS automatically adds the following metadata fields to log content:<br><br><br>* `__tag____client_ip__`: The public IP address of the log source device.<br><br>* `__tag____receive_time__`: The time when the TLS server receives the log. The value is a 10\-bit Unix timestamp.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When logs are written through web tracking, TLS uses clientAddr to record the public IP addresses of source devices.</div><br> |
      |Description |Specify a brief description of the topic. |
      |Tag |Click **Add tag**, then type a tag key and a tag value.<br><br>Tags help identify and categorize cloud resources, making it easier to search and aggregate resources. For more information, refer to [Tag Overview](https://docs.byteplus.com/docs/tls/tag_overview). |
      |Shards |Specify the number of shards. Default value: 1. Valid values: 1 to 10. Each shard supports a write capacity of 5 MiB/s and 500 operations/s, and a read capacity of 20 MiB/s and 100 operations/s.<br><br>The number of shards cannot be changed after a topic is created. However, you can enable the automatic sharding feature to improve the read/write performance of the topic. |
      |Automatic sharding |Specify whether to enable the automatic sharding feature.<br><br><br>* Enabled by default: When the written data volume exceeds the capacity of existing shards for 5 consecutive minutes, TLS performs automatic sharding to meet the business needs. The number of shards after automatic sharding cannot exceed the maximum number of shards. New shards generated within the recent 15 minutes after automatic sharding cannot be automatically split.<br><br>* Disabled: Automatic sharding is disabled. |
      |Maximum shards |Specify the maximum number of shards after automatic sharding, that is, the total number of shards in the read/write state after automatic sharding. Default value: 50. Valid values: 1 to 50.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You only need to set this parameter when <strong>Automatic sharding</strong> is enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The value of <strong>Maximum shards</strong> must exceed the value of <strong>Shards</strong>. Otherwise, automatic sharding cannot be performed.</div><br> |
      

   2. Optional: Configure the advanced settings.

      
      |Parameter |Description |
      |---|---|
      |WebTracking |Specify whether to enable the web tracking feature. This feature allows you to quickly collect front\-end event tracking data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enable the web tracking feature for a topic, authentication is not required when the WebTracks API action is used to write data. In other words, an anonymous user from the internet can write data to the topic, which may generate dirty data. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Use_web_tracking_to_collect_logs">Use web tracking to collect logs</a>.</div><br> |
      

7. Click **OK**.


<span id=".5L-u5pS55pel5b-X5Li76aKY6YWN572u"></span>
## Modify the settings of a topic

You can click **Edit** corresponding to a topic to modify the topic settings such as the topic name and log storage period. In the topic list, you can also modify the basic settings of a topic, such as the topic name and description.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You cannot change the shard count.</div>


* <div data-tips="true" data-tips-type="tip">When you enable the automatic sharding feature, you must set the value of the <strong>Maximum shards</strong> parameter to a value greater than the existing shard count.</div>


1. Enter the details page of the log project.

   1. In the top navigation bar, select the region where the TLS is located.

   2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

   3. Select the target project, then click the project name.

2. In the **Topic** area, locate the target topic, and click **Edit** in the **Actions** column.

3. Modify the settings of the topic.

   For more information about the parameters, see [Create a topic](https://docs.byteplus.com/docs/tls/Managing_topics#.5Yib5bu65pel5b-X5Li76aKY).

4. Click **OK**.


<span id=".5L-u5pS55pel5b-X5a2Y5YKo5pe26Ze0"></span>
## Change the log storage period


1. Enter the details page of the log project.

   1. In the top navigation bar, select the region where the TLS is located.

   2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

   3. Select the target project, then click the project name.

2. In the **Topic** area, find the target topic.

   On the upper\-left corner of the area, you can search for the topic based on the topic name or ID.

3. In the **Log storage period** column, click the **Edit** icon, then set a new value.

   You can also change the topic name and description in the topic list. TLS automatically generates an ID for each topic. The ID of a topic cannot be changed.


<span id="1e21d4c6"></span>
## Import a topic

TLS supports batch import of specified topics and their index configurations across regions and projects.


1. Enter the details page of the log project.

   1. In the top navigation bar, select the region where the TLS is located.

   2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

   3. Select the target project, then click the project name.

2. In the **Topic** area, find the target topic.

3. In the **log topics** area, click **Import Topic**.

4. On the **Topic Import Task** Page, complete the following configuration and click **Next: Execute Tasks** .

   
   |Parameter |Description |
   |---|---|
   |Source region |Select the region of the journal topic to import. |
   |Source project |Select the project where the topic to be imported is located. |
   |Source topic |Select the topics to be imported, up to 100 log topics can be imported at a time.<br><br>When Import index at the same time is selected, the index of the source topic is imported at the same time. |
   

5. Confirm that the topic import task is complete.

   After confirming that the import is complete, you can click **Finish** or click **Continue to import the acquisition configuration**. For more information, refer to [Import collection rules ](https://docs.byteplus.com/docs/tls/logcollector_collection_rule_management#5253bb5a).


<span id=".5Yig6Zmk5pel5b-X5Li76aKY"></span>
## Delete a topic

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before you delete a topic, make sure that you have disassociated the topic from all log collection rules.</div>


* <div data-tips="true" data-tips-type="warning">After a topic is deleted, all log data and configuration data related to this topic are permanently deleted and cannot be recovered. Perform this operation with caution.</div>


1. Enter the details page of the log project.

   1. In the top navigation bar, select the region where the TLS is located.

   2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

   3. Select the target project, then click the project name.

2. In the **Topic** area, find the target topic.

3. In the **Actions** column, click **Delete**.

4. In the dialog box that appears, confirm the information of the topic that you want to delete, then click **OK**.

   The resources associated with this topic are displayed in the dialog box. When there is an associated resource, you can click **to delete** , first delete the corresponding resource.
