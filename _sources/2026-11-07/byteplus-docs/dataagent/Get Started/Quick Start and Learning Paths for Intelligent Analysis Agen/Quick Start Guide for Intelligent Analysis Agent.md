---
title: "Quick Start Guide for Intelligent Analysis Agent"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Quick_Start_Guide_for_Intelligent_Analysis_Agent"
---

After purchasing and activating Intelligent Analysis Agent, Intelligent Analysis Agent currently provides a general agent for you (default name: DataAgent). You can directly use the pre\-configured general agent to consult on issues, and you can also create and configure custom agents. This article will guide you through quickly using both the general agent and custom agents, and completing analysis tasks with the general agent.

To learn about the comparison between the two, refer to [Description of Agent Types: General and Custom Agents](https://docs.byteplus.com/docs/dataagent/Description_of_Agent_Types_General_and_Custom_Agents).

<span id="997c9f21"></span>
# Prerequisites

The following conditions are required to use the general agent:


* **Account and permissions**: You need to have a valid platform account and be successfully logged into the system; please ensure your account has been granted permission to use the general agent. If it has not been activated yet, please contact your system administrator.

* **Understanding the data**: Connect relevant data or upload files, and briefly describe the background or source of the core business data used by Intelligent Analysis Agent.


<span id="20ad38c5"></span>
# Purchase and activation


1. Please visit [BytePlus official website](https://www.byteplus.com/en) to log in or register a BytePlus account.

2. After successfully registering a BytePlus account, you need to complete the relevant real\-name authentication process. For details, see Personal authentication and Enterprise authentication.

3. After registering your account and completing real\-name authentication, you can use this account to access the Intelligent Analysis Agent product homepage to view or place orders for products.

4. Purchase Intelligent Analysis Agent services on the Intelligent Analysis Agent order page.


<span id="ab8ddb86"></span>
# Create a project


1. After purchasing Intelligent Analysis Agent services, log in to the DataAgent interface using your account and password.

2. After entering the product page, select the corresponding region, click the 'Create project' button at the top right of the page, fill in the project name, select the project administrator, and fill in the reason for creation field. After completion, click the 'Confirm' button.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2048a373eb9c4b3396eaddb4853be53a~tplv-goo7wpa0wc-image.image) </span>


3. After creating the project, set project information, add users, and grant permissions in the project center.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/391c65dd66ec47c5aa8994f762fb46fc~tplv-goo7wpa0wc-image.image) </span>

<span id="9b83a69d"></span>
# Quick start guide for the general agent


1. After authorization is complete, click the Agent button at the top of the page to enter the Agent usage interface.

2. In the left navigation bar of the Intelligent Analysis Agent usage interface, you can view all Agents that you have permission to access and use in the current region. Click the Agent name to enter the Agent.

   * The Data Agent at the top of the list is the **general Agent**.

   * The other Agents listed below are custom Agents that you have created. For details on creating custom Agents, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e02bdbcee0f246ebb3be634a5f604abf~tplv-goo7wpa0wc-image.image) </span>


3. In the central dialog box of the Agent interface, use the Q&A service. Click the **Connect Data** button in the lower right corner to upload a data source. After the data source is uploaded, enter the task description in the dialog box. In addition, the following features are available:

   * **Select whether to enable internet access**: After enabling internet access, the Agent will retrieve the latest information from the internet in real time and analyze it based on the latest information. To disable internet access, click the internet access button again; when the button is grayed out, internet access is disabled.

   * **Configure capability extensions**: The general Agent allows you to configure different capability extensions according to your needs (multiple selections supported). The following is an explanation of capability extension configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc8e6562108f4e6d9f26fb41861dc842~tplv-goo7wpa0wc-image.image) </span>


