---
title: "Migration guide for existing agents (high-code framework)"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/high_code_framework_migration"
---

<span id="noyY9llP"></span>
## Capability boundaries and precautions

Migration covers entry points, protocols, deployment, and sessions, but does not guarantee the replacement of all platform capabilities. Therefore, these boundaries should be clarified before migration:


* **Legacy API compatibility limits**: After frameworks such as LangChain are migrated, existing legacy HTTP clients cannot be compatible without modifications. Compatibility with existing calls is available only when you enable the `--compat` parameter (`langserve`/`fastapi-mount`).

* **HITL interaction and data persistence limits: ** A LangGraph compiled graph does not automatically generate a complete HITL resume protocol for manual recovery. Complex session persistence and state restoration logic must be configured and implemented by users.

* **A2A capability iteration limit:**  The current A2A communication capability is implemented based on an experimental version of ADK. The protocol can be used normally, but you need to monitor upstream version iterations and compatibility changes continuously.

* **AgentCore platform capabilities:**  Migration does not replace the full Bedrock AgentCore Runtime platform capabilities. Underlying platform capabilities such as IAM permissions, workload identity, memory, gateway, MCP tools, and login state are fully managed by the original project and its existing deployment environment.

* **Migration and evaluation decoupling principle:**  The migrate tool is responsible only for generating the runtime entry point, business configuration, and deployment artifacts. It does not automatically trigger eval evaluation. Low\-code migration artifacts automatically include a generated evaluation set. After migration is complete, users can independently decide whether to run the evaluation and trigger it manually.


<span id="tnGBfzHp"></span>
## Prerequisites


