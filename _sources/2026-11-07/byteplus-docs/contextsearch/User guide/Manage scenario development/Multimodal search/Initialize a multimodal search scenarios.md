---
title: "Initialize a multimodal search scenarios"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Initialize_a_multimodal_search_scenario"
---

Multimodal search scenarios support unified retrieval and understanding of various modal data, such as text and pictures. By combining multimodal models and retrieval capabilities, cross\-modal content search and image\-text Q&A scenarios can be achieved, providing users with richer and more accurate search experiences. This topic describes how to initialize a multimodal search scenario.

## Prerequisites

A multimodal search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

## Procedure

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. select **My Scene** in the left navigation bar, then click the target multimodal search scene.

4. in the **Welcome to multimodal search scenarios** dialog, configure the following parameters, then click **Configure**.

   |Parameter |Description |
   |---|---|
   |Storage location |Select the instance where the multimodal scenario is located. |
   |Database type |Select the database type used for multimodal scenarios. Currently, only **Cloud Search** is supported. |
   |Instance name/ID |select the target instance from the dropdown list. Supports fuzzy search based on keywords in the instance name. if a new instance is needed, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).<br><br>> **tip**<br><br><br>> Only OpenSearch version 2.9.0 instances support ContextSearch.<br> |
   |User name |Enter the username of the instance. |
   |Password |Enter the instance password. |
   |Private network |To ensure smooth intranet visit, select the Virtual Private Cloud in the region where your existing cloud services are located. Subnets in different availability zones within the same Virtual Private Cloud are interconnected.<br><br>If a new Virtual Private Cloud is needed, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Embedding configuration, LLM configuration, rerank configuration, ASR configuration (optional) ||
   |Select model/inference service |Select the model and inference service used for the scenario from the dropdown lists of each configuration type. Currently supported are **Common models**, **Custom models**, and **Ark models** (Rerank and ASR are not supported).<br><br>If you need a new inference service, click **Create an inference service**. For detailed steps to create a common model, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).  |
   |API Key |Select the API Key to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |
   |Search resources, import resource ||
   |Specification |Select the resource specification from the dropdown list. |
   |Quantity |Set the quantity of the resource. The selectable quantity is limited by the remaining stock of the chosen specification. |
   |Agent Team |Select whether to enable Agent Team. |
   |User\-defined parameter (optional) |Configure user\-defined parameters for the multimodal search scenario. Click **Add custom parameters**, then configure the parameter name and value. |

   when the scenario status changes to **Running**, the scene initialization is complete.
