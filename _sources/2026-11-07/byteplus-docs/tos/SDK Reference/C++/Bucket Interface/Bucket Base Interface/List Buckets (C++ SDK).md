---
title: "List Buckets (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-c-sdk"
---

Obtain the list of storage buckets (Bucket) using ListBuckets. You can list all storage spaces under every region of the current account that meet the specified criteria.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before listing buckets, you must have the `tos:ListBuckets` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* This interface returns all buckets across all regions for the current account.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code enumerates all buckets across all regions for the current account.

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


    ListBucketsInput input;
    auto output = client.listBuckets(input);
    if (!output.isSuccess()) {
       
        std::cout << "ListBuckets failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
  
    std::cout << "ListBuckets Success, the bucket count is :" << output.result().getBuckets().size() << std::endl;
    std::cout << "Bucket Info is" << std::endl;
    for (auto& result : output.result().getBuckets()) {
        std::cout << "bucketName: " << result.getName() << " location: " << result.getLocation()
                  << " createDate: " << result.getCreationDate() << std::endl;
    }
  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on listing buckets, refer to [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
