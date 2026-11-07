---
title: "Obtaining Bucket Region (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-the-bucket-region-go-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container for storing Object data. This document describes how to obtain the region information where a bucket is located.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* By default, only the bucket owner can view the region where the bucket is located.

* When managing buckets and objects within buckets using the TOS Go SDK, you must use the domain name of the bucket's region. For more information about regions and access domain names, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to obtain the region (Region) of a bucket.

```go
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
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
 
   output, err := client.GetBucketLocation(context.Background(), &tos.GetBucketLocationInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketLocation Request ID:", output.RequestID)
  
   fmt.Println("Bucket Region:", output.Region)
   
   fmt.Println("Bucket ExtranetEndpoint:", output.ExtranetEndpoint)
   
   fmt.Println("Bucket IntranetEndpoint:", output.IntranetEndpoint)
}
```
