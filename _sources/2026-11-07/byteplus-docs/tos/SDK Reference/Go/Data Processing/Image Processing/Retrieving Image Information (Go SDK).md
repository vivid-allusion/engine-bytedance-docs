---
title: "Retrieving Image Information (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-image-information-go-sdk"
---

The image information retrieval function provides access to the basic attributes of an image, including its length, width, file size, and format. If the image contains Exif information, the content will be returned in JSON format. This document describes how to obtain image information using the TOS Go SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve image information.

```go
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
    "io/ioutil"
)

type ImageInfo struct {
    FileSize struct {
       Value string `json:"value"`
    } `json:"FileSize"`
    Format struct {
       Value string `json:"value"`
    } `json:"Format"`
    ImageHeight struct {
       Value string `json:"value"`
    } `json:"ImageHeight"`
    ImageWidth struct {
       Value string `json:"value"`
    } `json:"ImageWidth"`
}

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

    
       imageKey = "image.png"
       ctx      = context.Background()
    )
 
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    style := "image/info" 
    out, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{Bucket: bucketName, Key: imageKey, Process: style})
    checkErr(err)
    defer out.Content.Close()
    fmt.Println("ContentType:", out.ContentType)
    info, err := ioutil.ReadAll(out.Content)
    checkErr(err)
    imageInfo := &ImageInfo{}
    err = json.Unmarshal(info, imageInfo)
    checkErr(err)
    fmt.Println("ImageInfo FileSize:", imageInfo.FileSize.Value, " Format:", imageInfo.Format.Value, " ImageHeight:", imageInfo.ImageHeight.Value, " ImageWidth:", imageInfo.ImageWidth.Value)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to obtaining image information, please refer to [Obtaining Image Information](https://docs.byteplus.com/docs/tos/docs-information-query).
