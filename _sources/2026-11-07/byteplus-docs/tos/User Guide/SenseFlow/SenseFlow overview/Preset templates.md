---
title: "Preset templates"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Preset-templates"
---

TOS SenseFlow offers a variety of preset templates. This topic describes the currently available preset templates.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">SenseFlow is currently only available in China (Beijing). Please contact your account manager for access.</div>


<span id="RC7eXyPX"></span>
## Preset template list


|Template name |Description |
|---|---|
|[Intelligent Security Template](https://docs.byteplus.com/en/docs/tos/Preset-templates?lang=en#FVankTei) |This template is designed for security scenarios, such as video surveillance. It offers default content understanding capabilities for videos and images, as well as a daily summary workflow.<br><br>It is ideal for business scenarios in which devices consistently generate and upload unstructured data to TOS buckets. Examples include industrial parks, retail stores, and residential areas, which usually involve large data volumes, multiple file types, and uploads from various locations. |
|[Media Asset Management Template](https://docs.byteplus.com/en/docs/tos/Preset-templates?lang=en#4pMOFh9u) |This template is designed for video processing scenarios. It provides default content understanding capabilities for documents, images, and videos, along with a workflow for removing subtitles.<br><br>It is ideal for long\-term storage of unstructured data, such as images and videos, in settings like short drama platforms, film and television production companies, and content distributors. Examples include everyday photos, videos, and screenshots. These datasets are typically large in volume and contain rich metadata that requires long\-term retention. |


<span id="FVankTei"></span>
## Intelligent Security Template


* Indexing strategy

   
   |**Dimension** |**Method** |**Description** |
   |---|---|---|
   |Semantic video indexing |Vector indexing (VLM) |Captures frames from video clips, uses vision language models (VLMs) to understand them, and generates semantic descriptions that are then vectorized. |
   |Image indexing |Multimodal indexing |Uses VLMs to understand captured images, and determines the appropriate type of alert to send. |
   

* Preset workflows

   * Content aware workflow

      This workflow automatically performs **multimodal understanding** on objects uploaded to the bucket and **creates indexes**. It supports three types of content: documents, images, and videos.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c28f2c7ad6748ae63f12898a804323b3.png) </span>

   * Daily summary workflow

      This workflow uses the content summarization operator to automatically generate a daily summary report of the previous day's content.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c005ad432f17552f7c831d9ffa05acc.png) </span>


<span id="4pMOFh9u"></span>
## Media Asset Management Template


* Indexing strategy

   
   |**Dimension** |**Method** |**Description** |
   |---|---|---|
   |Semantic scene indexing |Vector indexing (VLM) |Uses VLMs to understand photos and videos, and vectorizes the content for semantic searches. |
   |Face indexing |Facial vector indexing |Performs face detection, extraction of facial features, and clustering, and supports search by person. |
   

* Preset workflows

   * Content aware workflow

      This workflow automatically performs **multimodal understanding** on objects uploaded to the bucket and **creates indexes**. It supports three types of content: documents, images, and videos.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b7dbaf9f665f040841049395a469341.png) </span>

   * Subtitle erase workflow

      This workflow automatically removes subtitles from video files. To use this workflow, you must specify where the outputs should be stored.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b7862e0209a0a103501770910ee687b.png) </span>


&nbsp;
