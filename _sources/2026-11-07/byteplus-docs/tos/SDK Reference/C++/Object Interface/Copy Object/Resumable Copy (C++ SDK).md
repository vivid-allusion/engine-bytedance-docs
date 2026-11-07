---
title: "Resumable Copy (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-copy-c-sdk"
---

Resumable copy is suitable for scenarios where large objects are copied using the TOS C++ SDK either within a single bucket or between two buckets in the same region. The TOS C++ SDK provides a resumable download feature, utilizing a local checkpoint mechanism to record segments that have been successfully copied. In the event of network exceptions or machine failures that interrupt segment copying, this interface can be invoked again to resume the download process.

Resumable copying divides the object to be copied into multiple segments and supports concurrent copying. Once all segments have been copied, they are merged into a complete file. You can configure the segment size for resumable copy operations, the number of threads for segment copying, event callback functions, and other related parameters. It is also possible to cancel the task during the execution of the resumable copy task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* File copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you may retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5pat54K557ut5Lyg5ou36LSd"></span>
## **Resumable Copy**

The following code is used to perform a resumable copy of the object srcdir/exampleobject.txt from the srcbucket bucket to the destbucket bucket, assigning the object name destdir/exampleobject.txt in the destination. It also supports resuming the copy operation in case of failure. If a network timeout error occurs during the copy process, you can resume the download from the breakpoint and re\-enter the download process by invoking resumableCopyObject with the same parameters.

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
   
   
    std::string CheckpointFilePath = "yourCheckpointFilepath";
    
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);

    ResumableCopyObjectInput input;
    
    input.setBucket(bucketName);
    input.setKey(objectName);
    input.setSrcBucket(srcBucketName);
    input.setSrcKey(srcObjectName);

    
    input.setTaskNum(1);
    
    input.setEnableCheckpoint(true);
  
    input.setPartSize(5 * 1024 * 1024);

    auto output = client.resumableCopyObject(input);
    if (!output.isSuccess()) {
      
        std::cout << "ResumableCopyObject failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "ResumableCopyObject success. object etag is: " << output.result().getETag() << std::endl;
   
    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
## **Handling Event Callbacks**

During the invocation of the resumableCopyObject interface, events such as initializing multipart copy tasks, copying parts, and merging parts are triggered. You can pass in a custom interface to monitor download\-related events and implement your own business logic.

The following code is used to customize the callback function for resumable copy operations.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static void CopyCallBack(std::shared_ptr<CopyEvent> event) {
    CopyEventType type_ = event->type_;
    bool error_ = event->error_;
    std::string bucket_ = event->bucket_;
    std::string key_ = event->key_;
    std::string fileInfo = bucket_ + key_;
    std::shared_ptr<std::string> uploadId_ = event->uploadId_;
    std::shared_ptr<std::string> checkpointFile_ = event->checkpointFile_;
    std::shared_ptr<CopyPartInfo> uploadPartInfo_ = event->copyPartInfo_;
    std::string uploadPartInfo = "";
    if (uploadPartInfo_ != nullptr) {
        uploadPartInfo = std::to_string(uploadPartInfo_->partNumber_) + "," +
                         std::to_string(uploadPartInfo_->copySourceRangeStart_) + "," +
                         std::to_string(uploadPartInfo_->copySourceRangeEnd_) + "," + *(uploadPartInfo_->eTag_);
    }
    std::cout << "type:" << type_ << ","
              << "error:" << error_ << ","
              << "fileInfo:" << fileInfo << ","
              << "checkpointFile:" << *checkpointFile_ << ","
              << "uploadId:" << *uploadId_ << ","
              << "uploadPartInf:" << uploadPartInfo << std::endl;
}

int main(void){
    
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
 
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";
    
    
    std::string CheckpointFilePath = "yourCheckpointFilepath";
   
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    ResumableCopyObjectInput input;
    
    input.setBucket(bucketName);
    input.setKey(objectName);
    input.setSrcBucket(srcBucketName);
    input.setSrcKey(srcObjectName);

  
    input.setTaskNum(1);
    
    input.setEnableCheckpoint(true);
    
    input.setPartSize(5 * 1024 * 1024);
    
    CopyEventListener copyHandler = {CopyCallBack};
    input.setCopyEventListener(copyHandler);
    auto output = client.resumableCopyObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "ResumableCopyObject failed." << output.error().String() << std::endl;
 
        CloseClient();
        return -1;
    }
    std::cout << "ResumableCopyObject success. object etag is: " << output.result().getETag() << std::endl;
 
    CloseClient();
    return 0;
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
## **Cancellation Mechanism**

The resumableCopyObject interface allows you to actively pause or cancel a resumable transfer task. Pausing a resumable download task will stop the download. When resumableCopyObject is invoked again, the download can resume from the point where it was previously paused. Canceling a resumable transfer task will stop the download and delete the local CheckPoint file as well as any temporary files. If resumableCopyObject is called again, the upload will restart from the beginning.

The following code demonstrates how to pause or cancel a resumable copy operation.

```cpp
#include "TosClientV2.h"
#include <thread>
using namespace VolcengineTos;

static void threadFunction1(TosClientV2 client, ResumableCopyObjectInput input) {
    auto output = client.resumableCopyObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "ResumableCopyObject failed." << output.error().String() << std::endl;
        
        CloseClient();
    }
    std::cout << "ResumableCopyObject success. object etag is: " << output.result().getETag() << std::endl;
}

static void threadFunction2(std::shared_ptr<CancelHook> CancelHook) {
    
    CancelHook->Cancel(false);
}

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
     
    std::string bucketName = "destbucket";
    
    std::string objectName = "destdir/exampleobject.txt";
    
    std::string srcBucketName = "srcbucket";
    
    std::string srcObjectName = "srcdir/exampleobject.txt";
    
    
    std::string CheckpointFilePath = "yourCheckpointFilepath";
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);

    ResumableCopyObjectInput input;
    
    input.setBucket(bucketName);
    input.setKey(objectName);
    input.setSrcBucket(srcBucketName);
    input.setSrcKey(srcObjectName);

    
    input.setTaskNum(1);
    
    input.setEnableCheckpoint(true);
    
    input.setPartSize(5 * 1024 * 1024);
    
    std::shared_ptr<CancelHook> CancelHook(NewCancelHook());
    input.setCancelHook(CancelHook);

    
    std::thread thread1(threadFunction1, client, input);
    thread1.detach();
    TimeUtils::sleepSecondTimes(5);
    
    std::thread thread2(threadFunction2, CancelHook);
    thread2.join();
    
    CloseClient();
    return 0;
}
```
