---
title: "Deleting a Bucket (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/delete-bucket-c-sdk"
---

When you no longer need to retain a bucket (Bucket), you may delete it to avoid incurring additional charges.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Once a bucket is deleted, it cannot be restored. Please proceed with caution.

* Before deleting a bucket, you must have the `tos:DeleteBucket` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been removed.


* If versioning is enabled for the bucket, please ensure that all current and historical version objects within the bucket have been deleted. For detailed instructions, see [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged shards in the bucket, ensure that all shard data is deleted. For specific operations, refer to [Delete Shard](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If your bucket contains a large number of objects, you can configure lifecycle rules to enable batch deletion of objects. For detailed instructions, please refer to [Setting Lifecycle Rules](https://docs.byteplus.com/docs/6349/75028).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to delete the bucket `examplebucket`.

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
    
 
    DeleteBucketInput input(bucketName);
    auto output = client.deleteBucket(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteBucket failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucket success." << std::endl;
    
    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For API documentation on deleting buckets, refer to [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
