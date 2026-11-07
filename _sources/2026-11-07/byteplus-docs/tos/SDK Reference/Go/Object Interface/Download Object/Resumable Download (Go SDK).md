---
title: "Resumable Download (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-go-sdk"
---

When downloading large files, you can use the DownLoadFile download interface with breakpoint resume capability. The resumable download process utilizes segmented downloading to write content into a temporary file. If some segments are downloaded successfully while others fail, information regarding the successful and failed segments can be recorded and saved in a Checkpoint file. When re\-downloading the same object, only the failed chunks are downloaded. When all shards have been successfully processed, the temporary file is renamed to the official file, and the Checkpoint file is deleted.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. It is recommended that you utilize CDN products to enhance performance while simultaneously reducing your costs. For detailed information on accessing TOS via CDN, please refer to [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).

* The SDK records the download status information in the `Checkpoint` file, so the program must have write permissions for the `Checkpoint` file.

* When performing a resumable download, the progress information of the file is recorded in the `Checkpoint` file. If a segment fails to download during the process, the next download attempt will resume from the point recorded in the `Checkpoint` file, thereby achieving the effect of resumable download. After the download is complete, the `Checkpoint` file will be deleted.

* If, during the download process, the file's ETag changes or any part is lost or modified, the file will be re\-downloaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pat54K557ut5Lyg5LiL6L29"></span>
### **Resumable Download**

```go
package main

import (
   "context"
   "fmt"
   "sync"
   "time"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
)


type eventChange struct {
}

func (e eventChange) EventChange(event *tos.DownloadEvent) {
   switch event.Type {
   case enum.DownloadEventCreateTempFileSucceed:
      fmt.Println("Download File Create Temp File Success.")
   case enum.DownloadEventCreateTempFileFailed:
      fmt.Println("Download File Create Temp File Fail.")
   case enum.DownloadEventDownloadPartSucceed:
      fmt.Printf("Download %s %s part success, DownloadPartInfo:%v\n", event.Bucket, event.Key, event.DowloadPartInfo)
   case enum.DownloadEventDownloadPartAborted:
      fmt.Printf("Download %s %s part aborted.", event.Bucket, event.Key)
   case enum.DownloadEventDownloadPartFailed:
      fmt.Printf("Download %s %s part fail, err:%v\n", event.Bucket, event.Key, event.Err)
   case enum.DownloadEventRenameTempFileSucceed:
      fmt.Printf("Download %s %s success.\n", event.Bucket, event.Key)
   case enum.DownloadEventRenameTempFileFailed:
      fmt.Printf("Download %s %s fail,err:%v\n", event.Bucket, event.Key, event.Err)

   }
}


type listener struct {
}

func (l *listener) DataTransferStatusChange(event *tos.DataTransferStatus) {
   switch event.Type {
   case enum.DataTransferStarted:
      fmt.Println("Data transfer started")
   case enum.DataTransferRW:
      if event.TotalBytes != -1 {
         fmt.Printf("Once Read:%d,ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.RWOnceBytes, event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
      } else {
         fmt.Printf("Once Read:%d,ConsumerBytes:%d\n", event.RWOnceBytes, event.ConsumedBytes)
      }
   case enum.DataTransferSucceed:
      fmt.Printf("Data Transfer Succeed, ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
   case enum.DataTransferFailed:
      fmt.Printf("Data Transfer Failed\n")
   }
}

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

type rateLimit struct {
   rate     int64
   capacity int64

   currentAmount int64
   sync.Mutex
   lastConsumeTime time.Time
}

func NewDefaultRateLimit(rate int64, capacity int64) tos.RateLimiter {
   return &rateLimit{
      rate:            rate,
      capacity:        capacity,
      lastConsumeTime: time.Now(),
      currentAmount:   capacity,
      Mutex:           sync.Mutex{},
   }
}

func (d *rateLimit) Acquire(want int64) (ok bool, timeToWait time.Duration) {
   d.Lock()
   defer d.Unlock()
   if want > d.capacity {
      want = d.capacity
   }
   increment := int64(time.Now().Sub(d.lastConsumeTime).Seconds() * float64(d.rate))
   if increment+d.currentAmount > d.capacity {
      d.currentAmount = d.capacity
   } else {
      d.currentAmount += increment
   }
   if want > d.currentAmount {
      timeToWaitSec := float64(want-d.currentAmount) / float64(d.rate)
      return false, time.Duration(timeToWaitSec * float64(time.Second))
   }
   d.lastConsumeTime = time.Now()
   d.currentAmount -= want
   return true, 0
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
      
      bucketName = "*** Provide your bucket name ***"

      
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   cancel := tos.NewCancelHook()
   rateLimit1m := int64(1024 * 1024)
   output, err := client.DownloadFile(ctx, &tos.DownloadFileInput{
      HeadObjectV2Input: tos.HeadObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      
      FilePath: "./example.txt",
     
      PartSize: tos.DefaultPartSize,
     
      TaskNum: 5,
    
      EnableCheckpoint: true,
     
      CheckpointFile: "./example.checkpoint",
     
      DataTransferListener: &listener{},
     
      DownloadEventListener: eventChange{},
      
      RateLimiter: NewDefaultRateLimit(rateLimit1m, rateLimit1m),
    
      CancelHook: cancel,
   })
   checkErr(err)
   fmt.Println("DownloadFile Request ID:", output.RequestID)
}
```


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Progress Bar Configuration**

