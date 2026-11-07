---
title: "Image Processing Persistence (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Image-processing-persistence-go-sdk"
---

By default, TOS does not save processed images. You can use code to save the processed images to the specified storage bucket. This article describes how to use the TOS Go SDK to save processed images to a designated storage bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* An account used for persistent image processing must have read permission for the bucket containing the original image and write permission for the target bucket where the image will be transferred.

* When saving processed images to a specified storage bucket as an anonymous user, the bucket must be configured with public write permissions.

* The source bucket of the original image and the target bucket for image transfer must be located in the same region.

* By default, the access permission for transferred images is set to private, and the storage type is set to standard storage.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to set the image height to 100px, convert the image format to JPG, name the processed image temp.jpg, and save it to the target storage bucket.

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

       
       imageKey = "image.png"
       ctx        = context.Background()
     
       saveBucket = "*** Provide your bucket name ***"
     
       saveObject = "temp.jpg"
    )
  
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

   
    style := "image/resize,h_100/format,jpg" 
    out, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{Bucket: bucketName, Key: imageKey, Process: style, SaveBucket: base64.URLEncoding.EncodeToString([]byte(saveBucket)), SaveObject: base64.URLEncoding.EncodeToString([]byte(saveObject))})
    checkErr(err)
    var saveAsResult SaveAsResult
    err = json.NewDecoder(out.Content).Decode(&saveAsResult)
    checkErr(err)
    fmt.Println("Save As Result:", saveAsResult)
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to image processing persistence, please refer to [Image Processing Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
