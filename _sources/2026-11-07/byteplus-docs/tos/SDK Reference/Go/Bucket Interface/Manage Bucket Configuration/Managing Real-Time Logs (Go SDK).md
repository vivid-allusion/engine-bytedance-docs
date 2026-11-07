---
title: "Managing Real-Time Logs (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-real-time-logs-go-sdk"
---

TOS supports log analysis functionality and enables retrieval and analysis of access logs generated during your interactions with TOS through the log service. You can configure log analysis features using the TOS Go SDK.

<span id=".6K6-572u5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Configure Real\-Time Log Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use the log analysis feature, you must have enabled the log service and authorized TOS to access the BytePlus Log Service (TLS).</div>


* <div data-tips="true" data-tips-type="warning">After the log analysis feature is enabled, the log service will automatically create log projects and topics to store logs related to TOS.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to configure the bucket's real\-time log configuration rules.

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
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   input := &tos.PutBucketRealTimeLogInput{
      Bucket: bucketName,
      Configuration: tos.RealTimeLogConfiguration{
    
         Role: "TOSLogTLSRole",
      
         Configuration: tos.AccessLogConfiguration{
            UseServiceTopic: true,
            TLSProjectID:    "TLSProjectID",
            TLSTopicID:      "TLSTopicID",
         },
      },
   }
   output, err := client.PutBucketRealTimeLog(context.Background(), input)
   checkErr(err)
   fmt.Println("PutBucketRealTimeLog Request ID:", output.RequestID)
}
```


<span id=".6I635Y-W5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Retrieve Real\-Time Log Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To access the real\-time log configuration rules for a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to retrieve the real\-time log configuration rules for the bucket.

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
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   output, err := client.GetBucketRealTimeLog(context.Background(), &tos.GetBucketRealTimeLogInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("GetBucketRealTimeLog Request ID:", output.RequestID)

   fmt.Println("GetBucketRealTimeLog Role", output.Configuration.Role)
   fmt.Println("GetBucketRealTimeLog TLSTopicID", output.Configuration.Configuration.TLSTopicID)
   fmt.Println("GetBucketRealTimeLog TLSProjectID", output.Configuration.Configuration.TLSProjectID)
   fmt.Println("GetBucketRealTimeLog UseServiceTopic", output.Configuration.Configuration.UseServiceTopic)

}
```


<span id=".5Yig6Zmk5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Delete Real\-Time Log Configuration Rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the real\-time log configuration rules of a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code is used to delete the real\-time log configuration rules of a bucket.

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
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   output, err := client.DeleteBucketRealTimeLog(context.Background(), &tos.DeleteBucketRealTimeLogInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("DeleteBucketRealTimeLog Request ID:", output.RequestID)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about real\-time log configuration, see [Log Analysis](https://docs.byteplus.com/docs/tos/Log-analysis).
