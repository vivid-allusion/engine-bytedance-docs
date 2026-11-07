---
title: "getVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbCollection_v2"
---

<span id="overview"></span>
# Overview

The GetVikingdbCollection interface is used to query the metadata, field configuration, and vectorization settings of a specified Collection.

<span id="method-definition"></span>
# Method Definition

Python SDK is called via `VIKINGDBApi().get_vikingdb_collection(request)`, where `request` is of type `volcenginesdkvikingdb.GetVikingdbCollectionRequest`.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`, default value is default. |
|collection_name |str |Either/or |Collection name, corresponds to API field `CollectionName`. Must start with a letter, can only contain letters/numbers/underscores, length 1\-128. |
|resource_id |str |Either/or<br><br>Either/or |Collection resource ID, corresponds to API field `ResourceId`. Can be used as an alternative to `collection_name` or both can be provided to ensure precise positioning. |


<span id="response-parameters"></span>
# Response Parameters

A successful response returns `GetVikingdbCollectionResponse`, containing the following fields:


|Parameter |Type |Description |
|---|---|---|
|project_name |str |Project the collection belongs to, corresponds to API field `ProjectName`. |
|resource_id |str |Collection resource ID, corresponds to API field `ResourceId`. |
|collection_name |str |Collection name, corresponds to API field `CollectionName`. |
|description |str |Collection description, corresponds to API field `Description`. |
|create_time |str |Creation time (RFC3339), corresponds to API field `CreateTime`. |
|update_time |str |Last update time, corresponds to API field `UpdateTime`. |
|update_person |str |Last operator, corresponds to API field `UpdatePerson`. |
|enable_keywords_search |bool |Whether keyword search is enabled, corresponds to API field `EnableKeywordsSearch`. |
|index_count |int |Number of indexes under the collection, corresponds to API field `IndexCount`. |
|index_names |list[str] |List of index names, corresponds to API field `IndexNames`. |
|fields |list[FieldForGetVikingdbCollectionOutput] |List of field definitions, corresponds to API field `Fields`. |
|collection_stats |CollectionStatsForGetVikingdbCollectionOutput |Data volume statistics, corresponds to API field `CollectionStats`. |
|vectorize |VectorizeForGetVikingdbCollectionOutput |Vectorization configuration, corresponds to API field `Vectorize`. |



* FieldForGetVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|field_name |str |Field name, corresponds to API field `FieldName`. |
|field_type |str |Field type, corresponds to API field `FieldType`. |
|dim |int |When field type is `vector`, represents dense vector dimension, corresponds to API field `Dim`. |
|is_primary_key |bool |Whether it is a primary key, corresponds to API field `IsPrimaryKey`. Only string / int64 fields can be set as primary keys. |
|default_value |object |Field default value, corresponds to API field `DefaultValue`. |



* CollectionStatsForGetVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|data_count |int |Number of data entries in the collection, corresponds to API field `DataCount`. |
|data_storage |int |Collection storage usage (Bytes), corresponds to API field `DataStorage`. |



* VectorizeForGetVikingdbCollectionOutput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|dense |VectorizeForGetVikingdbCollectionOutput |Yes |Dense vectorization configuration, corresponds to API field `Dense`, used to specify embedding model, dimensions, and input fields. |
|sparse |SparseForGetVikingdbCollectionOutput |No |Sparse vectorization configuration, corresponds to API field `Sparse`. |



* DenseForGetVikingdbCollectionOutput and SparseForGetVikingdbCollectionOutput parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|model_name |str |Yes |Model name, corresponds to API field `ModelName`. See embedding model list below for optional values. |
|model_version |str |No |Model version, corresponds to API field `ModelVersion`. Required for Doubao series models, defaults to `default` for bge series. |
|dim |int |No |Dense vector dimension. See embedding model list for dimensions supported by each model. |
|text_field |str |No |Text vectorization field name, corresponds to API field `TextField`. |
|image_field |str |No |Image vectorization field name, corresponds to API field `ImageField`. |
|video_field |str |No |Video vectorization field name, corresponds to API field `VideoField`. |


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

request = vdb.GetVikingdbCollectionRequest(
    collection_name="sdk_demo_collection",
    project_name="default",
)
response = client.get_vikingdb_collection(request)

print("collection:", response.collection_name)
print("fields:", [f.field_name for f in (response.fields or [])])
if response.collection_stats:
    print("doc count:", response.collection_stats.data_count)
```
