---
title: "Managing Cross-Origin Resource Sharing (CORS) (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-origin-resource-sharing-go-sdk"
---

You can configure Cross\-Origin Resource Sharing (CORS) rules through the SDK interface. When TOS receives a cross\-origin request or an OPTIONS request, it reads the corresponding CORS rules for the bucket, performs the necessary permission checks, and returns the appropriate headers to ensure the security of cross\-origin data transmission. This article describes how to configure cross\-region resource sharing for buckets.

<span id=".6K6-572u6Leo5Z-f6LWE5rqQ5YWx5Lqr"></span>
## **Configure Cross\-Origin Resource Sharing**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring cross\-origin resource sharing rules for a storage bucket, you must have the <code>tos:PutBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure the cross\-origin resource sharing (CORS) rules for the bucket.

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
   corsRule1 := tos.CorsRule{
      
      AllowedOrigin: []string{"*"},
     
      AllowedMethod: []string{http.MethodGet, http.MethodPut},
     
      AllowedHeader: []string{"header1", "header2"},
      
      ExposeHeader: []string{"tos-1", "tos-2"},
     
      MaxAgeSeconds: 100,
   }
   corsRule2 := tos.CorsRule{
      AllowedOrigin: []string{"http://example.com", "http://www.volcengine.com"},
      AllowedMethod: []string{http.MethodGet, http.MethodPut},
      AllowedHeader: []string{"header1", "header2"},
      ExposeHeader:  []string{"tos-1", "tos-2"},
      MaxAgeSeconds: 100,
   }

   putOutput, err := client.PutBucketCORS(ctx, &tos.PutBucketCORSInput{
      Bucket:    bucketName,
      CORSRules: []tos.CorsRule{corsRule1, corsRule2},
   })
   checkErr(err)
   fmt.Println("PutBucketCORS Request ID:", putOutput.RequestID)
}
```


<span id=".6I635Y-W6Leo5Z-f6LWE5rqQ5YWx5Lqr6YWN572u"></span>
## **Retrieve Cross\-Origin Resource Sharing (CORS) configuration**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring Cross\-Origin Resource Sharing (CORS) rules for a storage bucket, you must have the <code>tos:GetBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the Cross\-Origin Resource Sharing (CORS) rules for a bucket.

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

   getOutput, err := client.GetBucketCORS(ctx, &tos.GetBucketCORSInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketCORS Request ID:", getOutput.RequestID)
   fmt.Println("CORS Length:", len(getOutput.CORSRules))

   for _, corsRule := range getOutput.CORSRules {
      fmt.Println("cors Rule AllowedOrigin:", corsRule.AllowedOrigin)
      fmt.Println("cors Rule AllowedHeader:", corsRule.AllowedHeader)
      fmt.Println("cors Rule ExposeHeader:", corsRule.ExposeHeader)
      fmt.Println("cors Rule AllowedMethod:", corsRule.AllowedMethod)
      fmt.Println("cors Rule MaxAgeSeconds:", corsRule.MaxAgeSeconds)
   }

}
```


<span id=".5Yig6Zmk6Leo5Z-f6LWE5rqQ5YWx5Lqr6YWN572u"></span>
## **Delete Cross\-Origin Resource Sharing Configuration**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting the bucket's cross\-origin resource sharing rules, you must have the <code>tos:PutBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the Cross\-Origin Resource Sharing (CORS) rules of a bucket:

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

   deleteOut, err := client.DeleteBucketCORS(ctx, &tos.DeleteBucketCORSInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("DeleteBucketCORS Request ID:", deleteOut.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information on Cross\-Origin Resource Sharing (CORS), please refer to [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).
