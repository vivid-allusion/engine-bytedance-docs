---
title: "Pipeline status"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Pipeline_status"
---

This topic describes the status transitions and meanings of various pipeline types in Logstash.

<span id="C5iNNMbq"></span>
## Standard pipeline

The status transitions of a standard pipeline are shown in the diagram below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4af6534efa436dd8e0b6fa3f21ee87d5.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">A standard pipeline enters the stopped status only when you click the <strong>Stop</strong> button. For non\-persistent tasks, such as stock Data migration, non\-continuous reading of File records, reading data from stdin, etc., a standard pipeline does not automatically enter the stopped status after completion.</div>


   * <div data-tips="true" data-tips-type="default">If the Logstash YAML configuration is set to <code>config.reload.automatic: true</code> (default), the following output appears in the logs when the pipeline finishes:</div>


      <div data-tips="true" data-tips-type="default"><code>[2025-10-20T17:45:47.216][INFO ][logstash.javapipeline    ][pipeline_id] Pipeline terminated {"pipeline.id"=>"pipeline_id"}</code>      </div>
      

   * <div data-tips="true" data-tips-type="default">If the Logstash YAML configuration is set to <code>config.reload.automatic: false</code>, the Logstash node will restart after the pipeline finishes, and the pipeline task will run again.</div>


* <div data-tips="true" data-tips-type="default">When deploying pipelines, if the pipeline configuration is incorrect, the pipeline will still enter the <strong>Running</strong> status. Check the logs to confirm whether the pipeline task is running normally. For specific actions, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/Query_logs">Query logs</a>.</div>



<span id="UZid8xAW"></span>
## Metadata migration pipeline

The status flow of the metadata migration pipeline is shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3da9a42a5661773d6d14762cea67cd08.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The metadata migration pipeline cannot be suspended or stopped. Even if the logs show the metadata migration pipeline has completed running, the pipeline status still displays as <strong>Running</strong>.</div>
