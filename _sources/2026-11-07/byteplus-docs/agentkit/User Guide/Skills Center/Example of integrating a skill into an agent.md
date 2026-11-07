---
title: "Example of integrating a skill into an agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_Skills_into_agent"
---

This topic uses [VeADK](https://deepwiki.com/volcengine/veadk-python/1-overview) as an example to describe how to integrate a preset skill into your **agent** code. This enables the **agent** to retrieve and execute the target skill at runtime, thereby extending its task processing capabilities.

## Prerequisites

* AK/SK has been obtained. If not, log in to the platform console. Navigate to the [API Access Key](https://console.byteplus.com/iam/keymanage/) page and create and retrieve the Access Key ID and Secret Access Key.

   > **warning**

   > Keep your AK/SK credentials confidential. AK/SK credentials are the primary identity credentials for platform API calls and carry account\-level permissions. Do not disclose, forward, or publicly expose them because credential leakage may cause account data security and business risks.

* You have installed Python **3.10 or later** in the local development environment. If you have not installed Python, go to the [official Python website ](https://www.python.org/downloads/)to download and install the required version.

   > Earlier Python versions have syntax and standard library compatibility issues and cannot support the dependencies that the skill requires. We recommend installing a stable version of Python 3.10 or later.

* You have created a skills space and obtained the space ID. For more information, see [Skills spaces](https://docs.byteplus.com/en/docs/agentkit/Skills_space).

* You have created a skill sandbox tool and obtained the tool ID. For operation details, see [Creating tools](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).

## Procedure

1. Configure environment variables.

   ```Bash
   # The platform AK and SK.
   # The Tool ID of the skill sandbox created on the AgentKit platform.
   export AGENTKIT_TOOL_ID=<agentkit_tool_id>
   # The ID of the skills space.
   export SKILL_SPACE_ID=<skill_space_id>
   ```

2. Install the dependency package in the local development environment.

   ```Bash
   pip install 'veadk-python==1.1.5'
   ```

3. Integration example.

   ```Python
   from veadk import Agent, Runner
   from veadk.tools.builtin_tools.execute_skills import execute_skills
   
   root_agent = Agent(
       name="skill_agent",
       instruction="Invoke the execute_skills tool to execute the技能based on the user's requirements.",
       tools=[execute_skills],
   )
   
   runner = Runner(agent=root_agent)
   
   # If you want to use a specific skill, we recommend that you directly declare the skill name in the prompt.
   user_prompt = f"""
       Please execute the following workflow:
       1. Utilize the skill-creator skill to generate a streamlined PDF processing skill with PDF loading and editing capabilities.
       2. Register the finalized skill to the skill space.
   """
   session_id = "skill_session_123"
   response = asyncio.run(
       runner.run(messages=user_prompt, session_id=session_id)
   )
   
   print(response)
   ```

## What to do next

After local development and testing are complete, you can deploy the tool\-integrated agent to the agent runtime. For operation details, see [the guide on deploying an agent to the cloud-based production environment](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool?lang=en).
