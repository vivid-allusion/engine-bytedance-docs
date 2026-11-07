---
title: "Setting a Static Website"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-up-a-static-website"
---

TOS supports hosting static websites. You can store all the content of a static website in a TOS bucket. After configuring static website rules, you can access the website through the bucket domain name. This article describes the specific steps for setting up static website rules in TOS.

<span id="98901ab8"></span>
## Background information

Static website, that is, all the content of the website is composed of static content, including the homepage, images, execution scripts, and so on. When setting up a static website rule, you need to specify the homepage of the website. You can also choose whether to specify a default 404 page, which will be returned by default if a 404 error occurs when visiting a website.

<span id="f8dfbb19"></span>
## Prerequisite

The website content has been uploaded to the bucket, and the file ACL or bucket policy is public reading. For the specific steps of uploading a file and setting the ACL, please refer to the following documents:


* [Uploading a File](https://docs.byteplus.com/docs/tos/docs-uploading-a-file)

* [Configuring a Bucket ACL](https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl)

* [Configuring an Object ACL](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl)


<span id="97602ede"></span>
## Precautions


* Only one static website hosting rule can be created in a bucket.

* After setting up a static website, you must bind a custom domain name to take effect. For details, see [Set up a Custom Domain Name](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name).

* For security compliance reasons, starting from October 18, 2022, if you use the default domain name of the bucket to access the webpage type file (mimetype is text/html, the extension includes HTM, HTML, JSP, PLG, HTX, STM), the Response Header will automatically add `Content-Disposition: attachment`, that is, when accessing the webpage type file from the browser, the website will not be previewed directly, but the content of the website will be downloaded locally.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to preview a webpage directly, you can bind a custom domain name to your bucket. When you access a web page type file with a bound custom domain name, you can directly preview the web page content. For specific steps,Please refer to<a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Set up a Custom Domain Name</a>.   </div>
   

<span id="c081dd27"></span>
## Configuration example

The static website function of TOS defaults to the function of the first page of the subdirectory, that is, when you visit the URL ending with a forward slash (/) under the root domain name, it will return the default first page of the corresponding directory.

For example, you have bound a custom domain name `www.test.com`for the bucket, and you have uploaded the home file `index.html`and the default 404 file `error.html`to the bucket, and the subdirectory `/subdir`has also uploaded the home file `index.html`, the access rules are as follows:


|**visit URL** |**Return result** |
|---|---|
|`http://www.test.com/` |Return to `http://www.test.com/index.html`. |
|`http://www.test.com/subdir/` |Return to `http://www.test.com/subdir/index.html`. |
|`http://www.test.com/test.jpg` |Get `the test.jpg`file normally. |
|`http://www.test.com/object` |If no `object`file exists in the bucket, `http://www.test.com/error.html`is returned. |


<span id="fc5b9b93"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane,select **Basic configurations \> Static website**.

4. On the **Static website** page, click **Set default page rules**.

5. In the dialog box that pops up, set the following parameters and click **Create**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Default homepage |Set the default homepage when visiting a static website, only `.html`format is supported. The example file is as follows:<br><br>```html```<br>```<html>```<br>```<head>```<br>```    <title>Home Page</title>```<br>```    <meta charset="utf-8">```<br>```</head>```<br>```<body>```<br>```  <h1>Welcome to TOS</h1>```<br>```  <p>Welcome to TOS</p>```<br>```</body>```<br>```</html>```<br> |
   |Default 404 page |The page returned when a 404 error occurs when accessing a file in the bucket is not required. The example file is as follows:<br><br>```html```<br>```<html>```<br>```<head>```<br>```    <title>Welcome to TOS</title>```<br>```    <meta charset="utf-8">```<br>```</head>```<br>```<body>```<br>```  <h1>Access Error</h1>```<br>```  <p>This is error 404 page.</p>```<br>```</body>```<br>```</html>```<br> |
   


<span id="820d7e63"></span>
## Other operations

Click **Delete** in the target rule **Actions** column, and in the pop\-up dialog box, click **Delete** to delete static website rule.
