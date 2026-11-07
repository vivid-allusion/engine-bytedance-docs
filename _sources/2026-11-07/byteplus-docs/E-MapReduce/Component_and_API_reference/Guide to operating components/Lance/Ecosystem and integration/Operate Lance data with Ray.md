---
title: "Operate Lance data with Ray"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operate_Lance_data_with_Ray"
---

<span id="60ee007e"></span>
## Preparation

This feature requires Ray version 2.46.0 or above provided by Volcano Engine to be installed.

<span id="7f96a07e"></span>
## Sample operation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For TOS access configuration, refer to the document <a href="https://www.volcengine.com/docs/6491/1359395">Access Lance data on TOS using the Lance Python SDK</a>.</div>


<span id="a5a64627"></span>
### Write data

<span id="47233ace"></span>
#### Writing in the new version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This operation applies to version 2.46.0 and later.</div>


In the new version, the `write_lance` method is integrated into the `ray.data.Dataset` object as a built\-in method.


* **Legacy implementation**: You need to import the `LanceDatasink` class from the `lance.ray.sink` module, instantiate it manually, and then use it.

* **New implementation**: No additional import or instantiation is required; you can call it directly through the `ray.data.Dataset` object.


```Python
import ray

# Initialize Ray
ray.init()

# Create Ray Dataset
ds = ray.data.range(10).map(
    lambda x: {"id": x["id"], "str": f"str-{x['id']}"}
)

# Use the write_lance method to write data in Lance format
ds.write_lance(
    path="s3://{PATH}",
    storage_options={
        "access_key_id": "{用户实际的AK}",
        "secret_access_key": "{用户实际的SK}",
        "aws_endpoint": "https://{bucket name}.{S3 Endpoint}.ivolces.com",
        "virtual_hosted_style_request": "true"
    },
    mode='create',
    max_rows_per_file=8192
)

print("数据已成功写入 Lance 格式。")
```


Lance writing in Ray is encapsulated as LanceDatasink. You can construct a LanceDatasink object and schedule write_datasink to complete the write operation.

**write_lance parameters**


|Parameter |Meaning |Sample |
|---|---|---|
|path |Dataset path |Use "s3://{PATH}" for object address, "./db" for local address |
|schema |Dataset structure |Optional parameter, defaults to empty, pass in pyarrow.Schema format |
|mode |Dataset mode |Optional parameter, three options: "create", "append", "overwrite". Defaults to create, which means creating a dataset |
|max_rows_per_file |Number of rows per Lance file |Optional parameter, defaults to 1M rows. If the Lance file is too large, you can lower this value |
|storage_options |Object storage configuration |Refer to TOS access configuration |


<span id="28ae5f1d"></span>
#### Writing in the legacy version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This operation applies to version 2.44.0 and earlier.</div>


```Python
import ray
from lance.ray.sink import LanceDatasink

ray.init()

sink = LanceDatasink(
       uri="s3://{PATH}",
       storage_options={
         "access_key_id": "{用户实际的AK}",
         "secret_access_key": "{用户实际的SK}",
         "aws_endpoint": "https://{bucket name}.{S3 Endpoint}.ivolces.com",
         "virtual_hosted_style_request": "true"
       }
)
ray.data.range(10).map(
    lambda x: {"id": x["id"], "str": f"str-{x['id']}"}
).write_datasink(sink)
```


Writing Lance data with Ray is encapsulated as LanceDatasink. You can construct a LanceDatasink object and schedule write_datasink to complete the write operation.

**Note**


