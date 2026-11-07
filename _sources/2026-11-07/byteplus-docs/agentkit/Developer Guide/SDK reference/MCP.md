---
title: "MCP"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_SDK"
---

This topic describes how to use VeADK to build a simple agent that calls an MCP service.

## Prerequisites

* Python 3.10 or later is installed. To check the Python version, execute `python --version`.

* The [AgentKit service has been activated](https://console.byteplus.com/AgentKit).

* [ModelArk has been activated](https://console.byteplus.com/ark/openManagement), and [the API Key has been obtained](https://docs.byteplus.com/en/docs/modelark/api-key).

* You have [obtained an Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) in the platform console. You can create and obtain an **Access Key ID** and **Secret Access Key ** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/)page.

* The MCP backend service has been deployed.

## Step 1: Configure the local environment

You can use `uv` or `python3 -m venv` for virtual environment management. In the example provided in this topic, `uv` is used.

1. Configure the virtual environment.

   ```Bash
   mkdir agentkit-mcp-quickstart
   cd agentkit-mcp-quickstart
   uv venv --python 3.12.0
   source .venv/bin/activate
   ```

2. Install dependencies.

   > You can also specify a source with `--index` to speed up installation.

   ```Bash
   uv pip install veadk-python
   uv pip install google-adk
   pip install agentkit-sdk-python
   ```

## Step 2: Create an AgentKit MCP service

1. Log in to the [AgentKit MCP Service console](https://console.byteplus.com/agentkit/region:agentkit+cn-beijing/gateway/mcpservice?pageSize=10&currentPage=1), and create an MCP service for the MCP backend service in the prerequisites. For details, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

2. Obtain the Endpoint and API Key for the MCP service. For details, see [Obtaining MCP service call examples](https://docs.byteplus.com/en/docs/agentkit/Obtaining_sample_calls_svc).

## Step 3: Configure environment variables

```Bash
export MCP_ENDPOINT={{Endpoint obtained in Step 2}}
export MCP_AUTH_KEY={{API Key obtained in Step 2}}
export API_KEY={{ModelArk API Key}}
```

## Step 4: Run the agent

### **Sample code**

```Python
import logging

from veadk import Agent, Runner
from veadk.config import getenv
from agentkit.apps import AgentkitSimpleApp
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, StreamableHTTPConnectionParams

logger = logging.getLogger(__name__)


url = getenv("MCP_ENDPOINT")
mcp_auth_key = getenv("MCP_AUTH_KEY")
apikey = getenv("API_KEY")

mcp_ecs_toolset = MCPToolset(
        connection_params=StreamableHTTPConnectionParams(
        url=url,
        headers={"Authorization": f"Bearer {mcp_auth_key}"}
    ),
)

app = AgentkitSimpleApp()

root_agent = Agent(
    name="ecs_helper",
    model_name="doubao-1-5-pro-256k-250115",
    instruction='''
        Help user find ECS instances and their details.
    ''',
    description="ECS Helper Agent",
    tools=[mcp_ecs_toolset]
)

runner = Runner(agent=root_agent)


@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    prompt = payload["prompt"]
    user_id = headers["user_id"]
    session_id = headers["session_id"]

    logger.info(
        f"Running agent with prompt: {prompt}, user_id: {user_id}, session_id: {session_id}"
    )
    
    # Run agent and automatically handle tool calling
    response = await runner.run(
        messages=prompt, 
        user_id=user_id, 
        session_id=session_id
    )

    logger.info(f"Run response: {response}")
    return response

@app.ping
def ping() -> str:
    """Health check interface"""
    return "pong!"

if __name__ == "__main__":
    # Start local development server
    app.run(host="0.0.0.0", port=8000)
```

### Execute the request

```Python
curl --location 'http://localhost:8000/invoke' \
  --header 'Content-Type: application/json' \
  --header 'user_id: veadk-test' \
  --header 'session_id: local_session' \
  --data '{"prompt": "Analyze my ECS instances."}'
```

### Execution result

```Plain Text
2025-10-24 20:17:33 | INFO | ark_veauth.py:25 - Fetching ARK token...
2025-10-24 20:17:33 | INFO | agent.py:118 - Model extra config: {'extra_headers': {'x-is-encrypted': 'true', 'veadk-source': 'veadk', 'veadk-version': '0.2.13', 'User-Agent': 'VeADK/0.2.13', 'X-Client-Request-Id': 'veadk/0.2.13'}, 'extra_body': {'caching': {'type': 'enabled'}, 'expire_at': 1761311852}}
2025-10-24 20:17:33 | DEBUG | agent.py:127 - LiteLLM client created with config: {'extra_headers': {'x-is-encrypted': 'true', 'veadk-source': 'veadk', 'veadk-version': '0.2.13', 'User-Agent': 'VeADK/0.2.13', 'X-Client-Request-Id': 'veadk/0.2.13'}, 'extra_body': {'caching': {'type': 'enabled'}, 'expire_at': 1761311852}}
2025-10-24 20:17:33 | INFO | agent.py:153 - VeADK version: 0.2.13
2025-10-24 20:17:33 | INFO | agent.py:155 - Agent `ecs_helper` init done.
2025-10-24 20:17:33 | DEBUG | agent.py:156 - Agent: {'name': 'ecs_helper', 'tools': [<google.adk.tools.mcp_tool.mcp_toolset.MCPToolset object at 0x7f8b4f24b9b0>], 'model_name': 'doubao-1-5-pro-256k-250115', 'model_api_base': 'https://ark.cn-beijing.volces.com/api/v3/'}
2025-10-24 20:17:33 | WARNING | runner.py:198 - No short term memory or session service provided, use an in-memory one instead.
2025-10-24 20:17:33 | INFO | runner.py:217 - No long term memory provided.
INFO:     Started server process [1330124]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
2025-10-24 20:18:35 | INFO | runner.py:250 - Run config: speech_config=None response_modalities=None save_input_blobs_as_artifacts=False support_cfc=False streaming_mode=<StreamingMode.NONE: None> output_audio_transcription=AudioTranscriptionConfig() input_audio_transcription=AudioTranscriptionConfig() realtime_input_config=None enable_affective_dialog=None proactivity=None session_resumption=None context_window_compression=None save_live_audio=False max_llm_calls=100
2025-10-24 20:18:35 | DEBUG | runner.py:265 - Auto create session: local_session, user_id: veadk-test, app_name: veadk_default_app
2025-10-24 20:18:38 | DEBUG | runner.py:280 - Function call: id='call_xbyfcvc86wc26mbxz39v****' args={'region': 'cn-beijing', 'needNum': 10} name='describe_instances'
2025-10-24 20:19:14 | DEBUG | runner.py:288 - Event output: The following shows the details of your ECS instances:
1. **Instance 1**：
    - **Instance ID**：i-ye7irm2sqobw80cq****
    - **Creation time**：2025-10-23T21:36:31+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
2. **Instance 2**：
    - **Instance ID**：i-ye7ipm0dtsqc6imh****
    - **Creation time**：2025-10-23T21:05:44+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Debian 12 64 bit
    - **Image ID**：image-ydzwsvy72n46nmxz****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
3. **Instance 3**：
    - **Instance ID**：i-ye7ilsbbpcbw80ca****
    - **Creation time**：2025-10-23T20:06:54+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
4. **Instance 4**：
    - **Instance ID**：i-ye7fg1hgqoxjd1ut****
    - **Creation time**：2025-10-22T14:57:49+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
5. **Instance 5**：
    - **Instance ID**：i-ye5ejwoow0cva4fq****
    - **Creation time**：2025-09-24T14:25:37+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
6. **Instance 6**：
    - **Instance ID**：i-ye5ejub08wbw80bp****
    - **Creation time**：2025-09-24T14:24:35+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
7. **Instance 7**：
    - **Instance ID**：i-ye5e5jyq68bw80c8****
    - **Creation time**：2025-09-24T10:44:54+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
8. **Instance 8**：
    - **Instance ID**：i-ye5c4jbx8gqc6ily****
    - **Creation time**：2025-09-23T16:02:05+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Windows Server 2022 Datacenter Edition 64 - bit Chinese
    - **Image ID**：image-ye5907jc6ikhx1ex****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
9. **Instance 9**：
    - **Instance ID**：i-ye5c4end34xjd1um****
    - **Creation time**：2025-09-23T16:00:05+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Debian 12 64 bit
    - **Image ID**：image-ydzwsvfxhokhx11p****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a
10. **Instance 10**：
    - **Instance ID**：i-ye5blj0xdsxjd1tk****
    - **Creation time**：2025-09-23T11:09:46+08:00
    - **Billing method**：PostPaid (Pay-as-you-go)
    - **Instance type**：ecs.e-c1m2.xlarge
    - **CPU**：CPU: 4 vCPUs (2 cores, 2 threads per core)
    - **Memory**：8192MB
    - **Operating system**：Debian 12 64 bit
    - **Image ID**：image-ydzwsvfxhokhx11p****
    - **Status**：RUNNING (Running)
    - **Availability zone**：cn - beijing - a

All 10 instances above use the Pay-as-you-go billing method and are of the ecs.e-c1m2.xlarge instance type. Most run on the Chinese version of Windows Server 2022 Datacenter Edition 64-bit, with a small number using Debian 12 64-bit. All instances are currently in the RUNNING state and located in the cn-beijing-a availability zone. If you need further analysis or have other operational requirements, feel free to ask me.
```
