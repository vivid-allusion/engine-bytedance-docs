---
title: "Tools"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Tools_SDK"
---

This topic describes how to use [VeADK](https://github.com/volcengine/veadk-python) to build an agent that safely executes code in a sandbox environment by integrating the `run_code` tool from built\-in tools.

We recommend using `agentkit-cli` to create a project from the Basic Agent template. After the template\-based creation completes, you need to make the following modifications:

* Add the code execution tool `run_code` to the agent.

* Set the environment variable `AGENTKIT_TOOL_ID` to your sandbox tool instance ID.

**The complete code is as follows:**

Save the code as `simple_agent_tool.py`. For more tool integration examples, see [Integrating tools in agent](https://docs.byteplus.com/en/docs/agentkit/Code_sandbox_tool_example).

```Python
from veadk import Agent, Runner
from veadk.tools.builtin_tools.run_code import run_code
from agentkit.apps import AgentkitSimpleApp

app = AgentkitSimpleApp()
agent: Agent = Agent(
    tools=[run_code],
)
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

**Parameter description**

* **run_code tool**: Provides a secure code execution environment. Supports multiple programming languages including Python and JavaScript.

* **session_id**: Identifies a user session. Requests with the same session_id share a sandbox instance.

* **Asynchronous processing**: Uses `async/await` syntax to support high\-concurrency requests.

## Local testing

1. Install Python dependencies.

   * Create and activate a virtual environment based on Python 3.10 using `uv`.

      ```Python
      uv venv --python 3.10
      
      source .venv/bin/activate
      ```

   * Install from PyPI

      ```Python
      pip install veadk-python
      ```

2. Configure environment variables.

   ```Python
   # Required configuration: Sandbox tool ID (obtained from the console or by calling the ListTools operation)
   export AGENTKIT_TOOL_ID=t-ye7fhfmghsc1kdxxxxxx
   
   # Required configuration: BytePlus access credentials
   export BYTEPLUS_ACCESS_KEY=<your_access_key>
   export BYTEPLUS_SECRET_KEY=<your_secret_key>
   ```

3. Start the agent service locally.

   After the service starts successfully, it will listen on `http://0.0.0.0:8000`. You can call the agent via this address.

   ```Python
   python simple_agent_tool.py
   ```

4. Call the agent.

   > **tip**

   > `user_id`: User identifier.

   > `session_id`: Session identifier, used to associate the sandbox instance.

   ```Python
   curl --location 'http://localhost:8000/invoke' \
     --header 'Content-Type: application/json' \
     --header 'user_id: veadk-test' \
     --header 'session_id: local_session' \
     --data '{"prompt": "Give me a random prime number between 50 and 100."}'
   ```

   After the call succeeds, detailed execution logs are printed to the console.

   ```Python
   2025-11-23 21:10:24 | DEBUG | runner.py:578 - Function call: id='call_jwrcwdayjj8xnlgalyzzcoqq' args={'code': 'import random\n\ndef is_prime(n):\n    if n <= 1:\n        return False\n    if n == 2:\n        return True\n    if n % 2 == 0:\n        return False\n    for i in range(3, int(n**0.5) + 1, 2):\n        if n % i == 0:\n            return False\n    return True\n\nprimes_between = [p for p in range(50, 101) if is_prime(p)]\nrandom_prime = random.choice(primes_between)\nprint(random_prime)', 'language': 'python3'} name='run_code'
   2025-11-23 21:10:24 | DEBUG | run_code.py:48 - tools endpoint: agentkit.cn-beijing.volces.com
   2025-11-23 21:10:24 | DEBUG | run_code.py:54 - tool_user_session_id: veAgent_veadk-test_local_session
   2025-11-23 21:10:24 | DEBUG | run_code.py:56 - Running code in language: python3, session_id=local_session, code=import random
   
   def is_prime(n):
       if n <= 1:
           return False
       if n == 2:
           return True
       if n % 2 == 0:
           return False
       for i in range(3, int(n**0.5) + 1, 2):
           if n % i == 0:
               return False
       return True
   
   primes_between = [p for p in range(50, 101) if is_prime(p)]
   random_prime = random.choice(primes_between)
   print(random_prime), tool_id=t-ye7yhff668o2eybtfvr0, host=agentkit.cn-beijing.volces.com, service=agentkit, region=cn-beijing
   2025-11-23 21:10:24 | DEBUG | run_code.py:65 - Get AK/SK from tool context failed.
   2025-11-23 21:10:24 | DEBUG | run_code.py:77 - Successfully get AK/SK from environment variables.
   2025-11-23 21:10:25 | DEBUG | run_code.py:103 - Invoke run code response: {'ResponseMetadata': {'RequestId': '****', 'Action': 'InvokeTool', 'Version': '2025-10-30', 'Service': 'agentkit', 'Region': 'cn-beijing'}, 'Result': {'ToolId': 't-****', 'UserSessionId': '****', 'SessionId': 's-****', 'Endpoint': '', 'InternalEndpoint': '', 'Result': '{\n  "success": true,\n  "message": "Code executed successfully",\n  "data": {\n    "kernel_name": "python3",\n    "session_id": "****",\n    "status": "ok",\n    "execution_count": 1,\n    "outputs": [\n      {\n        "output_type": "stream",\n        "name": "stdout",\n        "text": "67\\n",\n        "data": null,\n        "metadata": {},\n        "execution_count": null,\n        "ename": null,\n        "evalue": null,\n        "traceback": null\n      }\n    ],\n    "code": "import random\\n\\ndef is_prime(n):\\n    if n \\u003c= 1:\\n        return False\\n    if n == 2:\\n        return True\\n    if n % 2 == 0:\\n        return False\\n    for i in range(3, int(n**0.5) + 1, 2):\\n        if n % i == 0:\\n            return False\\n    return True\\n\\nprimes_between = [p for p in range(50, 101) if is_prime(p)]\\nrandom_prime = random.choice(primes_between)\\nprint(random_prime)",\n    "msg_id": "****"\n  }\n}'}}
   2025-11-23 21:10:38 | DEBUG | runner.py:586 - Event output: Random prime number between 50 and 100: 67
   2025-11-23 21:10:38 | WARNING | runner.py:652 - No tracer is configured in the agent, no trace id provided.
   INFO:     127.0.0.1:52785 - "POST /invoke HTTP/1.1" 200 OK
   ```

## Deploy the agent to the cloud\-based production environment

After local development and testing are complete, you can deploy the tool\-integrated agent to the agent runtime.

1. Package the code: Ensure all dependencies are correctly specified in` requirements.txt`.

2. Deploy the agent to the agent runtime. During deployment, the system automatically injects the necessary environment information. Manual configuration is not required. The following two deployment methods are currently supported:

   * [Creating runtimes via CLI tool](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)

   * [Creating agent runtimes in console](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console)

3. After deployment, you can call the agent through the API or SDK provided by the platform. Call examples:

   ```Python
   agentkit invoke "Give me a random prime number between 50 and 100."
   ```
