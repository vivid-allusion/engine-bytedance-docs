---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/hive_FAQs"
---

<span id="查看hive日志"></span>
## View Hive logs


* On the machine where the task is triggered, check the client logs at `/tmp/hive/hive.log`

* On the primary node, check the HiveServer2 and Hive Metastore logs in the `/var/log/emr/hive/` directory


<span id="yarn资源监控"></span>
## Yarn resource monitoring


* On the EMR Cloud Monitoring page, view Yarn resource usage during cluster task execution


<span id="yarn任务日志查看"></span>
## View Yarn task logs


* On the EMR cluster page, under the Access Links tab, visit the Yarn UI page to locate the corresponding Application

* On the machine, using the hive user, export the task logs for troubleshooting with `yarn logs -applicationId xxx > yarn.txt`.
