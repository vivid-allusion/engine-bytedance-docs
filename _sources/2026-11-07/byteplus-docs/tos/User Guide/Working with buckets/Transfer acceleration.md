---
title: "Transfer acceleration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Transfer_acceleration"
---

The transfer acceleration feature utilizes the globally distributed nodes and the backbone network of BytePlus. It uses intelligent routing resolution technology to process requests from the nearest available locations. Combined with optimized network transmission protocols, it provides a secure, high\-quality, end\-to\-end network acceleration solution for TOS users. This topic covers use cases, notes, billing notes, and the steps for enabling and using the feature.

<span id="6697748b"></span>
## Use cases


* Cross\-border transfer of training dataset

   Companies engaged in AI training often have computing resources and datasets located far apart, which leads to slow network transfer of datasets. Enabling transfer acceleration can greatly increase the speed of large\-scale, cross\-border data transfers.

* Data transfer under poor network conditions

   As mobile internet technology has evolved, the use of mobile network communication technologies to access the internet has grown. However, users often cannot maintain optimal network performance in areas with poor base station coverage, on transportation such as high\-speed trains and subways, and in harsh environments such as mountains and deserts. The transfer acceleration feature uses optimized network transmission protocols to provide users with relatively smooth upload and download experiences under poor network conditions.

   If your business primarily targets mobile internet users, using the transfer acceleration feature can give your application more competitive edge.

* Long\-distance transfer of static data

   If your users are located across the country, you can use the transfer acceleration feature to enhance their experience with long\-distance network access. This feature is useful for activities such as downloading game installation packages, uploading and downloading photo albums, and uploading and downloading files to a cloud drive.


<span id="30ae98d3"></span>
## Billing notes

Different charges apply when you use the transfer acceleration feature, depending on the scenario. Common scenarios are explained below:


* If you use transfer acceleration when uploading objects, TOS will charge you for requests and transfer acceleration.

* If you use transfer acceleration when downloading objects, TOS will charge you for requests, data transfer, and transfer acceleration.

* If you use transfer acceleration for replication between regions inside and outside of the Chinese mainland, TOS will charge you for requests, data transfer, and transfer acceleration.


