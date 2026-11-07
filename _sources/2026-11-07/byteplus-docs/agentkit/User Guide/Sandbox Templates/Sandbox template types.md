---
title: "Sandbox template types"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Tool_type"
---

You can use AgentKit preset templates, custom templates, and [VeADK](https://docs.veadk.xyz/productions/veadk/preview/en) built\-in templates to extend the capabilities of your agent.

## Template types

* **Sandbox templates**

   * **Preset templates**: Provide the ArkClaw Sandbox, Hermes Sandbox, AIO Sandbox, Skills Sandbox, and Code Sandbox preset templates.

      * **ArkClaw Sandbox**: Includes built\-in ArkClaw, targeting individual users and light office scenarios. Supports handling everyday tasks and lightweight office automation using natural language.

      * **Hermes Sandbox**: Includes a built\-in, continuously learning Hermes Agent. Supports long\-term memory, skill evolution, multi\-model switching, and complex task automation.

      * **AIO Sandbox**: An all\-in\-one runtime environment for AI agents. Includes Browser, Terminal, and Code runtime environments. Suitable for multi\-step, complex tasks, with automatic switching between runtime environments based on the task.

      * **Skills Sandbox**: An agent with built\-in common Skills and executable Skills. Using it will incur model call costs. If you need to use both the run_code and execute_skill capabilities built into VeADK, create a Skills Sandbox template.

      * **Code Sandbox**: Provides a preset code execution environment and supports code generation, project testing, dependency installation, script execution, and test verification. If you want to focus on code development tasks, create a Code Sandbox.

   * **Custom templates**: Supports deploying templates using a custom container image.

* **VeADK built\-in templates**: VeADK is integrated with various built\-in templates that require no additional deployment. You can quickly integrate them into your agent by referring to the call examples.

### Preset template overview

|**Template type** |**Core built\-in capability** |**Target user/scenario** |**Typical task** |
|---|---|---|---|
|ArkClaw Sandbox |Built\-in ArkClaw |Individual users and light office scenarios |Handling everyday tasks and lightweight office automation with natural language |
|Hermes Sandbox |Continuous memory + proactive learning + skill accumulation |Complex tasks requiring long\-term evolution |Multi\-turn conversations with long\-term memory, continuous capability accumulation, and complex decision\-making |
|AIO Sandbox |Browser + Terminal + Code in one environment, with automatic switching based on the task |Scenarios that are not fixed and require flexible switching |Mixed agent tasks with cross\-execution of browser, command, and code operations within the same instance |
|Skills Sandbox |Preset commonly used Skills with automatic selection and execution |Requires the skill orchestration capability. |Using both run_code and execute_skill from VeADK simultaneously, invoking preset Skills |
|Code Sandbox |Built\-in Codex CLI |Pure code development workflows |Code generation, project debugging, dependency installation, script execution, test validation, and engineering tasks |

### Preset template details

#### ArkClaw Sandbox

* **Built\-in capabilities**: Built\-in ArkClaw.

* **Applicable scenarios**: Targeting individual users and light office scenarios. Supports handling everyday tasks and lightweight office automation using natural language, such as schedule organization, document summarization, and simple queries.

* **Not applicable**: Heavy scenarios involving enterprise\-level security auditing, system integration, or extensive code development (consider OpenClaw or Code Sandbox instead).

#### Hermes Sandbox

* **Built\-in capabilities**: Built\-in Hermes, with support for persistent memory, proactive learning, and skill accumulation.

* **Applicable scenarios**: Tasks that require context to be retained across multiple turns and sessions, and complex task scenarios where the agent needs to continuously accumulate dedicated skills during use.

* **Not applicable**: One\-off, simple tasks that do not require long\-term memory (consider ArkClaw Sandbox or AIO Sandbox instead).

#### AIO Sandbox

* **Built\-in capabilities**: AIO Sandbox (an all\-in\-one template set) includes three built\-in runtime environments: Browser, Terminal, and Code, with automatic switching based on the task.

* **Applicable scenarios**: Mixed tasks where the scenario is not fixed and you need to cross\-invoke browser, command\-line, and code execution capabilities within the same instance.

* **Not applicable**: Tasks that only require a single capability (for example, code development only); consider the more focused Code Sandbox instead.

#### Skills Sandbox

* **Built\-in capabilities**: Includes commonly used Skills with automatic selection and execution based on the task.

* **Applicable scenarios**: Scenarios where you want to use both the run_code and execute_skill capabilities built into VeADK simultaneously, or where you want to reuse platform preset Skills.

* **Not applicable**: Tasks that only need a basic runtime environment and do not involve skill orchestration (consider AIO Sandbox or Code Sandbox instead).

#### Code Sandbox

* **Built\-in capabilities**: Built\-in Codex CLI. It is suitable for scenarios such as code generation, project debugging, dependency installation, script execution, test validation, and engineering tasks.

* **Applicable scenarios**: Tasks that focus entirely on the code development workflow, with no need for browser interaction or complex skill orchestration.

* **Not applicable**: Tasks that require browser interaction, complex skill orchestration, or enterprise\-level system integration.

## Preset Skills list

|**skills** |**Description** |
|---|---|
|tos\-file\-access |Supports uploading files or directories to BytePlus TOS, or downloading files from URLs. Applicable scenarios include:<br><br><br>* Agent\-generated file or directory sharing (videos, images, reports, output folders) via TOS<br><br>* File downloading from URLs before agent processing |
|code\-optimization |Supports optimizing code performance through iterative improvements (up to 2 rounds). It also supports benchmarking execution time and memory usage, comparing against a baseline implementation, and generating a detailed optimization report. Supports C++, Python, Java, Rust, and more. |
|veadk\-python |Supports implementing a runnable agent based on the VeADK framework. |
|internal\-comms |An enterprise internal communication template. Used to draft formal emails, company\-wide announcements, weekly report summaries, and meeting notices, adaptable to different workplace scenarios. |
|skill\-creator |A skill generation template that assists in defining new agent skills. Supports automatically generating skill descriptions, JSON Schema parameter definitions, and Mock test data. |

## VeADK built\-in templates

|Built\-in template |Description |
|---|---|
|image_generate |An image generation template that can generate images based on your input text prompts. |
|image_edit |An image editing template that can generate modified images based on your input reference images and text prompts. |
|video_generate |A video generation template that can generate videos based on your input images and text information. |
