---
title: "Managing Object Renaming (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-renaming-objects-go-sdk"
---

TOS supports the renaming of individual objects within a bucket. To use the object renaming feature, you must first enable the bucket's renaming feature.

<span id="f68c1a2b"></span>
## **Configure renaming rules**

<span id="c3622f2e"></span>
### **Precautions**


* The `rename_enable` parameter can only be set to `True`.

* The rename functionality is not supported when versioning is enabled for the bucket.


<span id="4df78357"></span>
### **Sample code**

The following code is used to configure the bucket to enable the renaming feature.

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

    output, err := client.PutBucketRename(ctx, &tos.PutBucketRenameInput{
       Bucket:       bucketName,
       RenameEnable: true,
    })
    checkErr(err)
    fmt.Println("PutBucketRename Request ID:", output.RequestID)
}
```


<span id="5ac97325"></span>
## **Retrieve renaming rules**

<span id="5e00afbd"></span>
### **Precautions**

To obtain the renaming rules for a bucket, you must be the bucket owner.

<span id="8952771c"></span>
### **Sample code**

The following code is used to retrieve renaming rules.

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
 
    output, err := client.GetBucketRename(ctx, &tos.GetBucketRenameInput{
       Bucket: bucketName,
    })
    checkErr(err)
    fmt.Println("GetBucketRename Request ID:", output.RequestID)
}
```


<span id="79e0e895"></span>
## **Delete renaming rules**

<span id="dcc426ad"></span>
### **Precautions**

To remove a bucket's renaming rules, you must be the bucket owner.

<span id="f2962fde"></span>
### **Sample code**

The following code is used to delete renaming rules.

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

    output, err := client.DeleteBucketRename(ctx, &tos.DeleteBucketRenameInput{
       Bucket: bucketName,
    })
    checkErr(err)
    fmt.Println("DeleteBucketRename Request ID:", output.RequestID)
}
```


<span id="7d33b131"></span>
## Relevant documentation


* For detailed information about RenameObject, see [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).

* For API documentation regarding enabling object renaming, refer to [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename).

* For details on the API for obtaining object renaming rules, see [GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename).

* For API documentation regarding disabling object renaming, see [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename).
