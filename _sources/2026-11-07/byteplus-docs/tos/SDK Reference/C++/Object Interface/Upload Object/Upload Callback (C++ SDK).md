---
title: "Upload Callback (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-c-sdk"
---

An upload callback refers to a process in which the client includes a callback parameter in its request. Upon completion of the upload, the server sends a synchronous POST callback request to the third\-party application server specified in the Callback parameter. Only after the third\-party server confirms receipt and returns a result does the server return all results to the client.

For a detailed introduction to upload callbacks, see [Upload Callback](https://docs.byteplus.com/en/docs/tos/Upload-callback).

<span id="9b4cf5b9"></span>
## Sample Code

<span id="d5de9160"></span>
### Implementation of upload callback for standard upload

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
 
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
   
    std::string callback = "your callback param";
  
    std::string callbackVar = "your callback custom variable";


    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);
    
  
    std::string data("Object data to be uploaded");
    auto ss = std::make_shared<std::stringstream>(data);
    PutObjectV2Input input(bucketName, objectName, ss);
  
    input.setCallBack(callback);
    input.setCallBackVar(callbackVar);
    
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


<span id="04b3c44f"></span>
### Implementing upload callbacks for multipart uploads

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

static int64_t getFileSize(const std::string& file)
{
    std::fstream f(file, std::ios::in | std::ios::binary);
    f.seekg(0, f.end);
    int64_t size = f.tellg();
    f.close();
    return size;
}

int main(void){
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string callback = "your callback param";
    
    std::string callbackVar = "your callback custom variable";
    
  
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    CreateMultipartUploadInput input(bucketName, objectName);
    
    input.setAcl(ACLType::PublicRead);
    input.setStorageClass(StorageClassType::IA);
    input.setMeta({{"self-test", "yes"}});
    auto upload = client.createMultipartUpload(input);
    if (!upload.isSuccess()) {
        
        std::cout << "createMultipartUpload failed." << upload.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "createMultipartUpload success." << std::endl;

   
    std::string fileToUpload = "yourLocalFilename";
  
      int64_t partSize = 5 * 1024 * 1024;
    std::vector<UploadedPartV2> partResList;
    auto fileSize = getFileSize(fileToUpload);
    int partCount = static_cast<int>(fileSize / partSize);

    if (fileSize % partSize != 0) {
        partCount++;
    }

  
    auto uploadId = upload.result().getUploadId();
    for (int i = 1; i <= partCount; i++) {
        auto offset = partSize * (i - 1);
        auto size = (partSize < fileSize - offset) ? partSize : (fileSize - offset);
        std::shared_ptr<std::iostream> content = std::make_shared<std::fstream>(fileToUpload, std::ios::in|std::ios::binary);
        content->seekg(offset, std::ios::beg);

        UploadPartV2Input uploadPartInput(bucketName, objectName,uploadId, size,i,content);
        auto uploadPartOutput = client.uploadPart(uploadPartInput);
        if (!uploadPartOutput.isSuccess()) {
            std::cout << "uploadPart failed." << upload.error().String() << std::endl;
        
                CloseClient();
            return -1;
        }

        UploadedPartV2 part(i, uploadPartOutput.result().getETag());
        partResList.push_back(part);
    }

  
    CompleteMultipartUploadV2Input completeMultipartUploadInput(bucketName, objectName, uploadId, partResList);
    auto com = client.completeMultipartUpload(completeMultipartUploadInput);

    completeMultipartUploadInput.setCallBack(callback);
    completeMultipartUploadInput.setCallBackVar(callbackVar);
    
    if (!com.isSuccess()) {
     
        std::cout << "CompleteMultipartUpload failed." << upload.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "CompleteMultipartUpload success." << com.result().getRequestInfo().getRequestId() << std::endl;
   
    CloseClient();
    return 0;
}
```
