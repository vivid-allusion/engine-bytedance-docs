---
title: "How should a synchronous function timeout exceeding 900 seconds be handled?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/How_should_a_synchronous_function_timeout_exceeding_900_seconds_be_handled"
---

veFaaS provides asynchronous task capability, supporting a maximum runtime of 3 hours for a single request or task.

Currently, switching between synchronous and asynchronous modes after creating a function is not supported. If the timeout of the current synchronous function exceeds 900 seconds (15 minutes), please recreate the function and configure the asynchronous task feature. For Actions details, refer to [asynchronous task configuration](https://docs.byteplus.com/en/docs/faas/Configuring_async_tasks).
