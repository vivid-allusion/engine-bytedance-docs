---
title: "Release Log"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Release_Log_"
---

# October 23, 2026

## Knowledge Engine VeKnow

> **注意**

> **Enterprise Knowledge Engine** changes product name to **Knowledge Engine VeKnow**.

### Q&A

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Q&A |New |Specify that in knowledge retrieval, add ontology semantics and Knowledge Graph options.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/161996c80f514952aac9629c93d9ee8f~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Q&A](https://docs.byteplus.com/docs/dataagent/Q_A). |
||New |The Enterprise Knowledge Base List provides quick access to intelligent Q&A.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06a608f89d26471ba6573f4302b65852~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Q&A](https://docs.byteplus.com/docs/dataagent/Q_A). |
||Optimize |After the deep thinking function is turned on, it supports intensive reading of the original text and improves the accuracy of question answering. At present, it mainly covers the document class, and the table class is temporarily not supported. After opening, the Agent thinking process will be added, but the context scope will be improved. |

### Data access

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Visual Knowledge Processing |Optimize |* Optimize the default value of the "Video Intelligent Understanding\-Doubao" operator part<br><br>* Optimize the parameter configuration of the "speech\-to\-text (ASR) \-Qwen\-Omni" operator, support audio sharding<br><br>* Optimize the parameter configuration of the "Speech to Text (ASR) \-Doubao Standard Edition" operator, support audio sharding, hot words, replacement words<br><br>* Optimize the parameter configuration of the "Video Intelligent Understanding\-Qwen" operator and support video sharding<br><br><br>For details, please see [Audio Processing](https://docs.byteplus.com/docs/dataagent/Audio_Processing), [Video Processing](https://docs.byteplus.com/docs/dataagent/Video_Processing). |

### Knowledge Management

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Enterprise Knowledge Base |New |Common Content Knowledge Base:<br><br><br>* Support for importing local folders.<br><br>* Local files support the simultaneous import of mixed multiple types of documents, and increase the upper limit of each document size.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8458bdbc9ad943fab5a244c5920ac466~tplv-goo7wpa0wc-image.image)<br><br>* Provides knowledge segmentation default configuration to reduce user import operation content.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a241554b5fe4254b09231f7be5d44a2~tplv-goo7wpa0wc-image.image)<br><br><br>For details, please see [Common Type Knowledge Base](https://docs.byteplus.com/docs/dataagent/Import_Knowledge#3fd98d13). |
||New |The following features have been added to the Structured Data Knowledge Base:<br><br><br>* After uploading a local file, manually adding table fields is supported.<br><br>* After importing the dataset, new and deleted table fields are identified when knowledge is updated.<br><br>* Support AI intelligent filling column names after import.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f73079b310604010b578b46d2d6a4e8f~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Structured Data Types Knowledge Base](https://docs.byteplus.com/docs/dataagent/Import_Knowledge#aeaa045a). |
||New |When the general content knowledge base of the enterprise knowledge base is imported into the public link, it supports setting up regular updates.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dfde5c510a14c40a464c8ba2ee90693~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Method 4: Online link](https://docs.byteplus.com/docs/dataagent/Import_Knowledge#c2f59e4c). |
||New |At the top of the enterprise knowledge base list, it supports accurate search based on the full text of the article, and flexibly finds authorized knowledge content.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d955c7aef0d240c9a6ad0aaf2e3aaeb2~tplv-goo7wpa0wc-image.image) |
||Optimize |Enhance the ability to recognize complex knowledge, such as images nested within a table. |
|Personal knowledge base |New |Personal knowledge base knowledge addition method is updated.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b90fad7165cc45248ef4d94e10c58345~tplv-goo7wpa0wc-image.image)<br><br><br>* Support batch import of local files, import local folders; support manual authorization and add Lark, WeCom, DingTalk cloud documents; support web links (must be publicly accessible web articles).<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/652088f59491416c87d434771dd425c7~tplv-goo7wpa0wc-image.image)<br><br>* Support connector to automatically synchronize WeCom group chat information, Lark (cloud document, mailbox, group chat information), DingTalk document, mailbox body data.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0469e22ac754359ad9739977b71da07~tplv-goo7wpa0wc-image.image)<br><br><br>For details, please see [Manage Personal Knowledge Base](https://docs.byteplus.com/docs/dataagent/Manage_Personal_Knowledge_Base). |
||New |The homepage opens up intelligent question answering capabilities.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/613e874efe764af1a4a4efb268669d4e~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Manage Personal Knowledge Base](https://docs.byteplus.com/docs/dataagent/Manage_Personal_Knowledge_Base). |
||Optimize |Support flexible search of original knowledge content.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da6036544a5e40769663eab724f4351a~tplv-goo7wpa0wc-image.image) |
||Optimize |Enhance the ability to recognize complex knowledge, such as images nested within a table. |
|Knowledge Compilation |New |Added knowledge compilation function. Knowledge compilation is a set of business domain\-oriented knowledge processing capabilities, which supports the compilation of original documents in the knowledge base into consumable structured products in the knowledge compilation space, including ontology semantics, Knowledge Graph, LLM Wiki and other forms. Through the process of "Building Compilation Space \> Describing Business Objectives \> AI Intelligent Generation Compilation Scheme \> Review and Tuning Scheme \> Release Assets \> Packaging as Agent Skill", Intelligence efficiently builds business knowledge into a consumable knowledge base for Agents, and transforms the traditional manual construction + review and confirmation process into a new way of AI construction + review and confirmation. While improving the efficiency of knowledge construction, it relies on manual review to ensure the quality of knowledge content is controllable.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4de407f768a74f33858387a2474c537b~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Knowledge Compilation](https://docs.byteplus.com/docs/dataagent/knowledge-compilation). |

### knowledge application

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|CLI/MCP Services |New |Added CLI, MCP, and Skills services to make it easier for other agents to access knowledge engine capabilities.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b41c6b10996047b6b7896f38c7d68287~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [CLI/MCP Services](https://docs.byteplus.com/docs/dataagent/cli-mcp-services). |

### Project Center

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Open capability |New |* Personal Knowledge Base Added **get personal knowledge base resource sub\-list** interface.<br><br>* **Update structured data table structure** interface request parameters add `deleted_fields`field.<br><br>* Added 5 **intelligent Q&A** related APIs in session management.<br><br><br>For details, please see [Introduction to Enterprise Knowledge Engine OpenAPI](https://docs.byteplus.com/docs/dataagent/Enterprise_Knowledge_Engine_OpenAPI). |
|resource cap allocation |New |Supports configuring knowledge base capacity by storage space.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46441e24d4bf4d65a1a0725a4706ca27~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Configure Resource Cap](https://docs.byteplus.com/docs/dataagent/Configure_Resource_Cap). |
|Permission Management |New |Unified management knowledge engine VeKnow, marketing interaction assistant, one customer and one policy engine permissions; support batch addition of users.<br><br>For details, please see [Permission Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__). |

## Marketing Interactive Assistant

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Permission Management |New |Marketing interactive assistant rights management capabilities are integrated into Knowledge Engine \> Rights Management. Within the rights management function of the knowledge engine, the permissions of the enterprise knowledge engine, marketing interaction assistant, and one customer and one policy engine are managed uniformly, and users are added in batches.<br><br>For details, please see [Permission Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__). |

# September 18, 2026

## Enterprise Knowledge Engine

### Data access

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Visual Knowledge Processing |Optimize |* Optimize large model\-related operators and do not automatically initiate data previews.<br><br>* Speech\-to\-Text (ASR) \-Doubao Standard Edition operator supports outputting gender, emotion, and speaker.<br><br>* Fixed some known errors. |

### Knowledge Management

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Knowledge Base |New |Enterprise knowledge base adds **structured data** knowledge base type, supports importing local structured data(xlsx/csv file), dataset(Clickhouse/Hive).<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cbdf625c94b45d4abdd776159303a25~tplv-goo7wpa0wc-image.image) |
||New |Enterprise knowledge base added members and permission management, you can specify the knowledge base configuration of detailed members and permissions(view, edit, management permissions).<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ff50e789d6f4b3fa8ed1024b14cab56~tplv-goo7wpa0wc-image.image) |
||New |When the general content knowledge base of the enterprise knowledge base is imported into cloud documents and object storage, the **skip duplicate documents** switch \*\*\*\* is supported.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae50fb1c8c5c41a288e67f36f85e020d~tplv-goo7wpa0wc-image.image) |
||New |The general content knowledge base of the enterprise knowledge base adds a new **public link** import method, which supports entering the public link URL that can be downloaded without authorization for identification, analysis and import.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d450c5c5cc10429c94e8abcdff671157~tplv-goo7wpa0wc-image.image) |
||New |The common content knowledge base of the enterprise knowledge base adds **WeCom documents** and **DingTalk cloud document** import methods.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef7613a0d56c484d92d1a1efd1e39fe0~tplv-goo7wpa0wc-image.image) |
||New |The personal knowledge base adds open capabilities to provide knowledge access to the external client side through the standard MCP Streamable HTTP protocol.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f87c09fbecf74443ab7af858cdfd1618~tplv-goo7wpa0wc-image.image) |
||Optimize |Optimize the preview effect of the original text of the personal knowledge base, and update the Markdown display method to display the original content of the document.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e2ed2d0521d4a39b40c286afa0afa85~tplv-goo7wpa0wc-image.image) |
||Optimize |When importing HTML knowledge, optimize segmentation effects, remove irrelevant information such as top and bottom navigation bars, and optimize complex format parsing effects. |
||Optimize |Optimize the knowledge segmentation RAG analysis effect and fix known errors. |

