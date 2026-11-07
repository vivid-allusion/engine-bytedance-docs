---
title: "ChatOps: Managing VMP by using the MCP service"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Managing_VMP_by_using_the_MCP_service"
---

This topic mainly describes how to deploy the VMP MCP server and use VMP\-related features on it.

> This topic may contain information about third\-party services. The information is for reference only. BytePlus does not make a guarantee in any form for the performance and reliability of the third\-party tools, and the potential impacts of operations on these tools.


<span id="SYqYjHOx"></span>
## Use scenarios

The VMP MCP server helps operation and maintenance personnel perform metric queries and analysis by using natural language in scenarios such as troubleshooting and data analysis. This improves the efficiency of operation and maintenance, and observability. The following scenarios are supported:


* Create a VMP workspace instance in the specified region.

* Query the information about all workspaces in the specified region within the current account.

* Query the information about all workspaces in the specified region within the current account.

* Delete the specified workspace instance in the specified region within the current account.

* Delete the specified workspace instance in the specified region within the current account.

* Execute a PromQL instant query in the specified VMP workspace.

* Execute a PromQL query within a specified time range in the specified VMP workspace.

* Query the list of metric names that meet the specified criteria in the specified VMP workspace.

* Query all label names of the specified metric in the specified VMP workspace.

* Specify time series metadata for the specified label selector.


<span id="QrkznEhN"></span>
## Background

<span id="NzIAjNet"></span>
### **Introduction to MCP**

The Model Context Protocol (MCP) is an open protocol that is used by LLMs to access custom tools and services. An MCP server, such as a VMP MCP server, packages and provides various executable tools. In AI IDEs such as Trae and Cursor, the agent interprets user instructions in natural language, establishes communication between the MCP client and MCP server, and invokes the corresponding tools to complete specific tasks.

<span id="1vi5vbAo"></span>
### Usage after VMP ** is integrated with MCP**

As a dedicated connecting bond between LLMs and VMP, the MCP service enables a natural language\-driven intelligent management mode for VMP. The MCP server enables operation and maintenance personnel or business personnel who are not familiar with PromQL to easily perform operations, such as VMP workspace queries and metric retrieval. In addition, it also enables AI to securely and efficiently access and interact with resources across different scenarios. This significantly reduces the difficulty in using VMP.

<span id="5ZyW8mKB"></span>
## Prerequisites

A BytePlus root user has been created, and the API key of the account has been obtained. For more information, click the .

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">When you create an account for the VMP MCP server, we recommend that you conform to the following principles:</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Dedicated account: We recommend that you create a dedicated IAM user to perform operations related to the MCP server.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Principle of least privilege: Make sure that your account has permissions on VMP\-related APIs, such as CreateCluster and CreateNodePool. Attach the corresponding policies to the account based on the principle of least privilege. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions">Configuring IAM user permissions</a>.</div>



<span id="zlarkuXI"></span>
## Procedure

<span id="gXaSOjxe"></span>
### **Step 1: Deploy the ** **VMP MCP server**

You can deploy the MCP server of the VMP service in your on\-premises environment or ModelArk. Select an appropriate method based on your business requirements.


<Tabs>
<Tab zoneid="JH5rDGyMje" title="Deploy the server on the on-premises computer">
<TabTitle>Deploy the server on the on-premises computer</TabTitle>

Deploy the VMP MCP server in your on\-premises environment, such as your on\-premises computer, by using the AI IDE tool.

<span id="UycIOEqI"></span>
### Prerequisites

You have deployed the AI IDE platform and related dependencies (Python and uv) in your on\-premises environment.


