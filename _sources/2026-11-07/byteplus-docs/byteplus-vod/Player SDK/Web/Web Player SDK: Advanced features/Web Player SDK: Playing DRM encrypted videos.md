---
title: "Web Player SDK: Playing DRM encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/playing_drm_encrypted_videos_web"
---

BytePlus VOD supports DRM (Digital Rights Management) encryption for scenarios where copyright protection is necessary. The Web Player SDK supports playing DRM encrypted videos and is compatible with HLS and DASH protocols.

<span id="a10d9fb0"></span>
## Compatibility

<span id="c21e5182"></span>
### H.264 encoded HLS videos


|**Platform** |**Chrome** |**Safari** |**Edge** |**Firefox** |
|---|---|---|---|---|
|macOS |Version 41 and above |Version 10 and above |Version 79 and above |Version 38 and above |
|Windows |Version 41 and above |N/A |Version 16 and above |Version 38 and above |
|Android |Version 41 and above |N/A |Version 79 and above |Not supported |
|iOS |iOS 9 and above |iOS 9 and above |iOS 9 and above |iOS 9 and above |


<span id="0f9f12d1"></span>
### H.264 encoded DASH videos


|Platform |Chrome |Safari |Edge |Firefox |
|---|---|---|---|---|
|macOS |Version 41 and above |N/A |Version 79 and above |N/A |
|Windows |Version 41 and above |N/A |Version 79 and above |N/A |
|Android |Version 41 and above |N/A |Version 79 and above |N/A |
|iOS |N/A |N/A |N/A |N/A |


<span id="88304fcc"></span>
### H.265 encoded HLS videos


|Platform |Safari |
|---|---|
|macOS |Version 13 and above |
|iOS |Version 13 and above |


<span id="4559dccd"></span>
## Prerequisites


* To encrypt your content, complete the following task :

   * Get a DRM key from [Intertrust](https://portal.expressplay.com/) and get a FairPlay certificate from Apple.

   * Upload the DRM key and FairPlay certificate to the BytePlus VOD console.

   * Encrypt your audio and video files with DRM licenses using the BytePlus VOD media processing service.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption">DRM encryption overview</a>.      </div>
      

* Use the BytePlus VOD Server SDKs on your server to:

   * Generate the temporary playback token and DRM auth token and provide them to the client.

   * (Optional) Get the FairPlay certificate URL from the BytePlus VOD service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details, see the following articles:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk">Java SDK</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk">Python SDK</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk">PHP SDK</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk">Go SDK</a>   </div>
   


<span id="3fe29363"></span>
### Java SDK example

Here's an example of how to use the BytePlus VOD Java SDK to generate the required tokens for DRM playback:

```Java
// Java SDK Example for DRM Playback
package com.byteplus.example.vod.drm;


import com.byteplus.model.request.VodGetPlayInfoRequest;
import com.byteplus.model.request.VodGetDrmLicenseRequest;
import com.byteplus.model.response.VodGetPlayInfoResponse;
import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;


public class DrmPlaybackExample {


    public static void main(String[] args) {
        // Initialize VOD service
        IVodService vodService = VodServiceImpl.getInstance();
        // Call below method if you dont set ak and sk in ～/.byteplus/config
        vodService.setAccessKey("YOUR_ACCESS_KEY");
        vodService.setSecretKey("YOUR_SECRET_KEY");


        // Video ID of the DRM encrypted video
        String vid = "your-video-id";
    }


    // 1. Generate temporary playback token (PlayAuthToken)
    private static String generatePlayAuthToken(IVodService vodService, String vid) throws Exception {
        VodGetPlayInfoRequest.Builder reqBuilder = VodGetPlayInfoRequest.newBuilder();
        reqBuilder.setVid(vid);
        
        // Set FileType parameter (required for DRM content)
        // For DRM encrypted video, use one of these values:
        // - "drm_evideo": Widevine and FairPlay DRM encrypted video stream
        // - "drm_evideo_playready": PlayReady DRM encrypted video stream
        reqBuilder.setFileType("drm_evideo");
        
        // Set Format parameter (optional)
        // Options: "dash" or "hls" for DRM content
        reqBuilder.setFormat("hls");
        
        // Set token expiration time (in milliseconds)
        // Default is 1 hour (3600000 ms)
        String resp = vodService.getPlayAuthToken(reqBuilder.build(), 3600000L);
        return resp;
    }


    // 2. Generate DRM encryption token
    private static String generateDrmAuthToken(IVodService vodService, String vid, String drmType) throws Exception {
        VodGetDrmLicenseRequest.Builder reqBuilder = VodGetDrmLicenseRequest.newBuilder();
        reqBuilder.setVid(vid);
        // Set DRM type: "widevine", "fairplay", or "playready"
        // The value should match the browser/device capability
        reqBuilder.setThirdPartyDrmType(drmType);
        
        // Set token expiration time (in milliseconds)
        // Default is 1 hour (3600000 ms)
        String resp = vodService.getThirdPartyDrmAuthToken(reqBuilder.build(), 3600000L);
        return resp;
    }


    // 3. Get FairPlay certificate URL (only needed for FairPlay)
    private static String getFairPlayCertUrl(IVodService vodService, String certId) throws Exception {
        // Set token expiration time (in milliseconds)
        // Default is 1 hour (3600000 ms)
        String resp = vodService.getFairPlayCertUrl(certId, 3600000L);
        return resp;
    }
}
```


<span id="f014e0b9"></span>
## Implementation

You can only play DRM encrypted videos in Vid mode. The player will automatically choose the appropriate [EME](https://web.dev/articles/media-eme#how_does_eme_work) system for video playback based on the browser version and system environment. Sample code:

```JavaScript
const playerSdk = new VePlayer({
    lang: 'en',
    id: 'video',
    width: 600,
    height: 400,
    autoplay: true,
    getVideoByToken: {
        playAuthToken: 'your playAuthToken', // The temporary playback token
        thirdPartyDrmAuthToken: 'your thirdPartyDrmAuthToken', // The DRM auth token
        // Fairplay certificate URL. This URL is necessary for playback on Safari or iOS. You can upload the certificate to the BytePlus VOD service and then acquire the HTTPS URL
        serverCertificatePath: 'your fairplay cert http url',
         // Whether to enable anti-screen recording detection. When enabled, playback will be blocked with an error message if the current browser environment does not support anti-screen recording.
        unRecord: false
    },
    vodLogOpts: {
        line_app_id: 562771,
        tag: 'normal'
    }
});
```


When you want to switch to a different video, call `playNext` and provide the new video's `playAuthToken`, `thirdPartyDrmAuthToken`, and `serverCertificatePath`. Here is an example code snippet:

```JavaScript
playerSdk.playNext({
    getVideoByToken: {
        playAuthToken: 'new playAuthToken',
        thirdPartyDrmAuthToken: 'new thirdPartyDrmAuthToken',
        serverCertificatePath: 'new fairplay cert http url',
    },
})
```


<span id="990ed66e"></span>
## **Anti\-screen recording**

The DRM system's security features include anti\-screen recording functionality. Some browsers and systems do not support this feature due to differences in hardware acceleration support. Browsers known to lack this functionality are:


* Chrome and Chromium\-based browsers on Android

* Firefox on Windows, macOS, and Android


If anti\-screen recording is essential for your scenarios, check the browser environment before playback. For the above mentioned browsers, consider blocking playback and advising users to use a more secure browser for viewing.

&nbsp;
