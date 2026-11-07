---
title: "DeerGo integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_DeerGo"
---

‌DeerGo‌ is the Golang implementation of the DeerFlow framework built on ‌Eino‌. It delivers a Golang version of DeerFlow that integrates Large Language Models (LLMs) with specialized tools (such as web search, web crawlers, and Python code execution), enabling automated research and content creation.

Currently, DeerGo has built\-in integration with APMPlus Eino Callback (see the Eino community topic [callback_apmplus](https://www.cloudwego.io/zh/docs/eino/ecosystem_integration/callbacks/callback_apmplus/) for details). You only need to configure the **APMPLUS_APP_KEY** environment variable to enable the collection of trace and metrics instrumentation data at DeerGo runtime and report it to APMPlus. You can view the collected call traces and metrics in the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server).

<span id="j16GpFOd"></span>
## Procedure


1. Obtain the AppKey for authentication. For details, see [How do I obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication)

2. When you start DeerGo, configure the **APMPLUS_APP_KEY** environment variable.


```Go
export APMPLUS_APP_KEY=your_app_key
```


<span id="x8EJita7"></span>
## What to do next

After it is successfully integrated, you can view traces and metrics in the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server).
