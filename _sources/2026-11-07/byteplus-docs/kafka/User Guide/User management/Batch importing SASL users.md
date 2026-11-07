---
title: "Batch importing SASL users"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/batch-importing-SASLusers"
---

In scenarios like application migration to the cloud or instance backups, if you want to create multiple Simple Authentication and Security Layer (SASL) users at once, you can batch create SASL users in the console by uploading a configuration file. This topic describes how to batch import SASL users.

<span id="cdfbba5d"></span>
## Background information

In scenarios like application migration to the cloud or instance backups, you must rapidly create a batch of SASL users in the new instance with configurations identical to the source Kafka instance, including the same usernames, password types, and more. Message Queue for Kafka allows you to batch create SASL users in the console by uploading a configuration file. You can prepare the SASL user configuration file based on a specified format template and upload it to the Message Queue for Kafka console. The system back\-end service automatically creates the SASL users with the specified configurations.

<span id="b5ec0c4f"></span>
## Precautions


* Only configuration files in CSV format are supported. The file size cannot exceed 10 MB.

* You can import up to 200 SASL user configurations in batch at a time, which means up to 200 SASL users can be batch created simultaneously.

* For instances created before August 23, 2023, PLAIN SASL users cannot be imported.


<span id="ad5977b4"></span>
## Before you begin

Before batch importing SASL users in the console, prepare a configuration file based on the configuration template provided by the console. The configuration file must include usernames and other configuration information.

On the **User Management** page, click **Upload** and follow the prompts to download the configuration template. Fill in the information about the SASL users you want to import in the template.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each column in the configuration file is mandatory. Otherwise, template parsing fails during upload. The <strong>All Permitted</strong> parameter can be left blank, indicating that All Permitted is set to false and the user does not have read and write access to all topics. The <strong>Describe</strong> parameter can also be left blank, indicating no description.</div>


* <div data-tips="true" data-tips-type="tip">Parameter configurations must meet the specified requirements. For more information, refer to the header row of the template.</div>



<span id="575446d1"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **User Management** tab.

5. Click **Upload**.

6. Upload the configuration file following the prompts.

   * If the page displays **File data verification passed**, the configuration file has been correctly parsed. Continue with the following steps.

   * If the page displays **File data verification failed, please follow the prompts to modify**, the configuration file has errors. Correct these errors following the prompts and upload the configuration file again.

7. Click **Create Import Task**.

   The back\-end service batch creates SASL users based on the uploaded configuration file and generates a background task for tracking the task execution details.

   * If new SASL users appear in the user list, the SASL users are created and ready for use.

   * If a background task stays in the **Running** state for a long time or encounters other anomalies, you can view detailed task execution information in the **Task details** column on the **Background Task Management** tab.
