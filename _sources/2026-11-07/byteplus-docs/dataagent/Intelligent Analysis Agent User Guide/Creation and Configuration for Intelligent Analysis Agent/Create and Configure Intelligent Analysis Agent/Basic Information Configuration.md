---
title: "Basic Information Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Basic_Information_Configuration"
---

This article provides guidance on configuring basic information when creating and setting up an intelligent analysis Agent.

<span id="3bfd9595"></span>
# Background information

The intelligent analysis Agent supports two application types: **web client** and **Lark client**.


* Web client: After the Agent is created and launched, you can use it directly by opening the Agent page in a browser.

* Lark client: After the Agent is created and launched, it is integrated into the Lark application, and you can subsequently use the Agent directly within the Lark application.


To integrate the Agent into the Lark client for subsequent use, in the basic information configuration section, you must complete both the general configuration and the Lark client configuration.

<span id="1020e6d9"></span>
# General configuration


1. Go to the Agent configuration page. For detailed steps, see [Entry point](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures#1b6ae60c).

2. Click "Basic information" in the left navigation bar to enter the basic information configuration page. By default, you are on the general configuration page for basic information, where you can start configuring the Agent's basic information.

   The general configuration includes basic settings, Agent administrators, and the PC client member list. The effects of the basic settings on the left are immediately displayed in the preview on the right, allowing users to adjust the basic settings accordingly.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75100cfb01de4cddaab34a734ed88162~tplv-goo7wpa0wc-image.image) </span>


1. Basic settings.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Avatar |You can define a custom avatar for the agent by clicking the avatar image to upload your own image. |
   |Name, description, and introduction |* You can customize the agent name to identify the agent, and configure a summary description and detailed introduction to help users quickly understand the agent's purpose.<br><br>* When entering detailed introduction content, Markdown format is supported. |
   |User\-visible mode |Configure the scope of features displayed to end users for the agent.<br><br><br>* The configuration results only take effect for end users of the agent. Administrator accounts can access all purchased features of the agent.<br><br>* At least one feature option must be selected from Intelligent Q&A, In\-depth Research, or Insight Report; otherwise, the configuration results cannot be saved. |
   |First\-use mode |After configuration and agent launch, when target users use the agent for the first time, the default selected mode is either In\-depth Research or Intelligent Q&A.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed2b4042cd034f60ab064bcd712d3138~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For introduction and explanation of in\-depth research and intelligent query, please refer to <a href="https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent">Intelligent Query Agent</a> and <a href="https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent">Deep Research Agent</a> respectively.</div><br> |
   |Display analysis parameters |When target users use the agent in Intelligent Q&A mode, configure whether the "Analysis Parameters" section is expanded by default in the query result card. |
   |Enable chart analysis |Configure whether chart analysis needs to be performed simultaneously when using the agent. After enabling this feature, the agent will simultaneously analyze the chart of the query results during the data query process. When returning the agent's answer, the interpretation of the chart will be displayed below the query results chart. |
   |Enable multi\-path execution |After enabling multi\-path execution, during the intelligent query phase, the agent will execute multiple times in parallel (default is three times) to ensure the stability of the results. However, this also incurs performance costs for the agent's operation, such as increased token consumption, parallel processing pressure will increase by about three times, and data query times will be longer. |
   |Enable time engineering |Subsequently, when using the agent, if the problem description involves relative time expressions:<br><br><br>* When this switch is turned on (default), the large model will extract the time range described in the problem statement, and the specific time range will be calculated by the code module. This approach can improve the accuracy of time range\-related calculation results in most scenarios.<br><br>* When this switch is turned off, both extraction and calculation of the time range will be performed by the large model. |
   

2. Agent administrator configuration

   * In a private environment, the default admin user is the Agent administrator. You can enter other usernames in the input box to add users as administrators for the current Agent.

   * Agent administrators have editing permissions for the Agent and can edit, delete, publish, and perform other operations on the Agent.

      It is recommended to plan permission management based on the composition of the Agent's business team, and then configure administrator users according to the permission plan. For specific permission details, refer to [Permission Management](https://docs.byteplus.com/docs/dataagent/Permission_Management).

3. Add Agent members

   Agent administrators can view the member list, add or remove members, and perform other operations here.

4. After completing the above configuration, click the "Save" button in the upper right corner of the page to save the basic information configuration results for the agent.


<span id="7e7da41e"></span>
# Lark client configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65ef11882fc24d089bd99620da7f80c6~tplv-goo7wpa0wc-image.image) </span>


* To integrate the agent for use in the Lark client, in addition to completing the general configuration in the basic information settings, you must also configure the Lark client.

* When configuring the Lark client, you need to first obtain the Lark callback address for the current agent. After completing the integration configuration on the Lark application side, proceed with the configuration operation here for the agent.

   For the end\-to\-end configuration process of the Lark client, see [Lark-Side Intelligent Agent Configuration and Testing](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing).
