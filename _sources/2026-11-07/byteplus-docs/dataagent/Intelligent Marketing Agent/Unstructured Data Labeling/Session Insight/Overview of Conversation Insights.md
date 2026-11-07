---
title: "Overview of Conversation Insights"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Conversation_Insights"
---

Utilize advanced large\-scale model technology to mine user data in the private domain of enterprises (WeCom conversations, online customer service, 400 hotline, official account messages, community messages, etc.), understand user evaluations and suggestions on products, services, marketing, etc., and provide reference for business operations. At the same time, it also mines the intentions and preferences of individual users and groups, deeply understands users, better operates users, and provides assistance for enterprise growth. This article introduces the background, product features, application scenarios, and advantages of conversation insights.

<span id="82e56413"></span>
# Background introduction

Research shows that the current enterprise structured data only accounts for 20% of the total data volume, the remaining 80% are unstructured and semi\-structured data in the form of files, in the user's life cycle operation, we mine data before the structured behavior, orders, after\-sales details and other data, but there are also a large number of unstructured data between users and enterprises, such as online customer service, 400 hotline, WeCom dialogue, official account messages and other data, these data contain user concerns, user preferences, product evaluation, service evaluation and other information, from which mining and application can provide enterprises with Product Research & Development, product marketing, service system construction and other aspects to provide advice to improve business efficiency.

<span id="a3e26bf6"></span>
# Function introduction

In the conversation analysis scenario, unstructured data marking realizes multi\-dimensional analysis of high\-frequency problems, emotional tendencies, compliance, etc. by collecting multi\-channel conversation data and processing it structurally, outputs visual reports, synchronizes feedback speech optimization and knowledge completion, and forms a "data collection\-analysis\-insight\-closed\-loop optimization" full\-link capability to help enterprises improve service quality, reduce operational risks and optimize resource allocation.


* **Flexible AI plug\-in support** : Provide a variety of AI plug\-ins including customer tag extraction, customer emotion recognition, conversation summary generation, intelligent speech suggestions, and automated speech quality inspection.

* **Customer profile construction and management** : based on historical and real\-time session data, automatically identify customer information, build customer profiles, record customer characteristics and interaction history.

* **Session quality scoring and 360 customer portraits** : The system automatically performs multi\-dimensional scoring on session quality, and combines customer information to build a comprehensive 360\-degree customer portrait.


<span id="4a446192"></span>
# Detailed feature list


|**level 1 capability** |**Level 2 Ability** |**ability introduction** |**Product diagram** |
|---|---|---|---|
|session data preparation |session data access |Productized access to WeCom, voice conversations, agent conversations and other data |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e97e62293e704834b52ae0c2db83a41e~tplv-goo7wpa0wc-image.image) </span> |
||session data cleaning |Cleaning and processing data through ASR, data preprocessing (invalid data removal (fixed group sending, pure expressions, obvious garbled characters, etc.), session segmentation, session sorting), large model technology |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70fcb23321ab4248be825e0f437e633e~tplv-goo7wpa0wc-image.image) </span> |
||session file |Process the data into a standard session archive (ordered session data with business implications) for easy understanding of large models. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efefe1a316ab45299601b4bb39d7160b~tplv-goo7wpa0wc-image.image) </span> |
|session query |conversation overview |View the cumulative number of sessions, the number of new sessions, the average session duration, the maximum session duration, the minimum session duration, and the session addition trend graph in the time dimension. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68e7f462039b4bf4b4cc9ebef072b346~tplv-goo7wpa0wc-image.image) </span> |
||session detail query |You can check the session details through the session ID, customer name, customer original ID, customer service name, customer service ID, and session duration, and download the session details. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4cbd934c7694f8db89242798512cba2~tplv-goo7wpa0wc-image.image) </span> |
|session label/behavior extraction |session tag extraction |Support the creation of session label extraction tasks, extract the labels of subjects (such as users) from the session through a large model, support user customization of labels and label values, and support task timing updates (month, week, day) and manual updates. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/127d72ae3d2041529157f0a829987a7e~tplv-goo7wpa0wc-image.image) </span> |
||conversation behavior extraction |Support creating session behavior extraction tasks, extract key behavior events and behavior event attributes of the subject from the session through a large model, support user customization of events and event attributes, and support task timing updates (month, week, day) and manual updates. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b112e7502641efa23cc489f8400d86~tplv-goo7wpa0wc-image.image) </span> |
|session quality analysis |session quality assessment |Support evaluating session quality through customer sentiment analysis, customer service attitude analysis, conversation round analysis, and whether customer appeals are resolved, etc., and support opening session scoring (support setting session basic scores and scoring rules) to quantitatively evaluate session quality. Also, it supports viewing the evaluation reasons for each dimension. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2f9709786ea4a7f9d65ab799edb1202~tplv-goo7wpa0wc-image.image) </span> |


