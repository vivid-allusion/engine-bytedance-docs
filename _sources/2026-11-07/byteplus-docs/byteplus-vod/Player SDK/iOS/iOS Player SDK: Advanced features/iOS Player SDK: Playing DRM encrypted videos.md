---
title: "iOS Player SDK: Playing DRM encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-drm-videos-ios"
---

BytePlus VOD supports DRM (Digital Rights Management) encryption for scenarios requiring copyright protection. This article introduces how to play DRM\-encrypted videos using the Player SDK.

<span id="511315ad"></span>
## Prerequisites


* Configure the DRM licenses and encrypt your content in the BytePlus VOD console. For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption).

* Download your FairPlay certificate to your local device and save it in your project's sandbox directory. For details, see [Getting a FairPlay certificate from Apple](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-fairplay-certificate).

* To play DRM encrypted videos in Vid mode, your application server needs to generate temporary playback token and DRM auth token before playback, and then provide them to the client. You can use the BytePlus VOD Server SDKs to generate these tokens. For more information, refer to the documentation provided below:

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* Integrate the Player SDK 1.42.300.102 or later versions.


<span id="6c12304f"></span>
## Implementation


1. Obtain the sandbox FairPlay certificate file:

   ```objectivec
   - (NSData *)getAppCertificateData {
       // Ensure that the FairPlay certificate file has been placed in the local sandbox directory
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"fairplay" ofType:@"cer"];
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       
       if (certificate == NULL) {
           NSLog(@"Failed to read fairplay certificate");
       }
       NSLog(@"certificate : %@", certificate);
   
       return certificate;
   }
   ```
   

2. Build the video source:

   ```objectivec
   NSString *videoId = @"video id";
   NSString *playAuthToken = @"play auth token"; // Obtained from your app server
   NSString *fpsLicenseAuthToken = @"drm license auth token"; // Obtained from your app server
   NSData *fpsCertData = [self getAppCertificateData]; // Get the FairPlay certificate
   TTVideoEngineResolutionType *resolution = TTVideoEngineResolutionTypeHD; // Initial video resolution
   
   TTVideoEngineVidSource *drmVidSource = [[TTVideoEngineVidSource alloc] initWithVid:videoId playAuthToken:playAuthToken fpsLicenseAuthToken:fpsLicenseAuthToken fpsCertData:fpsCertData resolution:resolution];
   ```
   

3. Initialize the video player:

   ```objectivec
   // Fairplay only supports playback with the system player. Initialize the system player.
   - (void)createVideoEngine {
       TTVideoEngine *videoEngine = [[TTVideoEngine alloc] initWithType:TTVideoEnginePlayerTypeSystem];
       self.videoEngine = videoEngine;
   }
   ```
   

4. Set the video source and start playback:

   ```objectivec
   // Set the DRM video source
   [self.videoEngine setVideoEngineVideoSource:drmVidSource];
   // Start playback
   [self.videoEngine play];
   ```