|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). |
|Activate the service |The AgentKit service has been activated. To activate AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.</div><br> |
|Demo experience |The BytePlus platform provides demo examples so that you can quickly try the complete framework migration process. Visit [agentkit-samples](https://github.com/bytedance/agentkit-samples/tree/main) to download the ZIP package locally (as shown in the following figure), and then go to `agentkit-samples/tree/main/python/03-integrations/migration` and select an agent for the framework you want to try.<br><br><br><columns><br><columnsItem zoneid="dmGl17p3xd"><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c13ac569cab91656c8f8a45b642c343.png) </span><br><br></columnsItem><br><columnsItem zoneid="KsYYv7miVj"><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60d37800aedef15608e5e0c35b81f7b6.png) </span><br><br></columnsItem><br></columns><br> |


<span id="6XWCCyNT"></span>
## Complete migration process

<span id="tBzBFdDp"></span>
### Process diagram

The process from preparation to invocation consists of five steps. For high\-code, migration and adaptation are completed locally in a single pass during the "Execute migration" step. For low\-code, this step is split into two remote interaction phases: `create` and `status`.

<span id="G9uUroT7"></span>
### Minimal process example

For example, in LangChain, execute the following single command to complete the migration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For the first migration, add <code>--verify</code> to import the generated artifacts and locally request <code>/run_sse</code>.</div>


* <div data-tips="true" data-tips-type="default">If the project model call is slow, set <code>AGENTKIT_MIGRATE_VERIFY_TIMEOUT_SECONDS=240</code> to extend the timeout.</div>



```Bash
# Go to the local directory of the agent to be migrated.
cd <Local directory for the Agent to be migrated> 

# Migrate the existing agent.
agentkit migrate . \
  --framework langchain \
  --entry agent.py:agent \
  --name my-agent \
  --model-id <model name> \
  --model-base-url <model endpoint> \
  --model-api-key-env <model API Key> \
  --verify

# Deploy the existing agent to BytePlus AgentKit.
agentkit deploy

# Call the agent that has been deployed to BytePlus AgentKit.
agentkit invoke <agent id/name> -m "hi, please introduce yourself"
```


<span id="Po15b98U"></span>
### Command parameter descriptions


|**Parameter​**  |**Requirement level** |**Description** |**Usage examples** |
|---|---|---|---|
|`--framework` |Required |Specifies the original agent development framework to determine the migration adaptation logic. Options: `langchain`, `langgraph`, `adk`, `strands`, `agentcore`, `dify`, `any`. |`--framework langgraph` |
|`--entry` |Required |The project code entry identifier. For the default form, pass in `file.py:object`. For the LangGraph Server form, pass in `langgraph.json[:graph_id]`. |* General: `--entry agent.py:root_agent`<br><br>* LangGraph Server: `--entry langgraph.json:graph1` |
|`-n`, `--name` |Recommended |The name of the AgentKit application. If this parameter is not specified, the project folder name is used by default. |`-n my-agent` |
|`-o`, `--output` |Optional |Migration artifact output directory. For high\-code projects, the default is the project root directory. For Dify/any low\-code projects, the output directory must be outside the source code. |`-o ../agentkit-output` |
|`--input-key` |Optional |Adapts to custom LangGraph session fields. Specify this parameter when the source agent uses non\-standard messages input, such as a LangGraph state that uses `question` instead of` messages`. |\-\-input\-key question |
|`--stream-node` |Specific to LangGraph compiled graph |Specifies streaming output nodes. This parameter can be passed multiple times. It is not required for standard chat graphs. |`--stream-node answer_node` |
|`--compat` |Optional (legacy caller compatibility) |Generates legacy interface\-compatible routes and supports `langserve` and `fastapi-mount` modes. This parameter is disabled by default. |`--compat langserve` |
|`--compat-prefix` |Optional after compat is enabled |Specifies the mount prefix for compatibility routes. If it is not provided, the profile default value is used. |`--compat-prefix /old-api` |
|`--legacy-app` |fastapi\-mount mode only |Specifies the original FastAPI entry and mounts the full legacy service interfaces. |`--compat fastapi-mount --legacy-app api.py:app` |
|`--model-id` |Optional (ARK target\-model replacement) |Enables ARK target\-model replacement. This modifies only the runtime environment configuration and does not modify business source code. |`--model-id ep-xxxxxxxx` |
|`--model-base-url` |Recommended ​when a model\-id is provided |The ARK model service address, compatible with the OpenAI interface format. |`https://ark.cn-beijing.volces.com/api/v3` |
|`--model-api-key-env` |Recommended ​when a model\-id is provided |The environment variable that stores the model's API key. It is read\-only during deployment, and the key is not written to any code file. |`--model-api-key-env ARK_API_KEY` |
|`--server-mode langgraph` |LangGraph Server specific |Dual protocols coexist: the native LangGraph Server threads/runs/stream protocol is retained, and the AgentKit protocol is mounted at the same time. |`--server-mode langgraph` |
|`--allow-blocking` |LangGraph Server specific |Disables blocking code detection. This is not recommended for long\-term use in production environments. Prioritize optimizing synchronous blocking logic. |`--allow-blocking` |
|`--verify` |Recommended |Local self\-check after migration to validate the availability of routes and the streaming interface `/run_sse`. A complete Python dependency environment must be prepared in advance. |`--verify` |
|`--dry-run` |Preview and testing |Outputs only the migration plan without generating any files. This is to validate whether the parameters are correct in advance. |\-\-dry\-run |
|`-f`, `--force` |For repeated migration only |Forcibly overwrites existing AgentKit migration artifacts without deleting the original business source code. |\-f |
|`--json` |For automated pipelines only |Outputs a structured JSON migration report that is compatible with CI scripts for automatic reading and validation |\-\-json |


<span id="GmEqeL4a"></span>
## Step 1: Prepare the prerequisite environment

<span id="spRuFctC"></span>
### 1. Install the AgentKit CLI tool


1. In the terminal of the environment for the agent to be migrated, execute the following command to complete the installation.

   
   <Tabs>
   <Tab zoneid="p0gVw9eI" title="Install using curl (recommended)">
   <TabTitle>Install using curl (recommended)</TabTitle>
   
   Use the system's built\-in curl tool to download and execute the installation script:
   
   ```Bash
   curl https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="Rd1KLgSU" title="Install using wget">
   <TabTitle>Install using wget</TabTitle>
   
   Download and execute the installation script using the wget tool:
   
   ```Bash
   wget -qO- https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

2. Execute the following command to check the CLI tool version. Version number: 0.51.1.

   ```Bash
   agentkit -v
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Your environment may have two AgentKit CLI tools:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>TypeScript AgentKit CLI</strong>: Registers the <code>agentkit</code> command and the <code>ak</code> command. <strong>Version number: 0.51.1</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Python AgentKit CLI</strong>: Installed with agentkit\-python\-sdk. Registers the <code>agentkit</code> command. <strong>Version number: 0.8.x</strong>.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, <code>agentkit migrate</code> is only provided by <strong>TypeScript AgentKit CLI</strong>. Since both the TypeScript CLI and Python SDK register the <code>agentkit</code> command, after you install the agentkit‑python‑sdk package or activate a Python virtual environment, agentkit may resolve preferentially to the CLI provided by the Python SDK. As a result, you cannot use the <code>migrate</code> subcommand.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that when you encounter an error where the <code>agentkit migrate</code> command cannot be executed, enter <code>agentkit -v</code> to check which version is registered for the current agentkit command. If the output indicates you are currently using the Python AgentKit SDK CLI, we recommend that you use the equivalent command <strong><code>ak</code></strong><strong> (namely</strong><strong><code> ak migrate</code></strong><strong>) provided by the TypeScript CLI</strong>. The <strong><code>ak</code></strong> command is equivalent to the <strong><code>agentkit</code></strong> command in the <strong>TypeScript CLI and avoids path‑resolution conflicts with the identically‑named agentkit command registered by the Python SDK.</strong>   </div>
   

<span id="IOnbTpDg"></span>
### 2. Prepare the Python environment (optional)

If you need to test the agent to be migrated locally, refer to this step to prepare the Python environment.


1. Execute the following command to confirm that the Python version in the environment of the agent to be migrated is **3.10 or later**.

   ```Bash
   python --version
   ```
   

2. Use `uv` to manage the Python virtual environment and dependencies. We recommend using the `uv` tool to manage your Python environment and placing AgentKit\-related dependencies in a separate virtual environment to avoid affecting other Python projects running on your machine.

   ```Bash
   # install uv
   curl -LsSf https://astral.sh/uv/install.sh | sh
   
   # Initialize uv environment
   uv init --no-workspace
   
   # Specify Python version for the environment
   uv venv --python 3.12
   
   # Activate the virtual environment
   source .venv/bin/activate
   ```
   


<span id="DjAgZVor"></span>
### 3. Install project dependencies


1. Prepare the project dependencies.

   All business dependencies of the original project must be properly declared in `requirements.txt` and must be able to be installed in a batch without errors. The migration tool automatically appends the AgentKit SDK and the corresponding framework adapter dependencies, while ** preserving the original project dependencies without deletion or overwrite ** to ensure unchanged business capabilities.

   The `requirements.txt` file must provide the following two parts of Python dependencies:

   1. Original Python dependencies of the agent to be migrated: the Python dependencies of the user's existing agent project, used to ensure that the original agent can run.

   2. AgentKit agent adaptation layer dependencies: the Python dependencies of the AgentKit runtime adaptation layer. These must be fixed as follows:

      ```Bash
      a2a-sdk>=0.3.7,<0.4
      agentkit-sdk-python>=0.7.12
      google-adk>=1.32
      ```
      

   Using a simple Strands migration as an example, `requirements.txt` needs the following two parts:

   ```Bash
   # Part 1: native Strands agent dependencies
   strands-agents[openai]
   python-dotenv>=1.0.0
   
   # Part 2: AgentKit migration runtime dependencies
   a2a-sdk>=0.3.7,<0.4
   agentkit-sdk-python>=0.7.12
   google-adk>=1.32
   ```
   

2. Go to the local directory of the agent to be migrated.

   ```Bash
   cd <Local directory for the Agent to be migrated>
   ```
   

3. Execute the following command to install the dependencies.

   
   <Tabs>
   <Tab zoneid="Zv10mLw7" title="Install via uv (recommended)">
   <TabTitle>Install via uv (recommended)</TabTitle>
   
   Go to the directory of the agent to be migrated and execute the following command:
   
   ```Bash
   uv pip install -r requirements.txt
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="FixsRx8y" title="Install via pip">
   <TabTitle>Install via pip</TabTitle>
   
   Go to the directory of the agent to be migrated and execute the following command:
   
   ```Bash
   pip install -r requirements.txt
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="TupAW9cX"></span>
### 4. Prepare large model information

This topic uses the BytePlus ModelArk large model, Doubao\-Seed\-2.1\-pro, as an example. For models on third\-party platforms, obtain the model name, model API key, and model endpoint URL on your own.


1. [Activate the ModelArk service](https://console.byteplus.com/ark/openManagement).

2. Search for Doubao\-Seed\-2.1\-pro, complete the activation, and then click the model name to enter the details page.

3. Check the model usage instructions and note down the endpoint URL and name of the model. As shown in the following figure, these are the model endpoint URL and the model name, respectively.

4. Click "API access" in the upper\-right corner of the page to create and record an [API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D).


<span id="vF06c3iz"></span>
### 5. Prepare BytePlus AK/SK

[Obtain BytePlus AK/SK](https://docs.byteplus.com/en/docs/6291/65568). Navigate to the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page, where you can create and obtain **AK** and **SK**. [Learn more](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).  

<span id="4LNe4DgV"></span>
### 6. Prepare the migration environment


1. Go to the local directory of the agent to be migrated.

   ```Bash
   cd <Local directory for the Agent to be migrated>
   ```
   

2. Execute the `cp` command to copy the environment variable file (for example, `.env`), and execute `vim` to edit the new file.

3. In the new file, enter the model configuration and the BytePlus AK/SK required by AgentKit commands.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You only need to keep the model endpoint URL up to the version segment, for example, <code>https://ark.cn-beijing.volces.com/api/v3‌</code>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The BytePlus AK/SK is required for the subsequent deployment to the AgentKit platform. You can configure it now, or perform this step again later before deploying the existing agent.   </div>
   

   ```Bash
   # Model configuration
   MODEL_AGENT_NAME=<model name>
   MODEL_AGENT_API_BASE=<model endpoint URL> # In this example: https://ark.cn-beijing.volces.com/api/v3
   MODEL_AGENT_API_KEY=<model API Key>
   
   # BytePlus AK/SK
   BYTEPLUS_ACCESS_KEY=<access-key>
   BYTEPLUS_SECRET_KEY=<secret-key>
   CLOUD_PROVIDER=byteplus
   BYTEPLUS_REGION=ap-southeast-1
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01aa2fc14898b839722a90fed82aa521.png) </span>

