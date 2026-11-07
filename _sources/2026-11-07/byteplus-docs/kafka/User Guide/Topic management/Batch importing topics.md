---
title: "Batch importing topics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/batch-importing-topics"
---

In scenarios like application migration to the cloud or instance backups, if you want to create multiple topics at once, you can batch create topics in the console by uploading a configuration file. This topic describes how to batch import topics.

<span id="6cc4c20d"></span>
## Background information

In scenarios like application migration to the cloud or instance backups, you must create a batch of topics in the new instance with configurations identical to the topics of the source instance, including the same topic names, partition count, message retention time, and more. Message Queue for Kafka allows you to batch create topics in the console by uploading a configuration file. You can prepare a topic configuration file based on a specified format template and upload it to the Message Queue for Kafka console. The back\-end service automatically creates the topics with the specified configurations.

<span id="580b58bb"></span>
## Precautions


* Only configuration files in CSV format are supported. The file size cannot exceed 10 MB.

* You can import up to 200 topic configurations in batch at a time, which means up to 200 topics can be batch created simultaneously.


<span id="083abcd0"></span>
## Before you begin

Before batch importing topics in the console, prepare a configuration file based on the configuration template provided by the console. The configuration file must include topic names and other configuration information.

On the topic list page, click **Bulk import topics** and follow the prompts to download the configuration template. Fill in the information about the topics you want to import in the template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each column in the configuration file is mandatory. Otherwise, template parsing fails during upload. However, the description and user permissions can be left blank, indicating no description information and no custom permissions.</div>


* <div data-tips="true" data-tips-type="tip">Parameter configurations must meet the specified requirements. For more information, refer to the header row of the template.</div>



<span id="57d1a499"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic management** tab.

5. Click **Bulk import topics**.

6. Upload the configuration file following the prompts.

   * If the page displays **File data verification passed**, the configuration file has been correctly parsed. Continue with the following steps.

   * If the page displays **File data verification failed, please follow the prompts to modify**, the configuration file has errors. Correct these errors following the prompts and upload the configuration file again.

7. Click **Create Import Task**.

   The back\-end service batch creates topics based on the uploaded configuration file and generates a background task for tracking the task execution details.

   * If the status of the topic changes from **Creating** to **In service**, the topic is created and ready for use.

   * If a topic stays in the **Creating** state for a long time or encounters other anomalies, you can view detailed task execution information on the **Background task management** tab.
