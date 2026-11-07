---
title: "Use a single-region access point"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Use-a-single-region-access-point"
---

After a single\-region access point is successfully created, TOS will automatically generate an alias. You can share the alias with other users, allowing them to access resources within TOS via the alias of a single\-region access point. This article describes the procedure for accessing resources within TOS using a single\-region access point.

<span id="9f2421d8"></span>
## Alias Description

After a single\-region access point is created successfully, TOS will automatically generate an access point alias. The alias is always unique and cannot be modified. When accessing a TOS bucket, you must specify the bucket name in the request. When accessing a storage bucket through a single\-region access point, you must use an alias instead of the bucket name. TOS will automatically route requests to the corresponding storage bucket using the alias.

<span id="3f75562a"></span>
## Supported Operations

When accessing TOS through a single\-region access point, only certain operations on TOS are supported. For detailed information, please refer to [API operations supported by single-region access points](https://docs.byteplus.com/docs/tos/API-operations-supported-by-single-region-access-point).

<span id="7df5a5f6"></span>
## Precautions

Single\-region access points do not support anonymous access.

<span id="2700440a"></span>
## Operating Procedures


<Tabs>
<Tab zoneid="RWZaF9Ikk0" title="When calling the API, access bucket resources through a single-region access point.">
<TabTitle>When calling the API, access bucket resources through a single-region access point.</TabTitle>

1. Obtain the alias of a single\-region access point.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

   4. Obtain the **access point alias** from the **Basic information** section under the **Overview** tab.

2. Use a single\-region access point.

   When accessing TOS via API, you need to replace the request `Host` with `<Alias>.<TOS Endpoint>`, while keeping the original configuration method for other parameters. This enables you to access resources within TOS using a single\-region access point. For a detailed introduction to the API documentation, please refer to the [API Overview](https://docs.byteplus.com/docs/tos/reference-api-overview).

   The following example uses GetObject to demonstrate how to download the ai.png object using the alias `test-01976881ee547ed28a05b5ecaf93****-tosalias`.

   ```JSON
   GET /ai.png HTTP/1.1
   Host: test-01976881ee547ed28a05b5ecaf93****-tosalias.tos-cn-beijing.bytepluses.com.cn
   Date: Fri, 30 Jul 2021 08:05:36 GMT
   Authorization: authorization string
   ```
   


</Tab>
<Tab zoneid="iLEf9bV8Bn" title="When calling the SDK, access bucket resources via a single-region access point.">
<TabTitle>When calling the SDK, access bucket resources via a single-region access point.</TabTitle>

1. Obtain the alias of a single\-region access point.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

   4. Obtain the **access point alias** from the **Basic information** section under the **Overview** tab.

2. Use a single\-region access point.

   When accessing TOS using the SDK, you need to replace the **bucket name** in the SDK code with the **alias** obtained in Step 1. Keep the other parameters as originally configured to enable the single\-region access point feature. For a detailed introduction to the SDK documentation, please refer to [SDK Overview](https://docs.byteplus.com/docs/tos/SDK-overview).

   The following example uses the Go programming language to demonstrate how to use the `test-01976881ee547ed28a05b5ecaf93****-tosalias` alias to download the `example_dir/example.txt` file from TOS to the local machine.

   ```JSON
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
         // Endpoint for the Bucket – For example, for North China 2 (Beijing): https://tos-cn-beijing.volces.com 
         endpoint = "https://tos-cn-beijing.bytepluses.com.cn"
         region   = "cn-beijing"
         // Enter the BucketName
         bucketName = "test-01976881ee547ed28a05b5ecaf93****-tosalias"
   
         // Download a file with a specified filename
         objectKey = "example_dir/example.txt"
         ctx       = context.Background()
      )
      // Initialize the client
      client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
      checkErr(err)
   
      // Download the file to a specified path – In this example, the file is downloaded to example_dir/example.txt 
      getObjectToFileOutput, err := client.GetObjectToFile(ctx, &tos.GetObjectToFileInput{
         GetObjectV2Input: tos.GetObjectV2Input{
            Bucket: bucketName,
            Key:    objectKey,
         },
         FilePath: "example_dir/example.txt",
      })
      checkErr(err)
      fmt.Println("GetObjectToFile Request ID:", getObjectToFileOutput.RequestID)
      fmt.Println("GetObjectToFile File Size:", getObjectToFileOutput.ContentLength)
   }
   ```
   


</Tab>
<Tab zoneid="mPzhgSpysQ" title="When using tosutil, access resources within a bucket via a single-region endpoint.">
<TabTitle>When using tosutil, access resources within a bucket via a single-region endpoint.</TabTitle>

1. Obtain the alias of a single\-region access point.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation bar, select **Access Point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, click the name of the target single\-region access point.

   4. Obtain the **access point alias** from the **Basic information** section under the **Overview** tab.

2. After replacing the **bucket name** in the command with the **alias** obtained in Step 1 and keeping the other parameters as originally configured, you can use the single\-region access point feature. For a detailed introduction to tosutil, see [Quick Start](https://docs.byteplus.com/docs/tos/Quick-start).

   The following example demonstrates how to use the alias `test-01976881ee547ed28a05b5ecaf93****-tosalias` to download the `object1.png` file from TOS to the local system.

   ```Bash
   ./tosutil cp tos://test-01976881ee547ed28a05b5ecaf93****-tosalias/object1.png /Users/Downloads/TOS/tosutil
   ```
   


</Tab>
</Tabs>
