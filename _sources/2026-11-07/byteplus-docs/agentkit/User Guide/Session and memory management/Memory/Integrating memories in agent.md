---
title: "Integrating memories in agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_memories_in_agent"
---

This topic describes how to integrate memories into an agent.

<span id="9Www1Hql"></span>
## Prerequisites


* Agent code has been built based on the [VeADK](https://volcengine.github.io/veadk-python/agent/agent/) framework.

* [An existing memory has been imported](https://docs.byteplus.com/en/docs/agentkit/Importing_memories).


<span id="Fyw4CEJR"></span>
## Step 1: Configure environment variables

When integrating a memory into the agent, you can configure memory environment variables using either of the following two methods.


* Method 1: Associate the memory in the agent runtime. Refer to [Updating associated memory](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration).

* Method 2: After obtaining the environment variables, configure them in the code.

   1. Obtain information of the configured environment.

      > You can also obtain it by calling the [GetMemoryConnectionInfo](https://docs.byteplus.com/en/docs/agentkit/GetMemoryConnectionInfo_-_Queries_memory_LTM_retrieval_strategy_details) operation.      
      

      1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

      2. In the left\-side navigation pane, select "Memory" to open the Memory page.

      3. Click the target memory ID to open the "Basic information" tab.

      4. Click the "Integration code" tab, and then obtain information about the memory environment variables based on the development framework.

   2. Configure environment variables.

      ```Bash
      export DATABASE_VIKINGMEM_COLLECTION=my_memory
      export DATABASE_VIKINGMEM_MEMORY_TYPE=profile_v1,event_v1
      # If you configure the running memory + VeADK in the agent runtime environment, you do not need to configure AK/SK. For other usage methods, AK/SK must be configured.
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```
      


<span id="VpYzyi5a"></span>
## Step 2: Code integration

<span id="VpYzyi5a"></span>
### VeADK code integration examples

<span id="Ws6SzasL"></span>
#### Viking memory


1. Install veadk, volcengine\-python\-sdk, and volcengine.

   ```JSON
   pip install veadk-python volcengine-python-sdk volcengine
   ```
   

2. Integrate Viking memory in the agent.

   ```Python
   # Refer to the following sample memory integration code and modify the agent code
   import asyncio
   import os
   
   from veadk import Agent, Runner
   from veadk.memory.long_term_memory import LongTermMemory
   from dotenv import load_dotenv
   
   load_dotenv()
   
   collection_name = os.getenv("DATABASE_VIKINGMEM_COLLECTION")
   if not collection_name:
       raise ValueError("DATABASE_VIKINGMEM_COLLECTION environment variable is not set")
   
   long_term_memory = LongTermMemory(backend="viking_mem", index=collection_name)
   
   # Replace the following from your own user & session management system
   app_name = "ltm_demo"
   user_id = "temp_user"
   
   teaching_session_id = "teaching_session"
   student_session_id = "student_session"
   
   agent = Agent(long_term_memory=long_term_memory)
   
   runner = Runner(
       agent=agent,
       app_name=app_name,
       user_id=user_id,
   )
   
   teaching_prompt = "My secret is 0xabcd"
   asyncio.run(runner.run(messages=teaching_prompt, session_id=teaching_session_id))
   
   # save the teaching prompt and answer in long term memory
   asyncio.run(runner.save_session_to_long_term_memory(session_id=teaching_session_id,user_id=user_id))
   
   # now, let's validate this in a new session, with the same user_id configured in the Runner
   student_prompt = "What is my secret?"
   response = asyncio.run(
       runner.run(messages=student_prompt, session_id=student_session_id)
   )
   print(response)
   ```
