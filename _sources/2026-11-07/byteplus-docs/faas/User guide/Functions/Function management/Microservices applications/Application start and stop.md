---
title: "Application start and stop"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Application_Start_Stop"
---

Microservices applications provide a one\-click start/stop feature, supporting application control on demand to help users manage resource costs efficiently. This document introduces how to start and stop applications.

<span id="stop-application"></span>
## Stop application

Supports one\-click stopping of applications. After stopping the application, the system will destroy all instances, interrupting the related business operations, and costs associated with resource creation will also cease. The system saves the basic configuration information of components, facilitating a quick restart in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Applications in a disabled state do not support release operations. If you need to release application, start the application beforehand.</div>


* <div data-tips="true" data-tips-type="warning">Elastic policies do not apply to applications in a disabled state.</div>


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the region where your business is located.

3. On the **Function** page, find the target microservices application function and click the function name.

4. In the upper right corner of the function details page, click **Disabled**.

5. In the confirmation box, click **Stop**.


After the application is successfully disabled, its status will change to **Disabling**.

<span id="start-application"></span>
## Start application

Support one\-click application startup. After starting the application, the system will restore the application according to the online revision configuration, create instances based on the minimum number set in resource management configuration, and start charging. After successful startup, the corresponding business of the application can be used normally.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the region where your business is located.

3. On the **Function** page, find the target microservices application function and click the function name.

4. In the top right corner of the function details page, click **Enable**.

5. In the confirmation box, click **Start**.


After the start is successful, the application status will change to **Enabling**.
