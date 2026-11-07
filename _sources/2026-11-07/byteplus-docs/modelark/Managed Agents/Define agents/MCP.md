---
title: "MCP"
product: "ModelArk"
product_code: "modelark"
source: "https://docs.byteplus.com/en/docs/modelark/mcp"
---

MCP (Model Context Protocol) is used to connect tools and data sources from third\-party systems to an agent. Through MCP, an agent can access standardized tools exposed by external services, such as code hosting, project collaboration, knowledge bases, or internal business systems.

In ModelArk Managed Agents, MCP configuration is divided into two layers:

* **Agent definition layer**: declares which MCP servers to connect to.

* **Session runtime layer**: injects the corresponding credentials through vaults to complete authentication.

This separation keeps agent definitions reusable and avoids hard\-coding end\-user keys in agent resources.

## Declare MCP servers on an agent

When you create an agent, declare MCP servers through the `mcp_servers` array. Each server requires three parameters:

|Parameter |Note |
|---|---|
|`type` |How the MCP server is declared. Currently, all MCP servers are declared by URL, and the value is `url`. |
|`name` |MCP server name, up to 255 characters. If the name is omitted or does not follow naming rules, the server generates a name based on `url`; if multiple names conflict, the server adds numeric suffixes to subsequent names, so the caller does not need to ensure name uniqueness. To ensure stable subsequent references, we recommend explicitly specifying a lowercase name in `[a-z0-9_-]{1,64}` that remains unique after normalization instead of relying on the server to generate one. |
|`url` |MCP server URL. You cannot configure duplicate URLs in the same agent. |

Each `mcp_toolset` must reference a declared MCP server through `mcp_server_name`. You can also declare only an MCP server without adding the corresponding `mcp_toolset` for now; in this case, the server's tools are not enabled.

The following example attaches a GitHub MCP server to an agent:

**Curl**

```Bash
curl https://ark.ap-southeast.bytepluses.com/api/v3/agents \
  -H "Authorization: Bearer $ARK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "GitHubAssistant",
    "model": {
      "id": "dola-seed-2-1-turbo-260628"
    },
    "mcp_servers": [
      {
        "type": "url",
        "name": "github",
        "url": "https://mcp.example.com/github"
      }
    ],
    "tools": [
      {
        "type": "agent_toolset_20260916"
      },
      {
        "type": "mcp_toolset",
        "mcp_server_name": "github"
      }
    ]
  }'
```

## Control which MCP tools are available

The configuration of `mcp_toolset` is the same as that of built\-in toolsets. It also supports `default_config` and `configs`. The two types of tools use different runtime defaults when `default_config` is explicitly provided but `permission_policy` is omitted: built\-in tools use `always_allow`, while MCP tools use `always_ask`. To avoid execution behavior changing based on the tool type, examples should explicitly configure both `enabled` and `permission_policy`.

If an MCP server exposes many tools, we recommend disabling all of them first, and then enabling specific tools by allowlist:

**Curl**

```Bash
curl https://ark.ap-southeast.bytepluses.com/api/v3/agents \
  -H "Authorization: Bearer $ARK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "SimplifiedGitHubAssistant",
    "model": {
      "id": "dola-seed-2-1-turbo-260628"
    },
    "mcp_servers": [
      {
        "type": "url",
        "name": "github",
        "url": "https://mcp.example.com/github"
      }
    ],
    "tools": [
      {
        "type": "mcp_toolset",
        "mcp_server_name": "github",
        "default_config": {
          "enabled": false,
          "permission_policy": {
            "type": "always_ask"
          }
        },
        "configs": [
          {
            "name": "list_issues",
            "enabled": true
          },
          {
            "name": "get_issue",
            "enabled": true
          },
          {
            "name": "add_issue_comment",
            "enabled": true
          }
        ]
      }
    ]
  }'
```

If you only need to disable a small number of MCP tools, set `default_config.enabled` to `true`, explicitly configure `default_config.permission_policy`, and then set the corresponding tools to `enabled: false` in `configs`. For the complete default matrix, see [Tool permission policy](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/tool-permission-policy).

## Inject MCP credentials in a session

MCP server authentication is not passed in during the agent definition phase. Instead, credentials in vaults are referenced through `vault_ids` when a session is created. This lets the same agent access external systems on behalf of different end users in different sessions.

See the minimal example below:

**Curl**

```Bash
curl https://ark.ap-southeast.bytepluses.com/api/v3/sessions \
  -H "Authorization: Bearer $ARK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "agent": "agent-...",
    "environment_id": "env-...",
    "vault_ids": ["vlt-..."]
  }'
```

For details about how to create vaults, credential types such as `mcp_oauth` / `static_bearer`, and matching rules for multiple vaults, see [Use Vaults authentication](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/use-vaults-authentication).

## Constraints and recommendations

* In the same agent, duplicate `mcp_servers.url` values are not allowed; when `mcp_servers.name` conflicts, the server automatically appends a numeric suffix.

* Each `mcp_toolset` must reference a declared MCP server; declaring only an MCP server does not enable its tools.

* Do not write end\-user tokens directly into the agent definition. Inject them at the session level through vaults.

* **High\-risk tools**: For high\-risk MCP tools, we recommend using `always_ask` together with [Tool permission policy](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/tool-permission-policy).

* **Overly long results**: When an MCP tool in the cloud environment returns overly long plain text, it is handled the same way as built\-in tools, provided that the session has sandbox read and write capabilities; if it does not, the event retains the full result. The client displays `content` from the event; when a task depends on omitted content, the agent continues reading based on the summary. For the complete boundaries, see [Read oversized tool results](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/tools#large-tool-results).

## Related documents

[Agent](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/define-agent)

An agent is a configuration template that contains basic information, system prompt, and extended capabilities.

[Skills](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/skills)

Skills are used to add domain knowledge, operation processes, and best practices to an agent.

[Tools](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/tools)

Tools determine which execution capabilities an agent can call in a session.

[Tool permission policies](https://ai.byteplus.com/ark/region:ap-southeast-1/docs/tool-permission-policy)

Tool permission policies are used to control whether tool calls initiated by an agent are executed automatically or paused for confirmation from business applications.
