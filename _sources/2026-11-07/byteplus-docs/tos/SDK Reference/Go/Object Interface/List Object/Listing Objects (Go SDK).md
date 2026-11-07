---
title: "Listing Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-go-sdk"
---

This article describes how to use ListObjects to enumerate all objects within a specified bucket, files with a specified prefix, as well as files and subdirectories within a specified directory.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The ListObjects interface has been updated to ListObjectsType2. It is strongly recommended that developers use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use the object listing feature, you must have the `tos:ListBucket` permission. For specific instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|Prefix |The prefix of the current query results. |
|Delimiter |Character used to group object names. |
|Marker |Specify the starting position of the object. Return a list of objects sorted alphabetically, starting after the specified value. This is typically the NextMarker value returned by the previous request. |
|MaxKeys |Returns the maximum number of enumerated objects. The default value is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |
|EncodingType |Encode the returned content and specify the type of encoding.<br><br>Default value: None |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code enumerates 10 objects in the specified bucket.

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

   
   output, err := client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
      Bucket: bucketName,
      ListObjectsInput: tos.ListObjectsInput{
         MaxKeys: 10,
      },
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

The following code is used to list objects in the specified bucket with pagination.

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

  
   output, err := client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
      Bucket: bucketName,
      ListObjectsInput: tos.ListObjectsInput{
         MaxKeys: 1000,
      },
   })
   checkErr(err)
   printObjectContent(output.Contents)

   
   output, err = client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
      Bucket: bucketName,
      ListObjectsInput: tos.ListObjectsInput{
         MaxKeys: 1000,
         Marker:  output.NextMarker,
      },
   })
   checkErr(err)
   printObjectContent(output.Contents)

}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code is used to enumerate all objects in the bucket with the specified prefix.

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
   marker := ""
   for truncated {

      output, err := client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
         Bucket: bucketName,
         ListObjectsInput: tos.ListObjectsInput{
            MaxKeys: 1000,
            Prefix:  prefix,
            Marker:  marker,
         },
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
      marker = output.NextMarker
   }

}
```


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### **List all objects in the bucket**

The following code enumerates all objects within the specified bucket.

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
   marker := ""
   for truncated {

      output, err := client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
         Bucket: bucketName,
         ListObjectsInput: tos.ListObjectsInput{
            MaxKeys: 1000,
            Marker:  marker,
         },
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
      marker = output.NextMarker
   }

}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List files and subdirectories in the specified directory**

TOS supports only the concept of objects; it is possible to create an object with a size of zero and a slash in its name.`/`The object at the end simulates the functionality of a directory.

By using the `Delimiter` and `Prefix` parameters, you can simulate directory functionality:


* First, set `Delimiter` to`/`By simultaneously setting `Prefix` to empty, information about objects and subdirectories in the root directory can be returned.

* When setting the `Delimiter` to`/`When `Prefix` is simultaneously set to a subdirectory (subfiledir), objects and subdirectories within that subdirectory can be returned.


The following code is used to enumerate objects and subdirectories within a specified directory of a storage bucket.

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
   marker := ""
   for truncated {
      output, err := client.ListObjectsV2(ctx, &tos.ListObjectsV2Input{
         Bucket: bucketName,
         ListObjectsInput: tos.ListObjectsInput{
            MaxKeys:   1000,
            Delimiter: "/",
            Marker:    marker,
         },
      })
      checkErr(err)
      
      for _, prefix := range output.CommonPrefixes {
         fmt.Println("Sub Dir:", prefix.Prefix)
      }
      
      for _, obj := range output.Contents {
         fmt.Println("Obj:", obj.Key)
      }
      truncated = output.IsTruncated
      marker = output.NextMarker
   }

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on listing objects, refer to [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
