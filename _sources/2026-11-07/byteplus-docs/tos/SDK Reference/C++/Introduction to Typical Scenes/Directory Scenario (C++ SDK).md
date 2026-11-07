---
title: "Directory Scenario (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Catalog-scenes-c-sdk"
---

TOS is based solely on the concept of objects and stores data internally using a flat structure. To facilitate the grouping of objects and simplify management, you can organize objects using a directory hierarchy.

<span id=".5Yib5bu655uu5b2V"></span>
## **Create Directory**

TOS supports only the concept of objects, which can be created with a size of zero and a slash—[incomplete sentence].`/`The final object simulates the functionality of a directory.

The following code is used to create the directory `exampledir/` in the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
  
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
   
    std::string objectName = "exampledir/";

    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    auto ss = std::make_shared<std::stringstream>("");
    PutObjectV2Input input(bucketName, objectName, ss);
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "PutObject failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
     std::cout << "PutObject success. the object etag:" << output.result().getETag() << std::endl;
   
    CloseClient();
    return 0;
}
```


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## Simulated Directory Query

The `delimiter` and `prefix` parameters can be used to simulate directory query functionality:


1. First, set the `delimiter` to`/`By also setting `prefix` to an empty value, you can return information about objects and subdirectories under the root directory.

2. Reset the `delimiter` to`/`By simultaneously setting `prefix` to the subdirectory (`subfiledir`), objects and subdirectories within the subdirectory can be returned.


The following code is used to list the objects and subdirectories under the `exampledir/` directory of the `examplebucket` bucket.

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
    input.setDelimiter("/");
    bool isTruncated = true;
    std::string nextContinuationToken = "";
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

        std::cout << "ListObjects success." << std::endl;
        for (const auto& object : output.result().getContents()) {
            std::cout << "object"<<
                    ",name:" << object.getKey() <<
                    ",size:" << object.getSize() <<
                    ",lastmodify time:" << object.getStringFormatLastModified() <<
                    ",storage class:" << object.getStringFormatStorageClass() << std::endl;
        }
        for (const auto& prefix : output.result().getCommonPrefixes()) {
            std::cout << "subDir is:"<< prefix.getPrefix() << std::endl;
        }
    }

    
    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete Directory**

The following code is used to delete all data in the directory `exampledir/` of the bucket `examplebucket`.

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
