---
title: "Move and Rename Scenarios (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-go-sdk"
---

If you need to rename a file within a Bucket, you can use the CopyObject interface to copy the source object to the target object, and then use the DeleteObject interface to delete the source object.

<span id=".6YeN5ZG95ZCN5Y2V5Liq5a-56LGh"></span>
## **Rename a single object**

The following code is used to rename the object `src-object` in the bucket to `dest-object`.

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
   srcObjectKey := "src-object"
   dstObjectKey := "dest-object"
   
   output, err := client.CopyObject(ctx, &tos.CopyObjectInput{
      Bucket:    bucketName,
      Key:       dstObjectKey,
      SrcBucket: bucketName,
      SrcKey:    srcObjectKey,
   })
   checkErr(err)
   fmt.Println("CopyObject Request ID:", output.RequestID)
   
   deleteOutput, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
      Bucket: bucketName,
      Key:    srcObjectKey,
   })
   checkErr(err)
   fmt.Println("DeleteObjectV2 Request ID:", deleteOutput.RequestID)
}
```


<span id=".6YeN5ZG95ZCN55uu5b2V"></span>
## **Rename Directory**

The following code is used to rename the directory `exampledir1/` to `exampledir2/` within the specified storage bucket.

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
   oldPrefix := "exampledir1/"
   newPrefix := "exampledir2/"

   for truncated {

      output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
         Bucket:            bucketName,
         MaxKeys:           1000,
         ContinuationToken: continuationToken,
         Prefix:            oldPrefix,
      })
      checkErr(err)
      for _, obj := range output.Contents {
         
         newKey := strings.Replace(obj.Key, oldPrefix, newPrefix, 1)
         output, err := client.CopyObject(ctx, &tos.CopyObjectInput{
            Bucket:    bucketName,
            Key:       newKey,
            SrcBucket: bucketName,
            SrcKey:    obj.Key,
         })
         checkErr(err)
         fmt.Println("CopyObject Request ID:", output.RequestID)
        
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
