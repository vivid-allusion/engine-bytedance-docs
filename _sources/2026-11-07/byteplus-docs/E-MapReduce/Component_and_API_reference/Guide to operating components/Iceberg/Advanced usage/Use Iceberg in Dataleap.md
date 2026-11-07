---
title: "Use Iceberg in Dataleap"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_Iceberg_in_Dataleap"
---

<span id="38b2985a"></span>
## Spark

It is necessary to modify the parameter `spark.driver.extraClassPath` in the console and add the path to the Spark jars, such as /usr/lib/emr/current/spark3/jars/\* (please confirm that the path exists due to differences between versions). In addition, you need to add the relevant catalog parameters in spark\-default.conf or use the set command (see [Iceberg parameter configuration](https://docs.byteplus.com/docs/E-MapReduce/109285) for details).

<span id="2ac87ff8"></span>
## Flink

It is necessary to copy the Iceberg dependencies to the nodes in the cluster.

```SQL
cd /usr/lib/emr/current/flink 
-- Copy the dependencies required by Iceberg
cp /usr/lib/emr/current/iceberg/lib/iceberg-flink-runtime-*.jar  lib
```
