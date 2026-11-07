---
title: "監聽 SEI 訊息"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listening-to-sei-messages-zh-TW"
---

SEI（Supplemental Enhancement Information，補充增強資訊）訊息作為嵌入於視訊串流中的資料通道。這提供了一種方式，可將自訂資料與特定視訊畫面同步，常用於在特定時間點顯示互動內容，例如問答、彈幕或虛擬道具。這能為您的觀眾創造更豐富且更具吸引力的觀看體驗。本主題說明如何使用 Player SDK for Web（VePlayer）來監聽並處理來自視訊串流的這些 SEI 訊息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議您使用最新版本的 Player SDK for Web。版本資訊請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-TW">Player SDK for Web：發行說明</a>。舊版資訊請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-TW">Web 端播放器 SDK：1.x 版本</a>。</div>


<span id="c6282244"></span>
## SEI 訊息格式

當播放器收到 SEI 訊息時，會觸發 `SEI` 事件，並包含以下資料：

```javascript
interface Data {
  originPts: number; // Original PTS.來源串流中視訊畫面的時間戳記。
  pts: number; // Adjusted PTS.在直播場景中，播放器會根據觀眾加入時間將顯示時間戳記重設為 0。
  time: number; // The time (in seconds) at which the SEI message occurs in the current live stream.
  data: {
    payload: Uint8Array; // The SEI payload.
    type: number;        // Type of the SEI message.
    size: number;        // Size of the SEI payload.
    uuid: string;        // UUID of the SEI message.若未提供則為空。
  }
}
```


<span id="前提条件"></span>
## 先決條件

您已整合 Player SDK for Web。如需更多資訊，請參閱 [整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

<span id="022c49f2"></span>
## 設定範例

建立 VePlayer 實例後，您可以透過訂閱 `VePlayer.live.Events.SEI` 事件來監聽 SEI 訊息，如下方範例所示。


<Tabs>
<Tab zoneid="aB94MX3QGE" title="來自 CDN">
<TabTitle>來自 CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/stream1.flv',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  veplayer.on(VePlayer.live.Events.SEI, function (data) {
    console.info('SEI message', data);
  });
});        
```



</Tab>
<Tab zoneid="XMQRVBct0x" title="透過 NPM">
<TabTitle>透過 NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { flv } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([flv]);

createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pulldomain/appname/mystream.flv',
  logger: {
    appId: '2****4',
    userId: '1********6',
    deviceId: '3********7',
  },
}).then(function (veplayer) {
  veplayer.on(live.Events.SEI, function (data) {
    console.info('SEI message', data);
  });
}); 
```



</Tab>
</Tabs>
