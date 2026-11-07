---
title: "iOS Player SDK: Enabling QUIC playback acceleration"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs_enabling_quic_playback_acceleration_ios"
---

The Player SDK supports QUIC (HTTP/3) transport protocol. Based on our internal testing, enabling QUIC in weak network scenarios (such as packet loss and bandwidth throttling) can reduce the time\-to\-first\-frame and playback stuttering rates, significantly improving the playback experience in extreme network conditions.

The SDK provides the following two strategies for enabling QUIC:


* **Standard negotiation mode:**  Follows the standard QUIC protocol flow. The player internally performs intelligent racing between TCP and QUIC, and automatically selects the optimal link based on the network conditions and server responses.

* **Forced QUIC for specific domain names:**  Bypasses the standard protocol probing phase for core domain names known to support QUIC. By using pre\-configured domain hints, the SDK establishes a QUIC connection on the first hop, reducing the time\-to\-first\-frame and improving playback stability in high\-loss network environments.


<span id="cb5a230e"></span>
## Prerequisites


* **SDK version:**  Use \*\*\*\* 1.46.200.1 or later.

* **Dependency requirements:**  Add the relevant dependency to your project's `Podfile` and specify the `subspecs` that includes `Player-Quic`.

   ```Ruby
   # Podfile
   # Please replace the version number with the actual version you use.
   pod 'TTSDK', 'x.xx.x.x', :subspecs => ['Player-Quic']
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, <code>subspecs</code> does not support specifying both <code>Player-SR</code> (Super Resolution) and <code>Player-Quic</code> (QUIC) simultaneously through manual configuration. If your business requires both features, please <a href="https://console.byteplus.com/workorder/create">contact us</a> for a customized integration plan.   </div>
   

* **Server support:** 

   * Ensure that you have enabled QUIC protocol support for your CDN domains.

   * Ensure that the response headers of the video include the `Content-Length` field.


<span id="80becb81"></span>
## **Standard negotiation mode**

In this mode, the SDK automatically switches between TCP and QUIC based on network conditions and server responses.

```objectivec
// 1. Enable the new network download module (Required for QUIC).
[TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEMDLKeyIsEnableMDL2_BOOL) value:@(YES)];

// 2. Enable QUIC downloader.
[TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEMDLKeyIsEnableTTNetDownloader_BOOL) value:@(YES)];

TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:appId licenseName:licenseName];

TTSDKTTNetConfiguration* ttnetConfig = [[TTSDKTTNetConfiguration alloc] init];

// 3. Enable global QUIC switch.
ttnetConfig.shouldEnableQuic = YES;
configuration.ttnetConfiguration = ttnetConfig;

// 4. Initialize the SDK.
[TTSDKManager startWithConfiguration:configuration];
```


<span id="1dedf9da"></span>
## Forced QUIC for specific domains

Use the following configurations to skip the standard "TCP probing first" phase for core business domains, to achieve a faster first\-frame time by implementing First\-Hop QUIC.

```objectivec
// 1. Enable the new network download module.
[TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEMDLKeyIsEnableMDL2_BOOL) value:@(YES)];

// 2. Enable QUIC downloader.
[TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEMDLKeyIsEnableTTNetDownloader_BOOL) value:@(YES)];

// 3. Critical configuration: Disable internal SDK probing and domain blacklisting logic to force QUIC.
// ttnet_enable_quic_probe: 0 disables probing; ttnet_enbale_quic_broken: 0 disables blacklisting logic.
[TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEMDLKeyIsTemporaryOptStr_NSString) value:@"{\"ttnet_enable_quic_probe\": 0, \"ttnet_enbale_quic_broken\": 0}"];

TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:appId licenseName:licenseName];
TTSDKTTNetConfiguration* ttnetConfig = [[TTSDKTTNetConfiguration alloc] init];

// 4. Enable global QUIC switch.
ttnetConfig.shouldEnableQuic = YES;

// 5. Specify domains and ports (usually 443) to force QUIC. You can add multiple domains.
// Once configured, the player will attempt the QUIC protocol directly on the very first network request for these domains.
NSMutableDictionary* hints = [NSMutableDictionary dictionary];
hints[@"www.example.com"] = @(443);
hints[@"video.test.com"] = @(443);
ttnetConfig.quicHints = hints;
configuration.ttnetConfiguration = ttnetConfig;

// 6. Initialize the SDK.
[TTSDKManager startWithConfiguration:configuration];
```
