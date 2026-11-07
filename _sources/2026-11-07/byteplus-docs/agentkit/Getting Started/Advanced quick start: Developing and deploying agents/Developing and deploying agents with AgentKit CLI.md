---
title: "Developing and deploying agents with AgentKit CLI"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool"
---

This topic describes how to use the AgentKit CLI to quickly create and validate an agent based on the CLI's preset templates, deploy it as an AgentKit cloud agent runtime, and complete the end\-to\-end process of observing and evaluating the agent runtime image.

## Background

The AgentKit CLI‌ is a command\-line tool for developers that simplifies full lifecycle management of agent applications, covering key stages such as initialization, configuration, building, and deployment. Through a unified command entry point and standardized workflow, it addresses common engineering issues in agent delivery. The issues include inconsistent project startup methods, scattered configurations that are difficult to reuse, high costs of switching environments, and tedious and error\-prone build and deployment steps. This allows developers to focus more of their effort on the agents' capabilities and effectiveness.

The core advantages of the AgentKit CLI include:

* Adopts a declarative configuration approach, centralizing core configuration in the `agentkit.yaml` file for clearer, more portable configuration that is easier to manage under version control.

* Supports multiple modes, including local development, hybrid deployment, and cloud\-only deployment, to meet development and delivery needs at different stages.

* Comes with preset agent templates (such as Basic Agent App and Basic Stream Agent App) to help developers quickly generate runnable projects.

* Provides advanced commands such as `agentkit config` and `agentkit launch` to lower the barrier to configuring and publishing agents, improving delivery stability.

## Prerequisites

