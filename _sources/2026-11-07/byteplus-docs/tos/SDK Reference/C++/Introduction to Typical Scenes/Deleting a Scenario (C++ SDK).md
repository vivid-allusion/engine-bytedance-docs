---
title: "Deleting a Scenario (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-scenes-c-sdk"
---

This document introduces code examples for common object deletion scenarios.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* To delete an object, your account must have the `tos:DeleteObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete multi\-version objects, your account must have the `tos:DeleteObjectVersion` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Please exercise caution when performing delete operations, as files cannot be restored once deleted.


<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete Directory**

The following code is used to delete all data in the directory `exampledir/` within the bucket `examplebucket`.

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

    ListObjectsType2Input input(bucketName);
    std::string prefix = "exampledir/";
    bool isTruncated = true;
    std::string nextContinuationToken = "";

    DeleteObjectInput deleteInput;
    deleteInput.setBucket(bucketName);
    while(isTruncated){
        input.setContinuationToken(nextContinuationToken);
        input.setPrefix(prefix);
        auto output = client.listObjectsType2(input);
        if (!output.isSuccess()) {
            
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }

        nextContinuationToken = output.result().getNextContinuationToken();
        isTruncated = output.result().isTruncated();
        
        for (const auto& object : output.result().getContents()) {
            deleteInput.setKey(object.getKey());
            auto deleteOutput = client.deleteObject(deleteInput);
            if (!deleteOutput.isSuccess()) {
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "DeleteObject failed:" << deleteOutput.error().String() << std::endl;
                 
                    CloseClient();
                    return -1;
                }
            }
        }
    }

    
    CloseClient();
    return 0;
}
```


<span id=".5riF56m65qG2"></span>
## **Empty Bucket**

The following code is used to clear the entire bucket, including deleting all objects and all unmerged objects.

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

    DeleteObjectInput deleteObjectInput;
    deleteObjectInput.setBucket(bucketName);
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        auto output = client.listObjectVersions(input);
        if (!output.isSuccess()) {
          
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
          
            CloseClient();
            return -1;
        }
        nextKeyMarker = output.result().getNextKeyMarker();
        isTruncated = output.result().isTruncated();


        for (const auto& versions : output.result().getVersions()) {
            deleteObjectInput.setKey(versions.getKey());
            auto deleteOutput = client.deleteObject(deleteObjectInput);
            if (!deleteOutput.isSuccess()){
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "DeleteObject failed:" << deleteOutput.error().String() << std::endl;
                  
                    CloseClient();
                    return -1;
                }
            }

        }
        for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
            deleteObjectInput.setKey(deleteMarker.getKey());
            auto deleteOutput = client.deleteObject(deleteObjectInput);
            if (!deleteOutput.isSuccess()){
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
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


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## **Clearing a bucket with versioning enabled**

The following code provides an example for clearing an entire bucket with versioning enabled. It includes deleting all versions of objects, removing all versions of delete markers, and deleting all unmerged objects.

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
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
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
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
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
