---
title: "AgentKit Memory overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Memory_overview"
---

<span id="EmOtblam"></span>
## What is AgentKit Memory?

AgentKit Memory is an enterprise\-grade long\-term memory management component provided by BytePlus for AI agents. It integrates with mainstream memory frameworks  through a unified interface, addressing the challenge of memory persistence and reuse across sessions and instances. AgentKit Memory enables agents to maintain continuous context awareness, deliver personalized interactions, and support long\-term autonomous learning.

<span id="89bfgIf5"></span>
## Core capabilities and advantages


* **Unified memory interface**: AgentKit Memory supports integration with backends such as mem0 and Viking, reducing replacement and upgrade costs.

* **Long\-term memory generation and retrieval**: AgentKit Memory persists cross\-session information so that agents maintain context continuity across multiple turns and sessions.

* **Flexible memory extraction strategies**: AgentKit Memory combines preset strategies and custom prompts to cover scenarios such as summarization, preferences, and semantic facts.

* **Enterprise\-grade governance capabilities**: AgentKit Memory provides persistence, cross\-instance sharing, monitoring, and access control, making it suitable for production environments.


<span id="oXQ7WuRi"></span>
## Typical scenarios


* Role playing: An N\-dimensional (scalar + vector) retrieval architecture helps achieve precise memory for role settings and multi\-user interactions.

* Marketing recommendation: Custom profile entities are set to build a dynamic user memory, enabling end\-to\-end personalization from conversation tagging to precise targeting.

* Education companion: Create a personalized learning loop of "conversation \- practice \- consolidation" based on structured knowledge memory, and user proficiency tracking.

* Hardware products: Implement layered memory capabilities in hardware devices and enable long\-term storage of user profiles and key events to deliver a dedicated "user\-aware" experience.


<span id="FCW0T871"></span>
## Core features


|**Feature module** |**Description** |**Collaboration with AgentKit** |
|---|---|---|
|**Memory extraction strategy configuration** |Preset policies: Session summary, user preferences, semantic summarization, and support for custom prompt policies. |Defines "what to extract" and aligns with the presets of AgentKit's scenario\-based templates (customer service, approval, or knowledge Q&A) |
|**Memory write** |Automatic and manual triggering; asynchronous extraction that does not block conversations; structured storage after LLM compression. |Defines "how to extract and where to store". Writing does not block the AgentKit Runtime main chain. |
|**Memory retrieval and recall** |Session preloading/on\-demand loading; scalar filtering combined with hybrid vector retrieval; **re\-ranking, time decay, and conflict resolution**. |Fused ranking in the same pipeline as **AgentKit Knowledge**: AgentKit Memory provides user experience, while AgentKit Knowledge provides organizational knowledge. |
|**Memory analysis and observability** |Extraction success rate, recall hit ratio, average latency, and error rate; **reuse AgentKit platform observability capabilities**. |Only covers memory\-specific metrics, avoiding duplication of general AgentKit platform metrics. |


<span id="ALWjvR5n"></span>
## Procedure


1. [Import memory](https://docs.byteplus.com/en/docs/agentkit/Importing_memories): First, configure and build the memory retrieval policy in the Viking console, then import the corresponding memory into AgentKit.

2. [Integrate the memory into an agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_memories_in_agent): Bind the target memory using canvas\-based visual orchestration or API\-based coding, and configure the memory write triggers and memory recall modes.

3. [Debug memory extraction and recall](https://docs.byteplus.com/en/docs/agentkit/Memory_retrieval): Use the same user ID to conduct multi\-round conversation tests, verify cross\-session memory retention, and adjust memory strategy parameters as needed.

4. [Publish the agent service](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes): Save all configurations and publish the agent version, then perform end\-to\-end conversation verification after the agent is published.

5. [Perform maintenance and iteration](https://docs.byteplus.com/en/docs/agentkit/Observability-): Use the unified observability dashboard to monitor memory chain metrics, perform memory correction and cleanup as needed, and switch the underlying memory backend without code changes.
