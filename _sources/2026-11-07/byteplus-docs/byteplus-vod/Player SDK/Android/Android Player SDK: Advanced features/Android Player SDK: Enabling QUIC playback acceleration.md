---
title: "Android Player SDK: Enabling QUIC playback acceleration"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs_enabling_quic_playback_acceleration_android"
---

The Player SDK supports QUIC (HTTP/3) transport protocol. Based on our internal testing, enabling QUIC in weak network scenarios (such as packet loss and bandwidth throttling) can reduce the time\-to\-first\-frame and playback stuttering rates, significantly improving the playback experience in extreme network conditions.

The SDK provides the following two strategies for enabling QUIC:


* **Standard negotiation mode:**  Follows the standard QUIC protocol flow. The player performs intelligent racing between TCP and QUIC, and automatically selects the optimal link based on the network conditions and server responses.

* **Forced QUIC for specific domain names:**  Bypasses the standard protocol probing phase for core domain names known to support QUIC. By using pre\-configured domain hints, the SDK establishes a QUIC connection on the first hop, reducing the time\-to\-first\-frame and improving playback stability in high\-loss network environments.


<span id="d95c94fd"></span>
## Prerequisites


* **SDK version:**  1.46.200.2 or later.

* **Integrated QUIC components:**  You need to integrate ttnet module into `app/build.gradle` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If SDK version < 1.50.100.1: Use ttnet version 1.46.200.2.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If SDK version ≥ 1.50.100.1: The ttnet version should match the SDK version. For example, use ttnet version 1.50.100.1 if the SDK is 1.50.100.1.   </div>
   

   ```Groovy
   implementation "com.bytedanceapi:ttsdk-ttnet:your version number"
   // If you are using a version earlier than 1.50.100.1, you also need to add the following dependency:
   // implementation "com.ss.mediakit:ttnetloader:1.1.190.1-tob"
   ```
   

* **Server support:**  Ensure your CDN domain names have QUIC protocol support enabled.


<span id="26647507"></span>
## Standard negotiation mode

In this mode, the SDK responds based on the network conditions and server responses.

```Java
QuicConfig quicConfig = new QuicConfig();
// 1. Enable QUIC.
quicConfig.enable = true;
TTNetConfig config = new TTNetConfig.Builder()
                .setQuicConfig(quicConfig)
                .build();
TTNetManager.initTTNet(this, config);

// 2. Enable QUIC downloader.
// If your SDK version is below 1.50.100.1, you need to configure the following setIntValue to enable QUIC downloader. 
// For versions 1.50.100.1 and above, the SDK enables these by default.
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ENABLE_TTNETLOADER, 1);
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_NEED_MDL_LOAD_MDLV2_LIB, 1);
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ENABLE_MDLV2, 1);

// 3. Initialize the SDK.
Env.start(new Config.Builder()
     ....
    .build());
```


<span id="fdab50b1"></span>
## Forced QUIC for specific domains

Use the following configurations to skip the standard "TCP probing first" phase for core business domains, to achieve a faster first\-frame time by implementing First\-Hop QUIC.

```Java
// 1. Disable the internal SDK logic for QUIC probing and temporary domain blacklisting.
DataLoaderHelper.getDataLoader().setStringValue(DATALOADER_KEY_STRING_MDL_TEMP_OPTS,"{\"ttnet_enable_quic_probe\":0,\"ttnet_enbale_quic_broken\":0}");

// 2. Enable QUIC and configure acceleration domain names.
QuicConfig quicConfig = new QuicConfig();
Map<String, Pair<Integer, Integer>> quicHint = new HashMap<>();
// Set the domains for forced QUIC (QUIC Hints). Otherwise, the SDK probes internally based on standard logic.
quicHint.put("xxx.xxx.com", new Pair<>(443, 443));
// Enable QUIC support.
quicConfig.enable = true;
quicConfig.quicHint = quicHint;

TTNetConfig config = new TTNetConfig.Builder()
                .setQuicConfig(quicConfig)
                .build();
// Initialize the network components.
TTNetManager.initTTNet(this, config);

// 3. Enable QUIC downloader.
// If your SDK version is below 1.50.100.1, you need to configure the following setIntValue to enable QUIC downloader. 
// For versions 1.50.100.1 and above, the SDK enables these by default.
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ENABLE_TTNETLOADER, 1);
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_NEED_MDL_LOAD_MDLV2_LIB, 1);
// TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ENABLE_MDLV2, 1);

// 4. Initialize the SDK.
Env.start(new Config.Builder()
     ....
    .build());
```