4. Execute the following command to load the environment variables.

   ```Bash
   export $(grep -v '^#' .env | xargs)
   ```
   


<span id="rZ9lRXM1"></span>
### 7. Local testing (optional)

Execute the following command to test and verify the agent to be migrated in the local environment.

```Bash
python agent.py # Replace agent.py with the file name of your local agent to be migrated.
```


<span id="m8ktWT1U"></span>
## Step 2: Execute migration (high\-code framework)

The migration command varies by framework. For details about each parameter, see [Command parameter description‌s](https://docs.byteplus.com/en/docs/86681/2606799?lang=zh#Po15b98U). The differences across high\-code frameworks are mainly in `--framework` and `--entry`. The remaining parameter structure is the same.

<span id="MBCHMtsP"></span>
### Framework examples

<span id="3p98Oibt"></span>
#### LangChain

Compatible with the full capabilities of Runnable, LCEL orchestration, and agent executor. The existing LangServe interface requires no modification. Add` --compat langserve` at startup for compatibility with legacy clients.

```Bash
agentkit migrate . \
  --framework langchain \
  --entry langchain_agent_migrate/agent.py:agent \
  --name langchain-agent \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="vVAetCwv"></span>
#### LangGraph compiled graph

Suitable for projects that already have a Graph workflow defined. By default, it is directly compatible with the standard chat message structure (messages state). Use `--input-key` for custom state fields, and use `--stream-node` to specify streaming nodes.

```Bash
agentkit migrate . \
  --framework langgraph \
  --entry graph.py:graph \
  --name langgraph-agent \
  --stream-node chatbot \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="xfpoSpbL"></span>
#### LangGraph Server

For official LangGraph online service projects, add `--server-mode langgraph` at startup. After migration, the service supports both the native LangGraph interfaces (`/threads`, `/runs/stream`) and the AgentKit standard dual protocols, without affecting existing business calls.

```Bash
agentkit migrate . \
  --framework langgraph \
  --server-mode langgraph \
  --entry langgraph.json:agent \
  --name langgraph-server-agent \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="YnyPg0Pl"></span>
#### ADK

Native ADK agents can be migrated seamlessly without an intermediate conversion layer. The original tools (ADK tools), callbacks, and sub\-agent scheduling logic are fully preserved. The agents are finally deployed as standard AgentKit online services.

```Bash
agentkit migrate . \
  --framework adk \
  --entry agent.py:root_agent \
  --name adk-agent \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="Z3Plrlvv"></span>
#### Strands

A zero\-argument factory function is recommended as the program entry point. After migration, a Strands agent instance is created for each conversation session independently, preventing state confusion and data interference across multi\-user conversations.

```Bash
agentkit migrate . \
  --framework strands \
  --entry agent.py:build_agent \
  --name strands-agent \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="8ygpbHAN"></span>
#### Bedrock AgentCore

For projects already using the official Bedrock framework (`BedrockAgentCoreApp`). After migration, AgentKit standard interfaces are provided, while the original `/ping` health check and `/invocations` interfaces are preserved. The full Bedrock AgentCore Runtime platform capabilities are not replaced. It is not a complete replacement for the Bedrock AgentCore Runtime platform. External capabilities such as IAM, workload identity, memory, gateway, MCP, and login state are still managed by​ the original project and deployment environment.

```Bash
agentkit migrate . \
  --framework agentcore \
  --entry deploy/agentcore/app.py:app \
  --name agentcore-agent \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY \
  --verify
```


<span id="7wYRSUUS"></span>
### Files generated by migration


|**File** |**Purpose** |
|---|---|
|`agentkit_app.py` |AgentKit unified startup entry file. Automatically loads the original project entry point and generates the hosting application. Regular frameworks use `AgentkitAgentServerApp` by default, while LangGraph Server mode automatically adapts to `AgentkitLangGraphServerApp`.<br><br>At startup, the service first reads dependency packages (site\-packages) from the current runtime virtual environment to avoid platform\-injected paths shadowing local project dependencies. This ensures stable and controllable dependency loading. |
|`.agentkit/agentkit.yaml` |Core deployment configuration file, including the application runtime name, cloud deployment rules, environment variable mapping, and other capabilities.<br><br>APM observability is enabled by default (`apmplus: true`). If the original project has this configuration disabled (`apmplus: false`), the user's original configuration is retained and not forcibly overridden. |
|`.agentkit/Dockerfile` |Cloud image build file. For standard projects, all dependencies are installed via requirements or PyPI. For uv projects, the AgentKit SDK is reinstalled in the virtual environment, and import validation is performed to intercept dependency omissions, version conflicts, and other resolution errors in advance, improving the deployment success rate. |
|`.agentkit/migration-plan.json` |Full migration record file that retains the complete migration plan, risk warnings, local validation results, compatibility route configuration, observability capability status, and framework capability boundary information for issue tracing, version alignment, and acceptance archiving. |
|`requirements.txt` |Based on preserving all original project dependencies, the AgentKit SDK and the corresponding framework adapter dependencies are automatically appended. In production environments, the official release version is pulled from PyPI by default to ensure online version stability. |


<span id="Qf7yNmLO"></span>
## Step 3: Deployment and calling sample

After the migration artifacts are generated, the deployment process automatically reads the environment variable mapping in `.agentkit/agentkit.yaml` and completes the deployment to the cloud. Business calls are uniformly executed through the AgentKit native invoke protocol. All migrated frameworks support the standard streaming interface `/run_sse` by default.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">By default, the deployment process reads the cloud AK/SK credentials from environment variables to complete authentication. Make sure you <a href="https://docs.byteplus.com/en/docs/86681/2606799?lang=zh#4LNe4DgV">have configured the AK/SK and loaded them‌</a> in the environment variable file.</div>


<span id="z8XloQUE"></span>
### Deploy an existing agent


1. Execute the following command to deploy the existing agent to BytePlus AgentKit.


```Bash
agentkit release
```



2. If the following output is displayed and an AgentKit agent runtime ID is returned, the deployment was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc1f8ca86284f209bee19251a3aa1df0.png) </span>

3. Log in to [the BytePlus AgentKit console](https://console.byteplus.com/agentkit) to view the deployed agent.


<span id="4OdbSMkA"></span>
### Test the deployed agent

After the deployment succeeds, you can test the agent locally or online in the [BytePlus AgentKit console](https://console.byteplus.com/agentkit).


<Tabs>
<Tab zoneid="zMvA6puoPs" title="Local debugging">
<TabTitle>Local debugging</TabTitle>

Execute the `invoke` command to perform AgentKit native invocation, which applies to all migrated frameworks.

```Bash
agentkit invoke <agent id/name> -m "hi, please introduce yourself"
```



</Tab>
<Tab zoneid="n4qW6IbuQi" title="Online testing">
<TabTitle>Online testing</TabTitle>

1. Log in the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Basic components \> Agent Runtime".

3. Click the "Online test" button in the "Actions" column to the right of the target agent.

4. Enter natural language input, wait for the agent's response, and verify that the deployed agent behaves as expected.





</Tab>
</Tabs>


<span id="NMgkyNbb"></span>
## Step 4: Observe and evaluate the agent (optional)

After the agent is published and online testing is complete, we recommend continuing to use AgentKit's observability and evaluation capabilities to verify its operating status and actual effectiveness, gradually progressing from "stable and usable" to "ready for launch".

<span id="elpsyzlu"></span>
### Observe the agent

Observability is used to view the agent's runtime performance during actual calls, helping you detect call chain anomalies, model invocation errors, log errors, or performance bottlenecks. Once observability is enabled, AgentKit and the VeADK SDK automatically collect trace (call chain) and metric data for each stage (such as model calls, tool execution, and memory retrieval) based on OpenTelemetry and deliver the data to the observability platform.

You can view the runtime monitoring data, session analysis, trace analysis, model monitoring data, and log analysis of the agent on the "Observability" page. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Observability-)

<span id="GzJCq6Na"></span>
### Evaluate the agent

Evaluation measures the agent's performance across the three dimensions of effectiveness, performance, and cost through standardized experiments. It helps you determine whether the current version meets expectations and provides a basis for subsequent iteration, optimization, and launch.

The evaluation mechanism typically consists of three parts: evaluation sets, evaluators, and experiments. Evaluation sets provide standardized inputs and reference answers. Evaluators score results based on predefined rules using either an LLM or code. Experiments are responsible for combined execution and aggregating result metrics, while also supporting comparative analysis across multiple experiments. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Evaluation)

<span id="s4qObcfT"></span>
## What to do next

After the agent is launched, you can also update its instance specifications, custom image, model, environment variables, and other configurations at any time in the console. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After updating the agent runtime configuration, you need to republish it for the new configuration to take effect. <a href="https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes">Learn more</a></div>
