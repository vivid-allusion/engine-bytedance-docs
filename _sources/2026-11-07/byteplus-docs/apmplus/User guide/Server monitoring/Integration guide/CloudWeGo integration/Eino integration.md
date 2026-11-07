---
title: "Eino integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Eino"
---

Eino is an open\-source LLM application development framework developed by ByteDance. It is an AI application development framework in Golang. The framework features stability, flexible extensibility, comprehensive tooling ecosystem support, reliability, and easy maintenance. The framework delivers rich capabilities, including ‌modular components‌, ‌integration components‌, ‌component orchestration‌, and ‌aspect\-oriented extensions‌ to facilitate AI application development. This empowers developers to efficiently build ‌well\-architected, maintainable, and highly available AI applications‌.

<span id="R1vk190J"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information, see this Eino community topic: <a href="https://www.cloudwego.io/zh/docs/eino/ecosystem_integration/callbacks/callback_apmplus/">callback_apmplus</a>.</div>



1. Obtain the AppKey for authentication. For details, see [How do I obtain the AppKey for Server-side Monitoring authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication)

2. Configure the APMPlus Callback as follows.


```Go
package main

import (
    "context"
    "log"
    
    "github.com/cloudwego/eino-ext/callbacks/apmplus"
    "github.com/cloudwego/eino/callbacks"
)

func main() {
    ctx := context.Background()
    // Create the apmplus handler.
    cbh, showdown, err := apmplus.NewApmplusHandler(&apmplus.Config{
       Host: "apmplus-cn-beijing.volces.com:4317",
       AppKey:      "xxx",
       ServiceName: "eino-app",
       Release:     "release/v0.0.1",
    })
    if err != nil {
       log.Fatal(err)
    }

    // Set apmplus as the global callback.
    callbacks.AppendGlobalHandlers(cbh)

    g := NewGraph[string,string]()
    /*
     * compose and run graph
     */

    // Exit after all traces and metrics have been reported.
    showdown(ctx)
}
```


<span id="1KIxg1i5"></span>
## What to do next

After Eino is successfully integrated, you can view traces and metrics in the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server).
