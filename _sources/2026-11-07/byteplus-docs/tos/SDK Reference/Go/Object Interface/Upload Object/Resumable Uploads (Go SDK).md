---
title: "Resumable Uploads (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-go-sdk"
---

When uploading files to TOS using the resumable upload method, you can configure parameters such as part size, number of upload threads, client\-side upload rate limiting, and event callback functions. During the upload process, if a network anomaly or program crash causes the file upload to fail, the system will resume uploading the incomplete portion from the last recorded breakpoint. During the upload process, you can cancel the object upload by invoking the Cancel method of the passed\-in CancelHook.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading objects, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with specific standards. For detailed information, please refer to [Object Naming Standards](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To enable horizontal scaling of maximum throughput for uploading and downloading objects and to reduce the likelihood of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.

* The SDK records the upload status information in the `Checkpoint` file. Therefore, the program must have write permissions for the `Checkpoint` file.

* When using resumable upload, the file upload progress is recorded in the `Checkpoint` file. If a segment fails to upload during the process, when uploading again, it will resume from the point recorded in the `Checkpoint` file. After the upload is complete, the `Checkpoint` file will be deleted.

* If the local file is modified during the upload process, all segments will be re\-uploaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiK5Lyg5paH5Lu2"></span>
### **Upload File**

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
      
      fileName = "/usr/local/testfile.txt"
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   output, err := client.UploadFile(ctx, &tos.UploadFileInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      
      FilePath: fileName,
     
      PartSize: tos.DefaultPartSize,
     
      TaskNum: 5,
     
      EnableCheckpoint: true,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".6YGN5Y6G5pys5Zyw5paH5Lu25aS55bm25LiK5Lyg5Yiw5qG25Lit"></span>
### **Traverse the local folder and upload its contents to the bucket.** 

```go
package main

import (
   "context"
   "errors"
   "fmt"
   "io/ioutil"
   "os"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

var (
   accessKey = os.Getenv("TOS_ACCESS_KEY")
   secretKey = os.Getenv("TOS_SECRET_KEY")
   
   endpoint = "your endpoint"
   region   = "your region"
  
   bucketName = "*** Provide your bucket name ***"
   
   dirPath = "/usr/local/"
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

var cli *tos.ClientV2

func uploadDir(ctx context.Context, dirPath string) error {
   file, err := os.Stat(dirPath)
   if err != nil {
      return err
   }

   if !file.IsDir() {
      return errors.New("please input file path. ")
   }
   files, err := ioutil.ReadDir(dirPath)
   for _, f := range files {
      if f.IsDir() {
         err = uploadDir(ctx, dirPath+f.Name())
         if err != nil {
            return nil
         }
         continue
      }
      output, err := cli.UploadFile(ctx, &tos.UploadFileInput{
         CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
            Bucket: bucketName,
            Key:    dirPath + f.Name(),
         },
       
         FilePath: dirPath + f.Name(),
         
         PartSize: tos.DefaultPartSize,
       
         TaskNum: 5,
        
         EnableCheckpoint: true,
      })
      checkErr(err)
      fmt.Println("PutObjectV2 Request ID:", output.RequestID)
   }
}

func main() {

  
   var err error
   cli, err = tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   ctx := context.Background()
   err = uploadDir(ctx, dirPath)
   if err != nil {
      panic(err)
   }

}
```


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Configuring the Progress Bar**

During resumable uploads, you can receive upload progress by implementing the tos.DataTransferStatusChange interface. A sample code is provided below.

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
      
      endpoint = "your endpoint    bucketName = "*** Provide your bucket name ***"

     
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
     
      fileName = "/usr/local/testfile.txt"
   )
 
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
 
   output, err := client.UploadFile(ctx, &tos.UploadFileInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
   
      FilePath: fileName,
    
      PartSize: tos.DefaultPartSize,
      
      TaskNum: 5,
   
      EnableCheckpoint: true,
    
      DataTransferListener: &listener{},
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
### **Handling Event Callbacks**

The following code is used to customize the callback function for resumable upload.

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

func (e eventChange) EventChange(event *tos.UploadEvent) {
   switch event.Type {
   case enum.UploadEventCreateMultipartUploadSucceed:
      fmt.Printf("Upload to %s %s create multipart upload success, upload id:%s\n", event.Bucket, event.Key, event.UploadID)
   case enum.UploadEventCreateMultipartUploadFailed:
      fmt.Printf("Upload to %s %s create multipart upload fail, err:%v\n", event.Bucket, event.Key, event.Err)
   case enum.UploadEventUploadPartSucceed:
      fmt.Printf("Upload to %s %s part success, UploadPartInfo:%v\n", event.Bucket, event.Key, event.UploadPartInfo)
   case enum.UploadEventUploadPartAborted:
      fmt.Printf("Upload to %s %s part aborted,  upload id:%s\n", event.Bucket, event.Key, event.UploadID)
   case enum.UploadEventUploadPartFailed:
      fmt.Printf("Upload to %s %s part fail,  upload id:%s, err:%v\n", event.Bucket, event.Key, event.UploadID, event.Err)
   case enum.UploadEventCompleteMultipartUploadSucceed:
      fmt.Printf("Upload to %s %s success,  upload id:%s\n", event.Bucket, event.Key, event.UploadID)
   case enum.UploadEventCompleteMultipartUploadFailed:
      fmt.Printf("Upload to %s %s fail,  upload id:%s, err:%v\n", event.Bucket, event.Key, event.UploadID, event.Err)

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
   
      fileName = "/usr/local/testfile.txt"
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.UploadFile(ctx, &tos.UploadFileInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
   
      FilePath: fileName,
  
      PartSize: tos.DefaultPartSize,

      TaskNum: 5,

      EnableCheckpoint: true,
 
      UploadEventListener: eventChange{},
      
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Throttling**

During resumable uploads, bandwidth usage can be restricted on the client side by utilizing the tos.RateLimiter interface. The following code demonstrates this implementation.

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
    
      fileName = "/usr/local/testfile.txt"
   )
 
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   rateLimit1m := int64(1024 * 1024)
   output, err := client.UploadFile(ctx, &tos.UploadFileInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
    
      FilePath: fileName,
     
      PartSize: tos.DefaultPartSize,
   
      TaskNum: 5,
   
      EnableCheckpoint: true,
   
      RateLimiter: NewDefaultRateLimit(rateLimit1m, rateLimit1m),
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
### **Cancellation Mechanism**

The following code is used to cancel an ongoing resumable upload task during runtime.

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
   
      fileName = "/usr/local/testfile.txt"
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   cancel := tos.NewCancelHook()
   output, err := client.UploadFile(ctx, &tos.UploadFileInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
     
      FilePath: fileName,
    
      PartSize: tos.DefaultPartSize,
   
      TaskNum: 5,
   
      EnableCheckpoint: true,
      
      CancelHook: cancel,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```
