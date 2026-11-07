---
title: "Runtime"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Runtime_SDK"
---

This guide will walk you through the entire process, from environment setup and local development/debugging to deploying your ** Agent** to a production environment.

<span id="Gr4H9srQ"></span>
## Prerequisites


* You have activated [AgentKit ](https://console.byteplus.com/AgentKit)and [Container Registry](https://console.byteplus.com/cr).

* Log in to the platform console to create and retrieve the ** Access Key ID** and **Secret Access Key**.

* Python 3.10 or later has been installed. To check the Python version, execute `python --version`.


<span id="oxxnjmqY"></span>
## Step 1: Configure the environment

We recommend using `uv` or `python3 -m venv` to manage your Python virtual environment. This topic uses `uv` as an example.

For the `uv` installation guide, refer to [uv installation](https://docs.astral.sh/uv/getting-started/installation/).


1. Create and activate the virtual environment.

   ```Bash
   mkdir agentkit-runtime-quickstart
   cd agentkit-runtime-quickstart
   uv venv --python 3.12.0
   source .venv/bin/activate
   ```
   

2. Install core dependencies.

   > You can specify the mirror site by using the parameter `--index` to speed up installation.   
   

   ```Bash
   uv add veadk-python
   uv add agentkit-sdk-python
   ```
   


<span id="7zdzFQpd"></span>
## Step 2: Agent creation and local test

<span id="IBXkhNsH"></span>
### Initialize the Agent project

We recommend that you use `agentkit-cli` to quickly start the project. You can use the `init` command to create a well\-structured, streaming\-enabled **Agent ** project from a template.

```Bash
# Use agentkit-cli to create a project from a template
agentkit init
```


After you execute the command, a project structure containing `simple_agent.py `and `requirements.txt` is automatically generated, allowing you to start development immediately.

<span id="mBQVp8Pl"></span>
### Agent code overview

The core code of `simple_agent.py` generated from the `basic_stream` template is as follows. It demonstrates how to wrap a **VeADK** **Agent ** based on **AgentkitSimpleApp**, execute it via **Runner**, and return the result as an SSE (Server\-Sent Events) event stream.

```Python
import json
import logging

from google.adk.agents import RunConfig
from google.adk.agents.run_config import StreamingMode
from google.genai.types import Content, Part
from veadk import Agent, Runner

from agentkit.apps import AgentkitSimpleApp
from veadk.prompts.agent_default_prompt import DEFAULT_DESCRIPTION, DEFAULT_INSTRUCTION

logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

app = AgentkitSimpleApp()

app_name = "simple_streamable_app"

agent_name = "Agent"
description = DEFAULT_DESCRIPTION
system_prompt = DEFAULT_INSTRUCTION


tools = []

# from veadk.tools.builtin_tools.web_search import web_search
# tools.append(web_search)


agent = Agent(
    name=agent_name,
    description=description,
    instruction=system_prompt,
    tools=tools,
)
agent.model._additional_args["stream_options"] = {"include_usage": True}
runner = Runner(agent=agent, app_name=app_name)


@app.entrypoint
async def run(payload: dict, headers: dict):
    prompt = payload["prompt"]
    user_id = headers["user_id"]
    session_id = headers["session_id"]

    logger.info(
        f"Running agent with prompt: {prompt}, user_id: {user_id}, session_id: {session_id}"
    )

    session_service = runner.short_term_memory.session_service  # type: ignore

    # prevent session recreation
    session = await session_service.get_session(
        app_name=app_name, user_id=user_id, session_id=session_id
    )
    if not session:
        await session_service.create_session(
            app_name=app_name, user_id=user_id, session_id=session_id
        )

    new_message = Content(role="user", parts=[Part(text=prompt)])
    try:
        async for event in runner.run_async(
            user_id=user_id,
            session_id=session_id,
            new_message=new_message,
            run_config=RunConfig(streaming_mode=StreamingMode.SSE),
        ):
            # Format as SSE data
            sse_event = event.model_dump_json(exclude_none=True, by_alias=True)
            logger.debug("Generated event in agent run streaming: %s", sse_event)
            yield sse_event
    except Exception as e:
        logger.exception("Error in event_generator: %s", e)
        # You might want to yield an error event here
        error_data = json.dumps({"error": str(e)})
        yield error_data


@app.ping
def ping() -> str:
    return "pong!"


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```


**Key features of the code**:


* Uses the Doubao model from ModelArk by default and automatically manages the model API Key.

* Built\-in session management logic. This ensures continuity across multi\-turn conversations.

* Achieves seamless integration with **AgentKit Runtime** through AgentkitSimpleApp.


<span id="bUDguuwP"></span>
### Configure environment variables.

Before starting the **Agent** service, you need to configure BytePlus credentials:

```Bash
# Required: Configure your BytePlus access credentials
export BYTEPLUS_ACCESS_KEY=<your_access_key>
export BYTEPLUS_SECRET_KEY=<your_secret_key>
```


<span id="dqTdQZGu"></span>
### Start and call the service locally

Execute the following command to start the **Agent** service.

```Bash
python simple_agent.py
```


The service will listen on `http://0.0.0.0:8000`. Now, open another terminal and use curl to test your **Agent**:

```Bash
curl --location 'http://localhost:8000/invoke' \
  --header 'Content-Type: application/json' \
  --header 'user_id: test' \
  --header 'session_id: local_session' \
  --data '{"prompt": "Tell me a joke!"}'
```


**Parameter descriptions:** 


* user_id: user identifier

* session_id: session identifier

* prompt: user natural language request


**Execution logs example**

After the call succeeds, detailed execution logs are output to the console.

```Bash
INFO:     Started server process [38120]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
INFO:     127.0.0.1:60807 - "POST /invoke HTTP/1.1" 200 OK
INFO:__main__:Running agent with prompt: Tell me a joke!, user_id: test, session_id: local_session
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output: Why
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  did
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  the
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  AI
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  apply
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  for
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  a
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  job
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  at
2025-12-01 20:12:50 | DEBUG | runner.py:151 - Event output:  the
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  bakery
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: ?
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: Because
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  it
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  wanted
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  to
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  work
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  on
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  its
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  **
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: d
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: ough
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: **
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  processing
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  skills
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: !
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output:  😄
2025-12-01 20:12:51 | DEBUG | runner.py:151 - Event output: Why did the AI apply for a job at the bakery?

Because it wanted to work on its **dough** processing skills! 😄
```


<span id="T555eTeP"></span>
## Step 3: Deploy the agent to the production environment

After local development and testing are complete, you can deploy the agent to the AgentKit platform:


1. **Package the code**: Ensure all dependencies are correctly specified in requirements.txt. The code generated from the template already includes all necessary dependencies by default.

2. **Platform deployment**: Follow the [Quick start] guide to configure and deploy your application using the agentkit config and agentkit launch commands.

3. **Call the application**: Once deployed, you can call the Agent via the API or SDK provided by the platform. Sample call:


```Bash
agentkit invoke "Tell me a joke!"
```


You have now completed the end\-to\-end journey from local development to cloud deployment!
