---
title: "Data delivery"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/data_delivery"
---

The data delivery feature allows you to automatically export detailed playback quality data from **Quality Insights** to your own data analysis systems. This enables in\-depth analysis, real\-time monitoring, and seamless integration with your existing data pipelines.

This guide explains how to set up a delivery task to push your VOD data to an **AWS Kinesis** data stream. The process uses [BytePlus Torch Log Service (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS) as a secure and reliable intermediary to collect and forward the data.

<span id="915a39d7"></span>
## How it works

The data delivery process follows a simple, robust workflow. All configuration is done within the VOD console, and the data flows automatically once the task is activated.


1. **VOD console configuration**: You activate the service, configure a delivery task, and select the specific VOD applications whose data you want to export.

2. **Delivery to TLS**: The VOD service collects the data from your selected applications and delivers them to your dedicated BytePlus Torch Log Service (TLS) project.

3. **Push to AWS Kinesis**: BytePlus TLS then securely pushes this data to your specified AWS Kinesis service endpoint for consumption.


<span id="bfbbb73e"></span>
## Creating a data delivery task

Follow these steps to create and activate a data delivery task.


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Select **Quality insights** \> **Data delivery** on the left navigation bar.

3. Click **Create task**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If this is your first time using the feature, you will be prompted to activate the TLS service. Read the authorization description, which explains that a service\-linked IAM role will be created to allow VOD to access TLS. Click <strong>Activate Now</strong> and confirm the authorization. Once authorized, the system will automatically create a default TLS log project to host your VOD data.   </div>
   

4. In the **Create task** wizard, configure the following details:

   * **Data retention period**: Specify how long the data should be stored within TLS before being purged. You can set a value from 1 to 3649 days. To store logs permanently, set the value to **3650** days.

   * **Description**: (Optional) Add a brief description of the task for your own reference (up to 140 characters).

5. Click **Select app**. A list of your available VOD applications will be displayed. Select the checkbox next to each application you wish to include in this delivery task. You can select multiple applications.

6. Click **Confirm**. Your new delivery task will be created and will appear in the task list with an **Enabled** status. You can find the corresponding **Topic Name**, **Project Name**, and **Project ID** in the task list's details.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To prevent delivery failures, do not manually delete the topic or project directly from the TLS console.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fce4ac1ef03242a99953cd1611131543~tplv-goo7wpa0wc-image.image) </span>


<span id="93e013d7"></span>
## Next steps

After you successfully create a log delivery task in the VOD console, the playback quality data will be continuously delivered to the TLS topic. The next step is to configure a consumer to process this data from TLS and forward it to your downstream systems, such as AWS Kinesis.

BytePlus TLS supports data consumption via the **Kafka protocol**, allowing you to use common big data frameworks like **Apache Flink** to handle the log stream. To complete the integration, you need to:


1. **Enable Kafka protocol consumption**: Enable the Kafka protocol for your log topic to get a Kafka\-compatible Topic ID.

2. **Configure a Flink consumer**: Set up an Apache Flink job using the `flink-connector-kafka` plug\-in. This job will connect to the TLS endpoint, authenticate using your AccessKey pair, and subscribe to the topic.

3. **Write data to a sink**: Within your Flink job, you can then process the log data and write it to a sink, which can be configured to push data to your AWS Kinesis data stream.


For a complete, step\-by\-step guide with code examples on how to set this up, please refer to the detailed [Use Flink to consume logs](https://docs.byteplus.com/en/docs/tls/use_flink_to_consume_logs) documentation.
