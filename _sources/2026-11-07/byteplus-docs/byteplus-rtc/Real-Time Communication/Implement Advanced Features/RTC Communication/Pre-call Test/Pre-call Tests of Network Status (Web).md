---
title: "Pre-call Tests of Network Status (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79792"
---

To provide better user experience, you can conduct a network quality test before the user implements a call, and take measures according to the result of the test, for example, lower the bit rate, or remind users through UI to switch to a more stable network.

<span id="prerequisites"></span>
## Prerequisites

You have integrated the Web SDK and implemented [real-time communications](https://docs.byteplus.com/en/docs/12/docs-70130).

<span id="build-a-call-quality-dashboard"></span>
## Build a call quality dashboard


1. Call `createEngine` twice to create two instances.

* `uplinkClient`: used to probe the uplink network quality

* `downlinkClient`: used to probe the downlink network quality


```javascript
const uplinkClient = BytePlusRTC.createEngine(appId);
const downlinkClient = BytePlusRTC.createEngine(appId);
```



2. Call `startVideoCapture` and `startAudioCapture` on `uplinkClient`.


```javascript
await uplinkClient.startAudioCapture();
await uplinkClient.startVideoCapture();
```



3. Call `joinRoom` twice with different `userId` and `token`, and enter the same test room.

* `uplinkClient`: Set auto\-publish to `true`.

* `downlinkClient`: Set auto\-subscribe to `true`.


```javascript
uplinkClient.joinRoom(token1, roomId, { userId: userId1 }, {
    isAutoPublish: true,
    isAutoSubscribeAudio: false,
    isAutoSubscribeVideo: false
});

downlinkClient.joinRoom(token2, roomId, { userId: userId2 }, {
    isAutoPublish: false,
    isAutoSubscribeAudio: true,
    isAutoSubscribeVideo: true
});
```



4. Obtain network quality statistics from the `onNetworkQuality` event.


```javascript
// Get detailed uplink stream statistics
uplinkClient.on('onNetworkQuality', (uplinkNetworkQuality) => {
    console.log('onNetworkQuality: ', uplinkNetworkQuality);
});

// View downlink network quality statistics
downlinkClient.on('onNetworkQuality', (_, downlinkNetworkQuality) => {
    console.log('onNetworkQuality: ', downlinkNetworkQuality);
});
```


You can also get the detailed statistics such as round\-trip time and packet loss rate through `onLocalStreamStats` and `onRemoteStreamStats`. The following table shows the network quality levels and their corresponding metrics.


|Network quality |uplinkClient packet loss rate |downlinkClient e2e delay |RTT |Receiver\-side freeze rate |
|---|---|---|---|---|
|Good, perfect for video calls |< 0.05 |< 600 ms |< 250 ms |< 0.15 |
|Poor, suggesting to lower bit rate |0.05 ~ 0.1 |600 ms ~ 1200 ms |250 ms ~ 1000 ms |0.15 ~ 0.3 |
|Bad, suggesting to switch to a better network |> 0.1 |> 1200 ms |> 1000 ms |> 0.3 |


```javascript
// View uplink network quality statistics
uplinkClient.on('onLocalStreamStats', stats => {
          console.log('onLocalStreamStats: ', stats);

// View downlink network quality statistics
downlinkClient.on('onRemoteStreamStats', stats => {
          console.log('onRemoteStreamStats: ', stats);
```


<span id="api-reference"></span>
## API reference


* [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality)

* [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstreamstats)

* [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestreamstats)
