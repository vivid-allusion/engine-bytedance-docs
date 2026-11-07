---
title: "What is SenseFlow"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/What-is-SenseFlow"
---

This topic describes the features and billing of TOS SenseFlow.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">SenseFlow is currently in closed beta and is only available in China (Hong Kong). Please contact your account manager for access.</div>


<span id="2cqfLGwF"></span>
## Introduction

TOS SenseFlow is an intelligent object storage workspace built for AI applications. In the native storage environment, data can be perceived, retrieved, generated, in an intelligent, complete loop without ever leaving the TOS bucket. This reduces the barriers to development and operational costs for AI applications.

Create a SenseFlow rule, bind a scenario\-based template and preset workflow to a specified data scope, and then apply it to a bucket. As data enters the bucket, the system automatically executes the following features.


* **Content awareness**: This feature uses multimodal AI models to automatically understand the content and semantics of unstructured data, such as images and videos. It extracts key features and achieves a deep understanding of the data itself.

* **Multimodal retrieval**: This feature involves vectorizing semantic features and content descriptions and building indexes. It enables cross\-modal semantic retrieval using natural language, such as searching for images or videos with text queries.

* **Content generation**: This feature uses preset workflows to perform content analysis and intelligent content creation tasks. It produces reusable processing results that support various content production needs.


<span id="7628kOqc"></span>
## Billing notes


* SenseFlow is currently free. Before billing begins, we will notify you of the billing schedule and standards. Please pay close attention to billing notifications to avoid any unexpected charges.

* The subtitle erasure operator is provided by [AI MediaKit](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-overview). Using this operator incurs additional charges from AI MediaKit, which are not included in SenseFlow fees. 


<span id="3Smhv552"></span>
## Use cases

Using SenseFlow features requires compliance with all TOS constraints and limitations. For more information, see [Constraints and limitations](https://docs.byteplus.com/en/docs/tos/docs-restrictions).

SenseFlow specializes in understanding, retrieving, operating, and reusing multimodal unstructured data in TOS. It is ideal for the scenarios described below.


* Benefits

   
   |Benefit |Description |
   |---|---|
   |Native to object storage |All intelligent processing occurs internally within TOS. There is no need to transfer or synchronize data or metadata across multiple platforms. This approach ensures fundamental data security and consistency, as well as simplified permission management. |
   |Multimodal and closed loop |SenseFlow is an end\-to\-end solution that integrates perception, retrieval, and generation, rather than being a simple collection of features. With SenseFlow, you can configure your data once for the entire business chain. |
   |Rule\-based |You can configure multiple rules for a single bucket. This allows you to flexibly apply the most suitable intelligent processing templates to subsets of data in different business scenarios, easily meeting complex business needs. |
   |Lower barrier |SenseFlow greatly lowers the barrier to using AI capabilities with scenario\-based preset templates and a four\-step rule creation process. You can quickly add intelligence to your data without worrying about complex operator orchestration or model invocation. |
   |Enterprise‑grade controls |SenseFlow is designed with enterprise applications in mind. In the future, it will support refined permission management, budgeting and cost control, approval workflows, and diverse event notification mechanisms. This will ensure that you maintain full control over your data and costs while enjoying the convenience of AI. |
   

* Use cases

   * Intelligent security and event awareness

      In video surveillance scenarios, such as those involving industrial parks, retail stores, and residential areas, SenseFlow can automatically identify specific objects, scenes, and events. When preset conditions are met, SenseFlow triggers notifications and generates summaries or descriptions of the matched results.

   * Smart cloud photo albums

      You can use SenseFlow to manage cloud\-based mobile images and videos, such as personal and family albums in consumer applications. SenseFlow can automatically recognize the content of photos and videos. It supports semantic searches based on people, scenes, or time. It can also generate personalized content, such as animated GIFs, highlight reels, and daily memories.

   * Retrieval and reuse of AI asset libraries

      You can use SenseFlow to manage enterprise media assets and generate content. SenseFlow can quickly locate historical materials, such as ad materials, films, and brand content, in libraries by semantics, style, or theme. It supports multi\-select aggregation, enabling you to create temporary lists for reuse across projects and for secondary creation.


<span id="pfT3bRJl"></span>
## Workflow

The SenseFlow workflow is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4d9630f37439b74e214cb379ab39197.png) </span>

&nbsp;

Remarks:


|Category |Description |
|---|---|
|Preset templates |TOS offers a variety of SenseFlow preset templates. You can configure a processing pipeline by combining multiple preset operators with one click. For more information about preset templates, see [Preset templates](https://docs.byteplus.com/en/docs/tos/Preset-templates). |
|Preset operators |SenseFlow workflows include various common preset operators, eliminating the need for complex conversion rule configurations. For more information, see [Preset operators](https://docs.byteplus.com/en/docs/tos/Preset-operators). |
|Create SenseFlow rules |You can create SenseFlow rules directly using the preset templates.<br><br>If these templates do not meet your needs, you can create custom templates and configure workflows for them using preset operators to handle complex, scenario\-based tasks.<br><br><br>* To create a SenseFlow rule, see [Creating a SenseFlow rule](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-rule).<br><br>* To create a custom template, see [Creating a SenseFlow template](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-template).<br><br>* To create a workflow, see [Creating a SenseFlow workflow](https://docs.byteplus.com/en/docs/tos/Creating-a-SenseFlow-workflow). |


&nbsp;

<span id="Ut7kLLjw"></span>
## FAQ

**Will my data be lost or altered after I enable SenseFlow?** 

No. SenseFlow only reads your original data. It analyzes the content of your objects, and the generated indexes and metadata are stored separately from your original objects. Some workflows, such as video editing, generate new objects that are stored in your bucket by default. However, these new objects do not affect the original ones.

**Once I have enabled a SenseFlow rule for a bucket, how long will it take before I can retrieve content?** 

It depends on how much data needs to be processed under your rule. Typically, indexing and retrieval of newly uploaded objects are completed within minutes.

**Can I use only some of SenseFlow's features, such as content awareness, without retrieval?** 

Yes. SenseFlow is modular. Through template and workflow configuration, you can enable only the features you need. For example, you can set up a rule that performs content awareness and triggers notifications without creating an index for front\-end queries.
