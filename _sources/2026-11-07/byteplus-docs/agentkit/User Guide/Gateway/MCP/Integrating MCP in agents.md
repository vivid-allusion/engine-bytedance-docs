---
title: "Integrating MCP in agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_service_in_agent"
---

This topic uses a weather query example to describe how to integrate an MCP service or MCP toolset into an agent built with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en).

> **warning**

> This topic applies only to MCP services and toolsets that use an API Key for inbound identity authentication.

## Prerequisites

* You have built an agent with [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en). For detailed instructions, refer to [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial?lang=en).

* The URL of the MCP service has been obtained. You can obtain it from the call examples of the MCP service or toolset. For details, see [Obtaining MCP service call examples](https://docs.byteplus.com/en/docs/agentkit/Obtaining_sample_calls_svc) or [Obtaining MCP toolset call examples](https://docs.byteplus.com/en/docs/agentkit/Obtaining_sample_calls).

* The inbound API Key of the MCP service has been obtained. You can obtain it on the page displayed after you click "Basic information \> Inbound identity authentication" on the details page of the MCP service or toolset.

## Use VeADK to connect to MCP

The following sample code shows how to integrate the MCP service or toolset that uses an API Key for inbound authentication.

### Integrate an MCP service

1. Configure environment variables.

   ```Bash
   # The URL of the MCP service. It can be obtained from the call examples of the MCP service. For operation details, see Obtaining MCP service call examples.
   export MCP_SERVICE_URL=<mcp_service_url>
   # The inbound API Key credentials of the MCP service.
   export MCP_SERVICE_API_KEY=<mcp_service_api_key>
   # The platform AK and SK.
   export VOLCENGINE_ACCESS_KEY=<your_access_key>
   export VOLCENGINE_SECRET_KEY=<your_secret_key>
   ```

2. Install Python dependencies.

   ```Bash
   pip install veadk-python
   ```

3. Integration example.

   ```Python
   from veadk import Agent, Runner
   from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPConnectionParams
   from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset
   import asyncio
   import os
   
   mcp_service_url = os.getenv("MCP_SERVICE_URL")
   mcp_service_api_key = os.getenv("MCP_SERVICE_API_KEY")
   
   mcp_service_tool = MCPToolset(
       connection_params=StreamableHTTPConnectionParams(
           url=mcp_service_url, headers={"Authorization": f"Bearer {mcp_service_api_key}"}
       ),
   )
   
   agent = Agent(
       # An instruction is a prompt of the agent. This is only an example. You may need to adjust the prompt for specific scenarios.
       instruction="You are an intelligent assistant, skilled at using the mcp_service_tool to solve problems and replying to users' questions politely.",
       tools=[mcp_service_tool],
   )
   
   runner = Runner(agent=agent)
   user_prompt = "Hello, how many steps does it take to put an elephant into a refrigerator?"
   session_id = "mcp_service_session_id_123"
   response = asyncio.run(
       runner.run(messages=user_prompt, session_id=session_id)
   )
   
   print(response)
   ```

### Integrate an MCP toolset

1. Configure environment variables.

   ```Bash
   # The platform AK and SK.
   export VOLCENGINE_ACCESS_KEY=<your_access_key>
   export VOLCENGINE_SECRET_KEY=<your_secret_key>
   # The URL of the MCP toolset. It can be obtained from the call examples of the toolset. For operation details, see Obtaining MCP toolset call examples.
   export TOOL_MCP_ROUTER_URL=<tool_mcp_router_url>
   # The inbound API Key credential for the MCP toolset.
   export TOOL_MCP_ROUTER_API_KEY=<tool_mcp_router_api_key>
   ```

2. Install Python dependencies.

   ```Bash
   pip install veadk-python
   ```

3. Integration example.

   ```Python
   from veadk import Agent, Runner
   from veadk.tools.builtin_tools.mcp_router import mcp_router
   import asyncio
   
   agent = Agent(
       # An instruction is a prompt of the agent. This is only an example. You may need to adjust the prompt for specific scenarios.
       instruction="You are an intelligent assistant, skilled at using the mcp_service_tool to solve problems and replying to users' questions politely.",
       tools=[mcp_router],
   )
   
   runner = Runner(agent=agent)
   user_prompt = "Hello, how many steps does it take to put an elephant into a refrigerator?"
   session_id = "mcp_toolset_session_id_123"
   response = asyncio.run(
       runner.run(messages=user_prompt, session_id=session_id)
   )
   
   print(response)
   ```
