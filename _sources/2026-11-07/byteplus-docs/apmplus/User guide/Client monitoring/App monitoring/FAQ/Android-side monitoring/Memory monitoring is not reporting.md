---
title: "Memory monitoring is not reporting"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Memory_monitoring_is_not_reporting"
---

The data sources in the memory optimization section are divided into three parts:


* OOM crash trend section

* The extended indicators section

* Leaks, large objects, and single device query section


Troubleshooting process:


* **Leak, large object, and single device query section:** 


Confirm that memory initialization is normal.

Set debugMode(true) during testing to increase the reporting sample rate. For official launch, debugMode must be set to false.

Filter logs to confirm whether the memory file was successfully reported. During OOM or memory limit events, there is a certain success rate for generating a .heap file via dump. If generation fails, try several times or test on a different device.
