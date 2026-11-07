---
title: "Developing and deploying agents with VeADK"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial"
---

This topic describes the complete workflow of developing and testing an agent locally with VeADK and publishing the agent as an agent runtime with AgentKit.

<span id="RMvOfceB"></span>
## Background information

Volcengine Agent Development Kit (VeADK) is an agent development framework provided by BytePlus. It combines capabilities such as models, tools, memories, and knowledge bases into reusable components, with built\-in core capabilities including tool calling, multi\-turn conversations, and memory management. It also provides a standardized project structure and local testing tools, allowing you to complete the entire agent development process without relying on a cloud environment.BytePlus [Learn more](https://volcengine.github.io/veadk-python/cn/docs/framework/)

VeADK is deeply integrated with the BytePlus ecosystem. Agents built on this framework can also leverage AgentKit to gain the following capabilities:


* **Service calling:**  Call various services provided by AgentKit, such as MCP, memories, and knowledge bases, to quickly reuse platform capabilities.

* **Cloud publishing:**  Seamlessly publish to the cloud through AgentKit, reducing the adaptation cost between local development and cloud deployment.

* **Continuous optimization:**  Use AgentKit's capabilities, such as evaluation and observability, to continuously improve agent effectiveness.


<span id="tXcNeOZZ"></span>
## Prerequisites


|Condition |Requirements |
|---|---|
|Register an account |You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account). |
|Activate the service |The AgentKit service has been activated. To activate AgentKit, log in to the [AgentKit console](https://console.byteplus.com/AgentKit) and follow the system prompts to complete the operations.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.</div><br> |
||[ModelArk has been activated](https://console.byteplus.com/ark/openManagement). |
|Get an Access Key |You have created and obtained an [API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apiKey?apikey=%7B%7D) for accessing ModelArk model services. |
||You have created and obtained an API access key pair (Access Key ID and Secret Access Key) for calling BytePlus cloud resources. [Learn more](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).   |


<span id="kpQIAeev"></span>
## Environment configuration

We recommend using the `uv` tool to manage your Python environment and placing AgentKit\-related dependencies in a separate virtual environment to avoid affecting other Python projects running on your machine.


1. Log in to the machine where you want to install VeADK and AgentKit SDKs.

2. Execute the following command to confirm that the Python version is **3.10 or later**.

   ```Bash
   python --version
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cfd053631e425aefef3e85acf5e9c05.png) </span>

3. Execute the following command to download and install the `uv` tool.

   
   <Tabs>
   <Tab zoneid="V3vKdtxE92" title="Use the curl tool">
   <TabTitle>Use the curl tool</TabTitle>
   
   ```Bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="AKJqLFHMjX" title="Use the wget tool">
   <TabTitle>Use the wget tool</TabTitle>
   
   ```Bash
   wget -qO- https://astral.sh/uv/install.sh | sh
   ```
   
   
   
   </Tab>
   </Tabs>
   

4. Execute the following command to create and activate a `uv` environment. In the example provided in this topic, a virtual environment named `.venv` is created and activated based on `Python 3.13`.

&nbsp;

   ```Bash
   uv venv --python 3.13 .venv
   source .venv/bin/activate
   ```
   

   Once the environment is activated, you will see the virtual environment name in parentheses at the beginning of your command line.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56bf157546342aa9e4ccce521a51aded.png) </span>

5. Execute the following command to install VeADK and AgentKit SDKs in the activated virtual environment.

   ```Bash
   uv pip install -U veadk-python
   ```
   

6. Execute the following command to check whether the installation is successful.

   ```Bash
   veadk --version
   ```
   

   If output similar to the following is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7f3af41ade083d29157ffc90a311cff.png) </span>


<span id="HU8WjJWn"></span>
## Develop an agent

<span id="wzlSH6nR"></span>
### **Step 1: Initialize the application**


1.  **(Optional)**  If you have exited the virtual environment, execute the following command to reactivate it. Otherwise, skip this step.

   ```Bash
   source .venv/bin/activate
   ```
   

2. Execute the following command to generate an agent using the platform's preset project template.

   ```Bash
   veadk create
   ```
   

