---
title: "Batch importing groups"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/importing-groups"
---

In scenarios like application migration to the cloud or instance backups, if you want to create multiple groups at once, you can batch create groups in the console by uploading a configuration file. This topic describes how to batch import groups.

<span id="6cc4c20d"></span>
## Background information

In scenarios like application migration to the cloud or instance backups, you must create a batch of groups in the new instance with configurations identical to the groups of the source instance, including the same group IDs and descriptions. Message Queue for Kafka allows you to batch create groups in the console by uploading a configuration file. You can prepare the group configuration file based on a specified format template and upload it to the Message Queue for Kafka console. The back\-end service automatically creates the groups with the specified configurations.

<span id="580b58bb"></span>
## Precautions


* Once uploaded, the system parses the file and creates groups based on the configurations in the file.

* Only configuration files in CSV format are supported. The file size cannot exceed 10 MB.

* You can import up to 200 group configurations in batch at a time, which means up to 200 groups can be batch created simultaneously.


<span id="083abcd0"></span>
## Before you begin

Before batch importing groups in the console, prepare a configuration file based on the configuration template provided by the console. The configuration file must include the group IDs.

On the group list page, click **Bulk Import Group** and follow the prompts to download the configuration template. Fill in the IDs of the groups you want to import in the template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the configuration file, <strong>Group ID</strong> is required, while <strong>Describe</strong> is optional.</div>


* <div data-tips="true" data-tips-type="tip">Group IDs must comply with naming conventions. For more information, refer to the header row of the template.</div>



<span id="57d1a499"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Group Management** tab.

5. Click **Bulk Import Group**.

6. Upload the configuration file following the prompts.

   * If the page displays **File data verification passed**, the configuration file has been correctly parsed. Continue with the following steps.

   * If the page displays **File data verification failed, please follow the prompts to modify**, the configuration file has errors. Correct these errors following the prompts and upload the configuration file again.

* Click **Create Import Task**.

   The back\-end service batch creates groups based on the uploaded configuration file and generates a background task for tracking the task execution details. If the status of a group is Empty, the group is created and ready for use. In case of exceptions during group import, you can view detailed task execution information on the **Background Task Management** tab.
