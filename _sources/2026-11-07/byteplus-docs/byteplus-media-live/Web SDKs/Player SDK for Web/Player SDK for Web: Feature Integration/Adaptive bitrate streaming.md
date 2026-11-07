---
title: "Adaptive bitrate streaming"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr"
---

Adaptive bitrate (ABR) is a viewer\-focused video delivery technology designed to deliver seamless, high\-quality playback experiences regardless of fluctuating network conditions. You preconfigure multiple substreams with different encoding formats, resolutions, and bitrates, and the player automatically selects the optimal stream based on your viewers' real\-time network conditions to balance smooth playback and video quality. This topic describes how to configure the ABR feature for HLS, RTM, and FLV streams by using the Player SDK for Web.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the latest version of the Player SDK for Web. For version information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2">Player SDK for Web: Release notes</a>. For legacy versions, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions">Player SDK for Web: 1.x versions</a>.</div>


<span id="前提条件"></span>
## Prerequisites

You have integrated the Player SDK for Web. For more information, see [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="a0dade71"></span>
## Playing HLS\-ABR streams

<span id="8c72c128"></span>
### Step 1: Add an ABR configuration


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Adaptive bitrate** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. On the **Basic information** tab, enter the `AppName` from your push stream address, and select **HLS\-ABR** as the **Protocol Type**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52e6b604233348f1acedd0433ec2038e~tplv-goo7wpa0wc-image.image) </span>

5. Click **Add substream** to configure substreams for each quality level the player can switch between based on viewers' network conditions.


For other settings, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

<span id="2694fc4d"></span>
### Step 2: Get the HLS\-ABR address for your ABR stream

Get the HLS\-ABR address in one of the following ways:


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to get the **HLS\-ABR address** on the **Adaptive bitrate** tab. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate the HLS\-ABR address.


<span id="3083dd6e"></span>
### (Optional) Step 3: Import and register plugins when using the NPM method

If you use the NPM method to import dependencies, you must import and register the `abr` and `hlsjs` plugins to ensure that the ABR feature and HLS playback are available.

The sample code is as follows.

```JavaScript
import { hlsjs, abr } from '@byteplus/veplayer-plugin';
register([hlsjs, abr]);
```


<span id="396240fa"></span>
### Step 4: Configure ABR

When creating the player, you can configure the ABR feature and listen for quality level switch events.


* **Configure ABR feature**: The ABR feature is enabled by default in the SDK. You only need to provide the HLS\-ABR address. The player requests the address and receives the main playlist, which acts as a guide to all the available substreams (such as 1080p and 720p). The player then continuously monitors the viewer's network conditions and automatically switches between these substreams. When the network is poor, the player selects a lower\-bitrate stream to reduce buffering, and seamlessly switches back to a higher\-bitrate stream when the network improves, ensuring an optimal and uninterrupted viewing experience.

* **Listen** **for** **quality level switch events**: To implement custom logic when switching quality levels, such as updating the UI or reporting switch data, you can listen for the following events:

   * `ABR_SWITCH_START`: Start switching the quality level.

   * `ABR_SWITCH_SUCCESS`: The quality level was switched successfully.

   * `ABR_SWITCH_FAILED`: Quality level switching failed.


The sample code is as follows.


