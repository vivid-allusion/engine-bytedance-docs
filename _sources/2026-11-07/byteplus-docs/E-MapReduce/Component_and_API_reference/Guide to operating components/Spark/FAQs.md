---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/spark_faqs"
---

<span id="spark提交任务找不到对应jar，报错classnotfoundexception。"></span>
## When submitting a Spark task, the corresponding JAR cannot be found, resulting in a ClassNotFoundException error.


* Description: The task dependency JAR is copied to `/opt/emr/current/spark/jars/`, but a ClassNotFoundException error still occurs.

* Root cause: By default, the cluster is configured with spark.yarn.archive, which reads the tar.gz package on HDFS `hdfs://master-1-1.emr-xxx.cn-beijing.emr-volces.com:8020/user/spark/spark-jars.tar.gz`

* Solution:

   * Method 1 Set spark.yarn.archive to an empty value. In this case, the JARs in the `/opt/emr/current/spark/jars/` directory will be read.

   * Method 2 Compress the spark\-jars.tar.gz package and replace the package in the HDFS directory. Compression command: `cd /opt/emr/current/spark/jars/ && tar -zcvf /opt/new/spark-jars.tar.gz --exclude=spark-jars.tar.gz \*`
