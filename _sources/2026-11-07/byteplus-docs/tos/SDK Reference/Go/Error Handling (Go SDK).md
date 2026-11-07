---
title: "Error Handling (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-go-sdkSDK"
---

This article presents exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server complies with HTTP standards and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [Definition of TOS Server-Side Status Codes and Error Codes](https://docs.byteplus.com/docs/6349/74874).

<span id=".c2RrLeiHquWumuS5iemUmeivrw=="></span>
## SDK Custom Errors

<span id=".5a6i5oi356uv6ZSZ6K-vLXRvc2NsaWVudGVycm9y"></span>
### Client Error \- TosClientError

TosClientError is caused by incorrect client input parameters, connection timeouts, or the execution of special client operations such as canceling resumable uploads. For example, when using CreateBucketV2 to create a bucket, an exception is thrown if the bucket name exceeds 63 characters in length.

<span id=".5pyN5Yqh56uv6ZSZ6K-vLXRvc3NlcnZlcmVycm9y"></span>
### Server\-Side Error \- TosServerError

Requests are sent to the TOS server via the TOS Go SDK interface. The response includes status codes that comply with HTTP standards and business error codes, which together indicate the status of the current request.

<span id=".6ZSZ6K-v5aSE55CG56S65L6L"></span>
### Error Handling Examples

The following code demonstrates exception handling when attempting to download a non\-existent object. If a TosServerError exception occurs, the code prints the exception message, HTTP request status code, and request ID. If a TosClientError exception occurs, it prints the exception message and the underlying cause of the error.

```go
package main

import (
   "context"
   "fmt"
   "net/http"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
   if err != nil {
      panic(err)
   }
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      endpoint   = "your endpoint"
      region     = "your region"
      bucketName = "your bucket name"
      objectKey  = "your object key"
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   get, err := client.GetObjectV2(context.Background(), &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   if err != nil {
      switch terr := err.(type) {
      case *tos.TosServerError:
         fmt.Printf("Message:%s StatusCode:%d RequestID:%s", terr.Message, terr.StatusCode, terr.RequestID)
         if terr.StatusCode == http.StatusNotFound {
            return
         }
      case *tos.TosClientError:
         fmt.Printf("Message:%s Cause:%v", terr.Message, terr.Cause)

      }
   }
   fmt.Println("GetObjectV2 Request ID:", get.RequestID)

}
```
