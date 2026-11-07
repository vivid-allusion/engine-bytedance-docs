---
title: "Selection guide"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Selection_guide"
---

veFaaS is an event\-driven, fully managed serverless compute platform. Based on a unified compute foundation, veFaaS provides three core product patterns—**Application**, **Function**, and **Cloud Sandbox**—to meet the needs of scenarios ranging from lightweight tasks to complex AI applications. Understanding the differences and connections among these three patterns is key to efficiently leveraging serverless architecture and accelerating business innovation.

<span id="YtvQRivQ"></span>
## Application: One\-stop, scenario\-oriented serverless solution

[Application](https://docs.byteplus.com/en/docs/faas/Application_center) is a highly encapsulated serverless pattern designed for specific business scenarios. It packages underlying complex functions, triggers, dependency environments, and infrastructure configuration (for example, GPU, network) into a ready\-to\-use solution. Developers only need to perform simple console operations or API calls to deploy a fully featured application with one click.

You can think of **Application** as the official veFaaS **best practices template** and **one\-stop deployment unit**. This greatly lowers the threshold for using serverless, making it especially suitable for scenarios that require rapid implementation and have less concern for underlying details.

<span id="b3FLyVFF"></span>
### **Core features**


* **Scenario\-based encapsulation**: Each application is designed for a specific scenario, such as AI Agent, web service, AI painting (Stable Diffusion), and so on.

* **One\-click deployment**: With pre\-configured application templates, users do not need to configure resources from scratch and can complete deployment within minutes.

* **Maintenance\-free experience**: Inherits the core advantages of Serverless, automatically handling scaling, load balancing, and resource management.

* **Built\-in integration**: Pre\-integrated with BytePlus TOS, API Gateway, and other cloud services, highly compatible within the ecosystem to improve business development efficiency.


<span id="YljnDXFg"></span>
### **Applicable scenarios**

veFaaS applications are especially suitable for the following scenarios:


* **Rapid implementation of AI cloud\-native application POC**: This is the most fundamental scenario for the **application** form. veFaaS provides a large number of AI\-related application templates, for example:

   * **AI Agent and MCP Server**: Provides a Serverless hosting environment for large language model (LLM) applications, such as Browser Use Agent and Computer Use Agent, enabling agents to perform complex tasks that interact with browsers and desktop environments.

   * **GPU inference and training**: One\-click deployment of AI painting applications like Stable Diffusion and ComfyUI that require GPU acceleration, allowing you to use expensive GPU resources only when needed.

   * **Coze application hosting**: Seamlessly deploy AI Bots created on the Coze platform and expose them as independent services.

* **Standard web services and APIs**: Quickly build web applications or RESTful APIs that conform to standard frameworks (such as Express), suitable for small to medium\-sized projects, prototyping and validation, and internal tools.

* **Lightweight data and media processing**: For example, use FFmpeg application templates for video frame extraction, format conversion, and other tasks, processing media files as needed.


<span id="gBKJRwTy"></span>
## Function: Event\-driven computing unit

[Function](https://docs.byteplus.com/en/docs/faas/Functions) is the most fundamental form of Serverless computing, that is, what the industry commonly refers to as FaaS (Function Service). It allows developers to focus only on the core business logic code (a **function**). Unlike highly encapsulated **applications**, **functions** provide **maximum flexibility and customization**, allowing developers to start from scratch, freely combine triggers, and write arbitrarily complex code logic.

<span id="Uzvuzg7H"></span>
### **Core features**


* **Event\-driven**: Functions are triggered by explicit event sources, such as API Gateway receiving HTTP requests, message queues (Kafka/RocketMQ) receiving new messages, object storage (TOS) receiving new file uploads, or timers expiring.

* **Stateless and short\-lived execution**: Function instances are stateless by default and are typically designed to complete a single task within a limited time (from a few seconds to a few minutes). States that require persistence must rely on external storage, such as databases or caches.

* **On\-demand execution and automatic scaling**: The platform automatically creates or destroys function instances based on real\-time request volume, enabling rapid scaling up and down within milliseconds.

* **Fine\-grained billing**: Costs are based solely on the actual number of function executions and the computing resources consumed (CPU × duration, memory × duration), truly achieving **pay\-as\-you\-go**.


<span id="HZCyjkTc"></span>
### **Applicable scenarios**

veFaaS functions are efficient tools for building modern serverless backends and are suitable for nearly all backend scenarios that do not require long\-running processes or persistent connections:


* **Web API and microservices**: As core components of backend microservice architectures, each function hosts an independent API endpoint or business function. This approach is an ideal choice for building highly elastic, low\-cost web services, with services provided externally through an API gateway.

* **Data processing and ETL**: Real\-time cleansing, transformation, and loading (ETL) of data from sources such as Kafka, RocketMQ, and TOS. For example, when a user uploads a picture to TOS, a function is automatically triggered to compress it, add a watermark, and store it in another location.

* **Asynchronous task processing**: Executes time\-consuming backend tasks, such as sending emails, generating reports, and data analytics. The client receives an immediate response after submitting a task, while the function executes asynchronously in the backend. Upon completion, the client can be notified via callback or message.

* **Scheduled tasks and automated operations**: Through timer triggers, tasks such as database backups, report generation, system health checks, and cleaning up expired data are executed periodically.

* **Internet of Things (IoT) backend**: Processes massive data streams reported by IoT devices for real\-time analysis, alerting, and storage.


&nbsp;

<span id="dhOgSOQV"></span>
## Cloud sandbox: Secure, isolated execution environment for AI Agent applications

[Cloud sandbox](https://docs.byteplus.com/en/docs/faas/Cloud_sandbox) is a serverless model that provides a **secure and isolated execution environment**. It allows you to start a temporary, isolated container environment (sandbox instance) dynamically and on demand, in which you can execute untrusted code or perform tasks with complex environment dependencies, and immediately destroy it after the task is completed, ensuring security and cost\-effectiveness.

Unlike **service**\-oriented **applications** and **functions**, the core value of the cloud sandbox lies in its **isolation, security, and dynamic capabilities**. It is more like a **serverless temporary virtual machine or container**, designed specifically for scenarios that require a dynamic and secure execution environment.

<span id="xEK4OQLE"></span>
### **Core features**


* **Strong isolation and security**: Each sandbox instance runs in an independent virtualization environment, strictly isolated from the host and other instances, effectively preventing malicious code from escaping and lateral attacks.

* **Dynamic creation and destruction**: Sandbox instances can be created on demand via API, tasks can be executed, and the instances are automatically destroyed after the task is completed or upon timeout, with resources used only as needed.

* **Custom environment**: Supports building the sandbox runtime environment using custom container images, allowing any tools, libraries, and dependencies to be pre\-installed to meet the requirements of complex tasks.

* **API\-driven**: The entire lifecycle (creation, command execution, destruction) is fully controlled by the API, making it easy to integrate with existing business systems.


<span id="txm8CXUL"></span>
### Applicable scenarios

The cloud sandbox is an ideal solution for situations where users need a programmable and executable environment:


* **Tool execution environment for AI Agents**: Provides a secure "playground" for AI Agents. When Agents need to execute code, access the file system, or interact with external tools, they can do so within the sandbox. Even if risky actions are performed, the core system remains unaffected.

* **Reinforcement learning and evaluation**: Designed for scenarios that require rapid, batch creation of Agent runtime environments and evaluation environments (for example, Swe\-bench evaluation).

* **Code sandbox for Chatbot and online programming**: Provides users with an online code editor and runtime environment. The code submitted by the user is executed in an isolated sandbox, and the results are returned to the frontend to ensure the platform's security.


<span id="aiiRY2Cq"></span>
## Solution comparison

To better understand the differences among the three, we compare them across multiple dimensions:


|Aspect |[Application](https://docs.byteplus.com/en/docs/faas/Application_center) |[Function](https://docs.byteplus.com/en/docs/faas/Functions) |[Cloud Sandbox](https://docs.byteplus.com/en/docs/faas/Overview_of_cloud_sandbox) |
|---|---|---|---|
|**Core value** |Scenario\-based solutions, one\-click deployment |Event\-driven compute unit, extreme elasticity |Securely isolated dynamic execution environment |
|**Applicable scenarios**<br><br> |AI Agent, GPU inference, standard Web services, scenarios that closely match templates |Web API, microservices, data processing (ETL), scheduled tasks, asynchronous jobs |AI Agent execution, online programming, secure code execution, CI/CD |
|**Trigger/access method** |Typically accessed directly via public URL (built\-in API gateway) |Event\-driven (API gateway, MQ, TOS, Timer, and more) |Proactively invoke, create, and control instances via OpenAPI/SDK |
|**Scaling** |Fully automated, automatic scaling based on traffic patterns |Fully automated, with automatic scaling based on event frequency or request volume (configurable reservation available) |On\-demand, manual or programmatic creation and destruction of instances |
|**State management** |Stateless by default; some applications (such as MCP Server) provide session persistence mechanisms |Strictly stateless, relies on external storage (such as Redis, DB) |Stateful, sandbox instances can maintain state during their lifecycle (such as file system, memory) |
|**Cost and billing** |Billed based on the actual compute resources (vCPU, memory, GPU) consumed by the application and the number of invocations |Billed according to the number of function executions and computing resources (vCPU/memory/GPU \* seconds) |Billed according to the lifespan and specifications of sandbox instances |
|**Customization capability** |Relatively low, limited by template capabilities |Extremely high, fully customizable |High, controlled via custom image and API |
