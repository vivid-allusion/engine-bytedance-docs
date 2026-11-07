---
title: "Log structure description"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Log_structure_description"
---

FaaS function logs are written into Torch Log Service TLS by entry, each log entry follows a fixed `key:value` format. The following table describes the log structure.


|Description field |Field Type |Field Meaning |
|---|---|---|
|**path** |text |The filename of log collection; users need not be concerned. |
|**source** |text |The source IP of log collection; users need not be concerned. |
|content |text |**path** |
|function_id |text |The unique identifier of the function, which is the **Function ID** displayed on the **Configuration** tab. |
|function_name |text |Function name. |
|log_type |text |Log output types, including `stdout` and `stderr`.<br><br>FaaS will collect log information through the `stdout` and `stderr` fields in your code. |
|pod_name |text |The function instance (Pod) name; users need not be concerned. |
|revision_number |long |log_type |
