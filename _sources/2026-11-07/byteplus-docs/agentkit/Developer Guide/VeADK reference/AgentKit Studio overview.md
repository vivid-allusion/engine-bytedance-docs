---
title: "AgentKit Studio overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/agentkit-studio-overview"
---

## Introduction to AgentKit Studio

AgentKit Studio is a visual workspace provided by VeADK. It supports creating, testing, deploying, and managing agents in a single interface. It is suited for teams that need to build agents quickly, collaborate on configuration, or manage agents centrally. Studio reduces onboarding and delivery costs through standardized configuration and publishing workflows. It also centralizes runtime versions, deployment status, and key operation entry points. This helps development teams publish, validate, and iterate on agents more efficiently. [Learn more](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio)

## Studio and agent lifecycle

Studio serves as the workspace for agent development, deployment, and iteration. It also aggregates observability and evaluation features during interactions.

* **Develop**: Supports creating or importing agent projects. Covers configuration of models, prompts, tools, memory, knowledge bases, and skills. Also provides multi\-agent topology orchestration.

* **Test**: Supports running and testing agents in a temporary process with conversation testing. You can also download a ZIP package for offline delivery or archiving.

* **Deploy**: Supports deploying projects to AgentKit. Runtime version information and deployment status are displayed centrally in the Studio workspace.

* **Evaluate/Optimize**: When you switch agents, Studio can automatically load the conversation list, agent information, capability configuration, and auto\-evaluation status. This helps you adjust and optimize based on the results.

* **Iterate**: Supports continuous version updates on the same runtime. You can also upgrade a deployed Studio when needed to get the latest features and fixes.

## Core component

Studio's key components and their responsibilities are as follows:

|Core component |Main responsibility |Key modules/capabilities |
|---|---|---|
|[Studio workspace](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio) |Provides an end\-to\-end visual entry point for development, testing, and management workflows. |Conversation and session history, workspace (projects/files), multi\-agent canvas, system status, and task prompts |
|[Agent management](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E5%88%9B%E5%BB%BA%E6%99%BA%E8%83%BD) |Handles creation, import, configuration, and cloud deployment of agent projects, and manages versions and iterations. |Agent creation/import/migration, model configuration, tool/skill integration, knowledge base and memory association, and deployment tasks and progress |
|[Persistent storage](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#studio-%E6%8C%81%E4%B9%85%E5%8C%96%E5%AD%98%E5%82%A8) |Provides persistent storage for materials and outputs. |Material and resource library, project version and output persistence, evaluation\-related data persistence |
|[Permissions and roles](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#studio-%E8%A7%92%E8%89%B2%E4%B8%8E-runtime-%E6%9D%83%E9%99%90) |Controls resource visibility and operation permissions for different users. |User group\-based role control, runtime management permission constraints |
|[Conversation call trace and issue feedback](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#对话调用链路与问题反馈)<br><br> |Provides trace viewing and issue reporting entries on the chat page for diagnosing single\-turn execution issues. |Tracing flame graph, trace query, and issue feedback |
|[Auto-evaluation and optimization feedback](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#自动评测与优化反馈) |Automatically evaluates the conversation quality of deployed runtimes and generates optimization suggestions based on evaluation results. |Good/Bad case evaluation sets and auto\-evaluation feedback loop |

## Procedure

The typical Studio workflow includes the following steps:

1. [Install Studio](https://docs.veadk.xyz/productions/veadk/preview/zh/get-started/installation): Install VeADK and its dependencies.

2. Start Studio:

   * [Local startup](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E6%9C%AC%E5%9C%B0%E5%90%AF%E5%8A%A8): This is suitable for first\-time users who want to open the workspace quickly and explore the core workflow.

   * [Cloud deployment](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E4%BA%91%E7%AB%AF%E9%83%A8%E7%BD%B2): This is suitable for teams that need multiple members to access Studio through a unified public address, reducing issues caused by local environment differences.

3. [Create an agent and deploy it as a runtime](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E5%88%9B%E5%BB%BA%E6%99%BA%E8%83%BD%E4%BD%93): Create or import a project in Studio. Configure the model, system prompt, tools/skills, knowledge base, and memory. Then deploy the agent to AgentKit to generate a runtime.

4. [Conversation call trace and issue feedback](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E5%AF%B9%E8%AF%9D%E8%B0%83%E7%94%A8%E9%93%BE%E8%B7%AF%E4%B8%8E%E9%97%AE%E9%A2%98%E5%8F%8D%E9%A6%88): Use the call trace view and issue feedback entry on the conversation page to diagnose single\-turn execution issues.

5. [Auto-evaluation and optimization feedback](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E8%87%AA%E5%8A%A8%E8%AF%84%E6%B5%8B%E4%B8%8E%E4%BC%98%E5%8C%96%E5%8F%8D%E9%A6%88): View auto\-evaluation status and results for the agent in the Studio workspace. Validate the outcome and optimize accordingly.

6. [Update a deployed runtime](https://docs.veadk.xyz/productions/veadk/preview/zh/components/frontend/studio#%E6%9B%B4%E6%96%B0%E5%B7%B2%E9%83%A8%E7%BD%B2%E7%9A%84%E6%99%BA%E8%83%BD%E4%BD%93): Update the agent configuration based on observability and evaluation results. Publish the updated configuration as a new version of the corresponding runtime.
