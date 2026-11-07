---
title: "Standard Copy (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-go-sdk"
---

CopyObject enables the copying of objects between buckets within the same region, as well as within a single bucket. During copying, you may specify new metadata or retain the metadata of the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* File copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

```go
package main

import (
   "context"
   "fmt"

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
      
      bucketName    = "*** Provide your bucket name ***"
      dstBucketName = "*** Provide your dst bucket name ***"
      
      srcObjectKey = "srcObjectKey"
      dstObjectKey = "objectKey"
      ctx          = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.CopyObject(ctx, &tos.CopyObjectInput{
      Bucket:            bucketName,
      Key:               dstObjectKey,
      SrcBucket:         bucketName,
      SrcKey:            srcObjectKey,
      MetadataDirective: enum.MetadataDirectiveCopy,
   })
   checkErr(err)
   fmt.Println("CopyObject Request ID:", output.RequestID)

   
   output, err = client.CopyObject(ctx, &tos.CopyObjectInput{
      Bucket:            dstBucketName,
      Key:               dstObjectKey,
      SrcBucket:         bucketName,
      SrcKey:            srcObjectKey,
      MetadataDirective: enum.MetadataDirectiveReplace,
      
      StorageClass: enum.StorageClassIa,
      
      ACL: enum.ACLPrivate,
   })
   checkErr(err)
   fmt.Println("CopyObject Request ID:", output.RequestID)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on standard copy operations, refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