### Project Center

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Open capability |New |Added personal knowledge base and structured knowledge base related APIs. |

## Marketing Interactive Assistant

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Intent planning engine |New |In the intention planning engine configuration, a new **voice interaction** configuration is added, which supports enabling:<br><br><br>* Speech to text: Once turned on, users can interact with the agent through voice input.<br><br>* Text To Speech: When turned on, supports converse agent replies to voice playback.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80d8b62615b94b169c5f111d5c29bdf7~tplv-goo7wpa0wc-image.image) |
|Agent Center |New |Agent configuration:<br><br><br>* The tool configuration adds an **Internet search** switch, which can obtain real\-time network information on demand after opening.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f429cad245f04baf83c5318bbd38dcc6~tplv-goo7wpa0wc-image.image)<br><br><br>* Knowledge configuration adds a **knowledge pre\-recall** switch, which can pre\-recall the knowledge base content and inject context before the agent executes, which helps to shorten the response waiting time.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12753eea8a6b49cab6709159e59441df~tplv-goo7wpa0wc-image.image)<br><br><br>* Dialog Configuration adds **citation display** Configuration to set the presentation of referenced information in answers.<br><br>* The dialogue configuration adds a **feedback label** switch, which can be set to like the label or click on the label after opening.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c24d3087c20b448a8a975ea0c6365ad6~tplv-goo7wpa0wc-image.image) |
||New |In the agent configuration, a new **voice interaction** configuration is added, which supports opening:<br><br><br>* Speech to text: Once turned on, users can interact with the agent through voice input.<br><br>* Text to speech: When turned on, supports converse the agent replies to voice playback.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72d052763fe947cdb86ddb02c4491f7b~tplv-goo7wpa0wc-image.image) |
||New |The agent adds the function of **autonomous evolution**. By configuring the evaluation data and describing the business scenarios and quality directions that you want to improve, you can start autonomous evolution, and intelligently improve the task execution effect according to the evaluation feedback precipitation experience.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14dadd8058214580b547ef016804be9f~tplv-goo7wpa0wc-image.image) |
||Optimize |The in\-depth research agent multimodal recognition capability has been updated, and the following types of files are now supported:<br><br><br>* Image: JPG/PNG/WebP/GIF format, up to 20MB in size.<br><br>* Document: PDF/DOCX/PPTX/CSV/TXT/Markdown format, up to 100MB in size.<br><br><br>The number of files that can be uploaded at one time cannot exceed 5. |
|My App |New |The original **intelligent end point** function was upgraded to **my application**, and integrated into the marketing interactive assistant application as the function homepage. On the **My App** page, it supports switching between web and mobile ends, and the logged\-in user can choose to replace the authorized intent planning engine or agent.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c6fa52ed8344908b6e712a76d3d05f1~tplv-goo7wpa0wc-image.image) |
|Permission Management |New |The marketing interactive assistant permission management function has been updated to support session memory, MCP, Skill, observation, evaluation, my application, and automated task function permission control. |

