---
title: "Retrieving Bucket Information (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-information-go-sdk"
---

You can use HeadBucket to retrieve information about a storage bucket (Bucket). Additionally, by examining the HTTP Code in the returned err, you can determine whether the bucket exists. This document describes how to retrieve bucket metadata and determine whether a bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before retrieving bucket metadata, you must have the `tos:HeadBucket` permission. For detailed instructions, please refer to [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If the bucket does not exist, this interface will return a 404 error code; this interface is also commonly used to verify whether a bucket exists.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

<span id=".5Yik5pat5qG25piv5ZCm5a2Y5Zyo"></span>
### **Determine whether the bucket exists**

```go
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
   )
 
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)


   resp, err := client.HeadBucket(context.Background(), &tos.HeadBucketInput{Bucket: bucketName})
   if err != nil {
     
      if serverErr, ok := err.(*tos.TosServerError); ok {
         if serverErr.StatusCode == http.StatusNotFound {
       
            fmt.Println("Bucket not found.")
         } else {
            fmt.Println("Error:", serverErr.Error())
            fmt.Println("Request ID:", serverErr.RequestID)
            fmt.Println("Response Status Code:", serverErr.StatusCode)
            fmt.Println("Response Header:", serverErr.Header)
            panic(err)
         }
      } else {
         panic(err)
      }
   }
 
   fmt.Println("Head Bucket Request ID: ", resp.RequestID)
   fmt.Println("Head Bucket Response Status Code: ", resp.StatusCode)
   
}
```


<span id=".6I635Y-W5qG25YWD5pWw5o2u5L-h5oGv"></span>
### **Retrieve Bucket Metadata Information**

```go
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
   )
  
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

  
   resp, err := client.HeadBucket(context.Background(), &tos.HeadBucketInput{Bucket: bucketName})
   if err != nil {
  
      if serverErr, ok := err.(*tos.TosServerError); ok {
         if serverErr.StatusCode == http.StatusNotFound {
            fmt.Println("Bucket not found.")
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
  
   fmt.Println("Head Bucket Request ID: ", resp.RequestID)
   fmt.Println("Head Bucket Response Status Code: ", resp.StatusCode)
 
   fmt.Println("Bucket Region:", resp.Region)
 
   fmt.Println("Bucket Storage Class:", resp.StorageClass)
   View the bucket AZ type
   fmt.Println("Bucket Az Redundancy:", resp.AzRedundancy)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For documentation on retrieving bucket metadata, refer to [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
