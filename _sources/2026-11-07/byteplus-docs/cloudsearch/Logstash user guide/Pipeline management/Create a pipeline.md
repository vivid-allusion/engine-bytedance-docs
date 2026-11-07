---
title: "Create a pipeline"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline"
---

You can create a standard pipeline to collect and process data. The pipeline configuration includes input, output, and optional filter plugins. Input and output plugins configure data sources for input and output, while filter plugins handle data filtering or preprocessing. You can also create a metadata migration pipeline to transfer data between Elasticsearch/OpenSearch instances. Supports running up to 20 pipelines concurrently. This topic describes how to create a pipeline.

<span id="XOzF93b1"></span>
## Prerequisites

A Logstash instance has been created, and the Logstash instance is **Running**. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="l02S0M1x"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation, select **Data processing** \> **Logstash**.

3. In the Logstash instances list, click the target instance's name to enter the **Basic information** tab.

4. On the left, select the **Pipeline management** tab, then click **Create pipeline**.

5. In the **Create pipeline** panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Pipeline type |Select **Normal pipe** or **Metadata migration pipeline**. Details are available in [Normal pipelines](https://docs.byteplus.com/en/docs/cloudsearch/Standard_pipeline) and [Metadata migration pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Metadata_migration_pipelines). |
   |Pipeline name |Unique identifier of the pipeline. Naming rules are as follows:<br><br><br>   * Must start with a letter.<br><br>   * Length must be between 1 and 128 characters.<br><br>   * Can only contain letters, numbers, underscores (_), and hyphens (\-). |
   |Pipeline description |(optional) Description of the pipeline. Length must be between 1 and 256 characters. |
   |Configuration |Enter the configuration content in the editor box.<br><br>You can also click the **Use template** button on the right, choose a template from the pop\-up list, then click **OK** to reference the template content in the editor box, and modify the configuration content as needed. For details on ordinary pipeline configuration content, see [Structure of a pipeline](https://www.elastic.co/docs/reference/logstash/configuration-file-structure).<br><br>The configuration content includes the following plugins:<br><br><br>* input: specify the input data source. For input data source types supported by Logstash, see [Input plugins](https://www.elastic.co/docs/reference/logstash/plugins/input-plugins).<br><br>* filter: filter or preprocess the data. For filter plugins supported by Logstash, see [Filter plugins](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This plugin applies only to ordinary pipelines.   </div><br>   <br><br>* output: specify the target data source. Refer to [Output plugins](https://www.elastic.co/guide/en/logstash/current/output-plugins.html) for the types of input data sources supported by Logstash.<br><br>* index: specify the index to migrate.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This plugin is only for metadata migration pipelines.   </div><br>   <br><br>For enhanced security, if you use the JDBC driver when configuring the pipeline, add `allowLoadLocalInfile=false&autoDeserialize=false` after the **jdbc_connection_string** parameter. Otherwise, when adding a Logstash configuration file, the scheduling system will return a validation failure message, such as `RequestIllegal: jdbc_connection_string => jdbc:mysql://***.com:3306/db_name?allowLoadLocalInfile=false&autoDeserialize=false`. |
   

6. (Optional) If the **Pipeline type** for creating the pipeline is **Normal pipe**, continue configuring the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Pipeline worker threads |Number of pipeline worker threads, that is, the number of worker threads running filter and output plugins in parallel. Default value is the instance’s CPU cores. |
   |Pipeline batch delay |Maximum wait time per batch when the pipeline batch size is not met. Default value: 50. Unit: ms. |
   |Pipeline batch size |Maximum number of events processed per batch. Default value: 125. |
   |Queue type |Queueing model used for event buffering, valid values:<br><br><br>* Memory\-based queue<br><br>* Disk\-based persistent queue |
   |Maximum queue byte size |The maximum number of bytes the queue can store, which must be less than the disk capacity of a single instance node. Default value: 1024. Unit: MiB. |
   |Queue checkpoint write count |The maximum number of events written when enforcing a checkpoint. If set to 0, it means unlimited. Default value: 1024. |
   

7. Click **Save** or **Save and deploy** as needed.

   * **Save**: Save pipeline information only without running it. After saving, the system returns to the **Pipeline management** tab. In the pipeline list, click **Deploy** in the **Actions** column of the target pipeline to trigger instance restart and apply the configuration.

   * **Save and deploy**: Save the pipeline information to the Logstash instance, trigger instance restart and apply the configuration.
