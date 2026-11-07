---
title: "Resumable Transfer (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-c-sdk"
---

Before uploading files to TOS using resumable upload, you can configure parameters such as part size, number of upload threads, client\-side upload speed limit, and event callback functions. It is also possible to cancel the task during the execution of a resumable upload task. If a network error or similar issue causes the file upload to fail, the system will resume uploading the unfinished portion from the last recorded breakpoint.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading an object, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific standards. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for massive storage, with internal partitions that store object index data. To maximize the throughput of your object uploads and downloads and to reduce the likelihood of hotspot partitions as the system scales horizontally, please avoid using object names that increase in lexicographical order. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.

* The SDK records the upload status information in the `Checkpoint` file, so the program must have write permission for the `Checkpoint` file.

* When using resumable upload, the file upload progress information is recorded in the `Checkpoint` file. If a part fails to upload during the process, the next upload will resume from the point recorded in the `Checkpoint` file. Once uploading is complete, the `Checkpoint` file will be deleted.

* If the local file is modified during the upload process, all segments will be re\-uploaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pat54K557ut5Lyg5LiK5Lyg"></span>
### **Resumable Upload**

The following code is used for resumable upload, transferring a local file to the object `exampledir/exampleobject.txt` in the target bucket `examplebucket`. If a network timeout error is returned during the upload process, you can resume the upload from the breakpoint by invoking uploadFile again with the same parameters.

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

    std::string CheckpointFilePath = "yourCheckpointFilepath";
    
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);

  
    UploadFileV2Input input(bucketName, objectName);

    input.setTaskNum(10);
    
    input.setEnableCheckpoint(true);
    
    input.setPartSize(20 * 1024 * 1024);
  
    input.setFilePath(filePath);
    auto output = client.uploadFile(input);
    if (!output.isSuccess()) {
       
        std::cout << "UploadFile failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "UploadFile success. object etag is: " << output.result().getETag() << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG6L-b5bqm5p2h"></span>
### **Processing Progress Bar**

The following code is used to configure the upload progress bar functionality for resumable uploads.

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

    std::string filePath = "/localpath/examplefile.txt";
   
 
    std::string CheckpointFilePath = "yourCheckpointFilepath";
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);

   
    UploadFileV2Input input(bucketName, objectName);
 
    input.setTaskNum(10);
  
    input.setEnableCheckpoint(true);

    input.setPartSize(20 * 1024 * 1024);

    input.setFilePath(filePath);
    
    DataTransferListener processHandler = {ProgressCallback, nullptr};
    input.setDataTransferListener(processHandler);

    auto output = client.uploadFile(input);
    if (!output.isSuccess()) {
      
        std::cout << "UploadFile failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "UploadFile success. object etag is: " << output.result().getETag() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
### **Handling Event Callbacks**

During the invocation of the uploadFile interface, events such as chunk initialization, chunk uploading, and chunk merging are triggered. You may pass in a custom interface to listen for relevant upload events and implement your own business logic. The following code demonstrates the functionality of a custom callback function for resumable upload.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static void UploadCallBack(std::shared_ptr<UploadEvent> event) {
    UploadEventType type_ = event->type_;
    bool error_ = event->error_;
    std::string bucket_ = event->bucket_;
    std::string key_ = event->key_;
    std::string fileInfo = bucket_ + key_;
    std::shared_ptr<std::string> uploadId_ = event->uploadId_;
    std::shared_ptr<std::string> checkpointFile_ = event->checkpointFile_;
    std::shared_ptr<UploadPartInfo> uploadPartInfo_ = event->uploadPartInfo_;
    std::string uploadPartInfo = "";
    if (uploadPartInfo_ != nullptr) {
        uploadPartInfo = std::to_string(uploadPartInfo_->partSize_) + "," + std::to_string(uploadPartInfo_->offset_) +
                         "," + std::to_string(uploadPartInfo_->partNumber_) + "," + *(uploadPartInfo_->eTag_) + "," +
                         std::to_string(*(uploadPartInfo_->hashCrc64ecma_));
    }
    std::cout << "type:" << type_ << ","
              << "error:"<< error_ << ","
              << "fileInfo:" << fileInfo << ","
              << "checkpointFile:" << *checkpointFile_ << ","
              << "uploadId:" << *uploadId_ << ","
              << "uploadPartInf:" << uploadPartInfo << std::endl;
}

int main(void){


    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";

    std::string objectName = "exampledir/exampleobject.txt";

    std::string filePath = "/localpath/examplefile.txt";

    std::string CheckpointFilePath = "yourCheckpointFilepath";
 
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

 
    UploadFileV2Input input(bucketName, objectName);

    input.setTaskNum(10);

    input.setEnableCheckpoint(true);
  
    input.setPartSize(20 * 1024 * 1024);

    input.setFilePath(filePath);

    UploadEventListener uploadHandler = {UploadCallBack};
    input.setUploadEventListener(uploadHandler);

    auto output = client.uploadFile(input);
    if (!output.isSuccess()) {
    
        std::cout << "UploadFile failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "UploadFile success. object etag is: " << output.result().getETag() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".6K6-572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Limitation**

The following code is used to configure rate limiting for the resumable upload client.

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
   
    std::string CheckpointFilePath = "yourCheckpointFilepath";
  
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);

  
    UploadFileV2Input input(bucketName, objectName);
 
    input.setTaskNum(10);
   
    input.setEnableCheckpoint(true);
 
    input.setPartSize(20 * 1024 * 1024);
 
    input.setFilePath(filePath);
   
    std::shared_ptr<RateLimiter> RateLimiter(NewRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024));
    input.setRateLimiter(RateLimiter);

    auto output = client.uploadFile(input);
    if (!output.isSuccess()) {
     
        std::cout << "UploadFile failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
    std::cout << "UploadFile success. object etag is: " << output.result().getETag() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
### **Cancellation Mechanism**

The uploadFile interface allows you to actively pause or cancel resumable upload tasks. Pausing a resumable upload task will halt the upload process. When uploadFile is called again, the upload can resume from the point where it was previously paused. Canceling a resumable upload task will halt the upload process, delete the local CheckPoint file, and invoke abortMultipartUpload to remove the multipart upload task. If uploadFile is called again, the upload will restart from the beginning.

The following code demonstrates how to pause or cancel a resumable transfer.

```cpp
#include "TosClientV2.h"
#include <thread>
using namespace VolcengineTos;

static void threadFunction1(TosClientV2 client, UploadFileV2Input input) {
    auto output = client.uploadFile(input);
    if (!output.isSuccess()) {
        std::cout << "UploadFile failed." << output.error().String() << std::endl;
    }
    std::cout << "UploadFile success. object etag is: " << output.result().getETag() << std::endl;
}

static void threadFunction2(std::shared_ptr<CancelHook> CancelHook) {
 
    CancelHook->Cancel(false);
}

int main(void){

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
   
    std::string objectName = "exampledir/exampleobject.txt";

    std::string filePath = "/localpath/examplefile.txt";
 
    std::string CheckpointFilePath = "yourCheckpointFilepath";
 
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);


    UploadFileV2Input input(bucketName, objectName);

    input.setTaskNum(10);

    input.setEnableCheckpoint(true);

    input.setPartSize(20 * 1024 * 1024);

    input.setFilePath(filePath);
    
    std::shared_ptr<CancelHook> CancelHook(NewCancelHook());
    input.setCancelHook(CancelHook);

   
    std::thread thread1(threadFunction1, client, input);
    thread1.detach();
    TimeUtils::sleepSecondTimes(5);
  
    std::thread thread2(threadFunction2, CancelHook);
    thread1.join();
    thread2.join();
   
    CloseClient();
    return 0;
}
```
