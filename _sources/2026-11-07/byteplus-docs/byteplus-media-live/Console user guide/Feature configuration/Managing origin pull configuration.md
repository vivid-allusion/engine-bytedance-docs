---
title: "Managing origin pull configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-origin-pull-settings"
---

Origin pull enables your CDN to fetch a live stream from a third\-party origin server when a viewer makes a request and the stream is not cached. This topic provides instructions on how to configure an origin\-pull task.

You can choose between on\-demand pulling, which is cost\-effective, or scheduled pulling, which ensures content is always fresh for a better viewing experience.


* On\-demand: Origin pull is triggered only when there are viewers watching. This method saves bandwidth usage and is therefore more cost\-effective.

* Scheduled: The edge servers continuously pull the streamed content from the origin within the specified time range. This method guarantees that the edge servers always have the latest content, reducing the load time on the client side and improving the viewing experience.


<span id="8db887ad"></span>
## Limitations


* For on\-demand origin pull, the stream name in the pull stream address should not include any slashes. For instance, you cannot configure an origin\-pull task for a pull stream address such as "https://example_domain_name.com/appName/streamName1/streamName2.flv", because the stream name "streamName1/streamName2" contains a slash.

* Once you have configured an origin\-pull task for a domain name or AppName, you can no longer configure recording or screenshot\-capturing tasks for that domain name or AppName.


<span id="73cd97b1"></span>
## Prerequisite

A domain name for stream pushing. For details, refer to [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337).

<span id="c348f257"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Origin pull** tab.

3. Find **Domain name space** at the top of the page and select a domain name for stream pushing from the drop\-down list.

4. Select **On\-demand** or **Scheduled**, and then click **Add configuration** to launch the dialog box.

   The following table lists the configurations for an on\-demand origin pull task:

   
   |**Parameters** |**Descriptions** |
   |---|---|
   |AppName |Specify the AppName of the live stream to be pulled from the origin. Make sure it is the same as the AppName specified in the pull stream address.<br><br>This is the name of the application for which you want to configure the origin\-pull task.<br><br><br>* You can use an asterisk (\*) as a wildcard to apply this setting to all application names of the selected domain. In that case, the setting becomes the global setting for the selected domain name.<br><br>* For application names with both global and individual settings configured, the individual settings take precedence.<br><br>* Do not enter the name of an application that has already been configured with a scheduled origin\-pull task. |
   |Streaming protocol |Supports RTMP, FLV, HLS, and DASH.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot change the streaming protocol once you save the configuration.</div><br> |
   |Origin address |Target address from which to pull the live stream. You can enter domain names or IP addresses. You can enter up to 10 origin addresses. If a request to an origin address fails, the service will attempt to connect to the other addresses in the order they are listed. |
   |Parameters |Optional. You can use this field to pass additional information to the third\-party origin server. For example, you can set **key** to `from` and **value** to `byteplus`, so that the third\-party origin server knows where the pull\-stream request comes from. |
   

   The following table lists the configurations for a scheduled origin pull task:

   
   |**Parameters** |**Descriptions** |
   |---|---|
   |AppName |The application name for which you want to configure the origin\-pull task. Only lowercase is supported.<br><br><br>* You can use an asterisk (\*) as a wildcard to apply this setting to all application names of the selected domain. In that case, the setting becomes the global setting for the selected domain name.<br><br>* For application names with both global and individual settings configured, the individual settings take precedence.<br><br>* Do not enter an application name that has an on\-demand origin\-pull task configured. |
   |StreamName |The stream name for which you want to configure the origin\-pull task. |
   |Origin address |Target address from which to pull the live stream. You can enter domain names or IP addresses.<br><br>Supports RTMP, FLV, SRT, and HLS.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can enter up to 10 origin addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a request to an origin address fails, the service will attempt to connect to the other addresses in the order they are listed.</div><br> |
   |Type |**Fixed time**: The origin\-pull task runs during a specified time range. |
   |Time range |The start and end time of the origin\-pull task. The maximum time span is 7 days. |
   

5. Click **Confirm** to save the configuration. You can always click the **Edit** or **Delete** button in the **Actions** column to adjust these settings.


<span id="8ec3d770"></span>
## Example

Suppose you have configured an on\-demand origin\-pull task with the following settings for a domain name called "push_stream_domain.com":


* **AppName**: `myapp`

* **Streaming protocol**: `flv`

* **Origin address**: `third_party_domain.com`

* **Parameters**:

   * **key**: `from`

   * **value**: `byteplus`


In this case, if a user pulls a stream using the address "https://pull_stream_domain.com/myapp/mystream.flv?query1=value1", BytePlus MediaLive will pull the stream from the third\-party origin server using the address "https://third_party_domain.com/myapp/mystream.flv?query1=value1&from=byteplus".

The following diagram illustrates the various components of the pull stream addresses mentioned above:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90195dac107842e2a635e41a8efe12c8~tplv-goo7wpa0wc-image.image) </span>
