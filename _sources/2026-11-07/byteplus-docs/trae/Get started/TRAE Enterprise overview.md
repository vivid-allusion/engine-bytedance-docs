---
title: "TRAE Enterprise overview"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/trae-enterprise-overview"
---

TRAE Enterprise is an AI coding and R&D collaboration platform designed for enterprises. On one hand, enterprise members can use core AI coding features such as AI chat, code completion, and agents in various TRAE Enterprise clients to assist with daily development tasks such as code writing, troubleshooting, and code comprehension; on the other hand, enterprise administrators can centrally manage members, seats, usage, data, and security policies through the console, enabling the unified application, monitoring, and governance of AI coding features within the enterprise.

<span id="f4609670"></span>
## TRAE Enterprise plan

TRAE Enterprise offers the Teams plan. It includes core features such as AI coding, enterprise document sets, enterprise agents, SSO login, member management, data dashboards, usage control, and audit logs.

<span id="55db5546"></span>
## Available products

TRAE Enterprise provides two products, TRAE IDE and TRAE Plugin, to accommodate different user preferences:


|**Product Name** |**Description** |
|---|---|
|TRAE IDE |TRAE IDE is an integrated development environment deeply integrated with AI capabilities, providing a complete development experience from code writing and project understanding to debugging, running, and change management. It features built\-in IDE mode and SOLO mode: you can either exercise precise control over each step as with a traditional IDE, or allow the AI agent to autonomously plan and execute complex tasks in SOLO mode. |
|TRAE Plugin |TRAE Plugin integrates essential AI coding features, such as auto code completion, into the mainstream IDEs you are familiar with. It supports mainstream programming languages, provides suggestions for writing single lines of code or entire functions, and offers auxiliary features such as code explanation, code review, and bug fixing to help users improve development efficiency. |


<span id="ae2b23e7"></span>
## Enterprise management

Enterprise administrators can manage all core resources and settings of the enterprise through the console. The main modules include:


* **Member and seat management**

   Supports inviting members, adding members in bulk, removing members, and purchasing or unsubscribing seats.

* **Usage management**

   Supports viewing detailed usage for the entire enterprise and individual members, covering basic usage, excess usage, usage from resource packages, pay\-as\-you\-go usage, and more.

* **Data analysis**

   Provides multidimensional data insights, including the number of users and activity trends for each TRAE client, AI's code generation rate, LLM call distribution, programming language distribution, as well as rankings for MCP and enterprise agents.

* **Audit and logs**

   Supports querying administrator operation logs to facilitate internal audits and issue tracing for the enterprise.


<span id="5717c217"></span>
## Enterprise setup

Enterprise administrators can flexibly configure enterprise\-exclusive AI capabilities and security policies according to the enterprise's own development processes and security requirements:


* **Enterprise document sets**

   Supports creating an in\-house knowledge base for your enterprise by adding document sets, enabling development standards, technical documentation, and best practices to be consolidated as context that can be used in AI chats, ensuring that AI\-generated content complies with the requirements of your enterprise.

* **Enterprise agents**

   Supports creating enterprise\-exclusive AI agents and orchestrating their capabilities through prompts and toolsets. These agents are visible to all members and become reusable enterprise\-level AI assets.

* **Model settings**

   Supports unified management of TRAE built\-in models and enterprise built\-in models. TRAE built\-in models are provided by TRAE and are ready to use out of the box; enterprise built\-in models are configured and managed by your enterprise itself, making it possible to use AI capabilities while meeting in\-house requirements for model selection and data governance.

* **Security policies**

   Supports protecting code assets by prohibiting AI from accessing code repositories that contain sensitive information, core algorithms, or non\-open\-source projects.


<span id="ed55baed"></span>
## Privacy and security

TRAE is committed to safeguarding the privacy and data security of enterprise users through a comprehensive protection framework covering local data storage, access control, and regional deployment.


* **Local data storage**

   Code files remain stored on enterprise users' local devices by default. To enable indexing, certain files may be temporarily uploaded for vector computation. Once processing is complete, all plaintext data is permanently deleted.

* **Secure access control**

   TRAE employs strict access control policies and encrypted data transmission to prevent unauthorized access and minimize security risks.

* **Regional deployment**

   Enterprise data and service infrastructure are deployed and stored based on the account's geographic region. Data isolation mechanisms are implemented to support compliance with applicable local data protection and regulatory requirements.
