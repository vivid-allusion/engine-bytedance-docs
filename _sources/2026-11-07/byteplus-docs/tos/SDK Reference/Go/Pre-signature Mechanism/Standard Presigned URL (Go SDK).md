---
title: "Standard Presigned URL (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-go-sdk"
---

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports generating signed URLs, which users can utilize to initiate HTTP requests directly or share with third parties to enable access authorization.

<span id="KXqgr0H1"></span>
## **Downloading Objects Using Pre\-Signed URLs**

The following code is used to download objects from a specified bucket via a pre\-signed URL.

```go
package main

import (
   "net/http"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
)

func checkErr(err error) {
   if err != nil {
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
      httpClient = &http.Client{}
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   url, err := client.PreSignedURL(&tos.PreSignedURLInput{
      HTTPMethod: enum.HttpMethodGet,
      Bucket:     bucketName,
      Key:        objectKey,
   })
   checkErr(err)

   req, _ := http.NewRequest(http.MethodGet, url.SignedUrl, nil)
   res, err := httpClient.Do(req)
   checkErr(err)
   if res.StatusCode != http.StatusOK {
      panic("unexpected status code")
   }
}
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
## **Uploading Objects Using Pre\-Signed URLs**

The following code is used to upload objects to a specified bucket via a pre\-signed URL.

```go
package main

import (
   "net/http"
   "strings"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
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
      endpoint   = "your endpoint"
      region     = "your region"
      bucketName = "your bucket name"
      objectName = "your object name"
      httpClient = &http.Client{}
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   url, err := client.PreSignedURL(&tos.PreSignedURLInput{
      HTTPMethod: enum.HttpMethodPut,
      Bucket:     bucketName,
      Key:        objectName,
   })
   checkErr(err)

   body := strings.NewReader("your body reader")
   req, _ := http.NewRequest(http.MethodPut, url.SignedUrl, body)
   res, err := httpClient.Do(req)
   checkErr(err)
   if res.StatusCode != http.StatusOK  {
      panic("unexpected status code")
   }
}
```


<span id="VtgTHfjK"></span>
## **Deleting Objects Using Pre\-Signed URLs**

The following code is used to delete an object from a specified bucket using a pre\-signed URL.

```go
package main

import (
   "net/http"

   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos/enum"
)

func checkErr(err error) {
   if err != nil {
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

  
      objectKey  = "*** Provide your object key ***"
      httpClient = &http.Client{}
   )
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   url, err := client.PreSignedURL(&tos.PreSignedURLInput{
      HTTPMethod: enum.HttpMethodDelete,
      Bucket:     bucketName,
      Key:        objectKey,
   })
   checkErr(err)
  
   req, _ := http.NewRequest(http.MethodDelete, url.SignedUrl, nil)
   res, err := httpClient.Do(req)
   checkErr(err)
   if res.StatusCode != http.StatusNoContent {
      panic("unexpected status code")
   }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For detailed information about URLs containing signatures, see [URLs Containing Signatures](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
