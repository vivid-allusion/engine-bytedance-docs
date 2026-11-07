---
title: "Managing Bucket ACLs (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-acl-c-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container for storing Object data (Object). This article describes how to set and get the read and write permissions (ACL) of a bucket.

<span id=".6K6-572u5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## **Configuring Bucket Access Permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set read and write permissions for a bucket, you must have the <code>tos:PutBucketACL</code> permission or the WRITE_ACP bucket ACL permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">To configure a bucket ACL, the account must be either the creator of the bucket or possess write permission for the bucket ACL.</div>


* <div data-tips="true" data-tips-type="warning">ACL configuration is supported only for the main account ID; ACL configuration for sub\-accounts is not supported.</div>



<span id=".5qG2LWFjbC3or7TmmI4="></span>
### Bucket ACL Overview


|**Access Permissions** |**Description** |**corresponding enumeration value** |
|---|---|---|
|READ |Allow the authorized party to list objects in the bucket. |PermissionType::Read |
|WRITE |Permit authorized users to create, overwrite, and delete any objects within the storage bucket. |PermissionType::Write |
|READ_ACP |Permit authorized users to read the bucket ACL. |PermissionType::ReadAcp |
|WRITE_ACP |Allow grantees to write to the bucket ACL. |PermissionType::WriteAcp |
|FULL_CONTROL |Grant the grantee READ, WRITE, READ_ACP, and WRITE_ACP permissions on the storage bucket. |PermissionType::FullControl |


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Configuring access permissions in the request header**

You can use the `x-tos-acl` header field to select predefined permissions. Set the bucket's read and write permissions using the `x-tos-acl` request header as follows.


|**Access Permissions** |**Description** |**corresponding enumeration value** |
|---|---|---|
|private |Private. The owner of the bucket possesses full control permissions, while no permissions are granted to other users. The default policy is private. |ACLType::Private |
|public\-read |Public reading. Anyone has READ permission for the bucket. |ACLType::PublicRead |
|public\-read\-write |Public Read/Write Anyone has READ and WRITE permissions for the bucket. |ACLType::PublicReadWrite |
|authenticated\-read |Any authenticated user has READ permission on the bucket. |ACLType::AuthenticatedRead |


The following code demonstrates how to configure bucket read and write permissions using `x-tos-acl`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    
    PutBucketAclInput input(bucketName);
    input.setAcl(ACLType::PublicRead);
    auto output = client.putBucketAcl(input);
    if (!output.isSuccess()) {
       
        std::cout << "SetBucketACL failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "SetBucketACL success." << std::endl;

   
    CloseClient();
    return 0;
}
```


The following code sets read and write permissions for the bucket `examplebucket` via the `x-tos-grant-*` request header.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";

    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    
    PutBucketAclInput input(bucketName);
 
    input.setGrantFullControl("id=\"1000000001\"");
    input.setGrantRead("canned=\"AllUsers\"");
    auto output = client.putBucketAcl(input);
    if (!output.isSuccess()) {
       
        std::cout << "SetBucketACL failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "SetBucketACL success." << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Provide detailed ACL permission information in the request body.** 

The following code is used to set the permission information for the bucket `examplebucket` in the request body.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
   
    std::string bucketName = "examplebucket";
    
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);
    
    
    PutBucketAclInput input(bucketName);
    Owner owner;
    owner.setId("test-cid");
    GranteeV2 granteev2;
    granteev2.setType(GranteeType::Group);
    granteev2.setCanned(CannedType::AllUsers);
    GrantV2 grantv2;
    grantv2.setGrantee(granteev2);
    grantv2.setPermission(PermissionType::WriteAcp);
    input.setOwner(owner);
    input.setGrants({grantv2});
    auto output = client.putBucketAcl(input);
    if (!output.isSuccess()) {
       
        std::cout << "SetBucketACL failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "SetBucketACL success." << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## Obtaining Bucket Access Permissions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain access to a bucket, you must have the <code>tos:GetBucketACL</code> permission or the bucket ACL permission <code>READ_ACP</code>. For specific operations, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
    
    PermissionType permission_;

    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
    
  
    GetBucketAclInput input(bucketName);
    auto output = client.getBucketAcl(input);
    if (!output.isSuccess()) {
     
        std::cout << "GetBucketACL failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }


    std::cout << "GetBucketACL success." << std::endl;
    auto grant = output.result().getGrant();
    for(auto& g : grant){
        std::cout << " the premission is:" << g.getStringFormatPermission()
                  << " the grantee id is:" <<  g.getGrantee().getId()
                  << " the display name is:" <<  g.getGrantee().getDisplayName()
                  << " the grantee is:" <<  g.getGrantee().getStringFormatType()
                  << " the canned is:" <<  g.getGrantee().getStringFormatCanned() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For information on managing bucket permissions, see [Bucket ACLs](https://docs.byteplus.com/docs/tos/docs-bucket-acls).