During resumable downloads, you can receive download progress by implementing the tos.DataTransferStatusChange interface. A sample code is provided below.

```go
package main

import (
   "context"
   "fmt"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
)


type listener struct {
}

func (l *listener) DataTransferStatusChange(event *tos.DataTransferStatus) {
   switch event.Type {
   case enum.DataTransferStarted:
      fmt.Println("Data transfer started")
   case enum.DataTransferRW:
      if event.TotalBytes != -1 {
         fmt.Printf("Once Read:%d,ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.RWOnceBytes, event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
      } else {
         fmt.Printf("Once Read:%d,ConsumerBytes:%d\n", event.RWOnceBytes, event.ConsumedBytes)
      }
   case enum.DataTransferSucceed:
      fmt.Printf("Data Transfer Succeed, ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
   case enum.DataTransferFailed:
      fmt.Printf("Data Transfer Failed\n")
   }
}

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
      
      bucketName = "*** Provide your bucket name ***"

      
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.DownloadFile(ctx, &tos.DownloadFileInput{
      HeadObjectV2Input: tos.HeadObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
     
      FilePath: "./example.txt",
    
      PartSize: tos.DefaultPartSize,
      
      TaskNum: 5,
    
      EnableCheckpoint: true,
      
      CheckpointFile: "./example.checkpoint",
      
      DataTransferListener: &listener{},
   })
   checkErr(err)
   fmt.Println("DownloadFile Request ID:", output.RequestID)
}
```


<span id=".6YWN572u5LqL5Lu25Zue6LCD"></span>
### **Configuring Event Callbacks**

The following code is used to customize the callback function for resumable download.

```go
package main

import (
   "context"
   "fmt"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
)


type eventChange struct {
}

func (e eventChange) EventChange(event *tos.DownloadEvent) {
   switch event.Type {
   case enum.DownloadEventCreateTempFileSucceed:
      fmt.Println("Download File Create Temp File Success.")
   case enum.DownloadEventCreateTempFileFailed:
      fmt.Println("Download File Create Temp File Fail.")
   case enum.DownloadEventDownloadPartSucceed:
      fmt.Printf("Download %s %s part success, DownloadPartInfo:%v\n", event.Bucket, event.Key, event.DowloadPartInfo)
   case enum.DownloadEventDownloadPartAborted:
      fmt.Printf("Download %s %s part aborted.", event.Bucket, event.Key)
   case enum.DownloadEventDownloadPartFailed:
      fmt.Printf("Download %s %s part fail, err:%v\n", event.Bucket, event.Key, event.Err)
   case enum.DownloadEventRenameTempFileSucceed:
      fmt.Printf("Download %s %s success.\n", event.Bucket, event.Key)
   case enum.DownloadEventRenameTempFileFailed:
      fmt.Printf("Download %s %s fail,err:%v\n", event.Bucket, event.Key, event.Err)

   }
}

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
      
      bucketName = "*** Provide your bucket name ***"

      
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   cancel := tos.NewCancelHook()
   output, err := client.DownloadFile(ctx, &tos.DownloadFileInput{
      HeadObjectV2Input: tos.HeadObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      
      FilePath: "./example.txt",
      
      PartSize: tos.DefaultPartSize,
      
      TaskNum: 5,
      
      EnableCheckpoint: true,
      
      DownloadEventListener: eventChange{},
      
      CancelHook: cancel,
   })
   checkErr(err)
   fmt.Println("DownloadFile Request ID:", output.RequestID)
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Throttling**

During resumable downloads, the client can utilize the tos.RateLimiter interface to restrict the bandwidth consumed by downloaded data. The corresponding code is shown below.

```go
package main

