---
title: "Managing Object Read/Write Permissions (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-read-and-write-permissions-c-sdk"
---

This article describes how to obtain and configure access permissions for objects. The access permissions of an object take precedence over those of the bucket. If no access permissions are set for the object, the bucket's access permissions will apply.

<span id=".5a-56LGhLWFjbC3or7TmmI4="></span>
## Object ACL Overview

Object ACL permissions include the following types.


|**Access Permissions** |**Description** |**corresponding enumeration value** |
|---|---|---|
|READ |Authorized users are permitted to read object data and its metadata. |PermissionType::Read |
|READ_ACP |Allow the authorized user to read the object's ACL. |PermissionType::ReadAcp |
|WRITE_ACP |Authorized users are permitted to write ACLs for applicable objects. |PermissionType::WriteAcp |
|FULL_CONTROL |Authorized users are permitted to have READ, READ_ACP, and WRITE_ACP permissions on the object. |PermissionType::FullControl |


<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## **Configuring Object Read and Write Permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set object read/write permissions, you must have the <code>tos:PutObjectACL</code> permission or the <code>WRITE_ACP</code> object ACL permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


You may specify detailed ACL permission information either in the request body or by setting it in the request header.

<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Set access permissions in the request header**

There are six categories of object read and write permissions that can be configured via the `x-tos-acl` request header.


|**Access Permissions** |**Description** |**corresponding enumeration value** |
|---|---|---|
|Private |Private. The owner of the object possesses all permissions, while other users are not authorized to operate the object.<br><br>The default policy is private. |ACLType::Private |
|Public Reading |Public reading. Anyone has READ permission on the object. |ACLType::PublicRead |
|Public Read/Write |Public read/write access. Everyone has READ permission on the object. |ACLType::PublicReadWrite |
|Authenticated User Read |Any authenticated user has READ permission on the object. |ACLType::AuthenticatedRead |
|Bucket Owner Read |The owner of the bucket and object has READ permission for the object. |ACLType::BucketOwnerRead |
|The bucket owner possesses all permissions. |The owner of the bucket and the owner of the object have full control permissions over the object. |ACLType::BucketOwnerFullControl |


The following code sets the read and write permissions of an object through `x-tos-acl`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
 
    std::string objectName = "exampledir/exampleobject.txt";

   
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

    PutObjectAclV2Input input(bucketName,objectName);
  
    input.setAcl(ACLType::PublicRead);
    auto output = client.putObjectAcl(input);
    if (!output.isSuccess()) {
      
        std::cout << "PutObjectAcl failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }

    std::cout << "PutObjectAcl success." << std::endl;

    CloseClient();
    return 0;
}
```


The following code sets read and write permissions for the object `exampledir/exampleobject.txt` in the bucket `examplebucket` by using the `x-tos-grant-*` request header.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";

    std::string objectName = "exampledir/exampleobject.txt";

   
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

。
    PutObjectAclV2Input input(bucketName,objectName);
  
    input.setGrantFullControl("id=\"1000000001\"");
    input.setGrantRead("canned=\"AllUsers\"");
    auto output = client.putObjectAcl(input);
    if (!output.isSuccess()) {
        
        std::cout << "SetObjectACL failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }

    std::cout << "SetObjectACL success." << std::endl;
 
    CloseClient();
    return 0;
}
```