|Name of expansion capability configuration |Note |
|---|---|
|Formula breakdown |Break down complex metric calculation formulas or business logic into basic calculation steps and sub\-items, clearly displaying the logical structure and calculation process of the metric. For example, break down "Gross margin = (Operating revenue \- Operating cost) / Operating revenue" into "Operating revenue composition, operating cost details, proportion calculation logic" to help users understand the underlying principles of the metric, facilitating verification and optimization. |
|Related metric analysis |Automatically associate and analyze upstream, downstream, and related business metrics in the same scenario based on the core metrics of the current issue, forming a comprehensive business analysis perspective. For example, when analyzing "sales revenue", related metrics such as "average transaction value, conversion rate, repeat purchase rate, and channel share" are displayed simultaneously to help users comprehensively evaluate business performance. |
|Dimensional attribution |Conduct attribution analysis of metric fluctuations or differences across multiple dimensions, such as time, region, channel, user segmentation, and product category, to identify the key dimensions and subgroups that affect metric changes. For example, when sales revenue decreases year\-over\-year, dimensional attribution reveals that "offline channels in the East China region" are the main drag, providing precise direction for decision\-making. |
|Anomaly detection |Automatically identify abnormal fluctuations, outliers, or sudden changes in data sequences that do not conform to historical patterns, and mark and alert abnormal events. For example, when order volume surges or drops sharply during a certain period, or when the conversion rate deviates significantly from the threshold, the system issues timely alerts to help users quickly locate potential issues (such as campaign impact, system failures, external events, and more). |
|Formula attribution |Based on the calculation formula of the metric, quantitatively break down the contribution of each component to the overall metric change and clarify the influence weight of each factor. For example, when profit increases year\-over\-year, formula attribution quantifies "revenue growth contributes 60%, cost reduction contributes 40%", accurately identifying the core factors driving metric changes. |



4. After uploading the data source and providing a task description for the general Agent, click the Send button and wait for the Agent to execute the task.

5. The task execution time will vary depending on the complexity of the task. Please wait patiently. After the task is completed, the general Agent will return the execution result, which you can view in the dialog box. The analysis results are available in two formats: **web version** and **document version**. You can view different types of analysis results by clicking the corresponding button.

   There are several operations available for the analysis results. The following are illustrations and descriptions of the related operation items for the analysis results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82bf154607684aaf8b125878334b8bfd~tplv-goo7wpa0wc-image.image) </span>

   
   |Analysis report operations |Note |
   |---|---|
   |Copy |In the upper right corner of the report, copying of analysis results is supported. The copy function allows you to select the type of content to copy from a dropdown menu, with the following options:<br><br><br>* Report content: After selecting from the dropdown, you can copy all content of the report. The copied content is saved to the clipboard in **Markdown format**, making it easy to paste directly into editors that support Markdown.<br><br>* Report link: Copy the accessible link for the current analysis report. Others can open and view the report directly via this link (appropriate access permissions are required).<br><br>* Report ID: Copy the unique identifier ID for this report, which can be used to quickly locate, associate, or retrieve the analysis report within the system. |
   |Export |The report supports exporting in different formats. The following formats are supported:<br><br><br>* Feishu document: Export the analysis report directly as a Feishu document, enabling online collaboration, commenting, and version management within the Feishu ecosystem.<br><br>* Word document: Export as a standard Word (.docx) format, making it convenient for local further editing, layout, or printing.<br><br>* PDF document: Export as a PDF format, suitable for formal sharing, archiving, or printing, and ensures maximum consistency and immutability of the report format.<br><br>* Image: Export the report results as an image format (such as PNG/JPG), making it easy to quickly share the visual content of the report in social media or chat windows.<br><br>* Raw data: Export the original dataset used to generate the analysis report, facilitating further analysis, data validation, or additional processing. |
   |Share |Click the share button in the upper right corner of the analysis results. You can search for authorized users and select the recipients to share with. To authorize multiple users, separate them with English commas and paste into the input box, such as user1, user2. |
   


<span id="abd7cbac"></span>
# Agent demo room

To help you quickly master agent configuration logic and efficiently reuse proven practices, the platform provides built\-in **DEMO agent templates** covering multiple scenarios, including mature solutions for preset function configurations, data source associations, and extension capability settings. By copying the **DEMO agent templates**, you can make personalized adjustments directly based on the preset templates without building from scratch, making configuration easier and improving development efficiency.

