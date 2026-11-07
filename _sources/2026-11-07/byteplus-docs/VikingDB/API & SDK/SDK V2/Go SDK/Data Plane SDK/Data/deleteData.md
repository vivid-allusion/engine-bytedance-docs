---
title: "deleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteData"
---

<span id="overview"></span>
# Overview

deleteData is used to delete data in a specified Collection, deleting single or multiple data entries by primary key. A maximum of 100 data entries can be deleted in a single request.

<span id="request-parameters"></span>
# Request Parameters


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|ResourceId |string |Either one is required |Resource ID |
|collectionName |string | |Collection name |
|IDs |[]interface{} |Either one is required |List of primary keys for data to be deleted (primary key is int64 or string). Maximum 100 entries.<br><br>Note:<br><br><br>* If the request parameters are invalid (4xx type errors), all operations will fail. |
| | | | |
|DelAll |bool | |When set to true, deletes all data; default is false.<br><br>This interface deletes all data but cannot synchronize to the index immediately, so data can still be retrieved from the index for a period of time (approximately 5 minutes). |


<span id="return-parameters"></span>
# Return Parameters

This interface only returns common parameters, and `result` is always `null` (see "Response Body Common Parameters" below).

<span id="response-body-common-parameters"></span>
## Response Body Common Parameters


|Parameter Name |Type |Description |
|---|---|---|
|RequestID |string |Request ID. |
|Code |string |Operation status code. `Success` on success, otherwise an error code phrase. |
|Message |string |Execution information. On success, it is `The API call was executed successfully.`. |
|Result |map[string]interface{} |Operation result. If no data needs to be returned, `result = null`. |


<span id="examples"></span>
# Examples

<span id="request-parameters"></span>
## Request Parameters

```Go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/vikingdb-go-sdk/vector"
    "github.com/volcengine/vikingdb-go-sdk/vector/model"
    "os"
    "time"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       endpoint  = "https://api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com"
       region    = "ap-southeast-1"
    )

    client, err := vector.New(
       vector.AuthIAM(accessKey, secretKey), // IAM auth
       vector.WithEndpoint(endpoint),
       vector.WithRegion(region),
       vector.WithTimeout(time.Second*30),
       vector.WithMaxRetries(3),
    )
    if err != nil {
       fmt.Println("New client failed, err: ", err)
       panic(err)
    }
    ctx := context.Background()

    resp, err := client.Collection(model.CollectionLocator{
       CollectionName: "Your Collection Name",
    }).Delete(ctx, model.DeleteDataRequest{
       IDs: []interface{}{1},
    })
    if err != nil {
       fmt.Println("Delete failed, err: ", err)
       panic(err)
    }

    fmt.Println(resp.Message)
}
```


 &nbsp;
