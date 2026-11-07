---
title: "Using pre-signed URLs for secure data downloads"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Use-temporary-authorization-url-to-enable-secure-data-download"
---

You can access TOS through a temporary URL to securely upload and download data. This article explains the solution and steps for using temporary authorization URLs to access TOS.

<span id=".5Zy65pmv6K-05piO"></span>
## Scenario description

In applications such as video surveillance, apps, and web, many images, files, videos, and other data often need to be uploaded to the server or downloaded locally for use. In these scenarios, you can leverage the HTTP access features of object storage to implement low\-cost, high\-quality data transmission. Additionally, TOS's serverless service naturally adapts to business growth or reduction, ensuring flexible scaling.

<span id=".5pa55qGI6K-05piO"></span>
## Solution description

<span id=".5pa55qGI5qaC6L-w"></span>
### Solution overview


1. APP Server first creates an IAM sub\-user, authorizes the sub\-user with permissions to access the object storage bucket and its objects, and obtains the sub\-user's AK and SK information.

2. When the terminal requests a temporary URL from APP Server, APP Server generates a time\-limited authorization URL based on upload or download actions; meanwhile, it records the uploaded or downloaded object in the database for business use.

3. After obtaining the temporary URL, the terminal interacts with TOS service using this URL to perform upload or download operations.

4. After receiving the request, TOS server communicates with IAM to get the corresponding key, then uses it to calculate the signature and compares it with the client's request to verify validity; if valid, it proceeds with business processing.

5. The terminal receives the processing result of the request, and the process ends.


<span id=".5LyY5Yqj5Yq_"></span>
### Advantages and disadvantages

The advantages and disadvantages of using temporary URLs for upload and download solutions are as follows.


|Advantages and disadvantages |Details |
|---|---|
|Advantages |1. Temporary URL signs authenticate at the object level, ensuring high security.<br><br>2. Terminal development only requires support for sending HTTP requests, making development simple and fast.<br><br>3. Terminals do not need to support various cloud providers' object storage interfaces, enabling multi\-cloud business switching. |
|Disadvantages |1. Each request requires a server\-side signature, increasing server load as the number of terminals grows.<br><br>2. Concurrent uploads are difficult, which is unfavorable for uploading large files. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* Create an IAM user, grant the appropriate permissions, and obtain AKSK. For detailed steps, refer to the following documentation:

   1. [Create an IAM user](https://docs.byteplus.com/docs/byteplus-platform/docs-creating-a-user)

   2. [Grant permissions to the IAM user](https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy)

   3. [View AK and SK information](https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey)

* Create a TOS bucket and plan data storage regions such as folders based on business needs. For detailed steps, refer to the following documentation:

   1. [Creating a Bucket](https://docs.byteplus.com/docs/tos/docs-create-a-bucket)

   2. [Creating a Folder](https://docs.byteplus.com/docs/tos/docs-creating-a-folder)


<span id=".5a6e5pa95q2l6aqk"></span>
### Implementation steps

<span id=".5q2l6aqk5LiA77yaYXBwLXNlcnZlci3lvIDlj5HphY3nva4="></span>
#### Step 1: APP Server development configuration


1. Obtain SDKs for different languages according to business needs.

   Choose the TOS SDK matching the development language of your APP Server architecture to speed up the development process.

   For SDK languages supported by TOS, refer to [SDK Overview](https://docs.byteplus.com/docs/tos/SDK-overview).

2. Business code integration and development.

   This article uses Go language as an example to explain how to generate temporary URLs for downloading objects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For sample code generating temporary URLs in other languages, see <a href="https://docs.byteplus.com/docs/tos/SDK-overview">SDK Overview</a>.   </div>
   

```go
package main

import (
   "context"
   "fmt"
   "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)
func checkErr(err error) {
   if err != nil {
      if ServerErr, ok := err.(*tos.TosServerError); ok {
         fmt.Println("Error:", ServerErr.Error())
         fmt.Println("Request ID:", ServerErr.RequestID)
         fmt.Println("Response Status Code:", ServerErr.StatusCode)
         fmt.Println("Response Header:", ServerErr.Header)
         fmt.Println("Response Err Code:", ServerErr.Code)
         fmt.Println("Response Err Msg:", ServerErr.Message)
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
      accessKey = "*** Provide your access key ***"
      secretKey = "*** Provide your secret key ***"
      // Bucket's corresponding Endpoint, example for Asia Pacific (Johor): https://tos-ap-southeast-1.bytepluses.com
      endpoint = "https://tos-ap-southeast-1.bytepluses.com"
      region   = "ap-southeast-1" // Specify RegionID
      bucketName = "*** Provide your bucket name ***"
      objectKey = "example_dir/example.txt" 
      ctx       = context.Background()
      // Full path of the local file, e.g., usr/local/testfile.txt
      fileName = "/usr/local/testfile.txt"
   )
   // Initialize client
   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
   checkErr(err)
   // Set request method, bucket object name, expiry time
   respTempUrl, errURL := client.PreSignedURL(&tos.PreSignedURLInput{
         HTTPMethod: enum.HttpMethodGet,
         Bucket: bucketName,
         Key: objectKey,
         Expires: 3600,  // in seconds. 
   })

   checkErr(errURL)
   fmt.Println(respTempUrl.SignedUrl)
}
```


<span id=".5q2l6aqk5LqM77ya5a6i5oi356uv6K-35rGC5Y-R6YCB"></span>
#### Step 2: Sending client requests

This article uses Browser.js code to demonstrate how to send requests from the client.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When developing with the Web version, configure Cross\-Origin Resource Sharing (CORS). For detailed steps, see <a href="https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings">CORS rules</a>.</div>


```json
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
    $(document).ready(function(){
    const Url='https://jsonplaceholder.typicode.com/posts'
        $('.btn').click(function(){
            $.ajax({
                url: Url,
                type: "GET",
                success: function(result){
                console.log(result)
            },
            error:function(error){
            console.log(`Error ${error}`)
            }
            })
        })
     })
 </script>
```
