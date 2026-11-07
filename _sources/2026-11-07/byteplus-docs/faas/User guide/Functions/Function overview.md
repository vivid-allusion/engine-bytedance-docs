---
title: "Function overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Functions_overview"
---

A function is the smallest deployable and billable unit in FaaS. It hosts your business code or container images and supports multiple runtimes, various rich triggers, and on‑demand autoscaling. You do not need to manage underlying infrastructure such as servers. To run your business elastically and reliably, you only need to write and upload your code or images. You are charged for the resources you actually use.

<span id="ZX4RQrVu"></span>
## Procedure

Running a function in veFaaS generally involves a complete lifecycle from code writing to online O&M.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e395d573ac97d6c80e532b548175138a.png) </span>


1. [Write code](https://docs.byteplus.com/en/docs/faas/Function_management): Write your business code or prepare a container image based on the selected runtime. veFaaS provides multiple out\-of\-the\-box images to help you quickly create functions.

2. [Create and deploy a function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection?lang=en): Select a function type (including event function, web app function, microservices app function, task function, and GPU function), deploy it as a code package or image, and specify configurations, such as instance specifications, concurrency, timeout, and storage mounts.

3. (Optional) [Develop and debug](https://docs.byteplus.com/en/docs/faas/Debugging): After deployment, debug and test the function online to verify execution logic and return results.

4. [Release the function](https://docs.byteplus.com/en/docs/faas/Release_function): After confirmation, release the function. Both full release and canary release are supported. You can also view release notes and version records.

5. [Configure triggers](https://docs.byteplus.com/en/docs/faas/Trigger_overview): Bind triggers (including APIG, timer, Kafka, RocketMQ, TOS, BMQ, and TLS) to the function to connect upstream and downstream event sources.


<span id="UPTGNvQt"></span>
## Core capabilities


* **Multi‑language runtime**: Runtimes for mainstream languages such as Python, Golang, and Node.js are built in. Custom runtime environments can be created via native runtimes and container images.

* **Multi‑** **event‑** **source trigger**: Various triggers such as APIG, timer, Kafka, RocketMQ, and TOS are provided. They function as the glue between services and seamlessly connect upstream and downstream business logic.

* **Version and canary release**: Version management after code and configuration updates is supported. Both full and canary releases are supported. Agile development and quick iteration are supported.

* **Serverless GPU**: Mainstream GPU resources are allocated on demand to meet acceleration requirements in AI, audio/video, graphics, and other scenarios.

* **Asynchronous task**: Events are responded to in asynchronous mode. Invocations do not need to block and wait for results. The maximum execution timeout duration is 3 hours.

* **Observability and O&M**: Metric monitoring, TLS logs, instance‑level logs, and Webshell login are provided to support fine‑grained issue localization and O&M.
