---
title: "Managing Mirroring Rules (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-image-return-to-source-c-sdk"
---

Mirror\-based back\-to\-origin (mirroring) is primarily used in scenarios involving seamless data migration to TOS. For example, when your web service is already running on a self\-built origin server or other cloud products and you need to migrate it to TOS, you can use a mirroring rule during the migration process to retrieve some data that has not yet been migrated to TOS. This ensures the normal operation of the service throughout the migration.

<span id=".6K6-572u6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Configure mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure mirroring rules for a bucket, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">A bucket supports the creation of only one back\-to\-origin rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirroring supports objects up to a maximum size of 5 GiB. If you need to request objects larger than 5 GiB, please use the <a href="https://docs.byteplus.com/docs/tos/Scope-download-c-sdk">range download</a> feature.</div>


* <div data-tips="true" data-tips-type="warning">The maximum supported object size for redirect\-based back\-to\-origin is 300 GiB.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to set the mirroring rule for the specified bucket `examplebucket`.

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
    

    PutBucketMirrorBackInput input(bucketName);

    MirrorBackRule rule1;
    
    auto condition = rule1.getCondition();
    condition.setHttpCode(404);
    rule1.setCondition(condition);
    

    auto redirect = Redirect();
 
    redirect.setRedirectType(RedirectType::RedirectMirror);

    SourceEndpoint endpoint;
    endpoint.setPrimary({"https://www.example.com/"});
    endpoint.setFollower({"https://www.example.com/"});
    PublicSource publicSource(endpoint);
    redirect.setPublicSource(publicSource);
    
 
    redirect.setPassQuery(true);
    
    redirect.setFollowRedirect(true);
 
    redirect.setFetchSourceOnRedirect(true);
    
   
    MirrorHeader mirrorHeaders;
    mirrorHeaders.setPassAll(false);
    
    mirrorHeaders.setPass({"header-1", "header-2"});

    mirrorHeaders.setRemove({"header-3", "header-4"});
    redirect.setMirrorHeader(mirrorHeaders);
    

    std::vector<MirrorBackRule> rules{rule1};
    input.setRules(rules);
    
    auto output = client.putBucketMirrorBack(input);
    if (!output.isSuccess()) {
  
        std::cout << "PutBucketMirrorBack failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "PutBucketMirrorBack success." << std::endl;
    

    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Retrieve mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To retrieve the mirroring rules for a bucket, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the mirroring rules for the specified bucket `examplebucket`.

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
    

    GetBucketMirrorBackInput input(bucketName);
    auto output = client.getBucketMirrorBack(input);
    if (!output.isSuccess()) {

        std::cout << "GetBucketMirrorBack failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }


    auto mirrorBackRules= output.result().getRules();
    for (auto& rule : mirrorBackRules){

        std::cout << "rule:" << rule.getId() << std::endl;

  
        auto conditon = rule.getCondition();
        std::cout << "http code conditon:" << conditon.getHttpCode() << std::endl;

       
        auto redirect = rule.getRedirect();
        std::cout << "redirect:" << redirect.getStringFormatRedirectType() << "," << redirect.isFetchSourceOnRedirect() << "," <<
                redirect.isPassQuery() << "," <<  redirect.isFollowRedirect() << std::endl;

        auto mirrorHeader = redirect.getMirrorHeader();
        std::cout << "redirect-mirrorHeader:" << mirrorHeader.isPassAll() << std::endl;
        std::cout << "redirect-mirrorHeader-pass:" << std::endl;
        for(auto& pass : mirrorHeader.getPass()){
            std::cout << pass << std::endl;
        }
        std::cout << "redirect-mirrorHeader-remove:" << std::endl;
        for(auto& remove : mirrorHeader.getRemove()){
            std::cout << remove << std::endl;
        }
    
        auto publicSource = redirect.getPublicSource();
        auto sourceEndpoint = publicSource.getSourceEndpoint();
        std::cout << "redirect-publicSource-sourceEndpoint:" << std::endl;
        std::cout << "redirect-publicSource-sourceEndpoint-primary:" << std::endl;
        for(auto& primary : sourceEndpoint.getPrimary()){
            std::cout << primary << std::endl;
        }
        std::cout << "redirect-publicSource-sourceEndpoint-follower:" << std::endl;
        for(auto& follower : sourceEndpoint.getFollower()){
            std::cout << follower << std::endl;
        }
    }


    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5qG255qE6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## Delete mirroring rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the mirroring rule for a bucket, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the mirroring rule for the specified bucket `examplebucket`.

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
    
   
    DeleteBucketMirrorBackInput input(bucketName);
    auto output = client.deleteBucketMirrorBack(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteBucketMirrorBack failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketMirrorBack success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**

For more information about mirroring, see [Configuring back-to-origin rules](https://docs.byteplus.com/docs/tos/Overview9).
