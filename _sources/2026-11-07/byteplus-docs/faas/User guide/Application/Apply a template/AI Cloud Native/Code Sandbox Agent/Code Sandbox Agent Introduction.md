---
title: "Code Sandbox Agent Introduction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Code_Sandbox_Agent_Introduction"
---

This article mainly introduces the relevant information of Code Sandbox Agent intelligent agent application.

<span id="application-introduction"></span>
## Application introduction

Code Sandbox Agent is a code sandbox service offered by BytePlus Function Service (FaaS) based on the open\-source SandboxFusion project, while facing end users and AI suite developers. The user enters the programming task, then the programming task can be analyzed by Doubao large model, generating the program code in the corresponding language, and at last the user submits running request, and Sandbox runs the code and outputs execution result. The whole use process can be seen as follows: The large model helps solve the programming issues and output programs, and the Sandbox helps execute the programs and verify the correctness of codes.

<span id="direct-experience"></span>
### Direct experience


1. Log in to the [Function Service console](https://console.byteplus.com/FaaS).

2. On the top navigation bar, select the target region.

3. In the left navigation bar select **Application** \> **App Square**.

4. Find the **Code Sandbox Agent** on the **App Square** page and click **Free trial** to experience it directly.


<span id="process-architecture"></span>
### Process architecture

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a85d917f80c696aecda8dcdec07e1e23.png) </span>


* **Concurrent requests**: Code Sandbox Agent supports all the users logged in to the FaaS console to send concurrent requests.

* **Built\-in large model**: Doubao\-1.5\-pro\-32k.

* **Support building dedicated services**: Based on the public Code Sandbox Agent in the App Square, you can also [deploy code-sandbox applications with one click](https://docs.byteplus.com/en/docs/faas/Deploying_Code_Sandbox_Agent_applications_with_one_click).


<span id="associated-models-and-cloud-products"></span>
## Associated models and cloud products

<span id="model"></span>
### Model


|Related Services |Description |Billing Description |
|---|---|---|
|Doubao\-1.5\-pro\-32k |Doubao\-1.5\-pro is a brand\-new generation leading model, with all\-around upgraded performances, and has excellent performances in regards of knowledge, code, and inference, etc. It is used to quickly generate code for **sandbox** tests. |[Model Service Billing](https://docs.byteplus.com/en/docs/ModelArk/1099320) |


<span id="cloud-service"></span>
### Cloud service


|Related Services |Description |Billing Description |
|---|---|---|
|FaaS |BytePlus Function Service (FaaS) is an event\-driven computing platform fully managed by Serverless. Support quickly creating and deploying functions, and integrating middleware and database products on the cloud according to demands. |[Function Service billing](https://docs.byteplus.com/en/docs/faas/Billing_overview) |


<span id="technology-implementation"></span>
## Technology implementation

Code Sandbox Agent backend core components:


* **Code sandbox service**: It is responsible for running the codes submitted by users in the **sandbox** environment, outputting code compilation and running results, and cleaning up relevant progress and subdirectories after execution ends. Supports Python, Golang, Bash, Node.js, Java, and many other languages.

* **Sandbox built\-in large model**: Adopts Doubao\-1.5\-pro\-32k which is responsible for analyzing the programming tasks of users, and outputting program codes.


The Code Sandbox Agent is deployed in the FaaS, and it provides externally task request and result output through the API gateway trigger.
