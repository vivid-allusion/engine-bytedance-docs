---
title: "Sample JSON file for A2A agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Sample_A2A_agent_JSON_file"
---

The platform allows you to register an A2A agent in an agent space by importing a JSON file. This topic provides sample A2A agent JSON code for this registration scenario.

<span id="OWyfFO6t"></span>
## Sample code

The following example follows the A2A protocol version **0.3.0**. Core fields and required items may differ across protocol versions. Please follow the requirements of the actual protocol version. [Learn more](https://a2a-protocol.org/latest/specification/#441-agentcard)

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
    "description": "hello world agent that can roll a dice of 8 sides and check prime numbers.",
    "name": "hello_world_agent",
    "preferredTransport": "JSONRPC",
    "protocolVersion": "0.3.0",
    "provider": {
        "organization": "agentkit",
        "url": ""
    },
    "security": [
        {
            "apiKeyAuth": []
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
    "url": "https://sd6k****.com",
    "version": "1.0.0"
}
```


<span id="3tNRevuF"></span>
## Parameter description

This section only describes **the core AgentCard parameters for version 0.3.0** for your reference. For complete requirements such as field definitions, value ranges, and validation rules, see [A2A 0.3.0 AgentCard specification](https://a2a-protocol.org/v0.3.0/specification/#55-agentcard-object-structure).


|**Parameter​**  |**Description** |**Sample value** |
|---|---|---|
|**Basic information** |||
|`name` |**Required**. The agent name. |hello_world_agent |
|`description` |**Required**. A functional description of the agent. |hello world agent that can roll a dice of 8 sides and check prime numbers. |
|`version` |**Required**. The agent version number. We recommend using the semantic versioning format. Example: `1.0.0`. |1.0.0 |
|`url` |**Required.**  The A2A service entry address of the agent. Callers send requests through this address. |https://sd6k\*\*\*\*.com |
|**Protocol and transmission** |||
|`preferredTransport` |**Required**. Specifies the transport protocol preferred by the agent. Common values: `JSONRPC`, `GRPC`, and `HTTP+JSON`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The protocol must match the protocol actually supported by the service that the <code>url</code> points to.</div><br> |JSONRPC |
|`protocolVersion` |**Required**. The A2A protocol version followed by the agent. |0.3.0 |
|**Capability declaration** |||
|`capabilities` |**Required**. The set of optional A2A capabilities supported by the agent. Undeclared capabilities are unavailable.<br><br><br>* `streaming`: Whether streaming response is supported. Valid values:<br><br>   * `true`: Supported.<br><br>   * `false`: Unsupported. Default value. |{"streaming":true} |
|**Skills** |||
|`skills` |**Required**. The list of the agent's skills. Configure at least one skill.<br><br><br>* `id`: Unique identifier of the skill, which must not be duplicated within the current agent.<br><br>* `name`: Skill name.<br><br>* `tags`: An array of skill tags, used for capability retrieval and classification. It must contain at least one tag.<br><br>* `description`: Skill description. |[{"description":"Chat","id":"0","name":"chat","tags":["chat"]}] |
|**Input and output modes** |||
|`defaultInputModes` |**Required**. The list of input media types supported by the agent by default. Example: `text`. |["text"] |
|`defaultOutputModes` |**Required**. The list of output media types supported by the agent by default. Example: `text`. |["text"] |
|**Service provider** |||
|`provider` |**Optional**. Information about the agent service provider.<br><br><br>* `organization`: Name of the organization providing the agent service.<br><br>* `url`: The web address of the service provider. |{"organization":"agentkit","url":""} |
|**Security and authentication** |||
|`security` |**Optional**. The list of security requirements that must be met when accessing the agent.<br><br><br>* `apiKeyAuth`: Use the apiKeyAuth authentication scheme.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The names in the list must reference the authentication schemes already defined in <code>securitySchemes</code>.</div><br> |[{"apiKeyAuth":[]}] |
|`securitySchemes` |**Optional**. The set of authentication scheme definitions supported by the agent.<br><br><br>* `apiKeyAuth`: Authentication scheme name. It can be customized.<br><br>   * `name`: The request header name carrying the API Key.<br><br>   * `in`: Where the API key is passed in the request. Supported: `header`, `query`, or `cookie`.<br><br>   * `type`: Authentication scheme type.<br><br>   * `description`: Authentication scheme description. |{"apiKeyAuth":{"type":"apiKey","description":"ApiKey client credentials","in":"header","name":"Authorization"}} |


<span id="c6YuxhoE"></span>
###
