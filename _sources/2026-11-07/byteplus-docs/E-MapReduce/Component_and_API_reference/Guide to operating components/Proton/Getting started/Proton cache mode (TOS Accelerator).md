---
title: "Proton cache mode (TOS Accelerator)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/proton_cache_mode_tos_accelerator"
---

This article introduces how to use Volcano Engine E\-MapReduce (EMR) clusters with Proton and TOS Accelerator to implement a storage\-compute separation cache mode.

<span id="77a8b600"></span>
# TOS\-side configuration

<span id="60970dbf"></span>
## Configure the TOS Accelerator

<span id="06287539"></span>
### Configure the access point

In "Access Point" — "Single\-region Access Point", click "[Create single-region access point](https://www.volcengine.com/docs/6349/1863311?lang=zh)".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b898b658fbf44e84b38f0431744c452d~tplv-goo7wpa0wc-image.image) </span>

It is recommended to name the access point in the format {bucket}\-accelerator. In the bucket list, select the bucket to bind to the access point. This bucket will be accelerated by the accelerator in the future.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffb5ef1cc4594726b4b26304147b7274~tplv-goo7wpa0wc-image.image) </span>

<span id="3ac5a07f"></span>
### Configure the accelerator


1. Select "TOS Accelerator" and click "[Create TOS Accelerator](https://www.volcengine.com/docs/6349/1580777?lang=zh)".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/634ccc96efd648b6be0300d21a2aa437~tplv-goo7wpa0wc-image.image) </span>

2. Create the TOS Accelerator. Select the region that matches the access point just created. It is recommended to choose the same availability zone as the EMR cluster. For the acceleration scope, select the single\-region access point. For the acceleration domain name, select the access point just created. To accelerate multiple buckets, you can continue to add rows below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/751b99eaca3e42ee8d9a7e130ef152cf~tplv-goo7wpa0wc-image.image) </span>

3. After selecting the acceleration domain name, a new input box will pop up for configuring the acceleration policy and acceleration path. Choose as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48c4e23c88a14354a5bf14fa9a405d5e~tplv-goo7wpa0wc-image.image) </span>


<span id="d58bd681"></span>
## Configure TOS authentication

Proton access to the TOS Accelerator requires TOS authentication. Three authentication methods are supported: Assume Role, static AKSK, and environment variable AKSK. For details, refer to [Hadoop Using Proton with E-MapReduce (Volcano Engine)](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE).

<span id="1aed8640"></span>
# Proton\-side configuration

<span id="27f17096"></span>
## Use hadoop shell command to access the TOS Accelerator

The TOS Accelerator must be accessed using the access point domain name. In the storage\-compute separation architecture, the access point domain name is mapped to a special cluster name. For example, the original file path is `tos://{bucket_name}/datawarehouse/database/table`, and the accelerator access point path is `tos://{access_point_name}/datawarehouse/database/table`.


1. Go to the TOS Accelerator page to view its acceleration domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77ccb6144d974b3885a00d00e6377e81~tplv-goo7wpa0wc-image.image) </span>

   For example:

   * Original path: `bucket-accelerator-0197ca6c5e44759faf****-tosalias.tos-cn-beijing.ivolces.com`.

   * The format of the acceleration domain name is `{accelerator_name}.tos-{region}. ivolces.com`.

   * The accelerator name in the above acceleration domain name is `bucket-accelerator-0197ca6c5e44759faf****-tosalias`.

2. Use hadoop shell command to access the TOS Accelerator domain name. The command is as follows.

   ```Python
   hadoop fs -ls tos://bucket-accelerator-0197ca6c5e44759faf****-tosalias/
   ```
   


<span id="e634d2f5"></span>
## Use TOS Accelerator to accelerate Hive tables

<span id="372dc238"></span>
### Modify the Hive warehouse

Modify the warehouse path in HMS so that the default location for newly created databases points to the accelerator. The following configuration items need to be modified on the EMR management page. After modification, restart Hive MetaStore and Hive Server2.


* {bucket}: Original bucket name.

* {bucket\-accelerator}: Accelerator name. The accelerator name can be obtained from the acceleration domain name. For how to obtain it, see "Using hadoop shell commands to access the TOS accelerator".


```Python
// 旧
hive.metastore.warehouse.dir=tos://{bucket}/warehouse/managed
hive.metastore.warehouse.external.dir=tos://{bucket}/warehouse/external

// 新
hive.metastore.warehouse.dir=tos://{bucket-accelerator}/warehouse/managed
hive.metastore.warehouse.external.dir=tos://{bucket-accelerator}/warehouse/external
```


<span id="cea160ca"></span>
### Modify the Spark warehouse

Modify the Spark warehouse path so that when creating a new database in Spark, the default location of the new database points to the accelerator. The following configuration items need to be modified on the EMR management page.

```Python
// 旧
spark.sql.warehouse.dir=tos://{bucket}/warehouse/managed

// 新
spark.sql.warehouse.dir=tos://{bucket-accelerator}/warehouse/managed
```


<span id="af7e1141"></span>
### Modify existing databases

Modify the location of existing databases to point to the accelerator, so that the default location of newly created tables will point to the accelerator. Start the Hive terminal and run the following commands.

```Python
ALTER DATABASE {YOUR_DB} SET LOCATION 'tos://{bucket-accelerator}/warehouse/managed/{your.db}/'
```


<span id="8b95e6f8"></span>
### Modify existing tables

Modify the location of existing tables to point to the accelerator. Start the Hive terminal and run the following commands.

```Python
ALTER TABLE {YOUR_TBL} SET LOCATION 'tos://{bucket-accelerator}/warehouse/managed/{your.db}/{your_table}'
```
