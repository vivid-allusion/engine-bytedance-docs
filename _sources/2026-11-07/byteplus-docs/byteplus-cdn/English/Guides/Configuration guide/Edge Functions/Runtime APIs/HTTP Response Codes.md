---
title: "HTTP Response Codes"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Exception-Handling"
---

For a function execution triggered by a domain trigger, the function indicates whether the execution was successful through HTTP response status codes. If the function execution fails, BytePlus Edge Functions has different retry strategies for different status codes.


|Status Code |Meaning |Description |Retry Strategy |
|---|---|---|---|
|200 |Success |The function executed successfully. |No retry strategy |
|599 |Function code error |This could be due to a rejected promise or an uncaught exception. The runtime listens for all promise exceptions. If any promise is rejected or an exception is not caught, and it occurs during the response sending process, the runtime will truncate the response and cancel the request context. |Retry idempotent requests once within the current edge node |
|598 |Rate limiting |The function code has too many contexts, or resources (such as memory, CPU execution time, etc.) are severely insufficient. |Retry idempotent requests once across edge nodes. You can also [submit a ticket](https://console.byteplus.com/workorder/create) to request adjustments to resources or rate limiting policies. |
|597 |Banned |Banned for security reasons, usually for a few minutes, and automatically restored after that period. |Retry idempotent requests once across edge nodes |
|596 |Global rate limiting |The edge node hosting the Edge Function has reached its resource limit and starts circuit breaking and rate limiting. |Retry idempotent requests once across edge nodes |
|594 |Unrecognized user |Traffic from non\-Edge Function users enters the runtime. |No applicable strategy |
|593 |Service discovery infrastructure error |Platform service exception. |Retry idempotent requests once across edge nodes |
