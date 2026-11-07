---
title: "Sample JSON file for A2A agent"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Sample_A2A_agent_JSON_file"
---

The platform allows you to register an A2A agent to the Application Center by importing a JSON file. This topic provides sample A2A agent JSON code for this registration scenario.

<span id="CudtGQHB"></span>
## Sample code

The following example is written based on the A2A protocol version **0.3.0**. Core fields and required items may differ across protocol versions. Please follow the requirements of the actual protocol version. [Learn more](https://a2a-protocol.org/latest/specification/#441-agentcard)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the A2A Agent JSON code example, special attention should be paid to the following two points:</div>



* <div data-tips="true" data-tips-type="warning">Authentication information <code>apiKeyAuth</code>: Usually, there is no need to manually enter the authentication information. During actual calls, the authentication method configured on the page is applied.</div>


* <div data-tips="true" data-tips-type="warning">Service <code>url</code>: Enter the current publicly accessible Agent service endpoint.</div>



```JSON
{
  "capabilities": {
    "streaming": true
  },
  "defaultInputModes": [
    "text"
  ],
  "defaultOutputModes": [
    "text"
  ],
  "description": "sample_agent",
  "name": "sample_agent",
  "preferredTransport": "JSONRPC",
  "protocolVersion": "0.3.0",
  "security": [
    {
      "apiKeyAuth": [
        "apikey_5jrmt****" // The API Key actually used for calling the Agent. The authentication method configured on the page is applied, so there is no need to manually enter the authentication information. The configuration here is applied only if no authentication method is selected on the page.
      ]
    }
  ],
  "securitySchemes": {
    "apiKeyAuth": {
      "type": "apiKey",
      "description": "ApiKey client credentials",
      "in": "header",
      "name": "Authorization"
    }
  },
  "skills": [
    {
      "description": "Chat",
      "id": "0",
      "name": "chat",
      "tags": [
        "chat"
      ]
    }
  ],
  "url": "https://example.volceapi.com/a2a/jsonrpc",
  "version": "1.0.0"
}
```


<span id="KLlgUeSs"></span>
## Parameter description

This section only describes the **core AgentCard parameters for version 0.3.0** for your reference. For complete requirements such as field definitions, value ranges, and validation rules, see [A2A 0.3.0 AgentCard specification](https://a2a-protocol.org/v0.3.0/specification/#55-agentcard-object-structure).


|**Parameter​**  |**Description** |**Sample value** |
|---|---|---|
|**Basic information** |||
|`name` |**Required**. The agent name. |sample_agent |
|`description` |**Required**. A functional description of the agent. |sample_agent |
|`version` |**Required**. The agent version number. We recommend using the semantic versioning format. Example: `1.0.0`. |1.0.0 |
|`url` |**Required.**  The A2A service entry address of the agent. Callers send requests through this address. Enter an agent service address that is accessible on the Internet. |https://example.volceapi.com/a2a/jsonrpc |
|**Protocol and transmission** |||
|`preferredTransport` |**Required**. Specifies the transport protocol preferred by the agent. Common values: `JSONRPC`, `GRPC`, and `HTTP+JSON`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The protocol must match the protocol actually supported by the service that the <code>url</code> points to.</div><br> |JSONRPC |
|`protocolVersion` |**Required**. The A2A protocol version with which the agent complies. |0.3.0 |
|**Capability declaration** |||
|`capabilities` |**Required**. It is the set of optional A2A capabilities supported by the agent. Undeclared capabilities are considered unsupported.<br><br><br>* `streaming`: Whether streaming response is supported. Valid values:<br><br>   * `true`: Supported.<br><br>   * `false`: Unsupported. Default value. |{"streaming":true} |
|**Skill list** |||
|`skills` |**Required**. The list of skills that the agent possesses. At least 1 skill must be configured.<br><br><br>* `id`: Unique identifier of the skill, which must not be duplicated within the current agent.<br><br>* `name`: Skill name.<br><br>* `tags`: An array of skill tags, used for capability retrieval and classification. It must contain at least one tag.<br><br>* `description`: Skill description. |[{"description":"Chat","id":"0","name":"chat","tags":["chat"]}] |
|**Input and output modes** |||
|`defaultInputModes` |**Required**. The list of input media types that the agent supports by default. Example: `text`. |["text"] |
|`defaultOutputModes` |**Required**. The list of output media types supported by the agent by default. Example: `text`. |["text"] |
|**Security and authentication** |||
|`security` |**Optional**. The list of security requirements that must be met when accessing the agent.<br><br><br>* `apiKeyAuth`: Use the apiKeyAuth authentication scheme.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The names in the list must reference the authentication schemes already defined in <code>securitySchemes</code>. Usually there is no need to manually fill in authentication information. In actual calls, the authentication method configured on the page takes precedence. Only when the page is not configured will the authentication information filled in here be used.</div><br> |[{"apiKeyAuth":["apikey_5jrmt\*\*\*\*"]}] |
|`securitySchemes` |**Optional**. The set of authentication scheme definitions supported by the agent.<br><br><br>* `apiKeyAuth`: Authentication scheme name. It can be customized.<br><br>   * `name`: The request header name carrying the API Key.<br><br>   * `in`: Where the API key is passed in the request. Supported: `header`, `query`, or `cookie`.<br><br>   * `type`: Authentication scheme type.<br><br>   * `description`: Authentication scheme description. |{"apiKeyAuth":{"type":"apiKey","description":"ApiKey client credentials","in":"header","name":"Authorization"}} |


<span id="jmCTVDuh"></span>
###
