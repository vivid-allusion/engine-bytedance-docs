---
title: "Sandbox code tool example"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Code_sandbox_tool_example"
---

This topic uses [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) as an example to describe how to integrate the AIO Sandbox code sandbox tool into your agent code.

## Prerequisites

* Python 3.10 or later is installed.

* You have[ created an AIO Sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools)and obtained the tool ID.

   > If you also need to use the built\-in` run_code `and `execute_skills `capabilities of VeADK, create a Skills Sandbox tool. For integration, follow the guide on [Skills Sandbox template integration](https://docs.byteplus.com/en/docs/agentkit/Usage_example_of_preset_Skills).

* You have created and obtained an **Access Key ID ** and a **Secret Access Key**. For detailed instructions, see [Obtaining AK/SK](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

## Tool instance calling mechanism

AIO Sandbox code sandbox tools support session\-based intelligent scheduling management:

* **Automatic creation**: When a `session_id` is used to initiate a request for the first time, the system automatically creates a corresponding tool instance.

* **Session reuse**: Multiple requests with the same `session_id` share the same tool instance, ensuring continuity of the code execution context.

* **Lifecycle**: Each instance has a default validity period of 30 minutes and is automatically terminated upon expiration. You can also manually adjust the instance lifecycle duration. For details, see[ Updating lifecycle duration](https://docs.byteplus.com/en/docs/agentkit/Modify_the_lifecycle_duration_of_a_tool_instance).

* **Isolation**: Requests with different `session_id` values run in independent sandbox environments and do not affect each other.

## Procedure

1. Configure environment variables.

   * Method 1: After a tool is integrated into the agent, associate the tool on the component association page in the agent runtime. After association, the system automatically injects the required environment variables for the agent runtime\-managed resources. For details, see [Associating components](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration).

   * Method 2: Direct configuration.

      ```Bash
      # After you create the tool in the console, set the tool ID and the platform AK/SK in environment variables.
      export AGENTKIT_TOOL_ID=t-ye7yhff668o2eybt****
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```

2. Install Python dependencies.

   ```Bash
   pip install veadk-python
   ```

3. Integration example.

   ```Python
   from veadk import Agent, Runner
   import asyncio
   from veadk.tools.builtin_tools.run_code import run_code
   
   agent: Agent = Agent(
       tools=[run_code],
   )
   
   runner = Runner(agent=agent)
   built_in_tools_session = "built_in_tools_session"
   user_prompt ="Give me a random prime number between 50 and 100."
   response = asyncio.run(
       runner.run(messages=user_prompt, session_id=built_in_tools_session)
   )
   print(response)
   ```

## Deploy the agent to the cloud\-based production environment

After local development and testing are complete, you can deploy the tool\-integrated agent to the agent runtime.

1. **Package the code**: Ensure all dependencies are correctly specified in `requirements.txt`.

2. **Deploy the agent to an agent runtime.**  During deployment, the system automatically injects the necessary environment information. Manual configuration is not required. The following two deployment methods are currently supported:

   * [Developing and deploying agents with AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)

   * [Creating agent runtimes in console](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)
