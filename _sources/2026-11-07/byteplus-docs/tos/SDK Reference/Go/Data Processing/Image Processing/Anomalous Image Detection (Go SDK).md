---
title: "Anomalous Image Detection (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Abnormal-image-detection-go-sdk"
---

Abnormal image detection is used to identify whether an image contains suspicious files other than the image itself, such as MPEG\-TS files. If an image file containing suspicious content is detected, you may process the image file to prevent your storage space from being misused by illicit image hosting services. This article describes how to perform abnormal image detection using the TOS Go SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The size of the original image for detection must not exceed 20MB.

* Abnormal image detection is supported only for files in JPG, JPEG, PNG, BMP, GIF, and pure TS video stream file formats.

* The abnormal image detection function is billed based on the number of processing instances. For detailed information, please refer to [Data Processing Fees](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to detect abnormal images.

```go
package main

import (
    "context"
    "encoding/json"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
    "io/ioutil"
)

type ImageInspectResponse struct {
    PicSize             int    `json:"picSize"`
    PicType             string `json:"picType"`
    Suspicious          bool   `json:"suspicious"`
    SuspiciousBeginByte int    `json:"suspiciousBeginByte"`
    SuspiciousEndByte   int    `json:"suspiciousEndByte"`
    SuspiciousSize      int    `json:"suspiciousSize"`
    SuspiciousType      string `json:"suspiciousType"`
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

   
    style := "image/inspect" 
    out, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{Bucket: bucketName, Key: imageKey, Process: style})
    checkErr(err)
    defer out.Content.Close()
    fmt.Println("ContentType:", out.ContentType)
    info, err := ioutil.ReadAll(out.Content)
    checkErr(err)
    imageInspect := &ImageInspectResponse{}
    err = json.Unmarshal(info, imageInspect)
    checkErr(err)
    fmt.Println("picSize:", imageInspect.PicSize, " picType:", imageInspect.PicType, " suspicious:", imageInspect.Suspicious)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documents

For a detailed introduction to abnormal image detection, please refer to [Abnormal Image Detection](https://docs.byteplus.com/docs/6349/1140988).
