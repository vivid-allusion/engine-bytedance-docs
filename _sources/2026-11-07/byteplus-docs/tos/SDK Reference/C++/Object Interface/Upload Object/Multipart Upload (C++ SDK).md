---
title: "Multipart Upload (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-c-sdk"
---

For larger objects, the data can be divided into multiple data blocks (parts) and uploaded separately. Finally, the merge parts operation is invoked to combine the uploaded data blocks into a single object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before initiating a multipart upload, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Before canceling a multipart upload task, you must have the `tos:AbortMultipartUpload` permission. For specific steps, see the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Shard numbering starts at 1 and has a maximum value of 10,000. Except for the last fragment, the minimum size of the other fragments is 4 MiB.

* When uploading objects, object names must comply with specific standards. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions storing object index data. To maximize horizontal scalability for uploading and downloading objects and to reduce the likelihood of hotspot partitions, please avoid using object names that increase lexicographically. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Chunked Upload Procedure

Multipart upload generally consists of the following three steps:


1. Initialize multipart upload task.

   Before uploading multipart data, you must first initialize the multipart upload and obtain an uploadID via the createMultipartUpload API. For subsequent operations such as uploading parts, merging parts, aborting the multipart upload, and listing uploaded parts, you need to pass in the uploadID parameter. Initializing a multipart upload task does not affect any existing objects with the same name.

2. Upload chunk.

   Use this interface to upload data parts. You must specify the uploadID obtained via createMultipartUpload, as well as the part number, which must be within the range [1, 10000]. For the same object and the same multipart upload task, multiple parts can be uploaded concurrently, and the order of upload does not affect the final merge operation.

   The SDK supports direct multipart upload via uploadPart, as well as file\-based multipart upload via uploadPartFromFile.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload task (identified by uploadId), the part number (partNumber) indicates the relative position of the part within the entire object. If data is uploaded multiple times using the same shard identifier, TOS will overwrite the original data and retain only the most recently uploaded version.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The response header contains the MD5 value of the data, which can be obtained via the ETag. When merging parts, you must specify all part information (part number and ETag value) from the current multipart upload task.   </div>
   

3. Multipart upload completed.

   After all parts have been uploaded, invoke the completeMultipartUpload method to merge all parts into a single complete object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
### **Complete Process of Multipart Upload**

The following code uploads a local file to the object `exampledir/exampleobject.txt` in the target bucket `examplebucket` using multipart upload. During upload, specify the ACL as PublicRead, set the storage type to infrequent access, and add custom metadata.

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
    // 5MB
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


<span id=".5YiX5Li-5bey5LiK5Lyg55qE5YiG54mH5L-h5oGv"></span>
### **List information of uploaded file fragments**

The following code is used to list the uploaded part information for the object `exampledir/exampleobject.txt` in the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
   
    std::string bucketName = "examplebucket";
  
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string uploadId = "f93f6fc9da94371f321e1008";
    
    
   
    InitializeClient();
 
    TosClientV2 client(region, accessKey, secretKey);

 
    ListPartsInput input(bucketName,objectName,uploadId);
   
    input.setMaxParts(100);
  
    input.setPartNumberMarker(1);
    auto output = client.listParts(input);
    if (!output.isSuccess()) {
       
        std::cout << "ListParts failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "ListParts success." << std::endl;
    for (const auto& part : output.result().getParts()) {
        std::cout << "part"<<
                ",partNumber:" << part.getPartNumber() <<
                ",eTag:" << part.getETag() <<
                ",size:" << part.getSize() <<
                ",lastModified time:" << part.getStringFormatLastModified() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### **Cancel Multipart Upload Task**

You can cancel a multipart upload task by using the abortMultipartUpload method. Once a multipart upload task is canceled, TOS will delete all previously uploaded part data, and you will no longer be able to perform any operations on this multipart upload task.

The following code is used to cancel the multipart upload task for the object `exampledir/exampleobject.txt` in the bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
int UploadObjectSample::AbortMultipartUpload(){


    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
  
    std::string objectName = "exampledir/exampleobject.txt";

    std::string uploadId = "f93f6fc9da94371f321e1008";



    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);


    AbortMultipartUploadInput input(bucketName,objectName,uploadId);
    auto output = client.abortMultipartUpload(input);
    if (!output.isSuccess()) {
     
        std::cout << "AbortMultipartUpload failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }
    std::cout << "AbortMultipartUpload success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**


* For the API documentation on creating a multipart upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on uploading parts, please refer to [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For API documentation on completing multipart uploads, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on aborting multipart upload tasks, please refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
