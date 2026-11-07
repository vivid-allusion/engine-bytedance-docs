---
title: "Migration guide for existing agents (low-code framework)"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Low_code_framework_migration"
---

<span id="noyY9llP"></span>
## Capability boundaries and precautions

Migration covers entry points, protocols, deployment, and sessions, but does not guarantee the replacement of all platform capabilities. Therefore, these boundaries should be clarified before migration:


* **A2A capability iteration limit:**  The current A2A communication capability is implemented based on an experimental version of ADK. The protocol can be used normally, but you need to monitor upstream version iterations and compatibility changes continuously.

* **AgentCore platform capabilities:**  Migration does not replace the full Bedrock AgentCore Runtime platform capabilities. Underlying platform capabilities such as IAM permissions, workload identity, memory, gateway, MCP tools, and login state are fully managed by the original project and its existing deployment environment.

* **Low\-code migration acceptance criteria**: For Dify and any low\-code migration solutions, the acceptance criteria are **full alignment of core business logic, input/output semantics, tool capabilities, and deployment characteristics**. The core of acceptance is equivalent replacement of business capabilities, not merely implementing basic conversational functionality.

* **Migration and evaluation decoupling principle:**  The migrate tool is responsible only for generating the runtime entry point, business configuration, and deployment artifacts. It does not automatically trigger eval evaluation. Low\-code migration artifacts automatically include a generated evaluation set. After migration is complete, users can independently decide whether to run the evaluation and trigger it manually.


<span id="tnGBfzHp"></span>
## Prerequisites


