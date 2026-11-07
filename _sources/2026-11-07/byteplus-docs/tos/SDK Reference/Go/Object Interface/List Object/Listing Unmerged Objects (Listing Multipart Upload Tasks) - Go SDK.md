---
title: "Listing Unmerged Objects (Listing Multipart Upload Tasks) - Go SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmergedobjects-go-sdk"
---

This interface is used to list unmerged objects within a bucket, that is, to enumerate multipart upload tasks.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**

Before listing multipart upload tasks, you must have the `tos:ListBucketMultipartUploads` permission. For detailed instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|Delimiter |Character used to group object names. |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |
|MaxUploads |Returns the maximum number of multipart upload tasks. The default value is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |
|Prefix |Used to specify the prefix name for enumerating returned objects. |
|KeyMarker |List the starting positions of multipart upload tasks. Set to return a list of objects sorted alphabetically, starting after this value. This is typically the value of NextKeyMarker returned by the previous request. |
|UploadIDMarker |Used in conjunction with keyMarker, this parameter specifies that the list of multipart upload tasks will be returned in lexicographical order, starting from the value immediately following the specified keyMarker. Obtain NextUploadIDMarker from the results of the previous listing. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **A brief enumeration**

The following code is used to list up to 10 unmerged multipart upload tasks in the specified storage bucket.

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

      ctx = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   
   output, err := client.ListMultipartUploadsV2(ctx, &tos.ListMultipartUploadsV2Input{
      Bucket:     bucketName,
      MaxUploads: 10,
   })
   checkErr(err)
   for _, upload := range output.Uploads {
      fmt.Println("Object Key:", upload.Key)
      fmt.Println("UploadID:", upload.UploadID)
      fmt.Println("Owner:", upload.Owner)
      fmt.Println("StorageClass:", upload.StorageClass)
   }

}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### **List all unmerged shard tasks with the specified prefix.** 

The following code is used to list all unmerged multipart upload tasks under the specified prefix in the designated storage bucket.

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
       prefix     = "*** Provide your object key prefix ***"

       ctx = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    truncated := true
    marker := ""
    uploadIdMarker := ""
    for truncated {

       output, err := client.ListMultipartUploadsV2(ctx, &tos.ListMultipartUploadsV2Input{
          Bucket:         bucketName,
          MaxUploads:     1000,
          KeyMarker:      marker,
          Prefix:         prefix,
          UploadIDMarker: uploadIdMarker,
       })
       checkErr(err)
       for _, upload := range output.Uploads {
          fmt.Println("Object Key:", upload.Key)
          fmt.Println("UploadID:", upload.UploadID)
          fmt.Println("Owner:", upload.Owner)
          fmt.Println("StorageClass:", upload.StorageClass)
       }
       truncated = output.IsTruncated
       marker = output.NextKeyMarker
       uploadIdMarker = output.NextUploadIDMarker
    }
}
```


<span id=".5YiX5Li-5omA5pyJ5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### **List all multipart upload tasks**

The following code is used to list all unmerged multipart upload tasks for the specified storage bucket.

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
       } else {
          fmt.Println("Error:", err)
       }
       panic(err)
    }
}

func main() {
    var (
       accessKey = "*** Provide your access key ***"
       secretKey = "*** Provide your secret key ***"
     
       endpoint = "your endpoint"
       region   = "your region"
      
       bucketName = "*** Provide your bucket name ***"

       ctx = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

   
    truncated := true
    marker := ""
    uploadIdMarker := ""
    for truncated {

       output, err := client.ListMultipartUploadsV2(ctx, &tos.ListMultipartUploadsV2Input{
          Bucket:         bucketName,
          MaxUploads:     1000,
          KeyMarker:      marker,
          UploadIDMarker: uploadIdMarker,
       })
       checkErr(err)
       for _, upload := range output.Uploads {
          fmt.Println("Object Key:", upload.Key)
          fmt.Println("UploadID:", upload.UploadID)
          fmt.Println("Owner:", upload.Owner)
          fmt.Println("StorageClass:", upload.StorageClass)
       }
       truncated = output.IsTruncated
       marker = output.NextKeyMarker
       uploadIdMarker = output.UploadIDMarker
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For documentation on the API for listing multipart uploads, see [ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads).
