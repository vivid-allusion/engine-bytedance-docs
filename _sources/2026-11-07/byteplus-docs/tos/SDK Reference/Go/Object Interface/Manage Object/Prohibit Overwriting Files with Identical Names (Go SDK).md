---
title: "Prohibit Overwriting Files with Identical Names (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Do-not-overwrite-files-with-the-same-name-go-sdk"
---

This article describes how to prevent overwriting files with identical names during upload, copy, and multipart upload operations in the Go SDK by setting the x\-tos\-forbid\-overwrite request header.

<span id="89849e4d"></span>
# Simple Upload

The following code is used to prevent overwriting files with identical names during simple upload:

```Go
package main

import (
    "context"
    "fmt"
    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
    "os"
    "strings"
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
       
       bucketName = "*** Provide your bucket name ***"

       objectKey = "*** Provide your object key ***"
       ctx       = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
    
    
   
    body := strings.NewReader("Hello TOS")
    output, err := client.PutObjectV2(ctx, &tos.PutObjectV2Input{
       PutObjectBasicInput: tos.PutObjectBasicInput{
          Bucket:          bucketName,
          Key:             objectKey,
          ForbidOverwrite: true,
       },
       Content: body,
    })
    checkErr(err)
    fmt.Println("PutObjectV2 Request ID:", output.RequestID)
}
```


<span id="3ee551ee"></span>
# Copying Files

The following code is used to prevent overwriting files with identical names during file copying:

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
       
       bucketName = "*** Provide your bucket name ***"
       
       srcObjectKey = "srcObjectKey"
       dstObjectKey = "objectKey"
       ctx          = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)
 
   
    output, err := client.CopyObject(ctx, &tos.CopyObjectInput{
       Bucket:          bucketName,
       Key:             dstObjectKey,
       SrcBucket:       bucketName,
       SrcKey:          srcObjectKey,
       ForbidOverwrite: true,
    })
    checkErr(err)
    fmt.Println("CopyObject Request ID:", output.RequestID)
}
```


<span id="e6505587"></span>
# Multipart Upload

The following code is used to prevent overwriting files with identical names during chunked upload:

```Go
package main

import (
    "context"
    "fmt"
    "io"
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
     
       bucketName = "*** Provide your bucket name ***"

      
       objectKey = "*** Provide your object name ***"
       ctx       = context.Background()
    )

    
    localFile := "/root/example.txt"
    fd, err := os.Open(localFile)
    checkErr(err)
    defer fd.Close()
    stat, err := os.Stat(localFile)
    checkErr(err)
    fileSize := stat.Size()
   
    partNumber := 1
  
    partSize := int64(20 * 1024 * 1024)
    offset := int64(0)

   
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    
    
    createMultipartOutput, err := client.CreateMultipartUploadV2(ctx, &tos.CreateMultipartUploadV2Input{
       Bucket:          bucketName,
       Key:             objectKey,
       ForbidOverwrite: true,
    })
    checkErr(err)
    fmt.Println("CreateMultipartUploadV2 Request ID:", createMultipartOutput.RequestID)
   
    fmt.Println("CreateMultipartUploadV2 Upload ID:", createMultipartOutput.UploadID)

   
    var parts []tos.UploadedPartV2
    for offset < fileSize {
       uploadSize := partSize
      
       if fileSize-offset < partSize {
          uploadSize = fileSize - offset
       }
       fd.Seek(offset, io.SeekStart)
       partOutput, err := client.UploadPartV2(ctx, &tos.UploadPartV2Input{
          UploadPartBasicInput: tos.UploadPartBasicInput{
             Bucket:     bucketName,
             Key:        objectKey,
             UploadID:   createMultipartOutput.UploadID,
             PartNumber: partNumber,
          },
          Content:       io.LimitReader(fd, uploadSize),
          ContentLength: uploadSize,
       })
       checkErr(err)
       fmt.Println("upload Request ID:", partOutput.RequestID)
       parts = append(parts, tos.UploadedPartV2{PartNumber: partNumber, ETag: partOutput.ETag})
       offset += uploadSize
       partNumber++
    }


 
  
    completeOutput, err := client.CompleteMultipartUploadV2(ctx, &tos.CompleteMultipartUploadV2Input{
       Bucket:          bucketName,
       Key:             objectKey,
       UploadID:        createMultipartOutput.UploadID,
       Parts:           parts,
       ForbidOverwrite: true,
    })
    checkErr(err)
    fmt.Println("CompleteMultipartUploadV2 Request ID:", completeOutput.RequestID)

}
```
