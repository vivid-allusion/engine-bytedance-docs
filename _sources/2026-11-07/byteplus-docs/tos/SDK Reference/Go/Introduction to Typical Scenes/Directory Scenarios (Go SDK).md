---
title: "Directory Scenarios (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Directory-scenes-go-sdk"
---

TOS implements only the concept of objects and stores data using a flat structure. To facilitate object grouping and streamline permission management, you can organize objects using a directory hierarchy.

<span id=".5Yib5bu655uu5b2V"></span>
## **Creating a Table of Contents**

```go
package main

import (
   "bytes"
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

   
   key := "exampledir/"
   output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{Bucket: bucketName, Key: key},
      Content:             bytes.NewReader([]byte("")),
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
   
   key = "exampledir/test/"
   output, err = client.PutObjectV2(ctx, &tos.PutObjectV2Input{
      PutObjectBasicInput: tos.PutObjectBasicInput{Bucket: bucketName, Key: key},
      Content:             bytes.NewReader([]byte("")),
   })
   checkErr(err)
   fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## **Simulated Directory Query**

TOS supports only the concept of objects; it is possible to create an object with a size of 0 whose name ends with a slash.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the two parameters `Delimiter` and `Prefix`:


* First, set `Delimiter` to`/`When `Prefix` is also set to empty, information about objects and subdirectories in the root directory can be returned.

* When setting `Delimiter` to`/`By simultaneously setting `Prefix` to a subdirectory (subfiledir), objects and subdirectories within that subdirectory can be returned.


The following code enumerates the objects and subdirectories in the root directory.

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
   
   truncated := true
   continuationToken := ""
   for truncated {
      output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
         Bucket:            bucketName,
         MaxKeys:           1000,
         ContinuationToken: continuationToken,
         Delimiter:         "/",
      })
      checkErr(err)
      
      for _, prefix := range output.CommonPrefixes {
         fmt.Println("Sub Dir:", prefix.Prefix)
      }
      
      for _, obj := range output.Contents {
         fmt.Println("Obj:", obj.Key)
      }
      truncated = output.IsTruncated
      continuationToken = output.NextContinuationToken
   }

}
```


<span id=".5Yig6Zmk55uu5b2V5LiL55qE5paH5Lu2"></span>
## **Delete files in the directory.** 

The following code is used to delete all files under the `exampledir/` directory in the storage bucket.

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
