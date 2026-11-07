---
title: "Glossary"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Basic_concepts"
---

This topic lists common terms in BytePlus Function Service (veFaaS) for easy reference.


|Term |Description |
|---|---|
|Function |A function comprises function code and configuration. It serves as the fundamental unit for scheduling and executing code. |
|Function instance |The underlying Kubernetes resource that actually executes the function code. |
|Function ID |The unique identifier of a function. |
|Trigger |An event source that triggers function code execution. When an event meets specified rules in a trigger, the function is executed. |
|Runtime |The environment for running function code. The environment varies by programming language. |
|Cold start |The process of creating a function instance from scratch to handle requests. This process mainly involves downloading the function code, starting the container, and initializing the runtime. After the cold start is completed, the function instance is ready to handle subsequent requests.<br><br>When there is no traffic for a period of time, instances of a function will automatically scale down to zero. When a request is received again, the function will perform a cold start. |
|Function revision |A snapshot of function code and configuration. A released function is read\-only and not editable. |
|Latest revision |The latest function revision with editable function code and configuration. When a function is released based on its latest revision, the system will automatically generate a new revision number. |
|Online revision |The function revision that stably handles ‌trigger traffic‌ after a full release. In the canary release process, it refers to the ‌historically stable revision‌ not yet fully replaced (the one still serving <100% traffic). |
|Canary revision |The function revision that serves a ‌specified percentage of traffic‌ during a canary release. When its traffic ratio reaches 100%, it becomes the new online revision.<br><br>For example, the fully released V1 revision is the online revision. Following code or configuration modifications, a 60% canary release of ‌V2‌ makes it the canary revision, while ‌V1‌ remains online. After the V2 revision passes verification, adjust the traffic ratio of the V2 revision to 100%. At this point, the V2 revision becomes the new online revision. |
|Memory specification |The amount of memory used by a single function instance during execution. |
|Wildcard domain |A type of domain name format that uses a wildcard character (usually \*) to match all subdomains of a domain. For example, \*.example.com is a wildchard domain. Its core advantage lies in the ability to automatically generate an unlimited number of unique subdomains without the need for manual resolution of each subdomain, thereby enabling convenient assignment to different services or instances. |
