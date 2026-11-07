---
title: "Managing streams"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-streams"
---

To monitor and manage your streams for stability and compliance, use the **Streams** module in the MediaLive console. This topic describes how to view live, historical, and disabled streams, and perform key management tasks such as stopping, disabling, and re\-enabling them.

<span id="Prerequisite"></span>
## Prerequisites

To query streams, you must first get the `AppName`and `StreamName` from the push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test`, the `AppName` is `live` and the `StreamName` is `test`.

<span id="Procedure"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Live management** \> **Streams**.

3. Select the type of stream you want to search by clicking the corresponding tab at the top of the page.

   * **Live streams**: Displays ongoing streams.

   * **Stream history**: Displays ended or stopped streams.

   * **Disabled streams**: Displays disabled streams.

4. Enter the **AppName** and **StreamName**, select the query time range and stream source as needed, and then click **Search** to view the stream list.

   * To view streams pulled from third\-party CDN, select **Pulled from origin** as the stream configuration.

   * Otherwise, select **Pushed stream** as the stream configuration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you perform bulk operations to stop, disable, or enable streams, you can select up to 1,000 streams across multiple pages.</div>


* <div data-tips="true" data-tips-type="tip">After you select multiple streams in bulk, you can click the checkbox in the lower\-left corner of the list to deselect all.</div>


   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26031253f9954fedacd4fb585087cf91~tplv-goo7wpa0wc-image.image" width="229px" />   </div>
   


<span id="Live streams"></span>
### Live streams

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c33a52b5f03485faea32f171b1830dc~tplv-goo7wpa0wc-image.image) </span>

The **Live streams** tab displays the information of ongoing streams, such as the domain name, status, stream source, and start time. In the **Action** column, select the operation you want to perform:


* Click **Live address** to view the push stream address and generate pull stream addresses.

* Click **Stream data** to view push streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

* Click **Views statistic** to view pull streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

   * If there are multiple pull stream addresses, select a specific one in the dialog box and click **OK** to view the corresponding data display page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a962f310018486e9ae0bec84939bea6~tplv-goo7wpa0wc-image.image) </span>

   * If there is only one pull stream address, you will go to the data display page for that address directly.

* Stop one or more streams. You can find stopped streams on the **Stream history** tab.

   * Click the More (...) icon and select **Stop streaming** to stop the stream.

   * Select one or more streams and click **Batch interruption** at the bottom of the page to stop the selected streams in bulk.

* Disable one or more streams. By default, a stream is disabled for 90 days and automatically re\-enabled after this period. You can find disabled streams on the **Disabled streams** tab.

   * Click the More (...) icon and select **Disable** to disable the stream.

   * Select one or more streams and click **batch disable** at the bottom of the page to disable the selected streams in bulk.


<span id="Stream history"></span>
### Stream history

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ff210848dde4ece9c45a89cf26c9a00~tplv-goo7wpa0wc-image.image) </span>

The **Stream history** tab displays the stream information from the last 30 days, such as domain name, stream source, and end time. In the **Action** column, select the operation you want to perform:


* Click **Live address** to view the push stream address and generate pull stream addresses.

* Click **Stream data** to view push streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

* Click **Views statistic** to view pull streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

   * If there are multiple pull stream addresses, select a specific one in the dialog box and click **OK** to view the corresponding data display page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a962f310018486e9ae0bec84939bea6~tplv-goo7wpa0wc-image.image) </span>

   * If there is only one pull stream address, you will go to the data display page for that address directly.

* Disable one or more streams. By default, a stream is disabled for 90 days and automatically re\-enabled after this period. You can find disabled streams on the **Disabled streams** tab.

   * Click the More (...) icon and select **Disable** to disable the stream.

   * Select one or more streams and click **batch disable** at the bottom of the page to disable the selected streams in bulk.


<span id="Disabled streams"></span>
### Disabled streams

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6aaf676c8cc54ee3b512491cb34c8b34~tplv-goo7wpa0wc-image.image) </span>

The **Disabled streams** tab displays the information of disabled streams, such as the domain name, status, and the time when the stream was disabled. In the **Action** column, select the operation you want to perform:


* Click **Stream data** to view push streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

* Click **Views statistic** to view pull streaming data. For more information, see [Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data).

   * If there are multiple pull stream addresses, select a specific one in the dialog box and click **OK** to view the corresponding data display page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a962f310018486e9ae0bec84939bea6~tplv-goo7wpa0wc-image.image) </span>

   * If there is only one pull stream address, you will go to the data display page for that address directly.

* Enable one or more streams. You can find enabled streams on the **Stream history** tab.

   * Click **Enable** to enable the stream.

   * Select one or more streams and click **batch enable** at the bottom of the page to enable the selected streams in bulk.
