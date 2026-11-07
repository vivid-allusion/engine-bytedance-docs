---
title: "Standard Upload (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-go-sdk"
---

Standard upload refers to uploading a single object via the PutObjectV2 method. It supports four forms: uploading a string (character stream), uploading bytes (byte stream), uploading a network stream, and uploading a local file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading an object, you must have the `tos:PutObject` permission. For detailed instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific requirements. For more information, see [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To horizontally scale the maximum throughput of object uploads and downloads and reduce the likelihood of hot partitions, avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

<span id=".5LiK5Lyg5a2X56ym5Liy"></span>
### **Upload String**

You can use the following sample code and the PutObjectV2 interface to upload string data to the `example.txt` file under the `example_dir` directory specified in TOS.

```go
package main

import (
   "context"
   "fmt"
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
  
   body := strings.NewReader("Hello TOS")
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5LiK5Lyg572R57uc5rWB"></span>
### **Upload Network Stream**

You can use the following example code to upload network stream data to the `example.txt` file in the `example_dir` directory under TOS using the PutObjectV2 API.

```go
package main

import (
   "context"
   "fmt"
   "net/http"

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
   
   res, _ := http.Get("https://www.byteplus.com/en/")
   defer res.Body.Close()
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      Content: res.Body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu25rWB"></span>
### **Upload Local File Stream**

You can use the following sample code and the PutObjectV2 interface to upload a file from a specified path to the `example_dir` directory in TOS as `example.txt`.

```go
package main

import (
   "context"
   "fmt"
   "os"

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
      fileName = "/usr/local/test.txt"
      ctx       = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   f, err := os.Open("./example.txt")
   if err != nil {
      panic(err)
   }
   defer f.Close()
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      Content: f,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5LuO5pys5Zyw5paH5Lu25LiK5Lyg"></span>
### **Upload from local file**

You can use the following sample code. It uses the PutObjectFromFile API to upload a file to `example_dir`/`example.txt` in TOS by specifying the file path.

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
      region   = "your regionn"
   
      bucketName = "*** Provide your bucket name ***"


      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   output, err := client.PutObjectFromFile(ctx, &tos.PutObjectFromFileInput{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      FilePath: "./example.txt",
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5LiK5Lyg5pe26K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### **Configuring object metadata information during upload**

You can use the following sample code to upload string data to the `example_dir` directory's `example.txt` file via the PutObjectV2 API. During upload, specify the object storage type as infrequent access, set the permission to private, and configure the file metadata.

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

   body := strings.NewReader("Hello TOS")
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,

         StorageClass: enum.StorageClassIa,

         ACL: enum.ACLPrivate,
 
         Meta: map[string]string{"key": "value"},
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Configuring the Progress Bar**

During upload, you can receive progress updates by implementing the tos.DataTransferStatusChange interface. A sample code is shown below.

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
      fmt.Printf("Data Transfer Succeed, ConsumerBytes/TotalBytes: %d/%d,%d%%\n", event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
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

   body := strings.NewReader("Hello TOS")
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
 
         DataTransferListener: &listener{},
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configuring Client Bandwidth Throttling**

When uploading objects, you can use the tos.RateLimiter interface on the client side to limit the bandwidth consumed by the upload data. The sample code is shown below.

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
   body := strings.NewReader("Hello TOS")
   rateLimit1M := 1024 * 1024

   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket:      bucketName,
         Key:         objectKey,
         RateLimiter: NewDefaultRateLimit(int64(rateLimit1M), int64(rateLimit1M)),
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on uploading objects, refer to [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
