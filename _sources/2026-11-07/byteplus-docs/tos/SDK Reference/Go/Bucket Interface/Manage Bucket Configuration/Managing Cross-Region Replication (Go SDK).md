---
title: "Managing Cross-Region Replication (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-region-replication-go-sdk"
---

TOS supports cross\-region replication, enabling you to copy objects from one region to buckets in other regions. After cross\-region replication rules are enabled, when you upload a new file to the source bucket, TOS automatically synchronizes the file to the destination bucket. This feature is designed to meet the requirements for remote disaster recovery and data replication.

<span id=".6K6-572u6Leo5Yy65Z-f5aSN6KeE5YiZ"></span>
## **Configure Cross\-Region Replication Rules**

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Precautions**


* The corresponding files will be synchronized only after cross\-region rules are enabled.

* Cross\-region replication utilizes an asynchronous replication mechanism. Depending on the size of your files, the required time may range from several minutes to several hours.

* A maximum of 100 cross\-region replication rules can be created for a single storage bucket.

* Cross\-region replication can only be enabled when the versioning status of the source bucket and the destination bucket is identical.

* To configure cross\-region replication rules for a bucket, you must, by default, be the bucket owner.

* During CRR task execution, if both StorageClassType and StorageClassInheritDirectiveType are configured, the settings of StorageClassType shall take precedence.

* When only StorageClassInheritDirectiveType is set, if the configuration value is `StorageClassIDSourceObject`, it will be the same as the source object; if the configuration value is `StorageClassIDDestinationBucket`, it will be the same as the destination bucket.

* When neither StorageClassType nor StorageClassInheritDirectiveType is specified, the default policy is to align with the storage class of the target bucket.


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure cross\-region replication rules for the bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   rule := tos.ReplicationRule{
 
      ID: "rule_id",

      Status: enum.StatusEnabled,
     
      PrefixSet: nil,
     
      Destination: tos.Destination{
      
         Bucket: "dst_bucket",
       
         Location: "cn-shanghai",
     
      

         StorageClassInheritDirective: enum.StorageClassIDSourceObject,
      },
    
      HistoricalObjectReplication: enum.StatusDisabled,
   }


   role := "your role"
   output, err := client.PutBucketReplication(ctx, &tos.PutBucketReplicationInput{
      Bucket: bucketName,
      Role:   role,
      Rules:  []tos.ReplicationRule{rule},
   })
   checkErr(err)
   fmt.Println("PutBucketReplication Request ID:", output.RequestID)

}
```


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **View Cross\-Region Replication Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, you must be the bucket owner to access the cross\-region replication rules of a bucket.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the cross\-region replication rules of a bucket.

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
   input := &tos.GetBucketReplicationInput{
      Bucket: bucketName,
    

      RuleID: "ruleId",
   }
   output, err := client.GetBucketReplication(ctx, input)
   checkErr(err)
   fmt.Println("GetBucketReplication Request ID:", output.RequestID)
   for _, rule := range output.Rules {
    
      fmt.Println("rule id:", rule.ID)
   
      fmt.Println("rule status:", rule.Status)
      for _, prefix := range rule.PrefixSet {
      
         fmt.Println("rule prefix:", prefix)
      }
  
      fmt.Println("rule dst bucket:", rule.Destination.Bucket)
 
      fmt.Println("rule dst location:", rule.Destination.Location)
  
      fmt.Println("rule dst storage class:", rule.Destination.StorageClass)

      fmt.Println("rule dst storage class inherit directive:", rule.Destination.StorageClassInheritDirective)
   }

}
```


<span id=".5p-l6K-i6Leo5Yy65Z-f5aSN5Yi26L-b5bqm"></span>
## **Query Cross\-Region Replication Progress**

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Precautions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To obtain the cross\-region replication progress of a bucket, you must, by default, be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">The progress of historical data replication is represented as a percentage and is only applicable to storage spaces where historical data replication has been enabled.</div>


* <div data-tips="true" data-tips-type="warning">The replication progress of newly added data is indicated by the timestamp of the new data.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the cross\-region replication progress of a bucket.

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
   input := &tos.GetBucketReplicationInput{
      Bucket: bucketName,
  

      RuleID: "ruleId",
   }
   output, err := client.GetBucketReplication(ctx, input)
   checkErr(err)
   fmt.Println("GetBucketReplication Request ID:", output.RequestID)
   for _, rule := range output.Rules {
    
      fmt.Println("rule id:", rule.ID)
   
      fmt.Println("rule historical object:", rule.Progress.HistoricalObject)
 
      fmt.Println("rule new object:", rule.Progress.NewObject)
   }
}
```


<span id=".5Yig6Zmk6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **Delete Cross\-Region Replication Rule**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, you must be the bucket owner to delete cross\-region replication rules from a bucket.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete cross\-region replication rules for a bucket.

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
   input := &tos.DeleteBucketReplicationInput{
      Bucket: bucketName,
   }
   output, err := client.DeleteBucketReplication(ctx, input)
   checkErr(err)
   fmt.Println("DeleteBucketReplication Request ID:", output.RequestID)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documents

For more information on configuring cross\-region replication rules, see [Cross-Region Replication Rules](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account).
