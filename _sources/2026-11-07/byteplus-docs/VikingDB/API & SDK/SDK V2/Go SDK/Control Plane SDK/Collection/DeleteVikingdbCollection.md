---
title: "DeleteVikingdbCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DeleteVikingdbCollection"
---

<span id="overview"></span>
# Overview

DeleteVikingdbCollection is used to delete a created Collection.


* Deleting a Collection will permanently delete all data under the specified Collection. Please proceed with caution.

* Before deleting a Collection, you must first delete all Indexes associated with the Collection to successfully delete the Collection.


<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `DeleteVikingdbCollection(input)` method through the client instance created by `vikingdb.New(sess)` to initiate a collection deletion request. The input parameter type is `vikingdb.DeleteVikingdbCollectionInput`, which includes configurations such as project name, collection name/collection resource ID, etc.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |string |No |Project name, corresponding to the API field `ProjectName`, defaults to default. |
|CollectionName |string |Either is required |Name of the collection to be deleted, corresponding to the API field `CollectionName`.<br><br><br>* Starts with a letter, can only contain letters, numbers, and underscores, length 1\-128.<br><br>* The server allows choosing either this or `ResourceId`. |
|ResourceId |string | |Collection resource ID, corresponding to the API field `ResourceId`. Can be used in combination with `CollectionName` to help with tracking on the control plane. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |string |success |Operation result description, corresponding to the API field `Message`. |


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
    )
    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := &vikingdb.DeleteVikingdbCollectionInput{
       CollectionName: volcengine.String(collectionName),
    }

    output, err := svc.DeleteVikingdbCollection(input)
    if err != nil {
       panic(err)
    }
    fmt.Println(output)
}
```
