---
title: "Natural language-driven: Developing and deploying agents with TRAE"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/developing_and_deploying_agents_with_trae"
---

This topic describes how to install the official AgentKit skill in [TRAE](https://www.trae.cn/?utm_source=trae_homepage&utm_medium=international_site) and use natural language together with [AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/CLI_overview?LibVersion=v26.07.24) to create, test, deploy, invoke, observe, evaluate, update, roll back, and clean up an agent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><a href="https://www.trae.cn/?utm_source=trae_homepage&utm_medium=international_site">TRAE</a> is a ByteDance\-developed AI\-native programming IDE that brings together diverse large models with deep AI integration, delivering intelligent Q&A, code auto\-completion, and agent\-based AI automated programming capabilities. When developing projects with TRAE, you can collaborate flexibly with AI to boost productivity at every stage of development.</div>


* <div data-tips="true" data-tips-type="default">The <a href="https://docs.byteplus.com/en/docs/agentkit/CLI_overview?LibVersion=v26.07.24">AgentKit CLI</a> is a command\-line tool that AgentKit provides for developers. It simplifies the full lifecycle management of agent applications, covering key stages such as initialization, configuration, build, and deployment.</div>



<span id="uYuLDA67"></span>
## Agent lifecycle and CLI commands

The following table describes common agent lifecycle stages, the corresponding CLI commands, and the expected artifacts, so you can confirm the scope of operations before following this walkthrough.


|**Stage** |**Main commands** |**Output** |
|---|---|---|
|Initializing |`agentkit init` |Agent project and basic configuration. |
|Configuration |`agentkit config` |The `agentkit.yaml` file in the root directory of the agent project. |
|Build and deploy |`agentkit deploy` |Image, runtime ID, runtime version, and endpoint. |
|Call |`agentkit invoke` |Agent response and invocation result. |
|Observability |`agentkit runtime show`, `agentkit runtime logs`, `agentkit runtime attach` |Runtime status, logs, and runtime terminal. |
|Evaluation |`agentkit eval` |Evaluation dataset, evaluator, experiment, and score. |
|Update |`agentkit deploy`, `agentkit runtime update` |New runtime version. |
|Release and rollback |`agentkit runtime release` |Active version of the current runtime. |
|Yes |`agentkit destroy`, `agentkit runtime delete` |Deleted runtime and associated resources. |


<span id="NIHQUoAa"></span>
## Prerequisites


|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/6261/64925) and [real-name authentication](https://docs.byteplus.com/en/docs/6261/64935). |
|Activate the service |The AgentKit service has been activated. To enable AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The first time you log in to the AgentKit console, the platform will automatically <strong>select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry)</strong>. You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">To follow this walkthrough end to end, make sure the AgentKit service has management permissions for <strong>runtimes, evaluation datasets, and evaluators</strong>.</div><br> |


<span id="07f6VPep"></span>
## Step 1: Prepare the prerequisite environment

<span id="AAogrwL1"></span>
### 1. Install the AgentKit CLI tool


1. In the terminal of the environment for the agent to be migrated, execute the following command to complete the installation.

   
   <Tabs>
   <Tab zoneid="8LUxjwF8" title="Install using curl (recommended)">
   <TabTitle>Install using curl (recommended)</TabTitle>
   
   Use the system's built\-in curl tool to download and execute the installation script:
   
   ```Bash
   curl https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="Cmeih2hP" title="Install using wget">
   <TabTitle>Install using wget</TabTitle>
   
   Download and execute the installation script using the wget tool:
   
   ```Bash
   wget -qO- https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

