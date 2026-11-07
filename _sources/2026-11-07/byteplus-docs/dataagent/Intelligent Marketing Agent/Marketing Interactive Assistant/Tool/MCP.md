---
title: "MCP"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MCP"
---

MCP (Model Context Protocol) is an open standard that allows developers to establish a secure two\-way connection between their data sources and AI\-driven tools. The MCP tools registered on the platform can be used when creating autonomous planning agents. In the MCP function, you can register external tools for use through MCP Sever. This article shows you how to create an MCP Server.

# Creating an MCP Server

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. In the left navigation bar of the Marketing Interactive Assistant, select **MCP** and click Create **MCP Server** in the upper right corner of the page.

3. Complete the following configuration in the pop\-up window and click **OK** .

   |parameter |parameter description |
   |---|---|
   |agreement |Optional **SSE** or **Streamable** . |
   |source of service |OpenAPI registration or an existing MCP Server can be registered with the agent application platform and used as an agent tool for marketing agents. If you choose to register an existing MCP Server, you also need to fill in the Endpoint. |
   |display name |The name of the MCP. |
   |describe |Description of MCP, the description must comprehensively introduce the capability description of MCP, "Help the model understand the capabilities of MCP, and better choose MCP for use". |
   |Endpoint |Only register an existing MCP Server with this configuration, and registering OpenAPI will automatically generate one. |
   |Headers |Only register the existing MCP Server with this configuration, and request the header parameter configuration. |
   |enable authentication |* Open: Open is authenticated by API Key. After opening, you need to add the parameter "API key" to the header.<br><br>* Close: If closed, the authentication will not be turned on, and the display name can be called directly through the address: the display name of the MCP tool |

4. Click on the created server name to enter the editing page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33375a1ff636431c9cc87b90e6d4f7c4~tplv-goo7wpa0wc-image.image)

5. On the Edit page, click the **Tools Administration** tab, click **Create Tool** , fill in the relevant parameters, and then click **OK** .

   MCP tools are model\-driven operations that allow the AI model to choose to call functions during a conversation, including calling executable functions, API calls, data processing, and more. With these capabilities, AI can trigger actions in real time, such as adjusting meetings, sending emails, etc., and automatically identify the list of tools exposed by the server to support complex workflows.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86b8cd16e9764f66aa7d5ccf2d893372~tplv-goo7wpa0wc-image.image)

   |parameter |parameter description |example |
   |---|---|---|
   |display name |Name of Tool |Get rainfall probability |
   |identifier |The AI Agent invokes the unique identity of the MCP Server Tool. Contains only lowercase letters, numbers, underscores, dashes, and slashes, and can only begin with a lowercase letter, with a character limit of 100. |get_precipitation |
   |describe |Helping the AI Agent understand the capabilities of the MCP Server Tool is an important basis for deciding to use the current tool, with a character limit of 500. |Get the rainfall probability of the city |
   |Input Schema |Input parameters for calling the MCP tool after thinking about the big model, described using JSON Schema |```JSON```<br>```{```<br>```  "type": "object",```<br>```  "properties": {```<br>```    "city": {```<br>```      "type": "string",```<br>```      "description": "city"```<br>```    }```<br>```  },```<br>```  "required": ["city"]```<br>```}```<br> |
   |request type |Only HTTP is supported. |HTTP |
   |request method |Support GET and POST. GET is selected by default, based on the selection of the stitching request |POST |
   |request URL |Address URL of the tool call, limited to 100 characters |[https://e1XXXX4gmXXXXXngers-onpremise.volces.com/api/investment_advisor/mock_tools/get_precipitation](https://e16XXXXmp.datarangers-onpremise.volces.com/api/investment_advisor/mXXXXecipitation) |
   |request header |Add the Key and Value of the request header, up to 20 |content\-type<br><br>application/json |
   |Request Scheme |Optional, code input. JSONata format to replace the Request Body under POST requests |/ |
   |Response Scheme |Optional, JSONata format, used to describe the cropping, renaming, etc. of Response |/ |

6. Clicking on **RUN** will display the current response results, and you can see if the results are as expected.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/010262a8b93c4db3a06ba9a8143e22c7~tplv-goo7wpa0wc-image.image)

7. The created and debugged MCP Server can be invoked for autonomous planning agent, thinking chain, and other functions. See the specific operation [New Autonomous Planning Agent](https://docs.byteplus.com/docs/dataagent/New_Autonomous_Planning_Agent).

# Related Documentation

For related documentation, see [MCP official documentation](https://modelcontextprotocol.io/docs/getting-started/intro).
