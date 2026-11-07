---
title: "List Multi-Version Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multiversion-objects-c-sdk"
---

You can use listObjectVersions to list information about multiple object versions within a bucket, with a maximum of 1,000 objects returned per request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before listing multi\-version objects, you must have the `tos:ListBucketVersions` permission on the bucket. For detailed instructions, please refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* Each request returns a subset of multi\-version objects from the bucket, with a maximum of 1,000 objects per request. Request parameters can be used as selection criteria to return a specific subset of objects within the bucket.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|maxKeys |Returns the maximum number of enumerated objects. The default value is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |
|encodingType |Encode the returned content and specify the encoding type.<br><br>Default value: url |
|keyMarker |List the starting positions of multi\-version objects. Return a list of objects sorted alphabetically, starting after the specified value. This is typically the value of nextMarker returned by the previous request. |
|versionIdMarker |Used in conjunction with keyMarker, this sets the starting point after which a lexicographically sorted list of multi\-version objects is returned. Obtain nextVersionIdMarker from the results of the previous listing operation. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code is used to list up to 10 versioned objects in the bucket `examplebucket`.

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
    input.setMaxKeys(10);
    auto output = client.listObjectVersions(input);
    if (!output.isSuccess()) {
      
        std::cout << "ListObjectVersions failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }

    std::cout << "ListObjectVersions success." << std::endl;
    for (const auto& versions : output.result().getVersions()) {
        std::cout << "versions"<<
                ",name:" << versions.getKey() <<
                ",size:" << versions.getSize() <<
                ",etag:" << versions.getETag() <<
                ",is latest:" << versions.isLatest() <<
                ",version id:" << versions.getVersionId() <<
                ",hashCrc64:" << versions.getHashCrc64Ecma() <<
                ",lastmodify time:" << versions.getStringFormatLastModified() <<
                ",storage class:" << versions.getStringFormatStorageClass() << std:: endl;
    }
    for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
        std::cout << "deleteMarkers"<<
                ",name:" << deleteMarker.getKey() <<
                ",is latest:" << deleteMarker.isLatest() <<
                ",version id:" << deleteMarker.getVersionId() <<
                ",lastmodify time:" << deleteMarker.getStringFormatLastModified() << std:: endl;
    }
 
    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code is used to list all versioned objects and delete markers under the bucket `examplebucket` with the prefix `yourkeyPrefix`.

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
    input.setMaxKeys(1000);
    input.setPrefix(prefix);
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    std::string nextVersionIdMarker = "";
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        auto output = client.listObjectVersions(input);
        if (!output.isSuccess()) {
           
            std::cout << "ListObjectVersions failed." << output.error().String() << std::endl;
           
            CloseClient();
            return -1;
        }
        nextKeyMarker = output.result().getKeyMarker();
        isTruncated = output.result().isTruncated();
        
        std::cout << "ListObjectVersions success." << std::endl;
        for (const auto& versions : output.result().getVersions()) {
            std::cout << "versions"<<
                    ",name:" << versions.getKey() <<
                    ",size:" << versions.getSize() <<
                    ",etag:" << versions.getETag() <<
                    ",is latest:" << versions.isLatest() <<
                    ",version id:" << versions.getVersionId() <<
                    ",hashCrc64:" << versions.getHashCrc64Ecma() <<
                    ",lastmodify time:" << versions.getStringFormatLastModified() <<
                    ",storage class:" << versions.getStringFormatStorageClass() << std:: endl;
        }
        for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
            std::cout << "deleteMarkers"<<
                    ",name:" << deleteMarker.getKey() <<
                    ",is latest:" << deleteMarker.isLatest() <<
                    ",version id:" << deleteMarker.getVersionId() <<
                    ",lastmodify time:" << deleteMarker.getStringFormatLastModified() << std:: endl;
        }
    }

 
    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5omA5pyJ5a-56LGh"></span>
### **Enumeration means listing all objects.** 