2. Execute the following command to check the CLI tool version. The version number should be 0.51.x.

   ```Bash
   agentkit -v # If the version number returned is 0.51.x, the installation was successful.
   agentkit upgrade --check # If a newer version is detected, you can run agentkit upgrade to upgrade to the latest version.
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Your environment may have two AgentKit CLI tools:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>TypeScript AgentKit CLI</strong>: Registers the <code>agentkit</code> command and the <code>ak</code> command. <strong>Version: 0.51.x</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Python AgentKit CLI</strong>: Installed with agentkit\-python\-sdk. Registers the <code>agentkit</code> command. <strong>Version number: 0.8.x</strong>.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, <code>agentkit migrate</code> is only provided by <strong>TypeScript AgentKit CLI</strong>. Since both the TypeScript CLI and Python SDK register the <code>agentkit</code> command, after you install the agentkit‑python‑sdk package or activate a Python virtual environment, agentkit may resolve preferentially to the CLI provided by the Python SDK. As a result, you cannot use the <code>migrate</code> subcommand.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">We recommend that when you encounter an error where the <code>agentkit migrate</code> command cannot be executed, enter <code>agentkit -v</code> to check which version is registered for the current agentkit command. If the output indicates you are currently using the Python AgentKit SDK CLI, we recommend that you use the equivalent command <strong><code>ak</code></strong><strong> (namely </strong><strong><code>ak migrate</code></strong><strong>) provided by the TypeScript CLI.</strong> The <strong><code>ak</code></strong><strong> command is equivalent to the </strong><strong><code>agentkit</code></strong><strong> command in the TypeScript CLI and avoids path‑resolution conflicts with the identically‑named agentkit command registered by the Python SDK.</strong>   </div>
   

      3. Execute the following command to view the CLI tool commands.

   ```Bash
   agentkit --help
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d67efb5e87fa2d1e4d3200eccdbfdf6.png) </span>


<span id="8C2w13tZ"></span>
### 2. Prepare a Python environment

To test the agent locally, follow this step to prepare a Python environment.


