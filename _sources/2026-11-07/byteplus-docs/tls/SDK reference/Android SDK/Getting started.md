---
title: "Getting started"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_android_getting_started"
---

This topic describes how to use Torch Log Service (TLS) SDK for Android to quickly collect logs.

<span id="前提条件"></span>
## Before you begin


* Install TLS SDK for Android. For more information, refer to [Install TLS SDK for Android](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_android).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="注意事项"></span>
## Precautions

Uploading logs to TLS is based on the http protocol. For Android 11.0, if HttpUrlConnection is used in an HTTP request, the following exception occurs:

```Shell
W/System.err: java.io.IOException: Cleartext HTTP traffic to **** not permitted
```


For Android 11.0 and later, perform the following operations:


1. In the res folder of your project, create a folder named xml. Then, create a file named `network_security_config.xml` in the xml folder.

   The file content is as follows. Replace `tls-ap-southeast-1.ibytepluses.com` with the actual endpoint.

   ```XML
   <?xml version="1.0" encoding="utf-8"?>
   <network-security-config>
       <!--<base-config cleartextTrafficPermitted="true" />-->
       <domain-config cleartextTrafficPermitted="true">
           <domain includeSubdomains="true">tls-ap-southeast-1.ibytepluses.com</domain>
       </domain-config>
   </network-security-config>
   ```
   

2. Modify the `AndroidManifest.xml` file, and add the following attribute to the application tag:

   ```XML
   <application
       ...
       android:networkSecurityConfig="@xml/network_security_config"
       ...
   />
   ```
   


<span id="示例项目"></span>
## Sample project

TLS offers a sample project of collecting logs on GitHub: [android-demo](https://github.com/volcengine/volc-sdk-java/tree/main/android-example/src/main/java/com/volcengine/example/tls/android-demo). You can use this sample project to run the log collection process to test the collection capability of TLS SDK for Android.


1. Create an Android application through the sample project.

   1. Download the source code of the sample project from GitHub.

   2. Create a project through Android Studio and import source code files.

   3. In the attributes section of the `PutLogExample.java` file, specify information such as BytePlus AccessKey and the topic ID.

2. Test the collection capability of TLS SDK for Android.

   1. Connect your Android device to a computer.

   2. On Android Studio, click `Run 'app'`.

      If the application runs properly, the sample project is installed to the Android device.

   3. Start the application and send logs as prompted.

      TLS SDK for Android collects the log data of the application and sends the data to the specified topic. You can preview the log data in the TLS console.
