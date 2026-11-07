---
title: "Optimize monitoring tasks"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/Optimize"
---

[Monitoring task] The accuracy of pushed content depends heavily on the information provided by the user. The more accurate and detailed the input is, the better the monitoring results will be. This document explains the product logic and helps users clearly express their monitoring intent to obtain effective data and accurate results.

<span id="3UVaggqh"></span>
## Input for monitoring content

Because intent understanding relies on user input, descriptions of Subjects should avoid being vague, unclear, or ambiguous. Monitoring requirements should describe the desired sentiment, content scope, and other expectations as clearly as possible.

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120509-1353811636618.png" width="2153px" /></div>



|Example input |Incorrect example |Correct input |
|---|---|---|
|Case 1 |If the monitoring target is BytePlus, entering only “Volcano” may cause the model to interpret it as a literal volcano. Similar ambiguity can also happen with names like “Coze,” which may be interpreted as a clothing button. Vague input like this can easily lead to misunderstanding by the model. |Specify the exact subject to be monitored so the model can clearly understand the request. |
|Case 2 |Although “automotive industry information” is entered, it does not specify the sentiment direction or the exact content to monitor, which creates significant difficulty for the model in understanding the intent. |Clearly write “positive information about the automotive industry,” specify the sentiment direction, and list the content to monitor, so the model can understand the monitoring intent more accurately. |
|Case 3 ||Alternatively, provide a longer and clearer input, for example: “I am an automotive industry solutions analyst at BytePlus. I want to monitor the latest progress, case studies, and updates related to BytePlus’s automotive industry solutions, so that I can conduct an overall review and evaluation.” |


&nbsp;

<span id="q3FZ4PeU"></span>
## Intent clarification

To better understand the monitoring requirements, the right side of the page displays five corresponding fields to further help confirm intent. These fields correspond to Subjects, Topics, Sentiment, Locations, and Sources. The above information will directly affect the presentation and expansion of subsequent subscription keywords and subscription scope.


| |Intent example |
|---|---|
|Platform display |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120511-1654107403874.png" width="1927px" /></div><br> |
|Notes |\- Subjects and Topics continue from the subject content entered at the start of monitoring, while also incorporating any additions or edits made by the user during intent clarification. If associated entities, related companies, or monitoring directions are involved, they can be added directly in the input field or adjusted later in keyword settings.\- The monitoring scope is divided into positive, neutral, and negative. The product first presents the intent based on the user input, and later sentiment analysis of monitored content will be evaluated and output from the perspective of the monitoring subject.For example, if the monitoring subject is Brand A and Brand B is a competitor of Brand A, a piece of content may compare Brand B’s product with Brand A’s and indicate that Brand B is better than Brand A. Although the sentiment of the content itself is positive, the model will assess it as negative information from the perspective of the monitoring subject, Brand A.\- The content scope involves publishing location, POI location, and mentioned location. If no selection is made, all regions are included by default.\- Sources are displayed first at the platform level. Some platform categories include secondary site distinctions, which can be selected based on actual needs. |


&nbsp;

<span id="r3xZiBpP"></span>
## Optimization of the data monitoring plan

The Data monitoring plan directly affects how subscription results are presented. At this stage, it consists of data retrieval and relevance assessment.


* Data retrieval follows a logic similar to traditional keyword\-based subscription used by information providers. By listing keywords and adding keyword matching rules, it helps address issues such as incomplete source coverage, insufficient rewrites, and limited expansion.

* Relevance assessment uses the clarified intent from earlier steps as the basis for relevance judgment. Agent experts then perform relevance labeling to produce the final monitoring data. More examples can also be provided to help Agent experts further improve understanding and learning.



| |Incorrect example |Correct input |
|---|---|---|
|Data retrieval rules |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120511-495669780128.png" width="1929px" /></div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120510-1609276842657.png" width="1929px" /></div><br> |
|Notes |If the monitoring requirement is BytePlus automotive industry case studies and best practices, but during data retrieval only BytePlus and Volcengine are used for recall, this will inevitably lead to missing related terms and incomplete results. |Add related companies and products under the monitoring subject, such as Doubao large model, audio and video model, and BytePlus ModelArk, to make the original data retrieval scope as complete as possible. |



