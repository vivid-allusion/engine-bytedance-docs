---
title: "Standard Copy (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-c-sdk"
---

The copyObject operation enables copying objects between buckets within the same region, as well as copying objects within a single bucket. During copying, you can specify new metadata or retain the metadata of the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* File copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (by default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pmu6YCa5ou36LSd"></span>
### Standard Copy

When the object is smaller than 5 GiB, you can use standard copy. The following code copies the `srcdir/exampleobject.txt` object from the `srcbucket` bucket to the `destbucket` bucket and sets the object name to `destdir/exampleobject.txt`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
    
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";

    
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);

    CopyObjectV2Input input(bucketName, objectName, srcBucketName,srcObjectName);
    
    input.setAcl(ACLType::PublicRead);
    input.setStorageClass(StorageClassType::STANDARD);
    input.setMetadataDirective(MetadataDirectiveType::REPLACE);
     auto output = client.copyObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "CopyObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "CopyObject success. the object etag:" << output.result().getETag() << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".5ou36LSd5pe257un5om_5rqQ5a-56LGh5YWD5pWw5o2u"></span>
### **Inherit source object metadata during copy**

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
    
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";

    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);
    
    CopyObjectV2Input input(bucketName, objectName, srcBucketName,srcObjectName);
    auto output = client.copyObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "CopyObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "CopyObject success. the object etag:" << output.result().getETag() << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".5ou36LSd5pe26YeN5YaZ5a-56LGh5YWD5pWw5o2u"></span>
### **Overwrite object metadata during copy**

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
    
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";
    
  
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);

    CopyObjectV2Input input(bucketName, objectName, srcBucketName,srcObjectName);
    
    input.setMetadataDirective(MetadataDirectiveType::REPLACE);
    input.setMeta({{"self-test", "yes"}});
    auto output = client.copyObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "CopyObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "CopyObject success. the object etag:" << output.result().getETag() << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For the API documentation on standard copy operations, refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