1. Execute the following command to confirm that the Python version in the environment of the agent to be migrated is **3.10 or later**.

   ```Bash
   python --version
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cfd053631e425aefef3e85acf5e9c05.png) </span>

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
   


<span id="PhCZ4BCj"></span>
### 3. Prepare large model information

This topic uses the BytePlus ModelArk model Doubao\-Seed\-2.1\-pro as an example. For third\-party platform models, obtain the model API key and model endpoint ID on your own.


1. [Activate the ModelArk service](https://console.byteplus.com/ark/openManagement).

2. Search for Doubao\-Seed\-2.1\-pro, complete the activation, and then click the model name to enter the details page.

3. Click "API access" in the upper\-right corner of the page to create and record an [API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D).

4. Go to the [ModelArk online inference model list page](https://console.byteplus.com/ark/region:cn-beijing/endpoint) to query the model endpoint ID. This topic uses querying a preset inference endpoint as an example: search for Doubao\-Seed\-2.1\-pro and record the model endpoint ID. To create a custom model inference endpoint, see [Model endpoint usage](https://docs.byteplus.com/en/docs/82379/2121998?lang=en&open_in_browser=true&redirect=1#c71acab7).


<span id="e2VUs6x3"></span>
### 4. Prepare BytePlus AK/SK

[Obtain BytePlus AK/SK](https://docs.byteplus.com/en/docs/6291/65568). Navigate to the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page, where you can create and obtain **AK** and **SK**. [Learn more](https://docs.byteplus.com/en/docs/6291/65568)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure the AK/SK you created has management permissions for <strong>veFaaS, APIG, Container Registry, AgentKit runtimes, AgentKit evaluation datasets, and evaluators</strong>, so you can complete the full walkthrough.</div>


<span id="jZtCUQbv"></span>
### 5. Prepare the local environment

1. Execute the following command to configure administrator credentials.

   ```Bash
   export VOLCENGINE_ACCESS_KEY=<AK>
   export VOLCENGINE_SECRET_KEY=<SK>
   ```
   

   2. Execute the following command to verify that the AK/SK is valid and confirm the account associated with the credentials.

   ```Bash
   agentkit auth admin doctor \
    --account <BytePlus accound ID> \
    --region cn-beijing
   ```
   

   <span id="VpPDXkJs"></span>
   ### 6. Install TRAE and open the local project

   2. Go to the [official TRAE Download Center](https://www.trae.cn/download) and download the version that matches your local environment.

   3. Complete registration and log in.

   4. Create and select a new agent project directory in your local environment, or open an existing deployable agent project.

   <span id="aT8EMU7A"></span>
   ## Step 2: Install the official AgentKit skill

This step installs the official AgentKit skill into the current project or the local machine environment, so that TRAE can invoke AgentKit CLI capabilities.


1. In your local terminal, navigate to the agent project directory.

   ```Bash
   cd <Agent project directory>
   ```
   

2. Execute the following command to install the official AgentKit skill into the TRAE configuration of the current project.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>project</code> specifies a project\-level installation, which is suitable for team collaboration and allows the related configuration to be managed together with the project. To use the skill across all projects on the local machine, replace <code>project</code> with <code>global</code>.   </div>
   

   ```Bash
   agentkit onboard --agent trae --scope project
   ```
   

3. The output is as follows. The result shows the TRAE configuration path and the paths of the installed skills, indicating that the installation was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a641b501b26e3e039eaa54927cb4099.png) </span>

4. Open the current project in TRAE. All subsequent natural language instructions are executed within this project.


<span id="Z6m4AZlo"></span>
## Step 3: Create an agent using natural language

This step creates an agent project through TRAE, and confirms the plan, the scope of changes, and the list of commands before any execution takes place.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In all of the following operations, do not include an Access Key, Secret Key, model API Key, Feishu application secret, or any other sensitive information in your natural language instructions. When credentials are required, configure them in the terminal or in a credential management system approved by your organization.</div>



1. Submit the following instructions in TRAE.

   ```Plain Text
   Create a Python AgentKit project in the current directory and build an enterprise IT service agent.
   The agent needs to handle VPN, password reset, and software installation issues, and return fixed policies through a Python tool with type annotations and docstrings.
   Use the current project template for VeADK and AgentKit. Do not write any keys.
   Output the implementation plan, the files to be modified, and the commands to be executed first. Do not create any cloud resources. Wait for my confirmation before proceeding.
   ```
   

2. TRAE first lays out the implementation plan, and waits for the user to confirm.

   Before confirming the implementation plan, we recommend that you pay close attention to the following:

   * The project is created using `agentkit init`, not by manually copying an outdated template.

   * The responsibilities of the code entry point, tool functions, and `agentkit.yaml` are clearly separated.

   * No credentials are written into the code or configuration.

   * The plan includes local verification rather than proceeding directly to deployment.

   * The scope of changes is limited to the current project.

3. Enter "Confirm" or click the prompt shown by TRAE. TRAE then executes the plan and returns the resulting artifacts.

4. Execute the `ls -al` command to view the newly created project directory. Execute the `cd` command to enter the directory of the newly created project.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5a744fc6896518cc897e05a20abd74e.png) </span>

5. Execute the `ls -al` command to verify that the project contains the following files generated by `agentkit init`, which indicates that the agent was created successfully.

   *  **.dockerignore**: Records the file and directory paths to be ignored during the Docker build. During the Docker build, `COPY . .` ignores the files and directories recorded in this file, which reduces the image size and prevents sensitive information from being exposed.

   * **agentkit.yaml**: The configuration file for the AgentKit project. It defines the project metadata, runtime environment variables, cloud deployment parameters, and more.

   * **requirements.txt**: Declares the Python package dependencies required by the agent. During the Docker build, these dependencies are installed into the container image using `RUN uv pip install -r requirements.txt`.

   *  **<project\-name\>.py**: The agent application entry file, i.e., the one specified by `common.entry_point` in `agentkit.yaml`. It defines the agent's behavior, including receiving user requests, conversing with the model, and returning streaming responses.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3d1cae4daae39035a9ede50e176f046.png) </span>


<span id="qn1aKNCW"></span>
## Step 4: Check and test the agent locally

This step verifies that the current agent project can start locally, and performs a basic self\-check before deployment.


1. Submit the following instructions in TRAE.

   ```Plain Text
   Check whether the current agent project can run locally.
   First, check the dependencies, environment variable examples, port 8000 configuration, and agent tool definitions. Then provide the commands to be executed.
   Do not read or output any credentials. Only modify files directly related to the current check when issues are found.
   ```
   

2. Based on the commands recommended by TRAE, execute the following commands in the terminal in sequence.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The recommended commands may differ each time. Use the commands recommended by TRAE in the previous step as the reference. The commands below are for reference only.   </div>
   

      1. Install dependencies.

      ```Bash
      python3 -m pip install -r requirements.txt --break-system-packages
      ```
      

   2. Prepare the local environment variable file.

      ```Bash
      cp .env.example .env
      ```
      

   3. Open `.env` with `vim`, fill in MODEL_AGENT_API_KEY and your BytePlus AK/SK, and then save the file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e378a1c492bfbd255a309b0346e3bcde.png) </span>

   4. Start and verify the local service.

      ```Bash
      source .venv/bin/activate
      python <Agent application entry file>
      ```
      

      The following output is displayed. Do not close this window. Once you execute the next step, this window will return a 200 status code.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d63240ccbcebee66c1491d9fabf10892.png) </span><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e72a3a68666362e30bf528eba956eb0.png) </span>

3. Open a new terminal and execute the following command.

   ```Bash
   curl http://127.0.0.1:8000/ping
   ```
   

   If the request is successful and the response is as follows, the local service has started successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57a11806d82b809e0803409d2365bbed.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">If the current project uses Git, we recommend that you view the actual changes before committing the code.</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">```Bash
