---
title: "listVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbCollection_v2"
---

<span id="overview"></span>
# Overview

The ListVikingdbCollection interface is used to query the Collection list under the current project, supporting pagination and name keyword filtering.

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().list_vikingdb_collection(request)`, where `request` is of type `volcenginesdkvikingdb.ListVikingdbCollectionRequest`.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|project_name |str |No |Project name, corresponding to API field `ProjectName`, default is default. |
|page_size |int |No |Pagination size, corresponding to API field `PageSize`, value range 1\-100, default 10. |
|page_number |int |No |Pagination page number, corresponding to API field `PageNumber`, starting from 1. |
|filter |FilterForListVikingdbCollectionInput |No |Filter conditions, corresponding to API field `Filter`. |



* FilterForListVikingdbCollectionInput



|Parameter |Type |Required |Description |
|---|---|---|---|
|collection_name_keyword |str |No |Collection name keyword, corresponding to API field `CollectionNameKeyword`, used for fuzzy search. |


<span id="return-parameters"></span>
# Return Parameters

The interface returns `ListVikingdbCollectionResponse`, containing pagination information and collection list.


|Parameter |Type |Description |
|---|---|---|
|total_count |int |Total number of collections, corresponding to API field `TotalCount`. |
|page_number |int |Current page number, corresponding to API field `PageNumber`. |
|page_size |int |Number of items returned on this page, corresponding to API field `PageSize`. |
|collections |list[CollectionForListVikingdbCollectionOutput] |Collection details list, corresponding to API field `Collections`. |



* CollectionForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|collection_name |str |Collection name, corresponding to API field `CollectionName`. |
|project_name |str |Associated project, corresponding to API field `ProjectName`. |
|resource_id |str |Collection ID, corresponding to API field `ResourceId`. |
|description |str |Collection description, corresponding to API field `Description`. |
|create_time |str |Creation time (RFC3339), corresponding to API field `CreateTime`. |
|update_time |str |Update time, corresponding to API field `UpdateTime`. |
|update_person |str |Last operator, corresponding to API field `UpdatePerson`. |
|enable_keywords_search |bool |Whether keyword search is enabled, corresponding to API field `EnableKeywordsSearch`. |
|index_count |int |Number of indexes, corresponding to API field `IndexCount`. |
|index_names |list[str] |Index name list, corresponding to API field `IndexNames`. |
|fields |list[FieldForListVikingdbCollectionOutput] |Field list, corresponding to API field `Fields`. |
|collection_stats |CollectionStatsForListVikingdbCollectionOutput |Statistical information, corresponding to API field `CollectionStats`. |
|tags |list[TagForListVikingdbCollectionOutput] |Tag information, corresponding to API field `Tags`. |
|vectorize |VectorizeForListVikingdbCollectionOutput |Vectorization configuration, corresponding to API field `Vectorize`. |



* FieldForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|field_name |str |Field name, corresponding to API field `FieldName`. |
|field_type |str |Field type, corresponding to API field `FieldType`. |
|is_primary_key |bool |Whether it is a primary key, corresponding to API field `IsPrimaryKey`. |
|dim |int |Vector dimension, corresponding to API field `Dim`. |
|default_value |object |Default value, corresponding to API field `DefaultValue`. |



* CollectionStatsForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|data_count |int |Number of documents in the collection, corresponding to API field `DataCount`. |
|data_storage |int |Storage capacity (Bytes), corresponding to API field `DataStorage`. |



* TagForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|key |str |Tag key, corresponding to API field `Key`. |
|value |str |Tag value, corresponding to API field `Value`. |



* VectorizeForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|dense |DenseForListVikingdbCollectionOutput |Dense vectorization configuration, corresponding to API field `Dense`, field meaning is the same as the Get interface. |
|sparse |SparseForListVikingdbCollectionOutput |Sparse vectorization configuration, corresponding to API field `Sparse`. |


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

request = vdb.ListVikingdbCollectionRequest(
    project_name="default",
    page_number=1,
    page_size=10,
    filter=vdb.FilterForListVikingdbCollectionInput(collection_name_keyword="demo"),
)
response = client.list_vikingdb_collection(request)

print("total:", response.total_count)
for item in response.collections or []:
    print(item.collection_name, item.resource_id)
```
