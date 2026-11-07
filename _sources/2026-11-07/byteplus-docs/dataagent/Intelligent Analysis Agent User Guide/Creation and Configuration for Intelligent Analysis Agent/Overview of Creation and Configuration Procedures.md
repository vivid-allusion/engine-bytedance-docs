---
title: "Overview of Creation and Configuration Procedures"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures"
---

The Intelligent Analysis Agent supports two application types: web and Lark. There are some differences in the creation and configuration procedures. This article provides a brief introduction to the operation procedures and guidance links for both types. You can review this article before starting operations to quickly understand the workflow and key configuration points.

<span id="ffa3f8c6"></span>
# Operation procedures

Currently, the Intelligent Analysis Agent supports two versions: **web** and **Lark**. The differences are described below.


|Comparison items |Web version |Lark version |
|---|---|---|
|Main differences |After creating the Agent and configuring the dataset and other related settings, you can obtain the web version usage link and open the URL directly in your browser. |Interaction is based on the Lark bot, so you first need to create a Lark bot for the Agent, and then associate the Lark bot with the Agent; after configuration, the Lark version Agent can also be used directly on the web version. |
|Usage process |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b534ba33d94461fb3c1c6babbc07ce8~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2961a98a9f494c39ae0dbceb641460b6~tplv-goo7wpa0wc-image.image) </span> |


<span id="8186d4ef"></span>
## Caution and prerequisites


* Before creating and configuring an agent, you must first complete the purchase and activation of the Intelligent Analysis Agent, create a project, and prepare the data.

   * For detailed instructions on creating a project, see: [Project Information](https://docs.byteplus.com/docs/dataagent/Project_Information), [User Management](https://docs.byteplus.com/docs/dataagent/User_Management).

   * For instructions on preparing data, see: [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview).


<span id="fef5a334"></span>
## Create and configure the Intelligent Analysis Agent

<span id="1b6ae60c"></span>
### Entry point


1. Go to the configuration page of the Intelligent Analysis Agent and click "Create Agent" in the upper right corner to access the initial configuration page for the agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/799ab2a55f5440aeae1cd0b1f9ab01a6~tplv-goo7wpa0wc-image.image) </span>


2. Configure the basic information for the agent, including application name, application description, and administrator. After completing the configuration, click "Save".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c81937f69e04133aa969bfd69c34195~tplv-goo7wpa0wc-image.image) </span>


3. At this stage, an agent has been created. Further configuration and publishing are required before it can be used. You can view the agent in the "Pending Publish" tab of the agent list.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/837c6918f11c47f5a19f60ed72b35f51~tplv-goo7wpa0wc-image.image) </span>

<span id="ca312e58"></span>
### Configure the agent

Agents are typically configured by the data team, IT team, or professional analysts. Most business or management personnel only need to use the agent and do not need to perform configuration tasks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53b28e9131974180a3f11296b9893a77~tplv-goo7wpa0wc-image.image) </span>

The agent configuration includes multiple scenarios, as detailed below.


|Supported configuration directions |Configuration purpose |Detailed guidance documentation |
|---|---|---|
|Basic information |You can set the agent's avatar, name, and the agent's users on the basic information configuration page. |[Basic Information Configuration](https://docs.byteplus.com/docs/dataagent/Basic_Information_Configuration) |
|Dataset configuration |On the dataset configuration page, you can associate relevant datasets for data queries with the agent and configure semantic, knowledge, and other settings for the fields in the datasets. By further describing dataset fields, adding synonyms, and providing explanations for industry\-specific terms, you enable the large model to better understand the dataset fields, thereby improving the accuracy with which the agent retrieves corresponding data from the datasets based on user queries during subsequent use. |[Dataset Configuration](https://docs.byteplus.com/docs/dataagent/Dataset_Configuration) |
|Content configuration |On the content configuration page, you can configure the content layout and certain result display styles that users will see on the agent interaction page after the agent is published and goes live. For example, you can set frequently asked questions as recommended questions to be displayed directly on the page, or configure a welcome message for users when they use the agent for the first time. |[Content Configuration](https://docs.byteplus.com/docs/dataagent/Content_Configuration) |
|Intent clarification configuration |On the intent clarification configuration page, you can set up intent clarification rules for the agent. These rules enhance the intelligent analysis agent's ability to interact and execute tasks accurately when faced with complex, ambiguous, or incomplete user inputs. This allows the intelligent analysis agent to automatically determine whether the user's intent is clear based on the match between the user's input and the intent clarification rules when a question is entered, and to ask follow\-up questions to clarify ambiguous queries. |[Intent Clarification Configuration (in limited release)](https://docs.byteplus.com/docs/dataagent/Intent_Clarification_Configuration_in_limited_release) |
|Prompt configuration |The intelligent analysis agent system comes with some built\-in prompts and also allows you to add custom prompts according to your data query and analysis needs, providing the large model with certain prerequisites to enable it to generate more accurate answers. |[Prompt Configuration](https://docs.byteplus.com/docs/dataagent/Prompt_Configuration) |
|Audit |The agent configuration interface includes an audit feature that allows users to view the agent's usage records and question logs. |[Audit](https://docs.byteplus.com/docs/dataagent/Audit) |
|Knowledge configuration |You can upload and manage knowledge specific to data query scenarios on the knowledge configuration page to improve the accuracy of data queries. |[Knowledge Configuration](https://docs.byteplus.com/docs/dataagent/Knowledge_Configuration) |


<span id="91b3a17b"></span>
## Publish and manage the agent

After completing the creation and configuration of the agent, you must publish it online before further testing and use. For agents that are temporarily not in use, you can also take them offline. For detailed guidance on publishing, taking offline, and other management operations for agents, see [Publish and Manage Intelligent Analysis Agents](https://docs.byteplus.com/docs/dataagent/Publish_and_Manage_Intelligent_Analysis_Agents).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3086f96c23854595a68db5e8e909593b~tplv-goo7wpa0wc-image.image) </span>

<span id="f3085a16"></span>
## Test and use the agent


1. Test using agents

   * Web version

      1. After logging in to the BytePlus DataAgent\-Analysis Agent page with your account and password, click "Agent" to enter the agent list page.

      2. Click a published agent to enter the conversation page to use the intelligent analysis agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a132bed598c4e3095158880b0971058~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  3. After entering the agent conversation interface, click the switch button in the dialog box to toggle between the "Intelligent Query" and "In-depth Research" features.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d7b394eb35e473ebaa46990c5ae6075~tplv-goo7wpa0wc-image.image) </span>


* Lark version

   For agents on the Lark version, the overall configuration process is generally consistent with the web version, but additional configurations are required for authentication between the agent and the Lark application. After completing the configuration and publishing the agent, you can search for the agent name in Lark and click to use. For end\-to\-end configuration, see [Lark-Side Intelligent Agent Configuration and Testing](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing).

2. Application scenarios

   * For Intelligent Query Agent, refer to [Intelligent Query Agent](https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent).

   * For in\-depth research reports, refer to [Deep Research Agent](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent).


<span id="c2767f0d"></span>
## Agent usage optimization and best practices

<span id="67a53282"></span>
### Case 1: Best practices for Lark version usage

For details, see [Lark-Side Intelligent Agent Configuration and Testing](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing).

<span id="bf502a83"></span>
### Case 2: Agent question suggestions and examples

For details, see [Best Practices: Recommendations and Examples for Intelligent Data Query Questions](https://docs.byteplus.com/docs/dataagent/Best_Practices_Recommendations_and_Examples_for_Intelligent_Data_Query_Questions).
