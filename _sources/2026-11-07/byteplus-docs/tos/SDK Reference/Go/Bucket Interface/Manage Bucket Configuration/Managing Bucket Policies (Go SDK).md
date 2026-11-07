---
title: "Managing Bucket Policies (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-policy-go-sdk"
---

Bucket is the globally unique namespace in TOS, serving as a data container for storing Object data. Access control in TOS is implemented through IAM policies, bucket policies, and bucket and object ACLs. Both Bucket Policy and Bucket ACL are permission control strategies based on TOS resources. Compared to Bucket ACL, Bucket Policy offers more flexible permission configuration. This article describes how to set, retrieve, and delete the bucket authorization policy (Policy).

<span id=".6K6-572u5a2Y5YKo5qG2562W55Wl"></span>
## **Set Bucket Policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before configuring a bucket policy, you must have the <code>tos:PutBucketPolicy</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">Users with the <code>tos:PutBucketPolicy</code> permission can modify bucket policies without restriction and can use this permission to obtain other permissions. It is recommended that you configure this permission with caution.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to set the bucket policy.

```go
package main

import (
   "context"
   "encoding/json"
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

   policy := map[string]interface{}{
      "Statement": []map[string]interface{}{
         {
            "Sid":       "internal public",
            "Effect":    "Allow",
            "Action":    []string{"*"},
            "Principal": "*",
            "Resource": []string{
               fmt.Sprintf("trn:tos:::%s/*", bucketName),
               fmt.Sprintf("trn:tos:::%s", bucketName),
            },
         },
      }}
   data, err := json.Marshal(policy)
   checkErr(err)

   putOutput, err := client.PutBucketPolicyV2(ctx, &tos.PutBucketPolicyV2Input{
      Bucket: bucketName,
      Policy: string(data),
   })
   checkErr(err)
   fmt.Println("PutBucketPolicyV2 Request ID:", putOutput.RequestID)
}
```


<span id=".6I635Y-W5a2Y5YKo5qG2562W55Wl"></span>
## **Get Bucket Policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining the bucket policy, you must have the <code>tos:GetBucketPolicy</code> permission. For detailed instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the bucket policy.

```go
package main

import (
   "context"
   "encoding/json"
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

   getOutput, err := client.GetBucketPolicyV2(ctx, &tos.GetBucketPolicyV2Input{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketPolicyV2 Request ID:", getOutput.RequestID)
   fmt.Println("Policy:", getOutput.Policy)
}
```


<span id=".5Yig6Zmk5a2Y5YKo5qG2562W55Wl"></span>
## **Delete Bucket Policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting a bucket policy, you must have the <code>tos:DeleteBucketPolicy</code> permission. For specific instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the bucket policy.

```go
package main

import (
   "context"
   "encoding/json"
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

   deleteOutput, err := client.DeleteBucketPolicyV2(ctx, &tos.DeleteBucketPolicyV2Input{Bucket: bucketName})
   checkErr(err)
   fmt.Println("DeleteBucketPolicyV2 Request ID:", deleteOutput.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For more information about bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/docs/tos/docs-bucket-authorization-policy-management).