3. During execution, fill in the following information as prompted.

   1. Specify the agent project name. This name will also become your local directory name, for example, `personal_assistant`. Press "Enter" to confirm.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_327a59edd7d11fe590a1e5ec2c432120.png) </span>

   2. Enter `1` or `2` to select when to configure the API Key for calling the ModelArk model service (In this topic, `2` is selected). Press "Enter" to confirm.

      * `1`: Specify the ModelArk API Key now.

      * `2`: Skip this step and fill it in later, either manually in the environment variable file or automatically via BytePlus AK/SK.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81da18ca13c5391f5597bb9f4e579bd3.png) </span>

      After input, your local project structure is as follows:

      ```Plain Text
      your_project
      ├── __init__.py 
      ├── .env        
      └── agent.py    
      ```
      


<span id="pEILoMfw"></span>
### **Step 2: Write the ** agent **code**

This example uses the AgentKit "personal assistant agent" to demonstrate the workflow for building a simple personal assistant agent that uses multiple core components.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can refer to the <a href="https://deepwiki.com/volcengine/veadk-python">VeADK</a> documentation to develop an agent based on your actual business scenario. For agents in complex scenarios, see <a href="https://github.com/volcengine/agentkit-samples/tree/main/02-use-cases">Agent examples</a> and <a href="https://github.com/volcengine/agentkit-samples/tree/main/01-tutorials">Detailed tutorials</a>.</div>


<span id="0nHrVaNi"></span>
#### **Core features**


* Create a simple personal assistant agent.

* Short\-term memory: uses local memory to maintain conversation context.

* Long\-term memory: supports session memory and user history storage via VikingDB.

* Tool integration: supports code execution tools and the MCP toolset.


<span id="TgtVDetS"></span>
#### **Agent capabilities**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4cc8acf54c079d5ee5c1eb975271fa3e.jpeg) </span>

<span id="sQvVjOHv"></span>
#### **Agent code**


1. In the virtual environment where the agent was created, execute the following command to enter the project root directory.

   ```Bash
   cd <Project directory>
   ```
   

2. Execute the following command to open the agent.py file.

   ```Bash
   vim agent.py
   ```
   

3. Press the `i` key to enter edit mode, and then copy the following content to replace the existing content of the agent.py file.

   ```Python
   import asyncio
   import os
   
   from veadk import Agent, Runner  # Import VeADK's core classes for defining agents and the runner.
   from veadk.knowledgebase import KnowledgeBase  # Import the knowledge base component for storing and retrieving documentation knowledge
   from veadk.memory import LongTermMemory, ShortTermMemory  # Import the memory component
   from veadk.tools.builtin_tools.run_code import run_code  # Import the code sandbox template.
   from veadk.tools.builtin_tools.mcp_router import mcp_router  # Import the MCP toolset.
   from google.adk.agents.callback_context import CallbackContext # Import Google ADK's callback context class, used to get the current session and write it to long-term memory in after_agent_callback.
   from dotenv import load_dotenv
   
   load_dotenv()
   
   memory_name = os.getenv("DATABASE_VIKINGMEM_COLLECTION")
   if not memory_name:
       raise ValueError("DATABASE_VIKINGMEM_COLLECTION environment variable is not set")
   
   # Use Viking as the long-term memory.
   long_term_memory = LongTermMemory(backend="viking", index=memory_name)
   
   # Use local memory as short-term memory. If persistence is needed, the backend can be configured as MySQL, which requires creating a database on BytePlus in advance.
   short_term_memory = ShortTermMemory(backend="local")
   
   knowledge_name = os.getenv("DATABASE_VIKING_COLLECTION")
   if not knowledge_name:
       raise ValueError("DATABASE_VIKING_COLLECTION environment variable is not set")
   
   # Use Viking as the knowledge base store.
   knowledgebase = KnowledgeBase(backend="viking", index=knowledge_name)
   
   # Define an async callback function to obtain the current session and add it to long-term memory storage after agent execution
   async def after_agent_execution(callback_context: CallbackContext):
       session = callback_context._invocation_context.session
       await long_term_memory.add_session_to_memory(session)
   
   # Define the personal assistant agent.
   personal_assistant = Agent(
       name="personal_assistant",
       description="A personal assistant agent that can help users manage daily affairs and provide information.",
       instruction="""
   You are a user-friendly personal assistant agent. Please answer user questions in concise and clear language.
   If the user asks for information related to the knowledge base, please use the knowledge base for retrieval.
   If the user mentions personal preferences or important information, please store it in the long-term memory.
   If the user wants to perform code generation tasks, please use the code sandbox tool.
   If the user wants to perform other tasks, please select an appropriate MCP tool.""",
       short_term_memory=short_term_memory,
          long_term_memory=long_term_memory, 
            knowledgebase=knowledgebase,
       tools=[run_code, mcp_router],
       after_agent_callback=after_agent_execution,
   )
   
   # Use VeADK Web for testing.
   root_agent = personal_assistant
   
   async def main():
       """Main function to run the personal assistant agent"""
       print("Welcome to the personal assistant agent!")
       print("Enter 'exit' or 'quit' to exit the program.")
       print("=" * 50)
       
       # Create the agent runner
       runner = Runner(
           agent=personal_assistant,
           app_name="personal_assistant_demo",
           user_id="demo_user",
           short_term_memory=short_term_memory
       )
   
       while True:
           user_input = input("Enter your question: ")
           
           if user_input.lower() in ["exit", "quit", "terminate"]:
               print("Goodbye!")
               break
           
           try:
               # Run the agent and get the response.
               response = await runner.run(messages=user_input)
               print(f"Assistant: {response}")
           except Exception as e:
               print(f"An error occurred: {e}")
           
           print("=" * 50)
   
   if __name__ == "__main__":
       asyncio.run(main())
   ```
   

