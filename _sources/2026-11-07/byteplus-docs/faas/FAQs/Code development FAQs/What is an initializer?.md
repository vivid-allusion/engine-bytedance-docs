---
title: "What is an initializer?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/What_is_an_initializer"
---

The initializer is the entry point for the function's initialization logic. If an initializer function is set, veFaaS will first invoke the initializer to complete the function's initialization before calling the handler to process requests. If the function initialization fails, the request will not be executed. For more information, refer to [Code development overview](https://docs.byteplus.com/en/docs/faas/Code_development_overview).
