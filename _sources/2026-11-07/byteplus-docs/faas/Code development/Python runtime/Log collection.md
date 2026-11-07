---
title: "Log collection"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Python_runtime_Log_collection"
---

When logs are turned on, Function Service writes the `stdout` and `stderr` logs produced by functions to the user's account and identifies these two types of logs through the `log_type` field. Example code as follows:

```Python
# Print log to stdout.
print("info log from FaaS")

# Print log to stderr.
print("warn/error log from FaaS", file=sys.stderr)
```
