---
title: "Marketing Interactive Assistant Overview"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Marketing_Interactive_Assistant_Overview"
---

The marketing interactive assistant is a unified agent that assists enterprises in internal or external marketing. In multi\-intent scenarios, it can automatically generate execution plans based on hit intentions, and dispatch corresponding agents and tools to reply to questions, realizing intelligent Q & A, personalized recommendation, and other capabilities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a17c92b0b44aca9bb012d6316dfdf5~tplv-goo7wpa0wc-image.image) </span>

<span id="b9ef40d5"></span>
# Function introduction

The marketing interaction assistant is the "smart brain" provided by Volcano Engine for marketing conversation scenarios. It effectively solves the problems of entrance dispersion, memory isolation, and collaboration inefficiency encountered by enterprises in AI marketing scenarios by integrating the following functions, and provides powerful intelligent support for increasingly complex marketing business scenarios.


* Intent Planning Engine: Customize planning intentions according to business needs, decompose, refine, and organize vague goals into concrete executable plans.

* Agent Center: A unified management center for multiple agents within and outside the enterprise.

* MCP tool: Access OpenAPI to MCP, register MCP Server, and manage it uniformly to support agent calls.

* Enterprise Knowledge Engine: Provides a source of enterprise knowledge for marketing interaction assistants. Please see for details [Overview of Enterprise Knowledge Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_Enterprise_Knowledge_Engine).


The product architecture diagram is as follows, and the red box is the marketing interactive assistant part.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e78740b4ea3a43d89a2353935b42b1eb~tplv-goo7wpa0wc-image.image) </span>

<span id="2333b058"></span>
# Functional features


* **High\-precision intent recognition**

   Based on Query rewriting and mixed matching technologies, the accuracy of intent recognition is improved, providing users with a unified and intelligent interaction portal.

* **Unified memory management**

   Memory is the concept of maintaining state during the interaction between users and language models. A unified memory management system is the core foundation for agents to implement advanced intelligent behaviors such as long\-term planning, task follow\-up, and autonomous learning.

* **Agent autonomous planning**

   In the face of multi\-intent complex problems and dynamic uncertain usage scenarios, autonomous planning capabilities can endow agents with stronger autonomous decision\-making capabilities, ensuring that tasks can be executed efficiently and accurately.


<span id="1fb876c2"></span>
# Application scenario

Marketing Interactive Assistant is suitable for a variety of marketing business scenarios, providing a variety of capabilities including recognizing user purchase intentions, displaying customer portraits in real time, automatically generating marketing messages, intelligent product recommendations, and intelligent conversation analysis.

**Example of enterprise external marketing scenario**


* Financial industry: Provide AI investment advisory applications to provide professional financial analysis and interpretation services.

* Automotive industry: Provide brand\-specific AI assistants, providing 7 × 24\-hour model introductions, configuration explanations, test drive appointments, and other services.

* Internet of Things:

   * AI ordering assistant, through multiple rounds of dialogue and long\-term memory to understand user requests and preferences, to provide personalized ordering services.

   * AI intelligent shopping guide, understand user requests through multiple rounds of dialogue, and provide personalized product recommendations.

* General: AI intelligent Q & A customer service, based on users' online questions, combined with personalized user portraits and corporate knowledge, to provide personalized solutions.


**Example of an enterprise internal assistance scenario**


* Financial industry: Empower first\-line account managers or investment advisors within the enterprise to provide real\-time user portrait analysis, product recommendation speech, professional market interpretation and asset allocation plan generation.

* Automotive & Internet of Things industry: Empower customer service or sales personnel within the enterprise to generate auxiliary speech skills through real\-time knowledge recall, and obtain potential business opportunities based on chat content to make active product recommendations.


<span id="b64361c2"></span>
# Term explanation


