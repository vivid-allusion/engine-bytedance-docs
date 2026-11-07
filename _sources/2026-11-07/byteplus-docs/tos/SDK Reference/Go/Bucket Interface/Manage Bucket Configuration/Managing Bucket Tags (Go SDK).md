---
title: "Managing Bucket Tags (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-labels-go-sdk"
---

TOS supports the bucket tagging feature, which enables the identification of cloud resources. Tags facilitate the marking and classification of buckets with similar characteristics from multiple dimensions, such as purpose, type, owner, and environment, thereby streamlining management.

<span id="b78a7a8a"></span>
## Configure bucket tags

<span id="4065c718"></span>
### **Sample code**

The following code is used to set tags for the specified bucket.

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
       accessKey = "*** Provide your access key ***"
       secretKey = "*** Provide your secret key ***"

       endpoint = "your endpoint"
       region   = "your region"
   
       bucketName = "*** Provide your bucket name ***"
       ctx        = context.Background()
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
    input := &tos.PutBucketTaggingInput{
       Bucket: bucketName,

       TagSet: tos.TagSet{Tags: []tos.Tag{
          {
             Key:   "key1",
             Value: "value1",
          }, {
             Key:   "key2",
             Value: "value2",
          },
       }},
    }
    output, err := client.PutBucketTagging(ctx, input)
    checkErr(err)
    fmt.Println("PutBucketTagging Request ID:", output.RequestID)
}
```


<span id="5646a2cd"></span>
## Retrieve bucket tags

<span id="06a28458"></span>
### **Sample code**

The following code retrieves the tags for the specified bucket.

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
       accessKey = "*** Provide your access key ***"
       secretKey = "*** Provide your secret key ***"
   
       endpoint = "your endpoint"
       region   = "your region"

       bucketName = "*** Provide your bucket name ***"
       ctx        = context.Background()
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
    input := &tos.GetBucketTaggingInput{
       Bucket: bucketName,
    }
    output, err := client.GetBucketTagging(ctx, input)
    checkErr(err)
    fmt.Println("GetBucketTagging Request ID:", output.RequestID)
    for _, tag := range output.TagSet.Tags {
       fmt.Println("key:", tag.Key, " value:", tag.Value)
    }
}
```


<span id="a8a59e08"></span>
## Delete bucket tags

<span id="dfddccd9"></span>
### **Sample code**

The following code is used to delete the specified bucket tag.

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
       accessKey = "*** Provide your access key ***"
       secretKey = "*** Provide your secret key ***"
  
       endpoint = "your endpoint"
       region   = "your region"
 
       bucketName = "*** Provide your bucket name ***"
       ctx        = context.Background()
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
    input := &tos.DeleteBucketTaggingInput{
       Bucket: bucketName,
    }
    output, err := client.DeleteBucketTagging(ctx, input)
    checkErr(err)
    fmt.Println("DeleteBucketTagging Request ID:", output.RequestID)
}
```


<span id="3eae4ff2"></span>
## **Relevant documentation**

For more information about bucket tags, see [Setting bucket tags](https://docs.byteplus.com/docs/tos/Set-bucket-tag).
