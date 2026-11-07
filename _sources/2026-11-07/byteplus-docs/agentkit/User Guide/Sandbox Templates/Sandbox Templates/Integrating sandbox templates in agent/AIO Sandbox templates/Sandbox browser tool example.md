---
title: "Sandbox browser tool example"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Browser_sandbox_tool_example"
---

This topic uses [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) as an example to describe how to integrate the AIO Sandbox browser sandbox tool into your agent code.

## Prerequisites

* Python 3.10 or later is installed.

* You have created an [AIO Sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) and obtained the tool ID and API Key.

   > If you also need to use the built\-in` run_code `and `execute_skills` capabilities of VeADK, create a Skills Sandbox tool. For integration, follow the guide on [Skills Sandbox template integration](https://docs.byteplus.com/en/docs/agentkit/Usage_example_of_preset_Skills).

* You have [created a sandbox instance](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances) and obtained its access domain name.

* You have created and obtained an **Access Key ID ** and ** a Secret Access Key**. For detailed instructions, see [Obtaining AK/SK](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

## Procedure

1. Configure environment variables.

   ```Bash
   BYTEPLUS#BYTEPLUS After you create the tool in the console, create an instance. Then, set the API key from the tool details page and the access domain name of the instance in environment variables.
   # Note: Modify the routing configuration for the access domain name of the instance by adding "mcp" after ".com/".
   export AGENTKIT_TOOL_ID=t-ye7yhff668o2eybt****
   export BYTEPLUS_ACCESS_KEY=<your_access_key>
   export BYTEPLUS_SECRET_KEY=<your_secret_key>
   export TOOL_MCP_ROUTER_URL=https://sd4hdd25lq5o35lb8****.apigateway-****.volceapi.com/mcp?faasInstanceName=vefaas-ff7mnzmg-vljfx890ua-d4hf78g0j2qqha80****-sandbox
   export TOOL_MCP_ROUTER_API_KEY=6N5KITjwRa9XtyQ4jCZSfVCnq0sG*****
   ```

2. Install Python dependencies.

   ```Bash
   pip install veadk-python
   ```

3. Integration example.

   ```Python
   from veadk import Agent, Runner
   import asyncio
   import os
   from veadk.tools.builtin_tools.mcp_router import mcp_router
   
   agent: Agent = Agent(
       tools=[mcp_router],
   )
   
   runner = Runner(agent=agent)
   built_in_tools_session = "built_in_tools_session"
   user_prompt = "Open the BytePlus official website and check the latest Doubao model."
   response = asyncio.run(
       runner.run(messages=user_prompt, session_id=built_in_tools_session)
   )
   print(response)
   ```

## What to do next

After local development and testing are complete, you can deploy the tool\-integrated agent to the agent runtime. For operation details, see [the guide on deploying an agent to the cloud-based production environment](https://docs.byteplus.com/en/docs/agentkit/Code_sandbox_tool_example#mBP3N57n).
