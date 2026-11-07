---
title: "Access non-TOS schemes in Spark"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Access_non-TOS_schemes_in_Spark"
---

When storage metadata uses s3, s3a, or other non\-TOS schemes, and the data files are stored on TOS, it is recommended to use Proton to enable access to non\-TOS schemes in serverless scenarios. This article provides core configuration examples.

<span id="7271621b"></span>
# Configuration requirements

```Python
set spark.hadoop.fs.{scheme}.endpoint=http://tos-{region}.ivolces.com;
set spark.hadoop.fs.{scheme}.impl=io.proton.fs.ProtonFileSystem;
set spark.hadoop.fs.AbstractFileSystem.{scheme}.impl=io.proton.fs.ProtonFS;
set spark.hadoop.proton.objectstorage.{scheme}.impl=io.proton.common.object.tos.TOS;
set `spark.hadoop.fs.{scheme}.access-key-id`=xxxxxx;
set `spark.hadoop.fs.{scheme}.secret-access-key`=xxxxxx;

//如果是s3a，proton有重名配置的兼容性问题，需要额外加下面两个参数覆盖core-default.xml中的默认值：
set fs.s3a.multipart.size=65536;
set fs.s3a.multipart.threshold=131072;
```


You need to modify the following configuration parameters as needed:


1. endpoint: Change to the TOS endpoint address corresponding to the s3 or s3a protocol

2. access\-key\-id, secret\-access\-key: Change to the access keys (AK/SK) for TOS


<span id="02b4578c"></span>
# Configuration example

The following provides a complete configuration example using region: North China, scheme: s3a, and storage location: tos.

```Python
set spark.hadoop.fs.s3a.endpoint=http://tos-cn-beijing.ivolces.com;
set spark.hadoop.fs.s3a.impl=io.proton.fs.ProtonFileSystem;
set spark.hadoop.fs.AbstractFileSystem.s3a.impl=io.proton.fs.ProtonFS;
set spark.hadoop.proton.objectstorage.s3a.impl=io.proton.common.object.tos.TOS;
set `spark.hadoop.fs.s3a.access-key-id`=xxxxxx;
set `spark.hadoop.fs.s3a.secret-access-key`=xxxxxx;
set fs.s3a.multipart.size=65536;
set fs.s3a.multipart.threshold=131072;
```