|**noun** |**term explanation** |
|---|---|
|intent |Each of the user's queries contains one or **more targeted goals, which are called user intentions** |
|intent planning engine |As a unified entrance, it accepts user queries and configures end\-to\-end services for **identification\-planning\-execution\-output** according to intent |
|intent configuration |Define a scene scope by means of natural language or business rules, and when the directional target of the user query hits the scope, the execution action configured by the intent will be executed |
|intent priority |In the actual business implementation, it is found that the ideal clean (clear boundary) state is often not achieved between intentions. From the business perspective, there is a tendency to choose such conflicting intentions, and this tendency rule is the priority of intentions. When multiple intents are hit and the reasons for the hits are similar, the higher the priority, the easier it is to be selected |
|composite intent |A user's query may contain multiple directed targets (intents), and a query for such multiple directed targets is called a composite intent. The sub\-intents of compound intents have different hit causes, and intents with similar hit causes need to be filtered and only one is retained.<br><br>> For example: Help me see how XX is doing recently, do you want to sell it?<br><br>> Include intentions: [XX market analysis], [XX position diagnosis] |
|idea map |In a composite intent scenario, the user must have a goal with the highest priority, which becomes the idea map.<br><br>> For example: Help me see how XX is doing recently, do you want to sell it?<br><br>> Idea map: XX position diagnosis |
|Collaborative intent |In a composite intent scenario, other hit intents outside the idea map are called cooperative intents. The execution results of the collaborative intent will be used as supplementary information to the idea map and will be merged when reporting the output.<br><br>> For example: Help me see how XXX is doing recently, do you want to sell it?<br><br>> Collaborative Intent: XX Market Analysis |
|autonomous planning |Autonomous planning refers to the ability of an agent to independently disassemble tasks around the goals in the user query after receiving the user query, generate action paths based on selectable tools (sub\-Agent or MCP tools), and perform execution to generate answers |
|thought chain |The methodological experience of business precipitation is used to guide agent generation planning with autonomous planning capabilities. An agent can have multiple thinking chains, and flexibly choose the appropriate thinking chain based on practical problems |
|external agent |Agents developed outside the agent application platform may be built by low\-code open APIs such as Hiagent and dify, or they may be self\-developed high\-code agents. The external agent can access the agent center by calling the address + key, and be managed uniformly by the master control. Agents that are currently compatible with Hiagent, Coze, and Dify platforms, and agents developed on other platforms or high\-code need to be adapted according to the SSE protocol of intelligent master control (about 0.5\-1 pd workload) |
|autonomous planning agent<br><br>(Thinking\-Action Type) |An architecture of autonomous agent planning in which the agents interlace thought (reasoning) \-action (wanting to do it one step at a time) and continuously adjust subsequent execution strategies based on action feedback. Suitable for scenarios with few tools, flexible processes, real\-time feedback, and no complex planning required |
|autonomous planning agent<br><br>(Planning \- Action) |An architecture of autonomous planning by an agent. The intelligent experience of this architecture forms a complete execution plan, and then executes it according to the planning steps. The whole process is guided by a "clear planning path". It is suitable for complex tasks with multi\-tool collaboration, clear goals, and high process integrity requirements. |
|cache |Cache is a kind of track memory that stores the execution track (thinking process, planning, etc.) during the execution of the agent, and then directly reuses it without regeneration, which improves the speed of problem solving and reduces the consumption of computing power resources. There are different meanings in autonomous planning agent and intelligent master control scenarios<br><br><br>* Autonomous planning agent: The cache is the execution planning step output by the agent, and only the steps are stored without storing parameters;<br><br>* Intelligent master control: the cache is the recognition map of the query\-intent, and the query is the rewritten standard query, which is convenient for generalization and recognition. The hit cache can directly match the intent for execution; |


<span id="efd4a488"></span>
# Operation process

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid compatibility issues, we recommend that you use the latest version of Google Chrome browser to access the platform.</div>



1. New agent, support registration of external agents or new autonomous planning agents:

   * Register the external agent to the intelligent master control, please refer to the specific operation [Register External Agents](https://docs.byteplus.com/docs/dataagent/Register_External_Agents).

   * New autonomous planning agent to intelligent master control, please refer to the specific operation [New Autonomous Planning Agent](https://docs.byteplus.com/docs/dataagent/New_Autonomous_Planning_Agent).

2. Create the agent of the intent planning engine, orchestrate the agent and configure the intention, and determine which agent should be used for the user's intention. See the specific operation [Intent Planning Engine](https://docs.byteplus.com/docs/dataagent/Intent_Planning_Engine).

3. Create a good intention planning engine, which can be used with external systems through APIs and other forms. If you have specific needs, please contact Volcano Engine technical support.

4. Other operations:

   * Store memory data, including the memory retrieval strategy and the details of the extracted memory, see [Session Memory](https://docs.byteplus.com/docs/dataagent/Session_Memory).

   * Register the MCP tool on the platform to use the agent, see for details [MCP](https://docs.byteplus.com/docs/dataagent/MCP).

   * View session details and records of intent hits, see [Session Management](https://docs.byteplus.com/docs/dataagent/Session_Management).

   * Create a knowledge base and build an intelligent Q & A assistant, see for details [Overview of Enterprise Knowledge Engine](https://docs.byteplus.com/docs/dataagent/Overview_of_Enterprise_Knowledge_Engine).


<span id="89e8679c"></span>
# Contact Us

If you are interested in the product or need to know more product information, you can [consult immediately ](https://www.byteplus.com/en/contact-us).
