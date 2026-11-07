---
title: "Multi-Version Scenarios (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenes-c-sdk"
---

Version control is applied to all objects in the bucket. By enabling bucket versioning, you can restore an object to any previous version after accidental deletion or overwriting.

Currently, multi\-version support is available for the following interfaces: GetObject, GetObjectACL, CopyObject, UploadPartCopy, DeleteObject, and others. When invoking the relevant interfaces, you can specify the exact version of the target object by using the optional parameter versionID.

In TOS, bucket versioning status includes three states: not enabled, versioning enabled, and versioning suspended. This article introduces multi\-version management for buckets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* To manage the versioning status of a bucket, you must have `tos:PutBucketVersioning` permission.

* To query the multi\-version status of a bucket, you must have the `tos:GetBucketVersioning` permission.


<span id=".6K6-572u5qG254mI5pys5o6n5Yi254q25oCB"></span>
## **Configure Bucket Versioning Status**

The following code is used to set the bucket status to the multi\-versioning enabled (Enable) state.

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
    PutBucketVersioningInput input(bucketName,VersioningStatusType::Enabled);

    auto output = client.putBucketVersioning(input);
    if (!output.isSuccess()) {
        
        std::cout << "OpenBucketVersioning failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "OpenBucketVersioning success." << std::endl;

  
    CloseClient();
    return 0;
}
```


The following code is used to set the bucket status to the suspended versioning state (Suspended).

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
    PutBucketVersioningInput input(bucketName,VersioningStatusType::Suspended);

    auto output = client.putBucketVersioning(input);
    if (!output.isSuccess()) {
      
        std::cout << "SuspendBucketVersioning failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "SuspendBucketVersioning success." << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5qG255qE54mI5pys5o6n5Yi254q25oCB"></span>
## **Retrieve the bucket versioning status**

The following code is used to obtain the versioning status information of the bucket `examplebucket`.

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
    GetBucketVersioningInput input(bucketName);

    auto output = client.getBucketVersioning(input);
    if (!output.isSuccess()) {
    
        std::cout << "GetBucketVersioning failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketVersioning success." << std::endl;
    std::cout << "versioning statue" << output.result().getStringFormatVersioningStatus() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
## **Download Multi\-Version Objects**

The following code is used to download a specified version of the object `exampledir/exampleobject.txt` from the bucket `examplebucket` into memory.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string versionId = "your object version";
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    GetObjectV2Input input(bucketName, objectName);
    input.setVersionId(versionId);
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


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
## **Deleting Multi\-Version Objects**

The following code is used to delete a specified version of the `exampledir/exampleobject.txt` object in the specified bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
  
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string versionId = "your object version";

    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    DeleteObjectInput input(bucketName,objectName);
    input.setVersionID(versionId);
    auto output = client.deleteObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "DeleteObject failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }

    std::cout << "DeleteObject success." << std::endl;
    std::cout << " version id is:" <<  output.result().getVersionId()
              << " is delete marker:" << output.result().isDeleteMarker() << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## **Emptying a versioning\-enabled bucket**

The following code provides an example for emptying an entire bucket with versioning enabled. It includes deleting all versions of every object, removing all versions of delete markers, and deleting all unmerged objects.

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

    ListObjectVersionsV2Input input(bucketName);
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    std::string nextVersionIdMarker = "";
    DeleteObjectInput deleteObjectInput;
    deleteObjectInput.setBucket(bucketName);
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        input.setVersionIdMarker(nextVersionIdMarker);
        auto output = client.listObjectVersions(input);
        if (!output.isSuccess()) {
           
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }
 
        nextKeyMarker = output.result().getNextKeyMarker();
        nextVersionIdMarker = output.result().getNextVersionIdMarker();
        isTruncated = output.result().isTruncated();

        for (const auto& versions : output.result().getVersions()) {
            deleteObjectInput.setKey(versions.getKey());
            deleteObjectInput.setVersionID(versions.getVersionId());
            auto deleteOutput = client.deleteObject(deleteObjectInput);
            if (!deleteOutput.isSuccess()){
                if(output.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "DeleteObject failed:" << deleteOutput.error().String() << std::endl;
                  
                    CloseClient();
                    return -1;
                }
            }
        }
        for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
            deleteObjectInput.setKey(deleteMarker.getKey());
            deleteObjectInput.setVersionID(deleteMarker.getVersionId());
            auto deleteOutput = client.deleteObject(deleteObjectInput);
            if (!deleteOutput.isSuccess()){
                if(output.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "DeleteObject failed:" << deleteOutput.error().String() << std::endl;
                
                    CloseClient();
                    return -1;
                }
            }
        }
    }

   
    ListMultipartUploadsV2Input input2(bucketName);
    AbortMultipartUploadInput abortMultipartUploadInput;
    abortMultipartUploadInput.setBucket(bucketName);
    
    isTruncated = true;
    nextKeyMarker = "";
    while(isTruncated){
        input2.setKeyMarker(nextKeyMarker);
        auto output = client.listMultipartUploads(input2);
        if (!output.isSuccess()) {
            
            std::cout << "ListMultipartUploads failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }
        nextKeyMarker = output.result().getNextKeyMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListMultipartUploads success." << std::endl;
        for (const auto& part : output.result().getUploads()) {
            abortMultipartUploadInput.setKey(part.getKey());
            abortMultipartUploadInput.setUploadId(part.getUploadId());
            auto abortOutput = client.abortMultipartUpload(abortMultipartUploadInput);
            if (!abortOutput.isSuccess()){
                std::cout << "DeletePart failed:" << abortOutput.error().String() << std::endl;
              
                CloseClient();
                return -1;
            }
        }
    }
    
    CloseClient();
    return 0;
}
```
