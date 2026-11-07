---
title: "Why is the log time inconsistent with its generation time?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/the-log-time-inconsistent-with-its-generation-time"
---

When you collect logs using LogCollector, Torch Log Service (TLS) uses the time when LogCollector collected the logs as the log timestamp by default. If an application prints logs too quickly or only a few system resources are allocated to LogCollector, LogCollector may delay collecting logs due to busy processes. This causes the log timestamp to be later than the log generation time.

For example, an application printed logs at 8:00, but LogCollector collected the logs at 8:10. By default, the log timestamp is 8:10 instead of 8:00. If you select 7:55 to 8:05 as the time range when querying logs, no logs can be found.

To avoid this issue, add a time field to the log format and define it as the time when logs were generated. When you create a collection rule, disable **Use collection time**. In this case, you must set **Time key name** and **Time conversion format**. For more information on how to set them, refer to [Collect logs in JSON mode](https://docs.byteplus.com/docs/tls/json_mode).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84a853c282d24e319de3531cf3b5e0ce~tplv-goo7wpa0wc-image.image) </span>
