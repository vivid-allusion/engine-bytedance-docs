---
title: "View GenAI data outbound logs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/genai-data-outgoing-logs-view"
---

GenAI data outbound logs record policy matches when employees submit sensitive text to AI apps or large language model APIs. The logs show who submitted the text, which app or model provider received it, which sensitive data was matched, and whether the current conversation turn was blocked.

<span id="doxcnIXDrEymaFr21r5GfBcmi4f"></span>
## Log scope

When text that an employee sends to an AI app or large language model API matches a GenAI data protection policy, view the related logs here. The logs help you understand what sensitive information was sent and whether the current conversation turn was blocked. The available conversation content varies by action:


* **Audit**: The current conversation turn was not blocked by this policy. You can view the user prompt, subsequent reasoning process, tool calls, and AI response to understand how the sensitive information was used in context.

* **Block**: The current conversation turn was blocked by the policy. You can view the user prompt that triggered the policy. The log does not include subsequent reasoning processes, tool calls, or AI responses.


Use the **matched object** to confirm whether the employee used an AI app or a large language model API. For example, when DeepSeek is used, the log distinguishes between "AI app: DeepSeek web version" and "model provider: DeepSeek".

<span id="doxcnPqbuwVf2snoV6Kf5e5RTHn"></span>
## Prerequisites

A GenAI data protection policy has been configured and enabled, and an employee text outbound event has matched the policy and reported logs. For configuration instructions, see [Configure a GenAI data protection policy](https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy?lang=en).

<span id="doxcnsVV7Hfr9mspXbLq08B7Lab"></span>
## Query logs


1. Log in to the SealSuite Admin Console.

2. Choose **DLP** \> **Investigation Audit** \> **Audit Log**.

3. Switch to the **GenAI data protection** tab.

4. Select **All**, **Audit**, or **Block** as needed, and set the **Trigger Time** and **User** filters. Expand the filters to further narrow the scope by **Role**, **Department**, and **Device**.


The list supports **Columns** to adjust displayed fields. The main fields are described below.


|Field |Description |
|---|---|
|Trigger Time |The time when the sensitive text outbound event occurred. |
|User |The employee who triggered the event and department information. |
|Matched object |Displays "AI app" or "model provider" and the corresponding name. |
|Action |Indicates whether this event was audited or blocked. |
|Sensitive Data |Displays the detected sensitive data and sensitivity level. |
|Trigger type |The behavior detected by this policy is text outbound transfer. |
|Triggered policy |The name of the GenAI data protection policy that triggered this log. |


<span id="doxcnDwNpmbeTeYU2ukNZeJmQyb"></span>
## View log details

In the **Actions** column of the target record, click **Details**. The details entry includes the **Event Details**, **AI Conversation Content**, and **Detailed Logs** tabs. Use these tabs to view reported information for the same event.

During an audit, first check the event ID, trigger time, and matched object. Then use the matched policy, sensitive data, and action to evaluate the result. To investigate specific submitted content, view the records provided in the details.

<span id="doxcnRuvS6psRUeempf7gCb9srf"></span>
### Event details

First view the outbound event and sensitive details to confirm where this submission was sent, which rules it matched, and how the system handled it. Then use the user and device information to locate the initiator.


* **Outbound Event**: View the trigger URL, action, matched policy, associated object, model name, and outbound behavior. The associated object confirms the involved AI app or model provider. The model name helps you further verify the model used for this request.

* **Sensitive Information**: View the text size, matched classification and grading rules, and data sensitivity level to confirm which sensitive data this submission involved.

* **User information**: View the name, department, mobile number, email address, account creation date, expiration time, and account status to confirm the employee who initiated the operation.

* **Device information**: View the operating system, device IP address, device ID, and SealSuite version to locate the endpoint that triggered the behavior.


<span id="doxcn4qAaHPWkD3kXgVomo51PIe"></span>
### AI conversation content

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/swg-ndlp-en-20260923/genai-conversation-en.png) </span>

To check the actual content submitted by an employee, switch to the **AI Conversation Content** tab. The page reconstructs the conversation context based on security audit records and identifies the conversation turn that triggered the event.

Sensitive content in the conversation is hidden by default. An administrator with permission to view AI conversation content can click **View sensitive content**, read the prompt, and then click **Confirm View** to view the conversation text and highlighted matched content. You can use the annotated classification and grading rules and data sensitivity level to verify the sensitive information that triggered the policy.

The system records this unlock and view operation in **Admin Log** to trace who viewed sensitive content and when.

The reporting scope of conversation content varies by access method:


* **AI website**: Reports all content in the conversation, which helps you view the conversation turn that triggered the event in context.

* **Large language model API**: Reports only the conversation content that currently matches the policy. It does not report the complete conversation history.


The action also affects recorded content. When an **Audit** policy is matched, the user prompt, reasoning process, tool calls, and AI response are recorded. When a **Block** policy is matched, only the user prompt is recorded. Subsequent reasoning processes, tool calls, and AI responses are not reported.

The page highlights the classification and grading rules and data sensitivity level only for user prompts that match sensitive information.

<span id="doxcnvDM9c7GMGTt59Q9egHOmre"></span>
### Detailed logs

To further investigate a request, switch to the **Detailed Logs** tab. In **Request Details**, select **Basic Info** or **More Info**, and use the event ID, trigger time, and URL to verify the same request.


* **Basic Info**: Includes request time (timestamp_ms), user (user), status code (status), app host (host), HTTP URL (uri), request method (method), log status (level), request round\-trip time (duration), and User Agent (user_agent). Use this information to verify when the request occurred, the target address, the request method, and the software environment that initiated the request.

* **More Info**: Includes source IP address (sip), source port (sport), request size (size), HTTP version (protocol), protocol (scheme), and gateway intranet IP address (intranet_ip). Use this information to investigate the network connection of the request and the gateway it passed through.


To determine whether the current conversation turn was blocked, check **Action** in the event information. Do not rely only on the HTTP status code or log status.

<span id="doxcnFouqdBXTzv6wanMqwOBB0g"></span>
## Use logs to troubleshoot issues


* **Confirm the action result of an event**: View the action. "Audit" indicates that the current conversation turn was not blocked by this policy. "Block" indicates that the current conversation turn matched a blocking policy. In this case, the log records only the user prompt and does not include subsequent AI responses.

* **Confirm whether the protected object is correct**: Check whether the matched object is an AI app or a model provider, and compare it with the control scope in the policy.

* **Verify whether the rules meet business requirements**: View the matched sensitive data and the corresponding policy. Then check the definitions of the referenced classification and grading rules to decide whether to adjust the rules or the effective scope.

* **Expected logs are not found**: First check filters such as time and person. Then check whether the policy is enabled, whether the employee or device is within the effective scope or excluded, and whether the target app or provider has been selected.
