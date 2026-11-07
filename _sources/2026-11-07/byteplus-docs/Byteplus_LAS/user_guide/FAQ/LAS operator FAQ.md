---
title: "LAS operator FAQ"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/LAS_operator_FAQ"
---

<span id="fd8baef2"></span>
## Basic concepts

<span id="1c8ba5f2"></span>
### What are LAS intelligent data processing operators?

LAS offers a wide range of intelligent data processing operators, including video understanding, text generation, and image generation operators based on the Volcano Engine ModelArk model. It also provides multimodal data processing operators for audio, video, and documents, enhanced by LAS model capabilities, to meet more complex scenarios that require higher result quality and more convenient access.

<span id="0b740952"></span>
### What processing scenarios do LAS operators mainly cover?

LAS operators cover multimodal data processing scenarios such as audio, video, and documents, and include features for video understanding, text generation, and image generation.

<span id="5a2db7a5"></span>
### What is the difference between online operators and offline operators?

The core difference is in how they are used and the applicable scenarios.


|Comparison items |Online operators |Offline operators |
|---|---|---|
|Invocation method |Supports public network invocation via OpenAPI, and also supports invocation based on the daft framework on LAS development machines or in task management. |Only supports invocation based on the daft framework on LAS development machines or in task management. |
|Applicable scenarios |Flexible invocation scenarios based on OpenAPI |Scenarios requiring batch processing of multimodal data |


<span id="bd6b49b6"></span>
### Where can I find the list of supported online and offline operators?

You can view the official "[Supported operators: online operators](https://docs.byteplus.com/docs/Byteplus_LAS/Online_operators)" and "[Supported operators: offline operators](https://docs.byteplus.com/docs/Byteplus_LAS/offline-operators)" pages respectively.

<span id="954da44a"></span>
## Experience and integration

<span id="35116b77"></span>
### Is free trial or free experience supported? How can I try it out?

LAS provides an "online experience" feature and offers a certain amount of free quota. No configuration is required; you can quickly process sample documents, audio, video, and other files through the online experience entry to explore multimodal data processing effects.

Online experience entry path: After logging in to the LAS console, go to "Operator Plaza". Online operators support quick access; you can click "Online Experience" on the operator card.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The online experience provides a free quota; if the free quota is exceeded, the excess will be billed according to the operator's billing items.</div>


<span id="9c6931ae"></span>
### How do I start actually using online operators?

You can quickly initiate a data processing request through a simple API call to learn the workflow for using online operators. It is recommended to complete the preparation steps first and then proceed step by step.

<span id="5de5aa12"></span>
### What preparations are needed before using online operators?

Preparation essentials include: generating an API Key for authentication, and it is recommended to configure the API Key as an environment variable to use it securely; you also need to understand the operator invocation BaseURL (which is related to the region of your LAS service) to configure the operator invocation path parameter value.

<span id="3d6c10a2"></span>
### Why is it recommended to configure the API Key as an environment variable?

The LAS API Key contains sensitive information. If leaked, your model usage may be used by others, resulting in losses. Therefore, after obtaining the API Key, it is recommended to configure it as an environment variable for safer and more appropriate usage.

<span id="0bc27865"></span>
## Billing and activation

<span id="5abab1eb"></span>
### What are the basic rules for activation and billing?

If you are a new Volcano Engine user and have not previously activated the LAS product, you can activate LAS first. Activating the LAS product alone will not incur any charges if you do not use the billing features of LAS.

When using LAS for data processing, some operator capabilities may be based on ModelArk models or LAS self\-developed/enhanced models. The billing method is mainly "pay\-as\-you\-go" and is charged according to the type of model used. The online experience provides a certain free quota. Any usage beyond the free quota will be billed according to the operator's billing items. For more billing details, please refer to [Large model invocation billing - BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing).
