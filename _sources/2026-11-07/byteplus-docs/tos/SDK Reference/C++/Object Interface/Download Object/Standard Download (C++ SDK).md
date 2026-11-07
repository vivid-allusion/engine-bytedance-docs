---
title: "Standard Download (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-c-sdk"
---

Standard download refers to downloading a single object via the getObject method. This process supports two modes: downloading the object into memory or saving it to a local file. Additionally, it provides features such as progress bar display, client\-side rate limiting, and the ability to override HTTP response headers during object download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For specific instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To download a specified version of an object from a bucket with versioning enabled, you must have the `tos:GetObjectVersion` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities at the same time, your access speed will be limited by TOS bandwidth and geographic restrictions. It is recommended that you use CDN products to enhance performance while also reducing your costs. For detailed information on accessing TOS via CDN, see [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiL6L295a-56LGh5Yiw5YaF5a2Y"></span>
### **Download object to memory**

The following code is used to download the object `exampledir/exampleobject.txt` from the bucket `examplebucket` into memory.

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
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    auto stream = output.result().getContent();
    std::string ss;

    char streamBuffer[256];
    memset(streamBuffer, 0, 256);
    while (stream->good()) {
        stream->read(streamBuffer, 256);
        
    }
    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".5LiL6L295Yiw5pys5Zyw5paH5Lu2"></span>
### **Download to local file**

The following code is used to download the object `exampledir/exampleobject.txt` from the bucket `examplebucket` to a local file.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string filePath = "/localpath/examplefile.txt";
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    GetObjectToFileInput input(bucketName, objectName, filePath);
    auto output = client.getObjectToFile(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetObjectToFile failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "GetObjectToFile success. the object etag:" << output.result().getETags()  << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".5LiL6L295pe26YeN5YaZLWh0dHAt5ZON5bqU5aS0"></span>
### **Overwriting HTTP Response Headers During Download**

The following code is used to download the object `exampledir/exampleobject.txt` from the bucket `examplebucket` and to rewrite the HTTP response headers.

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
   
    input.setResponseCacheControl("no-cache");
    input.setResponseContentDisposition("attachment; filename=123.txt");
    //  input.setResponseContentEncoding("gzip");
    //  input.setResponseContentLanguage("en-US");
    //  input.setResponseContentType("text/plain");
    
  
    //    time_t expires = TimeUtils::transGMTFormatStringToTime("Sat, 1 Jan 2022 00:00:00 GMT");
    //    if (expires == -1){
    //        std::cout << "Check expires, transfer string type to time_t failed." << std::endl;
    //    }
 
    //        time_t expirationTime = time(nullptr);
    //        tm* gmtmExpiration = gmtime(&expirationTime);
    //        gmtmExpiration->tm_min = 0;
    //        gmtmExpiration->tm_hour = 0;
    //        gmtmExpiration->tm_sec = 0;
    //        gmtmExpiration->tm_mday = 1;
    //        gmtmExpiration->tm_mon = 0;
    //        gmtmExpiration->tm_wday = 6;
    //        gmtmExpiration->tm_year = gmtmExpiration->tm_year;
    //        auto expires = timegm(gmtmExpiration);
    //
    //        input.setResponseExpires(expires);
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


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Configuring the Progress Bar**

The following code is used to configure the download progress bar.

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
### **Configure Client Bandwidth Limiting**

The following code is used to configure the speed limit for the download client.

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
