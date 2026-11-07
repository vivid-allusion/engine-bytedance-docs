---
title: "veRL integration with veFaaS cloud sandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/veRL_integration_with_veFaaS_cloud_sandbox"
---

This article describes how to obtain the configuration parameter required for veRL integration with veFaaS cloud sandbox, and complete environment connection and connectivity verification.

<span id="aC89xkXo"></span>
## Background information

The core technologies and platform concepts involved in this article are described as follows:


* **Cloud sandbox**: A security\-isolated, resource\-controlled temporary cloud execution environment used to securely run code or tasks, preventing impact on external systems.

* **veRL (BytePlus Reinforcement Learning)** : An open\-source large model reinforcement learning training framework from BytePlus, capable of efficiently completing RLHF alignment training for LLMs, and supporting connection to cloud sandbox for secure tool execution and environment interaction.

* **LLM (Large Language Model)** : A large parameter language model based on Transformer and trained on massive text data, with capabilities for understanding, generation, reasoning, and conversation. It serves as the core foundation of current AI applications.

* **RLHF (Reinforcement Learning from Human Feedback)** : An alignment training method used to make large models output results that better fit human intentions and are more secure and reliable.

* **SWE\-bench**: A benchmark dataset and evaluation framework specifically designed to assess large models' capabilities on "real software engineering tasks".


<span id="bmKnpTLq"></span>
## Prerequisites


* The API access key has been obtained. For specific operations, see [Access Key (key) management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).

* An API gateway instance and corresponding service (domain names) have been created to expose the application interface externally. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance?LibVersion=markdown备份版本) and [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service?LibVersion=markdown备份版本).


<span id="KrMI96Ne"></span>
## Procedure

<span id="pD9OqAto"></span>
### Step 1: Create and release a sandbox application

Create a cloud sandbox application for veRL training.


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the left navigation bar, select **cloud sandbox** \> **sandbox application**.

3. Click the **create sandbox application** button.

4. On the creation page, pay special attention to the following configuration. Keep other configuration as default. For detailed description, see [sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications).

