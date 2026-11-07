---
title: "Log collection"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Log_collection"
---

When logs are turned on, Function Service writes the stdout and stderr logs produced by functions to the user's account and identifies these two types of logs through the log_type field. Example code as follows:

```javascript
// Print log to stdout.
console.log("info log from FaaS")

// Print log to stderr.
console.error("warn/error log from veFaaS")
```
