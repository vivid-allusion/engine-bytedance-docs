---
title: "Managing Bucket Lifecycle (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-the-bucket-lifecycle-c-sdk"
---

TOS supports configuring lifecycle rules for buckets (Lifecycle), enabling automatic conversion of object storage types and automatic deletion of expired objects. This facilitates efficient utilization of storage features and optimizes storage space. You can use the lifecycle management feature of object storage through the SDK to delete expired objects, thereby reducing storage costs. When configuring lifecycle rules, you can specify an object prefix or object tag for which the rule will take effect. If you specify two activation conditions simultaneously, the object must satisfy all configured conditions for the lifecycle rule to be applied.

<span id=".6K6-572u55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Configure lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure lifecycle rules for a bucket, you must have the <code>tos:PutLifecycleConfiguration</code> permission. For detailed instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">If lifecycle rules have already been configured for the bucket, performing this operation will overwrite the existing configuration. To append lifecycle rules, first use GetLifecycleConfiguration to retrieve the current rules, then add the new rules, and finally call PutLifecycleConfiguration to update the rules.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to configure the lifecycle rules for the bucket `examplebucket`.

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
    
   
    PutBucketLifecycleInput input(bucketName);
    
 
    auto rule1 = LifecycleRule();
  
    rule1.setId("rule1");

    rule1.setPrefix("test1/");
 
    rule1.setStatus(StatusType::StatusEnabled);

    rule1.setExpiratioon(std::make_shared<Expiration>(60));

    rule1.addTag(Tag("key1", "value1"));
    rule1.addTag(Tag("key2", "value2"));
    

    auto rule2 = LifecycleRule();

    rule2.setId("rule2");
 
    rule2.setPrefix("test2/");

    rule2.setStatus(StatusType::StatusDisabled);

    time_t expirationTime = time(nullptr);
    tm* gmtmExpiration = gmtime(&expirationTime);
    gmtmExpiration->tm_min = 0;
    gmtmExpiration->tm_hour = 0;
    gmtmExpiration->tm_sec = 0;
    gmtmExpiration->tm_year = gmtmExpiration->tm_year + 1;
    auto exactTime = timegm(gmtmExpiration);
   
 
    rule2.setExpiratioon(exactTime);
    
    
    auto rule3 = LifecycleRule();
    rule3.setId("rule3");
    rule3.setPrefix("test3/");
    rule3.setStatus(StatusType::StatusDisabled);
    
    
    auto transition = Transition();
    transition.setDays(365);
    transition.setStorageClass(StorageClassType::ARCHIVE_FR);
    rule3.addTransition(transition);
    
    
    auto transition1 = NoncurrentVersionTransition(10, StorageClassType::IA);
    
    
    auto transition2 = NoncurrentVersionTransition(20, StorageClassType::ARCHIVE_FR);
    
    
    rule3.setNoncurrentVersionExpiration(30);
    
    std::vector<NoncurrentVersionTransition> noncurrentVersionStorageTransitions{transition1, transition2};
    rule3.setNoncurrentVersionTransitions(noncurrentVersionStorageTransitions);
    
    
    std::vector<LifecycleRule> rules{rule1, rule2, rule3};
    input.setRules(rules);
    
    auto output = client.putBucketLifecycle(input);
    if (!output.isSuccess()) {
        
        std::cout << "PutBucketLifecycle failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketLifecycle success." << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Retrieve lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To retrieve lifecycle rules for a bucket, you must have the <code>tos:GetLifecycleConfiguration</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information on lifecycle rules, please refer to <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to retrieve the lifecycle rules for the bucket `examplebucket`.

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
    
    
    GetBucketLifecycleInput input(bucketName);
    auto output = client.getBucketLifecycle(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetBucketLifecycle failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    
    auto lifycycleRules= output.result().getRules();
    for (auto& rule : lifycycleRules){
        
        std::cout << "rule:" << rule.getId() << "," << rule.getPrefix() << "," << rule.getStringFormatStatus() << ","
                  << "hasExpiration:" << rule.hasExpiration() << "," << std::endl;

        
        auto taglist = rule.getTags();
        for (const auto& tag : taglist)
        {
            std::cout <<"GetBucketLifecycle tag success, Key:"
                      << tag.getKey() << "; Value:" << tag.getValue() << std::endl;
        }

        
        for (auto const lifeCycleTransition : rule.getTransitions()) {
            std::cout << "rule versions trans days:" << lifeCycleTransition.getDays() <<
                    " trans storage class: " << lifeCycleTransition.getStringFormatStorageClass() << std::endl;
        }

        
        for (auto const lifeCycleTransition : rule.getNoncurrentVersionTransitions()) {
            std::cout << "rule noncurrent versions trans days:" << lifeCycleTransition.getNoncurrentDays() <<
                    " trans storage class: " << lifeCycleTransition.getStringFormatStorageClass() << std::endl;
        }

        
        if (rule.hasExpiration()) {
            std::cout << "rule versions expiration days:" << rule.getExpiratioon()->getDays() << std::endl;
        }

        
        if (rule.hasNoncurrentVersionExpiration()) {
            std::cout << "rule noncurrent versions expiration days:" << rule.getNoncurrentVersionExpiration()->getNoncurrentDays() << std::endl;
        }

        
        if (rule.hasAbortInCompleteMultipartUpload()) {
            std::cout << "abort in completeMultipartUpload days:"
                      << rule.getAbortInCompleteMultipartUpload()->getDaysAfterInitiation() <<std::endl;
        }

    }

    
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Delete lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To delete lifecycle rules for a bucket, you must have the <code>tos:PutLifecycleConfiguration</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions configuration guide</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information about lifecycle rules, see <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the lifecycle rule of the bucket `examplebucket`.

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
    

    DeleteBucketLifecycleInput input(bucketName);
    auto output = client.deleteBucketLifecycle(input);
    if (!output.isSuccess()) {
   
        std::cout << "DeleteBucketLifecycle failed." << output.error().String() << std::endl;
  
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketLifecycle success." << std::endl;

 
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about lifecycle rules, see [Setting lifecycle rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).
