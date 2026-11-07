---
title: "Feature implementation"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-features"
---

This article introduces how to implement the features provided by the BytePlus MediaLive Player SDK for Web.

<span id="dc41133b"></span>
## Pulling an RTM stream

You can pull a stream using the Real Time Media (RTM) protocol with the Player SDK. For a detailed introduction to RTM, refer to [Introduction to Real Time Media](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media).


1. Use the address generator to generate an RTM pull stream address. Refer to [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses) for detailed instructions on how to generate the address.

2. Create a `VePlayer` instance and set the pull stream address as the one you acquired from the previous step.


```JavaScript
// Check if the player supports pulling an RTM stream
const isRTMSupported = VePlayer.isRTMSupported();
// Check if H.264 is supported (H.264 is supported since v1.6.3)
const isRTMSupportH264 = await VePlayer.isRTMSupportCodec('h264');

const playerSdk = new VePlayer({
    id: 'mse',
    url: isRTMSupported && isRTMSupportH264 ? 'https://testpull.mycloud.com/live/mystream.sdp' : 'https://testpull.mycloud.com/live/mystream.m3u8',
    isLive: true,
    width: 600,
    height: 400,
    rtm: {
        // Backup address and protocol. When the player fails to pull the RTM stream, it will use the following address instead.
        backupURL: 'https://testpull.mycloud.com/live/mystream.m3u8',
        backupStreamType: 'hls'
    }
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set an FLV or HLS stream as the backup stream by setting <code>backupStreamType</code> to <code>flv</code> and <code>hls</code> respectively.</div>


<span id="cc924516"></span>
## Time shifting

The time\-shifting feature allows your viewers to replay any streamed content. To play time\-shifted content, do the following:


1. Configure a time\-shifting task in the BytePlus MediaLive console. Refer to [Configuring a time-shifting task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting) for detailed instructions on the configurations.

2. Prepare an M3U8 pull stream address with the domain name and appName that you have configured in the previous step. Refer to [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses) for how to acquire a pull stream address in M3U8 format.

3. Add the following code to your project:

   ```JavaScript
   const playerSdk = new VePlayer({
      id: 'mse',
      isLive: true,
      // The pull stream address
      url: "//testpull.mycloud.com/live/mystream.m3u8", 
      width: 600, 
      height: 400,
      // Time-shifting configurations 
      TimeShiftPlugin: { 
        // The time the live stream session started
        livingStartTime: Date.now() / 1000 - 60, 
        // The maximum amount of time shifting available during playback, in seconds.
        maxMoveTime: 60
      }, 
      plugins: [VePlayer.TimeShiftPlugin], 
    });  
   ```
   


Refer to [timeShiftPlugin](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#2f07a993) for the parameter description relating to time shifting.

<span id="83de8250"></span>
## Uploading logs

For troubleshooting purposes, you can define `appId` in [liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) to enable log upload. Once an error occurs with the player, you can contact [technical support](https://www.byteplus.com/en/support) who will be able to locate the issue with the app ID.

We highly recommend that you set `userId` and `deviceId` to values that identify a unique user and device. Technical support may need the information to identify problems. If you do not define `userId` and `deviceId`, the SDK will generate random user IDs and device IDs, which will then be stored in the browser cache.

```JavaScript
const playerSdk = new VePlayer({
    id:'mse',
    isLive:true,
    width:600,
    height:400,
    url:'//pulldomain/appname/mainstream.flv',
    liveLogger: {
        appId: '2****4',
        userId: '1********6',
        deviceId: '3********7'
    }
});
```
