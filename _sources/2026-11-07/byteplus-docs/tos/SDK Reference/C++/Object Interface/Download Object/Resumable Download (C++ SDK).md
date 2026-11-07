---
title: "Resumable Download (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-c-sdk"
---

When downloading large objects, network fluctuations and similar issues may result in download failures. The TOS C++ SDK provides a retry mechanism to enhance the stability of object downloads; however, it is possible that, even after multiple retries, the download may still not be completed. To address the aforementioned situation, the TOS C++ SDK provides a resumable download feature, utilizing a local checkpoint mechanism to record successfully downloaded file segments. If a download is interrupted due to network anomalies or machine failures, this interface can be invoked again to resume the download.

Resumable download divides the target object into multiple segments and supports concurrent downloading. Once all segments have been downloaded, they are merged into a complete file. You can configure the chunk size for resumable downloads, the number of threads for downloading chunks, client\-side download speed limits, event callback functions, etc. It is also possible to cancel the task during the execution of a resumable download task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities simultaneously, your access speed will be restricted by TOS bandwidth and regional limitations. It is recommended that you utilize CDN products to enhance performance while simultaneously reducing your costs.

* The SDK records the download status information in the `Checkpoint` file, so the program must have write permissions for the `Checkpoint` file.

* When performing a resumable download, the progress information of the file is recorded in the `Checkpoint` file. If a segment fails to download during the process, the subsequent download will resume from the point recorded in the `Checkpoint` file, thereby achieving the effect of download resumption. After the download is complete, the `Checkpoint` file will be deleted.

* If, during the download process, the file's ETag changes or any part is missing or modified, the file will be re\-downloaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5pat54K557ut5Lyg5LiL6L29"></span>
### **Resumable download**

The following code is used to perform a resumable download of the object `exampledir/exampleobject.txt` from the bucket `examplebucket` to a local file, and to retry the download in case of failure. If a network timeout error occurs during the download process, you can call downloadFile with the same parameters to resume the download from the breakpoint and re\-enter the process.

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

    
    DownloadFileInput input(bucketName, objectName);
    
    input.setTaskNum(10);
   
    input.setEnableCheckpoint(true);
  
    input.setPartSize(20 * 1024 * 1024);
    
    input.setFilePath(filePath);
    auto output = client.downloadFile(input);
    if (!output.isSuccess()) {
        
        std::cout << "DownloadFile failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "DownloadFile success. object etag is: " << output.result().getHeadObjectV2Output().getETags() << std::endl;
    
    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG6L-b5bqm5p2h"></span>
### **Configure progress bar**

The following code configures the resumable download progress bar functionality.

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

  
    DownloadFileInput input(bucketName, objectName);
  
    input.setTaskNum(10);
   
    input.setEnableCheckpoint(true);
   
    input.setPartSize(20 * 1024 * 1024);
    
    input.setFilePath(filePath);
    
    DataTransferListener processHandler = {ProgressCallback, nullptr};
    input.setDataTransferListener(processHandler);

    auto output = client.downloadFile(input);
    if (!output.isSuccess()) {
        
        std::cout << "DownloadFile failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    std::cout << "DownloadFile success. object etag is: " << output.result().getHeadObjectV2Output().getETags() << std::endl;
 
    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
### **Handle event callbacks**

During the invocation of the downloadFile API, events such as temporary file creation, file segment download, and temporary file renaming are triggered. You may pass in a custom interface to monitor these download\-related events and implement your own business logic.

The following code is used to customize the callback function for resumable downloads.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static void DownloadCallBack(std::shared_ptr<DownloadEvent> event) {
    DownloadEventType type_ = event->type_;
    bool error_ = event->error_;
    std::string bucket_ = event->bucket_;
    std::string key_ = event->key_;
    std::string versionId_ = event->versionId_;
    std::string filePath_ = event->filePath_;
    std::string fileInfo = bucket_ + key_ + versionId_ + filePath_;
    std::shared_ptr<std::string> checkpointFile_ = event->checkpointFile_;
    std::shared_ptr<std::string> tempFilePath_ = event->tempFilePath_;
    std::shared_ptr<DownloadPartInfo> downloadPartInfo_ = event->downloadPartInfo_;
    std::string downloadPartInfo = "";
    if (downloadPartInfo_ != nullptr) {
        downloadPartInfo = std::to_string(downloadPartInfo_->rangeStart_) + "," +
                           std::to_string(downloadPartInfo_->rangeEnd_) + "," +
                           std::to_string(downloadPartInfo_->partNumber_);
    }

    std::cout << "type:" << type_ << ","
              << "error:" << error_ << ","
              << "fileInfo:" << fileInfo << ","
              << "checkpointFile:" << *checkpointFile_ << ","
              << "tempFilePath:" << *tempFilePath_ << ","
              << "downloadPartInfo:" << downloadPartInfo << std::endl;
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


    
    DownloadFileInput input(bucketName, objectName);
  
    input.setTaskNum(10);
    
    input.setEnableCheckpoint(true);
    
    input.setPartSize(20 * 1024 * 1024);

    input.setFilePath(filePath);

    DownloadEventListener downloadHandler = {DownloadCallBack};
    input.setDownloadEventListener(downloadHandler);

    auto output = client.downloadFile(input);
    if (!output.isSuccess()) {
        
        std::cout << "DownloadFile failed." << output.error().String() << std::endl;
   
        CloseClient();
        return -1;
    }
    std::cout << "DownloadFile success. object etag is: " << output.result().getHeadObjectV2Output().getETags() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5aSE55CG5a6i5oi356uv6ZmQ6YCf"></span>
### **Manage client\-side rate limiting**

The following code is used to set the speed limit for a resumable download client.

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

 
    DownloadFileInput input(bucketName, objectName);
 
    input.setTaskNum(10);

    input.setEnableCheckpoint(true);

    input.setPartSize(20 * 1024 * 1024);

    input.setFilePath(filePath);
  
    std::shared_ptr<RateLimiter> RateLimiter(NewRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024));
    input.setRateLimiter(RateLimiter);

    auto output = client.downloadFile(input);
    if (!output.isSuccess()) {
  
        std::cout << "DownloadFile failed." << output.error().String() << std::endl;
  
        CloseClient();
        return -1;
    }
    std::cout << "DownloadFile success. object etag is: " << output.result().getHeadObjectV2Output().getETags() << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
### **Pause or cancel resumable download**

The downloadFile interface allows you to proactively pause or cancel a resumable transfer task. Pausing a resumable download task will stop the download. When downloadFile is invoked again, the download can resume from the position where it was previously paused. 

The following code demonstrates how to pause or cancel a resumable transfer.

```cpp
#include "TosClientV2.h"
#include <thread>
using namespace VolcengineTos;

static void threadFunction1(TosClientV2 client, DownloadFileInput input) {
    auto output = client.downloadFile(input);
    if (!output.isSuccess()) {
        std::cout << "DownloadFile failed." << output.error().String() << std::endl;
    }

    std::cout << "DownloadFile success. object etag is: " << output.result().getHeadObjectV2Output().getETags()  << std::endl;
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

  
    DownloadFileInput input(bucketName, objectName);
  
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