|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). |
|Activate the service |The AgentKit service has been activated. To activate AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br>> **tip**<br><br><br>> The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.<br> |
||[You have activated Container Registry](https://console.byteplus.com/cr). |
||[ModelArk has been activated](https://console.byteplus.com/ark/openManagement). |

## Step 1: Configure the environment

1. Log in to the machine where you want to install the AgentKit CLI.

2. Execute the following command to confirm that the Python version is **3.12 or later**.

   ```Bash
   python3 --version
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_696334625a66d09fbc2d6654736fd434.png)

3. Execute the following command to download and install the AgentKit CLI.

   > **warning**

   > This topic uses AgentKit CLI `0.54.0` as an example. **Parameters may vary between versions, so use the parameters that correspond to your actual version**.

   **Use the curl tool**

```Bash
   curl -fsSL https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```

   **Use the wget tool**

```Bash
   wget -qO- https://agentkit-cli.tos-cn-beijing.volces.com/install.sh | sh
   ```

4. Execute the following command to check whether the installation is successful.

   ```Bash
   agentkit --version
   ```

   If output similar to the following is displayed, the installation is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0958b17bd98858cb39f26d538e58e366.png)

5. Configure access credentials.

   **Log in with your BytePlus account**

Log in to the BytePlus console through your browser to complete one\-click authorization. The AgentKit CLI automatically obtains a short\-lived credential for subsequent calls. You do not need to save access keys locally. This effectively reduces the risk of credential leakage. This method is suitable for local development, temporary operations, and multi\-user environments.

   1. Execute the following command to open your local browser for authorization.

      ```Bash
      agentkit login --console --provider byteplus
      ```

   2. On the BytePlus login page opened by AgentKit, log in with the target account.

   3. After a successful login, the browser redirects to a login success page, and the terminal simultaneously displays a login success message.

      * Browser

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e320e688bab84eb3a7a45e8e41f4ed8.png)

      * Terminal

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1e29c365e4e36e08b131ea9d01413b11.png)

   **Authorize with AK/SK environment variables**

Configure your BytePlus API access credentials (Access Key ID and Secret Access Key, referred to as AK/SK) as environment variables. The AgentKit CLI reads the credentials from the environment variables and calls cloud resources directly, without requiring browser interaction. This method is suitable for scenarios that require non\-interactive authentication, such as CI/CD pipelines, automation scripts, and long\-running unattended services.

   1. Create and obtain an API access key pair (Access Key ID and Secret Access Key) for calling BytePlus cloud resources. [Learn more](https://docs.byteplus.com/en/docs/IAM/creating-an-access-key?redirect=1)

   2. Execute the following command in your local terminal to set environment variables.

      > **warning**

      > Since AK/SK are highly sensitive credentials, directly writing them into static configuration files, such as `.env`, poses a security risk. When you configure BytePlus AK/SK in the local development environment, we recommend managing them by exporting session\-level environment variables in the terminal.

      ```Bash
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```

   3. Execute the following command to configure the default cloud provider and region.

      ```Bash
      agentkit config --global --init
      agentkit config --global \
          --cloud_provider byteplus \
          --region ap-southeast-1
      ```

## Step 2: Create an agent

1. Initialize the agent.

   1. Execute the following command to view the AgentKit CLI preset templates.

      ```Bash
      agentkit init --list-templates
      ```

   2. Execute the following command to start the agent initialization process.

      > **tip**

      > This practice uses the AgentKit CLI built\-in `a2a` template to initialize the agent and names both the agent and the project root directory `it-support-agent`.

      ```Bash
      agentkit init it-support-agent \
        --template a2a \
        --directory it-support-agent
      ```

      **Parameter description**

      |Parameter​ |Description |
      |---|---|
      |[project_name] |The agent project name. In this practice, `it-support-agent` is used as an example. |
      |\-\-template |Specify the CLI preset template ID, key, or name used to initialize the agent. This practice uses the `a2a` template as an example. |
      |\-\-directory |Specify the directory path for storing the agent project. If the directory does not exist, AgentKit CLI automatically creates it. This practice uses the `it-support-agent` directory as an example. |

2. After initialization is complete, you can view the project file information in the project root directory.

   1. Execute the following command to enter the project root directory.

      > **tip**

      > Replace `it-support-agent` with the actual root directory path of the agent project.

      ```Bash
      cd it-support-agent
      ```

   2. Execute the following command to view the project files.

      ```Bash
      find . -maxdepth 3 -type f | sort
      ```

      The AgentKit CLI generates the following files:

      *  **.dockerignore**: Records the file and directory paths to be ignored during the Docker build. During the Docker build, `COPY . .` ignores the files and directories recorded in this file, which reduces the image size and prevents sensitive information from being exposed.

      * **agentkit.yaml**: The configuration file for the AgentKit project. It defines the project metadata, runtime environment variables, cloud deployment parameters, and more.

      * **requirements.txt**: Declares the Python package dependencies required by the agent. During the Docker build, these dependencies are installed into the container image using `RUN uv pip install -r requirements.txt`.

      * **it\-support\-agent.py**: Agent application entry file, which defines the agent's behavior, including receiving user requests, interacting with models, returning streaming responses, and more.

      > **warning**

      > When an existing local agent is used, the AgentKit CLI adds the `agentkit-` prefix to the name of your original agent application entry file. For example, if the original entry file for a local agent is named `local_agent.py`, it will be renamed to `agentkit-local_agent.py` after initialization.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fe06fba98766e641dae0cf9cebd3f6e.png)

3. Modify the agent application entry file as needed to adjust the agent's behavior.

   1. In the project root directory, execute the following command to open the agent code file.

      ```Bash
      vim it-support-agent.py
      ```

   2. Press the `i` key to enter edit mode, and replace the default agent information in the template with the following content.

      > **tip**

      > To verify that the agent is invoked correctly, the agent in this guide is configured with fixed data. Before the agent is officially published, you can replace the agent implementation with an enterprise knowledge base, a ticketing system, or an internal API.

      ```Python
      import logging
      
      from veadk import Agent, Runner
      from veadk.a2a.agent_card import get_agent_card
      from veadk.prompts.agent_default_prompt import DEFAULT_DESCRIPTION, DEFAULT_INSTRUCTION
      from google.adk.a2a.executor.a2a_agent_executor import A2aAgentExecutor
      from agentkit.apps import AgentkitA2aApp
      
      logger = logging.getLogger(__name__)
      
      a2a_app = AgentkitA2aApp()
      
      
      def query_it_policy(topic: str) -> dict[str, str]:
          """Query the internal IT service policy for a topic."""
          policies = {
              "vpn": "Open the company VPN client, sign in with SSO, and complete MFA verification.",
              "password": "Open the account portal and select Reset password. Complete identity verification before setting a new password.",
              "software": "Submit a software installation request in the IT service portal and wait for approval.",
          }
          normalized_topic = topic.lower().strip()
      
          if "vpn" in normalized_topic:
              key = "vpn"
          elif any(keyword in normalized_topic for keyword in ("password", "passwd", "reset", "account", "credential")):
              key = "password"
          elif any(keyword in normalized_topic for keyword in ("software", "install", "installation", "app", "application", "program")):
              key = "software"
          else:
              return {
                  "result": "No matching policy was found. Contact the IT service desk for assistance."
              }
      
          return {"result": policies[key]}
      
      
      agent_name = "it_support_agent"
      description = "An enterprise IT service assistant."
      system_prompt = (
          "You are an enterprise IT service assistant. "
          "Use query_it_policy when the user asks about VPN, passwords, or software installation. "
          "Do not invent policies that are not returned by the tool."
      )
      
      
      tools = [query_it_policy]
      
      
      agent = Agent(
          name=agent_name,
          description=description,
          instruction=system_prompt,
          tools=tools,
      )
      runner = Runner(agent=agent)
      
      @a2a_app.agent_executor(runner=runner)
      class MyAgentExecutor(A2aAgentExecutor):
          pass
      
      @a2a_app.ping
      def ping() -> str:
          return "pong!"
      
      if __name__ == "__main__":
          from a2a.types import AgentCard, AgentProvider, AgentSkill, AgentCapabilities
      
          agent_card = AgentCard(
              capabilities=AgentCapabilities(streaming=True),
              description=agent.description,
              name=agent.name,
              default_input_modes=["text"],
              default_output_modes=["text"],
              provider=AgentProvider(organization="veadk", url=""),
              skills=[AgentSkill(id="0", name="chat", description="Chat", tags=["chat"])],
              url="http://0.0.0.0:8000",
              version="1.0.0",
          )
      
          a2a_app.run(
              agent_card=agent_card,
              host="0.0.0.0",
              port=8000,
          )
      ```

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and press Enter to save and exit the file.

## Step 3: Verify the agent locally

1. Execute the following command to enter the project root directory and modify the agent dependency file configuration.

   > **tip**

   > Replace `it-support-agent` with the actual path to the root directory of the agent project.

   ```Bash
   cd it-support-agent
   printf '%s\n' 'veadk-python[extensions]' > requirements.txt
   ```

2. Execute the following command to create and activate a virtual environment. This document uses the example of creating and activating a virtual environment named `.venv` based on `Python 3.12`.

   ```Bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

   Once the environment is activated, you will see the virtual environment name in parentheses at the beginning of your command line.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56bf157546342aa9e4ccce521a51aded.png)

3. Execute the following command to install the agent dependencies in the activated virtual environment.

   ```Bash
   python -m pip install -r requirements.txt
   ```

4.  **(Optional)**  If your agent uses components such as [sandbox template](https://docs.byteplus.com/en/docs/agentkit/Tool_overview), [knowledge base](https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview), [memory](https://docs.byteplus.com/en/docs/agentkit/Memory_overview), and [MCP](https://docs.byteplus.com/en/docs/agentkit/MCP_services), configure the corresponding environment variables in the `.env` file. **This practice does not use the related components.**

   > **tip**

   > Before committing the agent code to Git, add the `.env` file path to the `.gitignore` file to avoid committing the local environment variable file to the repository.

   1. Execute the following command to create and open the environment variable file.

      ```Bash
      vim .env
      ```

   2. Press the `i` key to enter edit mode and fill in the environment variables required by the agent, such as the sandbox template ID and region.

      ```Plain Text
      AGENTKIT_TOOL_ID=t-xxx
      AGENTKIT_TOOL_REGION=xxx
      ```

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and press Enter to save and exit the file.

5. Execute the following command to verify whether the tools in the agent can be loaded properly.

   ```Bash
   python -c 'from runpy import run_path; print(run_path("it-support-agent.py")["query_it_policy"]("vpn"))'
   ```

   If the output is as shown below, the tools can be loaded properly.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_780b3caede7de98a4e93352cb30baebd.png)

6. Verify whether the local service can run properly.

   1. Execute the following command to start the agent service locally.

      ```Bash
      python it-support-agent.py
      ```

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11773f66db317f43e29bd7a0be066b53.png)

   2. **Open a new local terminal window** and execute the following command to verify whether the local service has started successfully.

      ```Bash
      curl http://127.0.0.1:8000/ping
      ```

      If the output contains `pong`, the local service is running properly.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b2747e77f92bd85a9054a7f2530e7ec.png)

   3. After completing the verification, return to the terminal where the local agent service was started and press `Ctrl` + `C` to stop the local service.

