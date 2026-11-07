---
title: "Managing Bucket Storage Classes (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-storage-types-go-sdk"
---

A bucket (Bucket) in TOS serves as a globally unique namespace, functioning as a data container for storing object (Object) data. This article explains how to configure the storage class of a bucket.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Description of Storage Types

A bucket is the globally unique namespace in TOS, functioning as a data container for storing object (Object) data. TOS offers multiple types of bucket storage, suitable for a variety of application scenarios. For more information on storage types, see [Storage Types](https://docs.byteplus.com/docs/tos/docs-storage-type). This article describes how to configure the storage type for a bucket. The bucket storage types are classified into the following categories:


|Storage Type |Description |corresponding enumeration value |
|---|---|---|
|Standard Storage |Storage types featuring high availability, high reliability, and high performance, suitable for frequently accessed data. |enum.*StorageClassStandard* |
|Low\-Frequency Storage |Designed for infrequently accessed data, with a minimum storage period of 30 days. |enum.*StorageClassIa* |
|Archival Flashback Storage |Business scenarios requiring long\-term data retention with infrequent access, such as archival records, must be stored for a minimum of 90 days. |enum.*StorageClassArchiveFr* |
|Intelligent Tiered Storage |Applicable to data with uncertain access frequency, allowing adjustment of the access tier based on access frequency to reduce storage costs. |enum.*StorageClassIntelligentTiering* |
|Cold Archival Storage |Classified as a cold data type, it is suitable for business scenarios involving very infrequent access and long\-term data retention. Data must be stored for at least 180 days; data must be restored before accessing cold archive data. |enum.*StorageClassColdArchive* |


<span id=".6K6-572u5a2Y5YKo57G75Z6L"></span>
## **Configuring Storage Type**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">By default, only the bucket owner has permission to set the bucket storage type.</div>


* <div data-tips="true" data-tips-type="warning">After setting the bucket storage type, if the object storage type is not specified during object upload, object copy, or multipart upload initialization, the object will inherit the bucket's storage type.</div>


* <div data-tips="true" data-tips-type="warning">When creating a bucket, if no storage type is specified, the default storage type is Standard Storage.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to set the storage type of the bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)


   storageClass := enum.StorageClassIa

   output, err := client.PutBucketStorageClass(ctx, &tos.PutBucketStorageClassInput{
      Bucket:       bucketName,
      StorageClass: storageClass,
   })
   checkErr(err)
   fmt.Println("PutBucketStorageClass Request ID:", output.RequestID)
}
```


<span id=".6I635Y-W6buY6K6k5a2Y5YKo57G75Z6L"></span>
## **Retrieve Default Storage Type**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, only the bucket owner has permission to access the bucket's storage type.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the storage type of a bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)


   headOutput, err := client.HeadBucket(ctx, &tos.HeadBucketInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("Bucket Storage Class:", headOutput.StorageClass)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about storage types, please refer to [Storage Types](https://docs.byteplus.com/docs/tos/docs-storage-type).
