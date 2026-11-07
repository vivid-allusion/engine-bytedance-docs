---
title: "Integrate MCP"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1856160"
---

Through MCP (Model Context Protocol), you can encapsulate external services—such as knowledge base Q&A (RAG), web search, or business API calls—as standardized tools. This allows the LLM to intelligently invoke these tools during a conversation to retrieve necessary data or perform actions, and then generate more accurate and professional responses based on the results.

> For more about MCP, refer to the [official documentation](https://modelcontextprotocol.io/docs/getting-started/intro).


<span id=".6YCC55So5Zy65pmv"></span>
## Use Cases

&nbsp;


|Scenarios |Benefit |
|---|---|
|Integrate a Knowledge Base (RAG) |Enable agents to provide precise answers based on your private, internal documents or databases. |
|Real\-time Web Search |Enable agents to simultaneously obtain and intelligently summarize information from multiple data sources, such as weather, news, and stocks. |
|Execute Complex Business Processes |Enable agents to call external APIs to perform business operations like booking flights, placing orders, or querying account balances. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Restrictions

This feature has specific prerequisites and limitations:


* **Model Support:**  It is only compatible with BytePlus ModelArk models or third\-party LLMs that support Function Calling. For a comprehensive list of supported ModelArk models, refer to the [Model List-Tool use](https://docs.byteplus.com/en/docs/ModelArk/1330310#f44ceef7).

* **Response Format:**  Your MCP Server's response format must be Server\-Sent Events (SSE).


<span id=".5o6l5YWl5pa55byP"></span>
## Procedure

<span id=".XzEt5YeG5aSHLW1jcC1zZXJ2ZXI="></span>
### 1. Prepare Your MCP Server

Develop and deploy your own MCP Server. The service must adhere to the MCP protocol, handle requests, invoke your internal tools, and return results in the specified format. For step\-by\-step instructions, see the [official tutorial](https://modelcontextprotocol.io/docs/getting-started/intro).

<span id=".XzIt77yI5Y-v6YCJ77yJ6aqM6K-BLW1jcC1zZXJ2ZXIt5Y-v55So5oCn"></span>
### 2. (Optional) Verify MCP Server Availability

Before configuring the integration, we recommend you verify that your MCP Server is accessible from the public internet using `curl`.

`<YOUR_MCP_SERVER_URL>`: Replace this with your actual MCP Server address.

```sh
curl -i <YOUR_MCP_SERVER_URL>
```


<span id=".XzMt6YWN572uLXN0YXJ0dm9pY2VjaGF0LeaOpeWPow=="></span>
### 3. Configure the StartVoiceChat API

When calling [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163), you must configure the following fields within `LLMConfig`:

&nbsp;


|Field |Description |
|---|---|
|`LLMConfig.MCP` |Register your MCP toolset. |
|`LLMConfig.SystemMessages` |The LLM does not have prior knowledge of your internal systems. |
| |:::notice Warning<br><br>Ensure all tool capabilities described here are implemented in your MCP Server. The prompt guides the model; it does not create new functionality.<br><br>::: |


<span id=".5bqU55So56S65L6L"></span>
#### **Example**

```JSON
{
    "LLMConfig": {
        // ... Other LLM parameters like Mode, EndPointId, etc. ...

        "MCP": [{
            "URL": "<YOUR_MCP_SERVER_URL>",
            "Name": "product_database",
            "InterestedTools": ["query_product"],
            "ComfortWords": "Let me check on that for you..."
        }],
        "SystemMessages": [
           "You can call the `query_product` tool to look up product information. Adhere to the following rules:\n1. **Identify the Core Product:** Extract the main product name from the user's query and pass it to the `product_name` parameter (required).\n2. **Identify the Category:** If the user mentions a product category (e.g., 'laptop', 'smartphone'), populate the `category` parameter.\n3. **Construct Spec Filters:** If the user specifies attributes like 'memory' or 'hard drive', construct a JSON object for the `spec_filters` parameter. For example, if the user says '16GB of RAM', you should construct `{\"memory\":\"16GB\"}`."
        ]
    }
}
```
