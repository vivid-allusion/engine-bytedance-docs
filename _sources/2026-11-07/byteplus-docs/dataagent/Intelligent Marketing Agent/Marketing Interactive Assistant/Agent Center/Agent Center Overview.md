---
title: "Agent Center Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Agent_Center_Overview"
---

The agent center is a unified agent management portal. Users can register agents developed on platforms such as Coze, Hiagent, and Dify or high\-code to the agent application platform, and be called by the intention planning engine or self\-planning agent. They can also build self\-planning agents with React and Rewoo architectures.

<span id="c7729eaa"></span>
# Main ability


* **High Accuracy Intent Recognition, Unified Agent Entry**

   * Unified entrance: Provides a unified interface for users, allowing them to ask their own questions on demand and distribute tasks intelligently without paying attention to the underlying multi\-agent division of labor.

   * Query rewriting: Combining historical session memory, knowledge base information, industry terminology, etc., to optimize and rewrite the user's input content to make the expression of intentions more accurate.

   * Mixed matching mode: the combination of code matching rules and natural language reasoning two kinds of intent matching type, for a specific channel can define the intent by code rules, all queries from the source of the channel point to the specified intent, taking into account the accuracy, stability and scalability of recognition.

* **Domain knowledge enhancement and unified session memory management**

   * Industry terminology maintenance: Support the maintenance of the industry terminology database, allowing large models to "understand" the internal "slang" of the enterprise and improve their understanding.

   * Unified memory management: The sessions of all downstream agents are managed uniformly to achieve cross\-agent memory distribution and break down information barriers.

* **Flexible agent registration and management**

   * Provide standardized interfaces and processes, allowing self\-developed agents to be quickly and cost\-effectively integrated into the master control system, enabling plug\-and\-play.

* **Unified planning, scheduling, and configurable thinking chain**

   * Intelligent planning: When a complex task is identified and multiple intents are hit, the master control agent will automatically disassemble the task, generate an execution plan, and schedule downstream agents according to the plan.

   * Efficient scheduling: Invoke the most appropriate vertical agents on demand and in an orderly manner according to the schedule to execute subtasks and manage their collaboration.

   * Configurable thinking chain: It supports configuring the scenario\-based analysis framework into an analytical thinking chain, and the master control agent schedules and plans according to the constraints of the thinking chain, making the entire planning execution more controllable.

* **Authority control of fine grain (linkage large model security \- zero trust)** 

   * Enables managers to configure permissions for agent invocation tools or querying knowledge on demand. Ensure that Agent operations adhere to preset information policy boundaries, prevent unauthorized access and unauthorized operations, and ensure enterprise information security.


<span id="a5edb02b"></span>
# Core advantage


|Strengths |Business advantage |Technical advantage |
|---|---|---|
|Unified entrance |Improve problem\-solving efficiency: demand\-driven, intelligent master control, autonomous collaboration, multi\-agent to complete complex tasks, and solve the problem of tool fragmentation |Enhance the scalability of the system architecture: The master control\-vertical agent architecture model is clear, making it easy to expand new business capabilities.<br><br>Reduce front\-end maintenance costs: Unify the management of UI/UX for all agents to reduce duplicate development. |
|Flexible configuration |Reduce operating costs: Configurable thought chains and flexible intent\-matching rules enable more agile and cost\-effective adjustments to business logic. |Enhance the maintainability and flexibility of the system: rules and models are separated, logic is configurable, and the system can respond quickly to business changes with less technical debt. |
|efficient collaboration |Improve user experience: Based on complete contextual information, agents can provide more accurate and insightful answers and suggestions. |Implementing state sharing provides a foundation for building more complex cross\-domain applications. |


<span id="22ff4f67"></span>
# Function Overview


|**module** |**function item** |**Function Description** |
|---|---|---|
|Agent Center |external agent registration |Supports the registration of external agents to the master control platform. External agents support three agents built by Hiagent and conversational agents based on the Server Sent Event (SSE) protocol developed by other platforms |
||agent creation |Thinking\-Action: Support agents that configure the ReAct architecture, configure execution tools, planning requirements, reply requirements, and other information, so that the agent has the ability to plan independently. It is suitable for scenarios with few tools, flexible processes, real\-time feedback, and no complex planning.<br><br>Planning\-Action: Support agents that configure ReWoo architecture, configure execution tools, planning requirements, guidance thinking chains, reply requirements, and other information. Enabling agents to have complex autonomous planning capabilities. It is suitable for complex tasks with multi\-tool collaboration, clear goals, and high process integrity requirements.<br><br>Support business personnel to flexibly adjust the analytical thinking chain of agents based on needs<br><br>The thinking chain is a methodological framework for agents to analyze certain types of problems, and is a kind of experience precipitation of business scenarios, which is used to know the thinking and task execution planning of autonomous planning agents. For example:<br><br>Analysis of industry analysis/trend/rise and fall/operation strategy: industry market + industry concept stock market + news search + industry research report (search industry chain, etc.) + industry popular stock market + industry popular ETF market + industry upstream and downstream market.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40b1a6b93cdc436389572260cc6b868c~tplv-goo7wpa0wc-image.image) </span> |
