---
title: "Overview of cloud sandbox"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Overview_of_cloud_sandbox"
---

Cloud Sandbox Service is a next\-generation infrastructure offered by BytePlus Function Service (FaaS), designed for AI inference and training scenarios. It provides a secure, isolated, and efficient cloud sandbox environment. This topic introduces the concept and advantages of cloud sandbox.

<span id="JoDyFgIA"></span>
## Basic concepts


* **Cloud sandbox**: a serverless service built for AI task execution, offering high elasticity, low cost, stateful operation, secure isolation, easy maintenance, and rich features. You can create cloud sandbox environments within seconds based on your business requirements without the need to be concerned about the underlying infrastructure. In inference scenarios, a cloud sandbox provides an AI\-driven task execution environment. In training scenarios, such as model Reinforcement Learning (RL) training or Reinforcement Fine\-Tuning (RFT) training, a cloud sandbox execution environment supports code execution, enhanced tool calling, and complex task handling.

* **Sandbox applications**: they are the basic units of cloud sandbox, responsible for scheduling and operation of resources. A sandbox application is built based on sandbox images and related configurations.

* **Sandbox instances**: they are secure and isolated container runtime environments realized by loading and running sandbox images, with configurable lifetime for each instance.

* **Sandbox images**: they are standardized packages that include all of the files, binaries, libraries, and configurations to run sandbox instances. Cloud Sandbox supports custom images and ready\-to\-use public images.


<span id="7XEhTLvz"></span>
## Advantages


* Elasticity without maintenance: Based on serverless architecture, able to start up within 150 milliseconds (ms) and scale out with massive resources.

* Stateful operation: users are allowed to run specific sandbox instance and share the same sandbox runtime environment.

* Abundant templates: provide Code, Browser, and Computer runtime environment templates, giving an out\-of\-the\-box experience and helping users focus on developing business logic.

* Image distribution: capable of preheating and distributing thousands of images, meeting the requirement of rapid startup of sandboxes.

* Millisecond\-level billing: sandbox resources are charged based on the actual lifetime of instances.

* Flexible integration: easy integration of MCP, API, and SDK, allowing fast use of features.


<span id="qQ49dJMs"></span>
## Usage flow

Follow the steps below to use cloud sandbox:


1. Prepare the [sandbox images](https://docs.byteplus.com/en/docs/faas/Sandbox_images) to be used:

   * If you intend to use the **public images** provided by FaaS , there is no additional preparation required.

   * If you intend to use **custom images**, you need to first upload the image to the Container Registry (CR) and perform image preheating.

2. [Create a sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications): create a basic unit of the cloud sandbox configured with gateway routing, which facilitates scheduling and operation of resources in the cloud sandbox.

3. [Create a sandbox instance](https://docs.byteplus.com/en/docs/faas/Sandbox_applications): create a sandbox instance based on a sandbox image you selected.

4. [Test the sandbox application](https://docs.byteplus.com/en/docs/faas/Sandbox_applications#udy3KgNt): when sandbox instances are running, use the curl command or the Playground tool to perform tests.


<span id="qQ49dJMs"></span>
## Billing description

The sandbox will be charged during their lifetimes. For billing details, see [Pay-as-you-go - Cloud sandbox](https://docs.byteplus.com/en/docs/faas/Pay-as-you-go#A3MAJE08).