The following code is used to list all versioned objects and delete markers in the bucket `examplebucket`.

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
    input.setMaxKeys(1000);
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    std::string nextVersionIdMarker = "";
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        input.setVersionIdMarker(nextVersionIdMarker);
        auto output = client.listObjectVersions(input);
        if (!output.isSuccess()) {
         
            std::cout << "ListObjectVersions failed." << output.error().String() << std::endl;
           
            CloseClient();
            return -1;
        }

        nextKeyMarker = output.result().getNextKeyMarker();
        nextVersionIdMarker = output.result().getNextVersionIdMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListObjectVersions success." << std::endl;
        for (const auto& versions : output.result().getVersions()) {
            std::cout << "versions"<<
                    ",name:" << versions.getKey() <<
                    ",size:" << versions.getSize() <<
                    ",etag:" << versions.getETag() <<
                    ",is latest:" << versions.isLatest() <<
                    ",version id:" << versions.getVersionId() <<
                    ",hashCrc64:" << versions.getHashCrc64Ecma() <<
                    ",lastmodify time:" << versions.getStringFormatLastModified() <<
                    ",storage class:" << versions.getStringFormatStorageClass() << std:: endl;
        }
        for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
            std::cout << "deleteMarkers"<<
                    ",name:" << deleteMarker.getKey() <<
                    ",is latest:" << deleteMarker.isLatest() <<
                    ",version id:" << deleteMarker.getVersionId() <<
                    ",lastmodify time:" << deleteMarker.getStringFormatLastModified() << std:: endl;
        }
    }


    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List files and subdirectories in the specified directory**

TOS recognizes only the concept of objects; it is possible to create an object with a size of zero whose name contains a slash.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


1. First, set `delimiter` to`/`When `prefix` is also set to empty, you can return the objects and subdirectory information under the root directory.

2. Set the `delimiter` again to`/`When the `prefix` is set to a subdirectory (`subfiledir`), objects and subdirectories under that subdirectory can be returned.


The following code is used to recursively enumerate objects and subdirectories within a directory. For objects, information for all versions is returned. For directories, only the latest version information is provided.

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
    input.setDelimiter("/");
    input.setMaxKeys(100);
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    std::string nextVersionIdMarker = "";
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        input.setVersionIdMarker(nextVersionIdMarker);
        auto output = client.listObjectVersions(input);
        if (!output.isSuccess()) {
         
            std::cout << "ListObjectVersions failed." << output.error().String() << std::endl;
         
            CloseClient();
            return -1;
        }

        nextKeyMarker = output.result().getNextKeyMarker();
        nextVersionIdMarker = output.result().getNextVersionIdMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListObjectVersions success." << std::endl;
        for (const auto& versions : output.result().getVersions()) {
            std::cout << "versions"<<
                    ",name:" << versions.getKey() <<
                    ",size:" << versions.getSize() <<
                    ",etag:" << versions.getETag() <<
                    ",is latest:" << versions.isLatest() <<
                    ",version id:" << versions.getVersionId() <<
                    ",hashCrc64:" << versions.getHashCrc64Ecma() <<
                    ",lastmodify time:" << versions.getStringFormatLastModified() <<
                    ",storage class:" << versions.getStringFormatStorageClass() << std::endl;
        }
        for (const auto& deleteMarker : output.result().getDeleteMarkers()) {
            std::cout << "deleteMarkers"<<
                    ",name:" << deleteMarker.getKey() <<
                    ",is latest:" << deleteMarker.isLatest() <<
                    ",version id:" << deleteMarker.getVersionId() <<
                    ",lastmodify time:" << deleteMarker.getStringFormatLastModified() << std::endl;
        }
        for (const auto& prefix : output.result().getCommonPrefixes()) {
            std::cout << "Common Prefixes"<< prefix.getPrefix() << std::endl;
        }
    }

   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on listing multi\-version objects, refer to [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
