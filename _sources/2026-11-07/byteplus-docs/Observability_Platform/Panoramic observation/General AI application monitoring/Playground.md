---
title: "Playground"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Playground"
---

Playground is a feature of AI application monitoring that provides a web\-based interactive environment for debugging. In this environment, you can build multi\-turn conversations, adjust prompts, and simulate tool calls on a single page. By using this feature with ** LLM trace analysis**, you can reconstruct the context of abnormal calls. This allows you to complete the closed\-loop debugging workflow of "issue recurrence \-\> Prompt modification \-\> replay verification \-\> result comparison" without manually copying trace data or writing local debugging scripts. This improves the efficiency of locating and fixing agent issues. This topic describes how to use Playground.

<span id="hh87tioc"></span>
## Prerequisites

AI\-related applications have been integrated with Server\-side Monitoring and are reporting observability data normally. For details, see [AI scenario monitoring overview](https://docs.byteplus.com/en/docs/apmplus/Overview_of_AI_scenario_monitoring).

<span id="vpLqEdne"></span>
## Applicable scenario


* Online bad case review: You can reconstruct abnormal call scenarios based on **LLM trace analysis**, modify prompts or parameters, rerun, and verify the fix.

* Prompt optimization: You can compare different versions of prompt configurations across multiple windows to evaluate output stability and alignment with business requirements.

* Model selection: You can test multiple models side by side under the same input conditions and compare output quality to support model selection decisions.

* Parameter optimization: You can adjust `temperature`, `max_tokens`, `top_p`, and other parameters to find the optimal combination for the current scenario.

* Tool call debugging: You can configure Tools definitions and construct input messages to verify whether the model's tool selection, parameter filling, and result processing meet expectations.

* Structured output verification: You can configure Schema constraints to verify whether the model output consistently meets the format requirements of downstream systems.

* Offline validation of Agent tool orchestration: Before integrating the service into production, you can configure Tools definitions to verify the clarity of tool descriptions, the model's tool selection logic, and whether multi\-turn tool call orchestration meets expectations.


<span id="kXlCmoXJ"></span>
## Usage Process

<span id="71wmUZtz"></span>
### Step 1: Integrate a large model


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation pane, select **Playground**.

3. Click **Model connection management** \> **Add model connection** and configure the following parameters.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can associate multiple models with one model connection. After configuration is complete, the settings remain valid long\-term within the current workspace, and you do not need to configure the model connection again.   </div>
   

   
   |Parameters |Description |
   |---|---|
   |Connection name |The name of the model connection. |
   |Type |The interface protocol type. Currently, the OpenAI\-compatible protocol is supported. |
   |Integration address |The Base URL of the model service, for example, https://api.example.com. |
   |API KEY |The authentication key for the model service. |
   |Model list |The list of model names that can be called through this model connection. You can click **Auto fetch** to pull from the integration address, or click  **+ Add** to enter manually. After configuration, click **Test** to verify connectivity to the target model, or click **Test all** for batch verification. |
   


<span id="xRadZ9QW"></span>
### Step 2: Run a conversation


1. In the model drop\-down box at the top of the window, select the target model.

2. In the **INPUT** area, select a message role and enter the content in the input box. The supported message roles are as follows:

   
   |Message role |Description |
   |---|---|
   |User |User questions that express needs and specific problems. |
   |Assistant |The previous responses of the model. |
   |System |System instructions that define the identity, tasks, and overall constraints of the model. |
   |Developer |Developer instructions that supplement implementation\-oriented or more fine\-grained control requirements. |
   |Tool |The tool response. |
   

3. To build a multi\-turn conversation, click  **+ Add message**. You can also click the action buttons on the right side of the message row to copy or delete a message.

4. Click **Run** in the ** OUTPUT ** window. The model output is displayed in a streaming manner and can be copied with one click.


<span id="b0OCR6wc"></span>
## Other operations

<span id="uICSpMGw"></span>
### Multi\-window comparison

When you need to compare differences in results across models, parameters, or prompts, you can use the multi\-window side\-by\-side comparison feature. This feature allows you to place multiple debugging windows in the same view and run them at the same time.


1. Click  **+ Add comparison window** to create a new comparison window. You can open up to three comparison windows at the same time.

2. In each window, configure the model, parameters, and debugging options.

3. Click **Run all ** in the upper\-right corner of the page, or click ** Run ** in each **OUTPUT ** window separately.

4. In the **OUTPUT ** area of each window, compare the differences in outputs.


<span id="NeLF9N7u"></span>
### Configure model parameters

When you need to adjust the generation behavior of a model, click the model parameter configuration icon on the right of the model selection area to configure the following model parameters.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following parameters are disabled by default. When they are disabled, the model runs based on the default value of each parameter. After you enable a parameter, the model runs based on the value that you configure.</div>



|Model parameter |Description |
|---|---|
|Max output length |Limits the number of tokens in the model output. |
|Generation randomness |Controls the randomness of the output. The higher the value, the more divergent the results; the lower the value, the more stable and convergent the results. |
|Advanced options |Specifies other parameters supported by the model in JSON format. For example, `top_p `and `frequency_penalty`. |


<span id="U4E9AitB"></span>
### Configure debugging options

When you need to simulate tool calls, constrain the format of the model output, or reuse prompt variables, you can configure the following debugging options on the page.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">In the same conversation, Tools and Schema cannot be enabled at the same time.</div>


* <div data-tips="true" data-tips-type="default">You can enable multiple Tools at the same time, but only one Schema at a time.</div>


* Tools: On the **Tools** tab, click  **+ Create Tools** to add a new tool definition. You can enable a created tool from ** Unused tools** to **Used in this chat**, which enables the model to call the tool during this debugging run. If a tool call is triggered during the run, the result of the tool execution is written to the message list as a message with the Tool role.

* Schema: On the **Schema** tab, click  **+ Create Schema** to add a new structure definition. You can enable a created Schema from **Unused Schema** to ** Used in this chat**. At runtime, the model generates output according to the Schema constraint.

* Variables: When you need to reuse replaceable content in a prompt, you can use variables. You can use placeholder syntax in the message content to reference variables, for example,` {{NAME}}`. At runtime, the system replaces the placeholder with the variable value defined in **Variables**.
