---
title: "How memory works"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/How_memory_works"
---

The core memory workflow consists of two steps: memory generation and memory retrieval.


* Memory generation: During an agent conversation (as configured in code), you can send the session context to the AgentKit memory based on your needs. The memory service then asynchronously **extracts ** and **stores** key memory content automatically.

* Memory retrieval: In the agent code, you can retrieve relevant memories as needed to enhance the personalized interaction and continuous learning capabilities of the agent.


<span id="Jwhrmsmi"></span>
## Memory generation

The memory generation process involves automatically compressing and extracting key information from the context for storage, based on the configured **memory strategy type** and capabilities, such as those of large models and custom operators.

<span id="FoZkaZkp"></span>
### **Memory strategy types**


* **Preset strategies**:

   * Session summary: Summarizes long conversations within a session, such as meeting minutes and study notes.

   * User preference: Records and summarizes user preferences across sessions, such as user behaviors, interaction styles, and habitual choices.

   * Semantic summary: Captures factual information related to the user, such as personal information, important personal details, and professional details.

* **Custom strategy**:

   By defining custom prompts, you can implement custom memory strategies, enabling agents to deliver more comprehensive and customized capabilities.


<span id="WlRwkE5E"></span>
### Memory generation mode

During agent application code integration, memory generation generally supports two modes. Choose based on your agent requirements:


* **Manually triggered**: At the end of an agent session, manually persist a certain range of session data by adding a memory processing operation.

* **Automatically triggered**: Automatically write a specified range of session data into memory when specific nodes are reached (which requires calling the memory write interface in the node callback).


To ensure data security, data isolation is enforced based on dimensions such as session, user, and Agent, as defined in the mentioned memory strategies.

<span id="sstl5bOs"></span>
## Memory retrieval

The configured memory can be used within your agent to retrieve relevant memory contents as needed (via the memory retrieval API). These memory contents are then processed together with the current session's context and system prompt.

During agent application code integration, memory retrieval typically supports two methods. Choose based on your agent requirements:


* **Preloading memory method:**  Memory is retrieved at the beginning of each session. This method is mainly used in multi\-turn conversations and scenarios requiring continuous context (such as customer service or companion robots). At the start of each round, relevant memory is injected into the prompt to ensure low latency and coherence.

* **On\-demand memory loading method:**  With this method, the agent queries and loads relevant memory content into its current context when it deems necessary. This loading method is mainly used when retrieval is clearly required (for example, when the user asks for specific historical information, when executing a task that requires additional data, or when dealing with long lists or large\-scale memory).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Memory extraction involves a certain time delay and may not be completed immediately.</div>


<span id="qQYcjs8G"></span>
##
