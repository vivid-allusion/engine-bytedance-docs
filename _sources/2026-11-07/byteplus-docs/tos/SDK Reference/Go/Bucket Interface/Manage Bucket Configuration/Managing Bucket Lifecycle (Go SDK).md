---
title: "Managing Bucket Lifecycle (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-lifecycle-go-sdk"
---

You can utilize the lifecycle management feature of object storage through the SDK to delete expired objects, thereby reducing storage costs. When configuring lifecycle rules, you can specify an object prefix or an object tag for which the rule will take effect. If you specify two effective conditions simultaneously, the object must satisfy all set conditions; only then will the lifecycle rule be applied.

<span id=".6K6-572u55Sf5ZG95ZGo5pyf"></span>
## **Set lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before configuring lifecycle rules, you must have the <code>tos:PutLifecycleConfiguration</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">If lifecycle rules have already been configured for the bucket, performing this operation will overwrite the existing configuration. If you need to add lifecycle rules, first use GetLifecycleConfiguration to retrieve the current rules, then append and write the new rules, and finally call PutLifecycleConfiguration to update the rules.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to configure the lifecycle rules for a bucket.

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
   lifeCycleRule := tos.LifecycleRule{

      ID: "rule1",

      Prefix: "prefix-",

      Status: enum.LifecycleStatusEnabled,



      Expiration: &tos.Expiration{
         Days: 30,
      },

      Tag: []tos.Tag{{
         Key:   "key",
         Value: "value",
      }},
   }

   putOutput, err := client.PutBucketLifecycle(ctx, &tos.PutBucketLifecycleInput{
      Bucket: bucketName,
      Rules:  []tos.LifecycleRule{lifeCycleRule},
   })
   checkErr(err)
   fmt.Println("PutBucketLifecycle Request ID:", putOutput.RequestID)
   
}
```


<span id=".6I635Y-W55Sf5ZG95ZGo5pyf6YWN572u"></span>
## **Retrieve lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before retrieving lifecycle rules, you must have the <code>tos:GetLifecycleConfiguration</code> permission. For specific operations, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information on lifecycle rules, see <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to retrieve the lifecycle rules of a bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   getOutput, err := client.GetBucketLifecycle(ctx, &tos.GetBucketLifecycleInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketLifecycle Request ID:", getOutput.RequestID)
   fmt.Println("GetBucketLifecycle Rules Length:", len(getOutput.Rules))
   for _, rule := range getOutput.Rules {
      
      fmt.Println("Rule ID:", rule.ID)
      
      fmt.Println("Rule Prefix:", rule.Prefix)
    
      fmt.Println("Rule Status:", rule.Status)
     
      fmt.Println("Rule Transitions:", rule.Transitions)
      
      fmt.Println("Rule Expiration:", rule.Expiration)
     
      fmt.Println("Rule NonCurrentVersionTransition:", rule.NonCurrentVersionTransition)
     
      fmt.Println("Rule NoCurrentVersionExpiration:", rule.NoCurrentVersionExpiration)
    
      for key, value := range rule.Tag {
         fmt.Println("Rule Tag Key:", key)
         fmt.Println("Rule Tag Value:", value)
      }
     
      fmt.Println("Rule AbortInCompleteMultipartUpload:", rule.AbortInCompleteMultipartUpload)
   }
}
```


<span id=".5Yig6Zmk55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## **Delete lifecycle rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting lifecycle rules, you must have the <code>tos:PutLifecycleConfiguration</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete lifecycle rules for a bucket:

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
      ctx        = context.Background()
   )
 
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   
   deleteOutput, err := client.DeleteBucketLifecycle(ctx, &tos.DeleteBucketLifecycleInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("DeleteBucketLifecycle Request ID:", deleteOutput.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**

For more information about lifecycle rules, see [Configuring lifecycle rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).
