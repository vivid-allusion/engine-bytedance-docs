---
title: "updateVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbCollection_v2"
---

<span id="overview"></span>
# Overview

update_vikingdb_collection is used to append fields to a specified Collection dataset.

Collections support adding new fields; already defined fields cannot be modified, only the dataset description (description) can be modified.

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().update_vikingdb_collection(request)`, where `request` is of type `volcenginesdkvikingdb.UpdateVikingdbCollectionRequest`.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is UpdateVikingdbCollectionRequest, with parameters shown in the table below.


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`, defaults to default. |
|collection_name |str |At least one must be filled |Collection name, corresponds to API field `CollectionName`. Starts with a letter, can only contain letters, numbers, and underscores, length 1\-128. At least one of `collection_name` and `resource_id` must be filled, both can be filled simultaneously. |
|resource_id |str | |Collection resource ID, corresponds to API field `ResourceId`. At least one of `resource_id` and `collection_name` must be filled, filling both is recommended for accuracy. |
|description |str |No |Collection description, corresponds to API field `Description`, maximum 65535 bytes. |
|fields |list[FieldForUpdateVikingdbCollectionInput] |Yes |List of new fields, corresponds to API field `Fields`. Maximum 128 total fields per collection, only appending new fields is supported. |



* Field parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|field_name |str |Yes |New field name, corresponds to API field `FieldName`. Must start with a letter, length 1\-128. |
|field_type |str |Yes |Field type, corresponds to API field `FieldType`, supports vector/sparse_vector/string/int64/float32/bool/list/list/text/image/video/date_time/geo_point. |
|default_value |object |No |Default value configuration, corresponds to API field `DefaultValue`. vector/sparse_vector/text/image/video types not supported. |
|dim |int |No |Vector dimension, corresponds to API field `Dim`. vector field must be set to 4\-4096 and be a multiple of 4. |
|is_primary_key |bool |No |Whether to set as primary key, corresponds to API field `IsPrimaryKey`, only string/int64 supported. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |str |success |Operation result description, corresponds to API field `Message`. |


<span id="example"></span>
## Example

<span id="request-parameters"></span>
## Request Parameters

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

request = vdb.UpdateVikingdbCollectionRequest(
    collection_name="sdk_demo_collection",
    description="append new fields",
    fields=[
        vdb.FieldForUpdateVikingdbCollectionInput(
            field_name="new_tag",
            field_type="string",
        ),
        vdb.FieldForUpdateVikingdbCollectionInput(
            field_name="extra_score",
            field_type="float32",
        ),
    ],
)
response = client.update_vikingdb_collection(request)
print(response.message or "update submitted")
```
