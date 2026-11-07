---
title: "Session Memory"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Session_Memory_"
---

Session memory is used to help iDA continue to understand users in different sessions, reduce the cost of repetition, and improve communication efficiency. With this capability, users can record long\-term important content such as personal information, preferences, operation rules, and work habits, and add, modify, or delete them as needed. This document mainly explains the use of session memory, basic operations, and precautions, so that you can get started quickly.

<span id="6612a8a3"></span>
# Prerequisite


* You have successfully logged in to iDA and entered the conversation page that can be used normally.

* The session memory function is turned on; if it has been turned off, it needs to be reopened in the memory management entrance first;

* Long\-term memory is turned on by default. After being turned off, long\-term memory is no longer effective; after being turned on again, the original long\-term memory is restored.


<span id="e5f63438"></span>
# Enter memory management


1. Log in to the BytePlus console and enter the iDA to select the agent.

2. Hover over the user name in the lower left corner of the Q&A interface, and click "Memory Management" in the pop\-up option to enter the memory management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/629546730a4d40a9bbeb8e98262f8f1f~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3b4ceef7e7e43978f1254424c7559ae~tplv-goo7wpa0wc-image.image) </span>


<span id="57e41a3e"></span>
# Use of long\-term memory

In memory management, you can choose to turn long\-term memory on or off. After turning it on, you can manually enter important memories, and the agent will answer each of your questions according to your long\-term memory preferences. The following are instructions for long\-term memory:


* **Switch agent**: At the top of memory management, you can click the drop\-down to switch the agent. After switching the agent, the long\-term memory content corresponding to the selected agent is displayed at the bottom of the page. The long\-term memory of different agents is independent of each other. Please confirm whether the currently selected agent is correct before editing.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/239c8bb9c1b74bbcba8ea0a23061e9d0~tplv-goo7wpa0wc-image.image) </span>

* Edit memory: Click the Edit button at the top right of the memory editor to add, modify or delete memory content in the editor. After editing, click the "Save" button at the top right of the editor to update the memory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7899a0e9b13f4f70a36265554632ed9e~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Sessions generated during closing long\-term memory will not be written to long\-term memory, and historical sessions will not be written backwards after reopening.</div>


* <div data-tips="true" data-tips-type="warning">The current version of long\-term memory does not support automatic retrieval and is only written when the user explicitly requests recording or manual editing.</div>


* <div data-tips="true" data-tips-type="warning">Long\-term memory is suitable for recording long\-term information and is not recommended for writing to one\-time tasks, short\-term schedules, or temporary contexts.</div>


* <div data-tips="true" data-tips-type="warning">When the newly added content duplicates or conflicts with existing memories, the system will verify it and prompt the user for confirmation according to the situation.</div>



<span id="bb0dc2ff"></span>
# Long\-term memory template

You can refer to the following template to maintain long\-term memory content.

```Shell
## Coordination settings
- Call me by「...」
- Maintain the style when replying「...」
- My role in team is「...」
- My main responsibilities in daily work are 「...」
- 「...」

## Background knowledge
- My commonly used abbreviations/terms and their default meanings:「...」
- My frequently used resources（Document / Dashboard / Dataset / Table）：「...」
- The criteria, fields and mapping relationships of interpreting data or metrics:「...」
- 「...」

## Execution guidelines
- I have fixed process instructions and corresponding processing methods:「...」
- I have special task types and rules that must be followed:「...」
- The method I have corrected, and will not be used again in the future:「...」
- 「...」
```


&nbsp;
