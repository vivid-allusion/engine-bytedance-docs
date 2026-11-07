---
title: "Using TOS accelerators"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Using-tos-accelerators"
---

Once you have set up a TOS accelerator, any requests for resources within the acceleration scope, made via accelerated domain names, are automatically forwarded to the accelerator. There, access is accelerated. This topic introduces notes and steps for using TOS accelerators.

## Notes

* You can only access your bucket via accelerated domain names from the private network. Access from the public network is not supported.

* To achieve optimal results, deploy your client and accelerator within the same available zone.

## Alias

The TOS accelerator uses the domain\-name\-based traffic steering capability of a single\-region access point to direct requests. Once a single\-region access point is created, TOS automatically generates an alias. This alias is always unique and cannot be modified. Accessing bucket resources typically requires including the bucket name in the request. However, when accessing resources within the acceleration scope, you do not need to specify the bucket name. Instead, specify the single\-region access point alias associated with your accelerator. TOS will then route the request to the resource through the alias.

## Steps

You can use your accelerator to speed up access through APIs or SDKs, or via FSX. The steps are as follows:

**Use the accelerator via APIs**

1. Obtain the single\-region access point alias.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation pane, select **Access point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, locate the alias you need in the **Alias** column.

2. Use your accelerator via APIs.

   When using the accelerator via APIs, replace `Host` with `<alias>.<TOS endpoint>`. The following example uses the GetObject operation. For more API documentation, see [API overview](https://docs.byteplus.com/docs/tos/reference-api-overview).

   > **tip**

   > TOS only forwards requests to the accelerator when they are sent to resources included in the [acceleration strategy](https://docs.byteplus.com/docs/tos/Creating-tos-accelerators). Requests sent to other resources are not directed to the accelerator, but are forwarded directly to TOS. Therefore, when using the accelerator, ensure that requests are sent specifically to the resources it accelerates; otherwise, it will not function.

   ```JSON
   GET /image/test.jpg HTTP/1.1
   Host: example-0196a48a48937a6db124a80ec141****-tosalias.tos-ap-southeast-1.ibytepluses.com
   Date: Fri, 30 Jul 2021 08:05:36 GMT
   Authorization: authorization string
   ```

**Use the accelerator via SDKs**

1. Obtain the single\-region access point alias.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation pane, select **Access point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, locate the alias you need in the **Alias** column.

2. Use your accelerator via SDKs.

   When using the accelerator via SDKs, replace `bucketName` with the **alias** obtained in Step 1. The following example uses Go to demonstrate how to download data to a local file. For more information, see [SDK overview](https://docs.byteplus.com/docs/tos/SDK-overview).

   > **tip**

   > TOS only forwards requests to the accelerator when they are sent to resources included in the [acceleration strategy](https://docs.byteplus.com/docs/tos/Creating-tos-accelerators). Requests sent to other resources are not directed to the accelerator, but are forwarded directly to TOS. Therefore, when using the accelerator, ensure that requests are sent specifically to the resources it accelerates; otherwise, it will not function.

   ```Go
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
         // Bucket endpoint，e.g., https://tos-cn-beijing.ivolces.com (for China (Beijing))
         endpoint = "https://tos-ap-southeast-1.ibytepluses.com"
         region   = "ap-southeast-1"
         // Enter the access point alias
         bucketName = "apc-01971ef8e4c47d14b3a31cd1aa22****-tosalias"
   
         // Download a file with the specified object key
         objectKey = "example_dir/example.txt"
         ctx       = context.Background()
      )
      // Initialize client
      client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
      checkErr(err)
   
      // Download the file to specified path, e.g., example_dir/example.txt
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

**Use the accelerator via FSX**

1. Obtain the single\-region access point alias.

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation pane, select **Access point \> Single\-Region Access Point**.

   3. On the **Single\-Region Access Point** page, locate the alias you need in the **Alias** column.

2. Use your accelerator via FSX.

   When mounting a bucket to a Linux system via FSX, replace the bucket name with the **alias** obtained in Step 1. Once you have successfully mounted the bucket, you can use the accelerator on Linux.

   The following example shows how to mount a bucket. For more information, see [FSX Configuration and Mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting).

   > **tip**

   > TOS only forwards requests to the accelerator when they are sent to resources included in the [acceleration strategy](https://docs.byteplus.com/docs/tos/Creating-tos-accelerators). Requests sent to other resources are not directed to the accelerator, but are forwarded directly to TOS. Therefore, when using the accelerator, ensure that requests are sent specifically to the resources it accelerates; otherwise, it will not function.

   ```Plain
   mount -t fsx /tos/<alias> <mount point> -o region="<your region>",endpoint="<your TOS endpoint>",access_key_id="AK",secret_access_key="SK",no_writeback_cache
   ```
