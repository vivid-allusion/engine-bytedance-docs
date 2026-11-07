---
title: "Quick Start (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-go-sdk"
---

This article describes how to perform common operations using the TOS Go SDK, such as creating buckets and uploading, downloading, and deleting objects, etc.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install the SDK](https://docs.byteplus.com/docs/tos/Install-the-go-sdk)

2. [Initialize Client](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-go-sdk)


<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## General Client Example

A general example of using TosClient is provided below.

```go
package main

import (
   "context"
   "fmt"
   "strings"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

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
   if err != nil {
      panic(err)
   }
   
   body := strings.NewReader("Hello TOS")
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      Content: body,
   })
   
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
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5Yib5bu65qG2"></span>
## Create Bucket

A storage bucket (Bucket) in TOS is a globally unique namespace that serves as a container for data and is used to store object data. The following code demonstrates how to use the CreateBucket method to create a new storage bucket.

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
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   resp, err := client.CreateBucketV2(context.Background(), &tos.CreateBucketV2Input{
      Bucket: bucketName,
   })
   checkErr(err)
   fmt.Println("create bucket request id: ", resp.RequestID)
   fmt.Println("create bucket response status code: ", resp.StatusCode)
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about creating buckets, see <a href="https://docs.byteplus.com/docs/tos/Create-a-bucket-go-sdk">Create Bucket</a>.</div>


<span id=".5LiK5Lyg5a-56LGh"></span>
## Upload Object

After a storage bucket is successfully created, objects can be uploaded to the bucket. The following code uploads a string to a TOS bucket.

```go
package main

import (
   "context"
   "fmt"
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
      
      objectKey = "*** Provide your object key ***"
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   
   body := strings.NewReader("object content")
  
   output, err := client.PutObjectV2(context.Background(), &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{
         Bucket: bucketName,
         Key:    objectKey,
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("Put Object Request ID: ", output.RequestID)
   fmt.Println("Put Object Response Status Code: ", output.StatusCode)
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links related to uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Upload-object-overview-go-sdk">Uploading Objects</a>.</div>


<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following demonstrates how to download an object from a storage bucket into memory.

```go
package main

import (
   "context"
   "fmt"
   "io/ioutil"
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
      
      objectKey = "*** Provide your object key ***"
   )
 
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

  
   output, err := client.GetObjectV2(context.Background(), &tos.GetObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   checkErr(err)
   defer output.Content.Close()
   fmt.Println("Get object request id: ", output.RequestID)
   fmt.Println("Get object response status code: ", output.StatusCode)
   body, err := ioutil.ReadAll(output.Content)
   checkErr(err)
   fmt.Println("Get Object body: ", body)
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links related to downloading objects, see <a href="https://docs.byteplus.com/docs/tos/Download-object-overview-go-sdk">Download Objects</a>.</div>


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumeration of Objects

The following displays the objects that have already been uploaded to the storage bucket.

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
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   output, err := client.ListObjectsV2(context.Background(), &tos.ListObjectsV2Input{
      Bucket: bucketName,
   })
   checkErr(err)
   fmt.Println("List Object Request Id:", output.RequestID)
   
   if !output.IsTruncated {
      output, err = client.ListObjectsV2(context.Background(), &tos.ListObjectsV2Input{
         Bucket:           bucketName,
         ListObjectsInput: tos.ListObjectsInput{Marker: output.NextMarker},
      })
      checkErr(err)
      fmt.Println("List Object Request Id:", output.RequestID)
   }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links on object listing, please refer to <a href="https://docs.byteplus.com/docs/tos/List-objects-go-sdk">Object Listing</a>.</div>


<span id=".5Yig6Zmk5a-56LGh"></span>
## Delete Object

The following code demonstrates how to delete an object from a storage bucket.

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
    
      objectKey = "*** Provide your object key ***"
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

  
   output, err := client.DeleteObjectV2(context.Background(), &tos.DeleteObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   checkErr(err)
   fmt.Println("Delete object request id: ", output.RequestID)
   fmt.Println("Delete object response status code: ", output.StatusCode)
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links on deleting objects, please see <a href="https://docs.byteplus.com/docs/tos/Delete-objects-go-sdk">Delete Object</a>.</div>


<span id=".5YWz6ZetLWNsaWVudA=="></span>
## Close Client

The TOS Go SDK enables persistent connections by default. After creating a Client instance to access TOS, you can use the following code to close Client instances that are no longer in use and release connection resources.

```go
package main

import (
   "context"
   "fmt"
   "strings"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func main() {
   var (
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"

   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   if err != nil {
      panic(err)
   }

   client.Close()
}
```
