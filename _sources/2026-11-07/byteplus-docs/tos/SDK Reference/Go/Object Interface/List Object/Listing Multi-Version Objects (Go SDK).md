---
title: "Listing Multi-Version Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-go-sdk"
---

This interface is used to list multi\-version objects in a bucket. Each request returns a subset of multi\-version objects from the bucket, with a maximum of 1,000 objects per request. Request parameters can be used as selection criteria to return a specific subset of objects within the bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**

Before listing multi\-version objects, you must have the `tos:ListBucketVersions` permission. For specific instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|Prefix |The prefix of the current query results. |
|Delimiter |The character used to group object names. |
|MaxKeys |Returns the maximum number of objects to be listed; the default value is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |
|KeyMarker |List the starting positions of multi\-version objects. Configure the system to return a list of objects sorted alphabetically, starting after the specified value. This is typically the value of NextKeyMarker returned by the previous request. |
|VersionIdMarker |Used in conjunction with KeyMarker, this sets the point after which a lexicographically sorted list of multi\-version objects is returned. Obtain NextVersionIDMarker from the results of the previous listing. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **A brief enumeration**

The following code is used to list up to 10 multi\-version objects in the specified storage bucket.

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

  
   output, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
      Bucket: bucketName,
      ListObjectVersionsInput: tos.ListObjectVersionsInput{
         MaxKeys: 10,
      },
   })
   checkErr(err)
   for _, obj := range output.Versions {
      fmt.Println("Obj Key:", obj.Key)
      fmt.Println("Obj Version ID:", obj.VersionID)
      fmt.Println("Obj Last Modified:", obj.LastModified)
      fmt.Println("Obj Is Latest Version:", obj.IsLatest)
   }
   for _, deleteMarker := range output.DeleteMarkers {
      fmt.Println("Delete Maker Key:", deleteMarker.Key)
      fmt.Println("Delete Maker Version ID:", deleteMarker.VersionID)
      fmt.Println("Delete Maker Last Modified:", deleteMarker.LastModified)
      fmt.Println("Delete Maker Is Latest Version:", deleteMarker.IsLatest)
   }

}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code enumerates all multi\-version objects and delete markers under the specified prefix in the designated bucket.

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
   versionIdMarker := ""

   for truncated {
      output, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
         Bucket: bucketName,
         ListObjectVersionsInput: tos.ListObjectVersionsInput{
            MaxKeys:         10,
            Prefix:          prefix,
            KeyMarker:       marker,
            VersionIDMarker: versionIdMarker,
         },
      })
      checkErr(err)
      for _, obj := range output.Versions {
         fmt.Println("Obj Key:", obj.Key)
         fmt.Println("Obj Version ID:", obj.VersionID)
         fmt.Println("Obj Last Modified:", obj.LastModified)
         fmt.Println("Obj Is Latest Version:", obj.IsLatest)
      }
      for _, deleteMarker := range output.DeleteMarkers {
         fmt.Println("Delete Maker Key:", deleteMarker.Key)
         fmt.Println("Delete Maker Version ID:", deleteMarker.VersionID)
         fmt.Println("Delete Maker Last Modified:", deleteMarker.LastModified)
         fmt.Println("Delete Maker Is Latest Version:", deleteMarker.IsLatest)
      }
      truncated = output.IsTruncated
      marker = output.NextKeyMarker
      versionIdMarker = output.NextVersionIDMarker
   }

}
```


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### **Enumerate all objects**

The following code is used to enumerate all multi\-version objects and delete markers within the specified bucket.

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
   versionIdMarker := ""

   for truncated {
      output, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
         Bucket: bucketName,
         ListObjectVersionsInput: tos.ListObjectVersionsInput{
            MaxKeys:         1000,
            KeyMarker:       marker,
            VersionIDMarker: versionIdMarker,
         },
      })
      checkErr(err)
      for _, obj := range output.Versions {
         fmt.Println("Obj Key:", obj.Key)
         fmt.Println("Obj Version ID:", obj.VersionID)
         fmt.Println("Obj Last Modified:", obj.LastModified)
         fmt.Println("Obj Is Latest Version:", obj.IsLatest)
      }
      for _, deleteMarker := range output.DeleteMarkers {
         fmt.Println("Delete Maker Key:", deleteMarker.Key)
         fmt.Println("Delete Maker Version ID:", deleteMarker.VersionID)
         fmt.Println("Delete Maker Last Modified:", deleteMarker.LastModified)
         fmt.Println("Delete Maker Is Latest Version:", deleteMarker.IsLatest)
      }
      truncated = output.IsTruncated
      marker = output.NextKeyMarker
      versionIdMarker = output.NextVersionIDMarker
   }

}
```


<span id=".6YCS5b2S5YiX5Li-55uu5b2V5LiL55qE5a-56LGh5ZKM5a2Q55uu5b2V"></span>
### **Recursively enumerate objects and subdirectories within a directory**

TOS defines only the concept of objects; it is possible to create an object with a size of zero and a name consisting of a slash (/).`/`The object at the end simulates the function of a directory.

The functionality of a directory can be simulated using the `Delimiter` and `Prefix` parameters:


* First, set the `Delimiter` to`/`At the same time, when `Prefix` is set to empty, objects and subdirectory information in the root directory can be returned.

* When setting `Delimiter` to`/`By simultaneously setting the `Prefix` to a subdirectory (subfiledir), objects and subdirectories of that subdirectory can be returned.


The following code recursively enumerates objects and subdirectories within a directory. For objects, information on all versions is returned; for directories, only the latest version information is provided.

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
   versionIdMarker := ""
   delimiter := "/"

   for truncated {
      output, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
         Bucket: bucketName,
         ListObjectVersionsInput: tos.ListObjectVersionsInput{
            MaxKeys:         1000,
            KeyMarker:       marker,
            VersionIDMarker: versionIdMarker,
            Delimiter:       delimiter,
         },
      })
      checkErr(err)

      
      for _, prefix := range output.CommonPrefixes {
         fmt.Println("Sub Dir:", prefix.Prefix)
      }
      
      for _, obj := range output.Versions {
         fmt.Println("Obj Key:", obj.Key)
         fmt.Println("Obj Version ID:", obj.VersionID)
         fmt.Println("Obj Last Modified:", obj.LastModified)
         fmt.Println("Obj Is Latest Version:", obj.IsLatest)
      }
      for _, deleteMarker := range output.DeleteMarkers {
         fmt.Println("Delete Maker Key:", deleteMarker.Key)
         fmt.Println("Delete Maker Version ID:", deleteMarker.VersionID)
         fmt.Println("Delete Maker Last Modified:", deleteMarker.LastModified)
         fmt.Println("Delete Maker Is Latest Version:", deleteMarker.IsLatest)
      }
      truncated = output.IsTruncated
      marker = output.NextKeyMarker
      versionIdMarker = output.NextVersionIDMarker
   }

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For the API documentation on listing multi\-version objects, please refer to [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