|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). |
|Activate the service |The AgentKit service has been activated. To activate AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.</div><br> |
|Demo experience |The BytePlus platform provides demo examples so that you can quickly try the complete framework migration process. Visit [agentkit-samples](https://github.com/bytedance/agentkit-samples/tree/main) to download the ZIP package locally (as shown in the following figure), and then go to `agentkit-samples/tree/main/python/03-integrations/migration` and select an agent for the framework you want to try.<br><br><br><columns><br><columnsItem zoneid="qUpG9bG3zF"><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25b94e6d8cc42b0e9b1f567bdafd4027.png) </span><br><br></columnsItem><br><columnsItem zoneid="W1x79mB8VN"><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94d83f7f9c3d03f556351f4c2bebc76b.png) </span><br><br></columnsItem><br></columns><br> |


<span id="6XWCCyNT"></span>
## Complete migration process

<span id="tBzBFdDp"></span>
### Process diagram

The process from preparation to invocation consists of five steps. For high\-code, migration and adaptation are completed locally in a single pass during the "Execute migration" step. For low\-code, this step is split into two remote interaction phases: `create` and `status`.

<span id="G9uUroT7"></span>
### Minimal process example

Using Dify as an example, execute the following command to complete the migration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the project model call is slow, set <code>AGENTKIT_MIGRATE_VERIFY_TIMEOUT_SECONDS=240</code> to extend the timeout.</div>


```Bash
# Go to the migration directory.
cd <Local migration directory> 

# create submits dify_input/ to the remote Codex Sandbox to perform the migration. --output ../dify_output is resolved relative to dify_input/. The final artifacts are written to dify/dify_output/.
agentkit migrate dify_input --framework dify create --name dify-migrate --output ../dify_output \
  --codex-model <codex model name> \
  --codex-api-key-env CODEX_MIGRATE_MODEL_API_KEY \
  --model-id <VeADK model name> \
  --model-base-url <VeADK model base_url> \
  --model-api-key-env MODEL_AGENT_API_KEY

# Query the migration task status and download the final dify_output artifacts.
agentkit migrate dify_input --framework dify status --job-id <job_id>
 
# Deploy the built and generated VeADK project to BytePlus AgentKit.
agentkit deploy

# Call the agent that has been deployed to BytePlus AgentKit.
agentkit invoke <agent id/name> -m "hi, please intorduce yourself"
```


<span id="Po15b98U"></span>
### Command parameter descriptions

<span id="tdSd1W53"></span>
#### General parameters


|**Parameter​**  |**Requirement level** |**Description** |**Usage examples** |
|---|---|---|---|
|`--framework` |Required |Specifies the original agent development framework to determine migration adaptation logic. Options: `langchain`, `langgraph`, `adk`, `strands`, `agentcore`, `dify`, `any`. |`--framework langgraph` |
|`--entry` |Required |The project code entry identifier. For the default form, pass in`file.py:object`. For the LangGraph Server form, pass in `langgraph.json[:graph_id]`. |* General: `--entry agent.py:root_agent`<br><br>* LangGraph Server: `--entry langgraph.json:graph1` |
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
#### Low\-code remote task parameters

Low\-code migration runs through remote sandbox tasks. In addition to common parameters, the following actions and parameters are used:


|**Parameter/Action** |**Applicable scenario** |**Detailed description** |
|---|---|---|
|`create` |Initiate a migration process |After uploading the source code to the CodeEnv sandbox environment, migration capabilities are automatically installed, and Codex is called to complete project conversion. |
|`list` |View migration jobs |Displays a list of all remote migration tasks created for the current project |
|`status --job-id` |Query progress and download artifacts |Queries the running status of a specific task and automatically downloads the project artifacts, manifest, migration report, and runtime logs after the task succeeds. Add `--overwrite` to forcibly refresh local cache files |
|`--force-new` |Forcibly create a new migration job |By default, the system reuses a running task with identical parameters. Add this parameter when a full re\-execution of migration is required. |
|`--codex-model` |Specify a large model dedicated to migration |Controls only the model used in the Codex code conversion stage and does not change the inference model associated with the final agent application runtime. |
|`--codex-api-key-env` |Configure migration model key |Enter the name of the environment variable that stores the Codex authentication key, for example, `ARK_API_KEY`. The key is not hard\-coded into any file. |


<span id="nrUXsshx"></span>
## Step 1: Prepare the prerequisite environment

We recommend using the `uv` tool to manage your Python environment and placing AgentKit\-related dependencies in a separate virtual environment to avoid affecting other Python projects running on your machine.

<span id="wHATTqvT"></span>
### 1. Install the AgentKit CLI tool


1. Execute the following command to complete the installation.

   
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
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that when you encounter an error where the <code>agentkit migrate</code> command cannot be executed, enter <code>agentkit -v</code> to check which version is registered for the current agentkit command. If the output indicates you are currently using the Python AgentKit SDK CLI, we recommend that you use the equivalent command <strong><code>ak</code></strong><strong> (namely </strong><strong><code>ak migrate</code></strong><strong>) provided by the TypeScript CLI.</strong> The <strong><code>ak</code></strong><strong> command is equivalent to the </strong><strong><code>agentkit</code></strong><strong> command in the TypeScript CLI and avoids path‑resolution conflicts with the identically‑named agentkit command registered by the Python SDK.</strong>   </div>
   

   <span id="GkCbXvMz"></span>
   ### 2. Prepare the Python environment (optional)

If you need to test the agent to be migrated locally, refer to this step to prepare the Python environment.


1. Execute the following command to confirm that the Python version in the environment of the agent to be migrated is **3.10 or later**.

   ```Bash
   python --version
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cfd053631e425aefef3e85acf5e9c05.png) </span>

2. Use `uv` to manage the Python virtual environment and dependencies.

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
### 3. Prepare large model information

This topic uses the BytePlus ModelArk large model, Doubao\-Seed\-2.1\-pro, as an example. For models on third\-party platforms, obtain the model name, model API key, and model endpoint URL on your own.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During low\-code framework migration, both the "Submit the existing agent to the remote Codex sandbox for reconstruction" and "Build and generate the VeADK project" steps require large model capabilities, and the migration quality and success rate depend on the large model used. We recommend selecting a suitable large model based on your actual situation.</div>



1. [Activate the ModelArk service](https://console.byteplus.com/ark/openManagement).

2. Search for Doubao\-Seed\-2.1\-pro, complete the activation, and then click the model name to enter the details page.

3. Check the model usage instructions and note down the endpoint URL and name of the model. As shown in the following figure, these are the model endpoint URL and the model name, respectively.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06ad47f879198a039384876e7a199aac.png) </span>

4. Click "API access" in the upper\-right corner of the page to create and record an [API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26874d4982211ca036fb107c89cbea73.png) </span>


<span id="vF06c3iz"></span>
### 4. Prepare BytePlus AK/SK

[Obtain BytePlus AK/SK](https://docs.byteplus.com/en/docs/6291/65568). Navigate to the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page, where you can create and obtain **AK** and **SK**. [Learn more](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).  

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During low\-code framework migration, a tool sandbox needs to be created in BytePlus AgentKit. Therefore, make sure your AK/SK has the permission to create a sandbox (that is, CreateSandbox).</div>


<span id="PymRpq1z"></span>
### 5. Prepare the migration environment


1. Create the migration directory.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Before migration, you need to distinguish between two directories:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Migration working directory: The directory in which you execute the migration command in your local terminal, for example, <code>dify/</code> or <code>any/</code>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Migration input directory: A subdirectory under the migration working directory, for example, <code>dify_input/</code> or <code>any_input/</code>. This directory is uploaded in its entirety to the Codex Sandbox as the input for the migration task.   </div>
   

   You need to first create a brand\-new migration input directory, `dify_input/` or `any_input/`, locally, and copy all project files that are necessary and that affect migration decisions and runtime behavior, such as the source code, configuration templates, dependency declarations, and startup instructions required by the project to be migrated, into this directory. Do not copy the local runtime environment, cache, build artifacts, or sensitive configuration. The content to prepare differs by migration type, as follows:

   * `dify_input/`: The Dify application export directory. It must contain `workflow.yml`. You can add `node_config.yml` as needed to describe the runtime configuration of nodes such as models, knowledge bases, memories, and external services. Do not include migration artifacts, cache files, or plaintext keys.

   * `any_input/`: Stores the source code of the Python agent project to be migrated. It should include the program entry point, project source code, dependency declarations, configuration templates, and startup instructions. Do not include `.venv/`, uv cache, `pycache/`, logs, test caches, or build artifacts.

2. Create the environment variable file.

   1. Go to the migration working directory, for example, `dify/` or `any/`.

      ```Bash
      cd <Working directory for migration>
      ```
      

   2. Create a new environment variable file (for example, `.env`), and run `vim` to edit the new file.

   3. In the new file, enter the model configuration and the BytePlus AK/SK required by AgentKit commands.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You only need to keep the model endpoint URL up to the version segment, for example, <code>https://ark.cn-beijing.volces.com/api/v3‌</code>.      </div>
      

      ```Bash
      # Model key used by the remote Codex sandbox
      CODEX_MODEL_AGENT_NAME=<model name>
      CODEX_MIGRATE_MODEL_API_KEY=<model API Key> 
       
      # Model configuration for building and generating the VeADK project
      MODEL_AGENT_NAME=<model name>
      MODEL_AGENT_API_BASE=<model endpoint URL> # In this example: https://ark.cn-beijing.volces.com/api/v3
      MODEL_AGENT_API_KEY=<model API Key> 
      
      # BytePlus AK/SK
      BYTEPLUS_ACCESS_KEY=<access-key>
      BYTEPLUS_SECRET_KEY=<secret-key>
      CLOUD_PROVIDER=byteplus
      BYTEPLUS_REGION=ap-southeast-1
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5721f1279e05599e817434910dfc3f6.png) </span>

   4. Execute the following command to load the environment variables.

      ```Bash
      export $(grep -v '^#' .env | xargs)
      ```
      


