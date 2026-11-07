---
title: "DataExport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DataExport_v2"
---

<span id="overview"></span>
# Overview

Through the `CreateVikingdbTask` interface with `task_type=data_export`, batch export data from the specified Collection to TOS.

Before using, please authorize VikingDB cross\-service access to TOS: [Go to Authorization](https://console.volcengine.com/iam/service/attach_role/?ServiceName=ml_platform)

<span id="method-definition"></span>
# Method Definition

Python SDK initiates calls via `VIKINGDBApi().create_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|project_name | |str |No |The project to which the task belongs, corresponding to API field `ProjectName`. If not filled, it defaults to the SDK initialization configuration (usually `default`). |
|collection_name | |str |1 of 2 required |Collection name, corresponding to API field `CollectionName`, must match the dataset the task operates on. |
|resource_id | |str | |Collection resource ID, corresponding to API field `ResourceId`. At least one of `collection_name` or `resource_id` must be provided; it is recommended to pass both. |
|task_type | |str |Yes |Task type, corresponding to API field `TaskType`. Export tasks must be set to `data_export`. Other optional values include `data_import`, `filter_update`, `filter_delete`. |
|task_config | |TaskConfigForCreateVikingdbTaskInput |Yes |Detailed configuration for the export task, corresponding to API field `TaskConfig`. |
| |tos_path |str |Yes |TOS path, format: {bucket\-name}/{path}, note this is not a domain name. Corresponding to API field `TosPath`. |
| |file_type |str |No |File type, supports `json` or `parquet`. Corresponding to API field `FileType`, default value is `parquet`. |
| |export_all |bool |No |Whether to export all data, corresponding to API field `ExportAll`. When not filled or `False`, it exports data meeting `filter_conds` by default; when set to `True`, it forces export of all data, and `filter_conds` does not take effect; if `filter_conds` is not provided, all data will be exported regardless of the `ExportAll` setting. |
| |filter_conds |list[object] |No |Filter conditions (optional). If not filled, all data is exported by default. For usage reference: https://www.volcengine.com/docs/84313/1791133, corresponding to API field `FilterConds`. |
| |output_fields |list |No |Configure the list of fields to export. Defaults to all fields. |


<span id="response-parameters"></span>
## Response Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|task_id |str |Task ID, corresponding to API field `TaskId`. |
|message |str |Prompt message returned by the interface, corresponding to API field `Message`. |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

```python
import os
import volcenginesdkcore
import volcenginesdkvikingdb as vdb
from volcenginesdkvikingdb.api.vikingdb_api import VIKINGDBApi

configuration = volcenginesdkcore.Configuration()
configuration.ak = os.environ["VIKINGDB_AK"]
configuration.sk = os.environ["VIKINGDB_SK"]
configuration.region = os.environ["VIKINGDB_REGION"]
configuration.host = os.environ["VIKINGDB_HOST"]
configuration.scheme = "https"
volcenginesdkcore.Configuration.set_default(configuration)

client = VIKINGDBApi()

task_cfg = vdb.TaskConfigForCreateVikingdbTaskInput(
    file_type="parquet",
    export_all=True,
    tos_path="your-bucket/path/to/export.parquet",
)

request = vdb.CreateVikingdbTaskRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    task_type="data_export",
    task_config=task_cfg,
)
response = client.create_vikingdb_task(request)
print("task id:", response.task_id)
print("message:", response.message)
```


<span id="post-processing"></span>
## Post\-processing

<span id="_1-download-file-from-tos"></span>
### 1. Download File from TOS

```python
import tos

DOMAIN = "api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
TOS_ENDPOINT = "tos-ap-southeast-1.bytepluses.com"
REGION = "ap-southeast-1"
AK = "****"
SK = "****"
COLLECTION_NAME = "example"
BUCKET_NAME = "bucket_name"
TOS_DIR = "tos_dir"

def download(client, bucket_name, object_key, local_path):
    file_path = "{}/{}".format(local_path, object_key)
    try:
        client.get_object_to_file(bucket_name, object_key, file_path)
    except tos.exceptions.TosClientError as e:
        # Operation failed, catch client exception, usually due to invalid request parameters or network exceptions
        return 'fail with client error, message:{}, cause: {}'.format(e.message, e.cause)
    except tos.exceptions.TosServerError as e:
        return 'fail with server error : {}'.format(e)
    except Exception as e:
        return 'fail with unknown error: {}'.format(e)
    return ''
```


<span id="_2-parse-parquet-type-data"></span>
### 2. Parse Parquet Type Data

```python
import pyarrow.parquet as pq

def process_parquet(file_path):
    parquet_file = pq.ParquetFile(file_path)
    file_data_count = sum(parquet_file.metadata.row_group(i).num_rows for i in range(parquet_file.num_row_groups))
    schema = parquet_file.schema.to_arrow_schema()
    row_iterator = parquet_file.iter_batches(batch_size=100)
    # Iterate to read data
    for batch in row_iterator:
        df = batch.to_pandas()
        for index, row in df.iterrows():
            """
            do what you want
            """
            print(row)
    return ''

process_parquet("1.parquet")
```
