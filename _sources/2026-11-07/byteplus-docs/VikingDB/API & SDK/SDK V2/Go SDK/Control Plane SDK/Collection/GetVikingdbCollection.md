---
title: "GetVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/GetVikingdbCollection"
---

<span id="overview"></span>
# Overview

The GetVikingdbCollection interface is used to query the metadata, field configuration, and vectorization settings of a specified Collection.

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `GetVikingdbCollection(input)` method to initiate a collection query request. The input parameter type is `vikingdb.GetVikingdbCollectionInput`, which includes query conditions such as project name and CollectionName/ResourceId.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |string |No |Project name, corresponding to API field `ProjectName`. Default value is default. |
|CollectionName |string |1 of 2 required |Collection name, corresponding to API field `CollectionName`. Must start with a letter, can only contain letters, numbers, and underscores, with a length of 1\-128 characters. |
|ResourceId |string | |Collection resource ID, corresponding to API field `ResourceId`. Can be used as an alternative to `CollectionName` or both can be passed together to ensure precise location. |


<span id="response-parameters"></span>
# Response Parameters

A successful response returns `GetVikingdbCollectionResponse`, which contains the following fields:


|Parameter |Type |Description |
|---|---|---|
|ProjectName |string |The project to which the collection belongs, corresponding to API field `ProjectName`. |
|ResourceId |string |Collection resource ID, corresponding to API field `ResourceId`. |
|CollectionName |string |Collection name, corresponding to API field `CollectionName`. |
|Description |string |Collection description, corresponding to API field `Description`. |
|CreateTime |string |Creation time (RFC3339), corresponding to API field `CreateTime`. |
|UpdateTime |string |Last update time, corresponding to API field `UpdateTime`. |
|UpdatePerson |string |Last operator, corresponding to API field `UpdatePerson`. |
|EnableKeywordsSearch |bool |Whether keyword search is enabled, corresponding to API field `EnableKeywordsSearch`. |
|IndexCount |int |Number of indexes under the collection, corresponding to API field `IndexCount`. |
|IndexNames |[]string |List of index names, corresponding to API field `IndexNames`. |
|Fields |[]FieldForGetVikingdbCollectionOutput |List of field definitions, corresponding to API field `Fields`. |
|CollectionStats |CollectionStatsForGetVikingdbCollectionOutput |Data volume statistics, corresponding to API field `CollectionStats`. |
|Vectorize |VectorizeForGetVikingdbCollectionOutput |Vectorization configuration, corresponding to API field `Vectorize`. |



* FieldForGetVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|FieldName |string |Field name, corresponding to API field `FieldName`. |
|FieldType |string |Field type, corresponding to API field `FieldType`. |
|Dim |int |When the field type is vector, it represents the dimension of the dense vector, corresponding to API field `Dim`. |
|IsPrimaryKey |bool |Whether it is a primary key, corresponding to API field `IsPrimaryKey`. Only string / int64 fields can be set as primary keys. |
|DefaultValue |interface{} |Field default value, corresponding to API field `DefaultValue`. |



* CollectionStatsForGetVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|DataCount |int |Number of data entries in the collection, corresponding to API field `DataCount`. |
|DataStorage |int |Storage occupied by the collection (in Bytes), corresponding to API field `DataStorage`. |



* VectorizeForGetVikingdbCollectionOutput Parameter Structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|DenseVectors |DenseForGetVikingdbCollectionOutput |Yes |Dense vectorization configuration, corresponding to API field `Dense`, used to specify the embedding model, dimension, and input fields. |
|SparseVectors |SparseForGetVikingdbCollectionOutput |No |Sparse vectorization configuration, corresponding to API field `Sparse`. |



* DenseForGetVikingdbCollectionOutput and SparseForGetVikingdbCollectionOutput Parameter Structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|ModelName |string |Yes |Model name, corresponding to API field `ModelName`. See the embedding model list below for optional values. |
|ModelVersion |string |No |Model version, corresponding to API field `ModelVersion`. Required for Doubao series models, default is `default` for bge series models. |
|Dim |int |No |Dimension of dense vectors. See the embedding model list for dimensions supported by each model. |
|TextField |string |No |Text vectorization field name, corresponding to API field `TextField`. |
|ImageField |string |No |Image vectorization field name, corresponding to API field `ImageField`. |
|VideoField |string |No |Video vectorization field name, corresponding to API field `VideoField`. |


<span id="examples"></span>
# Examples

<span id="request-example"></span>
## Request Example

```go
package main

import (
    "fmt"
    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
    "os"
)

func main() {
    var (
       accessKey      = os.Getenv("VIKINGDB_AK")
       secretKey      = os.Getenv("VIKINGDB_SK")
       region         = "ap-southeast-1"
       collectionName = "Your Collection Name"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := &vikingdb.GetVikingdbCollectionInput{
       CollectionName: volcengine.String(collectionName),
    }

    output, err := svc.GetVikingdbCollection(input)
    if err != nil {
       panic(err)
    }
    fmt.Println(output)
}
```
