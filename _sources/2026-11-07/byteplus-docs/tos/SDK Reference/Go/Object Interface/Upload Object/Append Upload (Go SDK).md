---
title: "Append Upload (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-go-sdk"
---

The AppendObjectV2 interface is used to perform append\-write operations on an object. Append write refers to adding content to the end of an already uploaded object. This interface can only be used with objects of type Appendable. Objects created through direct upload and multipart upload are of type Normal.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before performing an append upload to an object, you must have the `tos:PutObject` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific conventions. For detailed information, please refer to [Object Naming Conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage. Its internal partitions store object index data. To horizontally scale the maximum throughput for uploading and downloading objects and to reduce the likelihood of hotspot partitions, please avoid using object naming methods that increase in lexicographical order. For more details, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.

* Append upload does not support requests using Chunk\-Encoded transfer encoding. When performing append uploads with network streams, please retrieve data iteratively and append each chunk as you receive it.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limitation Statement

The following outlines the object size limitations when using the AppendObject interface:


* The size of the object after appending must not exceed 5 GiB.

* When an object created using AppendObject is subjected to a PutObject operation, the object is overwritten and its type changes from Appendable to Normal. Conversely, objects uploaded via PutObject do not support append write operations.

* <SOURCE_TEXT\>Objects created by AppendObject do not support copying.</SOURCE_TEXT\>

* The AppendObject interface cannot be used if the object type is Infrequent Access Storage or Archive Instant Retrieval Storage.

* If your bucket has versioning enabled or suspended, the AppendObject interface cannot be used.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

<span id=".6L-95Yqg5LiK5Lyg"></span>
### **Additional Upload**

The following code is used to append\-upload a character stream to the target bucket.

```go
package main

import (
    "context"
    "fmt"
    "net/http"
    "os"
    "strings"

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
    body := strings.NewReader("your append object value")
    
    
    output, err := client.AppendObjectV2(ctx, &tos.AppendObjectV2Input{
       Bucket:  bucketName,
       Key:     objectKey,
       Content: body,
    })
    checkErr(err)
    fmt.Println("AppendObjectV2 Request ID:", output.RequestID)

   
    res, err := http.Get("your file url")
    checkErr(err)
    defer res.Body.Close()
    if res.ContentLength > 0 {
       output, err = client.AppendObjectV2(ctx, &tos.AppendObjectV2Input{
          Bucket: bucketName,
          Key:    objectKey,
          
          PreHashCrc64ecma: output.HashCrc64ecma,
       
          Offset:        output.NextAppendOffset,
          Content:       res.Body,
          ContentLength: res.ContentLength,
       })
    }

    checkErr(err)
    fmt.Println("AppendObjectV2 Request ID:", output.RequestID)

}
```


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Configure Progress Bar**

During incremental upload, you can receive upload progress by implementing the tos.DataTransferStatusChange interface. A sample code is provided below.

```go
package main

import (
   "context"
   "fmt"
   "strings"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
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
      fmt.Printf("Event success, ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
   case enum.DataTransferFailed:
      fmt.Printf("Data Transfer Failed\n")
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
   body := strings.NewReader("your append object value")
  
 
   output, err := client.AppendObjectV2(ctx, &tos.AppendObjectV2Input{
      Bucket:               bucketName,
      Key:                  objectKey,
      Content:              body,
      DataTransferListener: &listener{},
   })
   checkErr(err)
   fmt.Println("AppendObjectV2 Request ID:", output.RequestID)

}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Throttling**

During append uploads, you can use the tos.RateLimiter interface via the client to limit the bandwidth consumed by the uploaded data. The following code demonstrates this process.

```go
package main

import (
   "context"
   "fmt"
   "strings"
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
   rateLimit1M := int64(1024 * 1024)
   body := strings.NewReader("your append object value")
  
   
   output, err := client.AppendObjectV2(ctx, &tos.AppendObjectV2Input{
      Bucket:               bucketName,
      Key:                  objectKey,
      Content:              body,
      RateLimiter:          NewDefaultRateLimit(rateLimit1M, rateLimit1M),
   })
   checkErr(err)
   fmt.Println("AppendObjectV2 Request ID:", output.RequestID)
   

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For documentation on the append upload API, refer to [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