## Step 4: Configure deployment parameters

1.  **(Optional)**  The AgentKit CLI preset template is preconfigured with ModelArk's large language model for inference. If you need to use a different model, obtain information about the target model first.

   This topic uses the BytePlus ModelArk large model, Doubao\-Seed\-2.1\-pro, as an example. For models on third\-party platforms, obtain the model name, model API key, and model endpoint URL on your own.

   1. Log in to the [ModelArk console](https://console.byteplus.com/ark/openManagement).

   2. Search for `Doubao-Seed-2.1-pro`, complete the activation, and then click the model name to enter the details page.

   3. Check the model usage instructions and note down the endpoint URL and name of the model.

      > **tip**

      > You only need to keep the model endpoint URL up to the version segment.

   4. Click the "API access" button in the upper\-right corner of the page to create an [API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D) and save it.

2. Execute the following command in the project root directory to set deployment parameters using the interactive configuration wizard.

   ```Bash
    agentkit config
   ```

   The configuration wizard will guide you through the following settings. You can press `Enter` to use the default setting:

   |Parameter​ |Description |
   |---|---|
   |**Basic Configuration**<br><br>Configure basic information such as the agent name, code entry point, development language, and deployment mode. The configuration in this module applies to all deployment modes. ||
   | Agent application name |The agent name.<br><br>> **tip**<br><br><br>> This name is also used as the Docker image name generated during cloud deployment, the prefix for the agent runtime name, and the default CR repository name.<br> |
   |Agent application entry file |The entry file for the agent application. |
   |Agent application Language |The development language used. The default is `Python`. Supported:<br><br><br>* 1: Python<br><br>* 2: Golang |
   |Application description |The agent description. After deployment, this serves as the description of the corresponding agent runtime, helping team members understand the purpose of the project. |
   |Agent application Language |The development language of the agent application. The default language is `Python`. Supported:<br><br><br>* 1: Python<br><br>* 2: Golang |
   |Agent application Language version |The version of the agent application development language.<br><br><br>* The default Python version is `3.12`.<br><br>* The default Golang version is `1.24`. |
   |Agent application Dependencies file |The file that records agent application dependencies. Default value: `requirements.txt`. |
   |Application\-level runtime environment variables |Configure general environment variables readable by the agent runtime. Configure in `Key=Value` format. Multiple environment variables can be configured by specifying this parameter multiple times. Supported:<br><br><br>* `MODEL_AGENT_NAME=`Model name: The model name configured to provide inference services for the agent. The default is ModelArk's `doubao-seed-2-1-pro-260628` model.<br><br>* `MODEL_ENDPOINT=`Model endpoint URL: Configure the URL for calling the model service. The default is the ModelArk endpoint `https://ark.cn-beijing.volces.com/api/v3`.<br><br>* `MODEL_AGENT_API_KEY=`Model API Key: Configure the API Key for calling the model service. By default, the API access credentials (Access Key ID and Secret Access Key) of your configured BytePlus cloud resources are used to obtain ModelArk model invocation permissions.<br><br>* `DEBUG=`Testing mode switch: whether to enable testing mode. Supported:<br><br>   * `true`: Enabled. When testing mode is enabled, the agent outputs more detailed testing information for easier development and troubleshooting.<br><br>   * `false`: Disabled.<br><br>* `LOG_LEVEL=`Log level: Controls the verbosity of logs output by the agent runtime. Supported:<br><br>   * `debug`: Outputs all testing information, including model call details, tool execution processes, and intermediate states. Suitable for development, testing, and troubleshooting.<br><br>   * `info`: Default value. Outputs normal runtime logs, such as request start/end and key state changes. Suitable for daily use and general monitoring.<br><br>   * `warning`: Outputs only warning and error information. Suitable for scenarios that focus on potential risks.<br><br>   * `error`: Outputs only error logs. Suitable for scenarios that focus only on failures. |
   |Deployment and runtime mode |The deployment and runtime mode of the agent application. Supported:<br><br><br>* `local`: Default value. Builds and deploys the agent on your local machine. Suitable for scenarios that require rapid development and testing.<br><br>* `cloud`: Fully hosts the code build and deployment on AgentKit, without requiring a local Docker environment. Provides built\-in observability and high environment consistency, and is secure and reliable. Suitable for publishing agents to production environments. **This practice uses this deployment mode.** <br><br>* `hybrid`: Builds the image locally, then pushes it to AgentKit in the cloud for deployment. Combines the flexibility of local builds with the stability of the cloud runtime environment. Suitable for scenarios that require a custom build process. |
   |**Cloud Build and Deployment Configuration**<br><br>Configure the cloud resource information required for cloud deployment. The configuration in this module applies only to the `cloud` deployment mode. ||
   |Cloud service region |Specify the region ID for deploying local agent code. All cloud resources used during deployment will be created in this region. Supported:<br><br><br>* `ap-southeast-1`: Asia Pacific (Johor) |
   |Container Registry instance name |Specify the CR configuration for storing cloud\-built images, including the instance name, namespace, and repository name. By default, the AgentKit CLI automatically generates these values.<br><br>> **tip**<br><br><br>> CR stores container images generated during the cloud deployment of agents, providing you with a secure and highly available container image hosting service. [Learn more](https://docs.byteplus.com/en/docs/cr/what-is-cr)<br> |
   | Container Registry namespace ||
   | Container Registry repository name ||
   |BytePlus project for the Runtime |The project to which the deployed agent runtime belongs. The default value is `default`.<br><br>> **tip**<br><br><br>> A project is a collection of resources. You can add the new agent runtime to a project and manage it centrally at the project level, which helps keep resources independent and maintain data security. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Managing_projects)<br> |
   |Runtime authentication type |Configure the authentication method for accessing managed resources of the agent runtime. Supported:<br><br><br>* `key_auth`: Automatically create and associate an API Key with the agent runtime. After the agent runtime is successfully created, you can view it on the agent runtime details page. **This practice uses this authentication method.** <br><br>* `custom_jwt`: Use OAuth authorization mode to apply for access tokens and call APIs, enhancing security and simplifying configuration. |

   After the configuration is complete, the above content will be written to the `agentkit.yaml` configuration file. You can also execute the `cat agentkit.yaml` command to open the configuration file and view the agent metadata information.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14dec8d48b91f9c0684ce553cbed5243.png)

