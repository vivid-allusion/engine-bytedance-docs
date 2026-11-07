---
title: "Range Download (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-c-sdk"
---

If you only need to retrieve part of the data from an object, you can use the range download feature to obtain data within a specified range. This article provides sample code for range download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object many times simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. It is recommended that you use CDN products to enhance performance while simultaneously reducing your costs. For detailed information on accessing TOS via CDN, see [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5oyH5a6aLXN0YXJ0LWVuZC3kuIvovb3lr7nosaE="></span>
### **Specify Start/End Download Objects**

The following code is used to specify RangeStart/RangeEnd to download a portion of the data from the object `exampledir/exampleobject.txt` in the bucket `examplebucket`.

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

    GetObjectV2Input input(bucketName, objectName);

   
    input.setRangeStart(0);
    input.setRangeEnd(1000);
    
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "GetObject failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }

    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".6L-b5bqm5p2h5aSE55CG"></span>
### **Progress Bar Handling**

The following code is used to configure the progress bar during range downloads.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static void ProgressCallback(std::shared_ptr<DataTransferStatus> datatransferstatus) {
    int64_t consumedBytes = datatransferstatus->consumedBytes_;
    int64_t totalBytes = datatransferstatus->totalBytes_;
    int64_t rwOnceBytes = datatransferstatus->rwOnceBytes_;
    DataTransferType type = datatransferstatus->type_;
    int64_t rate = 100 * consumedBytes / totalBytes;
    std::cout << "rate:" << rate << ","
              << "ConsumedBytes:" << consumedBytes << ","
              << "totalBytes:" << totalBytes << ","
              << "rwOnceBytes:" << rwOnceBytes << ","
              << "DataTransferType:" << type << std::endl;
}

int main(void){
   
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
   
    std::string objectName = "exampledir/exampleobject.txt";

   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    GetObjectV2Input input(bucketName, objectName);
    
    input.setRangeStart(0);
    input.setRangeEnd(1000);
    
    DataTransferListener processHandler = {ProgressCallback, nullptr};
    input.setDataTransferListener(processHandler);

    auto output = client.getObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Rate Limiting**

The following code configures client\-side throttling for range downloads.

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

    GetObjectV2Input input(bucketName, objectName);
   
    input.setRangeStart(0);
    input.setRangeEnd(1000);
   
    std::shared_ptr<RateLimiter> RateLimiter(NewRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024));
    input.setRateLimiter(RateLimiter);
    
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "GetObject failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }

    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;

 
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
