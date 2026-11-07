---
title: "Multipart Copy (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-go-sdk"
---

When the object size exceeds 5 GiB, UploadPartCopyV2 must be used to perform multipart copy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* File copying does not support cross\-region bucket\-to\-bucket copying.

* When copying objects, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can either retain all metadata (the default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Sharded Copy Procedure


1. Initialize the multipart copy task via CreateMultipartUploadV2.

2. Segmented copying is performed via UploadPartCopyV2.

3. Merge parts using CompleteMultipartUploadV2.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

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
      
      srcBucketName = "*** Provide your bucket name ***"
      dstBucketName = "*** Provide your dst bucket name ***"
     
      srcObjectKey = "srcObjectKey"
      dstObjectKey = "objectKey"
      ctx          = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   headOutput, err := client.HeadObjectV2(ctx, &tos.HeadObjectV2Input{
      Bucket: srcBucketName,
      Key:    srcObjectKey,
   })
   checkErr(err)
   totalSize := headOutput.ContentLength
   partSize := tos.DefaultPartSize
   createMultiOutput, err := client.CreateMultipartUploadV2(ctx, &tos.CreateMultipartUploadV2Input{
      Bucket: dstBucketName,
      Key:    dstObjectKey,
   })
   checkErr(err)
   uploadId := createMultiOutput.UploadID
   parts := make([]tos.UploadedPartV2, 0)
   partNumber := 1
   offset := int64(0)
   for offset < totalSize {
      numToUpload := partSize
      end := offset + int64(numToUpload) - 1
      output, err := client.UploadPartCopyV2(ctx, &tos.UploadPartCopyV2Input{
         Bucket:               dstBucketName,
         Key:                  dstObjectKey,
         UploadID:             uploadId,
         PartNumber:           partNumber,
         SrcBucket:            srcBucketName,
         SrcKey:               srcObjectKey,
         CopySourceRangeStart: offset,
         CopySourceRangeEnd:   end,
      })
      checkErr(err)
      fmt.Println("UploadPartCopyV2 Request ID:", output.RequestID)
      parts = append(parts, tos.UploadedPartV2{
         PartNumber: output.PartNumber,
         ETag:       output.ETag,
      })
      offset += int64(numToUpload)
      partNumber++

   }
   completeOutput, err := client.CompleteMultipartUploadV2(ctx, &tos.CompleteMultipartUploadV2Input{
      Bucket:   dstBucketName,
      Key:      dstObjectKey,
      UploadID: uploadId,
      Parts:    parts,
   })
   checkErr(err)
   fmt.Println("CompleteMultipartUploadV2 Request ID:", completeOutput.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related Documents**


* For the API documentation on creating a multipart upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on multipart copy, refer to [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on merging parts, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