|Tool/add\-on |Description |
|---|---|
|AI IDE |In this example, Trae is selected as the AI IDE for subsequent operations.<br><br>> Trae is an AI IDE that supports MCP. You can quickly deploy the MCP server (such as connecting to VMP) by using the built\-in MCP marketplace of Trae or through manual configuration. You can go to the [TRAE official website](https://www.trae.com.cn) to download and install it on your computer. |
|Python |v3.10 or later. You can visit [the official Python website](https://www.python.org/) to download and install the tool. |
|uv |A tool that is used to quickly install and manage Python packages and provides the uvx command\-line tool. For more details, see the [official guide on uvx](https://astral.sh/uv).<br><br><br>* MacOS/Linux<br><br>   ```Plain Text```<br>```   curl -LsSf https://astral.sh/uv/install.sh \| sh```<br>```   ```<br>   <br><br>* Windows<br><br>   ```Plain Text```<br>```   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 \| iex"```<br>```   ```<br>   <br><br><br> |


<span id="HdsuAV0K"></span>
### Procedure

<span id="07zJDhoN"></span>
#### Step 1: **Add the VMP ** MCP server

Add the VMP MCP server from the BytePlus LLM ecosystem plaza to your local Trae.


1. Open the Trae platform installed locally.

2. Click the settings icon in the upper\-right corner of the page.

3. On the Settings page, click **MCP**.

4. Add the VMP MCP server.

   
   <Tabs>
   <Tab zoneid="ub0ZkWjNdf" title="Manually add the server">
   <TabTitle>Manually add the server</TabTitle>
   
   1. Click **Add** \> **Add Manually**.
   
   2. Paste the following JSON configurations in the code editor, and replace `Your Volcengine access key` and `Your Volcengine secret key` in the code with the actual access key ID and secret access key that correspond to your account.
   
      **UV**
   
      ```JSON
      {
        "mcpServers": {
          "mcp_server_vmp": {
            "command": "uv",
            "env": {
              "VOLCENGINE_ACCESS_KEY":"Your Volcengine access key",//The access key ID of the BytePlus root user.
              "VOLCENGINE_SECRET_KEY":"Your Volcengine secret key"//The secret access key of the BytePlus root user.
            },
            "args": [
              "--directory",
              "/<your local path to mcp-servers>/server/mcp_server_vmp",
              "run",
              "mcp-server-vmp"
            ]
          }
        }
      }
      ```
      
   
      **UVX**
   
      ```JSON
      {
        "mcpServers": {
          "mcp_server_vmp": {
            "command": "uvx",
            "env": {
              "VOLCENGINE_ACCESS_KEY":"Your Volcengine access key",//The access key ID of the BytePlus root user.
              "VOLCENGINE_SECRET_KEY":"Your Volcengine secret key"//The secret access key of the BytePlus root user.
            },
            "args": [
              "--from",
              "git+https://github.com/volcengine/mcp-server#subdirectory=server/mcp_server_vmp",
              "mcp-server-vmp"
            ]
          }
        }
      }
      ```
      
   
      **Environment variables**
   
      
      |**Environment variable name** |**Description** |**Required** |
      |---|---|---|
      |VOLCENGINE_ACCESS_KEY |The access key ID of your BytePlus root user.  |Yes |
      |VOLCENGINE_SECRET_KEY |The secret access key of your BytePlus root user.  |Yes |
      |VOLCENGINE_REGION |The region of BytePlus. |Optional |
      
   
   3. Click **Confirm** to save the configurations.
   
   
   </Tab>
   <Tab zoneid="Yo67IiFumk" title="Add the server from the marketplace">
   <TabTitle>Add the server from the marketplace</TabTitle>
   
   1. Click **Add** \> **Add from marketplace**.
   
   2. Enter VMP MCP in the search box and click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a83739c98a601be68af9f9c71131711.png) </span>icon.
   
   3. After you enter the actual access key ID and secret access key of your BytePlus root user, click **Confirm** to save the configurations.
   
   
   </Tab>
   </Tabs>
   


<span id="oXm9rvkh"></span>
#### Step 2: Associate the server with an agent

After you add the VMP MCP server, associate it with an agent. In this way, the agent can use the MCP capabilities provided by the VMP service.


1. Click the settings icon in the upper\-right corner of the Trae page.

2. On the Settings page, click **Agents.** 

3. Click **Create** and enter the agent name. In this example, enter VMP service agent.

4. In the **Tool \- MCP** list **,**  select the configured **VMP MCP**, and keep other default settings.

5. Click **Confirm** to complete the configuration.


</Tab>
<Tab zoneid="Yrr5KB0NId" title="Deploy the server in ModelArk">
<TabTitle>Deploy the server in ModelArk</TabTitle>

With the VMP service hosted by BytePlus and the built\-in MCP ecosystem in ModelArk, you can quickly configure the MCP server of the VMP service without the need to build infrastructure.


1. Visit [MCP MarketPlace](https://www.byteplus.com/en/mcp-marketplace). 

2. In the search box, enter **VMP MCP** and press Enter. ****Then, click **VMP MCP**.

3. Click the **Install** tab and specify the tool to use. In this example, select **ModelArk.**  Click  to learn more

4. Click **Generate** to obtain the MCP server URL.

5. Click **Experience** to enable the MCP service.

   1. Click **MCP.** 

   2. On the MCP Servers management page, search for **VMP** and then switch on VMP.

   3. Close the **MCP server management** page.


</Tab>
</Tabs>


<span id="DgX1OTXs"></span>
### Step 2: Use the server


<Tabs>
<Tab zoneid="itsxXALTQI" title="Use the server on the on-premises computer">
<TabTitle>Use the server on the on-premises computer</TabTitle>

After you create the MCP server, click **Use now**. In the dialog box with the agent, enter instructions in natural language as needed to interact with the agent. This topic uses the instruction **Query the information about all workspaces in the specified region within the current account** as an example.


1. Enter **Query the information about all workspaces in the specified region within the current account** in the dialog box with the agent.

2. Press Enter to view the answer returned by the agent. If the agent indicates that more information is required, enter the related information to view the feedback result.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the agent receives the instruction, it analyzes and determines which specific tool provided by the VMP MCP server needs to be used.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent automatically generates API request parameters and calls the tool provided by the VMP MCP server by using MCP.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the MCP server executes the query, it returns the result to the agent.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent organizes the result and presents it to you in an easy\-to\-understand format, such as charts and text.   </div>
   


</Tab>
<Tab zoneid="BQFbq9kAkR" title="Use the server in ModelArk">
<TabTitle>Use the server in ModelArk</TabTitle>

After MCP is enabled, use MCP capabilities based on your business requirements. Click  to learn more


1. Enter your question in the text box.

2. Press Enter to view the answer returned by ModelArk. If ModelArk indicates that more information is required, enter the related information to view the feedback result. 


</Tab>
</Tabs>
