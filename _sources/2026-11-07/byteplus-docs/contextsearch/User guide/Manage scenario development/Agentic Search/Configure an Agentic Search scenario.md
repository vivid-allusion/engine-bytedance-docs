---
title: "Configure an Agentic Search scenario"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Configure_an_Agentic_Search_scenario"
---

After completing the initialization of an Agentic Search scenario, you can further configure its capabilities based on business needs, including adding Skills, MCP, and Data sources, setting access permissions and global variables, and verifying the scenario effect through the conversation feature. This topic describes how to configure an Agentic Search scenario.

<span id="guKgwdYf"></span>
## Prerequisites

The Agentic Search scene has been created and initialized. For detailed operations, refer to [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario) and [Initialize an Agentic Search scenario](https://docs.byteplus.com/en/docs/contextsearch/Initialize_an_Agentic_Search_scenario).

<span id="4gtvgtdr"></span>
## Procedure

<span id="9rHJEM01"></span>
### Scenario conversation


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scenes** from the left navigation bar, then click the target Agentic Search scene.

4. Enter your question or request in the dialog box, then click the send button. The system outputs results based on your configured model, Skill, MCP, and Data source. For specific steps, refer to the following sections.


<span id="e6y9BuQA"></span>
### View Trace

You can enable tracing to view the call chain and detailed execution information, helping you analyze the request processing. For steps to enable tracing, refer to [View configuration information](https://docs.byteplus.com/en/docs/contextsearch/View_configuration_information).

After enabling tracing, click **Trace** below the output to go to the OpenSearch Instance Dashboards page. Log in to view trace data. For detailed steps, see [Query Agent Traces through Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/Query_Agent_Traces_in_Dashboards).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Trace configuration is currently a whitelist feature; to use it, please <a href="https://console.byteplus.com/workorder/create/?step=1">submit a ticket</a> to apply.</div>


* <div data-tips="true" data-tips-type="default">To enable tracing, complete the following steps in Cloud Search first:</div>


   * <div data-tips="true" data-tips-type="default">Create an OpenSearch 3.3 instance. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/creating-instance">Create an instance</a>.</div>


   * <div data-tips="true" data-tips-type="default">Turn on managed OTLP function. For more information, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP">Enable managed OTLP</a>.</div>


   * <div data-tips="true" data-tips-type="default">Enable private network access point for managed OTLP and set the virtual private cloud to the one used by the current Agentic Search scenario. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/Enable_managed_OTLP#mTmBnv9S">Enable the private network endpoint</a>.</div>


* <div data-tips="true" data-tips-type="default">After enabling tracing, you can view observability data in OpenSearch Dashboards. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Query_Agent_Traces_in_Dashboards">Query Agent Traces through Dashboards</a>.</div>



<span id="EDWgQFU5"></span>
### Skill management

Skills provide specific task processing capabilities for Agentic Search. You can add or remove Skills in the scene according to business needs to extend the scene’s tool invocation capabilities and support more complex search tasks.

<span id="CGWPfXXS"></span>
#### Create a skill


1. Select **Skills** from the left navigation bar, then click **Create skill** at the top right of the **Skills** page.

2. In the **Create skill** dialog, click the file upload area to select a Skill file or drag the Skill file into the upload area.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only ZIP format files are supported.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The maximum file size is 100 MB.   </div>
   

3. Configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Name |Set the name of the Skill. Naming rules are as follows:<br><br><br>* Can only contain letters, numbers, periods (.), underscores (_), and hyphens (\-).<br><br>* Must begin with a letter or number. |
   |Description (optional) |Description of the scene setup. |
   


<span id="QCJRk41F"></span>
#### Subsequent operations

After creating a Skill, you can download, edit, or delete it on the **Skills** page.

<span id="N61T5Tzy"></span>
### MCP management

MCP connects Agentic Search with external tools or services to provide richer capabilities for scenarios. You can create and manage MCP services based on business needs, enabling the Agent to autonomously call external tools for data queries, system operations, and other tasks during search execution.

<span id="sPBfdaiN"></span>
#### Create MCP


1. Select **MCP** in the left navigation bar, then click **Create MCP** at the top right of the **MCP** page.

2. Configure the following parameters in the **Create MCP** panel, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |MCP name |Set the name of the MCP. Naming rules are as follows:<br><br><br>* Can only contain letters, numbers, periods (.), underscores (_), and hyphens (\-).<br><br>* Must begin with a letter or number. |
   |Description (optional) |Description of the scene setup. |
   |MCP configuration |Enter the MCP configuration in the code box. The example fields are explained as follows:<br><br><br>* mcpServers: MCP Server configuration collection, which can include one or more MCP Servers.<br><br>* server\-name: the name of the MCP Server.<br><br>* command: the command to start the MCP Server.<br><br>* args: the parameter list for the start command.<br><br>* env: environment variables injected when starting the MCP Server.<br><br>* API_KEY: MCP Server provides the API Key required to access external services.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Startup commands, parameters, and environment variables supported by different MCP Servers may vary; refer to the official documentation of the corresponding MCP Server for configuration.</div><br> |
   


<span id="G2n2lMiZ"></span>
#### Subsequent operations

After creating an MCP, you can also edit or delete it on the **MCP** page.

<span id="sXmaC1Nv"></span>
### Data source management

The data source provides business data required for retrieval and Q&A in Agentic Search. You can add and manage data sources for scenarios according to business needs. This allows the Agent to retrieve relevant data during search tasks and generate more accurate answers based on the search results.

<span id="oDGhkmEc"></span>
#### Associate a data source


1. Select **Data source** in the left navigation pane, then click **Associate a data source** at the top right of the **Data source** page.

2. In the **Select data source** panel, click  **+**  on the target data source card, then click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can repeat this to bind multiple data sources.</div>


<span id="AspG6csa"></span>
#### Disassociate Data source

When you no longer need the bound data source, click **Disassociate** on the bound data source card, then click **OK** to unbind the data source.

<span id="fTk6mmr7"></span>
### Access Permission Management

Access permissions control the scope of calls in the Agentic Search scenario. You can configure scene access permissions based on business needs to ensure only authorized users or applications can access and call the scene.

Select **Access control** from the left navigation bar, then view authorized users on the **User permissions** page. If you want to prevent a user from accessing the scenario, click **Delete** in that user’s **Actions** column, then click **OK** to remove the user.

<span id="6wlQCPXW"></span>
### Global variable management

Global variables manage common parameters used during the Agentic Search scenario. You can create and manage global variables based on business needs and reference them in Prompt, Skill, MCP, and other configurations to improve reuse and maintenance efficiency.

<span id="8iGKPYiO"></span>
#### Create variables


1. Select **Global variables** in the left navigation bar, then click **Create variables** at the top right of the **Global variables** page.

2. In the Create Variable dialog, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Variable name |Set the name of the global variable |
   |Value |Set the value of the global variable. |
   |Encryption (optional) |Check to hide the variable value and prevent sensitive information leaks. |
   


<span id="LjKYzWu2"></span>
#### Subsequent operations

After creating a global variable, you can edit or delete it on the Global Variables page.
