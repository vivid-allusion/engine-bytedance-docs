---
title: "Managing Real-Time Logs (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-real-time-logs-c-sdk"
---

TOS provides log analysis capabilities, enabling you to retrieve and analyze access logs generated during your use of TOS through the log service. You can configure the relevant settings for log analysis functionality through the TOS C++ SDK.

<span id=".6K6-572u5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Configure real\-time log configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use the log analysis feature, you must have enabled the log service and authorized TOS to access Volcengine Log Service (TLS).</div>


* <div data-tips="true" data-tips-type="warning">After the log analysis feature is enabled, the logging service automatically creates log projects and topics to store logs related to TOS.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure real\-time log configuration rules for the bucket examplebucket.

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

    PutBucketRealTimeLogInput input(bucketName);

    AccessLogConfiguration accessLogConfiguration;
    
    accessLogConfiguration.setUseServiceTopic(true);
    
    // accessLogConfiguration.setUseServiceTopic(false);
    // accessLogConfiguration.setTlsProjectId("Your Tls Project Id");
    // accessLogConfiguration.setTlsTopicId("Your Tls Topic Id");

    RealTimeLogConfiguration realTimeLogConfiguration;
  
    realTimeLogConfiguration.setRole("TOSLogArchiveTLSRole");
  
    realTimeLogConfiguration.setConfiguration(accessLogConfiguration);
    
    input.setConfiguration(realTimeLogConfiguration);
    auto output = client.putBucketRealTimeLog(input);
    if (!output.isSuccess()) {
       
        std::cout << "PutBucketRealTimeLog failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketRealTimeLog success." << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Retrieve Real\-Time Log Configuration Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the real\-time log configuration rules for a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the real\-time log configuration rules for the bucket 'examplebucket.'

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
    GetBucketRealTimeLogInput input(bucketName);

    auto output = client.getBucketRealTimeLog(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetBucketRealTimeLog failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketRealTimeLog success." << std::endl;
    auto config = output.result().getConfiguration();
    std::cout << "role:" << config.getRole() << std::endl;
    std::cout << "is use service topic:" << config.getConfiguration().isUseServiceTopic() << std::endl;
    std::cout << "project id:" << config.getConfiguration().getTlsProjectId() << std::endl;
    std::cout << "tls topic id:" << config.getConfiguration().getTlsTopicId() << std::endl;
    

    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Delete Real\-Time Log Configuration Rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the real\-time log configuration rules of a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the real\-time log configuration rule for the bucket 'examplebucket.'

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
    DeleteBucketRealTimeLogInput input(bucketName);
    auto output = client.deleteBucketRealTimeLog(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteBucketRealTimeLog failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketRealTimeLog success." << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information on real\-time log configuration, see [Log Analysis](https://docs.byteplus.com/docs/tos/Log-analysis).
