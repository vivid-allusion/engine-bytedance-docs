---
title: "Standard Upload (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-c-sdk"
---

Standard upload refers to uploading a single object via the putObject method, supporting both string (character stream) uploads and local file uploads. Streaming upload refers to the process of using file streams, other streaming data, or strings as data sources for TOS, which are uniformly abstracted as iostream for uploading. File upload refers to using local files as the data source for TOS. This chapter describes how to upload your data using streaming upload and file upload methods. When uploading an object, if an object with the same name already exists in the bucket, the new object will overwrite the existing one. When versioning is enabled for a bucket, the original object is retained, and a new version identifier is generated to identify the newly uploaded object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading objects, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific standards. For detailed information, please refer to [Object Naming Standards](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To horizontally scale the maximum throughput for object upload and download and reduce the likelihood of hot partitions, avoid using lexicographically incremental object naming. For detailed information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".5paH5Lu25aS56K-05piO"></span>
## Folder Description


* If you wish to upload an object to a specific folder (a logical concept in object storage), you can add to the object's name...`/`The object name prefix supports multi\-level folders. For example, the object name `folder1/folder2/objectName` means that objectName will be uploaded to folder2, which is located under folder1.

* When uploading an object to a folder, the folder is merely a logical construct in object storage; as such, no actual folder is created on the object storage server.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiK5Lyg5a2X56ym5Liy"></span>
### **Upload String**

The following code is used to upload a string to the `exampledir/exampleobject.txt` object in the `examplebucket` bucket.

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


<span id=".5LuO5pys5Zyw5paH5Lu25rWB5LiK5Lyg"></span>
### **Upload from local file stream**

The following code is used to upload a local file stream to the `exampledir/exampleobject.txt` object in the target bucket `examplebucket`.

```cpp
#include <fstream>
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string filePath = "/localpath/examplefile.txt";
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);
    
    
    auto content = std::make_shared<std::fstream>(filePath, std::ios::in | std::ios_base::binary);
    PutObjectV2Input input(bucketName, objectName, content);
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
       
        std::cout << "PutObjectFromFileContent failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "PutObjectFromFileContent success. the object etag:" << output.result().getETag() << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
### **Upload Local File**

The following code is used to upload a local file to the object `exampledir/exampleobject.txt` in the target bucket `examplebucket`.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";

    std::string objectName = "exampledir/exampleobject.txt";
    
    std::string filePath = "/localpath/examplefile.txt";

    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    PutObjectFromFileInput input(bucketName, objectName, filePath);
    auto output = client.putObjectFromFile(input);
    if (!output.isSuccess()) {
      
        std::cout << "PutObjectWithMetaData failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
    std::cout << "PutObjectFromFileContent success. the object etag:" << output.result().getPutObjectV2Output().getETag() << std::endl;


    CloseClient();
    return 0;
}
```


<span id=".6YGN5Y6G5pys5Zyw5paH5Lu25aS55bm25LiK5Lyg5Yiw5qG25Lit"></span>
### **Traverse the local folder and upload to the bucket.** 

```cpp
#include "TosClientV2.h"
#include <dirent.h>
using namespace VolcengineTos;

static void GenerateFilePaths(const std::string& folderPath,std::vector<std::string>& filePaths){
    struct dirent *dirp;
    DIR *dp = opendir(folderPath.c_str());
    if(dp == nullptr){
        return;
    }
    while((dirp = readdir(dp)) != nullptr){
     
        if(dirp->d_type == 8){
            std::string fileName = dirp->d_name;
            std::string filePath = folderPath + fileName;
            filePaths.push_back(filePath);
        }
     
        if(dirp->d_type == 4){
            std::string folderName = dirp->d_name;
       
            if(folderName != "." && folderName != ".."){
                std::string NewfolderPath = folderPath + folderName + "/";
                mkFilePaths(NewfolderPath,filePaths);
            }
        }
    }
    closedir(dp);
}
int main(void){

 
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
 
    std::string bucketName = "examplebucket";
 
    std::string objectName = "exampledir/exampleobject.txt";
  
    std::string folderPath = "/localpath/";

    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    std::vector<std::string> filePaths;
    
    GenerateFilePaths(folderPath,filePaths);
    PutObjectFromFileInput input(bucketName);
    for (auto& filePath : filePaths ){
        input.setKey(filePath);
        input.setFilePath(filePath);
        auto output = client.putObjectFromFile(input);
        if (!output.isSuccess()) {
            
            std::cout << "PutObjectFromFile failed. the object name:" << filePath << std::endl;
            std::cout << "PutObjectFromFile failed." << output.error().String() << std::endl;
        }
        std::cout << "PutObjectFromFile success. the object name:" << filePath << std::endl;
    }
    
    

    CloseClient();
    return 0;

};
```


<span id=".5LiK5Lyg5a-56LGh5pe25oyH5a6aLWFjbOOAgXN0b3JhZ2VjbGFzc-OAgeWvueixoeWFg-aVsOaNruetiQ=="></span>
### **Specify ACL, StorageClass, object metadata, and other parameters when uploading an object.** 

When performing stream uploads or file uploads, the SDK supports configuring the ACL and metadata of the object to be uploaded.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The ACL, StorageClass, and object metadata parameters for the object are all optional; please select them according to your specific requirements.</div>


The following code is used to upload a character stream to the object `exampledir/exampleobject.txt` in the target bucket `examplebucket`, while specifying parameters such as the object's ACL, StorageClass, and object metadata.

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


<span id=".6L-b5bqm5p2h5aSE55CG"></span>
### **Progress Bar Handling**

The following code provides an example of uploading a string to illustrate the use of a progress bar.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;


static void ProgressCallback(std::shared_ptr<DataTransferStatus> datatransferstatus) {
    int64_t consumedBytes = datatransferstatus->consumedBytes_;
    int64_t totalBytes = datatransferstatus->totalBytes_;
    int64_t rwOnceBytes = datatransferstatus->rwOnceBytes_;
    DataTransferType type = datatransferstatus->type_;
    int64_t rate = 100 * consumedBytes / totalBytes;
    std::cout << "rate:" << rate << ","
              << "ConsumedBytes:" << consumedBytes << ","
              << "totalBytes:" << totalBytes << ","
              << "rwOnceBytes:" << rwOnceBytes << ","
              << "DataTransferType:" << type << std::endl;
}

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
    
    
    DataTransferListener datatransferlistener = {ProgressCallback, nullptr};
    input.setDataTransferListener(datatransferlistener);
    
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
      
        std::cout << "PutObjectWithProcess failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }
    std::cout << "PutObjectWithProcess success. the object etag:" << output.result().getETag() << std::endl;

    
    CloseClient();
    return 0;
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configure Client Bandwidth Limiting**

The following code is used to configure client\-side rate limiting during normal upload.

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
    
  
    std::string data("1234567890abcdefghijklmnopqrstuvwxyz");
    auto ss = std::make_shared<std::stringstream>(data);
    PutObjectV2Input input(bucketName, objectName, ss);
    
   
    std::shared_ptr<RateLimiter> RateLimiter(NewRateLimiter(10 * 1024 * 1024, 5 * 1024 * 1024));
    input.setRateLimiter(RateLimiter);
    
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "PutObjectWithRateLimiter failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "PutObjectWithRateLimiter success. the object etag:" << output.result().getETag() << std::endl;

  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on uploading objects, refer to [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
