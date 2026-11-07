---
title: "iOS Player SDK: Playing FairPlay-encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/playing-fairPlay-encrypted-videos-ios"
---

FairPlay Streaming (FPS) is Apple's Digital Rights Management (DRM) technology designed to protect video content delivered via the HLS protocol. This guide provides a comprehensive walkthrough on how to use the Player SDK to implement the complete lifecycle for FairPlay\-encrypted videos, including **online playback**, **downloading for offline use**, and **offline playback**.

<span id="1f9c95b3"></span>
## Prerequisites


* SDK version: 1.49.100.2 or later versions

* Playback method: Only HLS videos played via Vid + PlayAuthToken + DrmAuthToken are supported.

* Before starting client\-side integration, you must configure FairPlay encryption and transcoding settings in the BytePlus VOD console. For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption).


<span id="aa59bbc4"></span>
## Playing online FairPlay\-encrypted videos


1. Acquire the FairPlay certificate (the `.cer` file) from your Apple Developer account and provide its content to the SDK as `NSData`. The following example shows how to read the certificate file from your project's bundle:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For how to get the FairPlay certificate file from your Apple Developer account, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-getting-fairplay-certificate">Getting a FairPlay certificate from Apple</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Best practices for certificate management: Since FairPlay certificates have an expiration date, it is highly recommended to manage them as follows to ensure continuous validity:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Store and manage your FairPlay certificates on a cloud server.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When playback is initiated, the client app dynamically fetches the latest valid certificate from your server and passes its content to the Player SDK.   </div>
   

   ```objectivec
   - (NSData *)getAppCertificateData {
       // Ensure the FairPlay certificate file exists in the app's sandbox.
       // The certificate is obtained from the Apple Developer portal.
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"fairplay" ofType:@"cer"];
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       
       if (certificate == NULL) {
           NSLog(@"Failed to read FairPlay certificate");
       }
       NSLog(@"Certificate data loaded: %@", certificate);
   
       return certificate;
   }
   ```
   

2. Set the playback source and start playback:

   ```objectivec
   // 1. Build the DRM play source
   NSString *videoId = @"your_video_id"; // Obtained from your application server
   NSString *playAuthToken = @"your_play_auth_token"; // Obtained from your application server
   NSString *fpsLicenseAuthToken = @"your_drm_license_auth_token"; // Obtained from your application server
   NSData *fpsCertData = [self getAppCertificateData]; // Get the FairPlay certificate data
   TTVideoEngineResolutionType resolution = TTVideoEngineResolutionTypeHD; // Specify the initial resolution
   
   // Use the initializer designed for DRM scenarios
   TTVideoEngineVidSource *drmVidSource = [[TTVideoEngineVidSource alloc] initWithVid:videoId playAuthToken:playAuthToken fpsLicenseAuthToken:fpsLicenseAuthToken fpsCertData:fpsCertData resolution:resolution];
   
   // 2. Initialize and configure the player
   // FairPlay only supports the system player (AVPlayer).
   TTVideoEngine *videoEngine = [[TTVideoEngine alloc] initWithType:TTVideoEnginePlayerTypeSystem];
   self.videoEngine = videoEngine;
   
   // Key: Enable the FairPlay option.
   [videoEngine setOptionForKey:VEKKeyDrmType_ENUM value:@(TTVideoEngineDrmFairPlay)];
   
   // Set to YES to allow the player to automatically hit the offline cache if it exists.
   self.videoEngine.fairPlayOffline = YES;
   
   // 3. Set the playback source and start playback
   [self.videoEngine setVideoEngineVideoSource:drmVidSource];
   [self.videoEngine play];
   ```
   


<span id="b6550966"></span>
## Downloading FairPlay\-encrypted videos

The SDK provides the `TTVideoEngineFpsDownloadTask` class to handle the downloading of FairPlay\-encrypted videos.

<span id="ed097c86"></span>
### Step 1: Create the download task

Create a download task instance for each video you need to download.

```objectivec
// Create a TTVideoEngineFpsDownloadTask and set its delegate to receive callbacks.
// The `getAppCertificateData` method is the same as in the online playback section.
if (self.fpsTask == nil) {
    TTVideoEngineFpsDownloadTask *task = [[TTVideoEngineFpsDownloadTask alloc] initWithVideoId:self.model.vid playAuthToken:self.model.playAuthToken fpsLicenseToken:self.model.fpdrmAuthToken fpsCertificateData:[self getAppCertificateData] resolution:TTVideoEngineResolutionTypeHD];
    task.delegate = self;
    self.fpsTask = task;
}
```


<span id="774935d7"></span>
### Step 2: Control the download task

You can start, pause, and cancel the download by calling methods on the task instance.

```objectivec
// Start or resume the download task
[self.fpsTask resume];

// Pause the download task
[self.fpsTask pause];

// Cancel the download task (cannot be resumed after cancellation)
[self.fpsTask cancel];
```


<span id="a43cf64c"></span>
### Step 3: Listen for download callbacks

By implementing the `TTVideoEngineFpsDownloadTaskDelegate` protocol, you can monitor the download progress and completion status.

```objectivec
#pragma mark - TTVideoEngineFpsDownloadTaskDelegate

// Progress callback
- (void)videoEngineFpsDownloadTask:(TTVideoEngineFpsDownloadTask *)FpsDownloadTask downloadProgress:(double)downloadProgress {
    // `downloadProgress` ranges from 0.0 to 1.0
    NSLog(@"[FairPlay Download] Progress: %.2f%%", downloadProgress * 100);
    self.fpsTipLabel.text = [NSString stringWithFormat:@"Downloading: %.2f%%", downloadProgress * 100];
}

// Completion callback
- (void)videoEngineFpsDownloadTask:(TTVideoEngineFpsDownloadTask *)FpsDownloadTask didFinish:(NSURL *)localURL error:(NSError *)error {
    if (error) {
        NSLog(@"[FairPlay Download] Finished with error: %@", error);
        self.fpsTipLabel.text = [NSString stringWithFormat:@"Download failed: %@", error.localizedDescription];
    } else {
        NSLog(@"[FairPlay Download] Finished successfully. Location: %@", localURL.absoluteString);
        self.fpsTipLabel.text = @"Download finished.";
        self.fpsFileURL = localURL.absoluteString; // Save the local file URL for debugging or management
    }
}
```


<span id="8ff2a8f6"></span>
## Playing offline FairPlay\-encrypted videos

The implementation of playing a downloaded FairPlay video is **identical to playing an online video**. You do **not** need to worry about whether the video has been downloaded, nor do you need to manually pass a local file path. Simply follow the steps in the [Playing online FairPlay-encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/84305#aa59bbc4) section to initialize the player and set the `TTVideoEngineVidSource`. When you call `play`, if the SDK detects that a completed offline download exists that matches the current `vid` and `resolution`, it will automatically and seamlessly switch to playing the local file instead of making a network request.