<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Provide detailed ACL permission information in the request body.** 

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
  

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
  
    std::string objectName = "exampledir/exampleobject.txt";

    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);


    PutObjectAclV2Input input(bucketName,objectName);

    
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
    auto output = client.putObjectAcl(input);
    if (!output.isSuccess()) {
       
        std::cout << "SetObjectACL failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }

    std::cout << "SetObjectACL success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5a-56LGh6K-75YaZ5p2D6ZmQ"></span>
### **Configuring object read and write permissions during standard upload**

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";

 
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    
    std::string data("Object data to be uploaded");
    auto ss = std::make_shared<std::stringstream>(data);
    PutObjectV2Input input(bucketName, objectName, ss);
    
    input.setAcl(ACLType::PublicRead);
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "PutObjectWithMetaData failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "PutObjectWithMetaData success. the object etag:" << output.result().getETag() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5YiG54mH5LiK5Lyg5pe26K6-572u5a-56LGh6K-75YaZ5p2D6ZmQ"></span>
### **Configuring object read/write permissions during multipart upload**

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static int64_t getFileSize(const std::string& file)
{
    std::fstream f(file, std::ios::in | std::ios::binary);
    f.seekg(0, f.end);
    int64_t size = f.tellg();
    f.close();
    return size;
}

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    
    CreateMultipartUploadInput input(bucketName, objectName);
    
    input.setAcl(ACLType::PublicRead);
    auto upload = client.createMultipartUpload(input);
    if (!upload.isSuccess()) {
        
        std::cout << "createMultipartUpload failed." << upload.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "createMultipartUpload success." << std::endl;

    
    std::string fileToUpload = "yourLocalFilename";
    
      int64_t partSize = 5 * 1024 * 1024;
    std::vector<UploadedPartV2> partResList;
    auto fileSize = getFileSize(fileToUpload);
    int partCount = static_cast<int>(fileSize / partSize);
    
    if (fileSize % partSize != 0) {
        partCount++;
    }

    
    auto uploadId = upload.result().getUploadId();
    for (int i = 1; i <= partCount; i++) {
        auto offset = partSize * (i - 1);
        auto size = (partSize < fileSize - offset) ? partSize : (fileSize - offset);
        std::shared_ptr<std::iostream> content = std::make_shared<std::fstream>(fileToUpload, std::ios::in|std::ios::binary);
        content->seekg(offset, std::ios::beg);

        UploadPartV2Input uploadPartInput(bucketName, objectName,uploadId, size,i,content);
        auto uploadPartOutput = client.uploadPart(uploadPartInput);
        if (uploadPartOutput.isSuccess()) {
             std::cout << "uploadPart failed." << upload.error().String() << std::endl;
             
            CloseClient();
            return -1;
        }

        UploadedPartV2 part(i, uploadPartOutput.result().getETag());
        partResList.push_back(part);
    }

    
    CompleteMultipartUploadV2Input completeMultipartUploadInput(bucketName, objectName, uploadId, partResList);
    auto com = client.completeMultipartUpload(completeMultipartUploadInput);
    if (!com.isSuccess()) {
        
        std::cout << "CompleteMultipartUpload failed." << upload.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "CompleteMultipartUpload success." << com.result().getRequestInfo().getRequestId() << std::endl;
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Relevant Documentation**

For API documentation on configuring object read and write permissions, refer to [PutObjectAcl](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## Obtaining read and write permissions for an object

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain access permissions for an object, you must have the <code>tos:GetObjectACL</code> permission or the object's ACL permission <code>READ_ACP</code>. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".6YCa6L-HLWdldG9iamVjdGFjbC3mjqXlj6Pmn6Xor6Llr7nosaHor7vlhpnmnYPpmZA="></span>
### Query object read/write permissions via the getObjectACL interface.

The following code is used to obtain read and write permissions for the object `exampledir/exampleobject.txt` in the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";

   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    GetObjectAclV2Input input(bucketName,objectName);
    auto output = client.getObjectAcl(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetOBjectAcl failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "GetObjectAcl success." << std::endl;
    
    auto grant = output.result().getGrant();
    for(auto& g : grant) {
        std::cout << " the premission is:" << g.getStringFormatPermission()
                  << " the grantee id is:" << g.getGrantee().getId()
                  << " the display name is:" << g.getGrantee().getDisplayName()
                  << " the grantee is:" << g.getGrantee().getStringFormatType()
                  << " the canned is:" << g.getGrantee().getStringFormatCanned() << std::endl;
    }
    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Relevant Documentation**

For documentation on obtaining read and write permissions for an object via the API, refer to [GetObjectAcl](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
