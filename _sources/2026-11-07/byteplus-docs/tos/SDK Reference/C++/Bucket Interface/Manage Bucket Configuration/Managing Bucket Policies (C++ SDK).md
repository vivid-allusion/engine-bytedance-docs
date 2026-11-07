---
title: "Managing Bucket Policies (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-policy-c-sdk"
---

A bucket (Bucket) in TOS serves as a globally unique namespace, functioning as a data container for storing object (Object) data. In TOS, permission control is implemented through IAM Policy, Bucket Policy, and bucket and object ACLs. Both bucket policies and ACLs are resource\-based permission control mechanisms within TOS. Compared to bucket ACLs, bucket policies offer more flexible permission configurations. This article describes how to set, retrieve, and delete a bucket authorization policy (Policy).

<span id=".6K6-572u5qG2562W55Wl"></span>
## Configure Bucket Policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure a bucket policy, you must have the <code>tos:PutBucketPolicy</code> permission. For detailed instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">Users with this permission can freely modify bucket policies and may use this permission to obtain other permissions. We recommend that you configure this permission with caution.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure the bucket policy for bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
   
    std::string policy = R"({"Statement": [{"Sid": "internal public","Effect": "Allow","Action":
["tos:ListBucket"],"Principal": "*","Resource": ["trn:tos:::examplebucket/*","trn:tos:::examplebucket"]}]})";
    
   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    
    PutBucketPolicyInput input(bucketName);
    input.setPolicy(Policy);
    auto output = client.putBucketPolicy(input);
    if (!output.isSuccess()) {
        
        std::cout << "PutBucketPolicy failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketPolicy success." << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5qG2562W55Wl"></span>
## Retrieve Bucket Policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the bucket policy, you must have the <code>tos:GetBucketPolicy</code> permission. For specific operations, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the bucket policy for bucket `examplebucket`.

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
    
 
    GetBucketPolicyInput input(bucketName);
    auto output = client.getBucketPolicy(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketPolicy failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
   
    std::cout << "GetBucketPolicy success, the bucket policy is:" << output.result().getPolicy() << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5qG2562W55Wl"></span>
## Bucket Deletion Policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete a policy, you must have the <code>tos:DeleteBucketPolicy</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the bucket policy for the bucket `examplebucket`.

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
    

    DeleteBucketPolicyInput input(bucketName);
    auto output = client.deleteBucketPolicy(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteBucketPolicy failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketPolicy success." << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For more information about bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/docs/tos/docs-bucket-authorization-policy-management).