## Step 5: Deploy the agent

1. Execute the following command in the project root directory to build and deploy the application to the AgentKit agent runtime.

   ```Bash
   agentkit launch
   ```

   > **tip**

   > The initial deployment may take a while. Please wait for it to complete.

   When the agent runtime status shown in the output is **Ready**, the creation is successful. Here, you can obtain the agent runtime name and ID, as well as information about the cloud resources used for this deployment.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_959e899f439cfed6399c1b741dd848a1.png)

2. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). You can view the deployed agent runtime instances and their detailed information.

## Step 6: Test the agent online

After the agent is created, you can verify whether the agent works as expected by clicking "Online test" in the console or by executing the `invoke` command.

**Online testing**

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Basic Components \> Agent Runtime".

3. Click the "Online test" button in the "Actions" column to the right of the target agent.

4. Send test text in the chat box (for example: How to configure VPN), and verify that the returned content meets expectations.

**Testing via CLI commands**

1. Execute the following command to send a prompt.

   ```Bash
   agentkit invoke run \
       --runtime-id r-yettxxxx \
       "How do I connect to VPN"
   ```

   **Parameter description**

   |Parameter​ |Description |
   |---|---|
   |\-\-runtime\-id |The ID of the agent runtime to be verified. |
   |[message] |The user message to be sent. |

