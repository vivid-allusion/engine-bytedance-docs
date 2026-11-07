---
title: "Video Frame Image Persistence (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-go-sdk"
---

TOS supports saving images generated from video frame extraction to a specified storage bucket. This article describes how to use the TOS Go SDK to save images captured from video frames to a specified storage bucket.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to capture the video frame at 300 milliseconds, name the resulting image temp.jpg, and save it to the target storage bucket.

```go
package main

import (
    "context"
    "encoding/base64"
    "encoding/json"
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

type SaveAsResult struct {
    Bucket   string `json:"bucket"`
    FileSize string `json:"fileSize"`
    Object   string `json:"object"`
    Status   string `json:"status"`
}

func main() {
    var (
       accessKey = os.Getenv("TOS_ACCESS_KEY")
       secretKey = os.Getenv("TOS_SECRET_KEY")
       
       endpoint = "your endpoint"
       region   = "your region"
     
       bucketName = "*** Provide your bucket name ***"

       
       videoKey   = "video.mp4"
       ctx        = context.Background()
       
       saveBucket = "*** Provide your bucket name ***"
       
       saveObject = "temp.jpg"
    )
   
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    style := "video/snapshot,t_300" 
    out, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{Bucket: bucketName, Key: videoKey, Process: style, SaveBucket: base64.URLEncoding.EncodeToString([]byte(saveBucket)), SaveObject: base64.URLEncoding.EncodeToString([]byte(saveObject))})
    checkErr(err)
    var saveAsResult SaveAsResult
    err = json.NewDecoder(out.Content).Decode(&saveAsResult)
    checkErr(err)
    fmt.Println("Save As Result:", saveAsResult)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to the persistence of images captured from video frames, please refer to [Image Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
