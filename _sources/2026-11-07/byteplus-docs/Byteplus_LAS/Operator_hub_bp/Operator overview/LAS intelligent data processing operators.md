---
title: "LAS intelligent data processing operators"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/operator_overview"
---

LAS provides a wide range of intelligent data processing operators, including operators for video understanding, text generation, and image generation based on BytePlus ModelArk models, as well as multimodal data processing operators for audio, video, and documents that are enhanced by LAS's model capabilities. These operators enable more complex scenarios, higher quality results, and more convenient data processing.

> **说明**

> If you are a new BytePlus user and have not previously activated the LAS product, you can activate LAS first. Activating only the LAS product, without using the billing function, will not incur any charges. For activation instructions, see [Preparatory work](https://docs.byteplus.com/docs/Byteplus_LAS/Preparation_tasks); for LAS billing services and billing instructions, see [Billing instructions](https://docs.byteplus.com/docs/Byteplus_LAS/Billing_instructions).

# List of supported operators

LAS provides two types of operators, "online" and "offline", covering a wide range of multimodal data processing scenarios such as audio, video, and documents.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d36a587894124c348bd87818144a05dc~tplv-goo7wpa0wc-image.image)

|Comparison criteria |Online operators |Offline operators |
|---|---|---|
|List of supported operators |[Supported operators: online operators](https://docs.byteplus.com/docs/Byteplus_LAS/Online_operators) |[Supported operators: offline operators](https://docs.byteplus.com/docs/Byteplus_LAS/offline-operators) |
|Invocation method |Supports invoking over the public network via OpenAPI, and also supports invocation using the daft framework in the LAS development machine or task management. |Only supports invocation using the daft framework in the LAS development machine or task management. |
|Applicable scenarios |Flexible invocation scenarios based on OpenAPI |Scenarios that require batch processing of multimodal data |

# Operator pricing information

|Function modules |Billing items |Billing overview |
|---|---|---|
|Operator square & operator services |**ModelArk models**<br><br>When using LAS for data processing, some operator capabilities are based on ModelArk models. When using these operators, model fees are charged based on the type of ModelArk model used. |Billing method: "pay\-as\-you\-go", fees are charged based on the type of model used.<br><br>For details, see [Large model invocation billing - BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
||**Self\-developed models, model enhancement**:<br><br>Some operators use LAS self\-developed models, or have enhanced capabilities based on certain models. When using these operators, model fees are charged based on the type of model associated with the operator. |Billing method: "pay\-as\-you\-go", fees are charged based on the type of model used.<br><br>For details, see [Large model invocation billing - BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |

# Quick start

In addition to using the online trial feature, you can quickly initiate a data processing request through a simple API call to learn about the workflow for using online operators. You can refer to the process below, complete the preparation steps, and practice step by step to understand the workflows and key points for different scenarios.

## Preparation

* When using LAS operators for data processing, you need to generate an API Key for operator authentication. Because API Key information is sensitive, leaking your API Key may result in your model usage being consumed by others, causing potential losses. Therefore, after obtaining the API Key, it is recommended to configure it as an environment variable to ensure safe and proper use of the API Key. For details, see: [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/118248).

* When calling online operators, you first need to determine the BaseURL for operator calls based on the region where your current LAS service is deployed, which is used to configure the operator call path parameters. For details, see: [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/118249).

## Hands\-on practice

* You can quickly initiate a data processing request through a simple API call to learn how to call the interface and set key parameters for LAS data processing operators. For details, see: [Quick experience](https://docs.byteplus.com/docs/Byteplus_LAS/118257).

# Related features

## Datasets & Lance

* LAS provides dataset features for data lakes designed for multimodal data, supporting more efficient and cost\-effective data version management, data sharing, and more. For more details, see [Dataset management](https://docs.byteplus.com/docs/Byteplus_LAS/Dataset_management).

* Lance is a modern columnar data format designed specifically for large\-scale AI datasets. It is similar to Parquet, but has been deeply optimized for the storage and access of multimodal data such as images, videos, audio, point clouds, and traditional tabular data. Lance supports POSIX\-compliant Linux file systems as well as mainstream cloud object storage (Volcano Engine TOS), making it an ideal foundation for building a unified AI data lake. LAS datasets support creating datasets in the Lance format and allow you to quickly convert other types of datasets to Lance datasets for easy data ingestion into the lake. For more details, see: [Instructions for using veDaft-based datasets](https://docs.byteplus.com/docs/Byteplus_LAS/Daft-dataset-usage).

## Development machine & VeDaft

The LAS development machine is a professional development environment tailored for algorithm developers, featuring high efficiency and convenience. Developers can use it to quickly start writing, debugging, and running data processing tasks.

* In terms of resource support, the development machine provides flexible computing resource configurations, covering both CPU and GPU, to meet the computing power requirements of tasks with varying complexity. At the same time, it supports mounting storage systems such as TOS and vePFS, providing stable support for data storage and reading.

* For the development environment, the development machine comes pre\-integrated with a wide range of open\-source images, including Daft, Ray, and Spark, significantly reducing environment setup time. In addition, it is equipped with persistent cloud disk storage services dedicated to storing data during development, ensuring data security and traceability.

This integrated design enables a truly "out\-of\-the\-box" development model, effectively improving development efficiency and allowing algorithm developers to focus more on core data processing and algorithm optimization. For more information, see: [Development machine overview](https://docs.byteplus.com/docs/Byteplus_LAS/Development_machine_overview).

## Chat API & Responses API

LAS also provides general\-purpose data plane OpenAPI, including the Chat API and Responses API. Model capabilities for data processing can also be invoked through the general\-purpose OpenAPI. For details, see: [Chat API](https://docs.byteplus.com/docs/Byteplus_LAS/Chat_API), [Create model response](https://docs.byteplus.com/docs/Byteplus_LAS/Create_a_model_response).
