---
title: "Importing memories"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Importing_memories"
---

You can import an existing memory in [Viking](https://console.byteplus.com/vikingdb/memory) into AgentKit with one click. This saves you from rebuilding user profiles and session memory from scratch in AgentKit, allowing you to complete environment setup quickly. This topic describes how to import an existing memory in the AgentKit console.

<span id="EK3vbFEk"></span>
## Usage notes


* An imported memory can only be used within the AgentKit platform. Modifying its strategy on the AgentKit platform is not supported. To modify its strategy, delete it, update the memory strategy on the source platform (mem0/Viking), and then import it again.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the memory has already been integrated into an agent, after importing it again, you must also update the environment variables related to that memory in the agent runtime. Otherwise, the agent continues to use the old memory configuration, <strong>causing memory retrieval results to be inconsistent with the latest strategy.</strong>   </div>
   

* Cross\-region import of Viking memories from the China (Hong Kong) region is supported.

* After an existing memory is imported, only two memory retrieval strategies are supported: "User preference" and "Session summary", which correspond to "Profile rule" and "Event rule" in the original memory, respectively.


<span id="G7SQFBCG"></span>
## Prerequisites

The Viking memory to be imported has been initialized on the source platform and its status is **Built successfully**.

<span id="XmDE5dIL"></span>
## Billing

When you import and use a Viking memory in AgentKit, **the Viking memory service charges fees separately based on actual usage**. AgentKit does not charge or collect these fees. For details, see [Viking memory billing instructions](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_VikingMem).

<span id="hBLkVxYU"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Memory".

3. Click the "Import memory" button and select "Viking".

4. In the list, select the memory with the status "Ready" and click the "Import" button to complete the operation.


<span id="fSgZ54Ha"></span>
## What to do next

After the memory is imported, you can integrate it into the agent to retain context, knowledge, and user preferences across sessions. For details, refer to [Integrating memories in agents](https://docs.byteplus.com/en/docs/agentkit/Integrating_memories_in_agent).
