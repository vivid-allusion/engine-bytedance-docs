---
title: "Managing Object Metadata (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-c-sdk"
---

Object metadata refers to the attribute description of an object, comprising both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id=".6K6-572u6Ieq5a6a5LmJ5YWD5pWw5o2u"></span>
## Set Custom Metadata

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">By default, only the object owner has permission to set object metadata.</div>


* <div data-tips="true" data-tips-type="warning">When configuring user\-defined metadata, the key for user\-defined metadata using English letters supports only lowercase letters and does not allow spaces or other special characters.</div>



<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### **Setting Metadata Information During Standard Upload**

You can set object metadata to identify the purpose or attributes of an object. The following code is used to set object metadata.

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

  
    std::string data("Object data to be uploaded");
    auto ss = std::make_shared<std::stringstream>(data);
    PutObjectV2Input input(bucketName, objectName, ss);
 

    input.setAcl(ACLType::PublicRead);

    input.setStorageClass(StorageClassType::IA);

    input.setMeta({{"self-test", "yes"}});

    input.setContentType("application/json");

    auto output = client.putObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "PutObjectWithMetaData failed." << output.error().String() << std::endl;
  
        CloseClient();
        return -1;
    }

    std::cout << "PutObjectWithMetaData success. the object etag:" << output.result().getETag() << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".5YiG54mH5LiK5Lyg5pe26K6-572u5a-56LGh5YWD5pWw5o2u"></span>
### **Setting Object Metadata During Multipart Upload**

```cpp
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
    int64_t partSize = 100 * 1024;
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
    if (com.isSuccess()) {
       
        std::cout << "CompleteMultipartUpload failed." << upload.error().String() << std::endl;
  
        CloseClient();
        return -1;
    }
    std::cout << "CompleteMultipartUpload success." << com.result().getRequestInfo().getRequestId() << std::endl;
    CloseClient();
    return 0;
}
```


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt5o6l5Y-j6K6-572u5a-56LGh5YWD5pWw5o2u"></span>
### **Set object metadata via the setObjectMeta interface.** 

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

    SetObjectMetaInput input(bucketName,objectName);

    input.setMeta({{"self-test", "yes"}});
    auto output = client.setObjectMeta(input);
    if (!output.isSuccess()) {
   
        std::cout << "SetObjectMeta failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }

    std::cout << "SetObjectMeta success." << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Related Documents**

For API documentation on setting object metadata, refer to [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).

<span id=".6I635Y-W5a-56LGh5YWD5pWw5o2u"></span>
## Retrieving Object Metadata

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain object metadata, you must have the <code>tos:GetObject</code> permission. For specific instructions, refer to <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u"></span>
### **Query Object Metadata**

You can obtain object metadata using headObject. The following code example demonstrates how to retrieve object metadata.

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

    HeadObjectV2Input input(bucketName,objectName);
    auto output = client.headObject(input);
    if (!output.isSuccess()) {
       
        std::cout << "HeadObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "HeadObject success." << std::endl;
    std::cout << output.result().getStringFormatStorageClass() << ","
              << output.result().getContentDisposition() << ","
              << output.result().getContentType() << ","
              << output.result().getContentLength() << std::endl;
    for(const auto& meta : output.result().getMeta()){
        std::cout << meta.first << "," << meta.second << std::endl;
    }
   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Relevant Documentation**

For API documentation on querying object metadata, refer to [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
