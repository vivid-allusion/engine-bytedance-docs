---
title: "iOS Player SDK: Playing HDR videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-hdr-videos-ios"
---

Compared to SDR (Standard Dynamic Range) videos, HDR (High Dynamic Range) videos have higher color depth, a wider dynamic range, and more powerful color expression. This makes pictures more realistic and layered, and intuitively enhances video picture quality, thereby effectively improving people's viewing experience. This article explains how to play HDR videos using the Player SDK.

<span id="14ab5858"></span>
## Prerequisites


* Use hardware decoding. The SDK enables hardware decoding by default.

* Play H.265\-encoded HDR10 or HLG video sources.

* Calling the `TTVideoEngine.isSupportHDR` method to check whether the device supports HDR.


<span id="e1e5ca61"></span>
## Playing HDR sources in DirectUrl mode

To play HDR videos with the HTTP URL, you just need to set the `url` parameter:

```objectivec
// Play video in DirectUrl mode
// @param url The playback URL
// @param key The cache key of the video. It is recommended to use a unique identifier for the video, such as the MD5 value of the URL
// @param isHDRUrl YES for HDR video
- (void)playWithUrl:(NSString *)url key:(NSString *)key isHDRUrl:(BOOL)isHDRUrl {
    TTVideoEngineUrlSource *source = [[TTVideoEngineUrlSource alloc] initWithUrl:url cacheKey:key];
    if (isHDRUrl && [self.videoEngine isSupportHDR]) {
        source.isHDRSource = YES;
    }
    [self.videoEngine ls_setDirectURLSource:source];
}
```


<span id="6cd4dc45"></span>
## Playing HDR sources in Vid mode

To play HDR videos with the video ID, follow these steps:


1. Get the HDR videos by using the BytePlus VOD media processing service. For details, see [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template).

2. Your app server generates temporary playback tokens with the `HDRDefinition` parameter being set and passes the token to the app client. The values of the `HDRDefinition` parameter are explained as follows:

   * If you set `HDRDefinition` to `all`, it requests videos of all available HDR and SDR resolutions.

   * Set `HDRDefinition` to `4k`, `2k`, `1080p`, `720p`, `480p`, or `360p` to request specific resolutions. For example, setting `HDRDefinition` to `1080p` requests the 1080p HDR and SDR resolutions. If the 1080p resolution is not available, it will return all available HDR resolutions, and you can handle them accordingly.

      You can use the BytePlus VOD Server SDKs to issue the temporary playback token. For details, refer to the following documents:

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

3. Switch to HDR playback. For details, see [Set the resolution](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-ios#60e86b22). The enumerations for HDR resolutions are as shown in the table below.

   
   |Enumeration |Resolution |Description |
   |---|---|---|
   |TTVideoEngineResolutionTypeHDR_360P |360P |Standard definition HDR |
   |TTVideoEngineResolutionTypeHDR_480P |480P |High definition HDR |
   |TTVideoEngineResolutionTypeHDR_720P |720P |Ultra high definition HDR |
   |TTVideoEngineResolutionTypeHDR_1080P |1080P |1080P HDR |
   |TwoK_HDR |2K |2K HDR |
   |FourK_HDR |4K |4K HDR |
   

4. (Optional) Get the list of all supported definitions. Sample code:

   ```objectivec
   // Handle according to your own business logic and UI style.
   NSArray<NSNumber *> *allSupportedResolutions = [engine supportedResolutionTypes];
   ```
   

5. (Optional) Check whether a certain definition is HDR. Sample code:


```objectivec
// Check if it is an HDR resolution.
// @param  resolutionType Resolution
- (BOOL)isHDRResolution:(TTVideoEngineResolutionType)resolutionType {
    NSDictionary<NSString *, NSNumber *> *resolutionMapDic = [self.videoEngine resolutionMap];
    for (NSString *key in resolutionMapDic.allKeys) {
    NSNumber *resolutionObj = [resolutionMapDic objectForKey:key];
        if ([resolutionObj integerValue] == resolutionType && [[key lowercaseString] containsString:@"hdr"]) {
            return YES;
        }
    }
    return NO;
}
```


&nbsp;