The following are the steps for copying **DEMO agent templates**. For more instructions on using templates, see the [Intelligent Analysis Agent Administrator Quick Start Guide](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Administrator_Quick_Start_Guide).


1. In the agent dashboard, click the management console button in the lower left corner to access the agent list.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2f14462fac3467a9d3f1e3acc9f82cc~tplv-goo7wpa0wc-image.image) </span>


2. Click the Copy **DEMO agent** button in the upper right corner of the agent list page, select the agents you need (multiple selection supported), and then click the **Confirm** button. After confirming, wait for a period of time. Once the copying is complete, you can view the copied agents on the agent list page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a00933eb9c5c45fb99e36837c3a14605~tplv-goo7wpa0wc-image.image) </span>


3. Click the copied agent to enter the agent page.

4. To configure the copied agent, click the **Agent Configuration** button below the agent to perform detailed configuration. For agent configuration instructions, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures).


<span id="05581a0c"></span>
# Quick start for custom agents

<span id="7ff11859"></span>
## Prepare data

Before performing intelligent data analysis, you need to import the data to be analyzed into the Agent Analytics module. Currently, uploading data files and connecting to data warehouses are supported. For details, see [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview). The following provides a sample data demo. You can download the demo and upload it to quickly experience the data preparation process.


1. Select Data Preparation—Data Connection, and click the New button to establish a data connection.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f7096c281244b0f83e59c7e05ff45f5~tplv-goo7wpa0wc-image.image) </span>


2. Select the Excel data connection method, and click to upload the provided Agent Analytics dataset sample.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cffacef2474a4fcc90ec76138fb7e926~tplv-goo7wpa0wc-image.image" name="Intelligent Analysis Agent Dataset Sample.xlsx">Intelligent Analysis Agent Dataset Sample.xlsx</Attachment>


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db4515f7218b474b8051b955d2848a57~tplv-goo7wpa0wc-image.image) </span>


3. Select the sample data. After seeing the upload success prompt, click the Next button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f7871d6b8414118be48b48e352dcfb7~tplv-goo7wpa0wc-image.image) </span>

4. After verifying that the data preview is correct, click the Confirm button. Once the data connection is created successfully, you can view the basic information and lineage view of the uploaded Excel data in the data connection list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e9dda4645654f0f8136592702277ad8~tplv-goo7wpa0wc-image.image) </span>

5. Select Data Preparation—Dataset, and click the New Dataset button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ca1027c5acb4657a1d1ed72d90c7d83~tplv-goo7wpa0wc-image.image) </span>

6. In Add Data Connection, select Upload to Sample Dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c51cc4734cb4f9aa3d2c112f5e7f15e~tplv-goo7wpa0wc-image.image) </span>

7. Drag the selected data table into the dataset creation area, then click Save.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d371bfdf2144a6bf6407cf5f492199~tplv-goo7wpa0wc-image.image) </span>

8. Set the dataset information, configure the relevant parameters, and click the Confirm button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a861c416ab794964bb7be125594dad9c~tplv-goo7wpa0wc-image.image) </span>

9. The dataset is created successfully. You can perform dataset operations such as data preview, field modification, and setting row and column permissions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df27c188b8604305bda7a568ded3a0c3~tplv-goo7wpa0wc-image.image) </span>

10. After the dataset is created successfully, click the Enable Data Agent Analysis Capability button, then click Enable. Choose the data update mode and whether to synchronize in real time based on the actual data update situation. Click the Confirm button and wait for the data to be vectorized. **Only when the vectorization status shows "Success" can the created dataset be configured in the agent**. The expected wait time is 15+ minutes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46b474be03224ec1991be7349a2d46a3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/944eb8d5c76a4b16b49f7a3e963c6bee~tplv-goo7wpa0wc-image.image) </span>

<span id="0133e04a"></span>
## Create agent.

You can create multiple intelligent analysis agents in the Intelligent Analysis Agent according to your business data analysis needs.


