---
title: "Managing Cross-Origin Resource Sharing (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-origin-resource-sharing-c-sdk"
---

You can configure Cross\-Origin Resource Sharing (CORS) rules through the SDK interface. When TOS receives a cross\-origin request or an OPTIONS request, it reads the corresponding CORS rules for the bucket, performs the corresponding permission checks, and returns the appropriate headers to ensure the security of cross\-origin data transmission. This article describes how to configure cross\-region resource sharing for buckets.

<span id=".6K6-572u6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Configure Cross\-Origin Resource Sharing (CORS) rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To configure cross\-origin resource sharing rules for a bucket, you must have the <code>tos:PutBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to set the cross\-origin resource sharing rules for the bucket `examplebucket`.

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
    
 
    PutBucketCORSInput input(bucketName);
   
    CORSRule rule1;

    rule1.addAllowedOrigin("*");

    rule1.setAllowedMethods({"GET","PUT"});

    rule1.setAllowedHeaders({"header1", "header2"});

    rule1.setExposeHeaders({"tos-1", "tos-2"});

    rule1.setMaxAgeSeconds(100);
    
    auto rule2 = CORSRule();
    rule2.setAllowedOrigins({"http://example.com", "http://www.volcengine.com"});
    rule2.addAllowedMethod("GET");
    rule2.addAllowedHeader("header1");
    rule2.addExposeHeader("tos-1");
    rule2.setMaxAgeSeconds(100);
    
   
    std::vector<CORSRule> rules{rule1,rule2};
    input.setRules(rules);

    auto output = client.putBucketCORS(input);
    if (!output.isSuccess()) {
      
        std::cout << "PutBucketCORS failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketCORS success." << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Retrieve Cross\-Origin Resource Sharing Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the cross\-origin resource sharing rules of a bucket, you must have the <code>tos:GetBucketCORS</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the Cross\-Origin Resource Sharing rules for the bucket `examplebucket`.

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
    
 
    GetBucketCORSInput input(bucketName);
    auto output = client.getBucketCORS(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketCors failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }
    
    std::cout << "GetBucketCors success" << std::endl;

    for (const auto&  rule : output.result().getRules()) {
        std::cout << "Get Bucket Cors List:" << std::endl;
        for (auto const& origin : rule.getAllowedOrigins()) {
            std::cout << "Allowed origin:" << origin << std::endl;
        }
        for (auto const& header : rule.getAllowedHeaders()) {
            std::cout << "Allowed header:" << header << std::endl;
        }
        for (auto const& header : rule.getExposeHeaders()) {
            std::cout << "Expose header:" << header << std::endl;
        }
        for (auto const& method : rule.getAllowedMethods()) {
            std::cout << "Allowed method:" << method << std::endl;
        }
        std::cout << "Allowed method:" << rule.getMaxAgeSeconds() << std::endl;
    }


    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Delete Cross\-Origin Resource Sharing (CORS) rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the bucket's cross\-origin resource sharing rules, your account must have the <code>tos:PutBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to delete the cross\-origin resource sharing (CORS) rules for a specified bucket.

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
    
  
    DeleteBucketCORSInput input(bucketName);
    auto output = client.deleteBucketCORS(input);
    if (!output.isSuccess()) {
        
        std::cout << "DeleteBucketCORS failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketCORS success." << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about Cross\-Origin Resource Sharing, see [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).
