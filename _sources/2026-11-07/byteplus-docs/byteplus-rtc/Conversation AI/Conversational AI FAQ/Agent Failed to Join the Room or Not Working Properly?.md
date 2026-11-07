---
title: "Agent Failed to Join the Room or Not Working Properly?"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1557772"
---

<span id="problem-description"></span>
## Problem Description

If your AI agent fails to join a room or function correctly despite a successful API call (HTTP 200 status), this guide provides the necessary troubleshooting steps. Follow this document to diagnose whether the root cause is a device issue or a parameter configuration error, and learn how to verify critical parameters like RoomId and UserId to resolve the issue.

<span id="troubleshooting"></span>
## Troubleshooting

You can follow these steps to troubleshoot:

<span id="step-1-identify-the-problem-type"></span>
### Step 1: Identify the Problem Type

Access the [Real-time Conversational AI Web Demo](https://demo.byteplus.com/rtc/solution/aigc?from=doc) to start an AI conversation:


* If you cannot have a normal conversation with the agent, the problem is likely a device issue. Please check if the device is functioning properly.

* If you can have a normal conversation with the agent, the problem is likely an agent API configuration issue. Please verify the parameters in the `StartVoiceChat` API request:

   * Are all required parameters provided?

   * Are `RoomId`, `TaskId`, `TargetUserId`, and `UserId` set according to the [Parameter Assignment Specifications](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70114)? No Chinese characters are allowed.

   * Does the `RoomId` match the one used by the client SDK to join the room?

   * Does the `TargetUserId` match the `UserId` used by the client SDK to join the room?


If the agent still does not work properly after following these steps, contact [Technical Support](https://console.BytePlus.com/workorder/create?step=2&SubProductID=P00000081) and provide the `RequestId` from the OpenAPI request for further troubleshooting.

```Plain

```
