---
title: "Computer Use Agent Introduction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Computer_Use_Agent_Introduction"
---

This article mainly introduces the relevant information of Computer Use Agent intelligent agent application.

<span id="application-introduction"></span>
## Application introduction

Computer Use Agent is an intelligent agent service promoted by the BytePlus based on ByteDance's Doubao large model, and facing end users and AI applications developers. This service has built\-in self\-developed out\-of\-the\-box MCP protocol\-driven computer use capabilities, which supports mouse control, keyboard control, and screenshot control, and other capabilities for Windows and Linux remote virtual computers. This service easily realizes remotely controlling ends (computers), completing work such as cutting and editing videos, creating PowerPoint slides, and operating and maintaining self\-media accounts, etc.

<span id="direct-experience"></span>
### Direct experience


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar select **Application** \> **App Square**.

4. Find the **Computer Use Agent** on the **Application Square** page and click **Free trial** to experience it directly.


<span id="process-architecture"></span>
## Process architecture

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bae6adddafb0d73defe894059548b56d.png) </span>

<span id="associated-models-and-cloud-products"></span>
## Associated models and cloud products

<span id="model"></span>
### Model


|Related Services |Description |Billing Description |
|---|---|---|
|Doubao\-1.5\-thinking\-vision\-pro\-250428 |A brand\-new visual & deep thinking model, equipped with stronger general multi\-modal understanding and reasoning capabilities, and interacts with Sandbox through human\-like capabilities including perception, reasoning, and actions, etc. |[Model Service Billing](https://docs.byteplus.com/en/docs/ModelArk/1099320) |
|Doubao\-1.5\-UI\-TARS |A native GUI\-oriented Agent model **that** interacts with Sandbox through human\-like capabilities such as perception, reasoning, and actions, etc. ||
|Doubao\-embedding |The semantic vectorization model is mainly oriented to the usage scenario of vector retrieval, which is used to retrieve the recorded user context.<br><br>This model is used only by Computer Use Agents that bind cloud search instances. ||


<span id="cloud-service"></span>
### Cloud service


|Related Services |Description |Billing Description |
|---|---|---|
|ECS |Elastic Compute Service (ECS) is a collection of resources composed of CPU, memory, and volumes, each of which is logically related to a computing hardware entity in the data center. You can apply for resources of corresponding size and different specifications according to your own needs for running different business loads |[Elastic Compute Service billing](https://docs.byteplus.com/en/docs/ecs/Billing-overview) |
|APIG |API Gateway (APIG) is a cloud\-native, highly scalable, and highly available cloud\-based gateway hosting service |[API gateway billing](https://docs.byteplus.com/en/docs/apig/Billing_overview) |
|FaaS |Function Service (FaaS) is an event\-driven computing platform fully managed by Serverless. Support quickly creating and deploying functions, and integrating middleware and database products on the cloud according to demands. |[Function Service billing](https://docs.byteplus.com/en/docs/faas/Billing_overview) |
|VPC |Virtual Private Cloud (VPC) builds an isolated, self\-configured virtual network environment for resources on the cloud. You can customize Internet Protocol address segments, security groups, and routing policies, and other network features in Virtual Private Cloud to manage resources on the cloud simply and efficiently. |Free |
|NAT gateway |Applications access the public network through the NAT gateway. |[NAT gateway billing](https://docs.byteplus.com/en/docs/natgateway/Billing-overview) |
|EIP |The application using the NAT gateway needs to associate an Elastic IP Address. |[Elastic IP Address billing](https://docs.byteplus.com/en/docs/eip/Billing-overview) |
|Torch Log Service (optional) |Provides one\-stop services for logs\-like data. |[Torch Log Service billing](https://docs.byteplus.com/en/docs/tls/billable_items) |
|Cloud Monitor (optional) |Support viewing function basic monitoring through Cloud Monitor. |Free |
|Cloud Search (optional) |For Computer Use Agent to have long\-term memory feature, select to bind the cloud search OpenSearch instance to the Computer Use Agent. |[Cloud Search billing](https://docs.byteplus.com/en/docs/cloudsearch/billing-overview) |


<span id="technology-implementation"></span>
## Technology implementation


* **WebUI**: It is responsible for displaying the desktop status of the computer instance in real time, and interactively displaying with the Agent the execution steps and screenshots, and managing the computer instances.

* **Computer Use Agent backend core components**:

* **Linux/Windows Computer management components**: Responsible for creating and deleting computer instances and managing instances desktop display.

* **Task execution components**: Responsible for interacting with the large model to obtain execution steps, and operating computer instances according to response results, outputting execution steps in real time, making screenshots in every step, and updating task status.


The Computer Use Agent and Web UI are deployed in the FaaS, and provide externally task request and result output through API gateway trigger.
