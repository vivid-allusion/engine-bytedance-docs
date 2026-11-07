---
title: "Multi-Version Scenarios (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenes-go-sdk"
---

<SOURCE_TEXT\>Versioning is applied to all objects within the bucket.</SOURCE_TEXT\> By enabling bucket versioning, you can restore an object to any previous version after accidental deletion or overwriting.

Currently, the interfaces that support multiple versions include GetObject, GetObjectACL, CopyObject, UploadPartCopy, DeleteObject, etc. When calling the relevant interfaces, you can specify the exact version of the target object by using the optional parameter VersionID.

<span id=".5qG25aSa54mI5pys566h55CG"></span>
## **Bucket Versioning Management**

In TOS, bucket versioning status includes three types: versioning not enabled, versioning enabled, and versioning suspended. This article introduces multi\-version management for buckets.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before configuring the bucket versioning status, you must have the <code>tos:PutBucketVersioning</code> permission.</div>


* <div data-tips="true" data-tips-type="warning">Before querying the multi\-version status of a bucket, you must have the <code>tos:GetBucketVersioning</code> permission.</div>



<span id=".6K6-572u5qG254mI5pys5o6n5Yi254q25oCB"></span>
### **Configure Bucket Versioning Status**

```go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
    "os"
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

    
    output, err := client.PutBucketVersioning(ctx, &tos.PutBucketVersioningInput{
       Bucket: bucketName,
       Status: enum.VersioningStatusEnable,
    })

    fmt.Println("PutBucketVersioning Request ID:", output.RequestID)

    
    output, err = client.PutBucketVersioning(ctx, &tos.PutBucketVersioningInput{
       Bucket: bucketName,
       Status: enum.VersioningStatusSuspended,
    })

    fmt.Println("PutBucketVersioning Request ID:", output.RequestID)

}
```


<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
### **Download Multi\-Version Objects**

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
 
   
   versionID := "your object version id"
   getOutput, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
      Bucket:    bucketName,
      Key:       objectKey,
      VersionID: versionID,
   })
   checkErr(err)
   fmt.Println("GetObjectV2 Request ID:", getOutput.RequestID)
   
   fmt.Println("GetObjectV2 Response ContentLength", getOutput.ContentLength)
   defer getOutput.Content.Close()
   body, err := ioutil.ReadAll(getOutput.Content)
   checkErr(err)
   
   fmt.Println("Get Object Content:", body)
}
```


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
### **Deleting Multi\-Version Objects**

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
      versionID = "*** Provide object Version ID"
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
      Bucket:    bucketName,
      Key:       objectKey,
      VersionID: versionID,
   })
   checkErr(err)
   fmt.Println("DeleteObjectV2 Request ID:", output.RequestID)

}
```


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
### **Emptying a versioning\-enabled bucket**

The following code is used for clearing an entire bucket with multi\-versioning enabled, including deleting all versions of objects, deleting all versions of delete markers, and deleting all unmerged objects.

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

       ctx = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    truncated := true
    marker := ""
    versionIdMarker := ""

    for truncated {
       listOutput, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
          Bucket: bucketName,
          ListObjectVersionsInput: tos.ListObjectVersionsInput{
             MaxKeys:         1000,
             KeyMarker:       marker,
             VersionIDMarker: versionIdMarker,
          },
       })
       checkErr(err)
       for _, obj := range listOutput.Versions {
          
          output, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
             Bucket:    bucketName,
             Key:       obj.Key,
             VersionID: obj.VersionID,
          })
          checkErr(err)
          fmt.Printf("Delete %s, Request ID: %s\n", obj.Key, output.RequestID)

       }
       
       for _, deleteMarker := range listOutput.DeleteMarkers {
          output, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
             Bucket:    bucketName,
             Key:       deleteMarker.Key,
             VersionID: deleteMarker.VersionID,
          })
          checkErr(err)
          fmt.Printf("Delete deleteMarker %s, Request ID: %s\n", deleteMarker.Key, output.RequestID)
       }
       truncated = listOutput.IsTruncated
       marker = listOutput.NextKeyMarker
       versionIdMarker = listOutput.NextVersionIDMarker
    }

    truncated = true
    marker = ""
    uploadIDMarker := ""
    for truncated {

       output, err := client.ListMultipartUploadsV2(ctx, &tos.ListMultipartUploadsV2Input{
          Bucket:         bucketName,
          MaxUploads:     1000,
          KeyMarker:      marker,
          UploadIDMarker: uploadIDMarker,
       })
       checkErr(err)
       for _, upload := range output.Uploads {
          abortUpload, err := client.AbortMultipartUpload(ctx, &tos.AbortMultipartUploadInput{
             Bucket:   bucketName,
             Key:      upload.Key,
             UploadID: upload.UploadID,
          })
          checkErr(err)
          fmt.Println("AbortMultipartUpload Upload ID:", upload.UploadID, " Request ID:", abortUpload.RequestID)
       }
       truncated = output.IsTruncated
       marker = output.NextKeyMarker
       uploadIDMarker = output.NextUploadIDMarker
    }

}
```
