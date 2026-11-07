---
title: "Renaming Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Rename-objects-go-sdk"
---

TOS supports renaming the key of an individual object within a bucket without copying or deleting data.

<span id="c51642df"></span>
## **Precautions**


* Before renaming an object, you must first enable the renaming feature.

* Renaming is only supported for objects uploaded after the RenameObject feature is enabled; objects that existed prior to enabling this feature are not supported for renaming.

* Concurrent renaming is not supported for the same object.

* All information contained in the metadata of the renamed object is identical to that of the source object. For more information, see [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).


<span id="cdcc5d95"></span>
## **Sample Code**

The following code is used for the object renaming functionality.

```Go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
    if err != nil {
       if serverErr, ok := err.(*tos.TosServerError); ok {
          fmt.Println("Error:", serverErr.Error())
          fmt.Println("Request ID:", serverErr.RequestID)
          fmt.Println("Response Status Code:", serverErr.StatusCode)
          fmt.Println("Response Header:", serverErr.Header)
          fmt.Println("Response Err Code:", serverErr.Code)
          fmt.Println("Response Err Msg:", serverErr.Message)
       } else {
          fmt.Println("Error:", err)
       }
       panic(err)
    }
}

func main() {
    var (
       accessKey = os.Getenv("TOS_ACCESS_KEY")
       secretKey = os.Getenv("TOS_SECRET_KEY")
       
       endpoint = "your endpoint"
       region   = "your region"
       
       bucketName = "*** Provide your bucket name ***"
       key        = "old-key"
       newKey     = "new-key"
       ctx        = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
   
    output, err := client.RenameObject(ctx, &tos.RenameObjectInput{
       Bucket: bucketName,
       Key:    key,
       NewKey: newKey,
    })
    checkErr(err)
    fmt.Println("RenameObject Request ID:", output.RequestID)
}
```


<span id="15d3a72a"></span>
## Relevant Documentation

For the API documentation on RenameObject, please refer to [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
