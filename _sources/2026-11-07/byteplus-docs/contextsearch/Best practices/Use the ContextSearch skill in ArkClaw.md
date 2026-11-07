---
title: "Use the ContextSearch skill in ArkClaw"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Use_the_ContextSearch_skill_in_ArkClaw"
---

This topic describes how to integrate and use the ContextSearch skill in ArkClaw to help developers build multi\-knowledge source and multi\-modal context retrieval capabilities for Agent applications. By properly configuring context and call strategies, the large model can proactively acquire more relevant information before answering, significantly improving answer accuracy and business results.

<span id="7kqmKnZW"></span>
## Feature introduction

ContextSearch builds a "context layer" for large model applications. Its core goal is not merely to improve retrieval hit rates but to enable the model to obtain more accurate, relevant, and multi\-modal contextual information before generating answers. In the Agent architecture of ArkClaw, ContextSearch integrates as a skill, enabling the large model to actively retrieve context.


* Unified access and automatic selection of multiple knowledge bases

   Suitable for multiple business lines or multi\-data source scenarios. Supports configuring multiple contexts corresponding to different business domains, teams, or systems, with features including:

   * Automatic selection of the most relevant knowledge base

   * Avoid information noise or insufficient coverage caused by a single knowledge base

   * Improve context matching accuracy for complex problems

* Multimodal context retrieval

   In addition to text, ContextSearch supports image and video search, allowing the model to reason and respond based on product pictures, user screenshots, video clips, and structured descriptive information, upgrading from "text\-only understanding" to "real\-world data comprehension".


<span id="uatWytPV"></span>
## Application scenarios


* E\-commerce scenarios

   * Same product recognition

   * Image\-text consistency verification

   * Product image\-based Q&A and guided shopping

* Customer service and operations

   * Combine institutional documents with user screenshots and videos for precise responses

   * Reduce repeated inquiries and increase one\-time resolution rates

* Content platforms and media

   * Similar picture and video search

   * Content deduplication, review, and reuse detection

* Retail, local life, and brand compliance

   * Search store photos linked with historical cases

   * Provide more explainable judgment basis


<span id="vOZwX5gB"></span>
## Preparations


* The knowledge base scenario has been created, public network access enabled, and publishing completed. For more information, see [Scenario management](https://docs.byteplus.com/en/docs/contextsearch/Manage_scenario_development).

* API Key has been created. For more information, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).

* Exclusive ArkClaw has been created.

* ContextSearch skill file has been downloaded. The file is as follows.

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ac395c7a34cb04cff41612df62073cb.zip" name="context-search.zip">context-search.zip</Attachment>
   


<span id="I3LwYELM"></span>
## Procedure


1. Install ContextSearch skill.

   1. Upload the downloaded ContextSearch skill file `context-search.zip` to ArkClaw.

   2. Obtain the link of the uploaded File in TOS. For more information, see [Obtain object links](https://docs.byteplus.com/en/docs/tos/Quickly-use-the-tos-browser#.5q2l6aqk5Zub77ya6I635Y-W5paH5Lu25Zyw5Z2A).

   3. Log on to the [ArkClaw console](https://console.byteplus.com/arkclaw/) and select your dedicated ArkClaw.

   4. Enter the following content in the ArkClaw dialog.

      ```Plain Text
      安装 skill，地址如下：{context-search.zip 文件在 TOS 中的链接}
      ```
      

2. Configure the knowledge base.

   1. In the knowledge base scenario example, copy the base URL of the scenario (ignoring the part after `.com`, e.g., `https://xxx-cn-beijing.contextsearch-dev.ivolces.com`). For more information, see [View the calling example](https://docs.byteplus.com/en/docs/contextsearch/Scenario_development#h0obf9JM).

   2. Enter the following content in the ArkClaw dialog.

      ```Plain Text
      配置知识库，地址如下：{场景的 base URL}
      ```
      

3. Configure the API Key.

   Enter the following content in the ArkClaw dialog.

      ```Plain Text
      配置 API Key，信息如下：{您创建的 API Key}
      ```
      

4. Use the ContextSearch skill.

   Enter the content you want to search in context in the ArkClaw dialog.
