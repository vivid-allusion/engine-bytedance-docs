---
title: "Function creation method selection"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection"
---

To meet the needs of users in different contexts, FaaS provides various types of functions. This document introduces the applicable scenarios and differences of each type, for your technical selection.


|Comparison Item |[Event Function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions) |[Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) |[Microservices applications](https://docs.byteplus.com/en/docs/faas/Create_microservices_applications) |[Task](https://docs.byteplus.com/en/docs/faas/Creating_tasks) |
|---|---|---|---|---|
|Applicable scenarios |Write the program according to the interface defined by the FaaS. |* Write programs based on popular frameworks for various languages (such as Python Flask, Golang Gin, etc.).<br><br>* Migrate existing web framework applications.<br><br>* Support for container image deployment, fully control the environment in which web applications run, with no language restrictions. |* Hosting for any language/framework, aimed at microservices applications, MQ consumer services, etc.<br><br>* Seamlessly migrate to containerized deployment applications. |Respond to asynchronous call requests through task mode and exit the program once completed. Track and save the status of each stage of the task, providing comprehensive task control and observability. |
|Deployment method |Code package |* Code package<br><br>* Container image |* Code package<br><br>* Container image |* Code package<br><br>* Container image |
|CPU allocation mode |Allocate CPU only upon requests |Allocate CPU only upon requests |Always allocate CPU |Allocate CPU only upon requests |
|Support for GPU instances |Not supported |Support for container images |Support for container images |Container image support |
|Cold start |Fastest. Code packages don’t contain runtime, so its have the fastest cold start. |Deployment with code packages is faster, whereas deployment with container images is slower. |Deployment using code packages is faster, while using container images is slower. |Deployment with code packages is faster, whereas deployment with container images is slower. |
|Code package size and format |256 MiB uncompressed code package, `.zip` file. ||||
|Image size and format |1 GiB uncompressed image, refer to [What is Container Registry](https://docs.byteplus.com/en/docs/cr/what-is-cr). ||||
|Runtime environment |Python、Golang、Node.js |Native Python、Native |Native |Native |
|Traffic access method |Access through triggers. |Access through triggers. |Does not support triggers. |Access through triggers. |