4. Press the `esc` key to exit edit mode, and enter `:wq` to save and exit the file.


<span id="XPOXVuX4"></span>
### Step 3: Create components and obtain **environment variables**

<span id="QqrMogiY"></span>
#### **Core components**


|**Component** |Description |
|---|---|
|Agent service |`agent.py` \- The main application, used to define the agent, memory, knowledge base, and tool components. |
|Short\-term memory |Uses local memory to store session context. |
|Long\-term memory |Uses Viking memory from AgentKit to support cross\-session memory storage and retrieval. |
|Knowledge Base |Uses the AgentKit knowledge base as a personal knowledge base, supporting custom file uploads. |
|Sandbox templates |Use the AgentKit sandbox template AIO Sandbox as the execution tool for code tasks. |
|MCP toolset |Uses the AgentKit MCP toolset to customize MCP tools. |
|Environment variable configuration |Environment variables are maintained in the` .env` file. |


<span id="iAHng3L7"></span>
#### Obtain environment variables


* **Tool**

   In the above [agent code](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial#sQvVjOHv), the `run_code` module capability is used for code execution. This module corresponds to the AgentKit sandbox template component. You need to create the corresponding component in advance and obtain the environment variables.

   1. [Create a tool](https://docs.byteplus.com/en/docs/agentkit/Creating_tools).

   2. Obtain environment variables: After creation, navigate to the "Integration code" tab on the tool details page to get the required environment variables of the tool.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d65ad723b913cffe0a4f1f27091f351.png) </span>

* **Memory**

   In the above [agent code](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial#sQvVjOHv), the LongTermMemory module capability is used for storing and retrieving cross\-session memory. This module corresponds to the AgentKit memory component. You need to create this component in advance and obtain its environment variables.

   1. [import an existing Viking memory](https://docs.byteplus.com/en/docs/agentkit/Importing_memories).

   2. Obtain environment variables: On the target memory details page, navigate to the "Integration code" tab to get the required memory environment variables.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36b5fcb9cba01cfdaa402bbf3005cdbb.png) </span>

* **Knowledge Base**

   In the above [agent code](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial#sQvVjOHv), the Knowledge module capability is used for storing and retrieving knowledge. This module corresponds to the AgentKit knowledge base component. You need to create this component in advance and obtain its environment variables.

   1. [Create a knowledge base](https://docs.byteplus.com/en/docs/RAG_Cloud/Create_a_knowledge_base): Create a Viking knowledge base in the vector database and upload files (you can upload materials such as news articles or personal notes as needed, to facilitate testing the agent's features described above).

   2. [Import the knowledge base](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases): Import the newly created knowledge base.

   3. Obtain environment variables: After creation, click the knowledge base name to enter its details page, select "Integration code", and obtain the required environment variables of the knowledge base.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f660a6a78d403442a27347924f1e6d1.png) </span>

* **MCP toolset**

   In the above [agent code](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial#sQvVjOHv), the `mcp_router` module capability is used for automatically matching and invoking the most relevant tools for the intent through semantic search. This module corresponds to the AgentKit MCP toolset component. You need to create this component in advance and obtain its environment variables.

   1. [Create MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services): Create or import MCP tools as needed (for example, Sequential Thinking MCP and Map MCP).

   2. [Create MCP toolsets](https://docs.byteplus.com/en/docs/agentkit/MCP_toolset?lang=en): Select the MCP services to mount to the MCP toolset.

   3. Obtain environment variables: On the MCP toolset details page, obtain the access domain name URL and the API Key for inbound identity authentication.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_183ddfc7de0f5072b899539b3751e05e.png) </span>


<span id="7AMhwpyV"></span>
### Step 4: Configure environment variables

<span id="aOWnfyxj"></span>
#### **Introduction to environment variables**


|**VeADK module name** |**Corresponding AgentKit component** |**Corresponding environment variables** |
|---|---|---|
|run_code |Sandbox template—AIO Sandbox |```Bash```<br>```AGENTKIT_TOOL_ID=xxx # Sandbox template ID.```<br>```AGENTKIT_TOOL_REGION=xxx # Optional. Defaults to the Asia Pacific (Johor) region (ap-southeast-1).```<br><br><br> |
|KnowledgeBase |Knowledge base—Viking |```Bash```<br>```DATABASE_VIKING_COLLECTION=xxx # Knowledge base name.```<br>```DATABASE_VIKING_PROJECT=xxx # Optional and defaults to the default project.```<br>```DATABASE_VIKING_BASE_URL="<PrivateLink URL for VPC access only, possibly starts with http://>" # Private network access domain name. This is required only when private network access is configured.```<br> |
|LongTermMemory |Memory—Viking |```Bash```<br>```DATABASE_VIKINGMEM_COLLECTION=xxx # Memory name.```<br>```DATABASE_VIKINGMEM_MEMORY_TYPE=xxx # Configured memory strategy. Separate multiple strategies with commas.```<br>```DATABASE_VIKINGMEM_BASE_URL="<PrivateLink URL for VPC access only, possibly starts with http://>" #Private network access domain name. This is required only when private network access is cojifgured.```<br>```DATABASE_VIKINGMEM_PROJECT="default" # Optional and defaults to the default project.```<br> |
|mcp_router |MCP toolset |```Bash```<br>```TOOL_MCP_ROUTER_URL=https://sd598mk9acju1mtc7****.apigateway-southeast-1.volceapi.com/mcp # Access domain name URL of the MCP toolset.```<br>```TOOL_MCP_ROUTER_API_KEY=xxx # API Key for MCP toolset inbound identity authentication.```<br> |


<span id="siHUF7e0"></span>
#### **Environment variable configuration**


* **Set environment variables in the local environment**

   Execute the following command in your local terminal to set environment variables.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Since AK/SK are highly sensitive credentials, directly writing them into static configuration files, such as <code>.env</code>, poses a security risk. When you configure BytePlus AK/SK in the local development environment, we recommend managing them by exporting session\-level environment variables in the terminal.   </div>
   

   ```Bash
   export BYTEPLUS_ACCESS_KEY=<your_access_key>
   export BYTEPLUS_SECRET_KEY=<your_secret_key>
   ```
   



&nbsp;

* **Configure other environment variables in **  **`.env`**

   1. In the virtual environment where the agent was created, execute the following command to enter the project root directory.

      ```Bash
      cd <Project directory>
      ```
      

   2. Execute the following command to open the `.env` file.

      ```Bash
      vim .env
      ```
      

   3. Press `I` to enter edit mode and fill in the environment variables required for agent configuration.

      ```Bash
      AGENTKIT_TOOL_ID=t-xxx # Sandbox template ID.
      AGENTKIT_TOOL_REGION=xxx # Optional. Defaults to the Asia Pacific (Johor) region (ap-southeast-1).
      DATABASE_VIKINGMEM_COLLECTION=memory_xx # Viking memory name
      DATABASE_VIKINGMEM_MEMORY_TYPE=memory_summary_xxx # Viking memory strategy
      DATABASE_VIKING_COLLECTION=xxx # Viking knowledge base name
      TOOL_MCP_ROUTER_URL=https://sd55xxxx.apigateway-ap-southeast-1.apigw-byteplus.com/mcp # Access domain name URL of the MCP toolset
      TOOL_MCP_ROUTER_API_KEY=1OtLoGxxxx # API Key for MCP toolset inbound identity authentication
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4919bddf69660dfb5a289f980a0d1023.png) </span>

   4. Press the `esc` key to exit edit mode, and enter `:wq` to save and exit the file.


<span id="Dw4BCqrx"></span>
### Step 5: Local test

<span id="l87vNJz5"></span>
#### Use the VeADK Web test interface


1. Return to the parent directory of the project directory.

   ```Bash
   cd ..
   ```
   

2.  **(Optional)**  If you have exited the virtual environment, execute the following command to reactivate it. Otherwise, skip this step.

   ```Bash
   source .venv/bin/activate
   ```
   

3. Start the VeADK Web interface.

   ```Bash
   veadk web
   ```
   

   When the following output is displayed, it indicates that the VeADK Web interface has started successfully. Follow the on\-screen prompt to get the link for accessing the Web interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eec7be9667aac95a5b45ff37332ab9e1.png) </span>

4. In a local browser on the machine where your project is running, open the VeADK Web interface URL obtained in the previous step. This topic uses `http://127.0.0.1:8000` as an example.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06e7ba694cbb7cb8b5ee5547b0e7c402.png) </span>

5. After entering the page, verify in the following order:

   1. In the drop\-down list on the left, select the target agent (that is, the project name, for example, `personal_assistant`).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_680736934098bf9ea308112c9d75d28e.png) </span>

   2. Send a message in the chat box at the bottom, for example, "Introduce yourself".

   3. Confirm that the target agent can respond normally.


<span id="4uObFtOH"></span>
## Deploy the agent

After a successful local test, you can use the CLI tool provided by AgentKit to deploy the agent to the cloud quickly.

<span id="MNvH5hgx"></span>
### **Step 1: Initialize the project to be deployed**


1.  **(Optional)**  If you have exited the virtual environment, execute the following command to reactivate it. Otherwise, skip this step.

   ```Bash
   source .venv/bin/activate
   ```
   

2. Execute the following command to enter the project root directory.

   ```Bash
   cd <Project directory>
   ```
   

3. Execute the following command to initialize the agent application.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>agent.py</code> with the name of your agent's definition file. <a href="https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial#wzlSH6nR">Learn more</a>   </div>
   

   ```Bash
   agentkit init --from-agent ./agent.py
   ```
   

   Initialization causes the following files to be automatically generated:

   * **agentkit\-agent.py**: The entry file for the agent application. It enables your agent to be automatically wrapped into an HTTP service compliant with the AgentKit standard. The default framework is AgentkitSimpleApp. Refer to [SDK overview](https://docs.byteplus.com/en/docs/agentkit/SDK_overview) to use other frameworks.

   * **requirements.txt**: The Python dependencies.

   * **agentkit.yaml**: The configuration file.

   *  **.dockerignore**: The files or directories to be ignored during Docker image building.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15148cbc8c7502e3f59826a4560722c7.png) </span>


<span id="KmvDXr8r"></span>
### **Step 2: Publish the ** agent


1.  **(Optional)**  If you have exited the virtual environment, execute the following command to reactivate it. Otherwise, skip this step.

   ```Bash
   source .venv/bin/activate
   ```
   

2. Execute the following command to enter the project root directory.

   ```Bash
   cd <Project directory>
   ```
   

3. Execute the following command to publish the agent.

   ```Bash
   agentkit launch
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The initial deployment takes approximately 2–3 minutes. Please wait for the operation to complete.   </div>
   

   When the following output is displayed, it indicates that the local agent has been successfully published as an AgentKit agent runtime.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ce8dd111871c4c56fff47df6f0fc04e.png) </span>

4. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). You can view the deployed agent runtime instances and their detailed information.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fbaba7866cefc97c06fce25e2712555.png) </span>


<span id="7QvJIdtN"></span>
## Testing the agent online

After the agent is published, you can go to the agent runtime console to test the agent online.


1. Log in the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Basic components \> Agent Runtime".

3. Click the "Online test" button in the "Actions" column to the right of the target agent.

4. In the **Body type** section, select **raw** and enter the test parameters (in this topic, the prompt changes to "Introduce yourself and tell me which MCP tools you have available"). Click the "Test" button to send a POST request. For more details on test parameters, see [Calling agent](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts).

5. In the **Test result** section, confirm that the status code is **200** and verify that the returned content matches your expectations.


   &nbsp;

<span id="VkrlZtym"></span>
## What to do next

After the agent is launched, you can also update its instance specifications, custom image, model, environment variables, and other configurations at any time in the console. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After updating the agent runtime configuration, you need to republish it for the new configuration to take effect. <a href="https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes">Learn more</a></div>
