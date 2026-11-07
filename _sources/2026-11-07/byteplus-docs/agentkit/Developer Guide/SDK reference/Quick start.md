---
title: "Quick start"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Quick_start"
---

<span id="QhVxq8ir"></span>
## Install

```Bash
pip install agentkit-sdk-python
```


<span id="6iNbzq8B"></span>
## Create a simple agent

```Python
from agentkit.apps import AgentkitSimpleApp
from veadk import Agent, Runner
from veadk.tools.demo_tools import get_city_weather

app = AgentkitSimpleApp()
agent = Agent(tools=[get_city_weather])
runner = Runner(agent=agent)

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    prompt = payload["prompt"]
    user_id = headers["user_id"]
    session_id = headers["session_id"]
    
    response = await runner.run(
        messages=prompt,
        user_id=user_id,
        session_id=session_id
    )
    return response

@app.ping
def ping() -> str:
    return "pong!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8000)
```


<span id="12q64tzv"></span>
## Use the AgentKit service

```Python
from agentkit.sdk.memory import AgentkitMemory
from agentkit.base_client import ApiConfig

# Initialize the client
config = ApiConfig(
    access_key="your_ak",
    secret_key="your_sk"
)
memory_client = AgentkitMemory(config)

# Create a memory
response = memory_client.create_memory_collection(
    name="my-memory",
    short_term_configuration={...},
    long_term_configuration={...}
)
print(f"Memory ID: {response.id}")
```
