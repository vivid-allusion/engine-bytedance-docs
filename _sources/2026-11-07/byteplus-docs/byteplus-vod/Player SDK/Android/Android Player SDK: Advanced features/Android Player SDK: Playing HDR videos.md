---
title: "Android Player SDK: Playing HDR videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-hdr-videos-android"
---

Compared to SDR (Standard Dynamic Range) videos, HDR (High Dynamic Range) videos have higher color depth, a wider dynamic range, and more powerful color expression. This makes pictures more realistic and layered, and intuitively enhances video picture quality, thereby effectively improving people's viewing experience.

This article explains how to play HDR videos using the Player SDK.

<span id="14ab5858"></span>
## Prerequisites


* Android system \>= 9.0

* Calling the `mVideoEngine.isSupportHDR()` method to check whether the device supports HDR.

* Use `SurfaceView` to play videos.

* Play H.265\-encoded HDR10 or HLG video sources.

* Use hardware decoding.


<span id="e1e5ca61"></span>
## Playing HDR sources in DirectUrl mode

To play HDR videos with the HTTP URL, you just need to set the `url` parameter:

```Java
// The unique identifier of the video
final String vid = "video id";
// The HTTP URL of the HRD video
final String url = "http://www.example.com/h264.mp4";
final String cacheKey = TTVideoEngine.computeMD5(url);

// 1. Assemble the video source
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(url)
                .setCacheKey(cacheKey)
                .build())
        .build();
       
// 2. Set the video source
ttVideoEngine.setStrategySource(directUrlSource);
// 3. Play the video
ttVideoEngine.play()
```


<span id="6cd4dc45"></span>
## Playing HDR sources in Vid mode

To play HDR videos with the video ID, follow these steps:


1. Get the HRD videos by using the BytePlus VOD media processing service. For details, see [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template).

2. Your app server generates temporary playback tokens with the `HDRDefinition` parameter being set and passes the token to the app client. You can use the BytePlus VOD Server SDKs to issue the temporary playback token. For details, refer to the following documents:

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

3. Switch to HDR playback. Sample code:

   ```Java
   ttVideoEngine.configResolution(High_HDR);
   ```
   

   The enumerations for HDR resolutions are as shown in the table below.

   
   |Enumeration |Resolution |Description |
   |---|---|---|
   |Standard_HDR |360P |Standard definition HDR |
   |High_HDR |480P |High definition HDR |
   |SuperHigh_HDR |720P |Ultra high definition HDR |
   |ExtremelyHigh_HDR |1080P |1080P HDR |
   |TwoK_HDR |2K |2K HDR |
   |FourK_HDR |4K |4K HDR |
   

4. (Optional) Get the list of all supported definitions. Sample code:

   ```java
   ttVideoEngine.setVideoInfoListener(new VideoInfoListener() {
       @Override
       public boolean onFetchedVideoInfo(VideoModel videoModel) {
           // Callback for successful video data retrieval
           Log.v("VideoPlay", "onFetchedVideoInfo " + videoModel);
           if (videoModel == null) return false;
           
           // Get an array of resolutions for the current VideoModel, which can be used to display the resolution list
           Resolution[] resolutions = ttVideoEngine.supportedResolutionTypes();
             
           return false;
       }
   });
   ```
   

5. (Optional) Check whether a certain definition is HDR. Sample code:


```Java
private boolean isHDRResolution(Resolution resolution) {
    return resolution.toString(TYPE_VIDEO).contains("HDR");
}
```


&nbsp;
