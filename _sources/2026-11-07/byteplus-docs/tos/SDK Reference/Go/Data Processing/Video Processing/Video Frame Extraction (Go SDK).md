---
title: "Video Frame Extraction (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-go-sdk"
---

The video frame capture function enables extraction of a single frame from a video stream at a specified time and resizes it to a designated image size. This article describes how to perform video frame extraction using the TOS Go SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 300 milliseconds, save the captured image as temp.jpg, and download it to the local device.

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

 
       videoKey = "video.mp4"
       ctx      = context.Background()
     
       fileName = "temp.jpg"
    )
  
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

   
    style := "video/snapshot,t_300" 
    
    _, err = client.GetObjectToFile(ctx, &tos.GetObjectToFileInput{GetObjectV2Input: tos.GetObjectV2Input{Bucket: bucketName, Key: videoKey, Process: style}, FilePath: fileName})
    checkErr(err)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to video frame extraction, please refer to [Video Frame Extraction](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
