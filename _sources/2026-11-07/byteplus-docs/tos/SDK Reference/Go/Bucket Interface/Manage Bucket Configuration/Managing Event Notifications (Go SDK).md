---
title: "Managing Event Notifications (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-event-notifications-go-sdk"
---

If you wish to monitor resource changes in TOS in real time, you can configure event notification rules using the Go SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Only the bucket Owner can create event notification services.

* Setting up event notifications requires reliance on function services. You must first create and publish a function service in Volcengine. For detailed instructions, refer to [Create Function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection) and [Publish Function](https://docs.byteplus.com/en/docs/faas/Release_function).


<span id=".6K6-572u5LqL5Lu26YCa55-l"></span>
## **Configure Event Notifications**

The following code is used to configure event notification rules for the bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   input := &tos.PutBucketNotificationInput{Bucket: bucketName,
      CloudFunctionConfigurations: []tos.CloudFunctionConfiguration{
         {
            
            ID: "TestNotification",
       
            Events: []string{"tos:ObjectCreated:Put"},
           
            Filter: tos.Filter{Key: tos.FilterKey{Rules: []tos.FilterRule{{
               Name:  "prefix",
               Value: "test-",
            }, {
               Name:  "suffix",
               Value: "-ci",
            }}}},
        
            CloudFunction: "Provide the ID of your cloud function",
         },
      }}
   out, err := client.PutBucketNotification(ctx, input)
   checkErr(err)
   fmt.Println("Request ID:", out.RequestID)

}
```


<span id=".6I635Y-W5LqL5Lu26YCa55-l"></span>
## **Get Event Notifications**

The following code is used to retrieve the event notification rules of a bucket.

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
      ctx        = context.Background()
   )

   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)

   out, err := client.GetBucketNotification(ctx, &tos.GetBucketNotificationInput{Bucket: bucketName})
   checkErr(err)
   fmt.Println("Request ID:", out.RequestID)
   for _, conf := range out.CloudFunctionConfigurations {
  
      fmt.Println("Cloud Function Configuration ID:", conf.ID)
  
      fmt.Println("Cloud Function Configuration Events", conf.Events)

      fmt.Println("Cloud Function Configuration Filter", conf.Filter)

      fmt.Println("Cloud Function Configuration CloudFunction", conf.CloudFunction)
   }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For more information about event notifications, see [Event Notifications](https://docs.byteplus.com/docs/tos/Event-notification-overview).
