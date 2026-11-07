---
title: "Managing Static Websites (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-static-websites-go-sdk"
---

TOS supports hosting static websites. You can store all static website content in a TOS bucket and, after configuring static website rules, access the website via the bucket domain name.

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
## **Set Website Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only one static website hosting rule can be created in a bucket.</div>


* <div data-tips="true" data-tips-type="warning">After configuring the static website, you must bind a custom domain name for it to take effect. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Bind Custom Domain Name</a>.</div>


* <div data-tips="true" data-tips-type="warning">For security and compliance purposes, effective October 18, 2022, when you access web\-type files (with mimetype 'text/html' and extensions including HTM, HTML, JSP, PLG, HTX, STM) via the default domain of a storage bucket, the Response Header will automatically include <code>Content-Disposition:attachment</code>. As a result, when accessing web\-type files through a browser, the file will not be previewed directly; instead, its content will be downloaded locally.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure the redirection of all requests to another site.

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

   input := &tos.PutBucketWebsiteInput{
      Bucket: bucketName,
      RedirectAllRequestsTo: &tos.RedirectAllRequestsTo{
         HostName: "www.example.com",
         Protocol: "http",
      },
   }
   output, err := client.PutBucketWebsite(ctx, input)
   checkErr(err)
   fmt.Println("PutBucketWebsite Request ID:", output.RequestID)

  
   input = &tos.PutBucketWebsiteInput{
      Bucket: bucketName,
      IndexDocument: &tos.IndexDocument{
         Suffix: "index.html",
      },
      ErrorDocument: &tos.ErrorDocument{
         Key: "error.html",
      },

      RoutingRules: &tos.RoutingRules{Rules: []tos.RoutingRule{{
    
         Condition: tos.RoutingRuleCondition{
        
            KeyPrefixEquals: "prefix",
         
            HttpErrorCodeReturnedEquals: 403,
         },
     
         Redirect: tos.RoutingRuleRedirect{
       
            Protocol: "https",
            HostName: "www.redirect.com",
         },
      },
      }},
   }
   output, err = client.PutBucketWebsite(ctx, input)
   checkErr(err)
   fmt.Println("PutBucketWebsite Request ID:", output.RequestID)

}
```


<span id=".6I635Y-W572R56uZ6YWN572u6KeE5YiZ"></span>
## **Retrieve Website Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the website configuration rules for a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the website configuration rules for the bucket.

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
   output, err := client.GetBucketWebsite(ctx, &tos.GetBucketWebsiteInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketWebsite Request ID:", output.RequestID)
   
   if output.RedirectAllRequestsTo != nil {
      fmt.Println("GetBucketWebsite RedirectAllRequestsTo HostName:", output.RedirectAllRequestsTo.HostName)
      fmt.Println("GetBucketWebsite RedirectAllRequestsTo Protocol:", output.RedirectAllRequestsTo.Protocol)
   }

   if output.IndexDocument != nil {
      fmt.Println("GetBucketWebsite IndexDocument ForbiddenSubDir:", output.IndexDocument.ForbiddenSubDir)
      fmt.Println("GetBucketWebsite IndexDocument Suffix:", output.IndexDocument.Suffix)

   }

   if output.ErrorDocument != nil {
      fmt.Println("GetBucketWebsite ErrorDocument Key:", output.ErrorDocument.Key)
   }

   for _, rule := range output.RoutingRules {
      fmt.Println("GetBucketWebsite RoutingRules Rule Condition HttpErrorCodeReturnedEquals:", rule.Condition.HttpErrorCodeReturnedEquals)
      fmt.Println("GetBucketWebsite RoutingRules Rule Condition KeyPrefixEquals:", rule.Condition.KeyPrefixEquals)
      fmt.Println("GetBucketWebsite RoutingRules Rule Redirect HostName:", rule.Redirect.HostName)
      fmt.Println("GetBucketWebsite RoutingRules Rule Redirect Protocol:", rule.Redirect.Protocol)
      fmt.Println("GetBucketWebsite RoutingRules Rule Redirect ReplaceKeyWith:", rule.Redirect.ReplaceKeyWith)
      fmt.Println("GetBucketWebsite RoutingRules Rule Redirect ReplaceKeyPrefixWith:", rule.Redirect.ReplaceKeyPrefixWith)
      fmt.Println("GetBucketWebsite RoutingRules Rule Redirect HttpRedirectCode:", rule.Redirect.HttpRedirectCode)
   }

}
```


<span id=".5Yig6Zmk572R56uZ6YWN572u6KeE5YiZ"></span>
## **Delete Website Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, you must be the bucket owner to delete the website configuration rules.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the website configuration rules of a bucket.

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
   output, err := client.DeleteBucketWebsite(ctx, &tos.DeleteBucketWebsiteInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("DeleteBucketWebsite Request ID:", output.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about configuring a static website, see [Configuring a Static Website](https://docs.byteplus.com/docs/tos/Set-up-a-static-website).
