---
title: "Intelligent Marking Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Marking_Overview"
---

Intelligent marking is based on AI large model capabilities and is used to mine the value of unstructured data in the private and public domains of enterprises, including session data, image data, video content data, etc. Utilize text recognition, automatic speech recognition, video needle cutting and other capabilities to preprocess data, and combine vectorized models, large model reasoning and other capabilities for data analytics, marking and point of view extraction to release data value. This article introduces the functional content, features, and operation guidelines of the application scene memory function of intelligent marking.

# Function introduction

After the enterprise generates the dataset through the visual modeling function in the CDP, it can use the AI large model ability of intelligent marking to analyze and label the dataset data, helping the enterprise to quickly mine the key information of the data and support downstream business decision\-making and optimization. The marking function includes:

* Emotion recognition: Analyze and identify emotional tendencies in data for marking.

* Subject identification: Analyze and identify subjects in data to extract user portrait information.

* Point of View Summary: Analyze and distill the core ideas and key arguments in the data.

* Marketing Water Army: Analyze and determine the marketing water army information that may be contained in the data.

* Label recognition: Analyze and match the content in the data that is relevant to the specified label.

* Custom: In addition to the above marking functions, custom marking is also supported. You can configure the large model prompt word flexibly, and the AI will mark the data according to the prompt word you set.

# Functional features

* **Out of the box, focus on core business**

   Data processing is placed in multimodal data processing modules, such as HTML tag removal for web pages, document knowledge segmentation, and so on. In the intelligent marking function, you can focus on the business itself, build marking ideas and prompt words, and customize and adjust the marking results to improve business processing efficiency.

* **Industry knowledge accumulation, lowering the threshold for use**

   Based on the accumulation of social media marketing insights in the public domain and the accumulation of experience in private domain projects, large model applications and prompt words are preset, and you can complete data marking without manually adjusting cumbersome function configurations.

* **Automatic optimization of prompt words to ensure marking effect**

   Intelligent marking supports uploading "wrong questions", summarizes the output result fields that have errors, optimizes and scores, and provides you with better prompt words to ensure the marking effect.

* **Performance optimization to increase efficiency and control costs**

   Based on the accumulation of project experience, the intelligent marking function has excellent marking speed, task stability and success rate, and has optimized the cost of tokens.

# Application scenario

|**application domain** |**scene** |**describe** |**Applicable industries (including but not limited to)**  |
|---|---|---|---|
|public opinion analysis |brand evaluation<br><br>user VOC |Analyze users' opinions on different dimensions of this product, competing brands, and products in social media content, and evaluate them positively and negatively. |Automotive, general purpose, consumer |
|Product Research & Development/Design |Brand power evaluation<br><br>Product evaluation |Analyze users' positive and negative evaluations of brands and commodities in various dimensions, such as quality, cost performance, packaging, etc., mine users' suggestions and complaints about products, optimize products, and provide some constructive ideas for new product development. |Automotive, general purpose, consumer |
|Product operation |Product selling point extraction<br><br>content recognition<br><br>user tag extraction |Extract more selling points from product detail maps and introduction manuals to assist in product operation.<br><br>Analyze users' preferences for products from historical user behavior data and products viewed in a fine grain. |Automotive, general purpose, consumer |
|Marketing |User purchase intention identification, label extraction, key behavior extraction |Based on conversation tags/behavior extraction, extract tags such as customer intention, intentional goods, etc., and push related goods and activities based on user interests to improve purchase or retention conversion. |Automotive, finance, general purpose, consumer |
||Gold customer service/shopping guide |Based on the conversation records between the full number of customer service/shopping guides and users, we can mine the best words and improve the purchase conversion. |Automotive, finance, general purpose, consumer |
|Product after\-sales |Service system optimization |Analyze user conversation logs:<br><br><br>* To understand which areas of consultation users have the most questions, they can organize common FAQs or solve targeted problems to improve the efficiency of Client Server.<br><br>* Understand users' opinions on after\-sales services, customer service evaluation, etc., and optimize.<br><br>* Understand the best customer reach time period, robot matching optimization, etc. |Automotive, finance, general purpose, consumer |
|quality monitoring |Service quality monitoring<br><br>Equipment operation monitoring |Based on surveillance videos or pictures, determine the quality of employee service, such as whether the countertops are clean, whether gloves, masks, etc., identify non\-compliant pictures or videos, and process and operate management.<br><br>Based on the equipment monitoring video, determine the equipment status. |General purpose, consumer |

# Related operations

* Intelligent marking task: By running the intelligent marking task, you can mark and save the specified dataset. For details see [Task Management](https://docs.byteplus.com/docs/dataagent/Task_Management_).

* Configure the tag library: the tag library required for subject identification or tag identification, which is used as a data reference when marking in AI applications. For details see [Manage Tag Library](https://docs.byteplus.com/docs/dataagent/Manage_Tag_Library).
