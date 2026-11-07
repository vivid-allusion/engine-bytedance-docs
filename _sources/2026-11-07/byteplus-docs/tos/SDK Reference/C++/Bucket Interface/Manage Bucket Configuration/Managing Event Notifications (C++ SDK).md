---
title: "Managing Event Notifications (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-event-notifications-c-sdk"
---

TOS supports delivering changes of certain events to the function service. If you wish to monitor resource changes in TOS in real time, you can configure event notification rules. This article presents sample code for event notification.

For more information about Function Service, see [What is Function Service](https://docs.byteplus.com/en/docs/faas/What_is_Function_Service).

<span id=".6K6-572u5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## Configure Event Notification Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A maximum of 10 event notification rules can be created for a single storage bucket.</div>


* <div data-tips="true" data-tips-type="warning">An event notification rule can specify only one push target, which must be a function service.</div>


* <div data-tips="true" data-tips-type="warning">An object cannot match multiple rules that contain the same event type; that is, within the same bucket, the ranges of <strong>type + prefix/suffix</strong> combinations among different rules must not overlap.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure event notification rules for the bucket examplebucket.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";
  
    std::string cloudFunction = "your cloud function";
    
  
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

    PutBucketNotificationInput input(bucketName);

  

    FilterKey filterKey;
    
    FilterRule rule1({"prefix", "test/"});
 
    FilterRule rule2({"suffix", ".png"});
    filterKey.setRules({rule1,rule2});
    Filter filter(filterKey);
    
    CloudFunctionConfiguration configuration;

    configuration.setId("test-id");
    
    configuration.setEvents({"tos:ObjectCreated:Put"});
 
    configuration.setCloudFunction(cloudFunction);
 
    configuration.setFilter(filter);

    auto output = client.putBucketNotification(input);
    if (!output.isSuccess()) {
     
        std::cout << "PutBucketNotification failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketNotification success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## Retrieve Event Notification Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, you must be the bucket owner to obtain the event notification rules for a bucket.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the event notification rules for the bucket 'examplebucket'.

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
    GetBucketNotificationInput input(bucketName);

    auto output = client.getBucketNotification(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketNotification failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketNotification success." << std::endl;
    for (const auto& config : output.result().getCloudFunctionConfigurations()) {
        std::cout << "id:" << config.getId() << std::endl;
        std::cout << "cloud function:" << config.getCloudFunction() << std::endl;
        auto rules = config.getFilter().getKey().getRules();
        for(const auto&  rule : rules){
            std::cout << "filter name:" << rule.getName() << std::endl;
            std::cout << "filter value:" << rule.getValue() << std::endl;
        }
        for(const auto&  event : config.getEvents()){
            std::cout << "event:" << event << std::endl;
        }
    }

    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about event notification configuration, see [Event Notification](https://docs.byteplus.com/docs/tos/Event-notification-overview).
