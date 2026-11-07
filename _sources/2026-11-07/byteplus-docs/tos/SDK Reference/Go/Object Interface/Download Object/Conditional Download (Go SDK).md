---
title: "Conditional Download (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-go-sdk"
---

If you wish to set constraints—such as object ETag or modification time—when downloading an object, you can use the conditional download feature provided by the TOS Go SDK. The object will only be downloaded if its information meets the conditions you specify. This document describes how to download objects by specifying limiting conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For specific instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When downloading a specified version of an object in buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads many instances of the same object simultaneously, your access speed will be limited by the bandwidth and regional restrictions of TOS. It is recommended that you utilize CDN products to enhance performance while simultaneously reducing your costs. For detailed information on accessing TOS via CDN, please refer to [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).

* Different conditions can be combined; for example, both If\-Modified\-Since and If\-Unmodified\-Since may be present simultaneously, and both If\-Match and If\-None\-Match may also coexist.

* You can retrieve the Etag information of an object by using the HeadObjectV2 interface of the TOS Go SDK.


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## Specification of Limiting Conditions

When downloading an object, you may specify conditions for the download. The object will be downloaded only if the specified conditions are met. The limiting conditions are as follows:


|Parameters |Description |
|---|---|
|If\-Match |The object is returned only if the incoming `ETag` matches the object's `ETag`; otherwise, a 412 Precondition Failed is returned. |
|If\-None\-Match |The object is returned only if the incoming `ETag` does not match the object's `ETag`; otherwise, a 304 Not Modified response is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time; otherwise, a 304 Not Modified response is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time; otherwise, a 412 Precondition Failed response is returned. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"
   "net/http"
   "time"

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
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
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


      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   date := time.Date(2022, time.October, 24, 0, 0, 0, 0, time.UTC)
   getoutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket:          bucketName,
      Key:             objectKey,
      IfModifiedSince: date,
   })
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
        
         if serverErr.StatusCode == http.StatusNotModified {
            fmt.Println("Object not modify, Request ID:", serverErr.RequestID)
         } else {
            fmt.Println("Error:", serverErr.Error())
            fmt.Println("Request ID:", serverErr.RequestID)
            fmt.Println("Response Status Code:", serverErr.StatusCode)
            fmt.Println("Response Header:", serverErr.Header)
            fmt.Println("Response Err Code:", serverErr.Code)
            fmt.Println("Response Err Msg:", serverErr.Message)
         }
      }
      panic(err)
   }
   defer getoutput.Content.Close()
   
   body, err := ioutil.ReadAll(getoutput.Content)
   checkErr(err)
   fmt.Println("GetObject Content:", body)

   getoutput, err = client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket:            bucketName,
      Key:               objectKey,
      IfUnmodifiedSince: date,
   })
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         
         if serverErr.StatusCode == http.StatusPreconditionFailed {
            fmt.Println("Object modify, Request ID:", serverErr.RequestID)
         } else {
            fmt.Println("Error:", serverErr.Error())
            fmt.Println("Request ID:", serverErr.RequestID)
            fmt.Println("Response Status Code:", serverErr.StatusCode)
            fmt.Println("Response Header:", serverErr.Header)
            fmt.Println("Response Err Code:", serverErr.Code)
            fmt.Println("Response Err Msg:", serverErr.Message)
         }
      }
      panic(err)
   }
   defer getoutput.Content.Close()
   
   body, err = ioutil.ReadAll(getoutput.Content)
   checkErr(err)
   fmt.Println("GetObject Content:", body)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
