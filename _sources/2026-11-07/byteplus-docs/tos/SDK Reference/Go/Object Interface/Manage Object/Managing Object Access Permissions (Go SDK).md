---
title: "Managing Object Access Permissions (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-go-sdk"
---

This article describes how to obtain and configure access permissions for objects. The access permissions of an object take precedence over those of the bucket. If no access permissions are set for the object, the bucket's access permissions will apply.

<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## **Configuring Object Read and Write Permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring read and write permissions for an object, you must have the <code>tos:PutObjectACL</code> permission or the WRITE_ACP object ACL permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".YWNsLeivtOaYjg=="></span>
### ACL Description

The object ACL permissions include the following types.


|**Access Permissions** |**Description** |**Access Permission Value** |
|---|---|---|
|READ |Authorized users are permitted to read object data and its metadata. |enum.*PermissionRead* |
|READ_ACP |Allow grantees to read object ACL |enum.*PermissionReadAcp* |
|WRITE_ACP |Authorized users are permitted to write ACLs for applicable objects. |enum.*PermissionWriteAcp* |
|FULL_CONTROL |Allow the grantee to have READ, READ_ACP, and WRITE_ACP permissions on the object. |enum.*PermissionFullControl* |


You can specify detailed ACL permissions either by including them in the request body or by setting them in the request header.

<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Provide detailed ACL permission information in the request body.** 

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

      
      objectKey = "*** Provide your object key ***"
      ctx       = context.Background()
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   
   input := &tos.PutObjectACLInput{
      Bucket: bucketName,
      Key:    objectKey,
      
      VersionID: "",
      Owner: tos.Owner{
        
         ID: "ownerid",
      },
      Grants: []tos.GrantV2{
         {
            GranteeV2: tos.GranteeV2{
               ID:   "userId",
               Type: enum.GranteeUser,
            },
            Permission: enum.PermissionRead,
         },
      },
   }
   output, err := client.PutObjectACL(ctx, input)
   checkErr(err)
   fmt.Println("PutObjectACL Request ID:", output.RequestID)

}
```


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Setting access permissions in the request header**

There are seven categories of object read/write permissions that can be configured via the x\-tos\-acl request header:


|**Access Permissions** |**Description** |Access Permission Value |
|---|---|---|
|private |Private. The owner of the object possesses all permissions, while other users are not authorized to operate the object. |enum.*ACLPrivate* |
|public\-read |Public reading. The owner of an object possesses all permissions, while other users have only read permission for that object. |enum.*ACLPublicRead* |
|public\-read\-write |Public Read/Write All users have read permission for this object. |enum.*ACLPublicReadWrite* |
|authenticated\-read |The owner of the object possesses all permissions, while authenticated users are granted read access to the object. |enum.*ACLAuthRead* |
|bucket\-owner\-read |The object owner has full permissions, while the bucket owner has read permission for this object. |enum.*ACLBucketOwnerRead* |
|bucket\-owner\-full\-control |Both the bucket owner and the object owner have all operation permissions on the object. |enum.*ACLBucketOwnerFullControl* |
|bucket\-owner\-entrusted |The bucket owner has full control over this object and can use bucket policies to authorize other accounts or users to access this object, either allowing or denying such access. |enum.*ACLBucketOwnerEntrusted* |


The following code sets object read and write permissions using x\-tos\-acl:

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

     
      objectKey = "*** Provide your object key ***"
      ctx       = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)


   input := &tos.PutObjectACLInput{
      Bucket: bucketName,
      Key:    objectKey,

      VersionID: "",
      ACL:       enum.ACLPrivate,
   }
   output, err := client.PutObjectACL(ctx, input)
   checkErr(err)
   fmt.Println("PutObjectACL Request ID:", output.RequestID)

}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Relevant Documentation**

For API documentation on configuring object read/write permissions, refer to [PutObjectAcl](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## **Obtaining read and write permissions for objects**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining access permissions for an object, you must have the <code>tos:GetObjectACL</code> permission or have the object's ACL permission READ_ACP. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


The following code is used to obtain access permissions for the object.

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

   
      objectKey = "*** Provide your object key ***"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

 
   getAclOutput, err := client.GetObjectACL(ctx, &tos.GetObjectACLInput{Bucket: bucketName, Key: objectKey})
   checkErr(err)
   fmt.Println("GetObjectACL Request ID:", getAclOutput.RequestID)
  
   fmt.Println("GetObjectACL Owner:", getAclOutput.Owner)
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
### **Relevant Documentation**

For API documentation on obtaining read and write permissions for an object, refer to [GetObjectAcl](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
