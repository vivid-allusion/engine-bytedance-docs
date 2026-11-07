---
title: "UpdateVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/UpdateVikingdbCollection"
---

<span id="overview"></span>
# Overview

`UpdateVikingdbCollection` is used to add fields to a specified Collection.

Collection supports adding new fields; already defined fields cannot be modified, only the Collection description can be modified.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `UpdateVikingdbCollection(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a collection update request. The input parameter is of type `vikingdb.UpdateVikingdbCollectionInput`, which includes configurations such as collection name, description, project name, and new field definitions.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is UpdateVikingdbCollectionInput. The parameters included in UpdateVikingdbCollectionInput are shown in the table below.


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |string |No |Project name, corresponding to API field `ProjectName`, default is "default". |
|CollectionName |string |Either/Or |Collection name, corresponding to API field `CollectionName`. Starts with a letter, can only contain letters, numbers, and underscores, length 1\-128. Either this or `ResourceId` must be provided. |
|ResourceId |string |Either/Or |Collection resource ID, corresponding to API field `ResourceId`. Either this or `CollectionName` must be provided. It is recommended to fill in both to ensure accuracy. |
|Description |string |No |Collection description, corresponding to API field `Description`, maximum 65535 bytes. |
|Fields |[]FieldForUpdateVikingdbCollectionInput |Yes |List of new fields, corresponding to API field `Fields`. The maximum total number of fields per collection is 128, and only appending new fields is supported. |



* Field parameter structure



|Parameter |Type |Required |Description |
|---|---|---|---|
|FieldName |string |Yes |Field name.<br><br>Restrictions: English letters, numbers, or underscores. Must start with an English letter. Length does not exceed 64 Bytes. |
|FieldType |FieldTypeEnum (enumeration type) |Yes |Field type. |
|DefaultValue |interface{} |No |Default value for field content.<br><br>Note: Fields of type vector/sparse_vector/text/image/video do not support default values. |
|Dim |Int |No |If the field type is vector, this parameter specifies the dimension of the dense vector. Supports 4\-4096 and must be a multiple of 4. |
|IsPrimaryKey |bool |No |Whether it is a primary key field. One primary key field (string or int64 type) can be specified for the dataset. If not specified, an automatically generated primary key is used with the field name "**AUTO_ID**". |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |string |success |Operation result description, corresponding to API field `Message`. |


<span id="example"></span>
# Example

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
       description    = "Your Collection Description"
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := &vikingdb.UpdateVikingdbCollectionInput{
       CollectionName: volcengine.String(collectionName),
       Description:    volcengine.String(description),

       Fields: []*vikingdb.FieldForUpdateVikingdbCollectionInput{
          {
             FieldName: volcengine.String("new_tag"),
             FieldType: volcengine.String("string"),
          },
          {
             FieldName: volcengine.String("extra_score"),
             FieldType: volcengine.String("float32"),
          },
       },
    }

    output, err := svc.UpdateVikingdbCollection(input)
    if err != nil {
       panic(err)
    }
    fmt.Println(output)
}
```
