---
title: "Retrieving Bucket Metadata (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-c-sdk"
---

HeadBucket is used to retrieve information about a storage bucket (Bucket). Additionally, you can use the returned TosError to check the HTTP Code and determine whether the bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before you can obtain bucket metadata, you must have the `tos:HeadBucket` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If the bucket does not exist, this interface will return a 404 error. This mechanism is also commonly used to verify the existence of a bucket.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to obtain the metadata of the `examplebucket` bucket.

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
    
  
    HeadBucketV2Input input(bucketName);
    auto output = client.headBucket(input);
    if (!output.isSuccess()) {
       
        if(!output.error().isClientError() && output.error().getStatusCode() == 404) {
            std::cout << "Bucket not found." << std::endl;
        } else {
            std::cout << "HeadBucket failed." << output.error().String() << std::endl;
          
            CloseClient();
            return -1;
        }
    }
 
    std::cout << "HeadBucket success, the bucket region is:" << output.result().getRegion()
              << " the storage class is:" << output.result().getStringFormatStorageClass()
              << " the azRedundancy is:" << output.result().getStringFormatAzRedundancy() << std::endl;
    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For API documentation on retrieving bucket metadata, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
