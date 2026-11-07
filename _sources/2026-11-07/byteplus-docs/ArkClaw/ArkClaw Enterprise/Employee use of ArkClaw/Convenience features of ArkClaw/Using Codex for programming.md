---
title: "Using Codex for programming"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_Codex_Programming"
---

Codex is the code runtime capability built into ArkClaw. It runs directly within ArkClaw and shares the same conversation context and memory as ArkClaw. Designed for development execution scenarios, Codex is suitable for continuously completing tasks such as code generation, script execution, file modification, and engineering operations within a single session. Simply describe your requirements in natural language to improve the efficiency of development\-related tasks.

<span id="PLxiX7SV"></span>
## Differences between Codex and ArkClaw

ArkClaw is geared toward general\-purpose task comprehension, information organization, problem analysis, and context collaboration. It is suitable for understanding requirements, breaking down problems, structuring ideas, and formulating solutions. Codex, on the other hand, is geared toward development action execution. Once the objective is clearly defined, Codex handles concrete tasks such as writing code, running scripts, modifying files, and performing engineering operations.

Codex and ArkClaw are not interchangeable. They are complementary and work in sequence. In a complete development workflow, ArkClaw is more suitable for the "understand the problem, define the goal" phase, while Codex is more suitable for the "execute changes, drive implementation" phase. Because Codex and ArkClaw share the same conversation context and memory, you can complete the entire process from problem discussion to task execution within a single session.

<span id="SWderehA"></span>
## Usage notes


* ArkClaw version: Version 1.3.3 or later is required. [Upgrading ArkClaw version](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_).

* ArkClaw specification: If you are using an ArkClaw Starter instance, certain Codex features may be limited due to instance configuration constraints. We recommend that you contact your administrator to upgrade the instance to **Standard edition** or higher, or [create a new instance with higher specifications](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_#SdWGV7CH) to access the full feature set.

* Model: The ModelArk Coding Plan, or the Deepseek v4 model from the "Foundation models" must be configured. If the current ArkClaw has not been configured with either of the above models, contact your administrator to configure it.


<span id="f4M9cQCZ"></span>
## Enable and use Codex


1. Open a browser, enter the ArkClaw login link in the address bar, and press the "Enter" key.

2. Switch to the target ArkClaw page.

3. If multiple agents have been added to your ArkClaw, switch to the target agent.

4. At the bottom of the chat box, select "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a517fa4c89e7fae20c2a9a06333a9f13.png) </span>\> Codex", and enable **Codex**.

   > If the system prompts you to upgrade ArkClaw when you use Codex for the first time, click **Upgrade now** to complete the upgrade, and then re\-enter the target session and enable **Codex**.   
   

5. If the  **"Codex mode enabled"**  message is displayed, Codex is enabled as expected.

6. After enabling **Codex**, you can initiate development\-related tasks directly in ArkClaw. Codex continues to process requests based on the current session context and memory. You do not need to switch to a separate terminal page or re\-explain background information that has already been clarified in the current session.

   > If your goal is still in the understanding, comparison, or decision\-making phase, we recommend that you use ArkClaw to clarify the problem and define the objective first. If your goal has moved into the execution phase, Codex is typically the more suitable entry point. This helps maximize the collaborative value of ArkClaw and Codex within the same workflow.   
   

   Example: Help me write a Python script that reads a CSV file and collects statistics on each column.


&nbsp;

<span id="eWDR2AmZ"></span>
## Disable Codex

After Codex is disabled, subsequent instructions will be processed in ArkClaw's default mode. However, the context generated during the session, including conversation history, file background, and memory, is retained and remains available for reference in subsequent interactions.


1. At the bottom of the chat box, select "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a517fa4c89e7fae20c2a9a06333a9f13.png) </span>\> Codex", and disable **Codex**.

2. If the  **"Codex mode exited"**  message is displayed, Codex is disabled as expected.


&nbsp;
