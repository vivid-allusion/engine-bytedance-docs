---
title: "Knowledge"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Knowledge_SDK"
---

This topic describes how to use VeADK to build an agent with knowledge base capabilities, powered by VikingDB Knowledge. The agent can answer user questions based on information from the knowledge base.

<span id="Y3O6MWCx"></span>
## Step 1: Create a knowledge base

Log in to the [Knowledge Base console](https://console.byteplus.com/vikingdb/knowledge/region:vdb-knowledge+cn-beijing/collection/list?projectName=default), create a **VikingDB\-Knowledge** knowledge base, and add the following content as `qa.md` to the `customer_support` knowledge base.

```Markdown
# Intelligent customer service knowledge base

## 1. Company profile

VE Technology is a high-tech enterprise focusing on intelligent customer service and knowledge management. Our core product is the **intelligent customer service system**, which provides enterprise customers with efficient and intelligent automated customer service solutions through natural language processing and knowledge base retrieval.

## 2. Product feature description

- **Automatic Q&A**：Quickly respond to common questions based on the knowledge base.
- **Multi-channel access**：Supports web pages, apps, WeChat, Feishu, and other channels.
- **Intelligent recommendation**：Recommend relevant answers based on context.
- **Data analysis**：Provide user question statistics and customer service performance reports.
- **Self-service knowledge base management**：Enable non-technical personnel to quickly edit knowledge content.

---

## 3. FAQ

### Q1: What languages does the intelligent customer service system support?

A1: Currently, it supports **Chinese** and **English**, and multi-language support for Japanese, Korean, and others will be gradually added in the future.

### Q2: Can the system be connected to the existing CRM?

A2: Yes. Our system supports seamless integration with mainstream CRM systems through APIs.

### Q3: What happens if the robot cannot answer a user's question?

A3: The system will automatically transfer the question to human customer service and record the question in the background, making it convenient for administrators to add it to the knowledge base.

### Q4: How often is the knowledge base content updated?

## A4: The knowledge base supports **real-time updates**, which take effect immediately after submission by administrators.

## 4. Contact us

- Official website: [https://www.example.com](https://www.example.com)
- Customer service email: support@ve
- Service hotline：400-123-4567
```


<span id="amsP1IpQ"></span>
## Step 2: Import the knowledge base and obtain environment variables

Log in to the [AgentKit Knowledge Base console](https://console.byteplus.com/agentkit/region:agentkit+cn-shanghai/knowledge) and import the newly created **VikingDB\-Knowledge** knowledge base. After the import succeeds, click "View" in the "Actions" column, and select the "Integration code" tab to obtain the environment variable information.

<span id="betWW3zN"></span>
## Step 3: Build the agent

You do not need to build a veadk project from scratch. We recommend using `agentkit-cli `to create a project from the "Basic Agent App" template (which uses the VeADK framework). After the template\-based creation completes, you need to make the following modifications:


* Associate `Knowledgebase` with the agent.

* Configure the environment variables obtained in [Step 2](https://docs.byteplus.com/en/docs/347/89587#amsP1IpQ) into `agentkit.yaml`.


The final code file is as follows:

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
from veadk.knowledgebase import KnowledgeBase


from agentkit.apps import AgentkitSimpleApp

logger = logging.getLogger(__name__)

collection_name = os.getenv("DATABASE_VIKING_COLLECTION")
if not collection_name:
    raise ValueError("DATABASE_VIKING_COLLECTION environment variable is not set")

model_name = "doubao-seed-1-6-250615"

app = AgentkitSimpleApp()
knowledgebase = KnowledgeBase(backend="viking", index=collection_name)


agent = Agent(
    instruction="Answer customer's questions according to your knowledgebase.",
    model_name=model_name,
    knowledgebase=knowledgebase
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
    return response


@app.ping
def ping() -> str:
    return "pong!"


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```


<span id="XdGqEfkn"></span>
## Step 4: Environment configuration

Add the following configuration to the `agentkit.yaml` file.

```Python
launch_types:
  cloud:
    runtime_envs:
      DATABASE_VIKING_COLLECTION: <your viking collection name>
```


<span id="drSieAvK"></span>
## Step 5: Start the service

Execute `agentkit launch`. After the configuration completes, the Runtime connection information will be automatically saved to the `agentkit.yaml` file.

<span id="AZO52XJ1"></span>
## Step 6: Initiate a call

```Python
agentkit invoke "What products do you have?"
```


You should see the agent successfully retrieve information from the knowledge base and respond by rephrasing the content from `qa.md`.
