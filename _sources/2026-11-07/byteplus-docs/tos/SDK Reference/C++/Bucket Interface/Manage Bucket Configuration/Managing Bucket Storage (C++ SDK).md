---
title: "Managing Bucket Storage (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-storage-c-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container for storing Object data. TOS provides multiple bucket storage types suitable for a variety of application scenarios. This article describes how to configure the bucket storage type.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Storage Type Description

Bucket storage types include the following categories. For more information about storage types, please refer to [Storage Types](https://docs.byteplus.com/docs/tos/docs-storage-type).


|**Storage Type** |**Description** |**corresponding enumeration value** |
|---|---|---|
|Standard Storage |The default bucket storage type is characterized by high availability, high reliability, and high performance, making it suitable for data that is accessed frequently. |StorageClassType::STANDARD |
|Low\-Frequency Storage |Applicable to business scenarios with low access frequency (an average of 1 to 2 accesses per month), with a minimum storage period of 30 days. |StorageClassType::IA |
|Archival Flashback Storage |For business scenarios requiring long\-term retention with infrequent access, data must be stored for a minimum of 90 days. |StorageClassType::ARCHIVE_FR |
|Intelligent Tiered Storage |Suitable for data with uncertain access frequency, storage tiers can be switched based on access frequency to reduce storage costs. |StorageClassType::INTELLIGENT_TIERING |
|Cold Archive Storage |Classified as cold data, it is suitable for business scenarios that require long\-term data retention with infrequent access. A minimum storage period of 180 days is required. Data must be restored before accessing cold archive data. |StorageClassType::COLD_ARCHIVE |


<span id=".6K6-572u5a2Y5YKo57G75Z6L"></span>
## Configure Storage Type

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Configure the bucket storage type; by default, only the bucket owner has this permission.</div>


* <div data-tips="true" data-tips-type="warning">After the bucket storage type is set, if the object storage type is not specified during object upload, object copy, or multipart upload initialization. In this case, the object inherits the storage type of the bucket.</div>


* <div data-tips="true" data-tips-type="warning">When creating a bucket, if no storage type is specified, the default storage type is Standard Storage.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to set the storage class for the `examplebucket` bucket.

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
    

    PutBucketStorageClassInput input(bucketName, StorageClassType::IA);
    auto output = client.putBucketStorageClass(input);
    if (!output.isSuccess()) {
       
        std::cout << "PutBucketStorageClass failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketStorageClass success." << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5qG25a2Y5YKo57G75Z6L"></span>
## Retrieve Bucket Storage Type

The following code is used to obtain the storage class of the bucket `examplebucket`.

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
        
        std::cout << "GetBucketStorageClass failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
 
    std::cout << "GetBucketStorageClass success, the bucket storage class is:" << output.result().getStringFormatStorageClass() << std::endl;
    
 
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about storage types, see [Storage Types](https://docs.byteplus.com/docs/tos/docs-storage-type).
