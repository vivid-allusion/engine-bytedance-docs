---
title: "Getting started: Deploy an agent in 1 minute"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit"
---

This topic uses the platform\-provided [VeADK](https://deepwiki.com/volcengine/veadk-python)\-based public agent image as a starting point to demonstrate the end\-to\-end process of creating, deploying, and calling an agent through the console, helping you get started with AgentKit quickly.

<span id="QZj0n3yL"></span>
## Prerequisites


* You have completed [account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The AgentKit service has been activated. To activate AgentKit, log in to[ the AgentKit console](https://console.byteplus.com/AgentKit)follow the system prompts to complete the operations.

   > The first time you log in to the AgentKit console, the platform will automatically select the dependent products required to use AgentKit basic features (such as veFaaS, API Gateway, and Container Registry). You can also select other products based on your needs. Then, click the "Batch activate and authorize" button to confirm the "Activation and cross\-service authorization of AgentKit dependent services", allowing AgentKit to access the selected products.   
   

* [ModelArk has been activated](https://console.byteplus.com/ark/openManagement).


<span id="yTTxxUto"></span>
## Step 1: Create agent runtime


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic components \> Agent Runtime".

3. Click "Create agent" and configure the agent runtime information. Retain the default settings for parameters not mentioned.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more parameter descriptions, refer to <a href="https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console">Creating agent runtime</a>.   </div>
   

   
   |Parameter​ |Description |
   |---|---|
   |Name |Specify the agent runtime name. For example, agentkit_runtime. |
   |Image |Select "Financial analysis agent" under "Public image". |
   |Network access |Configure the network access method of the agent runtime. Public images only support the "Public network" option. |
   |IAM role |Select "Create role". This allows the platform to automatically grant permission to access resources of other BytePlus cloud services. |
   |Inbound identity authentication |Configure the identity authentication method for accessing agent runtime\-managed resources (**API Key** or **OAuth JWT**). In this example, "API Key" is selected.<br><br><br>* **API Key**: Automatically created and associated by the platform, which is applicable to server\-side calls, quick verification, and testing.<br><br>* **OAuth JWT**: Requests an access token based on OAuth, which is applicable to scenarios requiring higher security and a unified identity system. A user pool and client are required before configuration.<br><br>   > For debugging with the **online test** feature on the console, the OAuth JWT client is required to be the **M2M** type. |
   |Observability service |Select "Enable" to enable the observability service.<br><br>> After observability is enabled, integrated observability services such as metrics, traces, and logs will be provided, and an observability dashboard will be generated. The platform will also activate APMPlus and TLS services, and authorize the APMPlus service to write logs. |
   |Model selection |Use the default model "doubao\-seed\-1\-8". |
   |Associated project |Select "default (default project)". |
   

4. Click "Create".

5. In the pop\-up window, carefully read the fee information for creating an agent. After confirming the information is correct, click the "I know it and confirm the creation" button to complete the operation.


<span id="42HbZAwJ"></span>
## Step 2: Test agent


1. After the agent is released, in the agent runtime list, click the "Online test" button in the "Actions" column of the created agent runtime.

2. In the agent online test panel, the agent's domain name is automatically populated, so you do not need to enter it manually. On the **Body** tab, select **raw (JSON)** , enter test parameters (this example keeps the default configuration), and click the "Test" button to initiate a POST request. For detailed parameter descriptions, refer to [Calling agent](https://docs.byteplus.com/en/docs/agentkit/Sample_calls_for_text_prompts).

3. View the test result, confirm that the status code is **200**, and verify that the returned content meets expectations.


<span id="dyUaLB3w"></span>
## Step 3: Observe and evaluate the agent

After a successful test, you can further use observability and evaluation capabilities to continuously monitor the agent's operation and assess its performance in terms of effectiveness, performance, and cost. This helps achieve the gradual progression from "stable and usable" to "good enough to be worth releasing".

<span id="L7tNTugO"></span>
### Observe the agent

Agent operation typically involves stages such as model calls, tool execution, memory retrieval, and knowledge base retrieval. Once observability is enabled, AgentKit and the VeADK SDK automatically collect traces (call chains) and metrics for each stage based on OpenTelemetry and deliver the data to the observability platform.

On the "**Observability**" page, you can view runtime monitoring (such as request volume, latency, and error rate), trace analysis (the complete call chain), session analysis, model monitoring (such as token consumption), and log analysis. Observability data is also a prerequisite for subsequent evaluation. For details, refer to [Observability](https://docs.byteplus.com/en/docs/agentkit/Observability-).

<span id="cmvCapaT"></span>
### Evaluate the agent

Evaluation measures the agent's performance across the three dimensions of effectiveness, performance, and cost in a structured manner, providing a basis for release decisions and iterations.

The evaluation mechanism typically consists of three parts: evaluation sets, evaluators, and experiments. Evaluation sets provide standardized inputs and reference answers. Evaluators score results based on predefined rules using either an LLM or code. Experiments are responsible for combined execution and aggregating result metrics, while also supporting comparative analysis across multiple experiments. For details, refer to [Evaluation](https://docs.byteplus.com/en/docs/agentkit/Evaluation).

<span id="WVhJ87OE"></span>
## What to do next

After the agent is released, you can update configurations in the console as needed, including observability, custom images, instance specifications, models, environment variables, and associated components. After you complete the modifications, release the agent again for the new version to take effect. Both full release and canary release are supported for agent release. You can view progress, adjust traffic ratios, cancel the release, or roll back versions in **Version management \> Release history**. For details, see [Updating runtimes](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime).
