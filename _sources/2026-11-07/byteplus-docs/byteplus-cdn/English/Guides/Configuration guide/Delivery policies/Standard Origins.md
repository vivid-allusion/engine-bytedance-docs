---
title: "Standard Origins"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-configurations"
---

To ensure your CDN can fetch and cache your content, you must configure an origin after adding a domain.

This guide provides step\-by\-step instructions for setting up various origin types, including IP addresses, domain names, and object storage buckets. You will also learn how to configure advanced features like weighted load balancing between multiple origins and setting up primary/backup origins to improve the reliability of your content delivery.

<span id="steps"></span>
## Steps


1. Open the **Origins** tab. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Origin** to add an origin configuration.

   You must add at least one primary origin. A backup origin is optional.

3. Configure the origin according to the following instructions.

   * If the origin type is **IP Address** or **Domain Name**, refer to [Origin Configuration Instructions (for "IP Address" and "Domain Name" types)](https://docs.byteplus.com/en/docs/18/6551#ip-domain%EF%BC%89).

   * If the origin type is **Object Storage**, refer to [Origin Configuration Instructions (for "Object Storage" type)](https://docs.byteplus.com/en/docs/18/6551#46d92e6c).

4. After completing the configuration, click **Save** in the lower right corner of the page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the switching logic between primary and backup origins, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en">Origin Retry</a>.</div>


* <div data-tips="true" data-tips-type="tip">When making an origin request, CDN uses the same request method as the user request. By default, CDN supports the following request methods: DELETE, GET, HEAD, POST, PUT, PATCH, CONNECT, OPTIONS. You can configure disallowed HTTP methods in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-disallowed-http-method">Disallowed HTTP Methods</a>. For example, to prevent users from accidentally deleting files on the origin, you can disallow the DELETE method.</div>


* <div data-tips="true" data-tips-type="tip">For third\-party object storage bucket origins, to prevent users from mishandling the bucket, it is recommended that you perform the following operations:</div>


   * <div data-tips="true" data-tips-type="tip">At the cloud provider that provides the object storage service, set permissions for the corresponding account to prevent unintended operations.</div>



<span id="ip-domain"></span>
## Origin Configuration Instructions (for "IP Address" and "Domain Name" types)

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6a6a2cea0768cb57d8b61911775113cf.png) </span>


|**Configuration** |**Description** |
|---|---|
|Origin Address |Specifies one or more origin addresses. Multiple addresses are separated by semicolons (;) or newlines.<br><br><br>* When **Origin Type** is **IP Address**, you can enter IPv4 and IPv6 addresses.<br><br>* When **Origin Type** is **Domain Name**, the domain name you enter cannot be a wildcard domain.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a single domain, you can configure a maximum of 50 origin addresses across all primary and backup origins.</div><br> |
|Weight |Defines the origin weight, from 1 to 100. A higher weight increases the probability of the origin being selected for requests. For example, if you have defined two primary origins with weights of 3 and 2 respectively, the probability of the origin with a weight of 3 being selected is 60%. |
|HTTP Port |Represents the origin port that CDN accesses when using the HTTP protocol for origin requests. The value ranges from 1 to 65535, with a default value of `80`. If the origin does not accept HTTP requests, you can keep the default value for this configuration. See **Additional Notes on Port Configuration** below. |
|HTTPS Port |Represents the origin port that CDN accesses when using the HTTPS protocol for origin requests. The value for this configuration ranges from 1 to 65535, with a default value of `443`. If the origin does not accept HTTPS requests, you can keep the default value for this configuration. See **Additional Notes on Port Configuration** below. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Additional Notes on Port Configuration</strong></div>


<div data-tips="true" data-tips-type="tip">You can verify that your origin is listening on the configured port in the following ways.</div>



* <div data-tips="true" data-tips-type="tip">Windows: In the Command Prompt window, run the command <code>telnet <IP/domain> <port></code></div>


   <div data-tips="true" data-tips-type="tip">If the Telnet command line window opens, this indicates that the origin supports the configured protocol and port.   </div>
   

* <div data-tips="true" data-tips-type="tip">macOS and Linux: In the Terminal window, run the command <code>nc -vz -w 2 <IP/domain> <port></code></div>


   <div data-tips="true" data-tips-type="tip">If the command returns <code>Connection succeeded!</code>, it means the origin supports the configured protocol and port.   </div>
   


<span id="46d92e6c"></span>
## Origin Configuration Instructions (for "Object Storage" type)

Select your scenario and then configure it based on the description in the scenario.


* [Scenario 1: Bucket is from BytePlus](https://docs.byteplus.com/en/docs/18/6551#a8e62914)

* [Scenario 2: Bucket is from Alibaba Cloud or Tencent Cloud](https://docs.byteplus.com/en/docs/18/6551#8cb51a30)

* [Scenario 3: Bucket is from AWS or other cloud providers](https://docs.byteplus.com/en/docs/18/6551#8fd2d9ba) (such as Qiniu Cloud, Huawei Cloud, etc.)

* [Scenario 4: Bucket is from Azure](https://docs.byteplus.com/en/docs/18/6551#8134ebaf)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the bucket is from a third\-party cloud provider in Chinese Mainland, please pay attention to the relevant statements from the cloud provider. When a user accesses the bucket using the default bucket domain name, the cloud provider's default behavior may be:</div>



* <div data-tips="true" data-tips-type="tip">For files with specific extensions, the cloud provider will add the <code>Content-Disposition: attachment</code> header to the response, forcing the browser to download the file.</div>


* <div data-tips="true" data-tips-type="tip">Reject requests for APK and IPA files.</div>



<div data-tips="true" data-tips-type="tip">To allow users to preview files in the browser and download APK and IPA files, you need to create a custom domain in the cloud provider's object storage service, and then follow the <a href="https://docs.byteplus.com/en/docs/18/6551#8fd2d9ba">configuration steps in Scenario 3</a>.</div>


<span id="a8e62914"></span>
### Scenario 1: Bucket is from BytePlus

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If any of the following conditions allpy, follow the <a href="https://docs.byteplus.com/en/docs/18/6551#8fd2d9ba">configuration steps in Scenario 3</a>.</div>



* <div data-tips="true" data-tips-type="tip">Your bucket belongs to another BytePlus primary account.</div>


* <div data-tips="true" data-tips-type="tip">You need to access the bucket through a custom domain.</div>



<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f3dff7a305ee56e4562a91a2c2606483.png) </span>


|**Configuration** |**Description** |
|---|---|
|Bucket Source |Select **BytePlus TOS**. |
|Service Authorization |Indicates whether the current CDN has permission to perform cross\-service access to TOS.<br><br>&nbsp;<br><br>If the page displays **Authorize**, it means that authorization has not yet been granted. Please use the primary account to click this link to complete the authorization. |
|Bucket |Select a TOS bucket from the list as the origin. |
|Private Bucket Access |If the bucket is private, you need to enable this configuration. |
|Weight |Defines the origin weight, from 1 to 100. A higher weight increases the probability of the origin being selected for requests. For example, if you have defined two primary origins with weights of 3 and 2 respectively, the probability of the origin with a weight of 3 being selected is 60%. |


<span id="8cb51a30"></span>
### Scenario 2: Bucket is from Alibaba Cloud or Tencent Cloud

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to access the bucket through a custom domain, please follow the <a href="https://docs.byteplus.com/en/docs/18/6551#8fd2d9ba">configuration steps in Scenario 3</a>.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_67ab92133085cd910c78371de6d65739.png) </span>


|**Configuration** |**Description** |
|---|---|
|Bucket Source |Select **Third\-party Object Storage**. |
|Object Storage Provider |Select **Alibaba Cloud** or **Tencent Cloud**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the bucket is from Alibaba Cloud and the domain has enabled the "Range GET" feature, please apply the <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-range-get-cn#alibabacloud-oss-%E5%85%BC%E5%AE%B9%E9%85%8D%E7%BD%AE">AlibabaCloud OSS Compatible Configuration</a>.</div><br> |
|Bucket Address |Enter the bucket domain name assigned by the provider. For example: `my_bucket.oss-cn-beijing.aliyuncs.com`. |
|Private Bucket Access |If the bucket is private, you need to enable this configuration.<br><br>After this configuration is enabled, you need to provide access credentials. CDN will include a signature generated based on the credentials and other information in the origin request to access your private bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the security of the content on the origin, it is recommended that the access credentials you provide only include read\-only permissions for the bucket.</div><br> |
|AccessKey ID |Represents the AccessKey ID in the access credentials, called SecretId in Tencent Cloud. |
|AccessKey Secret |Represents the AccessKey Secret in the access credentials, called SecretKey in Tencent Cloud. |
|Weight |Defines the origin weight, from 1 to 100. A higher weight increases the probability of the origin being selected for requests. For example, if you have defined two primary origins with weights of 3 and 2 respectively, the probability of the origin with a weight of 3 being selected is 60%. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you save the origin configuration, the AccessKey ID and AccessKey Secret you entered previously will not be displayed by default on the origin list page. You need to click the show button to view them.</div>


<span id="8fd2d9ba"></span>
### Scenario 3: Bucket is from AWS or other cloud providers

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the bucket is not from Amazon S3, please first contact the cloud provider to obtain a bucket domain name that is compatible with the S3 authentication method.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_26ff3c4943e020a8613ad2868598914e.png) </span>


|**Configuration** |**Description** |
|---|---|
|Bucket Source |Select **Third\-party Object Storage**. |
|Object Storage Provider |Select **AWS or S3\-compatible storage**. |
|Bucket Address |Enter the bucket domain name assigned by the cloud provider, or the custom domain you set for the bucket. |
|Origin Hostname |Leaving it blank means it is the same as the bucket address. Custom Host input is supported. |
|Private Bucket Access |If the bucket is private, you need to enable this configuration.<br><br>After this configuration is enabled, you need to provide access credentials. CDN will include a signature generated based on the credentials and other information in the origin request to access your private bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the security of the content on the origin, it is recommended that the access credentials you provide only include read\-only permissions for the bucket.</div><br> |
|AccessKey ID |Represents the AccessKey ID in the access credentials. |
|AccessKey Secret |Represents the AccessKey Secret in the access credentials. |
|Weight |Defines the origin weight, from 1 to 100. A higher weight increases the probability of the origin being selected for requests. For example, if you have defined two primary origins with weights of 3 and 2 respectively, the probability of the origin with a weight of 3 being selected is 60%. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you save the origin configuration, the AccessKey ID and AccessKey Secret you entered previously will not be displayed by default on the origin list page. You need to click the show button to view them.</div>


<span id="8134ebaf"></span>
### Scenario 4: Bucket is from Azure

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cab4c4d6864151bc5ec1ed8cfae47a1c.png) </span>


|**Configuration** |**Description** |
|---|---|
|Bucket Source |Select **Third\-party Object Storage**. |
|Object Storage Provider |Select **Azure**. |
|Storage Account Name |Represents the name of your Azure storage account. |
|Endpoint |Represents the domain name of your Azure storage bucket (container), ending with `blob.core.windows.net`. |
|Private Bucket Access |If the bucket is private, you need to enable this configuration. |
|Shared Key |Represents the shared key (Key) of your Azure storage account. |
|Weight |Defines the origin weight, from 1 to 100. A higher weight increases the probability of the origin being selected for requests. For example, if you have defined two primary origins with weights of 3 and 2 respectively, the probability of the origin with a weight of 3 being selected is 60%. |


<span id="origin-protocol"></span>
## Origin Protocol

Under **Origin Protocol**, you can set the protocol used for origin requests. This configuration has the following options:


* HTTP: Indicates that origin requests always use the HTTP protocol.

* HTTPS: Indicates that origin requests always use the HTTPS protocol.

* Follow Protocol: Indicates that the protocol used for origin requests is the same as the protocol used for user requests.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_58963cfd9ee6a788dc379cc6f7ec42e3.png) </span>

<span id="origin-hostname"></span>
## Origin Hostname

If there are multiple sites on the origin server, you need to manually specify the hostname of the site that CDN needs to access.

This configuration is a global hostname setting and has a lower priority than the origin's hostname configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For origins where the <strong>Origin Type</strong> is <strong>Object Storage</strong>, this configuration does not take effect. This is because CDN has preset the cloud provider's hostname for these origins. The origin's hostname configuration has a higher priority than the global hostname configuration.</div>


Under **Origin Hostname**, you can set a global hostname. The length cannot exceed 1,024 characters. By default, the hostname is the same as the domain name.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_36fa18f5b668dcd11df4e1d797ef685d.png) </span>
