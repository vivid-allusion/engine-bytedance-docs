---
title: "Listing Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-c-sdk"
---

This article describes how to use ListObject to enumerate all objects within a specified bucket, files with a designated prefix, and files and subdirectories within a specified directory.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The ListObjects interface has been revised to ListObjectsType2. It is strongly recommended that developers use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use List Objects V2, you must have the `tos:ListBucket` permission. For specific instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|marker |Starting position of the enumerated object. Configure the system to return a list of objects sorted alphabetically, starting after the specified value. This is typically the value of nextMarker returned by the previous request. |
|maxKeys |Returns the maximum number of objects to enumerate. The default value is 1000.<br><br>Value: greater than 0 and less than or equal to 1000. |
|encodingType |Encode the returned content and specify the type of encoding.<br><br>Default value: None |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code is used to list up to 10 objects in the bucket `examplebucket`.

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
    ListObjectsV2Input input(bucketName);
    input.setMaxKeys(10);
    auto output = client.listObjects(input);
    if (!output.isSuccess()) {

        std::cout << "ListObjects failed." << output.error().String() << std::endl;
 
        CloseClient();
        return -1;
    }
    std::cout << "ListObjects success." << std::endl;
    for (const auto& object : output.result().getContents()) {
        std::cout << "object"
                  << ",name:" << object.getKey() << ",size:" << object.getSize()
                  << ",lastmodify time:" << object.getStringFormatLastModified()
                  << ",storage class:" << object.getStringFormatStorageClass() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated Listing**

The following code is used to list up to 200 objects in the `examplebucket` bucket. By setting `maxKeys`, you can specify the maximum number of objects returned in a single request. By setting `marker` to the `nextMarker` returned from the first listing, you can continue listing objects.

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

    ListObjectsV2Input input(bucketName);
    input.setMaxKeys(100);
    auto output = client.listObjects(input);
    if (!output.isSuccess()) {
        
        std::cout << "ListObjects failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "ListObjects success." << std::endl;
    for (const auto& object : output.result().getContents()) {
        std::cout << "object"<<
                ",name:" << object.getKey() <<
                ",size:" << object.getSize() <<
                ",lastmodify time:" << object.getStringFormatLastModified() <<
                ",storage class:" << object.getStringFormatStorageClass() << std::endl;
    }
    if(output.result().isTruncated()){
        input.setMarker(output.result().getNextMarker());
        auto output1 = client.listObjects(input);
        if (!output1.isSuccess()) {
            
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }
        std::cout << "ListObjects success." << std::endl;
        for (const auto& object : output1.result().getContents()) {
            std::cout << "object"<<
                    ",name:" << object.getKey() <<
                    ",size:" << object.getSize() <<
                    ",lastmodify time:" << object.getStringFormatLastModified() <<
                    ",storage class:" << object.getStringFormatStorageClass() << std::endl;
        }
    }

  
    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code is used to list all objects with the specified prefix in the bucket `examplebucket`.

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

    ListObjectsV2Input input(bucketName);
    input.setPrefix(prefix);
    bool isTruncated = true;
    std::string nextMarker = "";
    while(isTruncated){
        input.setMarker(nextMarker);
        auto output = client.listObjects(input);
        if (!output.isSuccess()) {
         
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
           
            CloseClient();
            return -1;
        }
        nextMarker = output.result().getNextMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListObjects success." << std::endl;
        for (const auto& object : output.result().getContents()) {
            std::cout << "object"<<
                    ",name:" << object.getKey() <<
                    ",size:" << object.getSize() <<
                    ",lastmodify time:" << object.getStringFormatLastModified() <<
                    ",storage class:" << object.getStringFormatStorageClass() << std::endl;
        }
    }

    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### **Enumerate all objects**

The following code is used to list all objects in the `examplebucket` bucket.

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

    ListObjectsV2Input input(bucketName);
    input.setMaxKeys(100);
    bool isTruncated = true;
    std::string nextMarker = "";
    while(isTruncated){
        input.setMarker(nextMarker);
        auto output = client.listObjects(input);
        if (!output.isSuccess()) {
            
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }
        
        nextMarker = output.result().getNextMarker();
        isTruncated = output.result().isTruncated();
        
        std::cout << "ListObjects success." << std::endl;
        for (const auto& object : output.result().getContents()) {
            std::cout << "object"<<
                    ",name:" << object.getKey() <<
                    ",size:" << object.getSize() <<
                    ",lastmodify time:" << object.getStringFormatLastModified() <<
                    ",storage class:" << object.getStringFormatStorageClass() << std::endl;
        }
    }

   
    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **Enumerate the files and subdirectories within the specified directory.** 

TOS is based solely on the concept of objects; it is possible to create an object with a size of zero and a name containing a slash.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


1. First, set `delimiter` to`/`By simultaneously setting `prefix` to empty, the objects and subdirectory information in the root directory can be returned.

2. Set the `delimiter` again to`/`When `prefix` is simultaneously set as the subdirectory (`subfiledir`), objects and subdirectories within it can be returned.


The following code enumerates the objects and subdirectories in the root directory.

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

    ListObjectsV2Input input(bucketName);
    input.setDelimiter("/");
    input.setMaxKeys(10);
    auto output = client.listObjects(input);
    if (!output.isSuccess()) {
        
        std::cout << "ListObjects failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "ListObjects success." << std::endl;
    for (const auto& object : output.result().getContents()) {
        std::cout << "object"<<
                ",name:" << object.getKey() <<
                ",size:" << object.getSize() <<
                ",lastmodify time:" << object.getStringFormatLastModified() <<
                ",storage class:" << object.getStringFormatStorageClass() << std::endl;
    }
    for (const auto& prefix : output.result().getCommonPrefixes()) {
        std::cout << "Sub Dir:"<< prefix.getPrefix() << std::endl;
    }
    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on listing objects, see [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