git status --short
git diff --check
git diff
```
</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Confirm that the code contains no credentials, unrelated files, or unnecessary refactoring before proceeding to the deployment stage.</div>


<span id="f9uxCWSG"></span>
## Step 5: Deploy the agent

1. Submit the following instructions in TRAE. TRAE summarizes the configuration, resources, and commands to be executed (as shown in the figure below; the content returned may vary with each execution — refer to the actual output).

   ```Plain Text
   Check the AgentKit deployment configuration for the current project and prepare to deploy it to the default project in cn-beijing.
   Before deployment, list the runtime name, region, resource specifications, environment variable references, and the CLI commands to be executed.
   During deployment, use the AK/SK in the .env file for AgentKit authentication.
   Do not display or write any keys. Do not proceed with the deployment until I confirm.
   ```
   

2. Enter "Confirm" or click the instruction prompted by TRAE. TRAE deploys the agent using the following command.

   ```Bash
   agentkit deploy
   ```
   

3. After the deployment is complete, TRAE returns the runtime's name, ID, status, specifications, version, and other information.

4. Execute the following command in the local terminal.

   ```Bash
   agentkit runtime list
   agentkit runtime show <Runtime name or ID> --json
   ```
   

   If the runtime status is "Ready" and the result contains the runtime ID, name, version, and endpoint, the deployment was successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a9b43633a8c4b0130f17734ce30c6b5.png) </span>

5. Log in to the [BytePlus AgentKit console](https://console.byteplus.com/agentkit) to view the deployed agent.


<span id="0c8GFo6h"></span>
## Step 6: Invoke the agent and run smoke tests

This step uses a combination of natural language and CLI commands to verify that the runtime is available and that the key capabilities meet expectations.


<Tabs>
<Tab zoneid="OaswkMEtm8" title="Test with TRAE">
<TabTitle>Test with TRAE</TabTitle>

Submit the following instructions in TRAE.

```Plain Text
Run a smoke test on the current runtime using the AgentKit CLI.
Use the AK/SK in the .env file for AgentKit authentication.
Test three cases separately: a normal question, a question that requires a tool call, and a question that is out of capability scope.
Use a separate session ID for each call, and summarize the commands, results, and failure reasons.
```



</Tab>
<Tab zoneid="hciptlyqAY" title="Test with CLI">
<TabTitle>Test with CLI</TabTitle>

The following is an example CLI command.

```Bash
agentkit invoke -r <Runtime id/name> "Hello, please introduce yourself in one sentence."
```



</Tab>
</Tabs>


The smoke tests should verify the following:


* The runtime can receive requests normally.

* The agent returns results relevant to the question.

* The correct tool is triggered when a tool is required.

* Questions outside the agent's capabilities do not produce fabricated business information.

* Failed results retain a request ID or another retrievable identifier.


<span id="im47NSyk"></span>
## What to do next

<span id="COUNvn1a"></span>
### View agent runtime status and logs

This step is used to read the status and logs when results are abnormal, and to identify the root cause based on the evidence.


<Tabs>
<Tab zoneid="mayNrLhk" title="Use TRAE">
<TabTitle>Use TRAE</TabTitle>

Submit the following instructions in TRAE.

```Plain Text
Check the current agent's running status and read the last 100 lines of logs.
Categorize the exceptions into five groups: authentication, runtime, model, tool, and business logic.
Only provide conclusions supported by log evidence. Do not modify any code.
```



</Tab>
<Tab zoneid="7rFnRgaM" title="Use CLI">
<TabTitle>Use CLI</TabTitle>

The following is an example CLI command.

```Bash
agentkit runtime logs <Runtime name or ID> --limit 100
```


If you need to access a runtime instance for further checks, execute the following command to access the runtime terminal:

```Bash
agentkit runtime attach <Runtime name or ID>
```


The following output is returned. You can perform further checks as needed. Press `Ctrl-]` to exit the runtime terminal.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Do not modify production files directly in the runtime terminal. To fix an issue, return to the project code, test the fix, and redeploy.</div>



</Tab>
</Tabs>


<span id="j8N5nuZR"></span>
### Evaluate the agent

This step designs a minimal release evaluation for the current agent and checks the samples and experiment parameters before submitting the experiment.


<Tabs>
<Tab zoneid="gdurLdzj" title="Use TRAE">
<TabTitle>Use TRAE</TabTitle>

1. Create and run an evaluation

   1. Submit the following instructions in TRAE.

      ```Plain Text
      Design a minimal release evaluation for the current agent.
      First, provide 5 sample cases covering normal requests, tool calls, edge cases, and refusals. Then provide the CLI commands for the evaluation dataset, evaluator, and experiment.
      First, use dry-run to check the experiment parameters. Wait for my confirmation before submitting the experiment.
      ```
      

   2. Follow the TRAE prompt: enter "Confirm" or click the action suggested by TRAE, and then wait for the evaluation task to be created and completed. After the experiment is complete, . Ask TRAE to categorize the failure types based on individual results rather than making code changes directly based on the overall score.

2. Analyze results and tune the agent

   This step identifies issues based on failed evaluation samples and run logs, and then applies the minimum necessary changes.

   1. Submit the following instructions in TRAE.

      ```Plain Text
      Analyze the failed samples and corresponding run logs for the specified evaluation experiment.
      Distinguish between prompt issues, tool definition issues, business data issues, and runtime environment issues.
      Provide the minimal modification plan, the affected files, and the regression tests. Do not modify unrelated code. Wait for my confirmation before proceeding.
      ```
      

   2. Enter "Confirm" or click the action suggested by TRAE. TRAE then performs the following operations in sequence:

      1. Modify the code or configuration.

      2. Run local tests.

      3. View code differences.

      4. Redeploy.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The following commands are used during redeployment.         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">         ```Bash
         agentkit deploy
         agentkit runtime versions <Runtime name or ID>
         ```
                  </div>
         

               5. Create a new experiment using the same evaluation dataset and compare the results of the new and previous experiments. The release step proceeds only after both the regression tests and the release evaluation pass.


</Tab>
<Tab zoneid="mDm62M8g" title="Use CLI">
<TabTitle>Use CLI</TabTitle>

1. Create an evaluation dataset and add samples.

   ```Bash
   agentkit eval dataset create \
     --name <Evaluation dataset name> \
     --schema input,reference_output,output \
     --json
   
   agentkit eval dataset add <Evaluation dataset name> \
     --field input="<Test input>" \
     --field reference_output="<Reference result>" \
     --json
   ```
   

2. View the templates and record the template ID.

   ```Bash
   agentkit eval evaluator templates --json
   ```
   

3. Create an evaluator.

   ```Bash
   agentkit eval evaluator create \
     --name <Evaluator name> \
     --from-template <Template ID> \
     --model <ModelArk model Endpoint ID> \
     --json
   ```
   

   The following output is displayed, including the evaluator name and ID.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d6607816929b8925619f6eb3c2f7e41c.png) </span>

4. Preview and submit an evaluation experiment.

   ```Bash
   agentkit eval run \
     --dataset <Evaluation dataset name> \
     --evaluator <Evaluator name> \
     --target <Runtime name or ID> \
     --name <Experiment name> \
     --dry-run
   
   agentkit eval run \
     --dataset <Evaluation dataset name> \
     --evaluator <Evaluator name> \
     --target <Runtime name or ID> \
     --name <Experiment name> \
     --json
   ```
   

   The following output is displayed, including the experiment name and ID.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1352c6db48593aace2e4a76ac79acc99.png) </span>

5. View the evaluation status and results.

   ```Bash
   agentkit eval experiment get <Experiment ID> --json
   agentkit eval experiment results <Experiment ID> --json
   ```
   

   The following output is returned, indicating that the execution was successful.





</Tab>
</Tabs>


<span id="IP8UYBnD"></span>
### Update agent configuration

<span id="8tLGPViq"></span>
#### Create a new version and release it

For code updates, typically use `agentkit deploy`. If you only need to modify runtime specifications, associated resources, or observability toggles, use `agentkit runtime update`.


1. Go to the local terminal.

2. Execute the following command to update the runtime to 1 vCPU and 2 GiB memory, and automatically release a new version after the update. If `--auto-release` is not used, the update only creates a new version, which must be released separately.

   ```Bash
   agentkit runtime update <Runtime name or ID> \
     --cpu-milli 1000 \
     --memory-mb 2048 \
     --apmplus \
     --auto-release
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If <code>--auto-release</code> is not used, execute the following commands after the new version is created to view and release it.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">   ```Bash
   agentkit runtime versions <Runtime name or ID>
   agentkit runtime release <Runtime name or ID> --rev <version>
   ```
      </div>
   

   3. The following output is returned, indicating that the new version was released successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b1c4ebac22088f5102cdd855b92a023.png) </span>

   4. Execute the following command to confirm that the runtime has switched to the new version.

   ```Bash
   agentkit runtime show <Runtime name or ID> --json
   ```
   

   The following output is returned, confirming that the configuration changes have taken effect.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2fbc3a152218c60d8ea0dc3aca3057f.png) </span>


<span id="dyghjFXh"></span>
#### Roll back versions

This step is used when the current version encounters an error. It compares version information first, and then performs the rollback after the user confirms.


1. Submit the following instructions in TRAE.

   ```Plain Text
   An exception occurred in the current version. First, list the runtime version, and compare the current version with the previous stable version.
   Only output the rollback command and the verification steps after rollback. Do not execute the rollback. Do not proceed with the rollback until I confirm.
   ```
   

2. Enter "Confirm" or click the instruction prompted by TRAE. TRAE executes the following commands in sequence.

3. Execute the following commands in the local terminal to view the current version and make an invocation.

   ```Bash
   agentkit runtime show <Runtime name or ID> --json
   agentkit invoke "Hello, please inturduce yourself" -r <Runtime name or ID>
   ```
   


<span id="HxUb17W5"></span>
### Clean up resources

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting a runtime is an irreversible operation. Do not allow natural language instructions to skip the confirmation automatically.</div>



1. Submit the following instructions in TRAE.

   ```Plain Text
   Prepare to clean up the cloud resources for the current agent.
   First, list the runtime IDs, names, regions, evaluation datasets, and custom evaluators to be deleted. Do not proceed with the deletion.
   Wait for my confirmation on each item before executing the delete command without the --yes parameter.
   ```
   

2. After you enter "Confirm deletion" or click the instruction prompted by TRAE, TRAE executes the following commands.

   ```Bash
   agentkit runtime delete <Runtime name or ID>
   agentkit eval dataset delete <Evaluation dataset name or ID>
   agentkit eval evaluator delete <Evaluator name or ID>
   ```
   

3. After TRAE finishes cleaning up, execute the following commands in the local terminal.

   ```Bash
   agentkit runtime list
   agentkit eval dataset list
   agentkit eval evaluator list
   ```
   

   If the target resources no longer appear in the lists, the CLI\-side cleanup is complete.


<span id="7Yb2x6a9"></span>
## Appendix

<span id="fiaK9qmo"></span>
### Common natural language instructions


|**Task** |**Instruction requirements** |
|---|---|
|Create an agent |Output the plan, files, and commands first. Do not create any cloud resources. |
|Deploy an agent |Check the configuration and credential references first, and then proceed with deployment after confirmation. |
|Troubleshoot issues |Read the status and logs first. Attribute the root cause based on evidence only. |
|Run an evaluation |Show the samples, evaluators, and dry\-run results first. |
|Tune an agent |Start from failed samples. Make only the minimum necessary changes. |
|Update configuration |Indicate whether a new version will be created and releasd. |
|Roll back |Confirm the stable version first, and then run release. |
|Delete resources |List the resources first. Do not use \-\-yes to skip confirmation. |


<span id="TKdRUf4u"></span>
### Basic usage requirements


* For create, update, release, and delete operations, show the actual CLI commands first.

* Inject credentials only through a secure environment. Do not include them in instructions, code, or the repository.

* Review the git diff after each change to catch any unrelated refactoring.

* Smoke tests are required after deployment, and the predefined evaluation must be executed before the release.

* When tuning, compare against the same evaluation dataset to avoid masking regressions by modifying samples.

* Retain interactive confirmation for delete operations, and re\-query the resource list after execution.
