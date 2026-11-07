---
title: "Listing Buckets (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-go-sdk"
---

Obtain a list of storage buckets (Bucket) using ListBuckets. You can list all storage buckets under every region of the current account that meet the specified criteria.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before listing buckets, you must have the `tos:ListBuckets` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* This interface returns all buckets across all regions for the current account.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code is used to enumerate all buckets across all regions for the current account.

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
   )
   
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
  
   output, err := client.ListBuckets(context.Background(), &tos.ListBucketsInput{})
   checkErr(err)
   fmt.Println("List Buckets Request ID:", output.RequestID)
   fmt.Println("List Buckets Response Code:", output.StatusCode)
   for _, bkt := range output.Buckets {
      fmt.Println("Bucket Name:", bkt.Name)
      fmt.Println("Bucket CreationDate:", bkt.CreationDate)
      fmt.Println("Bucket Location:", bkt.Location)
      fmt.Println("Bucket ExtranetEndpoint:", bkt.ExtranetEndpoint)
      fmt.Println("Bucket IntranetEndpoint:", bkt.IntranetEndpoint)
   }

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on listing buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
