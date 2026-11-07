---
title: "Spark integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_integration"
---

In Ranger, Spark and Hive share the same policy, which is HADOOP SQL \-\> default_hive. Therefore, you can directly refer to [Hive integration](https://docs.byteplus.com/docs/E-MapReduce/109418) for specific configuration.

<span id="_1-使用前提"></span>
## Prerequisites


1. An E\-MapReduce (EMR) cluster with the Ranger service has been created. For detailed instructions, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For instructions on the Ranger UI login interface, see: [Ranger 概述---Ranger Admin UI 访问](https://docs.byteplus.com/docs/E-MapReduce/109411#_3-ranger-admin-ui-%E8%AE%BF%E9%97%AE) **.** 


<span id="_2-启用-ranger-spark-plugin"></span>
## Enable Ranger Spark Plugin

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current version of ranger\-spark\-plugin is not suitable for non\-interactive scenarios such as spark\-submit, which may prevent tasks from exiting. To run spark\-submit tasks, disable ranger\-spark\-plugin. To contact Volcano Engine technical support, <a href="https://console.volcengine.com/workorder/create/">submit a ticket</a>.</div>



1. In the cluster details, go to the service list, select Ranger service details, and on the service overview page, toggle the Spark Plugin switch to enable it.

2. The changes take effect after restarting the Spark service as prompted.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4818a24792727b11dda647763907f22a.png) </span>

<span id="_3-beeline-访问"></span>
## **Beeline access**

For details on how to use Spark, see [Quickstart](https://docs.byteplus.com/docs/undefined/69aa38f4e7d8cb052426cc57)

```shell
# spark 3.x
beeline -u jdbc:hive2://emr-master-1-1:10005 -n <user> -p <password>

# spark 2.x
spark-beeline -u jdbc:hive2://emr-master-1-1:10016 -n <username> -p <password>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The node domain naming conventions may differ between EMR versions, so the above "emr\-master\-1\-1" can be adjusted by referring to the EMR <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a> to make corresponding adjustments.</div>
