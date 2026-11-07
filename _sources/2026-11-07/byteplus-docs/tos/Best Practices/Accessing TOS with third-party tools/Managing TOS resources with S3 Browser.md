---
title: "Managing TOS resources with S3 Browser"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-managing-tos-resources-with-s3-browser"
---

This topic describes how to manage TOS resources with S3 Browser.

<span id="212bc93b"></span>
## Background

S3 Browser is a free Windows client for [Amazon S3](http://aws.amazon.com/s3/). TOS is compatible with the S3 protocol, so you can manage your TOS resources using S3 Browser.

For more information on S3 Browser, visit the [official website](https://s3browser.com/).

<span id="727cbf02"></span>
## Prerequisites


* You have created a BytePlus account and activated TOS.

* You have obtained the access key ID and secret access key of the current account.

* For more information on S3 endpoints of TOS for public network access, see [Regions and Endpoints](https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0).


<span id="6a876f6b"></span>
## Installation and configuration instructions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section describes how to install and configure S3 Browser 10.3.1.</div>



1. Download S3 Browser [here](https://s3browser.com/download.aspx).

2. Then, double\-click the exe file to install.

3. Open the software and choose **Accounts \> Add new account** in the upper\-left corner of the interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d22797d728f46b195310ec257ece76a~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add New Account** pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Display name |Set the name to be displayed. |
   |Account type |Select **S3 Compatible Storage**. |
   |REST Endpoint |Set the S3 endpoint for TOS, for example, `tos-s3-ap-southeast-1.bytepluses.com`. For more information on TOS endpoints, see [Regions and Endpoints](https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0). |
   |Access Key ID |Set the access key ID. |
   |Secret Access Key |Set the secret access key. |
   |Encrypt Access Keys with a password |Use the default value. |
   |Use secure transfer (SSL/TLS) |Use the default value. |
   

5. Click **Advanced S3\-compatible storage settings** at the bottom. In the pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Signature version |Select **Signature V4**. |
   |Addressing model |Select **Virtual hosted style**. |
   |Override storage regions |Use the default value. |
   |Region\-specific endpoint (optional) |Use the default value. |
   

6. Then, click **Add new account** to save the configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your key has the ListBuckets permission, you can see a list of buckets under the account.   </div>
   

<span id="5b17e316"></span>
## Common operations

<span id="8d9bd727"></span>
### Uploading files


* To upload one or more files, click **Files \> Upload file(s)**  at the top of the interface.

* To upload one or more folders, click **Files \> Upload folder(s)**  at the top of the interface.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36e8f8b20a3240db96c4661b57e69458~tplv-goo7wpa0wc-image.image) </span>

<span id="c3a005b9"></span>
### Downloading files

Select the target file or folder, click **Files \> Download** at the top of the interface, and select the download path.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3821443b98204d20ba74fd39e0b026c7~tplv-goo7wpa0wc-image.image) </span>

<span id="6288dedf"></span>
### Renaming files


1. Select the target file and click **Files \> Rename** at the top of the interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f2a21461efd414e839667b016cf2593~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up dialog box, type the new filename and click **Rename**.


<span id="06849714"></span>
### Adding an external bucket

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You may need to add an external bucket in the following scenarios:</div>



* <div data-tips="true" data-tips-type="tip">Account A owns BucketA and grants account B access to it, and account B needs to access BucketA in S3 Browser.</div>


* <div data-tips="true" data-tips-type="tip">Account A grants IAM user B access to BucketA only, and IAM user B needs to access BucketA in S3 Browser.</div>



Add an external bucket using S3 Browser in the following steps.


1. Click **Buckets \> Add External Bucket** at the top of the interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/429909c225c84976ab17b349d670f7f5~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up dialog box, type the path of the external bucket and click **Add External bucket**.
