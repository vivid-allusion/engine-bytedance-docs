---
title: "Runtime FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Runtime_FAQ"
---

<span id="QJGTWtqu"></span>
## What is the network access mode of an agent runtime created via CLI?

Both private network access and public network access modes are supported.

<span id="geQL9kgz"></span>
## Which configurations cannot be edited after an agent runtime is created?

After creation, the following configurations of the agent runtime cannot be modified: name, associated project, network configuration, and IAM role. For configurations that can be modified, see [Updating runtimes](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime).

<span id="n9LIN0vv"></span>
## Which communication protocols are currently supported by agent runtimes?

AgentKit agent runtimes support three communication protocols: **A2A, MCP, and standard HTTP**. You can use the decorators provided by the AgentKit SDK to quickly adapt agents to the corresponding protocols.