2. Confirm whether the agent can respond normally based on the output.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63f27f3a0f98b25e36190e18193b48e0.png)

## Related operation

### Used to view the running status of the agent runtime

1. Execute the following command to enter the root directory of the target agent.

   > **tip**

   > Replace `it-support-agent` with the actual path to the root directory of the agent project.

   ```Bash
   cd it-support-agent
   ```

2. Execute the following command to view the current agent's agent runtime ID, name, status, `Endpoint`, and other information.

   ```Bash
   agentkit status
   ```

   The following output indicates that the agent runtime is running normally.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_954e3c5d65210229e5838facbdae134b.png)

### Observe agent data

Observability is used to view the agent's runtime performance during actual calls, helping you detect call chain anomalies, model invocation errors, log errors, or performance bottlenecks.

1. Enable the observability service.

   1. Click the target agent runtime name and select the "Configuration information" tab.

   2. Click the edit icon for "Observability service".

   3. Select "Enable" and click the "Confirm" button to enable the observability service.

   4. Publish the agent runtime to apply the configuration.

      1. Click the "Publish" button.

      2. After confirming the change information, click the "Confirm" button.

2. Execute the following command to view the latest runtime logs.

   > **tip**

   > Replace `it-support-agent` with the actual agent runtime name.

   ```Bash
   agentkit runtime logs it-support-agent --limit 100
   ```

   The log information includes details such as request start, model invocation, tool execution, and request end. If any conversations contain failed invocations, we recommend checking the earliest error and its request ID first.

