---
title: "Access Lance data on TOS using the Lance Python SDK"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Access_Lance_data_on_TOS_using_the_Lance_Python_SDK"
---

<span id="68004d2a"></span>
## Install Lance Python SDK

```Bash
pip install ve-pylance
```


<span id="e0f9b316"></span>
## Usage example

<span id="b1047ccd"></span>
### Read example

```Python
import lance
ds = lance.dataset(
    "s3://{PATH}",
    storage_options={
        "access_key_id": "<用户实际的AK>",
        "secret_access_key": "<用户实际的SK>",
        "aws_endpoint": "https://{bucket name}.{S3 Endpoint}.ivolces.com",
        "virtual_hosted_style_request": "true"
    }
)
print(ds.to_table().to_pandas())
```


**Parameter description**


* PATH: The object storage path, including the bucket name. For example: `s3://bucket1/test/lance.db`.

* AK/SK: Access key and secret key.

* aws_endpoint: The [S3 Endpoint](https://www.volcengine.com/docs/6349/107356) of TOS. The HTTPS protocol must be used. The endpoint path must include the bucket name and use VirtualHost mode.

   For example, in **North China 2**:

   * If running on Volcano Engine ECS, use the following endpoint address: https://bucket1.tos\-s3\-cn\-beijing.ivolces.com.

   * If running on a local machine, use the public address: https://bucket1.tos\-s3\-cn\-beijing.volces.com.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Here, <code>ivolces</code> means internal network access; <code>volces</code> means public network access.   </div>
   

* virtual_hosted_style_request: Must be True.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, TOS S3 addresses only support the <a href="https://www.volcengine.com/docs/6349/1288493">VirtualHost</a> method.</div>


<span id="987e78e3"></span>
### Write example

```Python
import lance
import pyarrow as pa

table = pa.Table.from_pylist([{"name": "Alice", "age": 20},
                              {"name": "Bob", "age": 30}])
schema = pa.schema([
        pa.field("name", pa.string()),
        pa.field("age", pa.int64()),
    ])

storage_options={
        "access_key_id": "<用户实际的AK>",
        "secret_access_key": "<用户实际的SK>",
        "aws_endpoint": "https://bucket1.tos-s3-cn-beijing.ivolces.com",
        "virtual_hosted_style_request": "true"
    }
lance.write_dataset(table, "s3://{PATH}", schema, storage_options=storage_options)
```
