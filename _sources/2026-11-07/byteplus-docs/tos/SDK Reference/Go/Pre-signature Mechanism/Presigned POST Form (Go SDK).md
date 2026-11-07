---
title: "Presigned POST Form (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-pre-signature-go-sdk"
---

This article presents example code for POST form presigning.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

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
   
  
   res, err := client.PreSignedPostSignature(ctx, &tos.PreSingedPostSignatureInput{
      Bucket:  bucketName,
      Key:     objectKey,
      Expires: 3600,
   })
   fmt.Println("Policy:", res.Policy)
   fmt.Println("OriginPolicy:", res.OriginPolicy)
   fmt.Println("Algorithm:", res.Algorithm)
   fmt.Println("Credential:", res.Credential)
   fmt.Println("Date:", res.Date)
   fmt.Println("Signature:", res.Signature)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For detailed information on POST form presigning, see [Including a signature in browser-based upload forms](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
