---
title: "Determining Object Existence (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Determine-whether-an-object-exists-go-sdk"
---

You can determine whether an object exists by using the Go SDK's `HeadObject` interface.

<span id="391f9225"></span>
## Precautions

To determine whether an object exists, your account must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

<span id="e6928431"></span>
## Sample Code

The following code demonstrates how to determine whether an object exists.

```Go
package main

import (
   "context"
   "fmt"
   "net/http"

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
   output, err := client.HeadObjectV2(ctx, &tos.HeadObjectV2Input{
      Bucket: bucketName,
      Key:    objectKey,
   })
   if err != nil {
      if serverErr, ok := err.(*tos.TosServerError); ok {
         
         if serverErr.StatusCode == http.StatusNotFound {
            fmt.Println("Object not found.")
         } else {
            fmt.Println("Error:", serverErr.Error())
            fmt.Println("Request ID:", serverErr.RequestID)
            fmt.Println("Response Status Code:", serverErr.StatusCode)
            fmt.Println("Response Header:", serverErr.Header)
            fmt.Println("Response Err Code:", serverErr.Code)
            fmt.Println("Response Err Msg:", serverErr.Message)
            panic(err)
         }
      } else {
         panic(err)
      }
   }
   fmt.Println("HeadObjectV2 Request ID:", output.RequestID)
  
   fmt.Println("HeadObjectV2 Response ContentLanguage:", output.ContentLanguage)
   
   fmt.Println("HeadObjectV2 Response ContentDisposition:", output.ContentDisposition)
   
   fmt.Println("HeadObjectV2 Response ContentEncoding:", output.ContentEncoding)
   
   fmt.Println("HeadObjectV2 Response CacheControl:", output.CacheControl)
  
   fmt.Println("HeadObjectV2 Response ContentType:", output.ContentType)
  
   fmt.Println("HeadObjectV2 Response Expires:", output.Expires)
}
```


<span id="b125d336"></span>
## **Relevant Documentation**

For information on the API used to determine whether an object exists, refer to [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
