---
title: "Release notes"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Release_notes"
---

**2026**

## October 2026

|Feature |Feature description |Release date |Release regions |Related documentation |
|---|---|---|---|---|
|Data source supports MySQL |Support accessing MySQL instances as data sources, allowing direct scenario reference to facilitate users in obtaining and using business data from MySQL. |2026\-10\-13 |Asia Pacific (Johor) |[Add a data source](https://docs.byteplus.com/en/docs/contextsearch/Add_a_data_source_new) |
|Support model evaluation and release access control |Support configuring model evaluation rules for personalized search scenario model development. When core indicators do not meet preset requirements, the system restricts model release to reduce the risk of performance rollback and improve model deployment stability. |2026\-10\-13 |Asia Pacific (Johor) |[Model development](https://docs.byteplus.com/en/docs/contextsearch/Model_development) |

## September 2026

|Feature |Feature description |Release date |Release regions |Related documentation |
|---|---|---|---|---|
|Model training quality validation |Personalization search scenarios support comparing the current model evaluation indicators with those of the online model during model service release or upgrade. When detecting that the current model's core indicators fall below those of the online model, the system restricts the model release to avoid performance regression and reduce upgrade risk. |2026\-09\-08 |Asia Pacific (Johor) |[Manage model services](https://docs.byteplus.com/en/docs/contextsearch/Manage_model_services) |
|View Trace data |Agentic Search scenarios support the Trace function to view the call chain and detailed execution information of output content, helping analyze request processing.<br><br>> **tip**<br><br><br>> Trace configuration is currently in grayscale release. To use it, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |2026\-09\-08 |Asia Pacific (Johor) |[Configure an Agentic Search scenario](https://docs.byteplus.com/en/docs/contextsearch/Configure_an_Agentic_Search_scenario) |
|Agent Build capability |Multimodal search scenarios support retrieving or importing requests through natural language descriptions. The Agent Team automatically breaks down the requests and generates the corresponding retrieval/import code products. The generated product supports version control, allowing you to view code and Skills, then apply and replace the current active version with one click without manual backend configuration, improving scenario configuration and iteration efficiency.<br><br>> **tip**<br><br><br>> To use multimodal search scenarios, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for access.<br> |2026\-09\-08 |Asia Pacific (Johor) |[Configure a multimodal search scenario](https://docs.byteplus.com/en/docs/contextsearch/Configure_a_multimodal_search_scenario) |

## August 2026

|Feature |Feature description |Release date |Release regions |Related documentation |
|---|---|---|---|---|
|Personalization search scenario optimization |Personalization search scenarios include multiple new optimizations, such as:<br><br><br>* Agent interaction optimization;<br><br>* Supports viewing and modifying scene configuration information;<br><br>* Supports viewing monitoring. |2026\-08\-06 |Asia Pacific (Johor) |[Personalization search](https://docs.byteplus.com/en/docs/contextsearch/Personalization_Search) |
|Multimodal search scenario optimization |Multimodal search scenarios add multiple optimizations, including:<br><br><br>* Support importing TOS files via API;<br><br>* Support modifying instance password within the scenario;<br><br>* Search resources and import resources are decoupled and allow change specification;<br><br>* Support turning on or off specified types of models and inference services;<br><br>* Support custom parameters;<br><br>* Support getting access credentials.<br><br><br>> **tip**<br><br><br>> To use multimodal search scenarios, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for access.<br> |2026\-08\-06 |Asia Pacific (Johor) |[Multimodal search](https://docs.byteplus.com/en/docs/contextsearch/Initialize_a_multimodal_search_scenario) |

## July 2026

|Feature |Feature description |Release date |Release regions |Related documentation |
|---|---|---|---|---|
|Support multimodal search scenarios |Added multimodal search scenarios that support unified retrieval and understanding of various modalities, including text and pictures. By combining multimodal models and retrieval capabilities, cross\-modal content search, image\-text Q&A, and other search scenarios can be achieved, offering users a richer and more accurate search experience.<br><br>> **tip**<br><br><br>> To use multimodal search scenarios, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for access.<br> |2026\-07\-04 |Asia Pacific (Johor) |[Multimodal search](https://docs.byteplus.com/en/docs/contextsearch/Initialize_a_multimodal_search_scenario) |
|Data source management |The data source is a reusable knowledge resource in ContextSearch. After adding a data source, you can reference it in different scenarios to reduce repeated configurations and improve data management efficiency.<br><br>> **tip**<br><br><br>> To use data source management, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for access.<br> |2026\-07\-04 |Asia Pacific (Johor) |[Data source management](https://docs.byteplus.com/en/docs/contextsearch/Add_a_data_source_new) |
|Supports NER models |Supports NER (named entity recognition) models to automatically identify key entity information such as people’s names, locations, and organizations in text. This helps users improve text comprehension, information extraction, and knowledge construction, providing more precise semantic support for intelligent search and question\-answering scenarios. |2026\-07\-04 |Asia Pacific (Johor) |[Create a custom model](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_model) |

## June 2026

|Feature |Feature description |Release date |Release regions |Related documentation |
|---|---|---|---|---|
|Support Agentic Search scenarios |Add Agentic Search scenario, enabling autonomous planning and execution of complex search tasks. It can dynamically break down tasks according to your questions, invoke retrieval tools, and integrate search results to generate more accurate and comprehensive answers.<br><br>> **tip**<br><br><br>> To use the Agentic Search scenario, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for access.<br> |2026\-06\-04 |Asia Pacific (Johor) |[Agentic Search](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario) |
|Personalization search scenario optimization |Personalization search scenarios continue to optimize, adding model gray release evaluation metric display, Redis cache acceleration, and access point rate limiting, further improving model release efficiency, service performance, and system stability, providing more reliable operation support for recommendation services. |2026\-06\-04 |Asia Pacific (Johor) |[Manage model services](https://docs.byteplus.com/en/docs/contextsearch/Manage_model_services) |
