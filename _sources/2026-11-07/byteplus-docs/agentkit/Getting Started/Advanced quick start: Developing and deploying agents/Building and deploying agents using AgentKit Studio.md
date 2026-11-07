---
title: "Building and deploying agents using AgentKit Studio"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio"
---

This guide shows you how to visually create, test, and publish an agent from scratch using AgentKit Studio, and deploy it as an AgentKit cloud\-based agent runtime.

## Background information

AgentKit Studio is an all\-in\-one workbench for agent development, testing, and delivery. It consolidates model configuration, prompt authoring, tool and skill integration, knowledge base configuration, online testing, deployment and publishing, version management, and observability and evaluation into a single entry point. It is suitable both for rapidly validating agent ideas and for turning proven capabilities into collaborative, maintainable, and continuously improvable agent applications for your team.

* If you are an individual developer new to agents, you can complete configuration and test runs through the AgentKit Studio visual interface, reducing your reliance on code, the command line, and logs.

* If your team has moved into the collaboration, go\-live, and continuous operations phase, you can use AgentKit Studio as a unified engineering entry point for managing login state, session history, access control, version iteration, and multi\-role collaboration.

## Prerequisites

|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). |
|Activate the service |The AgentKit service has been activated. To activate AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br>> **tip**<br><br><br>> The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.<br> |
||[You have activated Container Registry](https://console.byteplus.com/cr). |
||[ModelArk has been activated](https://console.byteplus.com/ark/openManagement). |
|Obtain the API access key |Create and obtain an API access key pair (Access Key ID and Secret Access Key) for calling BytePlus cloud resources. [Learn more](https://docs.byteplus.com/en/docs/IAM/creating-an-access-key?redirect=1) |

## Environment configuration

We recommend using the `uv` tool to manage your Python environment and placing AgentKit\-related dependencies in a separate virtual environment to avoid affecting other Python projects running on your machine.

1. Log in to the machine where you want to install VeADK and AgentKit SDKs.

2. Execute the following command to confirm that the Python version is **3.10 or later**.

   ```Bash
   python --version
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cfd053631e425aefef3e85acf5e9c05.png)

3. Execute the following command to download and install the `uv` tool.

   **Use the curl tool**

```Bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

   **Use the wget tool**

```Bash
   wget -qO- https://astral.sh/uv/install.sh | sh
   ```

4. Execute the following command to create and activate a `uv` environment. In the example provided in this guide, a virtual environment named `.venv` is created and activated based on `Python 3.13`.

   ```Bash
   uv venv --python 3.13 .venv
   source .venv/bin/activate
   ```

   Once the environment is activated, you will see the virtual environment name in parentheses at the beginning of your command line.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56bf157546342aa9e4ccce521a51aded.png)

5. Execute the following command to install VeADK and AgentKit SDKs in the activated virtual environment.

   > **tip**

   > In the example provided in this guide, version `1.1.14` is installed. You can replace `1.1.14` with your target version number, or execute the `uv pip install -U veadk-python` command to install the latest version.

   ```Bash
   uv pip install veadk-python==1.1.14
   ```

6. Execute the following command to check whether the installation is successful.

   ```Bash
   veadk --version
   ```

   If output similar to the following is displayed, the installation is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cf9e361634ddfd8b645ebdca360f4fb.png)

## Develop an agent

### **Step 1: Launch AgentKit Studio**

1.  **(Optional)**  If you have exited the virtual environment, execute the following command to reactivate it. Otherwise, skip this step.

   ```Bash
   source .venv/bin/activate
   ```

2. Execute the following command in your local terminal to set environment variables.

   > **warning**

   > Since AK/SK are highly sensitive credentials, directly writing them into static configuration files, such as `.env`, poses a security risk. When you configure BytePlus AK/SK in the local development environment, we recommend managing them by exporting session\-level environment variables in the terminal.

   ```Bash
   export BYTEPLUS_ACCESS_KEY=<your_access_key>
   export BYTEPLUS_SECRET_KEY=<your_secret_key>
   ```

3. Start AgentKit Studio.

   1. Select a startup method for AgentKit Studio.

      AgentKit Studio supports two startup methods: **local startup** and **cloud deployment**.

      > **tip**

      * > We recommend using the **local startup** method first to complete the initial agent validation. Confirm that the agent, model, tools, and page flow work normally and as expected. Switch to the **cloud deployment** method when your team needs stable multi\-user access, unified login, or external demos.

      * > The **cloud deployment** method is built on [veFaaS](https://docs.byteplus.com/en/docs/faas/Overview_of_the_Application_center?lang=en) and [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway). While the services are running, you are **charged continuously** based on the number of calls and public network traffic. To avoid unexpected charges, review the billing rules before use. For details, see [veFaaS \- Billing overview](https://docs.byteplus.com/en/docs/faas/Billing_overview) and [APIG \- Billing overview](https://docs.byteplus.com/en/docs/apig/Billing_overview).

      |**Item** |**Local startup** |**Cloud deployment** |
      |---|---|---|
      |**Access scope** |You need to install and start the AgentKit Studio runtime environment locally. Only local access is supported. |Only the deployer needs to install the AgentKit Studio runtime environment locally and deploy AgentKit Studio as a Serverless application using [veFaaS](https://docs.byteplus.com/en/docs/faas/Overview_of_the_Application_center?lang=en). All team members can use the unified public network address provided by the veFaaS application to access AgentKit Studio. |
      |**Application scenarios** |* First\-time experience with AgentKit Studio, with a focus on opening the workbench quickly and understanding the core workflow.<br><br>* Frequent adjustments to agent code, model parameters, tool configurations, or prompts during development, with immediate result checking.<br><br>* Troubleshoot local issues, such as missing dependencies, configuration errors, model invocation failures, or page loading exceptions.<br><br>* Single\-developer or small\-group testing, with no requirement for public access, unified login, or long\-term multi\-user collaboration. |* Multi\-member access to AgentKit Studio through a unified public endpoint, reducing issues caused by differences in local environments.<br><br>* Demos for product, operations, customers, or partners, with a stable and reusable access entry point.<br><br>* Integration with an account system, role\-based access control, access auditing, or multi\-user isolation.<br><br>* Incorporation of AgentKit Studio into the enterprise application O&M system for long\-term maintenance of its runtime status, data storage, and access policies. |
      |**Identity authentication** |Primarily relies on the local environment and developer self\-management. Not suitable as an enterprise account system or audit entry point. |Supports login via [AgentKit Identity](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01) with identity verification through JWT. Suitable for use cases that require user identity, role\-based permission, and access auditing. |

   2. Go to the AgentKit Studio page.

      **Local startup**

1. Execute the following command to start AgentKit Studio locally.

         ```Bash
         veadk studio
         ```

         When the following output is displayed, it indicates that AgentKit Studio has started successfully. Follow the on\-screen instructions to get the link for accessing the web interface.

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7af1b07aaf159c2e2accca87694a3c74.png)

      2. In a local browser on the machine where your project is located, open the access address obtained in the previous step. This guide uses `http://127.0.0.1:8000`.

      3. Enter a custom username for this test to go to the AgentKit Studio page.

         > **warning**

         > AgentKit Studio identifies agents under development and agents published to AgentKit by username. We recommend using the same username each time you launch AgentKit Studio.

      **Cloud deployment**

1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and follow the console instructions to activate the veFaaS service.

      2. Execute the following command to deploy the local AgentKit Studio to the cloud.

         > **tip**

         * > Adjust the following parameters as needed:

            * > `--vefaas-app-name`: Specify the veFaaS application name.

            * > `--region`: Specify the region of the veFaaS application. Make sure this region is consistent with the region where you want to create the AgentKit agent runtime. Supported:

               * > ap\-southeast\-1: Asia Pacific (Johor)

         * > By default, this command creates an AgentKit Identity user pool and client for managing enterprise SSO login.

            * > If you want to use an existing user pool and client in AgentKit Identity, retrieve the[user pool ID](https://docs.byteplus.com/en/docs/identity/Create_a_user_pool?_vtm_=a78999.b69280.0_0.0_0.0.258_7696806410223453701)and [client ID](https://docs.byteplus.com/en/docs/identity/Create_a_client), and add the`--user-pool-id "your-user-pool-UID"` and`--allowed-client-id "your-client-UID"` parameters to the deployment command. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01)

            * > To enable local password login, passwordless login, registration, recovery, and unconfirmed user login flows for the user pool and client created by AgentKit Studio, add the`--allow-dangerous-login true`parameter to the command. This parameter takes effect only for user pools created by AgentKit Studio. If you specify an existing user pool by using`--user-pool-id`, its existing login configuration is retained. **Because this parameter can reduce login security, we do not recommend using it in production environments.**

         * > Before deployment, this command automatically verifies the permissions required to create cloud resources. If any permissions are missing, the command line displays the missing items, and deployment is paused. We recommend that you grant the missing permissions as prompted and then run the command again. If you confirm that the current account already has equivalent permissions, you can choose to continue. AgentKit Studio then ignores the permission issues and **continues attempting to create cloud resources**.

         ```Bash
         veadk studio deploy \
           --vefaas-app-name "veadk-studio" \
           --region "cn-beijing"
         ```

      3. After the deployment is complete, you can obtain the unified public access URL, the AgentKit Identity user pool ID (`user pool id`), the client ID (`client id`), and other cloud resource information from the `Frontend deployed` parameter in the output.

      4. Configure the login method.

         1. Log in to the [AgentKit Identity console](https://console.byteplus.com/agentkit/region:agentkit+cn-beijing/identity).

         2. Use the AgentKit Identity user pool ID (`user pool id`) obtained in the previous step to find and open its details page.

         3. As needed, [create users](https://docs.byteplus.com/en/docs/identity/Create_a_user) or [add an external identity provider](https://docs.byteplus.com/en/docs/identity/Add_external_identity_providers) to manage user identities outside the agent identity and access management platform.

      5. In any browser with public network access, open the AgentKit Studio public access URL.

      6. Log in with an authorized account to access the AgentKit Studio cloud page.

### Step 2: **Create an agent**

This step uses creating a chatbot named `personal_assistant` as an example to describe how to configure the primary agent, model, tools, skills, knowledge base, and memory in AgentKit Studio.

1. In the left directory pane, select "Agents" and click the "Create agent" button.

2. Select the creation method.

   > **warning**

   > This feature is supported only in VeADK `1.1.8` and later versions.

   |Method |Description |
   |---|---|
   |Fast mode |An agent created in this mode automatically includes the built\-in **CreateAgentToolset ** (a dynamic agent delegation toolset). At runtime, the primary agent can automatically collect the required resources based on the user's task, create sub\-agents, and transfer the tasks to the sub\-agents for execution. This mode also supports calling skills on demand, autonomous planning, multi\-agent collaboration, process tracing, and automatic summarization of results.<br><br>This mode is suitable for scenarios where task goals are relatively open, and steps must be broken down during execution, such as information collection, complex Q&A, and multi\-step task processing. |
   |Traditional mode |Supported operations include visually configuring the agent structure and applying fine\-grained control over the model, tools, parameters, and execution logic. You can also migrate existing agents, test them in real time, and optimize performance as needed. These capabilities help you integrate existing agent projects with AgentKit and publish them. **This guide uses this method to create the agent.** <br><br>This mode is suitable for scenarios where the agent workflow and structure are already defined, and you need fine\-grained control over runtime parameters and execution logic. Examples include targeted agent testing, performance optimization, and stability validation. |

4. Select a method for adding a new agent.

   |Method |Description |
   |---|---|
   |Quickly create from scratch |Create a new agent in AgentKit Studio from scratch, configure the model, system prompt, tools, memory, knowledge base, and skills one by one, and deploy the agent directly to AgentKit after testing. This guide uses this method. **This guide uses this method to create the agent.** <br><br>This method is suitable for building a new agent application for the first time, designing the capability structure based on business goals, or validating the effect of each configuration step by step in a visual interface. |
   |Intelligent mode |Describe the problem that you want the agent to solve in a single paragraph. Based on your natural language input, AgentKit Studio automatically determines your intent, builds, and tests the project. It then performs temporary verification in the cloud and generates deployable source code.<br><br>This method applies to scenarios where you have clear business goals but are not familiar with the details of agent configuration.<br><br>> **tip**<br><br><br>> Intelligent mode requires a development sandbox configured with Codex.<br><br><br><br>* > When you **run****locally**:<br><br><br>   1. > [Create a Code Sandbox sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) and obtain the template ID.<br><br><br>   2. > In the virtual environment where AgentKit Studio is installed and running, execute the `export SANDBOX_DEV=<your_sandbox_id>` command.<br><br><br>      > Replace `<your_sandbox_id>` with the actual sandbox template ID.<br>      <br><br>   3. > Re\-execute the `veadk studio` command to start AgentKit Studio.<br><br><br>* > During **cloud** **deployment**, the sandbox is created automatically and no additional configuration is required.<br> |
   |Add and deploy from a code package |Upload an existing agent project archive (.zip), view or edit the project configuration in AgentKit Studio, and deploy the project directly to AgentKit.<br><br>This method is suitable for quickly deploying an existing VeADK project to production, or redeploying an existing project after making minor adjustments to it.<br><br>> **warning**<br><br><br>> The agent project archive must meet the following requirements:<br><br><br><br>* > The size must not exceed 50 MB.<br><br><br>* > The number of files after extraction must not exceed 800.<br><br><br>* > The root directory must contain an app.py file as the AgentKit startup entry point.<br> |
   |Create from workspace |Studio provides a persistent cloud code project environment. Each user has a persistent cloud sandbox, with projects stored as directories under `/home/gem/Projects`. The workspace also provides cloud VS Code for writing, debugging, and managing project code online.<br><br>This is suitable for creating a VeADK\-compliant agent project from scratch and completing development, testing, and subsequent deployment in AgentKit Studio. |
   |Migrate from existing project |Upload an existing agent project archive (.zip). AgentKit Studio then automatically analyzes the project framework and entry point via Codex in the sandbox and generates a deployable VeADK project.<br><br>This method is suitable for quickly converting existing agent projects built on frameworks such as LangChain, LangGraph, and Dify into VeADK\-compliant projects and deploying them to AgentKit.<br><br>> **tip**<br><br><br><br>* > You can migrate existing projects built on LangChain, LangGraph, Google ADK, Strands, AgentCore, and Dify.<br><br><br>* > If your project framework is not one of the preceding frameworks, AgentKit Studio performs an Agentic migration based on the general migration mode (Any).<br> |

5. Follow the on\-screen instructions to configure the primary agent.

   > **tip**

   * > The primary agent is the entry point of an agent project. It receives user input, handles overall planning, and schedules subsequent capabilities. The primary agent type determines how the project is controlled: an LLM agent responds directly through model inference, while sequential, parallel, and loop agents are orchestration\-type primary agents that contain no model\-related configuration and schedule sub\-agents according to rules.

   * > To build a multi\-agent project that includes both primary and sub\-agents, see [Multi\-agent overview](https://volcengine.github.io/veadk-python/cn/docs/framework/multi-agent/overview/)for planning.

   * **Select** ** the primary agent type**

      |Type |Description |
      |---|---|
      |Agent |An autonomous decision\-making agent built on a large language model, supporting full intelligent conversation, tool calls, memory management, and more. It can **automatically call sub\-agents or tools** based on its configuration to complete complex tasks. **In this guide, this type of agent is created.** <br><br>This type is suitable for single\-agent conversations, strategy\-based tasks, and scenarios with dynamic requirements and unpredictable steps. |
      |Distributed collaboration |A sequential agent with no built\-in language model capability. It schedules sub\-agents ** one by one in series** to complete tasks, like a pipeline that only runs from front to back.<br><br>This type is suitable for tasks with clearly defined phases such as retrieval → summarization → generation → review. |
      |Parallel processing |A parallel agent with no built\-in language model capability. It runs multiple sub\-agent tasks **concurrently** and aggregates the results.<br><br>This type is suitable for simultaneous multi\-source retrieval, generation of multiple candidate solutions, or tasks requiring faster execution. |
      |Loop execution |A loop agent with no built\-in language model capability. It loops through a multi\-step workflow of sub\-agents within ** an iteration limit**, stopping when a condition is met or the maximum number of iterations is reached.<br><br>This type is suitable for tasks with clear quality thresholds that require multiple rounds of improvement, such as a generate → review → fix cycle. |

   * **Configure ** **basic** ** information**

      |Parameter​ |Description |
      |---|---|
      |Agent name |Specify a name for the agent. **This guide uses ** **`personal_assistant`** ** as an example**. |
      |Description |Enter a brief description of the agent's features, characteristics, and use cases. The description will be displayed in the agent list and selector. **This guide uses the default configuration as an example.**  |
      |System prompt |Defines the agent's role, objectives, execution strategy, and output format. This is the core static configuration that determines what the agent acts as, what it does, how it does it, and how it presents its output. **This guide uses the default configuration as an example.**  |

   * **Configure the model information**

      A model is the core capability source that enables an agent to understand, reason, and generate responses. It transforms user inputs into useful answers, solutions, or content, and serves as the foundation for intelligent interaction.

      |Parameter​ |Description |
      |---|---|
      |Model source |Configure the model that provides inference services for the agent. Supported:<br><br><br>* **ModelArk**: Use models from [ModelArk](https://docs.byteplus.com/en/docs/modelark/product-overview) to provide inference services for the agent.<br><br>   > **tip**<br>   <br><br>   > If no API Key is available, go to the [API Key management](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D) console to create one.<br>   <br><br>* **Custom**: Use a self\-hosted or third\-party model to provide inference services for the agent. Enter the service provider name, the API endpoint for the model, and the API Key. |
      |Model configuration |When you select **ModelArk** as the model source, you need to configure the following:<br><br><br>* **API Key**: Select the API Key for calling ModelArk models from the drop\-down list.<br><br>* **Model**: Select the primary model for inference services from the drop\-down list. **This guide uses the ** **`doubao-seed-2-1-pro-260628`** ** model on ModelArk as an example.** <br><br>* **Fallback model**: When configuring LLM agents, you can add an ordered list of fallback models for each agent. If the primary model is unavailable, the system automatically switches to the next model in order. **This guide uses the default configuration as an example.** <br><br>   * **Same provider**: Specify only the model name. The provider, API endpoint, and API Key are automatically reused from the primary model. The generated project code implements fallback through the model_name list.<br><br>   * **Cross\-provider**: Specify the model provider, API endpoint, and API Key separately for each fallback endpoint. |

   * **Configure tools**

      A tool is an executable capability that an agent can invoke to transform model decisions into concrete actions. Tools enable an agent not only to understand a problem, but also to perform real operations such as querying, calling, retrieving, and writing, increasing task automation and practical applicability. For example, an agent can use tools to check inventory, send requests, or read files.

      |Parameter​ |Description |
      |---|---|
      |Built\-in tool |Built\-in tools are native function tools pre\-packaged by VeADK, ready to use out of the box. They give an agent capabilities such as web search, code execution, and image/video generation powered by BytePlus, with no need to implement the underlying logic. **This guide uses code execution as an example.** <br><br><br>* **Web search**: Performs a full web search using **Searchinfinity**.<br><br>   > **tip**<br>   <br><br>   * > BytePlus **Searchinfinity** is an online search service built for large language models. It provides multi\-vertical, multi\-source search capabilities through a flexible API.<br>   <br><br>   * > Two billing methods are supported: **pay\-as\-you\-go** and **subscription plans**. Response billing is handled through their respective API keys.<br>   <br><br>* **Parallel web search**: Queries search engines for results using input keywords, and returns structured content including page titles, links, and summaries. This is suitable for scenarios that require real\-time retrieval of online information, improving the timeliness of model responses, or generating search\-augmented content.<br><br>* **Web reader**: Accepts a webpage URL, retrieves and parses its content. It is typically used alongside a search tool to let an agent dig into the content of a target page.<br><br>* **Image generation**: Generates images based on input images and text descriptions.<br><br>* **Image editing**: Edits an existing image based on text instructions provided by the user, such as replacing elements or changing the style.<br><br>* **Video generation**: Generates videos based on input images and text descriptions.<br><br>* **Code execution:**  Uses the AgentKit sandbox template AIO Sandbox as the execution tool for code tasks. This is suitable for scenarios where an agent needs to develop and debug code in a sandbox environment.<br><br>   1. [Create a sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).<br><br>   2. Obtain environment variables: After creation, navigate to the "Integration code" tab on the tool details page to get the required environment variables of the tool.<br><br>   3. Enter the sandbox ID for code execution (`AGENTKIT_TOOL_ID`) and the region of AgentKit tools (`AGENTKIT_TOOL_REGION`). |
      |More tool types |Configure more types of tools for the agent. Supported:<br><br><br>* **MCP tools:**  [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) is an open protocol for connecting large language models with external tools and data sources. AgentKit Studio supports connecting to MCP tools via two transport methods, `HTTP` (streamable\-http) and `stdio`, and invoking them on demand during inference.<br><br>   **This guide uses an MCP service created on the AgentKit platform as an example. You need to:** <br><br>   1. [Create an MCP service](https://docs.byteplus.com/en/docs/agentkit/MCP_services): Create or import MCP tools as needed, such as Sequential Thinking MCP or Map MCP.<br><br>   2. Obtain environment variables: After creation, navigate to the "Integration code" tab on the tool details page to get the required environment variables of the tool.<br><br>   3. Enter the MCP service URL (`MCP_SERVICE_URL`) and the MCP service authentication key (`MCP_SERVICE_API_KEY`).<br><br>   > **tip**<br>   <br><br>   > To govern MCP stability with the agent optimization component provided by AgentKit Studio, make sure that all MCP services to be governed **use the same service authentication key**. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio#zU7eaE0Z)<br>    |

   * **Configure skills**

      A skill is a standardized capability unit built for a specific task, packaging the knowledge instructions, execution workflow, code scripts, and related resources needed to complete the task. This allows an agent to quickly load a ready\-made capability on demand, reducing repetitive configuration and prompts while improving execution quality and efficiency. For example, an agent can invoke a document review skill to review and refine a technical document according to a fixed set of standards.

      When creating an agent, you can add skills from the following sources. After a skill is added, its files are written to the skills/ directory of the generated project.

      |Skill source |Description |
      |---|---|
      |Local file |Uploading a local folder or ZIP package containing skill information is supported.<br><br>> **tip**<br><br><br><br>* > Uploading a folder or ZIP package that contains multiple skills is supported.<br><br><br>* > Each skill directory must include a SKILL.md file. AgentKit Studio checks for file existence, file count, size, and path security. The complete frontmatter and skill format are validated by ADK at load time. In the generated project, the skill directory name is taken from the `name` field in SKILL.md or from the name of the uploaded directory.<br> |
      |BytePlus Find Skill marketplace |Search for skills by keyword in the BytePlus public skill repository and add them. |
      |AgentKit Skills Center |Browse the skills spaces in the AgentKit Skills Center that are visible to the current account, and select available skills and their versions. **This guide uses this skill source as an example.** <br><br>If no skills space or skill is available, you can:<br><br><br>1. [Create a skills space](https://docs.byteplus.com/en/docs/agentkit/Skills_space): A logical space for organizing and managing a set of skill versions.<br><br>2. [Create a skill](https://docs.byteplus.com/en/docs/agentkit/create_skills): Import a self\-built or third\-party skill into AgentKit.<br><br>3. [Add a skill to a skills space](https://docs.byteplus.com/en/docs/agentkit/Adding_and_Removing_Skills#OWabEO7z).<br><br>4. Select "AgentKit Skills Center", choose the target skills space from the drop\-down list, and add skills as needed. |

   * **Configure the knowledge base**

      A knowledge base provides an agent with an external knowledge source that is retrievable, updatable, and traceable. While a large language model has general language understanding and reasoning capabilities, it does not inherently know an enterprise's internal documents, product rules, latest policies, API specifications, or business workflows. By connecting this content to a knowledge base, an agent can retrieve relevant information before generating a response, reducing the likelihood of relying on experience\-based guesswork and producing responses that are more grounded in business facts.

      |Knowledge base backend |Description |
      |---|---|
      |VikingDB Knowledge<br><br> |Use the [VikingDB knowledge base](https://docs.byteplus.com/en/docs/RAG_Cloud/Core_process_of_knowledge_Q-A) provided by BytePlus. The VikingDB knowledge base supports parsing structured and unstructured documents, and enables semantic matching through chunking and vector retrieval. **This guide uses this knowledge base as an example.** <br><br>If no knowledge base is available, you can:<br><br><br>1. [Create a knowledge base](https://docs.byteplus.com/en/docs/RAG_Cloud/create_a_knowledge_base): Create a VikingDB knowledge base and upload files. You can upload materials such as news articles or personal notes based on your needs, which can be used to test the agent's functionality.<br><br>2. Select "VikingDB Knowledge", select the target knowledge base from the drop\-down list, and associate it with the current agent as needed. |
      |OpenSearch |Use a self\-hosted or managed OpenSearch cluster with a self\-configured embedding. |
      |Context Search |Use the BytePlus context search service for retrieval. [Learn more](https://docs.byteplus.com/en/docs/contextsearch/What_is_ContextSearch) |
      |OpenViking Knowledge |Use the OpenViking resource catalog knowledge base. Resource parsing and retrieval are handled on the server side, with no local embedding configuration required. |

   * **Configure memory**

      Memory is context information that an agent retains about users, sessions, or tasks. It allows an agent to maintain an understanding of the task background, user identity, and completed steps across multi\-turn conversations or cross\-session interactions, avoiding the need to start from scratch each time.

      |Parameters |Description |
      |---|---|
      |Short\-term memory |Saves context and intermediate state within the current session, helping an agent understand contextual references, track the progress of the current task, and reuse information already provided within the same conversation. This type of memory is generally discarded after the session ends or after a certain period of time. Supported:<br><br><br>* **Local memory:**  Stores short\-term memory in the running process of the current agent service, with no need to create an additional database or configure storage files. Short\-term memory stored in the memory is not retained after the process exits, the service restarts, or the instance is migrated. **This guide uses this storage location ** **as an example.** <br><br>* **SQLite file:**  Writes short\-term memory to a local database file. This option requires no separate database service deployment and supports persistent storage. It is suitable for single\-machine development, small\-scale trials, and offline demos.<br><br>* **MySQL:**  Writes short\-term memory to a local MySQL database.<br><br>* **PostgreSQL:**  Writes short\-term memory to a local PostgreSQL database. |
      |Long\-term memory |Saves information that remains valid for a user across sessions, allowing an agent to recognize users, reuse preferences, and continue long\-term tasks across different sessions and points in time, enabling personalized and continuous service. Supported:<br><br><br>* **Local vector store**: An in\-process vector store suitable for local debugging. Data is not persisted and an embedding model must be configured.<br><br>* **OpenSearch**: Use a self\-hosted or managed OpenSearch cluster with a self\-configured embedding model.<br><br>* **Redis**: Use Redis vector search with a self\-configured embedding model.<br><br>* **VikingDB Memory**: BytePlus VikingDB memory with user profile support, using the BytePlus credentials configured in AgentKit Studio. **This guide uses this memory as an example** **.** <br><br>* **OpenViking Memory**: OpenViking long\-term memory. Saves and retrieves preferences, events, and entities at the user level.<br><br>* **mem0**: Mem0 managed memory service. |

6.  **(Optional)**  To add sub\-agents to the primary Agent, click "Add sub\-agent" in the agent architecture diagram and follow Step 3 to complete the sub\-agent configuration. **This guide does not add any sub\-agents.**

   > **tip**

   * > A sub\-agent is a subordinate execution unit scheduled by the primary agent. Based on the architecture, the primary agent can automatically identify and assign tasks to the matching sub\-agent, enabling multi\-role collaboration.

   * > For a sub\-agent, you can also select the**remote agent** type and use an agent space in the AgentKit A2A Center that the current account has access to. This is suitable for integrating specialized capabilities already published to the A2A Center into a multi\-agent project. [Learn more](https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview)

7. After completing the configuration, click "Next" to proceed to the testing workflow.

### **Step 3: Test the agent locally**

1. Click the "Start environment" button to create a temporary local runtime environment for the agent.

2. Once the environment starts successfully, you can send test messages to the agent in the chat box to verify that it works as expected. For example: Introduce yourself.

   * If the test results do not meet your expectations, click "Previous" and confirm leaving the testing page to adjust the agent configuration.

   * If the test results meet your expectations, click "Use this configuration" or "Next". Then, confirm that you want to leave the test page and proceed to the configuration step for agent optimization items.

### Step 4: Select agent optimization items (optional)

You can enable optimization capabilities for the **primary agent** as needed. Through Harness Sidecar, AgentKit Studio provides enhancement services for an agent. These services improve the stability and task success rate of the agent without modifying the main code of the agent.  BytePlus agents do not currently support this optimization feature. Click "Next" to skip this step.

> **tip**

* > Harness Sidecar is an auxiliary service that runs in the same Pod as the main container. It improves the task success rate, enhances stability, and reduces token consumption for an agent without modifying the main code of the agent. For example, you can use Sidecar to proxy and govern model context requests and MCP tool calls, performing stability governance and request retries in a way that is transparent to the agent code.

* > After you enable Harness Sidecar optimization, the enhancement operations run in a controlled runtime environment and involve access to the model and the MCP gateway. **Make sure that the configured model credentials, MCP gateway address, and access scope meet the data processing and security requirements of your business.**

1. Select the agent optimization scenario.

   |**Optimization scenario** |**Description** |**Components selected by default** |
   |---|---|---|
   |**Custom** |This mode is suitable for scenarios where you want to select optimization components as needed.<br><br>> **tip**<br><br><br>> If you do not select any component, Sidecar is not started.<br> |\- |
   |**O&M scenario** |Based on common agent O&M scenarios, AgentKit Studio selects the commonly used optimization items in the corresponding scenario by default. This is suitable for scenarios that require improving the diagnosis success rate and stability of O&M agents, such as diagnosing production service issues and production database issues.<br><br>> **tip**<br><br><br>> When "O&M scenario" is selected, SQL read\-only protection is automatically loaded.<br> |* **Higher answer quality**<br><br>   * Context governance<br><br>   * Answer validation and repair<br><br>* **Higher operational stability**<br><br>   * Goal task control<br><br>   * MCP stability governance |

2. Select the components used for agent optimization.

   |Purpose |**Component** |Description |
   |---|---|---|
   |**Higher answer quality** |Context governance |Used to govern context assembly, task anchoring, and the context budget to reduce the impact of irrelevant context on answer quality. |
   ||Answer validation and repair |Used to validate evidence and answer content. If the validation fails, perform a repair or trigger an alert. |
   |**Lower operating costs** |Context and result compression |Used to compress long contexts and large tool responses to reduce token usage. |
   |**Higher operational stability** |Goal task control |Used to manage the progress, resumption, and completion conditions of Goal tasks so that long\-running tasks can finish reliably. |
   ||MCP stability governance |Used to govern MCP connections, timeouts, empty results, large responses, and call budgets. SQL read\-only protection is included by default.<br><br>> **tip**<br><br><br>> Make sure that you have added an MCP tool to the **primary agent**. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio#BR35GlsO)<br> |

   > **tip**

   > After you enable the optimization options, add the runtime configuration required by the optimization components to the environment variables when you publish the agent to AgentKit. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio#w5c6d17e)

3. Click "Next" to configure the cloud environment.

### Step 5: Configure the cloud environment

You can choose the base runtime environment for agent deployment to ensure consistent dependencies, reusable environments, and controllable O&M across deployments.

> **tip**

> A runtime environment is essentially a set of reusable image configurations that include the operating system, Python version, command\-line tools, skills, Dockerfile, and other components.

1. Select the target environment from the drop\-down list. **This guide uses the default environment preset in AgentKit Studio.**

2. Click "Next" to proceed to the agent publishing process.

### Step 6: Publish the agent

1. Confirm the current agent architecture.

2. Complete the following deployment configuration.

   |Parameter​ |Description |
   |---|---|
   |Runtime name |Configure the runtime name. By default, it is generated from your primary agent name, with a random suffix appended. |
   |Deployment region |Configure the deployment region for the runtime. Supported regions: China (Beijing) and China (Shanghai). **This guide uses ** **the China (Beijing) region ** **as an example**. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Available_regions) |
   |Access authentication |Configure the authentication method for accessing managed resources of the agent runtime. Supported:<br><br><br>* **API Key**: After you enter a name, an API Key will be automatically created and associated with the agent runtime. After the agent runtime is created, you can view the API Key on the agent runtime details page. **This guide uses ** **API Key authentication as an example.** <br><br>* **User pool:**  Uses the OAuth authorization mode to obtain access tokens and make API calls, enhancing security and simplifying configuration. Before configuring this option, ensure that you have [created a user pool](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01?lang=en#zL1cxFcx) and [a client](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01?lang=en#zL1cxFcx).<br><br>   > **tip**<br>   <br><br>   > For agents using OAuth JWT inbound authentication, if you need to use the [**online test**](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts) feature for testing, the client must be of the M2M type.<br>    |
   |Deliver an agent via GitHub |Studio can deliver the agent source code generated through custom creation to a GitHub repository. This is suitable for teams that require version management and Code Pipeline. **This guide does not configure this feature.** <br><br><br>* **Delivery modes:** <br><br>   * **GitHub code synchronization**: AgentKit Studio pushes the generated source code directly to the target branch. AgentKit Studio manages this branch, and synchronization fails when a remote conflict occurs.<br><br>   * **Mounted Code Pipeline:**  The target branch is initialized after the first successful deployment (that is, the source code and the GitHub Actions workflow are written to the branch). Subsequent pushes to this branch trigger the workflow and update the bound Runtime.<br><br>* **Configuration parameters:** <br><br>   * **GitHub URL**: The URL of the target GitHub repository. You can enter `owner/repository `or the full GitHub HTTPS or SSH URL. Currently, only `github.com` repositories are supported.<br><br>   * **Token**: The token required to access the target GitHub repository. This token must have `contents` write permission and `pull request` permission for the target repository, which are required to push source code, initialize a branch, or write the workflow.<br><br>   * **Target branch**: Optional. The branch that receives source code pushes and that the GitHub Actions workflow monitors. The default value is `main`.<br><br>   * **BytePlus AK**: The Access Key ID for the BytePlus access key. When you enable "Mounted Code Pipeline", AgentKit Studio writes the key to a GitHub Actions secret. The workflow can then access BytePlus cloud resources and publish the agent runtime.<br><br>   * **BytePlus SK**: The Secret Access Key for the BytePlus access key.<br><br>      > **tip**<br>      <br><br>      > Create and obtain an API access key pair (Access Key ID and Secret Access Key) for calling BytePlus cloud resources. [Learn more](https://docs.byteplus.com/en/docs/IAM/creating-an-access-key?redirect=1)<br>      <br><br>   * **BytePlus Session Token**: Optional. The session token for the temporary access credential. You can call the STS[ AssumeRole ](https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole)API operation to obtain temporary access credentials. |
   |Message channel |You can integrate a message channel for the agent. After a message channel is integrated, you can chat with the agent directly through the message channel, and the agent can also use bot capabilities to help you create documents, schedule events, and more. Supported:<br><br><br>* **Feishu:**  Integrates the Feishu message channel. Before the configuration, go to the [Feishu Open Platform](https://open.larkoffice.com/app?lang=zh-CN) to create a bot application and obtain its App ID and App Secret. |
   |Instance settings |Configure the number of compute resource instances for running the agent. **This guide uses the default settings.**  |
   |Network |Configure the network access method for the agent runtime. Supported options:<br><br><br>* **Public network**: Accesses the agent runtime over the public network. This is suitable for scenarios that require quick access from browsers, mobile clients, third\-party SaaS platforms, external business systems, or cross\-network environments. **This guide uses public network access.** <br><br>* **VPC**: Select any VPC and subnet in the same region. Up to one subnet can be selected per availability zone. This is suitable for scenarios where the runtime is used only within an enterprise intranet or a controlled network, such as when the runtime needs to access a private database or other resources accessible only over a private network.<br><br>* **Public network + VPC:**  Supports access to the agent runtime over both the public network and a private network. This is suitable for hybrid scenarios that require an external access endpoint and connectivity to services, databases, or middleware in the enterprise private network, such as providing agent services to external applications while accessing a private knowledge base, workflow service, or business system internally.<br><br><br>> **tip**<br><br><br>> When the **network** includes a **VPC**, you can enable the shared public network egress feature within the VPC as needed. After this feature is enabled, the runtime will access the public network through the public network egress provided by the platform. If shared public network egress is not enabled, the public network egress configured in your private network (such as [EIP](https://docs.byteplus.com/en/docs/ecs/EIP-overview), [NAT gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway), and other public network products) will be used by default to access the public network.<br> |
   |Evaluation set |Configure whether to enable the automatic creation of an AgentKit Studio evaluation set. **This guide uses the default setting with automatic evaluation set creation enabled.** <br><br>> **tip**<br><br><br><br>* > An evaluation set is a carefully designed standardized test dataset used to systematically evaluate agent performance.<br><br><br>* > When this feature is enabled, AgentKit Studio automatically creates Good Case and Bad Case evaluation sets for the agent. Failure to create an evaluation set **does not affect** the normal operation of the agent runtime.<br> |
   |Resource configuration |Configure the cloud resources used for image building and publishing during deployment to the AgentKit agent runtime.<br><br>> **tip**<br><br><br>> TOS, CR, and CodePipeline together form a complete, standardized, and traceable automated CI/CD delivery pipeline.<br><br><br><br>* **TOS bucket**: Stores object files generated or used during agent deployment, such as code packages, build artifacts, and resource files required at runtime. [Learn more](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos?lang=en)<br><br>* **Container Registry (CR)** : Hosts and distributes the built runtime container images, allowing the runtime to pull a specified image version from the registry for publishing. [Learn more](https://docs.byteplus.com/en/docs/cr/what-is-cr?lang=en)<br><br>* **CodePipeline**: Serves as the automated execution engine for the runtime deployment process, sequentially performing build, validation, and publishing operations based on a preset configuration. [Learn more](https://docs.byteplus.com/en/docs/cp/What_is_Code_Pipeline?lang=en)<br><br><br>The cloud resources used for image building and publishing support the following configuration methods:<br><br><br>* **Auto** **\-create**: The default method. AgentKit Studio automatically creates the required resources during deployment. Resource names are generated automatically by AgentKit Studio based on the account ID and deployment region, and the selected resources are recorded in the agent runtime tags after deployment. **All resources in this guide are created automatically.** <br><br>* **Specify name**: Enter a resource name. AgentKit Studio creates the cloud resource using that name during deployment.<br><br>* **Select existing**: Select from existing resources in the current BytePlus account. AgentKit Studio loads the list of resources you have permission to use based on the configured BytePlus credentials (AK/SK). |
   |Environment variables |View the environment variables included in the component and optionally configure custom environment variables that the agent code can read directly at runtime. This enables separation of code and configuration, enhancing code portability.<br><br>If you selected ** MCP stability governance ** in[ Step 4: Select optimization items](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio#zU7eaE0Z) for the agent, configure the following environment variables:<br><br><br>* **MCP_URLS**: Enter the URLs of the MCP tool services that are added to the current agent and require stability governance. Separate multiple URLs with commas (`,`). For example: `https://a/mcp,https://b/mcp`.<br><br>* **MCP_API_KEY**: Enter the MCP service authentication key. This key is used for identity verification when the Sidecar accesses the MCP service.<br><br>   > **tip**<br>   <br><br>   > Make sure that all tools with stability governance enabled **use the same service authentication key**.<br>    |

   After completing the configuration, click the "Deploy" button.

5. After confirming the risk notice, click "Confirm deployment".

6. View the progress of deploying the current agent as an AgentKit agent runtime.

7. After the deployment is complete, you can test the agent runtime online, or use it directly from the AgentKit Studio page.

   > **tip**

   > You are charged based on actual usage when calling resources such as **agent runtimes, sandboxes**, and **MCP**. To avoid unexpected charges, review the billing rules before use. For details, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

   **Online test**

1. Copy the agent name and go to the [AgentKit agent runtime console](https://console.byteplus.com/agentkit/region:agentkit+cn-beijing/runtime).

   2. In the top navigation bar, select the region where the target agent runtime is located.

   3. Locate the target agent by name, and click "Online test" in the "Actions" column on the right.

   4. Send a test prompt (this guide uses "Introduce yourself" as an example) and verify that the response meets your expectations.

   **Use from AgentKit Studio**

1. [Open AgentKit Studio](https://docs.byteplus.com/en/docs/agentkit/Building_and_deploying_agents_using_AgentKit_Studio#dHeWX7ct).

   2. In the left directory tree, select "Agents" and click the target agent card.

   3. Click "Chat".

   4. Once the connection is established, you can send messages to the agent in the chat box and use the agent you deployed on the clou

## Observe and evaluate the agent

After the agent is published and online testing is complete, we recommend continuing to use AgentKit's observability and evaluation capabilities to verify its operating status and actual effectiveness, gradually progressing from "stable and usable" to "good enough to be worth launching".

### Observe the agent

Observability is used to view the agent's runtime performance during actual calls, helping you detect call chain anomalies, model invocation errors, log errors, or performance bottlenecks. Once observability is enabled, AgentKit and the VeADK SDK automatically collect trace (call chain) and metric data for each stage (such as model calls, tool execution, and memory retrieval) based on OpenTelemetry and deliver the data to the observability platform.

You can view the runtime monitoring data, session analysis, trace analysis, model monitoring data, and log analysis of the agent on the "Observability" page. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Observability-)

### Evaluate the agent

Evaluation measures the agent's performance across the three dimensions of effectiveness, performance, and cost through standardized experiments. It helps you determine whether the current version meets expectations and provides a basis for subsequent iteration, optimization, and launch.

* **Evaluate with ** **AgentKit** ** Studio**

   AgentKit Studio provides the capability to automatically consolidate evaluation data and generate optimization suggestions after an agent is deployed to AgentKit, helping developers quickly identify and fix issues during the conversation validation phase.

   1. When you enable the evaluation set creation feature while deploying an agent to AgentKit, AgentKit Studio automatically creates **Good Case** and **Bad Case** evaluation sets for that agent.

   2. After each conversation with the agent in AgentKit Studio, AgentKit Studio automatically assesses the quality of each conversation turn, categorizes it into the corresponding evaluation set, and generates optimization suggestions based on the accumulated evaluation cases.

   3. You can view evaluation information on the "Evaluation sets" tab of the corresponding agent details page in AgentKit Studio.

* **Evaluate online with AgentKit**

   AgentKit provides an online evaluation mechanism with three core modules: **evaluation sets**, **evaluators**, and **experiments**, covering the full evaluation pipeline from data preparation to result analysis. Evaluation sets provide standardized inputs and reference answers. Evaluators score results based on predefined rules using either an LLM or code. Experiments are responsible for combined execution and aggregating result metrics, while also supporting comparative analysis across multiple experiments. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Evaluation)

## What to do next

After the agent is launched, you can also update its instance specifications, custom image, model, environment variables, and other configurations at any time in the console. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime)

> **warning**

> After updating the agent runtime configuration, you need to republish it for the new configuration to take effect. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes)
