---
title: "Use WebTracking to collect logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use_web_tracking_to_collect_logs"
---

Torch Log Service (TLS) supports the WebTracking feature. This feature enables you to use the API action for WebTracking to collect log data from various mobile applications, including HTML, iOS, and Android applications. This topic describes how to enable the WebTracking feature for a TLS topic, and how to collect and save log data to the TLS server.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In lightweight event tracking scenarios, you often have to configure event tracking and upload data quickly. For example, in some marketing events, you must collect and upload user behavior data and browsing data efficiently. The data includes the user device and browser information, browsing records, and stay time on specific content. WebTracking, also called tracking pixel, allows you to embed a 0\-pixel image into a page. By default, the image is invisible to users. When a user visits the page, the image is loading on the page, initiating a GET request to send the parameters to the server.

With WebTracking, TLS offers a lightweight log collection solution that allows you to upload data to the TLS server using an HTTP GET request. Tag tracking for browsers, JavaScript, and images is supported. The solution is suitable for collecting data that can be accessed without authentication from static pages, ads, promotion materials, and mobile apps.

When calling the WebTracking API action to write log data, TLS automatically adds the following reserved fields to the original log data:


|Reserved Field |Description |
|---|---|
|clientAddr |The IP address and port number of the log data source from which you use the WebTracking mode to collect log data. |
|User\-Agent |The name of the client.<br><br>By default, TLS adds this field only when collecting logs using HTML img tags. |
|referer |The referring page from which the current access is led.<br><br>By default, TLS adds this field only when collecting logs using HTML img tags. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After you enable the WebTracking feature for a topic, authentication is not required when the WebTracks API action is used to write data. In other words, an anonymous user from the internet can write data to the topic, which may generate dirty data.

* When you call the WebTracks API action using a GET request, the body length cannot exceed 16 KiB.

* When you call the WebTracks API action using a POST request, the size of log data written each time cannot exceed 5 MiB. For more information, refer to [WebTracks](https://docs.byteplus.com/docs/tls/api-webtracks).


<span id=".XzEt5byA5ZCvLXdlYi10cmFja2luZy3lip_og70="></span>
## 1. Enable WebTracking

You can enable the WebTracking feature for a specified topic using the TLS console. Only after this feature is enabled can you collect logs through WebTracking.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. Click the name of the target project.

4. Find the target topic, then click **Edit** in the **Action** column.

5. Toggle the **WebTracking** switch to enable the feature, then click **OK**.


<span id=".XzIt6YCa6L-HLXdlYi10cmFja2luZy3ph4fpm4bml6Xlv5c="></span>
## 2. Collect log data using WebTracking

After WebTracking is enabled, use one of the following methods to upload log data to the specified topic.

<span id=".aHRtbC1pbWct5qCH562-5pa55byP"></span>
### Use HTML tags

You can add an tag to embed a 0\-pixel image into a page. By default, the image is invisible to users. When a user visits the page, the image is loading on the page. At the same time, a GET request is initiated and sent to the server, and the data in `<img>` is sent to the specified topic in TLS.

For example, you can embed the following tags into a page:

```html
<img src='http://${host}/WebTrack.gif?ProjectId=testproject&TopicId=newtopic&key1=value1&key2=value2'/>
<img src='http://${host}/WebTrackUa.gif?ProjectId=testproject&TopicId=newtopic&key1=value1&key2=value2'/>
```


where:


* `${host}` indicates the public endpoint of TLS. For information on the TLS endpoint for each Region, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).

* `WebtrackUa.gif` is the name of the image. After this image is embedded in the page, not only custom parameters are uploaded, but also the UserAgent and Referer HTTP headers are uploaded as fields in log data to TLS.

* The HTTPS protocol is supported. It means that the WebTracking link in the tag can be specified with HTTPS. This allows for collecting the source information of HTTPS pages.


<span id=".aHR0cC1nZXQt6K-35rGC5pa55byP"></span>
### Use the HTTP GET request method

You can use the HTTP GET request method to call the WebTrack API to upload log data to the specified topic.


* Sample request:

   ```bash
   curl --request GET 'http://${host}/WebTrack?ProjectId=abc&TopicId=def&key1=val1&key2=val2'
   ```
   

* Request parameters:

   
   |Parameter |Required |Description |
   |---|---|---|
   |$ |Yes |The TLS endpoint for the corresponding Region. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |ProjectId |Yes |The project ID. |
   |TopicId |No |The topic ID. |
   |key1=val1&key2=val2 |Yes |The log data in key\-value pair format. Join multiple key\-value pairs with ampersands `&`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Make sure that the total size of the log data is less than 16 KiB.</div><br> |
   


<span id=".aHR0cC1wb3N0Leivt-axguaWueW8jw=="></span>
### Using the HTTP POST request method

If you must upload large volumes of data, you can use the POST method to call the WebTrack API action. For more information, refer to [WebTracks](https://docs.byteplus.com/docs/tls/api-webtracks).
