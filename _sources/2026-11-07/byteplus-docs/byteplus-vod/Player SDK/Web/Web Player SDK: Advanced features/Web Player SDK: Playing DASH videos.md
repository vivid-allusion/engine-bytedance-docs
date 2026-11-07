---
title: "Web Player SDK: Playing DASH videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/playing_dash_videos_web"
---

<span id="0f625003"></span>
## Compatibility


|**System or browser** |**Description** |
|---|---|
|Chrome |57 or later |
|Edge |Windows 10 or later |
|iOS |iPadOS 13 or later |
|Android |Android 5 or later<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Web Player SDK can not play HLS encrypted videos when the player is hijacked by browsers such as UC, QQ, and built\-in browsers (such as VIVO).</div><br> |
|||
|||
|||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is not recommended to play DASH videos on mobile browsers.</div>


<span id="a69965e4"></span>
## **Implementation**

To play DASH videos, whether they are encrypted or not, you only need to generate a `playAuthToken` on your app server and pass it to the Web Player SDK.

```JavaScript
const playerSdk = new VePlayer({
  id: 'mse',
  width: 800,
  height: 500,
  streamType: 'dash',
  getVideoByToken: {
    playAuthToken: 'playAuthToken' // The playAuthToken of DASH videos
  }
});
```


You can also obtain the playback information of DASH and set the DASH playback configuration.

```JavaScript
const Service = window.VePlayer.Service;

const playAuthToken = 'playAuthToken'; // The playAuthToken of DASH videos
Service.url(playAuthToken, '//vod.volcengineapi.com').then((res) => {
  // DASH playback configuration
  const playerSdk = new VePlayer({
    id: 'mse',
    lang: 'zh',
    width: 800,
    height: 500,
    DASHPlugin: {
      vid: res.Vid,
      playInfoType: 'TOP',
      getLicenseUrl: '//i.snssdk.com/video/drm/v1/play_licenses',
      definitionText: { '360p': '360p', '480p': '480p', '720p': '720p', '1080p': '1080p' },
      defaultDefinition: '360p',
      preloadTime: 180,
      defaultFormat: 'dash',
      dashOpts: { Data: res }
    }
  });
});
```


&nbsp;
