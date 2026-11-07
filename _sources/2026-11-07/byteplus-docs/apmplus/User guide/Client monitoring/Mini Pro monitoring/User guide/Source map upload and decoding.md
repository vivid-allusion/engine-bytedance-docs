---
title: "Source map upload and decoding"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Source_map_upload_and_decoding"
---

SourceMap is an information file that stores the mapping between code locations before and after transformation. The APM console provides the ability to upload and reverse map SourceMaps, helping you parse error stack traces in JS details.

<span id=".5q2l6aqk5LiA77ya6I635Y-WU291cmNlTWFw"></span>
## Step 1: Obtain SourceMap

Mini programs on each platform can obtain SourceMap files from the specified Background during upload or after going online. The following provides a detailed introduction using WeChat Mini Program as an example.


1. Log in to [WeChat Mini Program Developer Background](https://mp.weixin.qq.com/).

2. In the left navigation bar, select **Development \> Development management**.

3. In the **error** area, click **Download online SourceMap file**.


<span id=".5q2l6aqk5LqM77ya5LiK5LygU291cmNlTWFw"></span>
## Step 2: Upload SourceMap

The console provides two entry points for uploading SourceMap files: from the JavaScript error details page and from the SourceMap management page.

<span id=".SlPplJnor6_or6bmg4U="></span>
### JavaScript error details


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Mini Program Pro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> JavaScript overview**.

4. In the error and page overview, click the target error entry to go to the **error details** page.

5. In the error stack trace area, click **minified**.

6. After the target JS file, click the upload button.

7. On the **upload sourcemap** page, upload the SourceMap file that matches the current JS file name, select the mini program type, env, and release version, then click **confirm**. The platform will parse the context of the current code.


<span id=".566h55CGc291cmNlbWFw"></span>
### Manage sourcemap


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Mini Program Pro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> Manage sourcemap**.

4. Click **Upload Sourcemap**.

5. On the **upload sourcemap** page, enter the JS sourcemap file name, upload the SourceMap file, select the mini program type, env, and release version, then click **confirm**.

6. In the upper left corner of the console, select **All features \> JavaScript overview**.

7. In the error and page overview, click the target error content to go to the **error details** page.

8. View the decompiled content in the error stack trace area.


<span id=".5q2l6aqk5LiJ77ya6aqM6K-BU291cmNlTWFw"></span>
## Step 3: Verify SourceMap

You can use [WeChat Official Documentation](https://developers.weixin.qq.com/miniprogram/dev/devtools/sourcemap.html) to verify the SourceMap you have downloaded. If SourceMap is available, the developer tools will display content similar to the following:

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When developing with native mini programs, the source files do not contain a SourceMap. After you upload them using the mini program developer tool, the generated SourceMap is only a few kilobytes to several dozen kilobytes in size, because it only supports reverse mapping of **code line and column** and does not include any context information.

* When you use third\-party frameworks such as Taro or Uni App and turn on SourceMap, the packaged output will include a SourceMap. When you upload it using the mini program development tool, the context of the source code will also be included. This SourceMap can be quite large, ranging from several hundred kilobytes to several megabytes. After decompiling, you can view the specific context of the current error.