|Relevance assessment |Incorrect example<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120510-1712528333216.png" width="1928px" /></div><br> |Correct input<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120511-277808014116.png" width="1925px" /></div><br> |
|---|---|---|
|Example input |**Specialized monitoring of automotive customer case studies and best practices related to BytePlus** \n\n**Monitoring target:**  Information related to **BytePlus** in the **automotive industry** \n\n**Core objective:**  Capture customer case studies and best practices of BytePlus in the automotive industry to demonstrate its application achievements and value in this field. \n\n**Summary:**  The user wants to monitor positive information related to BytePlus customer case studies and best practices in the automotive industry.<br><br> | **[Overview]** <br><br>Comprehensive reputation and market dynamics monitoring for Seedance series models and associated AI video creation entities.<br><br>&nbsp;<br><br> **[Entity Definition & Exclusions]** <br><br><br>* **Core Monitoring Entities**: Seedance, Seedance 2.0 (ByteDance's AI video generation models); associated entities: AI video generation, AI video creation, Kling (Kuaishou AI video model), Veo (Google AI video model), Sora (OpenAI AI video model)<br><br>* **Exclusions**: No other entities outside the above list are included in monitoring.<br><br><br>&nbsp;<br><br> **[Monitoring Dimensions]** <br><br><br>1. Product Performance Comparison: Head\-to\-head test results, benchmark reviews, user experience contrasts between Seedance series and Kling, Veo, Sora<br><br>2. Feature & Capability Discussions: Function updates, unique technical advantages, limitation exposure of all monitored entities<br><br>3. User Feedback & Adoption: Real\-user reviews, enterprise workflow integration cases, usage volume statistics<br><br>4. Industry Positioning: Media coverage, analyst evaluations, market share and niche analysis of Seedance in the global AI video creation landscape<br><br><br>&nbsp;<br><br> **[Summary]** <br><br>Target entities: Seedance, Seedance 2.0, AI video generation, AI video creation, Kling, Veo, Sora. Full monitoring covering product performance, feature dynamics, user feedback and industry positioning dimensions. |
|Notes |\- It only restates the previous intent and content, without adding more useful information. \n\- The overall description is too broad, or the user simply proceeds with the generated content without further refinement. |\- Providing representative examples helps improve understanding and also clarifies what should be excluded to reduce irrelevant information. \n\- At this stage, Agent experts are relied upon to judge content relevance. Because the results may still be somewhat divergent, the scope of attention may expand. Therefore, users are advised to clearly emphasize the required content boundaries and focus areas at this stage, so as to reduce hallucinations and unnecessary expansion. |


<span id="ijiLCFLx"></span>
## Further calibration through preview data

Preview data is generated based on all previous steps, including monitoring content input and intent clarification, and traces back part of the real data from the past seven days according to subscription rules and relevance analysis. Except for publication time, which may differ from the actual monitoring period, all other content is consistent with the actual monitoring setup.

Therefore, the preview data presented here can help accurately determine whether the final results of the monitoring task will match expectations.


|Example |Notes |
|---|---|
|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260603120511-1665207475432.png" width="1930px" /></div><br> |You can use the **AI alert rationale** to understand why the content was pushed. By matching the push reason against the monitoring intent, you can determine whether the result fits the requirement. If the AI alert rationale does not match the intended scope, the monitoring content can be adjusted further to clarify the requirement. |


<span id="aECSBrLh"></span>
## Summary

During the creation of a Market Insights Agent Monitoring task, Agent experts break down the user’s intent based on the input, generate a subscription keyword monitoring plan, and complete relevance assessment. However, monitoring preferences and requirements vary across industries and scenarios. Internal testing shows that, within a reasonable number of rounds, multi\-turn intent clarification produces better intent understanding than a single one\-time input. Therefore, during configuration, users are advised to interact with the system multiple times in natural language to refine and confirm requirements, so as to achieve the best possible monitoring results.
