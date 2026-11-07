---
title: "Deleting a Bucket (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-go-sdk"
---

When a bucket (Bucket) is no longer required, you may delete it to avoid incurring additional charges.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Once a bucket is deleted, it cannot be restored. Please proceed with caution.

* Before deleting a bucket, you must have the `tos:DeleteBucket` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been removed.


* If versioning is enabled for the bucket, please ensure that all current and historical version objects within the bucket have been deleted. For specific operations, refer to [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged fragments in the bucket, ensure that all fragment data is deleted. For detailed instructions, see [Deleting Fragments](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If a bucket contains a large number of objects, you can configure lifecycle rules to enable batch deletion of objects. For detailed instructions, see [Setting Lifecycle Rules](https://docs.byteplus.com/docs/6349/75028).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

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
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
 
   output, err := client.DeleteBucket(context.Background(), &tos.DeleteBucketInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("Delete Bucket Request ID: ", output.RequestID)
   fmt.Println("Delete Bucket Response Status Code: ", output.StatusCode)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For API documentation on deleting a bucket, refer to [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
