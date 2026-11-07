---
title: "Web Player SDK: Dynamic buffer"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/dynamic_buffer_web"
---

By default, VePlayer sets different minimum buffer durations for MP4 MSE playback and DASH playback, with 10 seconds for MP4 and 50 seconds for DASH. When the remaining buffer duration is less than the minimum buffer duration, VePlayer starts loading new video data. On this basis, to counteract the impact of network jitter on the playback experience and reduce wasted bandwidth charges, VePlayer supports dynamic buffers. Dynamic buffer refers to dynamically adjusting the remaining buffer duration according to network conditions during playback to improve playback experience and reduce wasted bandwidth charges. By dynamically adjusting the remaining buffer time, VePlayer can maintain a high buffer level when the network condition is poor, thereby reducing playback experience issues caused by insufficient cache. Meanwhile, when the network condition is good, it can maintain a low buffer level to reduce wasted bandwidth charges. This can effectively improve the smoothness and stability of video playback, while also optimizing the utilization of network resources. The difference between loading with regular buffer and dynamic buffer is shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5487c9510c14ab3b10714636bac0b07~tplv-goo7wpa0wc-image.image) </span>

The example code below shows how to enable the dynamic buffer function. You need to set the video `duration` and use the `adaptRange` parameter to configure the dynamic buffer function. You also need to set a reasonable minimum and maximum cache duration (`minCacheDuration` and `maxCacheDuration`) based on the format and duration of the video.

```JavaScript
new VePlayer({
   id: 'video',
   url: 'https://example.com/af2534***/*****1/stream.mp4',
   // Enable MP4 MSE playback.
   enableMp4MSE: true,
   duration: 132,
   // Configure dynamic buffer.
   adaptRange: {
      enable: true, // Enable dynamic buffer functionality.
      // Minimum cache duration, in seconds
      minCacheDuration: 12,
      // Maximum cache duration, in seconds
      maxCacheDuration: 30,
   }
})
```


You can use the following recommended values for different video durations and formats to set the minimum and maximum cache durations:


|Video duration |MP4 |DASH |
|---|---|---|
|0–3 mins |* minCacheDuration: 6 s<br><br>* maxCacheDuration: 15 s |* minCacheDuration: 6 s<br><br>* maxCacheDuration: 15 s |
|3–30 mins |* minCacheDuration: 10 s<br><br>* maxCacheDuration: 28 s |* minCacheDuration: 15 s<br><br>* maxCacheDuration: 30 s |
|Other scenarios |* minCacheDuration: 12 s<br><br>* maxCacheDuration: 30 s |* minCacheDuration: 30 s<br><br>* maxCacheDuration: 60 s |
