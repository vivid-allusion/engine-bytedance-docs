---
title: "Browser Use Agent Introduction"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Browser_Use_Agent_Introduction"
---

This article mainly introduces the relevant information of Browser Use Agent intelligent agent application.

<span id="application-introduction"></span>
## Application introduction

Browser Use Agent is a Browser as a Service offered by Function Service (FaaS) based on the open\-source browser\-use project and facing end users and AI suite developers. Only by entering the retrieval task, you can analyze and disassemble the task by the large model, call the browser to search the task in real time, and finally integrate and output the task result. During the whole operation process, the procedure planning of the large model and browser operation can be viewed in real time, meanwhile manual intervention in browser operation is supported, e.g. entering verification code, receiving Cookies, and entering username and password, etc.

This service mainly supports the browser automation business, and can be used as a real\-time retrieval tool for the large model itself or the large model application expansion.

<span id="direct-experience"></span>
### Direct experience


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar select **Application** \> **App Square**.

4. Find the **Browser Use Agent** on the **Application Square** page and click **Free trial** to experience it directly.


<span id="process-architecture"></span>
### Process architecture

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f1a45a05b6fd875f8e9ef32fb8a55179.png) </span>


* **Concurrent requests**: Browser Use Agent supports all users logged in to the Function Service console to send concurrent requests.

* **Built\-in super\-capable large model**: Built\-in DeepSeek\-V3 latest version (250324) large model, driving retrieval task planning, scheduling, summary extraction, and returning.

* **Support building dedicated services**: Based on the public Browser Use Agent in the Application Square, you can also [deploy browser-use applications with one click](https://docs.byteplus.com/en/docs/faas/Deploying_Browser_Use_Agent_applications_with_one_click).


<span id="associated-models-and-cloud-products"></span>
## Associated models and cloud products

<span id="model"></span>
### Model


|Related Services |Description |Billing Description |
|---|---|---|
|DeepSeek\-V3 based on ModelArk |DeepSeek\-V3 is a MoE model developed by DeepSeek. |[Model Service Billing](https://docs.byteplus.com/en/docs/ModelArk/1099320) |


<span id="cloud-service"></span>
### Cloud service


|Related Services |Description |Billing Description |
|---|---|---|
|FaaS |BytePlus Function Service (FaaS) is an event\-driven computing platform fully managed by Serverless. Support quickly creating and deploying functions, and integrating middleware and database products on the cloud according to demands. |[Function Service billing](https://docs.byteplus.com/en/docs/faas/Billing_overview) |


<span id="technology-implementation"></span>
## Technology implementation

The Browser Use Agent backend has the following core components:


* **Browser management component**: It is responsible for creating the browser instance before the task starts, and withdrawing the browser instance when the task ends.

* **Task execution component**: It is responsible for outputting execution steps in real time, providing the interface for viewing and operating the browser in real time, and updating task status while the large model is scheduling and operating the browser to implement tasks. After the task is completed, a screen recording playback is generated.

* **Browser task management component**: After the user initiates a browser task request, it will be added to the queue. This component is responsible for quickly scheduling the tasks that are not executed, and cleaning up the completed tasks.


The Browser Use Agent is deployed in the FaaS, and it provides externally an interface for task request and result output, and viewing the real\-time operation of browser through API gateway trigger.
