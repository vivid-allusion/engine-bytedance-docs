---
title: "Deleting Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-go-sdk"
---

When an object is no longer in use, you may delete it to reduce cost overhead. Currently, the TOS Go SDK supports deleting individual objects and specified multiple objects within a bucket. For buckets with versioning enabled, you can specify and delete any version of an object's data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before deleting an object, you must have the `tos:DeleteObject` permission. For detailed instructions, see the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:DeleteObjectVersion` permission before deleting a specified version of an object. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### **Delete Specified Object**

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

     
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   checkErr(err)
   fmt.Println("DeleteObjectV2 Request ID:", output.RequestID)

}
```


<span id=".5Yig6Zmk5oyH5a6a54mI5pys55qE5a-56LGh"></span>
### **Delete the specified version of an object**

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

      
      objectKey = "example_dir/example.txt"
      ctx       = context.Background()
      
      versionID = "*** Provide object Version ID"
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   output, err := client.DeleteObjectV2(ctx, &tos.DeleteObjectV2Input{
      Bucket:    bucketName,
      Key:       objectKey,
      VersionID: versionID,
   })
   checkErr(err)
   fmt.Println("DeleteObjectV2 Request ID:", output.RequestID)

}
```


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### **Bulk Object Deletion**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In a bucket with versioning enabled, when the DeleteMultiObjects API is called to delete objects in bulk, if the <code>versionId</code> is not specified in the Delete request, a delete marker will be inserted. If <code>versionId</code> is specified, the specified version of the object will be permanently deleted.</div>


* <div data-tips="true" data-tips-type="warning">The supported response mode for batch object deletion can be configured using <code>quiet</code>:</div>


   * <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>false</code>, the response will include the deletion result regardless of whether the object was successfully deleted.</div>


   * <div data-tips="true" data-tips-type="warning">When <code>quiet</code> is set to <code>true</code>, the response only includes the results of objects whose deletion failed; objects not included in the response are considered successfully deleted.</div>



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

      
      objectKey1 = "*** Provide Object Key ***"
      objectKey2 = "*** Provide Object Key ***"
      ctx        = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   objects := make([]tos.ObjectTobeDeleted, 2)
   objects[0] = tos.ObjectTobeDeleted{Key: objectKey1}
   objects[1] = tos.ObjectTobeDeleted{Key: objectKey2}
   
   output, err := client.DeleteMultiObjects(ctx, &tos.DeleteMultiObjectsInput{
      Bucket:  bucketName,
      Objects: objects,
   })
   checkErr(err)
   fmt.Println("DeleteMultiObjects Request ID:", output.RequestID)

}
```


<span id=".5om56YeP5Yig6Zmk5oyH5a6a54mI5pys55qE5a-56LGh"></span>
### **Batch Deletion of Objects of a Specified Version**

The following code is used to delete multiple objects, identified by specified object names and version numbers, from a designated storage bucket.

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

      
      objectKey1 = "*** Provide Object Key ***"
      
      versionID1 = "*** Provide objectKey1 Version ID ***"
      objectKey2 = "*** Provide Object Key ***"
      versionID2 = "*** Provide objectKey2 Version ID ***"
      ctx        = context.Background()
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   objects := make([]tos.ObjectTobeDeleted, 2)
   objects[0] = tos.ObjectTobeDeleted{Key: objectKey1, VersionID: versionID1}
   objects[1] = tos.ObjectTobeDeleted{Key: objectKey2, VersionID: versionID2}
   
   output, err := client.DeleteMultiObjects(ctx, &tos.DeleteMultiObjectsInput{
      Bucket:  bucketName,
      Objects: objects,
   })
   checkErr(err)
   fmt.Println("DeleteMultiObjects Request ID:", output.RequestID)

}
```


<span id=".5Yig6Zmk5qG25Lit5omA5pyJ5a-56LGh"></span>
### **Delete all objects in the bucket**

The following code demonstrates how to delete all objects within a specified Bucket.

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
      ctx        = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   
   keyMarker := ""
   isTruncated := true
   for isTruncated {
      listOutput, err := client.ListObjectVersionsV2(ctx, &tos.ListObjectVersionsV2Input{
         Bucket: bucketName,
         ListObjectVersionsInput: tos.ListObjectVersionsInput{
            KeyMarker: keyMarker,
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

      isTruncated = listOutput.IsTruncated
      keyMarker = listOutput.NextKeyMarker
   }

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on deleting objects, refer to [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
