---
title: "Querying data using Hue"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Querying_data_using_Hue"
---

This article introduces how to query data using Hue.

<span id="dbd1c19d"></span>
## 1 Prerequisites


1. An EMR cluster with the Hue component service has been created. For details, see [Create a cluster (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. To access the cluster link, you need to bind an elastic public IP to the ECS instance. For public network operations, see [Bind public IP](https://www.volcengine.com/docs/6401/68687), and for other operations, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

3. In **Cluster details \> Access link \> Quick configuration of server ports**, you must add the source address and corresponding port to the allowlist to continue accessing.


<span id="7c8ee7df"></span>
## 2 Log in to the Hue UI


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, go to **Cluster list \> Cluster name details \> Access link,**  and click the HUE UI access link to enter.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_499ca1b2f911ae1e65a36610712bdd10.png) </span>

3. Enter the Hue login username and password in the window.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Hue has integrated LDAP authentication by default, and users can log in using existing accounts in LDAP. For first\-time login, you need to add a user. For detailed instructions, please refer to: <a href="https://docs.byteplus.com/docs/E-MapReduce/105426#_1-%E7%94%A8%E6%88%B7%E7%AE%A1%E7%90%86">1 User management</a>.</div>


<span id="b384c681"></span>
## 3 SQL query


1. In the left navigation bar, you can select installed engines such as Hive, SparkSQL, Presto, and Trino in Editor.

2. In the notebook editing box on the right, edit and execute relevant SQL statements and view the results.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b781e784a8e486fccb1e7e413715fec9.png) </span>


<span id="dfe87cd7"></span>
## 4 Submit Spark jobs locally

To upload a local file to the Hadoop cluster for Spark computation, simply perform a few operations in the Hue interface to view the computation results. For example, to calculate the value of pi:


1. Prepare the local file demo.py:

   ```python
   #
   # Licensed to the Apache Software Foundation (ASF) under one or more
   # contributor license agreements. See the NOTICE file distributed with
   # this work for additional information regarding copyright ownership.
   # The ASF licenses this file to You under the Apache License, Version 2.0
   # (the "License"); you may not use this file except in compliance with
   # the License. You may obtain a copy of the License at
   #
   #    http://www.apache.org/licenses/LICENSE-2.0
   #
   # Unless required by applicable law or agreed to in writing, software
   # distributed under the License is distributed on an "AS IS" BASIS,
   # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   # See the License for the specific language governing permissions and
   # limitations under the License.
   #
   
   import sys
   from random import random
   from operator import add
   
   from pyspark.sql import SparkSession
   
   
   if __name__ == "__main__":
       """
           Usage: pi [partitions]
       """
       spark = SparkSession\
           .builder\
           .appName("PythonPi")\
           .getOrCreate()
   
       partitions = int(sys.argv[1]) if len(sys.argv) > 1 else 2
       n = 100000 * partitions
   
       def f(_):
           x = random() * 2 - 1
           y = random() * 2 - 1
           return 1 if x ** 2 + y ** 2 <= 1 else 0
   
       count = spark.sparkContext.parallelize(range(1, n + 1), partitions).map(f).reduce(add)
       print("Pi is roughly %f" % (4.0 * count / n))
   
       spark.stop()
   ```
   

2. In the left navigation bar, select Spark Submit Python in Editor and click to enter the upload interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f77462801dc90ca7cb1f6cd8ebd35ce.png) </span>

3. Upload the demo.py file from your local machine

   1. Click the file entry.

   2. Click the **Upload a file** button and select the local demo.py file to upload.

   3. Click the uploaded file to add it to Path.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e21778a773d50352ab9d2a308144565.png) </span>

4. After uploading the file, click the execute button on the left, and Spark will start running the job.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e9b6379a691df1f79a2517f03c9a823.png) </span>

5. After the job runs successfully, click and enter the Jobs interface from the left navigation bar to see the demo job and view the computation results.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fd097bb202da2ae231738276e1a1b60.png) </span>

6. Click the application to view details, including the output result of the computation (the approximate value of Pi).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_612b87c58f78f82707059a2bc114c678.png) </span>