3. View model invocation and tool execution records through the observability service.

   1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

   2. In the left navigation tree, select "Observability \> Application observability".

   3. Search by agent runtime name, and click the "Monitoring details" button in the "Actions" column on the right.

   4. You can use the session ID, trace ID, and other information obtained from the logs to search the trace, view the model invocation and tool execution records for the corresponding request, and confirm that the overall trace meets expectations. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Observability-)

### Evaluate agent performance

Evaluation measures the agent's performance across the three dimensions of effectiveness, performance, and cost through standardized experiments. It helps you determine whether the current version meets expectations and provides a basis for subsequent iteration, optimization, and launch.

The evaluation mechanism typically consists of three parts: evaluation sets, evaluators, and experiments. Evaluation sets provide standardized inputs and reference answers. Evaluators score results based on predefined rules using either an LLM or code. Experiments are responsible for combined execution and aggregating result metrics, while also supporting comparative analysis across multiple experiments. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Evaluation)

### Update and roll back an agent

**Update an agent**

After you modify the prompts, tools, or business logic in the agent entry file locally (for example, `it-support-agent.py` in this guide) and complete local validation, you can sync the changes to the corresponding AgentKit agent runtime.

1. Execute the following command to enter the root directory of the agent project.

   > **tip**

   > Replace `it-support-agent` with the actual path to the root directory of the agent project.

   ```Bash
   cd it-support-agent
   ```

3. Execute the following command to deploy the new version.

   ```Bash
   agentkit launch
   ```

4. Subsequently, you can use features such as [online testing](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool#jzE7QkPB) and [observability](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool#luCojWOw) to verify whether the results returned by the new version meet expectations.

**Roll back an agent**

If the agent version you update to on AgentKit becomes unusable, has unsatisfactory performance, or produces responses that do not meet expectations, you can roll back the agent runtime version to a stable version.

1. Execute the following command to view the version list of the target agent runtime.

   > **tip**

   > Replace `it-support-agent` with the actual agent runtime name.

   ```Bash
   agentkit runtime versions it-support-agent
   ```

   When the output is as shown below, it indicates that the agent runtime has three versions: `0`, `1`, and `2`. Versions `1` and `2` are in the `Ready` state.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_552788cea6cede2f6e128292051e8666.png)

2. Execute the following command to roll back to the specified version.

   > **tip**

   > Replace `2` with the actual version.

   ```Bash
   agentkit runtime release it-support-agent --rev 2
   ```

   When the output is as shown below, it indicates that the rollback to the target version was successful. The agent runtime uses this version as the current version.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7fe01d41bf5a9d311d45742ab4a7ae6.png)

3. After publishing is complete, you can use [online testing](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool#jzE7QkPB) and [observability](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool#luCojWOw) features to verify whether the returned results after rollback meet expectations.

### Clean up resources

Once you have completed verification or no longer need the AgentKit agent runtime and related resources you created, you can delete the relevant resources.

1. Delete the agent runtime.

   1. Execute the following command to delete the agent runtime.

      > **warning**

      * > A deleted agent runtime instance and related resources cannot be recovered. Proceed with caution.

      * > The delete command only deletes the agent runtime you deployed to AgentKit. **It does not affect your local agent project files**.

      * > Replace `it-support-agent` with the actual agent runtime name.

      ```Bash
      agentkit runtime delete it-support-agent
      ```

   2. Confirm the agent runtime name and its region. Then use the arrow keys to select `yes` and press Enter to confirm.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e89be55e847dbfeba5e3a3a8bba725f7.png)

   3. Execute the following command to verify that the target agent runtime has been successfully deleted.

      ```Bash
      agentkit runtime list
      ```