1. Create agent. Go to the Intelligent Analysis Agent configuration page, and click the Create Agent button in the upper right corner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b0a5a5036544eb48f745b5d21a4502c~tplv-goo7wpa0wc-image.image) </span>


2. Configure the agent's application name, application description, avatar, administrator, members, and other basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6451d278fe04765971c14e6b5083096~tplv-goo7wpa0wc-image.image) </span>

3. Configure the agent.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ab529d6219843c6a56e868ef6c82505~tplv-goo7wpa0wc-image.image) </span>

   1. Go to the agent's **dataset configuration** module, and click the **Add Dataset button** in the middle.

   2. Search for the dataset you need to add. This page supports selecting multiple datasets in bulk.

   3. After clicking the **Confirm button**, the addition will be successful. You can continue to add other datasets or remove datasets later.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Agent configuration also involves detailed configurations such as content configuration, Prompt configuration, audit, and knowledge configuration. You can configure these as needed during actual use. This example is a simple demo for a quick experience and skips guidance for other configuration sections. To view the complete configuration documentation, refer to <a href="https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures">Overview of Creation and Configuration Procedures</a>.   </div>
   

4. Publish agent. After completing the agent configuration, you need to click the Publish button in the upper right corner. Only then will the agent appear in the published agent list and be available for use.

   After publishing, users with agent permissions can click an agent in the published agent list to access its page, and can find the agents they are authorized for in the agent list on the left.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/118191ce3961454b89bfbac0e50e388c~tplv-goo7wpa0wc-image.image) </span>


<span id="a989706d"></span>
## Use agents


1. After authorization by the primary account, the sub\-account can log in to the agent using their account password and click "Agent" to enter the agent list page.

2. Click a published agent to go to the conversation page for intelligent analysis agent usage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70baabd9c6224404a6bc0eee4705cfca~tplv-goo7wpa0wc-image.image) </span>

3. After entering the agent conversation interface, click the switch button in the dialog box to toggle between intelligent Q&A and in\-depth research functions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5869756de5ea413393e2c2d8ab7c5378~tplv-goo7wpa0wc-image.image) </span>

4. Users can click the dialog box to select a built\-in question to ask, or directly enter a question.

   
   |Natural language question |Quickly view recommended questions |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ded30535ed364b6c92d9586806a0386e~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The primary usage of the intelligent agent allows users to directly describe their data query requirements in text to the agent. After receiving a response, users can click "Follow\-up" to continue interactive Q&A with the agent regarding related issues.<br><br>* When querying data with the intelligent agent, there is no need to select a dataset; it will automatically query data from the configured datasets. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48329865e42c4f468a53236ceb714a1a~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Recommended questions are provided below the dialog box, and users can click any recommended question to directly query data.<br><br>* Recommended questions are automatically generated based on all users' historical query questions, and can also be customized. For specific configuration methods, see [Overview of Creation and Configuration Procedures](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures). |
   

   * For more instructions on using the analysis agent, see [Intelligent Query Agent](https://docs.byteplus.com/docs/dataagent/Intelligent_Query_Agent), [Deep Research Agent](https://docs.byteplus.com/docs/dataagent/Deep_Research_Agent), [Web Search](https://docs.byteplus.com/docs/dataagent/Web_Search), [Knowledge Document Configuration](https://docs.byteplus.com/docs/dataagent/Knowledge_Document_Configuration).

   * To integrate the published intelligent analysis agent into office software for subsequent use, or to use the intelligent analysis agent directly by calling OpenAPI, see [Intelligent Analysis Agent Third-Party Integration Guide](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide) ,[Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).


<span id="7be2e7e7"></span>
# Special statement


1. All content output by this service is generated by artificial intelligence models.

2. This feature is intended only for customers' internal, proprietary business, and personal use. Customers must not provide generative artificial intelligence services to the public through data agents.

3. This product supports both SaaS and private deployment versions. To purchase or try the product, please contact a sales representative for consultation.
