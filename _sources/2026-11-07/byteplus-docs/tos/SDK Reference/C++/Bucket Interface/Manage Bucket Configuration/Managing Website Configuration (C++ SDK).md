---
title: "Managing Website Configuration (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-site-configuration-c-sdk"
---

TOS supports hosting static websites. You can store all static website content in a TOS bucket. After configuring static website rules, the website can be accessed via the bucket domain name.

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
## Set Website Configuration Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only one static website hosting rule can be created in a storage bucket.</div>


* <div data-tips="true" data-tips-type="warning">After configuring the static website, you must bind a custom domain name for it to take effect. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Bind Custom Domain Name</a>.</div>


* <div data-tips="true" data-tips-type="warning">For security and compliance purposes, effective October 18, 2022, when you access web\-type files (with mimetype 'text/html' and extensions including HTM, HTML, JSP, PLG, HTX, STM) via the default domain of a storage bucket, the Response Header will automatically include <code>Content-Disposition:attachment</code>. As a result, when these files are accessed through a browser, the website will not be previewed directly; instead, the website's content will be downloaded locally.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to set the website configuration rules for the bucket examplebucket.

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

    PutBucketWebsiteInput input(bucketName);
   
    // RedirectAllRequestsTo redirectAllRequestsTo("www.volcengine.com", "https");
    // input.setRedirectAllRequestsTo(redirectAllRequestsTo);

 
    IndexDocument indexDocument("index.html", true);

   
    ErrorDocument errorDocument("error.html");

  
    RoutingRuleCondition condition("website", 404);

    RoutingRuleRedirect redirect(ProtocolType::Http, "www.volcengine.com", "voc", 301);
    RoutingRule rule(condition, redirect);

    input.setIndexDocument(indexDocument);
    input.setErrorDocument(errorDocument);
    input.setRoutingRules({rule});

    auto output = client.putBucketWebsite(input);
    if (!output.isSuccess()) {
       
        std::cout << "PutBucketWebsite failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketWebsite success." << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W572R56uZ6YWN572u6KeE5YiZ"></span>
## Retrieve Website Configuration Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the website configuration rules for a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the website configuration rules for the bucket 'examplebucket'.

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
    GetBucketWebsiteInput input(bucketName);

    auto output = client.getBucketWebsite(input);
    if (!output.isSuccess()) {
     
        std::cout << "GetBucketWebsite failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketWebsite success." << std::endl;
    auto res = output.result();
    if (res.getRedirectAllRequestsTo() != nullptr){
        auto redirectAllRequestsTo= *res.getRedirectAllRequestsTo();
        std::cout << "host name:" << redirectAllRequestsTo.getHostName() << std::endl;
        std::cout << "protocol:" << redirectAllRequestsTo.getProtocol() << std::endl;
    }
    if (res.getIndexDocument() != nullptr){
        auto indexDocument = *res.getIndexDocument();
        std::cout << "indexDocument suffix:" << indexDocument.getSuffix() << std::endl;
        std::cout << "indexDocument forbidden subdir:" << indexDocument.isForbiddenSubDir() << std::endl;
    }
    if (res.getErrorDocument() != nullptr){
        auto errorDocument = *res.getErrorDocument();
        std::cout << "error document key:" << errorDocument.getKey() << std::endl;
    }
    for (const auto& rule : output.result().getRoutingRules()) {
        auto condition = rule.getCondition();
        auto redirect = rule.getRedirect();
        std::cout << "Condition:" << std::endl;
        std::cout << "KeyPrefixEquals:" << condition.getKeyPrefixEquals() << std::endl;
        std::cout << "HttpErrorCodeReturnedEquals:" << condition.getHttpErrorCodeReturnedEquals() << std::endl;
        std::cout << "Redirect:" << std::endl;
        std::cout << "HostName:" << redirect.getHostName() << std::endl;
        std::cout << "ReplaceKeyPrefixWith:" << redirect.getReplaceKeyPrefixWith() << std::endl;
        std::cout << "ProtocolType:" << redirect.getStringFormatProtocol() << std::endl;
        std::cout << "HttpRedirectCode:" << redirect.getHttpRedirectCode() << std::endl;
        std::cout << "ReplaceKeyWith:" << redirect.getReplaceKeyWith() << std::endl;
    }

  
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk572R56uZ6YWN572u6KeE5YiZ"></span>
## Delete Website Configuration Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the website configuration rules of a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the website configuration rules for the bucket examplebucket.

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
    DeleteBucketWebsiteInput input(bucketName);
    auto output = client.deleteBucketWebsite(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteBucketWebsite failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketWebsite success." << std::endl;
   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For more information about configuring static website settings, see [Configuring a Static Website](https://docs.byteplus.com/docs/tos/Set-up-a-static-website).
