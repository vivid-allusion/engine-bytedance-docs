---
title: "Accessing Viking knowledge bases by using API Key authentication"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Accessing-Viking-knowledge-bases-by-using-API-Key-authentication"
---

This topic describes how to enable an API Key for a Viking knowledge base and configure the credential as an environment variable in an agent runtime. The agent can then use the API Key to authenticate and access the knowledge base. Enabling an API Key does not affect AK/SK authentication.

<span id="UI5WOymQ"></span>
## Authentication methods

Both API Key and AK/SK authentication are supported. Configure either method.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If both AK/SK and API Key are configured, the system uses the API Key for authentication by default.</div>



|**Authentication method** |**Applicable scenario** |**Description** |
|---|---|---|
|**API Key** |Scenarios requiring fine\-grained access control |Provides finer permission granularity. An API Key can be bound to a specific knowledge base on a one\-to\-one basis, making it suitable for precise access control based on the principle of least privilege. |
|**AK/SK** |Scenarios requiring unified management of access to multiple resources |Provides a broader permission scope. Access is managed uniformly through IAM policies, making it suitable for scenarios that require cross\-resource or cross\-service calls. |


<span id="XZ8w8Qlr"></span>
## Prerequisites

The target [Viking knowledge base has been imported into AgentKit](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases), and the knowledge base is in the **Succeeded** state.

<span id="cx79T1po"></span>
## Enable an API Key


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Knowledge Base".

3. Click the name of the target knowledge base to open the details page of the knowledge base.

4. In the **Access control** section of the **Basic information** tab, click the "Enable API Key" button.

5. Wait for the system to generate a dedicated API Key for the current knowledge base.


<span id="tbsz6vTk"></span>
## Configure the API Key in an agent runtime

After you enable the API Key for the knowledge base, you can use it for authentication and knowledge base access. To do so, configure the credential as an environment variable in the agent runtime.

<span id="UUTnOLNP"></span>
### The agent has already been integrated with the knowledge base

Go to the agent runtime details page. In the **Environment variables** section of the **Basic information** tab, add or update **`DATABASE_VIKING_API_KEY`** and set its value to the API Key for the knowledge base. For more information, see [Updating environment variables](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_environment_variables).

<span id="7eh6jI9H"></span>
### The agent has not been integrated with the knowledge base


1. [Integrate the target knowledge base into the agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent).

2. [Deploy the agent to an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent?lang=en#cjuVHbyn).
