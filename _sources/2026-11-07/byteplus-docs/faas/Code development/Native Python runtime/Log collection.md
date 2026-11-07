---
title: "Log collection"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_Python_runtime_Log_collection"
---

When logs are turned on, FaaS will write the stdout and stderr logs produced by functions to the user's account, and distinguish these two types of logs using the log_type field. The sample code is as follows.

```python
// Print log to stdout.print("Hello, Native Python!")

// Print log to stderr.import syssys.stderr.write("This is an error message.\n")
```
