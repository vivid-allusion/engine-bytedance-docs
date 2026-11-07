---
title: "Obtain Conversation AI Task Events"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1798101"
---

After calling the StartVoiceChat API to start a task, you can use server\-side callbacks to obtain real\-time updates on task status changes (such as task start and end), resource usage, and error information, enabling refined task monitoring and troubleshooting.

## Use cases

* **Monitor task status**

   By monitoring the status of AI voice chat tasks, you can capture key milestones such as when the user finishes speaking or when the AI completes its response. This allows you to add custom business logic, for example, recording task duration, updating client UI status, or triggering downstream data analysis processes.

* **Analyze server\-side processing time**

   By comparing timestamps from different status callbacks, you can analyze the processing time of each core stage—ASR, LLM, and TTS—providing data support for optimizing performance and user experience.

* **Obtain task usage**

   Obtain usage information for TTS, LLM, and other resources in the voice chat task.

* **Detect incomplete LLM responses**

   Receive an `llmIncomplete` event when the LLM response triggers content filtering or reaches a model output or context length limit. Use `ExtraInfo.FinishReason` to distinguish the cause. When the value is `contentFilter`, Conversation AI also removes the affected round from the LLM context used in subsequent rounds.

* **Troubleshoot task errors**

   When an AI voice chat task encounters an exception, the callback provides error codes and error information to help you quickly identify the root cause of the issue.

## Implementation

1. Go to [RTC Console-Settings](https://console.byteplus.com/rtc/cloudRTC?tab=callback) and select **Callback**.

2. Click **Add Configuration** and fill in the relevant parameters as guided on the page. For **Callback Event**, select **VoiceChat**.

   > **Tip**

   > Unless you have special requirements, do not configure a business identifier; otherwise, you may not receive callback messages properly.

After configuration is complete, when the AI voice chat task status changes, the LLM response ends incompletely, or an error occurs, the configured URL will receive a `VoiceChat` event (in JSON format). See details in [Events and Error Codes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1928198).
