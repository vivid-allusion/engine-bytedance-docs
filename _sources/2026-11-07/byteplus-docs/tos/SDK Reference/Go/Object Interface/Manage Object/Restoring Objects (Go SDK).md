---
title: "Restoring Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-go-sdk"
---

Restore cold archive objects; after restoration, the objects can be accessed via the download object interface. Different retrieval methods can be specified through parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The first invocation of the RestoreObject API returns a 202 status code. If the file is being restored, invoking the RestoreObject API again will return a 409 error. If the object has already been restored, a subsequent call to the RestoreObject interface returns 200 OK.

* For buckets with versioning enabled, you can restore a specific version of an object by specifying the VersionId. If VersionId is not specified, the current version of the object will be restored by default.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to restore objects.

```go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
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
       key        = "restore-key"
       versionId  = "restore-version-id"
       ctx        = context.Background()
    )
   
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
    
    output, err := client.RestoreObject(ctx, &tos.RestoreObjectInput{
       Bucket:    bucketName,
       Key:       key,
       VersionID: versionId,
       Days:      1,
       RestoreJobParameters: &tos.RestoreJobParameters{
          Tier: enum.TierStandard,
       },
    })
    checkErr(err)
    fmt.Println("RestoreObject Request ID:", output.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to the Restore Object API, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
