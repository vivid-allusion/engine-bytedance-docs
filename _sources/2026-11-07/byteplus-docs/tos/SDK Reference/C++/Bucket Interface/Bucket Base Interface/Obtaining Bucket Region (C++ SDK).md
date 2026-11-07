---
title: "Obtaining Bucket Region (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-the-bucket-region-c-sdk"
---

A bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. This article describes how to obtain the region where a bucket is located.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Only the bucket owner can view the region where the bucket is located.

* When managing buckets and objects within buckets using the TOS C++ SDK, you must use the domain name of the region where the bucket is located. For more information about regions and access domain names, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to obtain the region (referred to as Region or Location) where the bucket `examplebucket` is located.

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
    
   
    GetBucketLocationInput input(bucketName);
    auto output = client.getBucketLocation(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketLocation failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
  
    std::cout << "GetBucketLocation success, "
              <<  "the bucket region:" << output.result().getRegion()
              <<  "the bucket ExtranetEndpoint:" << output.result().getExtranetEndpoint()
              <<  "the bucket IntranetEndpoint:" << output.result().getIntranetEndpoint()
              << std::endl;
    
  
    CloseClient();
    return 0;
}
```
