---
title: "deleteVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteVikingdbCollection_v2"
---

<span id="overview"></span>
# Overview

DeleteCollection is used to delete an already created Collection dataset.


* Deleting a Collection will permanently delete all data under the specified Collection, please proceed with caution.

* Before deleting a Collection, you must first delete all Indexes associated with the Collection in order to successfully delete the Collection.


<span id="method-definition"></span>
# Method Definition

Python SDK is called via `VIKINGDBApi().delete_vikingdb_collection(request)`, where `request` is of type `volcenginesdkvikingdb.DeleteVikingdbCollectionRequest`.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`, default value is default. |
|collection_name |str |One of two required |Name of the collection to delete, corresponds to API field `CollectionName`.<br><br><br>* Starts with a letter, can only contain letters, numbers, and underscores, length 1\-128.<br><br>* The server allows choosing between this and `resource_id`, but the current Python SDK requires `collection_name` to be filled in. |
|resource_id |str | |Collection resource ID, corresponds to API field `ResourceId`. Can be used in combination with `collection_name` to help with tracing on the control plane. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |str |success |Operation result description, corresponds to API field `Message`. |


<span id="example"></span>
# Example

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

request = vdb.DeleteVikingdbCollectionRequest(
    collection_name="sdk_demo_collection",
    project_name="default",
)
response = client.delete_vikingdb_collection(request)
print(response.message or "delete request finished")
```
