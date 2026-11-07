---
title: "Deleting Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-object-c-sdk"
---

When an object is no longer in use, you may delete it to reduce cost overhead. Currently, the TOS C++ SDK supports deleting individual objects or multiple specified objects within a bucket. For buckets with versioning enabled, you can specify and delete any version of an object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* To delete an object, you must have the `tos:DeleteObject` permission. For specific instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete multi\-version objects, you must have the `tos:DeleteObjectVersion` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When versioning is enabled for a bucket, deleting an object without specifying its version ID will not permanently delete the object. Instead, a new version ID is generated and a DeleteMarker with a `null` version ID is inserted. Similarly, when versioning is `suspended`, deleting an object with a `null` version ID also creates a DeleteMarker with a `null` version ID. In a versioning\-enabled bucket, deleting a specific version ID permanently deletes that version of the object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### **Delete an object**

The following code is used to delete the `exampledir/exampleobject.txt` object from the specified bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    DeleteObjectInput input(bucketName,objectName);
    auto output = client.deleteObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "DeleteObject failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }

    std::cout << "DeleteObject success." << std::endl;
    std::cout << " version id is:" <<  output.result().getVersionId()
              << " request id is:" << output.result().getRequestInfo().getRequestId()
              << " is delete marker:" << output.result().isDeleteMarker() << std::endl;
    
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh"></span>
### **Delete an object version**

The following code is used to delete the specified version data of the `exampledir/exampleobject.txt` object in the specified multi\-version enabled bucket `examplebucket`.

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


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### **Batch delete objects**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When using the DeleteMultiObjects API to batch delete objects in a version\-controlled bucket, if <code>versionId</code> is not specified in the Delete request, a delete marker will be inserted. If <code>versionId</code> is specified, the designated version of the object will be permanently deleted.</div>


* <div data-tips="true" data-tips-type="warning">The response mode supported for batch object deletion can be configured using <code>quiet</code>:</div>


   * <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>false</code>, the response will include the deletion result regardless of whether the object was successfully deleted.</div>


   * <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>true</code>, only the results of objects that failed to be deleted are returned in the response; objects not returned are considered successfully deleted.</div>



**Batch delete objects**

The following code is used to delete multiple objects with specified object names from the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
 
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName1 = "exampledir/exampleobject1.txt";
    std::string objectName2 = "exampledir/exampleobject2.txt";
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    DeleteMultiObjectsInput input;
    input.setBucket(bucketName);
    ObjectTobeDeleted object1(objectName1);
    ObjectTobeDeleted object2(objectName2);
    input.addObjectTobeDeleted(object1);
    input.addObjectTobeDeleted(object2);

    auto output = client.deleteMultiObjects(input);
    if (!output.isSuccess()) {
       
        std::cout << "DeleteMultiObjects failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }

    std::cout << "DeleteMultiObjects success." << std::endl;
    for(auto& deleted : output.result().getDeleteds()){
        std::cout << " object key is:" << deleted.getKey()
                  << " object version id is:" <<  deleted.getVersionId()
                  << " is delete marker:" <<  deleted.isDeleteMarker()
                  << " delete marker version id is:" <<  deleted.getDeleteMarkerVersionId()<< std::endl;
    }
    for(auto& error : output.result().getErrors()){
        std::cout << " delete err object key is:" << error.getKey()
                  << " delete err object version id is:" <<  error.getVersionId()
                  << " delete err message:" <<  error.getMessage() << std::endl;
    }
  
    CloseClient();
    return 0;
}
```


**Batch delete object versions**

The following code is used to delete multiple object versions, specified by object name and version ID, from the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
  

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
    
    std::string objectName1 = "exampledir/exampleobject1.txt";
    std::string objectName2 = "exampledir/exampleobject2.txt";
    
    std::string versionId1 = "your object1 version";
    std::string versionId2 = "your object2 version";

    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);

    DeleteMultiObjectsInput input;
    input.setBucket(bucketName);
    ObjectTobeDeleted object1(objectName1,versionId1);
    ObjectTobeDeleted object2(objectName2,versionId2);
    input.addObjectTobeDeleted(object1);
    input.addObjectTobeDeleted(object2);
    
    auto output = client.deleteMultiObjects(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteMultiObjects failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }

    std::cout << "DeleteMultiObjects success." << std::endl;
    for(auto& deleted : output.result().getDeleteds()){
        std::cout << " object key is:" << deleted.getKey()
                  << " object version id is:" <<  deleted.getVersionId()
                  << " is delete marker:" <<  deleted.isDeleteMarker()
                  << " delete marker version id is:" <<  deleted.getDeleteMarkerVersionId()<< std::endl;
    }
    for(auto& error : output.result().getErrors()){
        std::cout << " delete err object key is:" << error.getKey()
                  << " delete err object version id is:" <<  error.getVersionId()
                  << " delete err message:" <<  error.getMessage() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5qG25Lit5omA5pyJ5a-56LGh"></span>
### **Delete all objects in the bucket**

The following code is used to delete all objects in the bucket.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
  
    std::string prefix = "yourkeyPrefix";
   
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

    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**


* For API documentation on deleting objects, refer to [DeleteObject](https://docs.byteplus.com/docs/tos/Delete-object-c-sdk).

* For API documentation on deleting multi\-version objects, see [DeleteMultiObject](https://docs.byteplus.com/docs/tos/reference-deletemultiobjects).
