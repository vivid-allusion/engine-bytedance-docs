---
title: "Restricted Download (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-c-sdk"
---

If you wish to set constraints—such as object ETag or modification time—when downloading an object, you can use the conditional download feature provided by the TOS C++ SDK. The object will be downloaded only if its information meets the conditions you specify. This article describes how to download objects under specified conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object many times simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. It is recommended that you use CDN products to enhance performance while also reducing your costs. For detailed information on accessing TOS via CDN, please refer to [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## Description of Limiting Conditions

The following are the restrictions supported by TOS.


|Parameters |**Description** |
|---|---|
|If\-Match |The object is returned only if the provided `ETag` matches the object's `ETag`; otherwise, a 412 Precondition Failed response is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time; otherwise, a 304 Not Modified response is returned. The time format is RFC1123 GMT. |
|If\-None\-Match |The object is returned only if the provided `ETag` does not match the object's `ETag`; otherwise, a 304 Not Modified response is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time; otherwise, a 412 Precondition Failed response is returned. The time format is RFC1123 in GMT. |


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to conditionally download the object `exampledir/exampleobject.txt` from the bucket `examplebucket`.

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

    input.setIfModifiedSince(time(nullptr)-86400);
   
    input.setIfUnmodifiedSince(time(nullptr));
  
    HeadObjectV2Input headInput(bucketName,objectName);
    auto headOutput = client.headObject(headInput);
    auto etag = headOutput.result().getETag();
    input.setIfMatch(etag);
     // input.setIfNoneMatch(etag)

    auto output = client.getObject(input);
    if (!output.isSuccess()) {
  
        std::cout << "GetObject failed." << output.error().String() << std::endl;
        if (output.error().getStatusCode() == 304){
            std::cout << "StatusCode: 304" << output.error().String() << std::endl;
        }
        if (output.error().getStatusCode() == 412){
            std::cout << "StatusCode: 412" << output.error().String() << std::endl;
        }
   
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

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
