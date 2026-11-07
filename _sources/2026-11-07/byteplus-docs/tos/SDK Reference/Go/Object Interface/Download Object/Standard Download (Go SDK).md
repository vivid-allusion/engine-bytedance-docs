---
title: "Standard Download (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-go-sdk"
---

The GetObject method enables downloading objects from a specified bucket. Before using this interface, ensure that you have read access to the object. During the use of the download interface, the current progress of downloaded data can be obtained by configuring a progress bar callback. To implement client\-side rate limiting during downloads, use the tos.RateLimiter interface. Additionally, you can configure the download process to return metadata information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object multiple times simultaneously, your access speed will be limited by TOS bandwidth and geographic restrictions. It is recommended that you use CDN products to enhance performance while simultaneously reducing your costs. For detailed information on accessing TOS via CDN, see [Using CDN to Accelerate Access to TOS Resources](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiL6L295pWw5o2u5Yiw5YaF5a2Y"></span>
### **Download data into memory**

The following code downloads objects from the bucket into memory.

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"
   "sync"
   "time"

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
   rateLimit1m := int64(1024 * 1024)
   
   getOutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   
      DataTransferListener: &listener{},
     
      RateLimiter: NewDefaultRateLimit(rateLimit1m, rateLimit1m),
   
      ResponseContentType:     "application/json",
      ResponseContentEncoding: "deflate",
   })
   checkErr(err)
   fmt.Println("GetObjectV2 Request ID:", getOutput.RequestID)

   fmt.Println("GetObjectV2 Response ContentType:", getOutput.ContentType)

   fmt.Println("GetObjectV2 Response ContentEncoding:", getOutput.ContentEncoding)

   fmt.Println("GetObjectV2 Response ContentLength", getOutput.ContentLength)
   defer getOutput.Content.Close()
   body, err := ioutil.ReadAll(getOutput.Content)
   checkErr(err)

   fmt.Println("Get Object Content:", body)
}
```


<span id=".5LiL6L295pWw5o2u5Yiw5pys5Zyw5paH5Lu2"></span>
### **Download data to a local file**

Download data from TOS to the specified local file path.

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

   
   getObjectToFileOutput, err := client.GetObjectToFile(ctx, &tos.GetObjectToFileInput{
      GetObjectV2Input: tos.GetObjectV2Input{
         Bucket: bucketName,
         Key:    objectKey,
      },
      FilePath: "example_dir/example.txt",
   })
   checkErr(err)
   fmt.Println("GetObjectToFile Request ID:", getObjectToFileOutput.RequestID)
   fmt.Println("GetObjectToFile File Size:", getObjectToFileOutput.ContentLength)
}
```


<span id=".5LiL6L295pe26YeN5YaZLWh0dHAt5ZON5bqU5aS0"></span>
### **Rewrite HTTP Response Headers During Download**

The following code is used to download the object 'object\-test' from the bucket and to rewrite the HTTP response headers.

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"

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
   
   getOutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
      
      ResponseContentType:     "application/json",
      ResponseContentEncoding: "deflate",
   })
   checkErr(err)
   fmt.Println("GetObjectV2 Request ID:", getOutput.RequestID)
   
   fmt.Println("GetObjectV2 Response ContentType:", getOutput.ContentType)
   
   fmt.Println("GetObjectV2 Response ContentEncoding:", getOutput.ContentEncoding)
   
   fmt.Println("GetObjectV2 Response ContentLength", getOutput.ContentLength)
   defer getOutput.Content.Close()
   body, err := ioutil.ReadAll(getOutput.Content)
   checkErr(err)
   
   fmt.Println("Get Object Content:", body)
}
```


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Progress Bar Configuration**

During downloading, you can receive download progress by implementing the tos.DataTransferStatusChange interface. A code example is provided below.

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"

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
   
   getOutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
      
      DataTransferListener: &listener{},
   })
   checkErr(err)
   fmt.Println("GetObjectV2 Request ID:", getOutput.RequestID)
   
   fmt.Println("GetObjectV2 Response ContentType:", getOutput.ContentType)
   
   fmt.Println("GetObjectV2 Response ContentEncoding:", getOutput.ContentEncoding)
  
   fmt.Println("GetObjectV2 Response ContentLength", getOutput.ContentLength)
   defer getOutput.Content.Close()
   body, err := ioutil.ReadAll(getOutput.Content)
   checkErr(err)
   
   fmt.Println("Get Object Content:", body)
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Limitation**

When downloading objects, you can use the tos.RateLimiter interface on the client side to restrict the bandwidth consumed by the downloaded data. The following code demonstrates this.

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"
   "sync"
   "time"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

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
   rateLimit1m := int64(1024 * 1024)
   
   getOutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
     
      RateLimiter: NewDefaultRateLimit(rateLimit1m, rateLimit1m),
   })
   checkErr(err)
   fmt.Println("GetObjectV2 Request ID:", getOutput.RequestID)
  
   fmt.Println("GetObjectV2 Response ContentType:", getOutput.ContentType)
   
   fmt.Println("GetObjectV2 Response ContentEncoding:", getOutput.ContentEncoding)
   
   fmt.Println("GetObjectV2 Response ContentLength", getOutput.ContentLength)
   defer getOutput.Content.Close()
   body, err := ioutil.ReadAll(getOutput.Content)
   checkErr(err)
   
   fmt.Println("Get Object Content:", body)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
