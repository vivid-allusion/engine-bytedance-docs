---
title: "Web 推流 SDK：本地合流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-local_mixing-zh-CN"
---

要将多个视频和音频源（如摄像头、屏幕共享、麦克风和系统音频）合并为一个输出流，可以使用 BytePlus MediaLive 推流 SDK for Web。本指南提供了启用**本地合流**的分步操作说明，帮助你降低带宽使用量、自定义视频布局，并灵活管理音频源。


* **降低带宽使用量**：在本地将多个流合并为一个输出流，最大程度减少上行带宽消耗。

* **自定义布局**：调整每个视频的大小、位置和层级。

* **灵活音频管理**：混合不同音频源并控制各自音量。


<span id="922d04f5"></span>
## 工作原理

在**BytePlus MediaLive 推流 SDK**中，音频和视频的处理方式会根据是否已开启**本地合流**而有所不同。SDK 提供两种模式：


* **默认模式（本地合流未开启，自动合流）** 

   * **使用场景**：仅包含摄像头和麦克风的简单推流。

   * **行为**：

      * 采集到的音频和视频流**会自动包含**在输出流中，无需手动操作。

      * SDK 会在内部完成音视频合流，并将最终流推送到服务器。

* **本地合流模式（手动流管理）** 

   * **使用场景**：多个视频源（如摄像头 + 屏幕共享）或更复杂的音频混合（如麦克风 + 系统音频）。

   * **行为**：

      * 采集到的音频和视频流**不会自动包含**在输出流中。你需要手动添加这些流。

      * 你需要调用：

         * `addVideoStream()`，将视频轨道添加到合流画布。

         * `addAudioStream()`，将音频轨道添加到混音器。


<span id="962898ec"></span>
## 前提条件


* 你已按照[集成指南](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web)完成 SDK 初始化，并获取了`livePusher`对象。

* 你已登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/locationGenerate)，生成 RTM 推流地址。


<span id="6d5c9766"></span>
## 操作流程


1. **启用本地合流**


在开始推流前，调用以下方法启用本地合流，使 SDK 能够合并多个音频和视频流：

```JavaScript
livePusher.enableMixing(true);
```



2. **配置合流属性**


使用`setMixingConfig`方法，指定合流视频的分辨率、帧率、背景色等属性：

```JavaScript
livePusher.setMixingConfig({
  width: 1080,               // Width of the mixing canvas
  height: 720,               // Height of the mixing canvas
  frameRate: 30,             // Frame rate of the merged video
  backgroundColor: '#000000',// Background color of the canvas
});
```



3. **采集多个媒体源**


启用本地合流后，采集到的源不会自动添加到流中。你需要手动将每个源的流 ID 添加到合流画布或音频混音器。以下是采集摄像头、屏幕共享和麦克风流的示例：

```JavaScript
const cameraStreamId = await pushClient.startCamera();
const screenStreamId = await pushClient.startScreenCapture();
const micStreamId = await pushClient.startMicrophone();
```



* 这些方法可能会触发浏览器权限弹窗。确保用户授予摄像头和麦克风访问权限。

* 屏幕共享的实现方式在不同浏览器间有所差异。请根据目标浏览器处理权限和兼容性。

4. **手动将流添加到合流会话**


在本地合流模式下，流不会自动添加。你需要显式添加这些流：


* **将视频流添加到合流画布**

   ```JavaScript
   livePusher.addVideoStream([{
     streamId: screenStreamId,
     width: 1280,
     height: 720,
     x: 1280 / 2,
     y: 720 / 2,
     zOrder: 1,
     keepRatio: true,
   }, {
     streamId: cameraStreamId,
     width: 320,
     height: 180,
     x: 320 / 2,
     y: 180 / 2,
     zOrder: 2,
     keepRatio: true,
   }]);
   ```
   

   * `x`和`y`用于定义视频在画布上的中心点位置。画布的坐标系以左上角为原点 (0,0)。

   * `zOrder`用于控制视频的堆叠顺序（层级）。具有更高`zOrder`值的视频会显示在值较低的视频之上。

   * 当`keepRatio`设置为`true`时，视频在缩放过程中会保持原始视频长宽比。

* **将音频流添加到混音器**

   ```JavaScript
   livePusher.addAudioStream({
     streamId: micStreamId,
     volume: 100,
   });
   ```
   

   * 对于多个音频源（例如外部文件或自定义音频源），需分别为每个源调用`addAudioStream`。

   * 使用`volume`调整每个音频流的初始音量。

5. **开始推流**


最后，调用`startPush`方法，并提供推流地址（由控制台生成），以启动直播流：

```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```
