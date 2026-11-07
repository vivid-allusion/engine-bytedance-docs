---
title: "Integrating knowledge bases into agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent"
---

After importing a knowledge base, you can call an API in the agent code to integrate knowledge base capabilities. This enables maintainable, updatable, traceable, and low\-cost agents. This topic describes how to quickly integrate a knowledge base into an agent built with [VeADK](https://deepwiki.com/volcengine/veadk-python/1-overview).

<span id="BmA4oXOT"></span>
## Prerequisites


* [The knowledge base has been imported](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases).

* An Agent has been built with [VeADK](https://deepwiki.com/volcengine/veadk-python/1-overview). For information about how to build an agent, see [Advanced quick start​: Developing and deploying agents](https://docs.byteplus.com/en/docs/agentkit/Developing_and_deploying_agents).

* The corresponding credentials have been prepared based on your chosen authentication method (choose one):

   > API Key provides finer permission granularity and can be bound to a specific resource on a one\-to\-one basis, making it suitable for precise access control based on the principle of least privilege. AK/SK provides a broader permission scope and is managed uniformly through IAM policies, making it suitable for scenarios that require cross\-resource or cross\-service calls.   
   

   * **AK/SK authentication**: You have logged in to the platform console and [obtained the AK/SK](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). You can create and obtain an **Access Key ID** and **Secret Access Key** on the [Access Key Management](https://console.byteplus.com/iam/keymanage/) page.

   * **API Key authentication**: You have [obtained the API Key for the knowledge base](https://docs.byteplus.com/en/docs/agentkit/Accessing-Viking-knowledge-bases-by-using-API-Key-authentication).


<span id="6rnwbdEu"></span>
## Procedure

<span id="gibcvAFR"></span>
### (Optional) Step 1: Configure environment variables

When integrating the knowledge base into the agent, you can configure the knowledge base environment variables using either of the following two methods.


* Method 1: Associate the knowledge base in the agent runtime. Refer to [Update associated knowledge base](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_configuration).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are using <strong>API Key authentication</strong>, you also need to add or update the <strong><code>DATABASE_VIKING_API_KEY</code></strong><strong> variable</strong> in the <strong>Environment variables</strong> section of the agent runtime's "Basic information" tab, and set its value to the API Key for the knowledge base.   </div>
   

* Method 2: After obtaining the environment variables, configure them in the code.

   1. Obtain environment variables.

      1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

      2. In the left\-side navigation pane, select "Knowledge Base".

   2. Configure environment variables for the knowledge base.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Both AK/SK and API Key authentication are supported. You only need to configure one. API Key provides finer permission granularity and can be bound to a specific resource on a one\-to\-one basis, making it suitable for precise access control based on the principle of least privilege. AK/SK provides a broader permission scope and is managed uniformly through IAM policies, making it suitable for scenarios that require cross\-resource or cross\-service calls.      </div>
      

      
      <Tabs>
      <Tab zoneid="uMSuCeatfN" title="AK/SK">
      <TabTitle>AK/SK</TabTitle>
      
      ```Bash
      export DATABASE_VIKING_COLLECTION=<collection_name> 
      export DATABASE_VIKING_PROJECT=default
      export DATABASE_VIKING_REGION=ap-southeast-1
      export BYTEPLUS_ACCESS_KEY=<your_access_key>
      export BYTEPLUS_SECRET_KEY=<your_secret_key>
      ```
      
      
      
      
      
      </Tab>
      <Tab zoneid="KaZiiV5SIw" title="API Key">
      <TabTitle>API Key</TabTitle>
      
      ```Bash
      export DATABASE_VIKING_COLLECTION=<collection_name> 
      export DATABASE_VIKING_PROJECT=default
      export DATABASE_VIKING_REGION=ap-southeast-1
      export DATABASE_VIKING_API_KEY =<APIKEY>
      ```
      
      
      
      
      
      </Tab>
      </Tabs>
      


<span id="2je9Lp3S"></span>
### Step 2: Integrate the knowledge base with VeADK


1. Install Python dependencies.

   > If the required Python dependencies are already installed in your local virtual environment, skip this step and proceed to the next.   
   

   ```Python
   pip install veadk-python
   ```
   

2. Integrate the knowledge base into the agent.

   ```Python
   # Refer to the following sample knowledge base integration code and modify the agent code
   import asyncio
   import os
   
   from veadk import Agent, Runner
   from veadk.knowledgebase import KnowledgeBase
   from veadk.memory.short_term_memory import ShortTermMemory
   
   collection_name = os.getenv("DATABASE_VIKING_COLLECTION")
   if not collection_name:
       raise ValueError("DATABASE_VIKING_COLLECTION environment variable is not set")
   
   # Add the following texts as an md file to the knowledge base corresponding to collection_name
   qa_text = """
   # Intelligent customer service knowledge base
   ## 1. Company profile
   VE Technology is a high-tech enterprise focusing on intelligent customer service and knowledge management. Our core product is the **intelligent customer service system**, which provides enterprise customers with efficient and intelligent automated customer service solutions through natural language processing and knowledge base retrieval.
   ## 2. Product feature description
   - **Automatic Q&A**：Quickly respond to common questions based on the knowledge base.
   - **Multi-channel access**：Supports web pages, apps, WeChat, Feishu, and other channels.
   - **Intelligent recommendation**：Recommend relevant answers based on context.
   - **Data analysis**：Provide user question statistics and customer service performance reports.
   - **Self-service knowledge base management**：Enable non-technical personnel to quickly edit knowledge content.
   ---
   ## 3. FAQ
   ### Q1: What languages does the intelligent customer service system support?
   A1: Currently, it supports **Chinese** and **English**, and multi-language support for Japanese, Korean, and others will be gradually added in the future.
   ### Q2: Can the system be connected to the existing CRM?
   A2: Yes. Our system supports seamless integration with mainstream CRM systems through APIs.
   ### Q3: What happens if the robot cannot answer a user's question?
   A3: The system will automatically transfer the question to human customer service and record the question in the background, making it convenient for administrators to add it to the knowledge base.
   ### Q4: How often is the knowledge base content updated?
   ## A4: The knowledge base supports **real-time updates**, which take effect immediately after submission by administrators.
   ## 4. Contact us
   - Official website: [https://www.example.com](https://www.example.com)
   - Customer service email: support@ve
   - Service hotline：400-123-4567
   """
   
   # Replace the values from your own user & session management system
   app_name = "app"
   user_id = "user"
   session_id = "session"
   
   knowledgebase = KnowledgeBase(backend="viking", index=collection_name)
   
   agent = Agent(
       name="customer_service",
       instruction="Answer customer's questions according to your knowledgebase.",
       knowledgebase=knowledgebase,
   )
   
   runner = Runner(
       agent=agent,
       short_term_memory=ShortTermMemory(),
       app_name=app_name,
       user_id=user_id,
   )
   
   response = asyncio.run(
       runner.run(messages="What is your product name, and what features does it have?", session_id=session_id)
   )
   
   print(response)
   ```
   


<span id="cjuVHbyn"></span>
## What to do next: Deploy to the cloud production environment

After completing local development and testing, you can deploy the agent with the integrated knowledge base to an agent runtime. Before deploying, make sure all dependencies are correctly configured in `requirements.txt`. The following two deployment methods are currently supported:


* **Custom image deployment**: Package the agent code and push it to Container Registry. Then, [update the agent runtime image version](https://aime.bytedance.net/assistant/task/%E9%93%BE%E6%8E%A5) in the console and republish the agent runtime to apply the changes.

* **AgentKit CLI deployment**: [Use the agentkit launch command‌](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool?lang=en#6OAaQbZI). The CLI automatically handles code packaging, image building, and deployment. The necessary environment information is automatically injected during deployment, so no manual configuration is required.
