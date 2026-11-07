---
title: "Create resources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/getting_started_creating_resources"
---

In Torch Log Service (TLS), you can manage basic log resources such as projects and topics. A project is an application project, and a topic corresponds to a type of service. One project can contain multiple topics. This topic introduces how to create basic log resources in the TLS console.

<span id="前提条件"></span>
## Before you begin

Create a BytePlus account and complete enterprise real\-name authentication. For more information, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="创建日志项目"></span>
## Create a project

To minimize the network latency, select a Region closest to your business when creating a project.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource Management** \> **Project**.

3. Click **Create project**.

4. Specify the project name and description.

   
   |Parameter |Description |
   |---|---|
   |Project name |Specify a name for the project. This parameter is required. |
   |Description |Specify a brief description of the project. This parameter is optional. |
   |Affiliated project |From the drop\-down list, select an IAM project for the project. If you have not created an IAM project or no suitable IAM project is available, click **Create Project** to create an IAM project.<br><br>In BytePlus Identity and Access Management (IAM), IAM projects serve as resource groups with different ACL policies. IAM offers a policy management feature that allows you to categorize cloud resources across Regions into projects and create different ACL policies for these projects for flexible resource management.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify an IAM project, TLS adds the project to the IAM project named <code>default</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you create a project, you can change the IAM project to which the project belongs in <strong>IAM</strong>.</div><br> |
   |Tag |Click **Add tag**, then type a tag key and a tag value. Tags help identify and categorize cloud resources such as projects and topics, making it easier to search and aggregate resources. For more information, refer to [Tag Overview](https://docs.byteplus.com/docs/tls/tag_overview). |
   

5. Click **OK**.


<span id="创建日志主题"></span>
## Create a topic


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource Management** \> **Project**.

3. Select the target project, then click the project name.

4. In the **Topic** area, click **Create topic**.

5. Proceed to configure the topic.

   1. Configure the basic settings.

      
      |Parameter |Description |
      |---|---|
      |Topic name |Specify a name for the topic. |
      |Log storage period |Specify a period for which log data is retained in TLS. Once the specified period is reached, the expired log data in the topic is automatically deleted.<br><br>Unit: days. Default value: 30. Valid values: 1 to 3650. The value 3650 means that log data is permanently stored. |
      |Record extranet IP |Specify whether to enable the feature of recording public IP addresses. The feature is enabled by default. Once enabled, TLS automatically adds the following metadata fields to log content:<br><br><br>* `__tag____client_ip__`: The public IP address of the log source device.<br><br>   `__tag____receive_time__`: The time when the TLS server receives the log. The value is a 10\-bit Unix timestamp.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When logs are written through web tracking, TLS uses clientAddr to record the public IP addresses of source devices.</div><br> |
      |Description |Specify a brief description of the topic. |
      |Tag |Click **Add tag**, then type a tag key and a tag value.<br><br>Tags help identify and categorize cloud resources, making it easier to search and aggregate resources. For more information, refer to [Tag Overview](https://docs.byteplus.com/docs/tls/tag_overview). |
      |Shards |Specify the number of shards. Default value: 1. Valid values: 1 to 10. Each shard supports a write capacity of 5 MiB/s and 500 operations/s, and a read capacity of 20 MiB/s and 100 operations/s.<br><br>The number of shards cannot be changed after a topic is created. However, you can enable the automatic sharding feature to improve the read/write performance of the topic. |
      |Automatic sharding |Specify whether to enable the automatic sharding feature.<br><br><br>* Enabled by default: When the written data volume exceeds the capacity of existing shards for 5 consecutive minutes, TLS performs automatic sharding to meet the business needs. The number of shards after automatic sharding cannot exceed the maximum number of shards. New shards generated within the recent 15 minutes after automatic sharding cannot be automatically split.<br><br>* Disabled: Automatic sharding is disabled. |
      |Maximum shards |Specify the maximum number of shards after automatic sharding, that is, the total number of shards in the read/write state after automatic sharding. Default value: 256. Valid values: 1 to 256.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You only need to set this parameter when <strong>Automatic sharding</strong> is enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The value of <strong>Maximum shards</strong> must exceed the value of <strong>Shards</strong>. Otherwise, automatic sharding cannot be performed.</div><br> |
      

   2. Optional: Configure the advanced settings.

      
      |Parameter |Description |
      |---|---|
      |WebTracking |Specify whether to enable the web tracking feature. This feature allows you to quickly collect front\-end event tracking data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After you enable the web tracking feature for a topic, authentication is not required when the WebTracks API action is used to write data. In other words, an anonymous user from the internet can write data to the topic, which may generate dirty data. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Use_web_tracking_to_collect_logs">Use web tracking to collect logs</a>.</div><br> |
      

6. Click **OK**.


<span id="后续操作"></span>
## What to do next

[Collecte logs](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs)
