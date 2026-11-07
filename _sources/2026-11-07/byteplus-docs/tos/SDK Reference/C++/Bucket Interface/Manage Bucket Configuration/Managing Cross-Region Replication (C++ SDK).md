---
title: "Managing Cross-Region Replication (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-region-replication-c-sdk"
---

TOS supports cross\-region replication (CRR), which enables you to copy objects from one bucket to another in different regions. After CRR rules are enabled, when you upload a new object to the source bucket, TOS will automatically synchronize the object to the destination bucket. This feature is designed to meet the requirements for remote disaster recovery and data replication.

<span id=".6K6-572u6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Configure CRR rules

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Precautions**


* Objects that existed before CRR rules are enabled will not be synchronized.

* CRR utilizes an asynchronous replication mechanism. Depending on the size of your objects, the required time may range from several minutes to several hours.

* A storage bucket can create up to 100 CRR rules.

* CRR can only be enabled when the versioning status of the source bucket and the destination bucket is the same.

* To configure CRR rules for a bucket, you must, by default, be the bucket owner.

* During CRR task execution, when both StorageClass and StorageClassInheritDirective are configured, the configuration of StorageClass shall take precedence.

* When only StorageClassInheritDirective is configured, if its value is SOURCE_OBJECT, the configuration is consistent with the source object; if its value is DESTINATION_BUCKET, the configuration is consistent with the destination bucket.

* If neither StorageClass nor StorageClassInheritDirective is configured, the default policy is applied, which aligns the storage type with that of the target bucket.


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to configure CRR rules for the bucket examplebucket.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
  
    std::string destBucketName = "yourdestbucket";
 
    std::string destRegion = "Your DestBucket Region";


    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

    PutBucketReplicationInput input(bucketName);
    ReplicationRule rule;
 
    rule.setId("1");

    rule.setStatus(StatusType::StatusEnabled);
   
    rule.setPrefixSet({"prefix1","prefix2"});
  
    Destination destination(destBucketName,destRegion);
   
        destination.setStorageClass(StorageClassType::IA);
        destination.setStorageClassInheritDirective(StorageClassInheritDirectiveType::DestinationBucket);

    rule.setDestination(destination);
    
    // rule.setHistoricalObjectReplication(StatusType::StatusEnabled);

    input.setRules({rule});
    input.setRole("ServiceRoleforReplicationAccessTOS");
    auto output = client.putBucketReplication(input);
    if (!output.isSuccess()) {
     
        std::cout << "PutBucketReplication failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "PutBucketReplication success." << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Obtain CRR rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the bucket owner to retrieve CRR rules.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the CRR rules for the bucket examplebucket.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";
 
    std::string ruleId = "yourCrrRuleId";

 
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
    GetBucketReplicationInput input(bucketName);
   
    // input.setRuleId(ruleId);
    auto output = client.getBucketReplication(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketReplication failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketReplication success." << std::endl;
    std::cout << "Role:" << output.result().getRole() << std::endl;
    std::cout << "Get Bucket Crr Rule List:" << std::endl;
    for (const auto& rule : output.result().getRules()) {
        std::cout << "id:" << rule.getId() << std::endl;
        std::cout << "status:" << rule.getStringFormatStatus() << std::endl;
        std::cout << "historical object replication:" << rule.getStringFormatHistoricalObjectReplication() << std::endl;
        if (rule.getProgress() != nullptr) {
          
            std::cout << "new object speed of progress:" << rule.getProgress()->getHistoricalObject() << std::endl;
           
            std::cout << "historical object speed of progress:" << rule.getProgress()->getHistoricalObject()
                      << std::endl;
        }
        for (auto const& prefix : rule.getPrefixSet()) {
            std::cout << "prefix is:" << prefix << std::endl;
        }
        auto destination = rule.getDestination();
        std::cout << "dest bucket is:" << destination.getBucket() << std::endl;
        std::cout << "storage class is:" << destination.getStringFormatStorageClass() << std::endl;
        std::cout << "storage class inherit directive is:" << destination.getStringFormatStorageClassInheritDirective()
                  << std::endl;
        std::cout << "dest location is:" << destination.getLocation() << std::endl;
    }

 
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Delete CRR rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete a bucket's CRR rule, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the CRR rule for the bucket examplebucket.

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
    DeleteBucketReplicationInput input(bucketName);
    auto output = client.deleteBucketReplication(input);
    if (!output.isSuccess()) {
        
        std::cout << "DeleteBucketReplication failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "DeleteBucketReplication success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents

For more information on configuring CRR rules, see [Cross-region replication rules](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account).