For transfer acceleration pricing, see [Transfer acceleration](https://docs.byteplus.com/en/docs/tos/transfer-acceleration-fee).

<span id="bebdafe7"></span>
## Notes


|**Category** |Description |
|---|---|
|Billing |Fees are only charged when the transfer acceleration feature is used. Enabling the feature without using it will not incur any charges. |
|Permissions |Only the bucket owner or a user with the "tos:PutBucketTransferAcceleration" permission can configure transfer acceleration. For more information, see [Configuring IAM policies](https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy). |
|Effective time |After you enable or disable transfer acceleration, it may take up to 30 minutes for the changes to take effect. |
|Logging |To ensure data transfer security, the transfer acceleration feature may use the HTTPS protocol, even if the client accesses TOS via HTTP. Logs may show HTTPS instead of HTTP. |
|Network |* Transfer acceleration is compatible with public networks but not private networks.<br><br>* Transfer acceleration only supports the IPv4 protocol and does not support dual\-stack.<br><br>* The default bandwidth limit is 5 Gbps. [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) if you need more bandwidth. |
|Usage |* After enabling transfer acceleration, you can access TOS through two types of domain names. Only transfer acceleration domain names provide acceleration benefits. The specific domain formats are as follows:<br><br>   * Default domain: <bucketname\>.tos\-<Region\>.volces.com<br><br>   * Transfer acceleration domain: <bucketname\>.tos\-accelerate.volces.com and <bucketname\>.tos\-s3\-accelerate.volces.com<br><br>* Access to TOS will fail if you attempt to use the transfer acceleration domain names without enabling the transfer acceleration feature. |
|Availability |* Transfer acceleration is not supported for ListBuckets, CopyObject, and same\-region replication operations.<br><br>* Transfer acceleration is only available for replication between regions inside and outside of the Chinese mainland. Once enabled for such scenarios, you cannot disable transfer acceleration. Transfer acceleration is not available for replication between regions within the Chinese mainland. |


<span id="e67c338c"></span>
## Enabling transfer acceleration


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to configure.

3. In the left navigation pane, select **Domain name and transfer acceleration ** \> **Transfer acceleration**.

4. On the **Transfer acceleration** page, click **Edit**. Then, click **Enable** and **Select**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your bucket is located in China (Hong Kong) or Asia Pacific (Johor), you must read and check the box for <strong>Compliance commitment</strong>.   </div>
   

5. In the **Make sure to turn on transfer acceleration** dialog, click **Save**.

   Wait 30 minutes for transfer acceleration to take effect. Thank you for your patience.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To disable transfer acceleration, navigate to the <strong>Transfer acceleration</strong> page, and click <strong>Edit</strong>. Then, click <strong>Close</strong> and <strong>Select</strong>. Finally, click <strong>Save</strong> in the box that appears.   </div>
   

<span id="1d9b0b85"></span>
## Using transfer acceleration

The default domain names for transfer acceleration are tos\-accelerate.volces.com and tos\-s3\-accelerate.volces.com. After enabling transfer acceleration, you can also obtain these domain names on the **Transfer acceleration** page. You can then use these domain names to access TOS.


<Tabs>
<Tab zoneid="AVIBnNNMI7" title="API">
<TabTitle>API</TabTitle>

To speed up data transfers when accessing TOS via APIs, replace the domain in the `Host` request with the transfer acceleration domain name. The following example uses the GetObject operation to illustrate this process.

```JSON
GET /objectName HTTP/1.1
Host: bucketname.tos-accelerate.volces.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```



</Tab>
<Tab zoneid="K4hDbyzIO9" title="SDK">
<TabTitle>SDK</TabTitle>

To speed up data transfers when accessing TOS via SDKs, replace the `endpoint` in each language with the transfer acceleration domain name. The following example shows how to upload a local file using Go SDK. For more information, see [SDK overview](https://docs.byteplus.com/docs/tos/SDK-overview).

```Go
package mainimport (   "context"   "fmt"   "github.com/volcengine/ve-tos-golang-sdk/v2/tos")func checkErr(err error) {   if err != nil {      if serverErr, ok := err.(*tos.TosServerError); ok {         fmt.Println("Error:", serverErr.Error())         fmt.Println("Request ID:", serverErr.RequestID)         fmt.Println("Response Status Code:", serverErr.StatusCode)         fmt.Println("Response Header:", serverErr.Header)         fmt.Println("Response Err Code:", serverErr.Code)         fmt.Println("Response Err Msg:", serverErr.Message)      } else if clientErr, ok := err.(*tos.TosClientError); ok {         fmt.Println("Error:", clientErr.Error())         fmt.Println("Client Cause Err:", clientErr.Cause.Error())      } else {         fmt.Println("Error:", err)      }      panic(err)   }}func main() {   var (      accessKey = os.Getenv("TOS_ACCESS_KEY")      secretKey = os.Getenv("TOS_SECRET_KEY")      // For transfer acceleration, use the transfer acceleration endpoint      endpoint = "https://tos-accelerate.volces.com"      region   = "cn-beijing"      // Provide your bucket name      bucketName = "*** Provide your bucket name ***"      // Upload the file to example.txt in the example_dir directory      objectKey = "example_dir/example.txt"      ctx       = context.Background()   )   // Initialize client   client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))   checkErr(err)   // Upload the file directly using local file path   output, err := client.PutObjectFromFile(ctx, &tos.PutObjectFromFileInput{      PutObjectBasicInput: tos.PutObjectBasicInput{         Bucket: bucketName,         Key:    objectKey,      },      FilePath: "./example.txt",   })   checkErr(err)   fmt.Println("PutObjectV2 Request ID:", output.RequestID)}
```



</Tab>
<Tab zoneid="GSfbLRrQSe" title="tosutil">
<TabTitle>tosutil</TabTitle>

When using the `config` command for initial configuration, set the Endpoint to the transfer acceleration domain name. For instructions, see [Step 1: Initial configuration](https://docs.byteplus.com/docs/tos/Quick-start#.5q2l6aqk5LiA77ya5Yid5aeL5YyW6YWN572u). Example:

```JSON
# The -i parameter specifies the account/sub-account access key
# The -k parameter specifies the account/sub-account secret key
# The -e parameter specifies the endpoint
# The -re parameter specifies the region
./tosutil config -i <access key> -k <secret key> -e tos-accelerate.volces.com -re <region>
```


After completing the initial configuration, you can speed up data transfers in tosutil.


</Tab>
<Tab zoneid="qGkM0OKkTS" title="Other browsers">
<TabTitle>Other browsers</TabTitle>

To speed up data transfers when accessing TOS from other browsers, replace the default domain name in the file URL with the transfer acceleration domain name. For example, replace `https://bucketname.tos-cn-beijing.volces.com/abc.jpg` with `https://bucketname.tos-accelerate.volces.com/abc.jpg`.


</Tab>
</Tabs>


<span id="29595359"></span>
## Observability


<Tabs>
<Tab zoneid="vXt4Vw4kAL" title="Log analysis">
<TabTitle>Log analysis</TabTitle>

Logs record access requests to TOS. When the log field `RequestSourceType` is `accelerate`, it indicates that the request is for transfer acceleration. You can use this field to query the request time, source IP address, and requested object key. For more information, see [Log analysis](https://docs.byteplus.com/docs/tos/Log-analysis).


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. In the **Buckets** list, click the bucket you want to configure.

3. In the left navigation pane, click **Logging**.

4. On the **Search Analysis** tab, set the time range for the query, enter `RequestSourceType:accelerate` in the search box, and click **Search**.

   On the **Raw log** tab, view the log details related to transfer acceleration requests, including request time, source IP address, and account ID.


</Tab>
<Tab zoneid="PXP3OFMqS4" title="Transfer acceleration traffic statistics">
<TabTitle>Transfer acceleration traffic statistics</TabTitle>

TOS supports statistics on transfer acceleration traffic. On the **Usage statistics** page, you can view metrics such as Transfer Acceleration Inflow Traffic (Chinese mainland to Chinese mainland) and Transfer Accelerated Outflow Traffic (outside the Chinese mainland to Chinese mainland) for a specific period. For more information, see [Usage statistics](https://docs.byteplus.com/docs/tos/docs-usage-statistics).


</Tab>
</Tabs>


<span id="02dc8025"></span>
## FAQs


* How does the transfer acceleration feature differ from using BytePlus Global Accelerator with TOS's default domains?

   The transfer acceleration feature offers simpler and more flexible operations than using the BytePlus Global Accelerator with TOS's default domains. You can increase transfer speeds with one click, without preparing domain names in advance.

* Can the transfer acceleration feature be used with BytePlus Content Delivery Network (CDN) for downloads?

   Yes. Combining the transfer acceleration feature with CDN improves the speed and success rate of back\-to\-origin requests.
