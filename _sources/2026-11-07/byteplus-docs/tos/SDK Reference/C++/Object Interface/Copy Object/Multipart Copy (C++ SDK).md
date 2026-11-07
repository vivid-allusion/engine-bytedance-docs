---
title: "Multipart Copy (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-c-sdk"
---

When an object exceeds 5 GiB in size, you can use the uploadPartCopy API to perform a multipart copy operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Object copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Steps

When an object exceeds 5 GiB in size, the uploadPartCopy operation must be used for multipart copying, which consists of three steps:


1. Initialize the multipart copy task using createMultipartUpload.

2. Perform the multipart copy using uploadPartCopy.

3. Merge the parts using completeMultipartUpload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code is used to copy the `srcdir/exampleobject.txt` object from the `srcbucket` bucket to the `destbucket` bucket, and set the object name to `destdir/exampleobject.txt`.

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
    CreateMultipartUploadInput input_part_create(bucketName, objectName);
    auto upload = client.createMultipartUpload(input_part_create);
    if (!upload.isSuccess()) {
        std::cout << "createMultipartUpload error: " << upload.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
   
    HeadObjectV2Input headInput(srcBucketName, srcObjectName);
    auto headOutput = client.headObject(headInput);
    if (!headOutput.isSuccess()) {
        std::cout << "head object error: " << headOutput.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    int64_t objectSize = headOutput.result().getContentLength();
    
    int partSize = 5 * 1024 * 1024;
    int partCount = (int)(objectSize / partSize);
    std::vector<UploadedPartV2> copyParts;
   
    if (objectSize % partSize != 0) {
        partCount++;
    }
    int64_t copySourceRangeEnd_ = 0;
 
    for (int i = 1; i <= partCount; i++) {
        auto offset = partSize * (i - 1);
        auto size = (partSize < objectSize - offset) ? partSize : (objectSize - offset);
        UploadPartCopyV2Input input(bucketName, objectName, srcBucketName, srcObjectName, i,upload.result().getUploadId());
        input.setCopySourceRangeStart(offset);
        input.setCopySourceRangeEnd(offset + size - 1);
        auto output = client.uploadPartCopy(input);
        if (!output.isSuccess()) {
            std::cout << "upload part " << i << "failed, error is: " << output.error().String() << std::endl;
        
            CloseClient();
            return -1;
        }
        UploadedPartV2 temp(output.result().getPartNumber(), output.result().getETag());
        copyParts.push_back(temp);
    }
    CompleteMultipartUploadV2Input input(bucketName, objectName, upload.result().getUploadId(), copyParts);
    auto complete = client.completeMultipartUpload(input);
    if (!complete.isSuccess()) {
        std::cout << "CompleteMultipartUpload error: " << complete.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
 
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**


* For API documentation on creating a multipart upload task, refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on copying parts, please refer to [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For documentation on the API for completing multipart uploads, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