2. Clean up associated cloud resources.

   1. Execute the following command to enter the root directory of the target agent.

      > **tip**

      > Replace `it-support-agent` with the actual path to the root directory of the agent project.

      ```Bash
      cd it-support-agent
      ```

   2. Execute the following command to view information about the cloud resources associated with the target agent during deployment.

      ```Bash
      agentkit config --show
      ```

      In the `cloud Mode Configuration` module of the output, you can obtain information about the cloud resources associated during deployment.

      |Resource name |Description |Screenshot |
      |---|---|---|
      |region |The region to which the cloud resources belong. |![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea81aca2ae6abbf414e95be261f34482.png)<br><br> |
      |tos_bucket |The TOS bucket name. The default naming rule is `agentkit-platform-{{account_id}}`.<br><br>> **tip**<br><br><br>> `{{account_id}}` is the account ID placeholder. Replace it with the BytePlus account ID associated with your AK/SK.<br> ||
      |cr_instance_name |The CR instance for storing built images. The default naming rule is `agentkit-platform-{{account_id}}`. ||
      |cr_namespace_name |The namespace under the CR instance. ||
      |cr_repo_name |The specific repository name in CR, used to store the current agent's image and different versions. ||
      |cp_workspace_name |The name of the workspace to which the CP pipeline belongs.<br><br>> **tip**<br><br><br>> Code Pipeline (CP) is a managed continuous integration (CI) build service in the AgentKit cloud deployment pipeline. It automatically builds the uploaded agent code package into a container image in a standardized cloud environment and pushes it to CR. [Learn more](https://docs.byteplus.com/en/docs/cp/What_is_Code_Pipeline?lang=en)<br> ||
      |cp_pipeline_name |The name of the CP pipeline. ||
      |cp_pipeline_id |The CP pipeline ID. ||

   3. Delete unused cloud resources as needed.

      **Delete TOS-related resources**

1. Log in to the TOS [Buckets console](https://console.byteplus.com/tos/bucket?projectName=default).

      2. Use the bucket name obtained in the previous step to locate the target bucket.

      3. Click the bucket name to go to the details page and clear all files stored in the bucket.

      4. Return to the bucket list page and click the "Delete" button in the "Actions" column for the target bucket.

      5. After confirming the information, click the "Delete" button to complete the operation.

      **Delete CR-related resources**

1. Log in to the [CR console](https://console.byteplus.com/cr/region:cr+cn-beijing/instances).

      2. In the top navigation bar, select the region where the target repository instance is located.

      3. Use the CR instance name obtained in the previous step to find the target instance.

      4. If you no longer need the CR instance and all its data, you can permanently destroy the instance and its resources with one click. [Learn more](https://docs.byteplus.com/en/docs/cr/Destroy_mixed_billing_instances_pending_payment)

         > **tip**

         > To retain the repository instance, click the "Enter Instance" button and delete namespaces, OCI artifacts, and other resources as needed. [Learn more](https://docs.byteplus.com/en/docs/cr/delete-a-namespace)

         1. Click the "... \> Completely destroy" button on the target instance card.

         2. Verify the repository instance information, enter the repository instance name, and click the "Completely destroy" button to complete the operation.

      **Delete CP-related resources**

1. Log in to the [CP console](https://console.byteplus.com/cp/region:cp+cn-beijing/v2/workspace?limit=10&start=0&tab=all).

      2. In the top menu bar, select the region where the target workspace is located.

      3. Use the CP workspace name obtained in the previous step to find the target workspace.

      4. If you no longer use the workspace and all configurations such as pipelines within it, you can delete the workspace and its resources with one click. [Learn more](https://docs.byteplus.com/en/docs/cr/Destroy_mixed_billing_instances_pending_payment)

         > **tip**

         > To retain the workspace, click the workspace name and delete pipeline resources within it as needed. [Learn more](https://docs.byteplus.com/en/docs/cp/Pipeline_management?lang=en#.5Yig6Zmk5rWB5rC057q_)

         1. Click the "... \> Delete" button in the "Actions" column of the target workspace.

         2. Confirm the workspace information, enter the workspace name, check "Also delete related resources in the deployment clusters of all applications associated with the workspace", and click the "Delete" button to complete the operation.

## What to do next

After the agent is launched, you can also update its instance specifications, custom image, model, environment variables, and other configurations at any time in the console. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime)

> **warning**

> After updating the agent runtime configuration, you need to republish it for the new configuration to take effect. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes)
