---
title: "Configuring Object-Level Expiration Time (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-object-level-expiration-time-go-sdk"
---

You can set the expiration time for uploaded objects via the TOS Go SDK's `SetObjectExpires` interface. Once expired, TOS will automatically delete the object.

<span id="ab21f5da"></span>
## **Precautions**


* To set object\-level expiration time, you must have the `tos:SetObjectExpires` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To set object\-level expiration times using the Go SDK, ensure that the Go SDK version is v2.7.20 or later.


<span id="6f833653"></span>
## Sample Code

```Go
package main
import (
    "context"
    "fmt"
    "os"
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
     
       objectKey  = "example_dir/example.txt"
       ctx        = context.Background()
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    output, err := client.SetObjectExpires(ctx, &tos.SetObjectExpiresInput{
       Bucket:        bucketName,
       Key:           objectKey,

       ObjectExpires: 1,
    })
    checkErr(err)
    fmt.Println("SetObjectExpires Request ID:", output.RequestID)
}
```


<span id="c9101722"></span>
## **Relevant Documentation**

For API documentation on configuring object\-level expiration times, refer to [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires).
