---
title: "Application overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Overview_of_the_Application_center"
---

The application manages function instances, triggers, and other dependent cloud resources in an aggregated manner, helping you deploy Serverless applications with one click and achieve full lifecycle management of applications. This article introduces the concepts and advantages of the Application Center.

<span id=".5Z-65pys5qaC5b-1"></span>
## Glossary

An application is a concept at a higher level than a function. A Serverless application consists of functions, triggers, and the various cloud resources involved in your business, which work together to implement end\-to\-end business logic.

The Application Center is a full lifecycle management platform for Serverless applications. At the application level, it aggregates the management of function instances, triggers, and other dependent cloud resources, helping you orchestrate and deploy applications with one click. This further lowers the barrier to using Serverless applications and improves productivity.

<span id=".5LyY5Yq_"></span>
## Advantages


* **Experience a wide range of agent applications with one click**

   veFaaS provides an **App plaza** where agent applications built on large models are available. In the **App plaza**, you can try, for free and with one click, the applications that veFaaS has curated and published, and then further develop and implement your own agent applications based on them.

   * [Computer Use Agent](https://docs.byteplus.com/en/docs/faas/Deploying_Computer_Use_Agent_application_with_one_click): A BytePlus agent service powered by the Doubao large model and designed for end users and AI application developers. The service provides built\-in, self\-developed, out\-of\-the\-box Computer Use capabilities driven by the MCP protocol, supporting mouse control, keyboard control, and screen capture on remote Windows and Linux virtual machines. It makes it easy to remotely control endpoints (computers) to perform tasks such as editing videos, creating presentations, and managing social media accounts.

   * [Coze Studio](https://docs.byteplus.com/en/docs/6662/1756919): The next\-generation AI agent development platform launched by ByteDance. By integrating plugins, workflows, cards, and other robust features, Coze Studio empowers you to rapidly build personalized or commercially viable agents with minimal technical barriers.

* **Simplified application deployment**

   veFaaS provides a rich set of application templates that cover a wide range of scenarios, including AI, web services, data and logs, image and document processing, and audio and video processing. By deploying applications from templates, you only need to adjust a few parameters to deploy an application with one click, without writing business code from scratch or performing extra operations such as building, packaging, and releasing, and without manually setting up a complex environment of upstream and downstream cloud resources. This greatly lowers the barrier to using Serverless applications and helps you get started with and experience Serverless applications more easily, conveniently, and quickly.

* **Truly focus on businesses**

   veFaaS aggregates the management of functions, triggers, storage instances, and other dependent cloud resources at the application level, allowing you to manage Serverless applications from a holistic perspective instead of managing functions and resources scattered across different product pages. This helps developers truly focus on their business and applications.


<span id="Q7r147z8"></span>
## Procedure

The typical procedure for using an application is as follows:


1. [Create and deploy an application](https://docs.byteplus.com/en/docs/faas/Manage_applications?lang=en): Create and deploy an application by using an application template, code repository, or code package. The deployed application can be accessed via the built\-in APIG public URL of the application.

2. [Manage the application](https://docs.byteplus.com/en/docs/faas/Manage_applications?lang=en): View the details, logs, and associated cloud resources of the application in the application center, and perform full\-lifecycle management such as update, start/stop, and delete.


<span id="dyDGnQBr"></span>
## Core scenarios and recommended templates

The App plaza provides various application templates. The following table lists some popular templates by core scenario. For more templates, go to the [App plaza](https://console.byteplus.com/vefaas/market) to view the templates and deploy them with a few clicks.


|**Core scenario** |**Popular template** |
|---|---|
|AI agent/agent |[Computer Use Agent](https://docs.byteplus.com/en/docs/faas/Deploying_Computer_Use_Agent_application_with_one_click), [Coze Studio](https://docs.byteplus.com/en/docs/6662/1756919), and other LLM agent application templates. |
|Agent runtime environment |MCP Server templates that provide tools and runtime environments for agents. |
|Web development framework |Standard web app templates based on frameworks such as Next.js and FastAPI. |
