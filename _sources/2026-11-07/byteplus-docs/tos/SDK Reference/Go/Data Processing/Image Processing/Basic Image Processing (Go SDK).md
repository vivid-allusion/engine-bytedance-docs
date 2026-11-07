---
title: "Basic Image Processing (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-go-sdk"
---

TOS supports processing of stored images, including image resizing, image cropping, image watermarking, format conversion, and other image processing operations. This article introduces how to perform basic image processing using the TOS Go SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The original image format supports only JPG, PNG, BMP, GIF, WEBP, and TIFF.

* The size of the original image must not exceed 20 MB.

* The original image width and height must not exceed 30,000 px, and the total number of pixels must not exceed 250 million px. For rotation operations, the original image width and height must not exceed 4,096 px.

* Neither the width nor the height of the scaled image may exceed 16,384 px, and the total number of pixels must not exceed 16,777,216 px.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to set the image height to 100px, convert the image format to JPG, name the image temp.jpg, and download it to your computer.

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

   
       imageKey = "image.png"
       ctx      = context.Background()
       fileName = "temp.jpg"
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)


    style := "image/resize,h_100/format,jpg" 
    out, err := client.GetObjectToFile(ctx, &tos.GetObjectToFileInput{GetObjectV2Input: tos.GetObjectV2Input{Bucket: bucketName, Key: imageKey, Process: style}, FilePath: fileName})
    checkErr(err)
    fmt.Println("ContentType:", out.ContentType)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to image processing, please refer to [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
