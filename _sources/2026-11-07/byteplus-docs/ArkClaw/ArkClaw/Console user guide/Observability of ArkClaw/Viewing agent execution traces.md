---
title: "Viewing agent execution traces"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/viewing_agent_execution_traces"
---

The platform supports agent execution trace analysis for conversations in ArkClaw. It tracks the full call chain of conversations, facilitating call relationship querying and chain issue analysis. This topic describes how to view the agent execution traces of a conversation.

<span id="Xy7jkHQr"></span>
## Prerequisites

You have already applied for and created ArkClaw, and initiated a conversation with ArkClaw to process tasks. 

<span id="ZUXkdHFS"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page.

3. At the bottom of the output content, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1799d07f7e7d88379d079c2192304fc2.png) </span> to view the agent execution traces and details.


<span id="imO9MVSa"></span>
## Execution trace diagnosis


1. After you go to the page for viewing execution traces, the system automatically initiates basic diagnosis and provides diagnosis results within 5 seconds. If the "No obvious issues found" message appears, it indicates that the workflow completes as expected without identifiable errors.

2. If the basic diagnosis returns anomalies, click **In\-depth diagnosis** to run comprehensive analysis. The system generates a detailed diagnosis report containing root cause summary, issue list, severity levels, problem descriptions, corrective actions, and expected effects.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The in\-depth diagnosis generally takes 1 to 2 minutes.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In\-depth diagnosis can be triggered only once. Repeated diagnosis is not required.   </div>
   

3. After the in\-depth diagnosis is complete, click the thumbs\-up or thumbs\-down button in the lower\-left corner of the diagnosis result to submit feedback on the result.


<span id="gW9uUljH"></span>
## Execution trace details

The agent execution traces mainly display the following three types of detailed information:

<span id="SKwrFKtD"></span>
### Usage data

The usage data for the current conversation includes the following key metrics:


|Metric |Description |
|---|---|
|Task execution duration |The total end\-to\-end duration from user request initiation to final response completion in the current conversation. It intuitively reflects the response efficiency of a single conversation and acts as a core user experience metric. |
|Model call count |The total number of inference requests initiated to the large model in the current conversation. It reflects the reasoning rounds and decision\-making complexity of the agent in the conversation. |
|Tool call count |The total number of actual tool calls initiated in the current conversation. It reflects the complexity and dependency of tool collaboration in the conversation. |
|Token consumption |The total token consumption of the current conversation (Total token consumption = Input tokens + Output tokens + Cached input tokens). It measures conversation resource consumption. |
|Input token cache hit ratio |The proportion of input token cache hits in the current conversation (Input token cache hit ratio = Cached input tokens/Total token consumption \* 100%). It reflects context reuse efficiency and evaluates cache policy performance. |


<span id="9fEZiDRi"></span>
### Event traces

During the execution of the current conversation, the involved events and their key information, for example: event name, event duration, and token input/output consumption.

<span id="nJePK7EP"></span>
### Event details

Click the target event entry to view the detailed information of the event. You can also click **View raw data** in the upper\-right corner to view the raw data of the event in JSON format.


* User task execution events: mainly include task duration, task details, task results, and other detailed information.

* Agent execution events: mainly include agent duration, task details, task results, and other detailed information.

* Large model call loop events: mainly include large model call loop duration, model information, Harness ID, large model call loop context, large model call loop results, and other detailed information.

* Large model call events: mainly include large model call duration, model information, token input/output consumption, call request termination reason, model call context, the complete process of model output, and other detailed information.

* Tool call events: mainly include tool call duration, tool call parameters, tool call results, and other detailed information.
