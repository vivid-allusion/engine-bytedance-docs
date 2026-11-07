---
title: "Creating a Bucket (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-bucket-go-sdk"
---

A Bucket in TOS is a globally unique namespace that serves as a container for storing Object data. The name of a newly created bucket must be unique within TOS. This article explains how to create a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Bucket [naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts) are as follows:

   * Only lowercase letters (a–z), digits, and hyphens (\-) are permitted.

   * The beginning and end can only be a digit or a letter.

   * The length must be between 3 and 63 characters.

* When accessing TOS via other BytePlus products in the same region as TOS, it is recommended to use the internal network Endpoint. For more information about regions and Endpoints, please refer to [Regions and Access Endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the corresponding permissions through IAM policies. For detailed steps, please refer to [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

<span id=".5Yib5bu65a2Y5YKo5qG25pe25bm25Yib5bu65pe25oyH5a6aLWFjbA=="></span>
### Specify the ACL when creating a bucket.

```go
package main

import (
   "context"
   "fmt"
   "os"

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
  
   acl := enum.ACLPrivate
 
   resp, err := client.CreateBucketV2(context.Background(), &tos.CreateBucketV2Input{
      Bucket:       bucketName,
      ACL:          acl,
   })
   checkErr(err)
   fmt.Println("create bucket request id: ", resp.RequestID)
   fmt.Println("create bucket response status code: ", resp.StatusCode)
}
```


<span id=".5Yib5bu65pe25oyH5a6a5a2Y5YKo57G75Z6L"></span>
### **Specifying Storage Type During Creation**

```go
package main

import (
   "context"
   "fmt"
   "os"

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
  
   storageClass := enum.StorageClassIa
  
   resp, err := client.CreateBucketV2(context.Background(), &tos.CreateBucketV2Input{
      Bucket:       bucketName,
      StorageClass: storageClass,
   })
   checkErr(err)
   fmt.Println("create bucket request id: ", resp.RequestID)
   fmt.Println("create bucket response status code: ", resp.StatusCode)
}
```


<span id=".5Yib5bu65pe25oyH5a6aLWF6Leexu-Weiw=="></span>
### **Specify AZ Type During Creation**

```go
package main

import (
   "context"
   "fmt"
   "os"

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
  
   azRedundancy := enum.AzRedundancyMultiAz
  
   resp, err := client.CreateBucketV2(context.Background(), &tos.CreateBucketV2Input{
      Bucket:       bucketName,
      AzRedundancy: azRedundancy,
   })
   checkErr(err)
   fmt.Println("create bucket request id: ", resp.RequestID)
   fmt.Println("create bucket response status code: ", resp.StatusCode)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For API documentation on bucket creation, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
