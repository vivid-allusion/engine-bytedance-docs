---
title: "Register External Agents"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Register_External_Agents"
---

The agent center is located at the unified agent management entrance. You can register Coze, HiAgent, Dify and other platforms or high\-code developed agents into the agent application platform and be called by the intelligent master control or autonomous planning agent. You can also build your own autonomous planning agent with React and Rewoo architectures. External agents need to be registered with the intelligent master before they can be dispatched. This article mainly introduces how to register external agents.

<span id="d7bde324"></span>
# Register external agents

You can register Coze, HiAgent, Dify and other platforms or high\-code developed agents with the agent application platform, and be called by the intelligent master control or autonomous planning agent.


1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. In the left navigation bar of Marketing Interactive Assistant, select **Agent Center** and click **Register External Agent** in the top right corner of the page.

3. In the **new external agent** pop\-up window, configure the relevant parameters of the agent, and then click **Save** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/030ed81ffc374bceaccc78db2809a806~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |parameter description |
   |---|---|
   |Agent name |Agent name, within 50 characters. |
   |describe |The function range of the agent, within 200 characters. |
   |Agent access URL |URL address of the agent, API call address of the agent |
   |APP ID |Agent ID |
   |API Key |Fill in the API key. Scheduling agents via API Key. |
   |source |Select the source of your agent. Used to distinguish between different agent invocation protocols, the following protocols are supported. If the self\-developed agent is not in the following scope, you need to adapt to the standard protocol of the platform and choose other.<br><br><br>* Hiagent\-conversation: a conversation agent built by Hiagent<br><br>* Hiagent\-conversation flow: a conversation flow agent built by Hiagent<br><br>* Hiagent\-process orchestration: a process orchestration agent built by Hiagent<br><br>* Dify\-Conversation Stream: A Conversation Agent Built by Dify<br><br>* Dify\-Agent: Agent built by Dify<br><br>* Dify\-Workflow: A workflow agent built by Dify<br><br>* Public Cloud Coze\-Agent: An agent built by Public Cloud Coze<br><br>* Public Cloud Coze\-Workflow: A Workflow Agent Built by Public Cloud Coze<br><br>* Public Cloud Coze\-Dialogue Flow: A Dialogue Agent Built by Public Cloud Coze<br><br>* Other (SSE protocol conversation type): Agents built by other development platforms need to be adapted to the SSE protocol of the master control |
   


<span id="b961b6cc"></span>
# View agent

In the **Agent Center** of the Marketing Interactive Assistant, the card list displays all registered external agents and self\-built self\-planning agents, distinguished by card labels.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad32e259b3274826b61bfd842fafba18~tplv-goo7wpa0wc-image.image) </span>

<span id="c67557f1"></span>
# Editing agent

Click **Edit** of the corresponding card in the agent center to modify the name, description, URL, APPID, source and other information of the external agent.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4c89e95a2ca4c4faae46f050b37e84d~tplv-goo7wpa0wc-image.image) </span>

<span id="72e8b617"></span>
# The limited viewership of agents

External agents support limited viewership of QPS, error codes, and error messages.


1. Click on the \*\*limit viewership of \*\*the corresponding card in the Agent Center.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/891b8b43c9c64725bf81363e85d22430~tplv-goo7wpa0wc-image.image) </span>

2. In the **limit viewership of settings** dialog box, complete the following configuration and click **save** .

   * **QPS** **Configuration** : Maximum number of requests per second/minute, set to null to indicate unlimited. Units can be set **per second** or **per minute** .

   * **Error code** : Custom error code that triggers limit viewership of, defaults to 429.

   * **Error message** : Customize the error message that triggers limit viewership of, the default is "There are too many visitors at present, please try again later".
