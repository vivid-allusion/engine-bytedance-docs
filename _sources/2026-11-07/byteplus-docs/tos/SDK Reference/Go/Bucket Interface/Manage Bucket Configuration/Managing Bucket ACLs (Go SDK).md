---
title: "Managing Bucket ACLs (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-acl-go-sdk"
---

You can configure the bucket ACL through the interfaces provided by the TOS SDK. Permission settings can be configured via either the request header or the request body.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* To configure the bucket ACL, the account must be either the creator of the bucket or possess write permission for the bucket ACL.

* ACL configuration is supported only for the main account ID; ACL configuration for sub\-accounts is not supported.


<span id=".5qG2LWFjbC3or7TmmI4="></span>
## Bucket ACL Overview


|**Access Permissions** |**Description** |**Enumeration Type** |
|---|---|---|
|READ |Allow authorized users to list objects in the bucket and perform multipart upload tasks. |*enum.PermissionRead* |
|WRITE |Authorized users are permitted to create, overwrite, and delete any object within the bucket, as well as to initialize multipart upload tasks, upload parts, merge parts, and cancel multipart upload tasks. |enum.*PermissionWrite* |
|READ_ACP |Permit authorized users to read the bucket ACL. |enum.*PermissionReadAcp* |
|WRITE_ACP |Permit authorized users to set ACLs for applicable storage buckets. |enum.*PermissionWriteAcp* |
|FULL_CONTROL |Authorized users are permitted READ, WRITE, READ_ACP, and WRITE_ACP permissions on the storage bucket. |enum.*PermissionFullControl* |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".6YCa6L-H6K-35rGC5L2T6K6-572uLWFjbC3mnYPpmZA="></span>
### **Setting ACL permissions via the request body**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting the ACL permissions for a bucket, you must have the <code>tos:PutBucketACL</code> permission or the <code>WRITE_ACP</code> bucket ACL permission. For detailed procedures, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


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
   
   input := &tos.PutBucketACLInput{
      Bucket: bucketName,
      Owner: tos.Owner{
       
         ID: "ownerid",
      },
      Grants: []tos.GrantV2{
         {
            GranteeV2: tos.GranteeV2{
               ID:   "userId",
               Type: enum.GranteeUser,
            },
            Permission: enum.PermissionWrite,
         },
      },
   }
   
   putAclOutput, err := client.PutBucketACL(ctx, input)
   checkErr(err)
   fmt.Println("PutBucketACL Request ID: ", putAclOutput.RequestID)

   getAclOutput, err := client.GetBucketACL(ctx, &tos.GetBucketACLInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketACL Request ID:", getAclOutput.RequestID)
   
   fmt.Println("GetBucketACL Owner:", getAclOutput.Owner)
   for _, grant := range getAclOutput.Grants {
     
      fmt.Println("Grant Permission:", grant.Permission)
    
      fmt.Println("Grant GranteeV2 ID", grant.GranteeV2.ID)
     
      fmt.Println("Grant GranteeV2 DisplayName", grant.GranteeV2.DisplayName)
   
      fmt.Println("Grant GranteeV2 Canned", grant.GranteeV2.Canned)
   
      fmt.Println("Grant GranteeV2 Type", grant.GranteeV2.Type)
   }

}
```


<span id=".6YCa6L-H6K-35rGC5aS06K6-572u5p2D6ZmQ"></span>
### **Setting Permissions via Request Headers**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting the ACL permissions for a bucket, you must have the <code>tos:PutBucketACL</code> permission or the <code>WRITE_ACP</code> bucket ACL permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


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
   
  
    putAclOutput, err := client.PutBucketACL(ctx, &tos.PutBucketACLInput{
       Bucket:  bucketName,
       ACLType: enum.ACLPrivate,
    })
    checkErr(err)
}
```


<span id=".6I635Y-W5a2Y5YKo5qG25p2D6ZmQ"></span>
### **Obtaining Storage Bucket Permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining access to the bucket, you must have the <code>tos:GetBucketACL</code> permission or the <code>READ_ACP</code> bucket ACL permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


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

   getAclOutput, err := client.GetBucketACL(ctx, &tos.GetBucketACLInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketACL Request ID:", getAclOutput.RequestID)

   fmt.Println("GetBucketACL Owner:", getAclOutput.Owner)
   for _, grant := range getAclOutput.Grants {
   
      fmt.Println("Grant Permission:", grant.Permission)

      fmt.Println("Grant GranteeV2 ID", grant.GranteeV2.ID)

      fmt.Println("Grant GranteeV2 DisplayName", grant.GranteeV2.DisplayName)
  
      fmt.Println("Grant GranteeV2 Canned", grant.GranteeV2.Canned)

      fmt.Println("Grant GranteeV2 Type", grant.GranteeV2.Type)
   }

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

To manage bucket permissions, see [Bucket ACLs](https://docs.byteplus.com/docs/tos/docs-bucket-acls).