<span id="rcF8U6hA"></span>
## Step 2: Execute migration (low\-code framework)

<span id="1SlRdi74"></span>
### Framework examples

The migration command varies by framework. For details about each parameter, see [Command parameter description‌s](https://docs.byteplus.com/en/docs/86681/2611422?lang=zh#Po15b98U). Low\-code frameworks (Dify / any) involve two steps: `create` and` status`. The artifacts are placed outside the source code directory.

<span id="1q9h1BNp"></span>
#### Dify

No significant code changes are required. Upload your Dify workflow or chatflow configuration file, and the tool automatically parses the prompts, model configurations, and tool configurations to generate a complete VeADK project, test cases, and migration documentation in one step.

```Bash
agentkit migrate dify_input --framework dify create \
  --name dify-agent \
  --output ../agentkit-dify-output \
  --codex-model doubao-seed-2-1-pro-260628 \
  --codex-api-key-env ARK_API_KEY \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY
```


<span id="jSO8LDaf"></span>
#### Any

A generic fallback migration solution suitable for any agent project with source code. Codex automatically analyzes the existing project code, rebuilds the entire project according to VeADK best practices, and automatically generates batch evaluation cases to reduce manual rebuilding workload. The acceptance criteria require the ** complete alignment of core business logic, input and output semantics, tool capabilities, and deployment characteristics**. The core acceptance criterion is an equivalent replacement of business capabilities, not merely the implementation of basic chat capability.

```Bash
agentkit migrate any_input --framework any create \
  --name any-agent \
  --output ../agentkit-output \
  --codex-model doubao-seed-2-1-pro-260628 \
  --codex-api-key-env ARK_API_KEY \
  --model-id doubao-seed-2-1-pro-260628 \
  --model-base-url https://ark.cn-beijing.volces.com/api/v3 \
  --model-api-key-env ARK_API_KEY
```


<span id="y6KNSqdJ"></span>
### View migration progress

Low\-code framework migration is an asynchronous migration. You can follow the steps below to check the migration progress. This topic uses migrating dify as an example.


1. After the migration command is executed successfully, record the returned jobID, as shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_258340db386393fa935a6cc85f5e1fd8.png) </span>

