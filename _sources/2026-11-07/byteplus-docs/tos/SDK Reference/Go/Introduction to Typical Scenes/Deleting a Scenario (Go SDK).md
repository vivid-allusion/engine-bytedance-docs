---
title: "Deleting a Scenario (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-scenes-go-sdk"
---

This article introduces code examples for common object deletion scenarios.

<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete Directory**

The following code is used to delete objects under the directory `exampledir`.

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
         if serverErr.StatusCode == http.StatusNotFound {
            return
         }
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
   continuationToken := ""
   prefix := "exampledir/"

   for truncated {

      output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
         Bucket:            bucketName,
         MaxKeys:           1000,
         ContinuationToken: continuationToken,
         Prefix:            prefix,
      })
      checkErr(err)
      for _, obj := range output.Contents {
         deleteOutput, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
            Bucket: bucketName,
            Key:    obj.Key,
         })
         checkErr(err)
         fmt.Println("DeleteObjectV2 Request ID:", deleteOutput.RequestID)
      }
      truncated = output.IsTruncated
      continuationToken = output.NextContinuationToken
   }

}
```


<span id=".5riF56m65qG2"></span>
## **Empty Bucket**

The following code is used to clear the entire bucket, including deleting all objects and all unmerged objects.

```go
package main

import (
    "context"
    "fmt"
    "net/http"
    "os"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
    if err != nil {
       if serverErr, ok := err.(*tos.TosServerError); ok {
          if serverErr.StatusCode == http.StatusNotFound {
             return
          }
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
    continuationToken := ""
    for truncated {

       output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
          Bucket:            bucketName,
          MaxKeys:           1000,
          ContinuationToken: continuationToken,
       })
       checkErr(err)
       for _, obj := range output.Contents {
          deleteOutput, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
             Bucket: bucketName,
             Key:    obj.Key,
          })
          checkErr(err)
          fmt.Println("DeleteObjectV2 Request ID:", deleteOutput.RequestID)
       }
       truncated = output.IsTruncated
       continuationToken = output.NextContinuationToken
    }

   
    truncated = true
    marker := ""
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


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## **Emptying a bucket with versioning enabled**

The following code provides an example for clearing an entire multi\-version enabled bucket, including deleting all versions of all objects, deleting all versions of delete markers, and deleting all unmerged objects.

```go
package main

import (
    "context"
    "fmt"
    "net/http"
    "os"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
    if err != nil {
       if serverErr, ok := err.(*tos.TosServerError); ok {
          if serverErr.StatusCode == http.StatusNotFound {
             return
          }
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
