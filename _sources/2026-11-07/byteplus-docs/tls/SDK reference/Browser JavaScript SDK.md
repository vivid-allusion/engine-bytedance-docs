---
title: "Browser JavaScript SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/browser_javascript_sdk"
---

Torch Log Service (TLS) allows you to use the web tracking feature to collect user browser logs. This topic describes how to use the web tracking SDK for JavaScript to collect user browser logs.

<span id="背景信息"></span>
## Background

In lightweight event tracking scenarios, you often have to configure event tracking and upload data quickly. For example, in some marketing events, you must collect and upload user behavior data and browsing data efficiently. The data includes the user device and browser information, browsing records, and stay time on specific content. Web tracking, also called tracking pixel, allows you to embed a 0\-pixel image into a page. By default, the image is invisible to users. When a user visits the page, the image is loading on the page, initiating a GET request to send the parameters to the server.

With web tracking, TLS offers a lightweight log collection solution that allows you to upload data to the TLS server using an HTTP GET request. Tag tracking for browsers, JavaScript, and images is supported. The solution is suitable for collecting data that can be accessed without authentication from static pages, ads, promotion materials, and mobile apps.

<span id="注意事项"></span>
## Precautions


* After you enable the web tracking feature for a topic, authentication is not required when the WebTracks API action is used to write data. In other words, an anonymous user from the internet can write data to the topic, which may generate dirty data.

* When you call the WebTracks API action using a GET request, the body length cannot exceed 16 KiB.

* When you call the WebTracks API action using a POST request, the size of log data written each time cannot exceed 5 MiB. For more information, refer to [WebTracks](https://docs.byteplus.com/docs/tls/api-webtracks).


<span id="步骤一：开启-webtracking"></span>
## Step 1: Enable the web tracking feature

Before you use the browser JavaScript SDK to write log data to a topic, enable the web tracking feature for the topic.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource Management** \> **Project**.

3. Click the name of the target project.

4. Find the **operation** column of the target topic, then click **Edit**.

5. enable **WebTracking**, then click **OK**.


<span id="步骤二：导入-sdk"></span>
## Step 2: Import the SDK

Before you use the browser JavaScript SDK to write user logs, import and integrate the SDK.


1. Install the dependency.

   ```shell
   npm install --save @volcengine/tls-js-sdk
   ```
   

2. Import the dependent module to your code project.

   ```javascript
   import { WebTrackerBrowser } from '@volcengine/tls-js-sdk'
   ```
   


<span id="步骤三：写入日志数据"></span>
## Step 3: Write log data

After you import the browser JavaScript SDK, refer to the following steps to set log collection parameters, including the name of the project that stores log data, topic name, and collection metrics:


1. Set the parameters in options.

   ```javascript
   const options = {
     host: `${host}`, // The endpoint of TLS in the corresponding Region.
     projectId: `${projectId}`, // The project ID.
     topicId: `${topicId}`, // The topic ID.
     source: `${source}`, // The log source.
     time: 10, // The interval at which log data is sent. Default value: 10. Unit: seconds.
     count: 10, // The number of log entries that are sent each time. Default value: 10.
     protocol: `${protocol}`, // The protocol type. Default value: https.
   }
   ```
   

   
   |Parameter |Required |Description |
   |---|---|---|
   |host |Yes |The endpoint of TLS in the corresponding Region. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |projectId |Yes |The project ID. |
   |topicId |Yes |The topic ID. |
   |source |No |The log source. Specify a custom value to identify different sources. |
   |time |No |The interval at which log data is sent from log sources. Default value: 10. Unit: seconds. |
   |count |No |The number of log entries that are sent each time. Default value: 10. |
   |protocol |No |The protocol type. Default value: https. |
   

2. Create a WebTrackerBrowser object, and use the object to initiate a request to upload logs to TLS.

   ```javascript
   const tracker = new WebTrackerBrowser(options)
   ```
   

3. Upload logs.

   Use methods such as `send()` to upload logs in the format of key\-value pairs. The methods are used to implement your business logic of uploading logs. To batch upload logs, use methods such as `sendBatchLogs()`.

   ```php
   tracker.send({
     name: 'wanger',
     status: 'normal',
     fee: 901,
   })
   ```
   


<span id="核心-api-列表"></span>
## Core methods

The browser JavaScript SDK offers the following core methods and sample code. Select a suitable method to upload logs as needed.


|Method |Description |Data Type |Example |
|---|---|---|---|
|send() |Upload a single log entry. |Object |```shell```<br>```tracker.send({```<br>```    name: 'wanger',```<br>```    status: 'normal',```<br>```    fee: 901,```<br>``` })```<br> |
|sendImmediate() |Upload a single log entry immediately. At this time, the time and count parameters set in options do not take effect. |Object |```shell```<br>```tracker.sendImmediate({```<br>```    name: 'wanger',```<br>```    status: 'normal',```<br>```    fee: 901,```<br>```})```<br> |
|sendBatchLogs() |Batch upload logs. |Array |```shell```<br>```tracker.sendBatchLogs([{```<br>```    name: 'wanger',```<br>```    status: 'normal',```<br>```    fee: 901,```<br>```}, {```<br>```    name: 'zhangsan',```<br>```    status: 'normal',```<br>```    fee: 1000,```<br>```}, ])```<br> |
|sendBatchLogsImmediate() |Batch upload logs. At this time, the time and count parameters set in options do not take effect. |Array |```shell```<br>```tracker.sendBatchLogsImmediate([ {```<br>```    name: 'wanger',```<br>```    status: 'normal',```<br>```    fee: 901,```<br>```}, {```<br>```    name: 'lisi',```<br>```    status: 'normal',```<br>```    fee: 801,```<br>```}, ])```<br> |
