---
title: "Log collection"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Log_collection"
---

When logs are turned on, Function Service writes the `stdout` and `stderr` logs produced by functions to the user's account and identifies these two types of logs through the `log_type` field. Example code as follows.

```go
// Print log to stdout.
fmt.Printf("info log from FaaS")

// Print log to stderr.
fmt.Fprintf(os.Stderr, "warn/error log from FaaS")
```