|Parameter |Meaning |Sample |
|---|---|---|
|uri |Dataset path |Use "s3://{PATH}" for object address, "./db" for local address |
|schema (optional) |Dataset structure |Defaults to empty, pass in pyarrow.Schema format |
|mode (optional) |Dataset mode |Three options: "create", "append", "overwrite". Defaults to create, which means creating a dataset |
|max_rows_per_file (optional) |Number of rows per Lance file |Defaults to 1M rows. If you find the Lance file is too large, you can lower this value. |
|storage_options |Object storage configuration |See [Accessing Lance data on TOS using the Lance Python SDK](https://www.volcengine.com/docs/6491/1359395) |


<span id="75a1b539"></span>
### Read data

```Python
import ray
ds = ray.data.read_lance( 
    uri="s3://hzw/tpcds/backup/store_sales_10g.lance",
    storage_options={
             "access_key_id": "{用户实际的AK}",
             "secret_access_key": "{用户实际的SK}",
             "aws_region": "shanghai",
             "aws_endpoint": "https://{bucket name}.{S3 Endpoint}.ivolces.com",
             "virtual_hosted_style_request": "true"
        },
    concurrency=1
)
ds.take(10)
```


**Note**


|Parameter |Meaning |Example |
|---|---|---|
|uri |Dataset path |Use "s3://{PATH}" for object addresses, and "./db" for local addresses |
|columns |Read only specific columns from the Lance data |By default, all columns are read |
|filter |Filter condition |The filter predicate will be pushed down to Lance, reducing the amount of scanned data |
|storage_options |Object storage configuration |See [Accessing Lance data on TOS using the Lance Python SDK](https://www.volcengine.com/docs/6491/1359395) |
|scanner_options |Scanning options |You can set `batch_size` and other options here |
|concurrency |Concurrency level |Number of concurrent reads for Lance data |
|override_num_blocks |Number of data blocks |Controls the number of output data blocks when reading from the data source. Specifically, it specifies the number of output blocks generated during data reading, which is equivalent to the number of read tasks created |


<span id="a71a8adf"></span>
### Example: Parquet to Lance conversion

Before use, ensure that pyarrow and s3fs are installed to facilitate reading s3 with Ray. If you are unsure, refer to Ray's [documentation](https://docs.ray.io/en/latest/ray-overview/getting-started.html).

Taking **North China 2** as an example:


* If running on Volcano Engine ECS, use the following Endpoint address: https://bucket1.tos\-s3\-cn\-beijing.ivolces.com.

* If running on a local machine, use the public address: https://bucket1.tos\-s3\-cn\-beijing.volces.com.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Here, <code>ivolces</code> represents intranet access, and <code>volces</code> represents access from the public network.</div>


```Python
import ray
import pyarrow.fs as fs
# Initialize Ray
ray.init()
# 1. Configure PyArrow FileSystem for reading data
#    Caution: The endpoint and configuration here are used for read operations
read_fs = fs.S3FileSystem(
    access_key='{用户实际的AK}',
    secret_key='{用户实际的SK}',
    region='cn-beijing',
    endpoint_override='https://{S3 Endpoint}.volces.com',
    force_virtual_addressing=True
)
# 2. Read Parquet data from S3
ds = ray.data.read_parquet("s3://bucket1/{parquet_PATH}/", filesystem=read_fs)

# 3. Use write_lance to directly write data
#    The original LanceDatasink parameters are passed directly to the write_lance method
ds.write_lance(
    path="s3://{PATH}",
    storage_options={
        "access_key_id": "{用户实际的AK}",
        "secret_access_key": "{用户实际的SK}",
        "aws_region": "cn-beijing",
        # Caution: The endpoint and configuration here are used for write operations
        "aws_endpoint": "https://{bucket name}.{S3 Endpoint}.volces.com",
        "virtual_hosted_style_request": "true"
    }, 
     max_concurrent_tasks=10  # The 'concurrency' parameter is now replaced by 'max_concurrent_tasks'
)

print("数据已成功转换为 Lance 格式并写入目标位置！")
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To access TOS, you need to provide Arrow's filesystem. The configuration statement for fs.S3FileSystem differs from that for LanceDatasink as follows: the bucket prefix must not be added in <code>endpoint_override</code>, whereas it must be added in Lance's <code>aws_endpoint</code>.</div>
