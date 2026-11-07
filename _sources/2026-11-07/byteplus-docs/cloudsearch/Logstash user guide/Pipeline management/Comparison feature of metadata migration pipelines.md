---
title: "Comparison feature of metadata migration pipelines"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Comparison_feature_of_metadata_migration_pipelines"
---

When using the metadata migration pipeline, you may need to verify whether the metadata of the source cluster matches that of the target cluster. This topic introduces the comparison feature of the metadata migration pipeline in Logstash.

<span id="TWHJitaG"></span>
## Prerequisites


* A Logstash instance has been created and is in the **Running** state. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

* A metadata migration pipeline has been created in the Logstash instance. For specific actions, see [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline).


<span id="yUPyMuno"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation, select **Data processing** \> **Logstash**.

3. In the Logstash instances list, click the target instance's name to enter the **Basic information** tab.

4. On the left, select the **Pipeline management** tab, then click **Compare** in the **Actions** column of the target metadata migration pipeline.

5. In the **Metadata comparison** panel, select the **Index** or **Index template** tab according to the content to compare, then filter the metadata to compare based on the following criteria.

   * Search by name

   * Specify metadata range

      * Filter results by current configuration: compare based on the current metadata migration pipeline's configuration (mainly including `include_list` and `exclude_list`), filtering out results outside the configuration scope.

      * All clusters: ignore the metadata migration pipeline configuration and compare all selected types of metadata in the cluster (excluding system metadata starting with `.`).

   * Display strategy

      * Prioritize showing existing metadata in the target cluster: by default, metadata already present in the target cluster is displayed first; switch pages to view and compare other metadata.

      * Show only missing target cluster: hide metadata already existing in the target cluster and only display the parts missing from the target cluster.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Cluster information is generated in real time based on the current pipeline configuration; modifying the pipeline configuration affects comparison results. If the source or target cluster configuration is incorrect, the comparison function will report an error. See <a href="https://docs.byteplus.com/en/docs/cloudsearch/Comparison_feature_of_metadata_migration_pipelines#9m8S1ha6">Debug</a> for details.</div>


<span id="9m8S1ha6"></span>
## Result description

After selecting the appropriate option, the system displays the metadata differences between the source cluster and the target cluster. The specific rules are as follows:


* Metadata present in both clusters: show specific differences. The `+n` or `-n` next to the metadata name indicates the number of rows added or removed in the target cluster compared to the source cluster. Difference content is collapsed by default and can be viewed by clicking the  **+**  before the metadata name or the **expand all** button at the top of the table. Click **full screen** after expanding to enter full\-screen mode and view the differences.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>uuid</code>, <code>version</code>, <code>creation_date</code>, and <code>provided_name</code> in the index metadata differ with each creation and are not included in the comparison.   </div>
   

* Metadata only exists in one cluster: the presence status will be shown to the right of the metadata name, and specific content will not be displayed at this time.


Possible reasons for metadata differences include:


* Differences in configurations developed by cloud providers.

   Some configurations are specific extensions for certain cloud providers. Common examples are as follows:

   * Tencent Cloud

      ```Plain Text
      index.hybrid_storage.segment.retention_period
      index.hybrid_storage.segment.replica.retention_period
      index.fast-indexing.enabled
      index.bulk_routing.enabled
      bulk_routing.enabled
      ```
      

   * Alibaba Cloud

      ```Plain Text
      apack.openstore.quota.limit.ratio
      index.direct_routing.enable
      index.merge.policy.time_series_field
      index.havenask.engine.enabled
      index.havenask.engine.search.type
      ```
      

   If the differences are caused by the above configurations, it is recommended to replace them with equivalent configurations supported by BytePlus Cloud Search Service.

* Default template automatic type conversion: the system may automatically convert some unsupported data types to compatible types (e.g., converting `flattened` to `flat_object`). This type of difference is normal and requires no action.


<span id="185PMDv9"></span>
## Debug

If a comparison function error occurs, check the specific cause in the logs. For specific actions, refer to [Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs). The `command` field in the logs distinguishes between metadata migration pipeline logs and comparison function logs. For example, `'command': 'migrate'` indicates a metadata migration request, while `'command': 'diff'` indicates a comparison function request.
