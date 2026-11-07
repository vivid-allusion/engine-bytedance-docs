---
title: "Product features"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Features"
---

veFaaS is a fully managed and Serverless computing platform that is driven by events. It provides three product patterns: function, application, and cloud sandbox. This topic describes the core features currently supported by veFaaS by product pattern.


|Category |**Feature** |**Description** |
|---|---|---|
|Application |[Application template](https://docs.byteplus.com/en/docs/faas/Apply_a_template) |An application is a deployment unit for complete business scenarios. It orchestrates functions and dependent resources and supports quick template deployment. |
||[Managing applications](https://docs.byteplus.com/en/docs/faas/Manage_applications?lang=en) |Creates, deploys, updates, and deletes applications. Functions and resources under an application are managed in a centralized manner. |
||[Starting or stopping applications](https://docs.byteplus.com/en/docs/faas/Application_Start_Stop?lang=en) |Starts or stops applications as needed and flexibly controls running status and resource usage. |
||[Automatically building and deploying applications](https://docs.byteplus.com/en/docs/6662/1928315?lang=en) |Automatically build images and deploy applications after code repositories are associated to achieve continuous delivery. |
|Function<br><br> |[Managing functions](https://docs.byteplus.com/en/docs/faas/Managing_functions?lang=en) |Creates, deploys, updates, and deletes functions. Functions can be deployed through code packages and images. |
||[Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration?lang=en) |Configures the instance memory size, maximum number of instances, concurrency per instance, execution timeout, VPC network, storage, environment variable, and more. |
||[Trigger](https://docs.byteplus.com/en/docs/faas/Trigger_overview?lang=en) |Supports various triggers such as Timer, APIG, TOS, Kafka, RocketMQ, and BMQ to meet the requirements of different event\-triggered scenarios. |
||[Autoscaling](https://docs.byteplus.com/en/docs/faas/Elastic_scaling?lang=en) |Automatically scales in or out based on request volume and provisions instances to reduce cold\-start latency. |
||[Releasing functions](https://docs.byteplus.com/en/docs/faas/Release_function?lang=en) |Releases code and configurations based on version snapshots. Supports full release and canary release. Monitors the release process and manages releases and version records. |
||[Dashboard overview](https://docs.byteplus.com/en/docs/faas/Dashboard_overview?lang=en) |Provides metric monitoring, persistent logging (TLS), real\-time instance logs, instance WebShell, and online testing to support function observability and debugging. |
||[Function resource statistics](https://docs.byteplus.com/en/docs/faas/Function_resource_statistics?lang=en) |Collects statistics on resource allocation for accounts and individual functions. Maximum function resources = Instance memory specification × Maximum number of instances. This facilitates appropriate resource allocation and cost control. |
||[Function type](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection) |* [Event function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions?lang=en): Event\-triggered functions. They are applicable to event processing, data forwarding, and similar scenarios.<br><br>* [Web app function](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications?lang=en): Functions for hosting web services. They are applicable to web backends and API services.<br><br>* [Microservices app function](https://docs.byteplus.com/en/docs/faas/Create_microservices_applications?lang=en): Functions deployed in the form of microservices. They are applicable to business architectures with service\-oriented decomposition.<br><br>* [Task function](https://docs.byteplus.com/en/docs/faas/Creating_tasks?lang=en): Responds to invocation events through asynchronous execution, returns a request ID upon task submission, and provides task status tracking and observability capabilities.<br><br>* [GPU function](https://docs.byteplus.com/en/docs/faas/Overview_of_serverless_GPU?lang=en): Provides high‑parallelism computing power based on Serverless GPU. This type of function is applicable to AI model inference, training, and media acceleration (audio/video and graphics/image). |
|Cloud sandboxes |[Sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications?lang=en) |Creates and manages sandbox applications, which provide runtime templates and configuration for sandbox instances. |
||[Sandbox instance](https://docs.byteplus.com/en/docs/faas/Sandbox_instances?lang=en) |Creates, suspends, resumes, and deletes sandbox instances and supports file system snapshots. |
||[Sandbox image](https://docs.byteplus.com/en/docs/faas/Sandbox_images?lang=en) |Manages the images required for sandbox execution and specifies custom sandbox environments. |
||[Sandbox instance warm pools](https://docs.byteplus.com/en/docs/faas/Sandbox_instance_warm_pools?lang=en) |Pre‑creates and maintains a certain number of sandbox instances to reduce cold‑start latency. |
