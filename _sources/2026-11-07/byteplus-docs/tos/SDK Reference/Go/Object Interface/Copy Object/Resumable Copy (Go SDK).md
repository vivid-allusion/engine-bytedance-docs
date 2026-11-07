---
title: "Resumable Copy (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-copy-go-sdk"
---

Using the TOS Go SDK, resumable copy is suitable for scenarios where large objects are copied within a single bucket or between two buckets in the same region. The TOS Go SDK provides a resumable copy feature. By utilizing a local CheckPoint mechanism to record successfully copied segments, the SDK enables interrupted segment copy operations—caused by network failures or machine malfunctions—to be resumed by invoking the same interface again. Resumable copy divides the object to be copied into multiple segments and supports concurrent copying. After all segments have been copied, they are merged into a complete file. You can configure parameters such as the segment size for resumable copy, the number of threads for copying segments, and event callback functions. It is also possible to cancel the task during the execution of the breakpoint resume copy task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Copying files does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you may retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5pat54K557ut5Lyg5ou36LSd"></span>
## **Resumable Copy**

The following code implements resumable copy of the `srcBucketName` bucket's `srcObjectKey` object to the `dstBucketName` bucket, sets the object name to `dstObjectKey`, and supports retrying download upon failure. If a network timeout error is returned during the copy process, invoke ResumableCopyObject with the same parameters to resume the copy operation from the breakpoint.

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
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      
      endpoint = "your endpoint"
      region   = "your region"
    
      srcBucketName = "*** Provide your src bucket name ***"
      dstBucketName = "*** Provide your dst bucket name ***"

      srcObjectKey       = "srcObjectKey"
      dstObjectKey       = "dstObjectKey"
      checkPointFilePath = "./example.checkpoint"
      ctx                = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   input := &tos.ResumableCopyObjectInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: dstBucketName,
         Key:    dstObjectKey,
      },
      SrcBucket:        srcBucketName,
      SrcKey:           srcObjectKey,
      PartSize:         20 * 1024 * 1024,
      TaskNum:          3,
      EnableCheckpoint: true,
      CheckpointFile:   checkPointFilePath,
   }
   output, err := client.ResumableCopyObject(ctx, input)
   checkErr(err)
   
   fmt.Println("ResumableCopyObject Request Bucket:", output.Bucket)
   fmt.Println("ResumableCopyObject Request Key:", output.Key)
   fmt.Println("ResumableCopyObject Request UploadID:", output.UploadID)
   fmt.Println("ResumableCopyObject Request Etag:", output.Etag)
   fmt.Println("ResumableCopyObject Request Location:", output.Location)
   fmt.Println("ResumableCopyObject Request VersionID:", output.VersionID)
   fmt.Println("ResumableCopyObject Request HashCrc64ecma:", output.HashCrc64ecma)
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
## **Handling Event Callbacks**

The following code is used to define a custom resumable copy callback function.

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

func (e eventChange) EventChange(event *tos.CopyEvent) {
   switch event.Type {
   case enum.CopyEventCreateMultipartUploadSucceed:
      fmt.Println("Resume Create Multipart Upload Success.\n ")
   case enum.CopyEventCreateMultipartUploadFailed:
      fmt.Println("Resume Create Multipart Upload Fail.\n ")
   case enum.CopyEventUploadPartCopySuccess:
      fmt.Printf("Copy %s %s part success, CopyPartInfo:%v\n", event.Bucket, event.Key, event.CopyPartInfo)
   case enum.CopyEventUploadPartCopyFailed:
      fmt.Printf("Copy %s %s part aborted.\n", event.Bucket, event.Key)
   case enum.CopyEventUploadPartCopyAborted:
      fmt.Printf("Copy %s %s part fail, err:%v\n", event.Bucket, event.Key, event.Err)
   case enum.CopyEventCompleteMultipartUploadSucceed:
      fmt.Printf("Copy %s %s success.\n", event.Bucket, event.Key)
   case enum.CopyEventCompleteMultipartUploadFailed:
      fmt.Printf("Copy %s %s fail,err:%v\n", event.Bucket, event.Key, event.Err)

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
      srcBucketName = "*** Provide your src bucket name ***"
      dstBucketName = "*** Provide your dst bucket name ***"

      srcObjectKey       = "srcObjectKey"
      dstObjectKey       = "dstObjectKey"
      checkPointFilePath = "./example.checkpoint"
      ctx                = context.Background()
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   input := &tos.ResumableCopyObjectInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: dstBucketName,
         Key:    dstObjectKey,
      },
      SrcBucket:         srcBucketName,
      SrcKey:            srcObjectKey,
      PartSize:          20 * 1024 * 1024,
      TaskNum:           3,
      EnableCheckpoint:  true,
      CheckpointFile:    checkPointFilePath,
      CopyEventListener: eventChange{},
   }
   output, err := client.ResumableCopyObject(ctx, input)
   checkErr(err)
   fmt.Println("ResumableCopyObject Request Bucket:", output.Bucket)
   fmt.Println("ResumableCopyObject Request Key:", output.Key)
   fmt.Println("ResumableCopyObject Request UploadID:", output.UploadID)
   fmt.Println("ResumableCopyObject Request Etag:", output.Etag)
   fmt.Println("ResumableCopyObject Request Location:", output.Location)
   fmt.Println("ResumableCopyObject Request VersionID:", output.VersionID)
   fmt.Println("ResumableCopyObject Request HashCrc64ecma:", output.HashCrc64ecma)
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
## **Cancellation Mechanism**

The following code is used to pause or cancel a resumable copy task.

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
      accessKey = os.Getenv("TOS_ACCESS_KEY")
      secretKey = os.Getenv("TOS_SECRET_KEY")
      endpoint = "your endpoint"
      region   = "your region"
      srcBucketName = "*** Provide your src bucket name ***"
      dstBucketName = "*** Provide your dst bucket name ***"

      srcObjectKey       = "srcObjectKey"
      dstObjectKey       = "dstObjectKey"
      checkPointFilePath = "./example.checkpoint"
      ctx                = context.Background()
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   cancel := tos.NewCancelHook()
   input := &tos.ResumableCopyObjectInput{
      CreateMultipartUploadV2Input: tos.CreateMultipartUploadV2Input{
         Bucket: dstBucketName,
         Key:    dstObjectKey,
      },
      SrcBucket:        srcBucketName,
      SrcKey:           srcObjectKey,
      PartSize:         20 * 1024 * 1024,
      TaskNum:          3,
      EnableCheckpoint: true,
      CheckpointFile:   checkPointFilePath,
      CancelHook:       cancel,
   }
   output, err := client.ResumableCopyObject(ctx, input)
   checkErr(err)
   fmt.Println("ResumableCopyObject Request Bucket:", output.Bucket)
   fmt.Println("ResumableCopyObject Request Key:", output.Key)
   fmt.Println("ResumableCopyObject Request UploadID:", output.UploadID)
   fmt.Println("ResumableCopyObject Request Etag:", output.Etag)
   fmt.Println("ResumableCopyObject Request Location:", output.Location)
   fmt.Println("ResumableCopyObject Request VersionID:", output.VersionID)
   fmt.Println("ResumableCopyObject Request HashCrc64ecma:", output.HashCrc64ecma)
}
```