2. Execute the following command to check the task status and download the final dify_output artifacts.

   ```Bash
   agentkit migrate dify_input --framework dify status --job-id <job_id>  # This topic uses migrating dify as an example. If you are migrating any, replace dify_input in the command with any_input.
   ```
   

   When the status field changes from "Running" to "Succeeded", the migration is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5377ccc4a910156bc06f9aff09891b98.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The migration success rate depends on the quality of the large model you select. If the migration fails, you can check the conver_report.md file to identify the cause of the failure, or retry directly by following these steps:   </div>
   

   1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">First, execute the <code>rm -rf dify_output</code> command to delete the output folder.   </div>
   

   2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">See <a href="https://docs.byteplus.com/en/docs/86681/2611422?lang=zh#PymRpq1z">Prepare the migration environment</a>. Update the large model in the .env environment variable file.   </div>
   

   3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/86681/2611422?lang=zh#rcF8U6hA">Execute the migration‌</a> again.   </div>
   

4. Execute the following command to view the local history of migration tasks.

   ```Bash
   agentkit migrate dify_input --framework dify list # This topic uses migrating dify as an example. If you are migrating any, replace dify_input in the command with any_input.
   ```
   


<span id="0y4Vc7du"></span>
### Files generated by migration

After the migration is complete, a new `dify_output/` or `any_output/` folder is generated, containing the VeADK project that can be deployed to the AgentKit runtime.


|**File** |**Purpose** |
|---|---|
|`.agentkit/agentkit.yaml` |Core deployment configuration file, including the application runtime name, cloud deployment rules, environment variable mapping, and other capabilities.<br><br>APM observability is enabled by default (`apmplus: true`). If the original project has this configuration disabled (`apmplus: false`), the user's original configuration is retained and not forcibly overridden. |
|`convert_report.md` |The migration report that consolidates complete migration implementation records, functional compatibility verification results, observability runtime status, and a summary of framework capability boundaries, for use in issue traceback, version alignment, and formal acceptance archiving. |
|`migration-plan.md` |The migration plan that retains the overall migration implementation plan, potential risk alerts, prerequisite validation requirements, and deployment routing adaptation rules, for use in migration execution and proactive risk control. |
|`eval/` |The evaluation test cases that include baseline conversation test samples and edge\-case/exception test cases. They are used to benchmark the performance of the old and new versions and for regression acceptance across iterations. |
|`requirements.txt` |Based on preserving all original project dependencies, the AgentKit SDK and the corresponding framework adapter dependencies are automatically appended. In production environments, the official release version is pulled from PyPI by default to ensure online version stability. |


<span id="O7BLz1T2"></span>
## Step 3: Deployment and calling sample

<span id="pjoYPtdw"></span>
### Deploy an existing agent


1. Execute the following command to copy the `.env` environment variable file to the `dify_output/` or `any_output/` folder.

   ```Bash
   cp .env dify_output/.env # This topic uses migrating dify as an example. If you are migrating any, replace dify_input in the command with any_input.
   ```
   

2. Execute the following command to go to the `dify_output/` or `any_output/` folder.

   ```Bash
   cd dify_output/ # This topic uses migrating dify as an example. If you are migrating any, replace dify_input in the command with any_input.
   ```
   

3. Execute the following command to deploy the built VeADK project to BytePlus AgentKit.

   ```Bash
   agentkit release
   ```
   

4. If the following output is displayed and an AgentKit agent runtime name and ID are returned, the deployment was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_520e87c8c55982acfe77cb79a2d25752.png) </span>

5. Log in to the [BytePlus AgentKit console](https://console.byteplus.com/agentkit) to view the deployed agent.


<span id="4OdbSMkA"></span>
### Test the deployed agent

After the deployment succeeds, you can test the agent locally or online in the [BytePlus AgentKit console](https://console.byteplus.com/agentkit).


<Tabs>
<Tab zoneid="zMvA6puoPs" title="Local testing">
<TabTitle>Local testing</TabTitle>

Execute the `invoke` command to perform AgentKit native invocation, which applies to all migrated frameworks.

```Bash
agentkit invoke <agent id/name> -m "hi, please intorduce yourself"
```



</Tab>
<Tab zoneid="n4qW6IbuQi" title="Online testing">
<TabTitle>Online testing</TabTitle>

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Basic components \> Agent Runtime".

3. Click the "Online test" button in the "Actions" column to the right of the target agent.

4. Enter natural language input, wait for the agent's response, and verify that the deployed agent behaves as expected.


</Tab>
</Tabs>


<span id="NMgkyNbb"></span>
## Step 4 (Optional): Observe and evaluate the agent

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