<Tabs>
<Tab zoneid="E0R6emP0Tb" title="CDN">
<TabTitle>CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
    width: 640,
    height: 360,
    url: 'http://pull.example.com/live/test/abr.m3u8',
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(VePlayer.live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
<Tab zoneid="csWrnWTm9s" title="NPM">
<TabTitle>NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { hlsjs, abr } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([hlsjs, abr]);

createLivePlayer({
    width: 640,
    height: 360,
    url: 'http://pull.example.com/live/test/abr.m3u8',
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
</Tabs>


<span id="c552533f"></span>
## Playing RTM\-ABR streams

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To play RTM\-ABR streams, make sure you have integrated the Player SDK version 2.12.0 or later.</div>


<span id="ef109318"></span>
### Step 1: Add an ABR configuration


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Adaptive bitrate** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. On the **Basic information** tab, enter the `AppName` from your push stream address, and select **RTM\-ABR** as the **Protocol Type**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/987feb246fd04cb0acf9d2dbe8bcda88~tplv-goo7wpa0wc-image.image) </span>

5. Click **Add substream** to configure substreams for each quality level the player can switch between based on viewers' network conditions.


For other settings, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

<span id="cd6f509c"></span>
### Step 2: Get the RTM\-ABR pull stream address

Get the RTM\-ABR pull stream address in one of the following ways.


* **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) and select the startup quality level (suffix) to get the **RTM Web SDK playback address** on the **Adaptive bitrate** tab. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

* **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate RTM\-ABR pull stream addresses. Different suffixes correspond to different startup quality levels. Select one address as the playback URL. Make sure the value of `Protocol` is `udp_websdk`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you cannot get the RTM\-ABR pull stream address, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>.</div>


* <div data-tips="true" data-tips-type="warning">The RTM\-ABR pull stream address supports automatic transcoding, including B\-frame removal and AAC\-to\-Opus audio conversion. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses">Generating live\-stream addresses</a>.</div>



<span id="84ece4f7"></span>
### (Optional) Step 3: Import and register plugins when using the NPM method

If you use the NPM method to import dependencies, you must import and register the `abr` and `rtm` plugins to ensure that the ABR feature and RTM playback are available.

The sample code is as follows.

```JavaScript
import { rtm, abr } from '@byteplus/veplayer-plugin';
register([rtm, abr]);
```


<span id="9e84cbf4"></span>
### Step 4: Configure ABR

When creating the player, you can configure the ABR feature and listen for quality level switch events.


* **Configure ABR feature**: The ABR feature is enabled by default in the SDK. You only need to provide one RTM\-ABR pull stream address. The suffix in the RTM\-ABR pull stream address determines the startup quality level. During playback, MediaLive automatically switches between quality levels based on the viewer's network conditions. When the network is poor, MediaLive switches to a lower\-bitrate stream to reduce buffering, and seamlessly switches back to a higher\-bitrate stream when the network improves, ensuring an optimal and uninterrupted viewing experience.

* **Listen** **for quality level switch events**: To implement custom logic when switching quality levels, such as updating the UI or reporting switch data, you can listen for the following events:

   * `ABR_SWITCH_START`: Start switching the quality level.

   * `ABR_SWITCH_SUCCESS`: The quality level was switched successfully.

   * `ABR_SWITCH_FAILED`: Quality level switching failed.


The sample code is as follows.


<Tabs>
<Tab zoneid="Big4rXVf6P" title="CDN">
<TabTitle>CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
    width: 640,
    height: 360,
    url: 'https://pull.example.com/live/test_sd_autortm.sdp?rtmabr=true',
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(VePlayer.live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
<Tab zoneid="mxntnHVIBd" title="NPM">
<TabTitle>NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { rtm, abr } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([rtm, abr]);

createLivePlayer({
    width: 640,
    height: 360,
    url: 'https://pull.example.com/live/test_sd_autortm.sdp?rtmabr=true',
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
</Tabs>


<span id="4199e517"></span>
## Playing FLV streams

<span id="f93c3f0f"></span>
### Step 1: Add an ABR configuration


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Feature configuration** and click the **Adaptive bitrate** tab on the right.

3. Select your desired domain name space from the **Domain name space** drop\-down list and then click **Add configuration**.

4. On the **Basic information** tab, enter the `AppName` from your push stream address.

5. Click **Add substream** to configure substreams for each quality level the player can switch between based on viewers' network conditions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a205a874210a4d3e9b8fc9500735ef21~tplv-goo7wpa0wc-image.image) </span>


For other settings, see [Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task).

<span id="ef0650ed"></span>
### Step 2: Get FLV pull stream addresses for different quality levels

Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to generate and get the FLV pull stream address for a specific quality level on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/795e50db176d41db8d3a03069538a2c4~tplv-goo7wpa0wc-image.image) </span>


* **Address type**: Select **Pull stream address**.

* **Domain name**: Select the domain name for stream pulling within the domain name space used when adding the ABR configuration.

* **AppName** and **StreamName**: Use your push stream address to determine the values for these fields. If your push stream address is `rtmp://push.example.com/live/test?authinfo`:

   * **AppName**: The `AppName` is the part of the address after the domain. In this case, you would enter `live`.

   * **StreamName**: First, identify the **base stream name** from the address, which is `test`. Then, for each quality level, append the corresponding substream suffix to this base name. For example:

      * For the UHD quality level, enter `test_uhd`

      * For the HD quality level, enter `test_hd`

   Record the FLV pull stream address for each quality level in this way.


**Example**

The following table lists examples of FLV pull stream addresses and corresponding bitrate values for different quality levels.


|Quality level |FLV pull stream address |Bitrate (kbps) |
|---|---|---|
|UHD |https://pull.example.com/live/123456_uhd.flv |3200 |
|HD |https://pull.example.com/live/123456_hd.flv |2048 |
|SD |https://pull.example.com/live/123456_sd.flv |1638 |
|Low Definition (LD) |https://pull.example.com/live/123456_ld.flv |1024 |


<span id="82250019"></span>
### (Optional) Step 3: Import and register plugins when using the NPM method

If you use the NPM method to import dependencies, you must import and register the `flv` and `abr` plugins to ensure that low\-latency FLV and ABR features are available. The sample code is as follows.

```JavaScript
import { flv, abr } from '@byteplus/veplayer-plugin'
register([flv, abr]);
```


Since some mobile browsers (such as Safari before iOS 16) cannot play FLV streams, to ensure that the live stream can still play normally on these devices, the SDK provides an HLS fallback solution. After enabling this solution, when the player detects that the current browser does not support playing FLV streams, it will automatically switch to the alternative HLS stream for playback. To ensure that the fallback works properly, if you import dependencies via NPM, be sure to also import and register the `hlsjs` plugin. The sample code is as follows.

```JavaScript
import { flv, hlsjs, abr } from '@byteplus/veplayer-plugin';
register([flv, hlsjs, abr]);
```


<span id="fb64008c"></span>
### Step 4: Configure ABR and enable low\-latency FLV in the SDK

When creating the player, you can use the following configurations to provide viewers with a low\-latency, smooth, and fully platform\-compatible live streaming experience:


* **Configure ABR feature**: The ABR feature is enabled by default in the SDK. You only need to provide a list containing multiple bitrates and their corresponding FLV pull stream addresses. The player will automatically switch quality levels during the live stream based on viewers' network conditions, ensuring smooth playback while providing good video quality.

* **Listen** **for quality level switch events**: To implement custom logic when switching quality levels, such as updating the UI or reporting switch data, you can listen for the following events:

   * `ABR_SWITCH_START`: Start switching the quality level.

   * `ABR_SWITCH_SUCCESS`: The quality level was switched successfully.

   * `ABR_SWITCH_FAILED`: Quality level switching failed.

* **Mobile HLS fallback solution**: Some mobile browsers (such as Safari before iOS 16) do not support playing FLV streams. To ensure that the live stream can play normally on these devices, you can provide a backup HLS pull stream address when configuring the FLV pull stream addresses. When the player detects that the current browser does not support playing FLV streams, it will automatically switch to the HLS stream for playback.


The sample code is as follows.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To ensure that the ABR feature works properly, make sure that the bitrate you set for each quality level in the code matches that of the ABR configuration in the console.</div>


<div data-tips="true" data-tips-type="warning"><strong>Please pay special attention to unit conversion:</strong></div>



* <div data-tips="true" data-tips-type="warning"><strong>Bitrate unit in the console:</strong> <code>kbps</code></div>


* <div data-tips="true" data-tips-type="warning"><strong>Bitrate unit in the code:</strong> <code>bps</code></div>



<div data-tips="true" data-tips-type="warning">Therefore, the bitrate value set in the code must be <strong>1000</strong> times the value in the console.</div>


<div data-tips="true" data-tips-type="warning">For example, if the console is set to <code>3200</code> kbps, then <code>3200000</code> should be passed in the code.</div>



<Tabs>
<Tab zoneid="cpStaaa5sH" title="CDN">
<TabTitle>CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
    width: 640,
    height: 360,
    playlist: [
      {
        definitions: [
          // FLV pull stream address for the initial playback quality level.
          'https://pull.example.com/live/123456_uhd.flv',
          // HLS pull stream address for fallback playback, which can be generated through the console's address generator.
          'https://pull.example.com/live/123456_uhd.m3u8',
        ],
      },
    ],
    flv: {
      abr: {
        // Bitrate for the initial playback quality level. Unit is bps.
        bitrate: 3200000,
        // Bitrates and FLV pull stream addresses for each quality level. Bitrate unit is bps.
        urls: {
          3200000: 'https://pull.example.com/live/123456_uhd.flv',
          2048000: 'https://pull.example.com/live/123456_hd.flv',
          1638000: 'https://pull.example.com/live/123456_sd.flv',
          1024000: 'https://pull.example.com/live/123456_ld.flv',
         }
     }
  },
    fallback: {
      // Try to play the low-latency FLV stream first. When the player detects that the current browser cannot play the low-latency FLV stream, it will automatically fallback to HLS stream for playback. 
      fallbackOrder: ['ll-flv', 'hls'],
    }
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(VePlayer.live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(VePlayer.live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
<Tab zoneid="H5LcRLRGs3" title="NPM">
<TabTitle>NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { flv, hlsjs, abr } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([flv, hlsjs, abr]);

createLivePlayer({
    width: 640,
    height: 360,
    playlist: [
      {
        definitions: [
           // FLV pull stream address for the initial playback quality level.
          'https://pull.example.com/live/123456_uhd.flv',
          // HLS pull stream address for fallback playback, which can be generated through the console's address generator.
          'https://pull.example.com/live/123456_uhd.m3u8',
        ],
      },
    ],
    flv: {
      abr: {
        // Bitrate for the initial playback quality level. Unit is bps.
        bitrate: 3200000,
        // Bitrates and FLV pull stream addresses for each quality level. Bitrate unit is bps.
        urls: {
          3200000: 'https://pull.example.com/live/123456_uhd.flv',
          2048000: 'https://pull.example.com/live/123456_hd.flv',
          1638000: 'https://pull.example.com/live/123456_sd.flv',
          1024000: 'https://pull.example.com/live/123456_ld.flv',
      }
    }
  },
    fallback: {
      // Try to play the low-latency FLV stream first. When the player detects that the current browser cannot play the low-latency FLV stream, it will automatically fallback to HLS stream for playback. 
      fallbackOrder: ['ll-flv', 'hls'],
    }
}).then(function (veplayer) {
    // Listen for quality level switching events.
    veplayer.on(live.Events.ABR_SWITCH_START, function (data) {
      console.log('ABR_SWITCH_START', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_SUCCESS, function (data) {
      console.log('ABR_SWITCH_SUCCESS', data.bitrate);
    });

    veplayer.on(live.Events.ABR_SWITCH_FAILED, function (data) {
      console.log('ABR_SWITCH_FAILED', data.bitrate);
    });
})
```



</Tab>
</Tabs>
