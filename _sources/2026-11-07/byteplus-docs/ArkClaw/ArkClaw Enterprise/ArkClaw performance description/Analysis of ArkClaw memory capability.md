---
title: "Analysis of ArkClaw memory capability"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Analysis_of_ArkClaw_memory_capability"
---

This topic introduces the effects of integrating ArkClaw memory with LanceDB **in terms of compatibility, performance, and capability improvement in real business scenarios**.

<span id="oAWQwM3g"></span>
## Background

<span id="cz9xPss8"></span>
### **ArkClaw memory capability**

ArkClaw memory capability is a **BytePlus self\-developed Context Engine** that enables enterprise AI agents to learn and evolve autonomously. It eliminates the traditional AI limitation of context loss per interaction. Through a continuously evolving three\-dimensional profile, i.e., memory, skills, and experience, the agent improves via user collaboration, delivering task execution with **higher accuracy, stability, efficiency, and sustained self\-optimization**. It achieves a **338%**  improvement in task success rate and a **64.7%**  reduction in token consumption on the LoCoMo benchmark. For details, see [Test result](https://docs.byteplus.com/en/docs/394/95152#ryuo57M1).

<span id="eIeVV8iJ"></span>
### **LoCoMo**

**LoCoMo** (Long\-Term Conversational Benchmark) is a public benchmark specifically designed to evaluate the long\-term conversational memory capability of LLMs and intelligent agents. It simulates long\-term human interactions to evaluate whether an agent can sustain memory\-aware conversation grounded in persona and life events. It is used to compare different memory mechanisms across long\-term, multi\-session conversational scenarios in terms of accuracy, factual consistency, temporal/causal reasoning, and multimodal understanding.

<span id="GZSVFTrm"></span>
## Evaluation scope and required capabilities

This test focuses on key business scenarios, including web browsing, retrieval, and complex reasoning. A unified evaluation framework is built upon the LoCoMo public benchmark. By comparing ArkClaw's performance before and after integrating the LanceDB module, the test monitors comprehensive changes in accuracy, latency, and cost, i.e., the three core dimensions, to thoroughly assess the optimization effect on ArkClaw's core business capabilities. This ensures that the test results are objective, reproducible, and relevant to business decisions. This test provides data support and theoretical basis for subsequent decisions, such as solution selection, resource allocation, and canary release.

The **LoCoMo** evaluation framework consists of three core steps: data ingestion, question answering (QA), and result judgment. It focuses on assessing the long\-term conversation capability of LLMs and memory\-enhanced agents. In ultra\-long conversation context scenarios, it focuses on evaluating the capabilities in understanding and recall of factual, temporal, and multimodal information. The evaluation dimensions and scenarios of the standard LoCoMo benchmark are shown in the following table:


|**Evaluation dimensions** |**Scenario/Task type** |**LoCoMo data scale and structural characteristics** |**Core evaluation objectives** |**Required core capabilities** |
|---|---|---|---|---|
|Long\-term conversational memory |Multi\-session long conversation (dual\-agent conversation) |Contains approximately 10 extremely long conversations, each averaging about 300 turns and 9K tokens, spanning up to 35 sessions. Sessions are generated under constraints of persona profiles and temporal event graphs, and are manually verified.<br><br> |Maintains persona and factual consistency across extremely long, multi\-turn conversations, and correctly references and updates historical information in subsequent turns. |Long\-term conversation context modeling, cross\-session fact memory and updating, persona and timeline consistency maintenance. |
|QA and Reasoning |Long\-context question answering (QA) |Constructs 1,540 multi\-type questions based on dialogues, with ground truth answers and annotations containing evidence segments, used to measure the response quality of different models under long\-context scenarios. |Evaluates whether the model can locate relevant segments within extremely long histories and perform various types of reasoning\-based question answering, including single\-hop, multi\-hop, temporal, commonsense, and adversarial reasoning. |Long\-context retrieval and aggregation, multi\-hop reasoning across multiple turns, temporal and causal reasoning, robustness to adversarial questions. |
|Event\-level understanding |Event Graph Summarization |Each conversation is accompanied by an event list for both roles, along with causal and temporal relationship annotations, serving as the ground truth event graph for the event summarization task. |Evaluates whether the model can extract key events from long dialogues and reconstruct a coherent temporal order and causal chain. |Key event extraction, temporal and causal structure modeling, and high\-level semantic compression and summarization based on conversation. |
|Multimodal dialogue |Text and image multimodal dialogue generation |Dialogues may include image sharing and image reaction information. Some extended versions of LoCoMo also provide image\-based visual question answering subtasks to evaluate visual memory and dialogue consistency. |Generates semantically coherent, contextually consistent, and visually aware responses by leveraging historical text and image information. |Multimodal dialogue modeling, visual information memory and retrieval, image\-text alignment, and visual reasoning. |


<span id="2bQkUrj2"></span>
## Models included in the test


* Embedding models: Doubao Embedding model (doubao\-embedding\-vision\-251215), and basic Embedding model (bge\-small\-zh\-v1.5)

* Large language model: doubao\-seed\-2\-0\-pro\-260215


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For detailed test procedures, see <a href="https://github.com/snap-research/locomo">LoCoMo evaluation process</a>. You may also conduct testing based on this document.</div>


<span id="ryuo57M1"></span>
## Test results

<span id="J5348epq"></span>
### Accuracy

This accuracy test covers 1,540 test items from the LoCoMo dataset. By comparing ArkClaw's accuracy performance before and after integrating LanceDB, you can see the improvement of the vector retrieval module in task completion quality. Detailed data is shown in the following table:


|**Accuracy without LanceDB** |**Accuracy with LanceDB** |**Improvement rate** |**Sample size/Notes** |
|---|---|---|---|
|**13.6%**  |**59.68%** <br><br> |**338%**  |**1,540** questions in total |


> Improvement rate = (Accuracy with LanceDB \- Accuracy without LanceDB) / Accuracy without LanceDB \* 100%


**Embedding model**


|Model type |**Accuracy with LanceDB** |
|---|---|
|Doubao Embedding model |59.68% |
|Basic Embedding model |39.87% |


&nbsp;

<span id="0PjAVA3N"></span>
### Token cost

Token cost is a core metric for system deployment and operation. This test focuses on measuring ArkClaw's token consumption before and after integrating LanceDB to evaluate the optimization effect on the system cost. Detailed data is shown in the following table:


|**Tokens without LanceDB** |**Tokens with LanceDB** |**Reduction rate/Cost reduction** |
|---|---|---|
|20958679 |7399781 |Cost reduced by **64.7%**  |


> Reduction rate = (Tokens with LanceDB \- Tokens without LanceDB) / Tokens without LanceDB \* 100%


**Embedding model (Tokens called with LanceDB)** 


|Model type |Total |Input |Output |
|---|---|---|---|
|Doubao Embedding model |33155331 |7399781<br><br> |1163786 |
|Basic Embedding model |58684765 |40260296 |1076335 |


<span id="aXjxkMtE"></span>
## Conclusion

Across **1,540** test items, the integration of LanceDB delivers significant improvements in accuracy, performance, and cost efficiency.

**Improvements**


* **Overall accuracy**: Increased from **13.6%**  to **59.68%** , representing a **338%**  improvement.


**Cost and efficiency**


* **Token cost**: According to the LoCoMo evaluation, LanceDB reduces input token cost by **64.7%.** 


**Model**


* We recommend the Doubao Embedding model. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Space_information#ftsmTKKb).
