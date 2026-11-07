---
title: "ListVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/ListVikingdbCollection"
---

<span id="overview"></span>
# Overview

The ListVikingdbCollection interface is used to query the list of Collections under the current project, supporting pagination and name keyword filtering.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `ListVikingdbCollection(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a collection list query request. The input parameter type is `vikingdb.ListVikingdbCollectionInput`, which includes configurations such as project name, pagination parameters, and filter conditions.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |string |No |Project name, corresponding to API field `ProjectName`, default value is default. |
|PageSize |int |No |Pagination size, corresponding to API field `PageSize`, value range 1\-100, default value is 10. |
|PageNumber |int |No |Pagination page number, corresponding to API field `PageNumber`, starting from 1. |
|Filter |FilterForListVikingdbCollectionInput |No |Filter condition, corresponding to API field `Filter`. |



* FilterForListVikingdbCollectionInput



|Parameter |Type |Required |Description |
|---|---|---|---|
|CollectionNameKeyword |string |No |Collection name keyword, corresponding to API field `CollectionNameKeyword`, used for fuzzy search. |


<span id="response-parameters"></span>
# Response Parameters

The interface returns `ListVikingdbCollectionResponse`, which includes pagination information and the collection list.


|Parameter |Type |Description |
|---|---|---|
|TotalCount |int |Total number of collections, corresponding to API field `TotalCount`. |
|PageNumber |int |Current page number, corresponding to API field `PageNumber`. |
|PageSize |int |Number of items returned on this page, corresponding to API field `PageSize`. |
|Collections |[]CollectionForListVikingdbCollectionOutput |Collection details list, corresponding to API field `Collections`. |



* CollectionForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|CollectionName |string |Collection name, corresponding to API field `CollectionName`. |
|ProjectName |string |Associated project, corresponding to API field `ProjectName`. |
|ResourceId |string |Collection ID, corresponding to API field `ResourceId`. |
|Description |string |Collection description, corresponding to API field `Description`. |
|CreateTime |string |Creation time (RFC3339), corresponding to API field `CreateTime`. |
|UpdateTime |string |Update time, corresponding to API field `UpdateTime`. |
|UpdatePerson |string |Last operator, corresponding to API field `UpdatePerson`. |
|EnableKeywordsSearch |bool |Whether keyword search is enabled, corresponding to API field `EnableKeywordsSearch`. |
|IndexCount |int |Number of indexes, corresponding to API field `IndexCount`. |
|IndexNames |[]string |Index name list, corresponding to API field `IndexNames`. |
|Fields |[]FieldForListVikingdbCollectionOutput |Field list, corresponding to API field `Fields`. |
|CollectionStats |CollectionStatsForListVikingdbCollectionOutput |Statistics information, corresponding to API field `CollectionStats`. |
|Tags |[]TagForListVikingdbCollectionOutput |Tag information, corresponding to API field `Tags`. |
|Vectorize |VectorizeForListVikingdbCollectionOutput |Vectorization configuration, corresponding to API field `Vectorize`. |



* FieldForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|FieldName |string |Field name, corresponding to API field `FieldName`. |
|FieldType |string |Field type, corresponding to API field `FieldType`. |
|IsPrimaryKey |bool |Whether it is a primary key, corresponding to API field `IsPrimaryKey`. |
|Dim |int |Vector dimension, corresponding to API field `Dim`. |
|DefaultValue |interface{} |Default value, corresponding to API field `DefaultValue`. |



* CollectionStatsForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|DataCount |int |Number of documents in the collection, corresponding to API field `DataCount`. |
|DataStorage |int |Storage capacity (Bytes), corresponding to API field `DataStorage`. |



* TagForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|Key |string |Tag key, corresponding to API field `Key`. |
|Value |string |Tag value, corresponding to API field `Value`. |



* VectorizeForListVikingdbCollectionOutput



|Parameter |Type |Description |
|---|---|---|
|DenseVectors |DenseForListVikingdbCollectionOutput |Dense vectorization configuration, corresponding to API field `Dense`, field meanings are the same as the Get interface. |
|SparseVectors |SparseForListVikingdbCollectionOutput |Sparse vectorization configuration, corresponding to API field `Sparse`. |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

```go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    var (
       projectName = "default"
    )

    input := &vikingdb.ListVikingdbCollectionInput{
       ProjectName: volcengine.String(projectName),
       PageSize:    volcengine.Int32(1),
       PageNumber:  volcengine.Int32(10),
    }
    output, err := svc.ListVikingdbCollection(input)
    if err != nil {
       panic(err)
    }
    fmt.Println(output)
}
```
