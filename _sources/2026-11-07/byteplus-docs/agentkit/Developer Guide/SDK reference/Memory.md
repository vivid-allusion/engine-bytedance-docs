---
title: "Memory"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Memory_SDK"
---

This topic uses the Viking memory as an example to guide you through installing dependencies and using VeADK to build an agent with long\-term memory capabilities.

<span id="3VzZw2mU"></span>
## Prerequisites

You have [imported the memory](https://docs.byteplus.com/en/docs/agentkit/Importing_memories) and [obtained the information about the memory environment variables](https://docs.byteplus.com/en/docs/agentkit/Integrating_memories_in_agent?lang=en#Fyw4CEJR).

<span id="t4Xk1QZ9"></span>
## Step 1: Build the Agent

You do not need to build a veadk project from scratch. We recommend using `agentkit-cli `to create a project from the "Basic Agent App" template (which uses the VeADK framework). After the template\-based creation completes, you need to make the following modifications:


* Associate `LongTermMemory` with the Agent.

* Configure the environment variables obtained in the previous section in `agentkit.yaml`.

* After each round of conversation, explicitly call `runner.save_session_to_long_term_memory` to persist the conversation results to the long\-term memory.


The modified code file is as follows:

```Python
'''
**simple agent demo app**

Before running, the user must set the following environment variables; otherwise, runtime exceptions will inevitably occur:
- MODEL_AGENT_NAME  # model id in BytePlus Ark platform
- MODEL_AGENT_API_KEY  # model api key in BytePlus Ark platform

MODEL_AGENT_NAME and MODEL_AGENT_API_KEY are used to access the model service of the BytePlus Ark platform.
'''
import logging
import os

from veadk import Agent, Runner
from veadk.memory.long_term_memory import LongTermMemory


from agentkit.apps import AgentkitSimpleApp

logger = logging.getLogger(__name__)

backend = "viking_mem"
collection_name = os.getenv("DATABASE_VIKINGMEM_COLLECTION")
if not collection_name:
  raise ValueError("DATABASE_VIKINGMEM_COLLECTION environment variable is not set")
index = collection_name

app = AgentkitSimpleApp()
long_term_memory = LongTermMemory(
  backend=backend,
  index=index
)

agent = Agent(
  name="simple_app_agent",
  instruction="You are a helpful assistant.",
  long_term_memory=long_term_memory
)
runner = Runner(agent=agent)


@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    prompt = payload["prompt"]
    user_id = headers["user_id"]
    session_id = headers["session_id"]

    logger.info(
        f"Running agent with prompt: {prompt}, user_id: {user_id}, session_id: {session_id}"
    )
    response = await runner.run(messages=prompt, user_id=user_id, session_id=session_id)

    logger.info(f"Run response: {response}")

    # save the teaching prompt and answer in long term memory
    await runner.save_session_to_long_term_memory(session_id=session_id, user_id=user_id)

    return response


@app.ping
def ping() -> str:
    return "pong!"


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```


<span id="5ltlWmvU"></span>
## Step 2: Environment configuration

Add the following configuration to the `agentkit.yaml` file:

```YAML

# Add the following configuration when the long-term memory backend is the Viking memory
launch_types:
  cloud:
    runtime_envs:
      DATABASE_VIKINGMEM_COLLECTION: <your vikingdb collection name>
      DATABASE_VIKINGMEM_MEMORY_TYPE: <your vikingdb memory type, defaults to "event_v1", separate multiple by comma, e.g. event_v1,event_v2>
```


<span id="sOAiAGBD"></span>
## Step 3: Start the service

Execute `agentkit launch`. After the configuration completes, the Runtime connection information will be automatically saved to the `agentkit.yaml` file.

<span id="STSJwetS"></span>
## Step 4: Initiate a call

`user_id="agentkit_user"` and `session_id="agentkit_sample_session"` will automatically be used to initiate the call.

```Bash
agentkit invoke "My secret is 0xabcd"
```


<span id="9hSUu9c0"></span>
## Step 5: Verify the effectiveness of the memory strategy

The password has been saved after the first call completes. To verify whether the agent can correctly retrieve data from the memory, initiate a new call with a different session_id. It is recommended to wait about 1 minute for long\-term memory extraction to complete before making the call.

```Bash
agentkit invoke \
  --payload '{"prompt": "What is my secret?"}' \
  --headers '{"user_id": "agentkit_user", "session_id": "s123"}'
```


After the execution completes, you will see that the agent successfully retrieves information from the memory and returns your password.
