---
title: "List Objects V2 (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-go-sdk"
---

This document describes how to use ListObjectsType2 to enumerate all objects within a specified bucket, files with a specified prefix, and files and subdirectories within a specified directory.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The ListObjects API has been updated to ListObjectsType2. Developers are strongly encouraged to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use List Objects V2, you must have the `tos:ListBucket` permission. For specific procedures, refer to the [ IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description

The parameters supported by ListObjectsType2 are as follows:


|**Parameters** |**Description** |
|---|---|
|Prefix |The prefix of the current query results. |
|Delimiter |Character used to group object names. |
|StartAfter |The starting point for the objects enumerated in this instance. |
|ContinuationToken |The specified enumeration operation must begin from this token. It can be obtained from the NextContinuationToken in the previous listing results. |
|MaxKeys |Returns the maximum number of objects to be listed; the default value is 1000.<br><br>Value: greater than 0 and less than or equal to 1000. |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code lists up to 10 objects from the specified storage bucket.

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
   
   output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
      Bucket:  bucketName,
      MaxKeys: 10,
   })
   checkErr(err)
   for _, obj := range output.Contents {
      
      fmt.Println("Object Key:", obj.Key)
      
      fmt.Println("Object LastModified:", obj.LastModified)
      
      fmt.Println("Object ETag:", obj.ETag)
      
      fmt.Println("Object Size:", obj.Size)
      
      fmt.Println("Object Owner:", obj.Owner)
      
      fmt.Println("Object StorageClass:", obj.StorageClass)
      
      fmt.Println("Object HashCrc64ecma:", obj.HashCrc64ecma)
   }

}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated Listing**

The following code is used to paginate and list objects in the specified storage bucket.

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

func printObjectContent(contents []tos.ListedObjectV2) {
   for _, obj := range contents {
      
      fmt.Println("Object Key:", obj.Key)
      
      fmt.Println("Object LastModified:", obj.LastModified)
      
      fmt.Println("Object ETag:", obj.ETag)
      
      fmt.Println("Object Size:", obj.Size)
     
      fmt.Println("Object Owner:", obj.Owner)
      
      fmt.Println("Object StorageClass:", obj.StorageClass)
      
      fmt.Println("Object HashCrc64ecma:", obj.HashCrc64ecma)
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
   
   output, err := client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
      Bucket:  bucketName,
      MaxKeys: 1000,
   })
   checkErr(err)
   printObjectContent(output.Contents)

   
   output, err = client.ListObjectsType2(ctx, &tos.ListObjectsType2Input{
      Bucket:            bucketName,
      MaxKeys:           1000,
      ContinuationToken: output.NextContinuationToken,
   })
   printObjectContent(output.Contents)

}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code enumerates all objects with the specified prefix in the designated bucket.

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
      prefix     = "*** Provide your object key prefix ***"

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
         Prefix:            prefix,
      })
      checkErr(err)
      for _, obj := range output.Contents {
         
         fmt.Println("Object Key:", obj.Key)
         
         fmt.Println("Object LastModified:", obj.LastModified)
        
         fmt.Println("Object ETag:", obj.ETag)
        
         fmt.Println("Object Size:", obj.Size)
       
         fmt.Println("Object Owner:", obj.Owner)
         
         fmt.Println("Object StorageClass:", obj.StorageClass)
       
         fmt.Println("Object HashCrc64ecma:", obj.HashCrc64ecma)
      }
      truncated = output.IsTruncated
      continuationToken = output.NextContinuationToken
   }

}
```


<span id=".5YiG6aG15YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### **List all objects in the bucket with pagination**

The following code enumerates all objects within the specified storage bucket.

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
      })
      checkErr(err)
      for _, obj := range output.Contents {
         
         fmt.Println("Object Key:", obj.Key)
         
         fmt.Println("Object LastModified:", obj.LastModified)
         
         fmt.Println("Object ETag:", obj.ETag)
        
         fmt.Println("Object Size:", obj.Size)
         
         fmt.Println("Object Owner:", obj.Owner)
         
         fmt.Println("Object StorageClass:", obj.StorageClass)
         
         fmt.Println("Object HashCrc64ecma:", obj.HashCrc64ecma)
      }
      truncated = output.IsTruncated
      continuationToken = output.NextContinuationToken
   }

}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List the files and subdirectories within the specified directory.** 

TOS only supports the concept of objects; it is possible to create an object with a size of zero whose name contains a slash.`/`The object at the end simulates the functionality of a directory.

By using the parameters `Delimiter` and `Prefix`, you can simulate the functionality of a directory:


* First, set `Delimiter` to`/`By setting the `Prefix` to empty, objects and subdirectory information under the root directory can be returned.

* When setting `Delimiter` to`/`By also setting `Prefix` as a subdirectory (subfiledir), objects and subdirectories of the subdirectory can be returned.


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
      region   = "cn-beijing"
      
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
         
         fmt.Println("Object Key:", obj.Key)
         
         fmt.Println("Object LastModified:", obj.LastModified)
        
         fmt.Println("Object ETag:", obj.ETag)
        
         fmt.Println("Object Size:", obj.Size)
         
         fmt.Println("Object Owner:", obj.Owner)
         
         fmt.Println("Object StorageClass:", obj.StorageClass)
         
         fmt.Println("Object HashCrc64ecma:", obj.HashCrc64ecma)
      }
      truncated = output.IsTruncated
      continuationToken = output.NextContinuationToken
   }

}
```
