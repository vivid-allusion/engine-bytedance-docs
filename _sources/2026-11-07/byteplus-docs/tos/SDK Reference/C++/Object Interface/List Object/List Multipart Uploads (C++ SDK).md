---
title: "List Multipart Uploads (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-shard-upload-tasks-c-sdk"
---

This article presents key considerations and sample code for listing multipart uploads.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* To list multipart uploads, you must have the `tos:ListBucketMultipartUploads` permission for the bucket. For detailed instructions, refer to the [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* This list pertains to ongoing multipart upload tasks with unmerged parts. If a multipart upload task has already had its parts merged, that task will no longer be listed.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|**Parameter** |**Description** |
|---|---|
|delimiter |A character used to group object names. |
|encodingType |Encode the returned content and specify the type of encoding.<br><br>Default value: None |
|maxUploads |Returns the maximum number of multipart upload tasks. The default value is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |
|prefix |Used to specify the prefix for objects returned by listing. |
|keyMarker |List the starting positions of multipart upload tasks. Return a list of objects sorted alphabetically, starting after the specified value. This is typically the nextMarker value returned by the previous request. |
|uploadIdMarker |Used in conjunction with keyMarker, this parameter specifies that the multipart upload task list will be returned in dictionary order starting from the value following keyMarker. Obtain nextVersionIdMarker from the results of the previous listing. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### **Briefly list incomplete multipart uploads**

The following code is used to list 10 incomplete multipart uploads in the specified bucket.

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

 
    ListMultipartUploadsV2Input input(bucketName);

    input.setMaxUploads(10);
    auto output = client.listMultipartUploads(input);
    if (!output.isSuccess()) {
    
        std::cout << "ListMultipartUploads failed." << output.error().String() << std::endl;
  
        CloseClient();
        return -1;
    }
    std::cout << "ListMultipartUploads success." << std::endl;
    for (const auto& part : output.result().getUploads()) {
        std::cout << "part"<<
                ",key:" << part.getKey() <<
                ",uploadId:" << part.getUploadId() <<
                ",storageClasss:" << part.getStringFormatStorageClass() <<
                ",initiated time:" << part.getStringFormatInitiated() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### **List all incomplete multipart uploads with the specified prefix**

The following code is used to list all incomplete multipart uploads under the specified prefix in the designated bucket.

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
 
    ListMultipartUploadsV2Input input(bucketName);

    input.setPrefix(prefix);
   
    input.setMaxUploads(100);
    
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        auto output = client.listMultipartUploads(input);
        if (!output.isSuccess()) {
            
            std::cout << "ListMultipartUploads failed." << output.error().String() << std::endl;
            
            CloseClient();
            return -1;
        }
        
        nextKeyMarker = output.result().getNextKeyMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListMultipartUploads success." << std::endl;
        for (const auto& part : output.result().getUploads()) {
        std::cout << "part"<<
                ",key:" << part.getKey() <<
                ",uploadId:" << part.getUploadId() <<
                ",storageClasss:" << part.getStringFormatStorageClass() <<
                ",initiated time:" << part.getStringFormatInitiated() << std::endl;
        }
    }

 
    CloseClient();
    return 0;
}
```


<span id=".5YiX5Li-5omA5pyJ5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### **List all multipart uploads**

The following code is used to list all incomplete multipart uploads in the specified bucket.

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
 
    ListMultipartUploadsV2Input input(bucketName);

    input.setMaxUploads(100);
    
    bool isTruncated = true;
    std::string nextKeyMarker = "";
    while(isTruncated){
        input.setKeyMarker(nextKeyMarker);
        auto output = client.listMultipartUploads(input);
        if (!output.isSuccess()) {
           
            std::cout << "ListMultipartUploads failed." << output.error().String() << std::endl;
           
            CloseClient();
            return -1;
        }

        nextKeyMarker = output.result().getNextKeyMarker();
        isTruncated = output.result().isTruncated();

        std::cout << "ListMultipartUploads success." << std::endl;
        for (const auto& part : output.result().getUploads()) {
            std::cout << "part"<<
                    ",key:" << part.getKey() <<
                    ",uploadId:" << part.getUploadId() <<
                    ",storageClasss:" << part.getStringFormatStorageClass() <<
                    ",initiated time:" << part.getStringFormatInitiated() << std::endl;
        }
    }


    CloseClient();
    return 0;
}
```


<span id=".5oyJ55uu5b2V6YCS5b2S5YiX5Li-5pyq5ZCI5bm25YiG54mH5Lu75Yqh"></span>
### **Recursively list incomplete multipart uploads**

TOS only uses the object model. To simulate directory functionality, create a zero\-byte object that ends with a forward slash (`/`).

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


1. First, set the `delimiter` to `/`. When `prefix` is also set to empty, objects and subdirectory information under the root directory can be returned.

2. Set `delimiter` again to`/`. By simultaneously setting `prefix` as a subdirectory (`subfiledir`), objects and subdirectories of the subdirectory can be returned.


The following code recursively lists incomplete multipart uploads in the bucket 'examplebucket'.

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

  
    ListMultipartUploadsV2Input input(bucketName);

    input.setDelimiter("/");
  
    input.setMaxUploads(100);
    auto output = client.listMultipartUploads(input);
    if (!output.isSuccess()) {
     
        std::cout << "ListMultipartUploads failed." << output.error().String() << std::endl;
 
        CloseClient();
        return -1;
    }

    std::cout << "ListMultipartUploads success." << std::endl;
    for (const auto& part : output.result().getUploads()) {
        std::cout << "part"<<
                ",key:" << part.getKey() <<
                ",uploadId:" << part.getUploadId() <<
                ",storageClasss:" << part.getStringFormatStorageClass() <<
                ",initiated time:" << part.getStringFormatInitiated() << std::endl;
    }
    for (const auto& prefix : output.result().getCommonPrefixes()) {
        std::cout << "Sub Dir:"<< prefix.getPrefix() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**

For API documentation on listing multipart uploads, see [ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads).
