---
title: "Managing Object Tags (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-labels-go-sdk"
---

TOS supports assigning tags to objects and enables lifecycle management of specific objects based on their tags. This document describes how to manage object tags.

<span id="e8c298ce"></span>
## Precautions


* To set object tags, you must have the `tos:PutObjectTagging` permission. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide).

* To retrieve object tags, you must have the `tos:GetObjectTagging` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide).

* To delete object tags, you must have the `tos:DeleteObjectTagging` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide).

* A maximum of 10 tags can be added to each object, and the Key for the same object must not be duplicated. For restrictions on object tags, please refer to [Object Tag Limitations Explanation](https://docs.byteplus.com/docs/tos/docs-managing-file-labels#%E5%AF%B9%E8%B1%A1%E6%A0%87%E7%AD%BE%E9%99%90%E5%88%B6%E8%AF%B4%E6%98%8E).


<span id="7d882408"></span>
## Set Object Tag

TOS supports classifying files within a bucket using object tags, and you can configure lifecycle rules for files that share the same object tags. The following code demonstrates how to set object tags.

```Go
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

     
      objectKey = "*** Provide your object name ***"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

  
   tags := []tos.Tag{
      {
         Key:   "key1",
         Value: "value1",
      }, {
         Key:   "key2",
         Value: "value2",
      },
   }
   output, err := client.PutObjectTagging(ctx, &tos.PutObjectTaggingInput{
      Bucket: bucketName,
      Key:    objectKey,
     
      VersionID: "",
      TagSet:    tos.TagSet{Tags: tags},
   })
   checkErr(err)
   fmt.Println("PutObjectTagging Request ID:", output.RequestID)

}
```


<span id="e5398f23"></span>
## Retrieve Object Tags

After setting object tags, you can retrieve the tag information for the object. When bucket versioning is enabled, TOS returns the tag information of the current version of an object by default. You can obtain the tag information for a specific version by specifying the object's version.

```Go
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

     
      objectKey = "*** Provide your object key ***"
      ctx       = context.Background()
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

  
   output, err := client.GetObjectTagging(ctx, &tos.GetObjectTaggingInput{
      Bucket: bucketName,
      Key:    objectKey,
      
      VersionID: "",
   })
   checkErr(err)
   fmt.Println("GetObjectTagging Request ID:", output.RequestID)
   for key, value := range output.TagSet.Tags {
      fmt.Printf("Object Key:%s,Key:%s, Value:%s\n", objectKey, key, value)
   }

}
```


<span id="e5457aaf"></span>
## Delete Object Tags

You may delete any unnecessary tag information as required. When bucket versioning is enabled, TOS deletes only the tag information of the current object version by default. You can delete the tag information of a specific version by specifying the object's version ID.

```Go
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

      
      objectKey = "*** Provide your object key ***"
      ctx       = context.Background()
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   
   output, err := client.DeleteObjectTagging(ctx, &tos.DeleteObjectTaggingInput{
      Bucket: bucketName,
      Key:    objectKey,
      
      VersionID: "",
   })
   checkErr(err)
   fmt.Println("DeleteObjectTagging Request ID:", output.RequestID)


}
```


<span id="56fcf6b5"></span>
## Relevant Documentation

For API documentation on object tagging, please refer to [PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-).
