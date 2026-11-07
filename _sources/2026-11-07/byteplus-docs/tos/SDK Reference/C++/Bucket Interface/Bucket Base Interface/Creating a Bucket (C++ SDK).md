---
title: "Creating a Bucket (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-c-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container used to store Object data. Users are provided with the capability to create a new bucket using a specified bucket name. The newly created bucket name must be unique within TOS. This document describes how to create a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The [bucket naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts) are as follows:

   * Only lowercase letters a–z, digits, and hyphens (\-) are permitted.

   * The beginning and end can only be digits or letters.

   * The length must be between 3 and 63 characters.

* When accessing TOS from other BytePlus products within the same region, it is recommended to use the internal network Endpoint. For more information about regions and Endpoints, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the appropriate permissions through IAM policies. For detailed steps, see [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to create a bucket named examplebucket.

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
    
    CreateBucketV2Input input(bucketName);
    
    
    // input.setAcl(ACLType::PublicRead);

    // input.setAzRedundancy(AzRedundancyType::MultiAz);

    // input.setStorageClass(StorageClassType::STANDARD);
    

    auto output = client.createBucket(input);
    if (!output.isSuccess()) {
 
        std::cout << "CreateBucket failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }

    std::cout << "CreateBucket Success, the bucket location:" << output.result().getLocation() << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For API documentation on creating a bucket, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