&nbsp;

   
   |Category |Parameter |Description |
   |---|---|---|
   |For sandbox images |Container image |Select **public image**. |
   ||Select images |Select **SWE\-bench  **  type and select the target image. This example selects the image with **image ID** `dm2t11rzrt`. |
   ||Startup command |Start command for the sandbox. This example uses `curl -fsSL https://vefaas-swe.tos-cn-beijing.ivolces.com/swe-rex/install_1.4.0.sh \| bash -s -- ixcprx`. |
   ||Listening port |Set to **8000**. |
   |Gateway routing configuration |Domain type |Select **unified domain**. |
   ||APIG instance |Select the API Gateway instance created. API gateway instance and service (domain), used to expose application interfaces externally. For detailed actions to create gateway instances and services, see [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance?LibVersion=markdown备份版本) and [Create service](https://docs.byteplus.com/en/docs/apig/Creating_a_service?LibVersion=markdown备份版本). |
   |Environment variables |Environment variables |Configure the environment variables for running the sandbox. This example requires adding the following environment variables on top of the default environment variables. Click **Edit in JSON format** and add the following configuration.<br><br>```JSON```<br>```{```<br>```  "HOME": "/root",```<br>```  "PIP_INDEX_URL": "https://mirrors.ivolces.com/pypi/simple/"```<br>```}```<br> |
   |Advanced settings |Instance specification |To ensure the task is executed smoothly, it is recommended to select an instance specification with at least **2 vCPU, 4 GiB memory** when creating a sandbox instance. |
   ||Execution timeout |It is recommended to set **650 ** s to avoid timeout when processing complex tasks. |
   

5. At the bottom of the page, click **confirm**.

6. After creation is complete, in the upper right corner of the application details page, click **release \> confirm** to publish the application.


<span id="KXhy7RTQ"></span>
### Step 2: Obtain the sandbox application ID and access address

Find the required sandbox application ID and access address for integration on the sandbox application details page.


* **Sandbox application ID**: In **Basic information** \> **ID**, obtain the sandbox application's ID.

* **Access address**: In **Gateway route configuration** \> **Configuration information**, obtain the sandbox application's **access address**.


<span id="httJA9al"></span>
### Step 3: Configure and verify in veRL

It is recommended to use the environment variable configuration method to configure the above key information in your veRL training environment.


1. **Configure environment variables**

   In your training environment, create a `.env ` file and enter the following content.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace the sample values with the actual information you have obtained.   </div>
   

   ```Bash
   # BytePlus cloud service access credentials
   VEFAAS_ACCESS_KEY="YOUR_VOLC_ACCESS_KEY_ID"
   VEFAAS_SECRET_KEY="YOUR_VOLC_SECRET_ACCESS_KEY"
   
   # veFaaS cloud sandbox application configuration
   VEFAAS_FUNCTION_ID="s1lw****" # Sample value, please replace
   VEFAAS_FUNCTION_ROUTE="https://example.apigateway.volceapi.com" # Sample value, please replace
   ```
   

   
   |Environment variable name |Description |
   |---|---|
   |VOLCE_ACCESS_KEY |BytePlus access key. |
   |VOLCE_SECRET_KEY ||
   |VEFAAS_FUNCTION_ID |ID of the sandbox application. |
   |VEFAAS_FUNCTION_ROUTE |Sandbox application's access address. |
   

2. **Minimal verification**

   After completing the configuration, execute the following command to verify the connectivity between the veRL environment and the cloud sandbox. The command will start the Python 3.12 environment, complete initialization, dependency installation, and code execution, and perform a single minimal verification.

   ```Python
   import os
   import shlex
   import uuid
   
   from vergent.interaction import AgentEnv, AgentEnvConfig
   from vergent.tools import ToolConfig
   
   # step 1: create environment
   run_id = str(uuid.uuid4())
   impl = os.getenv("DEPLOYMENT", "vefaas").lower()
   
   env_config = {
       "deployment": {
           "type": "vefaas",
           "image": "enterprise-public-2-cn-beijing.cr.volces.com/vefaas-public/python:3.12",
           "command": "curl -fsSL https://****-test-empty.tos-cn-beijing.ivolces.com/bin/tos_swe_rex.sh | bash -s -- ixcprx",
           "timeout": 300.0,
           "startup_timeout": 180.0,
           "function_id": os.getenv("VEFAAS_FUNCTION_ID"),
           "function_route": os.getenv("VEFAAS_FUNCTION_ROUTE"),
       },
       "env_variables": {
           "PIP_PROGRESS_BAR": "off",
       },
   }
   env_config = AgentEnvConfig(**env_config)
   env = AgentEnv(run_id=run_id, env_config=env_config)
   env.start()
   
   # install tools in the environment
   tools_config = [
       {"name": "execute_bash"},
       {"name": "str_replace_editor"},
   ]
   tools = [ToolConfig(**tool_config).get_tool() for tool_config in tools_config]
   env.install_tools(tools)
   out = env.communicate("which str_replace_editor")
   print(f"[Tool check] which str_replace_editor\n  -> {out.strip()}\n")
   
   # --- Simple sandbox demo: create script -> run -> output to file -> cat (shows persistence) ---
   print("=" * 60)
   print("  Sandbox demo: create script -> run -> output to file -> cat")
   print("=" * 60)
   
   # 1. Install dependency (persists in this sandbox)
   print("\n[Step 1] Install numpy")
   env.communicate("pip install numpy -q")
   print("  -> done\n")
   
   # 2. Create a runnable script with str_replace_editor (writes result to /tmp/demo_out.txt)
   _script = "import numpy as np; print(np.array([1,2,3]).sum())"
   print("[Step 2] str_replace_editor create /tmp/demo.py")
   env.communicate(f"str_replace_editor create --path /tmp/demo.py --file_text {shlex.quote(_script)}")
   print("  -> done\n")
   
   # 3. Run the script (output goes to /tmp/demo_out.txt)
   print("[Step 3] Run script (python3 /tmp/demo.py > /tmp/demo_out.txt)")
   env.communicate("execute_bash 'python3 /tmp/demo.py > /tmp/demo_out.txt'")
   print("  -> done\n")
   
   # 4. Cat the output path
   print("[Step 4] cat /tmp/demo_out.txt")
   out = env.communicate("cat /tmp/demo_out.txt")
   print(f"  -> {out.strip()}\n")
   
   print("=" * 60)
   print("  Demo done (sandbox: script + output file persisted)")
   print("=" * 60)
   
   env.close()
   ```