<span id="9059b810"></span>
# Application scenario


|**business link** |**application scenario** |**describe** |
|---|---|---|
|product research & development/design |Brand power evaluation<br><br>Product evaluation |Analyze users' positive and negative evaluations of brands and commodities in various dimensions, such as quality, cost performance, packaging, etc., mine users' suggestions and complaints about products, optimize products, and provide some constructive ideas for new product development. |
|marketing |User purchase intention identification, label extraction, key behavior extraction |Based on conversation tags/behavior extraction, extract tags such as customer intention, intentional goods, etc., and push related goods and activities based on user interests to improve purchase or retention conversion.<br><br>> Such as extracting user portraits: baby characteristics, baby growth and development, milk powder consumption (application scenarios, superimposed user operation system, analysis of customer purchase records, scan code behavior, return and exchange data, etc., to generate accurate customer portraits, to achieve accurate streaming and accurate user operation) |
||Gold customer service/shopping guide |Based on the conversation records between the full number of customer service/shopping guides and users, we can mine the best words and improve the purchase conversion. |
|product after\-sales |Service system optimization |Analyze user conversation logs:<br><br><br>* To understand which aspects of users' inquiries are more frequent, they can be organized into Frequently Asked Questions (FAQs) or targeted solutions to improve the efficiency of Client Server.<br><br>* Understand users' opinions on after\-sales services, customer service evaluation, etc., and optimize;<br><br>* Understand the best customer reach time period, robot matching optimization, etc. |


<span id="d7171f3b"></span>
# Advantage introduction


* Powerful data processing capabilities: multiple data source access (WeCom conversation, voice, agent conversation), data processing capabilities (ASR, data cleaning, data filtering, data standardization), all of which can be visualized.

* Product\-based interface operation: session content processing, quality assessment, label extraction, etc. are all packaged into product functions that are easy to understand by the business, ready to use out of the box.


<span id="248ce355"></span>
# Operation process


1. Access session data, productized access to WeCom, voice dialogue, agent dialogue and other data, please refer to the specific operation [Step2: Session data access and management](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#1fe79608).

2. Create a new session file, process the data into a standard session file (business meaning, ordered session data), which is convenient for large\-scale model understanding. Please refer to the specific operation [Step3: Create a new session file](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#17bd176e).

3. Create a task to extract session information, extract session labels, session behavior, see for details [Step4: Extract session information](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#0f6a7376).

4. Query sessions, view the cumulative number of sessions in the time dimension, session details and other information, please refer to the specific operation [Step5: Query Session](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#891f6b0a).

5. Create a new session quality evaluation task, evaluate session quality through customer sentiment analysis, customer service attitude analysis, dialogue round analysis, and whether customer demands are resolved. Support opening session scoring (support setting session basic scores and scoring rules), and quantitatively evaluate session quality. See for specific operations [Step 6: Session Quality Assessment](https://docs.byteplus.com/docs/undefined/6a200c3e04155105142ce01e#732d6b02).

6. Output conversational insights or analytical reports to provide customers with actionable improvement plans.

7. If you need a custom analysis session dashboard, you can build it flexibly based on BI tools.
