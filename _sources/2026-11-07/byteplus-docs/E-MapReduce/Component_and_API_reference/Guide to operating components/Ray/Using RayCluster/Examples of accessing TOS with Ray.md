---
title: "Examples of accessing TOS with Ray"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Examples_of_accessing_TOS_with_Ray"
---

In Ray, you can access TOS object storage data using the [pyarrow.fs.S3FileSystem](https://arrow.apache.org/docs/python/generated/pyarrow.fs.S3FileSystem.html) method or the [HDFS protocol](https://arrow.apache.org/docs/python/generated/pyarrow.fs.HadoopFileSystem.html). This section provides examples of both methods.

<span id="采用pyarrow-fs-s3filesystem方式访问tos示例"></span>
## Accessing TOS using pyarrow.fs.S3FileSystem


1. Define the FileSystem for object storage and specify the access_key, secret_key, and endpoint_override information.

   ```python
   # Configure the correct ak, sk, and endpoint:
   import ray
   from pyarrow import fs
   s3 = fs.S3FileSystem(access_key=xxxx, secret_key=xxxx,endpoint_override='tos-s3-cn-beijing.ivolces.com', force_virtual_addressing=True)
   ```
   


In the example: `access_key` and `secret_key` are the Access Key ID and Secret Access Key for accessing TOS object storage, which can be obtained from the [key list](https://console.volcengine.com/iam/keymanage/); `endpoint_override` is the S3 Endpoint value of the TOS access domain name (see [regions and access domain names](https://www.volcengine.com/docs/6349/107356)), and should be specified as appropriate.


2. Store data in object storage:

   ```python
   ds = ray.data.range(100)
   ds.write_csv(path = "{bucket_name}/test_tos_data", filesystem = s3)
   ```
   

   In the example, `{bucket_name}` is the name of the TOS bucket.

3. Read the CSV file stored in object storage and print one row.

   ```python
   ds = ray.data.read_csv(paths = "{bucket_name}/test_tos_data", filesystem = s3)
   ds.show(limit=1)
   ```
   


<span id="采用hdfs协议方式访问tos示例"></span>
## Accessing TOS using the HDFS protocol


1. Define the pyarrow.fs.HadoopFileSystem object and specify the *endpoint*, *access\-key\-id*, *secret\-access\-key*, and bucket_name information.

   ```python
   from pyarrow import fs
   import ray
   ray.init()
   
   hdfs_fs = fs.HadoopFileSystem(host='tos://{bucket_name}', extra_conf={
          "fs.AbstractFileSystem.tos.impl":"io.proton.tos.TOS",
          "fs.tos.impl":"io.proton.fs.RawFileSystem",
          "fs.tos.endpoint":"tos-cn-beijing.ivolces.com",
          "fs.tos.credentials.provider":"io.proton.common.object.tos.auth.DefaultCredentialsProviderChain",
          "fs.tos.access-key-id":"xxxx",
          "fs.tos.secret-access-key":"xxxx",
          })
   ```
   

   In the example: `fs.tos.access-key-id` and `fs.tos.secret-access-key` are the Access Key ID and Secret Access Key for accessing TOS object storage, which can be obtained from the [key list](https://console.volcengine.com/iam/keymanage/); `fs.tos.endpoint` is the Endpoint value of the TOS access domain name; `{bucket_name}` is the name of the TOS bucket. These should be specified as appropriate.

2. Store data in object storage

   ```python
   ds = ray.data.range(100)
   ds.write_csv(path = "/test_data", filesystem = hdfs_fs)
   ```
   

3. Read the CSV file stored in object storage and print one row.

   ```python
   ds = ray.data.read_csv(paths = "/test_data", filesystem = hdfs_fs)
   ds.show(limit=1)
   ```
