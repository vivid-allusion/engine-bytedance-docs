---
title: "List Objects V2 (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-c-sdk"
---

This article explains how to use listObjectsType2 to enumerate all objects within a specified bucket, files with a designated prefix, as well as files and subdirectories within a specified directory.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The ListObjects interface has been updated to ListObjectsType2. Developers are strongly encouraged to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use List Objects V2, you must have the `tos:ListBucket` permission. For detailed instructions, see the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description

The supported parameters for listObjectsType2 are as follows.


|**Parameters** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |The character used to group object names. commonly used`/`Used as a grouping character. |
|startAfter |The starting point for the objects enumerated in this instance. |
|continuationToken |The specified enumeration operation must begin from this token. It can be obtained from the nextContinuationToken in the previous listing results. |
|maxKeys |The maximum number of objects to be returned. The maximum value is 1,000, meaning that a single request can return up to 1,000 objects. |
|encodingType |Specifies the encoding type to be applied to the returned content. The possible values are explained as follows:<br><br>URL: Perform URL encoding. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code is used to list up to 100 objects in the bucket `examplebucket`.

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
    input.setMaxKeys(100);
    auto output = client.listObjectsType2(input);
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
                ",storage class:" << object.getStringFormatStorageClass() << std:: endl;
    }
   
    CloseClient();
    return 0;
}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated Listing**

The following code is used to list objects in the `examplebucket` bucket with pagination. By setting `maxKeys`, you can specify the maximum number of objects returned in a single request. In the sample code, 100 objects are listed from the bucket `examplebucket`. To continue listing objects, set `continuationToken` to the `nextContinuationToken` returned from the initial listing.

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
    input.setMaxKeys(100);
    auto output = client.listObjectsType2(input);
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

    
    if (output.result().isTruncated()){
        input.setContinuationToken(output.result().getNextContinuationToken());
        auto output1 = client.listObjectsType2(input);
        if (!output1.isSuccess()) {
            
            std::cout << "ListObjects failed." << output1.error().String() << std::endl;
            
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
    
    ListObjectsType2Input input(bucketName);
    input.setPrefix(prefix);
    bool isTruncated = true;
    std::string nextContinuationToken = "";
    while(isTruncated){
        input.setContinuationToken(nextContinuationToken);
        auto output = client.listObjectsType2(input);
        if (!output.isSuccess()) {
            
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
         
            CloseClient();
            return -1;
        }
        nextContinuationToken = output.result().getNextContinuationToken();
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

The following code is used to list all objects in the bucket `examplebucket`.

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
    bool isTruncated = true;
    std::string nextContinuationToken = "";
    while(isTruncated){
        input.setContinuationToken(nextContinuationToken);
        auto output = client.listObjectsType2(input);
        if (!output.isSuccess()) {
           
            std::cout << "ListObjects failed." << output.error().String() << std::endl;
          
            CloseClient();
            return -1;
        }

        nextContinuationToken = output.result().getNextContinuationToken();
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
### **List the files and subdirectories in the specified directory.** 

TOS supports only the concept of objects and allows the creation of an object with a size of zero and a slash in its name...`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


1. First, set the `delimiter` to`/`When `prefix` is set to empty, objects and subdirectory information in the root directory can be returned.

2. Set the `delimiter` again to`/`Simultaneously, when `prefix` is set to a subdirectory (`subfiledir`), objects within the subdirectory and its subdirectories can be returned.


The following code is used to enumerate objects and subdirectories in the root directory.

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
    input.setDelimiter("/");
    input.setMaxKeys(1000);
    auto output = client.listObjectsType2(input);
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
                ",storage class:" << object.getStringFormatStorageClass() << std:: endl;
    }
    for (const auto& prefix : output.result().getCommonPrefixes()) {
        std::cout << "Sub Dir: "<< prefix.getPrefix() << std:: endl;
    }
    
    
    CloseClient();
    return 0;
}
```
