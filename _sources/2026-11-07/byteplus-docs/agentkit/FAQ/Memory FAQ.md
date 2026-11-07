---
title: "Memory FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Memory_FAQ"
---

<span id="b1iJQY3u"></span>
## Why is previously added memory content not retrievable?

If one memory content is added for the first time, the memory database needs 3 to 5 minutes to build an index. Thus, the result cannot be retrieved immediately. Please wait patiently for a few minutes, and perform retrieval after you see the corresponding event in the memory.

If memory contents are added multiple times, please confirm whether the same session_id is used when the AddSession interface is called. If the same session_id is used, the new session will overwrite the user profile and events of the original session.

If the above reasons are excluded, please provide feedback to the product and R&D team for troubleshooting.

<span id="TrWRykQD"></span>
## What is a reasonable number of messages to write via the AddSession interface at one time?

We recommend accumulating multiple rounds of conversation before calling AddSession to avoid higher costs and poor extraction performance from writing too frequently. Currently, the memory supports a maximum of 100 messages per write. We recommend that you write about 100 messages at a time for the first attempt, and then adjust based on the results and business needs.
