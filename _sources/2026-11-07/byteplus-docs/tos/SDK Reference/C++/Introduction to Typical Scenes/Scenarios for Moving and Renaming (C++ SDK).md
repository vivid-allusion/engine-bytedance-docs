---
title: "Scenarios for Moving and Renaming (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-c-sdk"
---

If you need to rename a file within a Bucket, you can use the CopyObject interface to copy the source object to the target object, and then use the DeleteObject interface to remove the source object.

<span id=".56e75YqoLemHjeWRveWQjeWNleS4quWvueixoQ=="></span>
## **Move or Rename a Single Object**

The following code is used to rename the object `srcdir/exampleobject.txt` in the bucket `srcbucket` to `destdir/exampleobject.txt` in the bucket `destbucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
  
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
   
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";
    
  
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    CopyObjectV2Input input(bucketName, objectName, srcBucketName,srcObjectName);
    auto output = client.copyObject(input);
    if (!output.isSuccess()) {
      
        std::cout << "CopyObject failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "CopyObject success. the object etag:" << output.result().getETag() << std::endl;
    
    
    DeleteObjectInput deleteInput(srcBucketName, srcObjectName);
    auto deleteOutput = client.deleteObject(deleteInput);
    if (!deleteOutput.isSuccess()) {
     
        std::cout << "DeleteObject failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }

    std::cout << "DeleteObject success." << std::endl;
    std::cout << " version id is:" <<  deleteOutput.result().getVersionId()
              << " is delete marker:" << deleteOutput.result().isDeleteMarker() << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".56e75YqoLemHjeWRveWQjeebruW9lQ=="></span>
## **Move/Rename Directory**

The following code is used to rename the directory `exampledir1/` in the bucket `srcbucket` to `exampledir2/` in the bucket `destbucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

std::string subReplace(std::string resourceStr, std::string subStr, std::string newStr) {
    std::string dstStr = resourceStr;
    std::string::size_type pos = 0;
    dstStr.replace(pos, subStr.length(), newStr);
    return dstStr;
}

int main(void){
  
 
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "destbucket";
    std::string srcBucketName = "srcbucket";
    std::string dir1 = "exampledir1/";
    std::string dir2 = "exampledir2/";
   
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

        for (const auto& object : output.result().getContents()) {
            auto newKey = object.getKey();
            if (newKey == dir1){
                newKey = dir2;
            } else {
                newKey = subReplace(newKey,dir1,dir2);
            }
            CopyObjectV2Input input(bucketName, newKey, srcBucketName,object.getKey());
            auto output = client.copyObject(input);
            if (!output.isSuccess()) {
             
                if(output.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "CopyObject failed." << output.error().String() << std::endl;
                 
                    CloseClient();
                    return -1;
                }
            }
            std::cout << "CopyObject success. the object etag:" << output.result().getETag() << std::endl;
            
            DeleteObjectInput deleteInput(srcBucketName,object.getKey());
            auto deleteOutput = client.deleteObject(deleteInput);
            if (!deleteOutput.isSuccess()) {
               
                if(deleteOutput.error().getStatusCode() != 404 && output.error().getCode() != "NoSuchKey"){
                    std::cout << "DeleteObject failed:" << deleteOutput.error().String() << std::endl;
                 
                    CloseClient();
                    return -1;
                }
            }

            std::cout << "DeleteObject success." << std::endl;
            std::cout << " version id is:" <<  deleteOutput.result().getVersionId()
                          << " is delete marker:" << deleteOutput.result().isDeleteMarker() << std::endl;

        }
    }

    
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**


* For documentation on the Copy Object API, refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).

* For documentation on the object deletion API, refer to [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
