---
title: "Managing Mirroring Rules (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-image-return-to-source-go-sdk"
---

Mirror\-based back\-to\-origin (mirroring) is primarily used in scenarios involving seamless data migration to TOS. For example, your web service may already be running on a self\-built origin server. You can migrate static web pages to TOS for storage. To retrieve some data that has not yet been migrated to TOS, you can configure mirroring rules.

<span id=".6K6-572u6ZWc5YOP5Zue5rqQ"></span>
## **Configure mirroring rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Each bucket supports the creation of only one back\-to\-origin rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirroring supports objects up to a maximum size of 5 GiB. If you need to request objects larger than 5 GiB, please use the <a href="https://docs.byteplus.com/docs/tos/Scope-download-go-sdk">range download</a> feature.</div>


* <div data-tips="true" data-tips-type="warning">The maximum supported object size for redirect\-based back\-to\-origin is 300 GiB.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to set mirroring rules for the specified bucket.

```go
package main

import (
   "context"
   "fmt"
   "net/http"

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
   mirrorBucketRule1 := tos.MirrorBackRule{

      ID: "rule1",
      Condition: tos.Condition{

         HttpCode: http.StatusNotFound,
      },
      Redirect: tos.Redirect{

         RedirectType: enum.RedirectTypeMirror,
  
         FetchSourceOnRedirect: true,

         PassQuery: true,

         FollowRedirect: true,
         
         MirrorHeader: tos.MirrorHeader{

            PassAll: false,

            Pass:    []string{"header-1", "header-2"},

            Remove:  []string{"header-3", "header-4"},
         },

         PublicSource: tos.PublicSource{SourceEndpoint: tos.SourceEndpoint{
            Primary:  []string{"https://www.example.com"},
            Follower: nil,
         }},
      },
   }

   putOutput, err := client.PutBucketMirrorBack(ctx, &tos.PutBucketMirrorBackInput{Bucket: bucketName, Rules: []tos.MirrorBackRule{mirrorBucketRule1}})
   checkErr(err)
   fmt.Println("PutBucketMirrorBack Request ID:", putOutput.RequestID)
}
```


<span id=".6I635Y-W6ZWc5YOP5Zue5rqQ"></span>
## **Retrieve mirroring rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the owner of the bucket to retrieve its mirroring rule.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to retrieve the mirroring rules for a specified bucket.

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

   getOutput, err := client.GetBucketMirrorBack(ctx, &tos.GetBucketMirrorBackInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketMirrorBack Request ID:", getOutput.RequestID)
   fmt.Println("GetBucketMirrorBack Rule length:", len(getOutput.Rules))
   for _, rule := range getOutput.Rules {

      fmt.Println("rule ID:", rule.ID)

      fmt.Println("rule Condition HttpCode:", rule.Condition.HttpCode)

      fmt.Println("rule Redirect RedirectType:", rule.Redirect.RedirectType)

      fmt.Println("rule Redirect FetchSourceOnRedirect:", rule.Redirect.FetchSourceOnRedirect)

      fmt.Println("rule Redirect PassQuery:", rule.Redirect.PassQuery)

      fmt.Println("rule Redirect FollowRedirect:", rule.Redirect.FollowRedirect)

      fmt.Println("rule Redirect MirrorHeader PassAll:", rule.Redirect.MirrorHeader.PassAll)

      fmt.Println("rule Redirect MirrorHeader Pass:", rule.Redirect.MirrorHeader.Pass)

      fmt.Println("rule Redirect MirrorHeader Remove:", rule.Redirect.MirrorHeader.Remove)

      fmt.Println("rule Redirect PublicSource SourceEndpoint:", rule.Redirect.PublicSource.SourceEndpoint)
   }

}
```


<span id=".5Yig6Zmk6ZWc5YOP5Zue5rqQ"></span>
## **Delete mirroring rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the owner of the bucket can delete the bucket's mirroring rule.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the mirroring rule for a specified bucket.

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

   deleteOutput, err := client.DeleteBucketMirrorBack(ctx, &tos.DeleteBucketMirrorBackInput{Bucket: bucketName})
   fmt.Println("DeleteBucketMirrorBack Request ID:", deleteOutput.RequestID)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**

For more information about mirroring, see [Setting back-to-origin rules](https://docs.byteplus.com/docs/tos/Overview9).
