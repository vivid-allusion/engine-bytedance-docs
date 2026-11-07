---
title: "Object Metadata Management (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-go-sdk"
---

Object metadata refers to the attribute descriptions of an object, comprising both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Only the object owner has permission to set object metadata.

* When configuring user\-defined metadata, the metadata Key using English letters supports only lowercase characters and does not allow spaces or other special characters.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description

Using the TOS Go SDK, you can add and modify metadata for objects that have already been uploaded. TOS supports carrying the following seven request headers to modify object metadata. When downloading an object or performing a HEAD request, these values are set in the HTTP header and returned to the client. The request header is as follows:


|Name |Description |
|---|---|
|Content\-Type |Object Type |
|Cache\-Control |Specify the web page caching behavior when this object is downloaded. |
|Expires |Cache expiration time as defined in RFC2616 |
|Content\-Disposition |Name assigned to the object upon download |
|Content\-Encoding |Content encoding type when the object is downloaded |
|Content\-Language |Content language format of the object upon download |
|x\-tos\-meta\-\* |The metadata information set when using the SDK to set the Meta field. When this object is queried, the metadata will be included in the Header of the response message. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### **Setting Metadata Information During Standard Upload**

```go
package main

import (
   "context"
   "fmt"
   "strings"
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
         
         Meta: map[string]string{"key": "value"},
         
         ContentType: "text/html",
         
         ContentLanguage: "zh-cn",
         
         CacheControl: "no-store",
         
         Expires: time.Now().UTC().Add(time.Hour),
         
         ContentDisposition: "example.png",
        
         ContentEncoding: "deflate",
      },
      Content: body,
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5YiG54mH5LiK5Lyg6K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### **Configuring Metadata Information for Multipart Uploads**

```go
package main

import (
   "context"
   "fmt"
   "strings"
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
   
   output, err := client.CreateMultipartUploadV2(ctx, &tos.CreateMultipartUploadV2Input{

      Bucket: bucketName,
      Key:    objectKey,
      
      Meta: map[string]string{"key": "value"},
      
      ContentType: "text/html",
      
      ContentLanguage: "zh-cn",
      
      CacheControl: "no-store",
      
      Expires: time.Now().UTC().Add(time.Hour),
      
      ContentDisposition: "example.png",
     
      ContentEncoding: "deflate",
   })
   checkErr(err)
   fmt.Println("CreateMultipartUploadV2 Request ID:", output.RequestID)
   fmt.Println("CreateMultipartUploadV2 Upload ID:", output.UploadID)

   
   part, err := client.UploadPartV2(ctx, &tos.UploadPartV2Input{
      UploadPartBasicInput: tos.UploadPartBasicInput{
         Bucket:     bucketName,
         Key:        objectKey,
         UploadID:   output.UploadID,
         PartNumber: 1,
      },
      Content: strings.NewReader("your body data"),
   })
   checkErr(err)
   fmt.Println("UploadPartV2 Request ID:", part.RequestID)

   
   completeMultipartOutput, err := client.CompleteMultipartUploadV2(ctx, &tos.CompleteMultipartUploadV2Input{
      Bucket:   bucketName,
      Key:      objectKey,
      UploadID: output.UploadID,
      Parts: []tos.UploadedPartV2{{
         PartNumber: part.PartNumber,
         ETag:       part.ETag,
      }},
   })
   checkErr(err)
   fmt.Println("CompleteMultipartUploadV2 Request ID:", completeMultipartOutput.RequestID)
}
```


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt6K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### **Set object metadata information using SetObjectMeta.** 

```go
package main

import (
   "context"
   "fmt"
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

   
   output, err := client.SetObjectMeta(ctx, &tos.SetObjectMetaInput{
      Bucket: bucketName,
      Key:    objectKey,
      
      Meta: map[string]string{"key": "value"},
      
      ContentType: "text/html",
      
      ContentLanguage: "zh-cn",
     
      CacheControl: "no-store",
      
      Expires: time.Now().UTC().Add(time.Hour),
      
      ContentDisposition: "example.png",
      
      ContentEncoding: "deflate",
   })
   checkErr(err)
   fmt.Println("SetObjectMeta Request ID:", output.RequestID)
}
```


<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u5L-h5oGv77yI5Yik5pat5a-56LGh5piv5ZCm5a2Y5Zyo77yJ"></span>
### **Query Object Metadata Information (Determine Whether the Object Exists)** 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining object metadata, you must have the <code>tos:GetObject</code> permission. For detailed instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


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
   output, err := client.HeadObjectV2(ctx, &tos.HeadObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         
         if serverErr.StatusCode == http.StatusNotFound {
            fmt.Println("Object not found.")
         } else {
            fmt.Println("Error:", serverErr.Error())
            fmt.Println("Request ID:", serverErr.RequestID)
            fmt.Println("Response Status Code:", serverErr.StatusCode)
            fmt.Println("Response Header:", serverErr.Header)
            fmt.Println("Response Err Code:", serverErr.Code)
            fmt.Println("Response Err Msg:", serverErr.Message)
            panic(err)
         }
      } else {
         panic(err)
      }
   }
   fmt.Println("HeadObjectV2 Request ID:", output.RequestID)
   
   fmt.Println("HeadObjectV2 Response ContentLanguage:", output.ContentLanguage)
  
   fmt.Println("HeadObjectV2 Response ContentDisposition:", output.ContentDisposition)
   
   fmt.Println("HeadObjectV2 Response ContentEncoding:", output.ContentEncoding)

   fmt.Println("HeadObjectV2 Response CacheControl:", output.CacheControl)

   fmt.Println("HeadObjectV2 Response ContentType:", output.ContentType)

   fmt.Println("HeadObjectV2 Response Expires:", output.Expires)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For API documentation on setting object metadata, refer to [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