import (
   "context"
   "fmt"
   "sync"
   "time"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

type rateLimit struct {
   rate     int64
   capacity int64

   currentAmount int64
   sync.Mutex
   lastConsumeTime time.Time
}

func NewDefaultRateLimit(rate int64, capacity int64) tos.RateLimiter {
   return &rateLimit{
      rate:            rate,
      capacity:        capacity,
      lastConsumeTime: time.Now(),
      currentAmount:   capacity,
      Mutex:           sync.Mutex{},
   }
}

func (d *rateLimit) Acquire(want int64) (ok bool, timeToWait time.Duration) {
   d.Lock()
   defer d.Unlock()
   if want > d.capacity {
      want = d.capacity
   }
   increment := int64(time.Now().Sub(d.lastConsumeTime).Seconds() * float64(d.rate))
   if increment+d.currentAmount > d.capacity {
      d.currentAmount = d.capacity
   } else {
      d.currentAmount += increment
   }
   if want > d.currentAmount {
      timeToWaitSec := float64(want-d.currentAmount) / float64(d.rate)
      return false, time.Duration(timeToWaitSec * float64(time.Second))
   }
   d.lastConsumeTime = time.Now()
   d.currentAmount -= want
   return true, 0
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
      
      bucketName = "*** Provide your bucket name ***"

     
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   rateLimit1m := int64(1024 * 1024)
   output, err := client.DownloadFile(ctx, &tos.DownloadFileInput{
      HeadObjectV2Input: tos.HeadObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      
      FilePath: "./example.txt",
      
      PartSize: tos.DefaultPartSize,
     
      TaskNum: 5,
      
      EnableCheckpoint: true,
      
      CheckpointFile: "./example.checkpoint",
      
      RateLimiter: NewDefaultRateLimit(rateLimit1m, rateLimit1m),
   })
   checkErr(err)
   fmt.Println("DownloadFile Request ID:", output.RequestID)
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
### **Cancellation Mechanism**

The following code is used to cancel an ongoing breakpoint\-resume download task at runtime.

```go
package main

import (
   "context"
   "fmt"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", serverErr.Error())
         fmt.Println("Request ID:", serverErr.RequestID)
         fmt.Println("Response Status Code:", serverErr.StatusCode)
         fmt.Println("Response Header:", serverErr.Header)
         fmt.Println("Response Err Code:", serverErr.Code)
         fmt.Println("Response Err Msg:", serverErr.Message)
      } else if clientErr, ok := err.(*tos.TosClientError); ok {
         fmt.Println("Error:", clientErr.Error())
         fmt.Println("Client Cause Err:", clientErr.Cause.Error())
      } else {
         fmt.Println("Error:", err)
      }
      panic(err)
   }
}

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
      
      bucketName = "*** Provide your bucket name ***"

      
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   cancel := tos.NewCancelHook()
   output, err := client.DownloadFile(ctx, &tos.DownloadFileInput{
      HeadObjectV2Input: tos.HeadObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      
      FilePath: "./example.txt",
      
      PartSize: tos.DefaultPartSize,
      
      TaskNum: 5,
     
      EnableCheckpoint: true,
      
      CheckpointFile: "./example.checkpoint",
      
      CancelHook: cancel,
   })
   checkErr(err)
   fmt.Println("DownloadFile Request ID:", output.RequestID)
}
```