## One customer, one policy engine

|**Product module** |**Update type** |**Update instructions** |
|---|---|---|
|Profile Library |New |Added a new **profile result** function page to centrally display and manage all profile task results, including the profile results generated by the platform profile task function, and the profile results built through the interface(the profile results built through the interface, the task name and ID are fixed to the API creation identification). |

# May 12, 2026

## Intelligent Marketing Agent

The Intelligent Marketing Agent product is launched, including the following functions:

|**Function module** |**Update type** |**Update description** |
|---|---|---|
|Enterprise Knowledge Engine |New |Relying on Volcano Engine's advanced large\-scale model and big data technology, Enterprise Knowledge Engine is oriented to various intelligent agent application scenarios in enterprises, and has the ability to manage and apply knowledge of structured and unstructured data knowledge from access, processing, modeling, mining to application, etc. It can play a role in intelligent knowledge answering, product recommendation marketing, knowledge summary analysis and other scenarios (intelligent analysis agent, intelligent marketing agent, user research agent and other scenarios that support Data Agent as a knowledge engine). Helping enterprises fully explore the value of various types of knowledge in the era of big models.<br><br>For details, please see [Overview of Enterprise Knowledge Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_Enterprise_Knowledge_Engine). |
|Marketing Interactive Assistant |New |The marketing interactive assistant is a unified agent that assists enterprises in internal or external marketing. In multi\-intent scenarios, it can automatically generate execution plans based on hit intentions, and dispatch corresponding agents and tools to reply to questions, realizing intelligent Q&A, personalized recommendation, and other capabilities.<br><br>For details, please see [Marketing Interactive Assistant Overview](https://docs.byteplus.com/docs/dataagent/Marketing_Interactive_Assistant_Overview). |
|Marketing strategy assistant |New |The marketing strategy assistant realizes the whole process coverage from marketing element analysis, intelligent circle group matching to omni\-channel strategy output through intelligent circle, intelligent matching, and interactive recommendation functions, creating a flexible, efficient and continuously evolving "AI general staff" decision\-making system for enterprises.<br><br>For details, please see [Overview of Marketing Strategy Assistant](https://docs.byteplus.com/docs/dataagent/Overview_of_Marketing_Strategy_Assistant). |
|One customer, one policy engine |New |"One customer, one policy" is the core capability engine of Marketing Agent in Data Agent. Relying on large model and data mining technology, it provides each customer with "understand you" companion services. Its in\-depth analysis of the relationship between events, products, and users breaks through the gap from label portraits to generative monolithic profiles, and combines user habits to accurately grasp the timing to achieve intimate marketing recommendations.<br><br>For details, please see [Overview of One Customer, One Policy Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_One_Customer_One_Policy_Engine). |

# October 27, 2025

## One customer, one policy engine

|**Function module** |**Update type** |**Update description** |
|---|---|---|
|One customer, one policy engine |New |"One customer, one policy" is the core capability engine of Marketing Agent in Data Agent. Relying on large model and data mining technology, it provides each customer with "understand you" companion services. Its in\-depth analysis of the relationship between events, products, and users breaks through the gap from label portraits to generative monolithic profiles, and combines user habits to accurately grasp the timing to achieve intimate marketing recommendations.<br><br><br>* Operation Path: "Marketing Agent" \- "One Customer, One Policy Decision Engine"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca7ff4a62cd4c6087e9a156e68e69a4~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Overview of One Customer, One Policy Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_One_Customer_One_Policy_Engine). |

# September 23, 2025

## Intelligent conversation assistant

|**Function module** |**Update type** |**Update description** |
|---|---|---|
|Enterprise Knowledge Engine |New |The enterprise knowledge engine function module was launched for the first time. The enterprise knowledge engine is the underlying capability of the intelligent conversation assistant. The enterprise knowledge engine function provides full\-process knowledge construction, management capabilities, and intelligent AI application capabilities. It supports enterprise\-level users to build an enterprise's knowledge base, customize AI applications, and ensure data security through refined rights management.<br><br><br>* Operation Path: "Marketing Agent" \- "Intelligent Conversation Assistant" \- "Enterprise Knowledge Engine".<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b279ebee2a2745ca8431dc9d87c5bee6~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Overview of Enterprise Knowledge Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_Enterprise_Knowledge_Engine). |
||Optimize |Supports a variety of import methods. The knowledge base in the enterprise knowledge engine supports importing knowledge from uploaded files, WeChat material libraries, object storage, and relational databases.<br><br><br>* Operation Path: "Marketing Agent" \- "Intelligent Conversation Assistant" \- "Enterprise Knowledge Engine" \- "Enterprise Knowledge Engine"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/085cfccf35a14a63bee0b0fc4000724f~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Import Knowledge](https://docs.byteplus.com/docs/dataagent/Import_Knowledge). |
||New |Supports subject Knowledge Graph, which can automatically generate Knowledge Graph based on knowledge.<br><br><br>* Operation Path: "Marketing Agent" \- "Intelligent Conversation Assistant" \- "Enterprise Knowledge Engine" \- "Subject Knowledge Graph"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4ca4bbfabbc479e8f2161ed0dce5c4b~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Knowledge Graph](https://docs.byteplus.com/docs/dataagent/Knowledge_Graph). |
|Project Center |New |Workspaces that support mapping HiAgent.<br><br><br>* Operation Path: "Marketing Agent" \- "Intelligent Conversation Assistant" \- "Enterprise Knowledge Engine" \- "Project Center" \- "Group Settings" \- "HiAgent Space Mapping" |

## Unstructured data marking

|**Function module** |**Update type** |**Update description** |
|---|---|---|
|Visual modeling |New |Added "knowledge segmentation" and "import knowledge engine" operators to import unstructured data into CDP enterprise knowledge engine after segmentation.<br><br><br>* Operation Path: "Marketing Agent" \- "Unstructured Data Marking" \- "Customer Data Platform" \- "Data Management" \- "Visual Modeling"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95ef7692186f4c359fc61a8522ca10b2~tplv-goo7wpa0wc-image.image)<br><br>See the [Knowledge Segmentation ](https://docs.volcengine.com/docs/CustomerDataPlatform/Knowledgesegmentation-1?lang=zh)for details. |
||New |Added "Volcano Ark Large Model" operator, "Restful API operator" and other characteristic operators<br><br><br>* Operation path: "Marketing Agent" \- "Unstructured Data Marking"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/387b9f5de79741e3aa853f71c9f6fb77~tplv-goo7wpa0wc-image.image)<br><br>See [Volcano Ark Large Model ](https://docs.volcengine.com/docs/CustomerDataPlatform/VolcanoArkLargeModel-3?lang=zh)and [REST API 2.0](https://docs.volcengine.com/docs/CustomerDataPlatform/RESTAPI20-1?lang=zh) for details. |

# First release on June 09, 2025

The first release of intelligent marketing agent, the main functions include intelligent conversation assistant Agent (including unstructured data marking, intelligent conversation assistant) and marketing strategy Agent two modules.

## Intelligent conversation assistant

|**Function module** |**Update type** |**Update description** |
|---|---|---|
|Unstructured data marking function |New |Unstructured data marking is a business empowering tool that supports intelligent processing of multi\-modal data, which can help enterprises integrate multi\-channel unstructured data and convert unstructured data such as text, voice, image, and video into standardized business labels.<br><br><br>* Operation path: "Marketing Agent" \- "Unstructured Data Labeling"<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfd9441aff88491cab14422dc9b1e0d7~tplv-goo7wpa0wc-image.image)<br><br>For details, please see [Overview of Unstructured Data Labeling](https://docs.byteplus.com/docs/dataagent/Overview_of_Unstructured_Data_Labeling). |
|Intelligent conversation assistant |New |The intelligent conversation assistant Agent is a conversational marketing hub that integrates real\-time customer portrait insights and AI decision engines. It realizes full\-scene intelligent interaction from customer demand analysis, rights recommendation to file update through purchase intention recognition, intelligent speech generation, accurate product recommendation, and full\-link task automation, and improves customer conversion efficiency and business fineness through multi\-system collaborative closed\-loop management.<br><br><br>* Operation Path: "Marketing Agent" \- "Intelligent Conversation Assistant"<br><br><br>For details, please see [Marketing Interactive Assistant Overview](https://docs.byteplus.com/docs/dataagent/Marketing_Interactive_Assistant_Overview). |

## Marketing Strategy

|**Function module** |Update type |**Update description** |
|---|---|---|
|Marketing strategy intelligent generation |New |Smart circle group: Support online search for industry experience, combine industry experience and local data, and intelligently generate clusters. |
||New |Marketing strategy and task generation:<br><br><br>* Support generating multiple clusters for selection, which can be used to select one of the clusters for subsequent marketing plan design.<br><br>* Combined with the generated clusters, the clusters are finely split into multiple clusters through labels.<br><br>* For each sub\-group design reach timing, match the appropriate channel, generate reach content, generate a complete marketing plan, and automate reach task configuration.<br><br>* Marketing strategies that support the generation of WeCom mass messaging |
||New |Task editing and approval: Tasks created by large models support visual editing and are executed after manual review. |
||New |Support secondary modification: support the modification of the grouping, splitting plan, and marketing strategy channel automatically circled by the system |
|Process Engine Scheduling Execution |New |Personalized Marketing:<br><br><br>* Based on the user active time model, the optimal reach period is automatically selected.<br><br>* Based on user portrait information, match different marketing channels and content (benefits, materials, etc.) for each user. |
