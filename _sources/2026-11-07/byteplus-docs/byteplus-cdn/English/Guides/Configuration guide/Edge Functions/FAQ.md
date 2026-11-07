---
title: "FAQ"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge_functions_faq_en"
---

This document answers frequently asked questions about BytePlus Edge Functions.

<span id="how-is-the-edge-functions-runtime-different-from-runtimes-like-node-js-or-deno"></span>
## How is the Edge Functions runtime different from runtimes like Node.js or Deno?

The Edge Functions runtime is a lightweight Function\-as\-a\-Service (FaaS) environment deployed on global edge nodes. Unlike traditional cloud FaaS, it is designed for large\-scale, highly elastic, and low\-latency scenarios.

The key differences between the Edge Functions runtime and runtimes like Node.js or Deno are as follows:


* **Architecture and Resource Management**: The Edge Functions runtime is built on the V8 Isolate and implements lightweight multi\-tenant isolation. This architecture precisely controls the computing and memory resources for each tenant, including memory usage, CPU execution time, and function response time. For more information, see [Usage Limits](https://docs.byteplus.com/en/docs/byteplus-cdn/Usage_Limits_Functions).

* **Security**: To ensure the security of the runtime environment, Edge Functions adopt multi\-layered security policies to effectively prevent malicious code attacks. These policies include the V8 isolation mechanism, CPU time limits, and defensive API design. For example, the clock precision of the runtime is deliberately adjusted to around 10 milliseconds to prevent attackers from using the precise time returned by the [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) object to launch timing side\-channel attacks.

* **Execution Context**: The Edge Functions runtime enforces strict context isolation. API calls are restricted to their respective contexts, and the lifecycle of objects created by APIs is also precisely managed. For details, see [How It Works](https://docs.byteplus.com/en/docs/byteplus-cdn/How_It_Works_Functions).

* **API Compatibility**: The Edge Functions runtime is compatible with some [WinterTC](https://wintertc.org/) standard APIs and provides a set of APIs exclusive to edge computing scenarios. The underlying C++ implementation of these APIs is designed to optimize resource consumption and improve execution efficiency. At the same time, for security and performance reasons, the runtime does not support some APIs in Node.js or Deno, such as `net`, `process`, and `fs`.
