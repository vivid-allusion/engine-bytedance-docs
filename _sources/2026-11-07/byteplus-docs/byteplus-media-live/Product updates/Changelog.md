---
title: "Changelog"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog"
---

To stay informed about the latest developments for BytePlus MediaLive, you can use this topic as a central resource. It provides a comprehensive and chronological log of all product updates, including new features, SDK releases, API changes, and documentation improvements, with links to related documents for more details.

## October 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for Web |Version 2.13.0 was released. Added SEI delay statistics to the playback information returned by `getRTMStats()` and `getFLVStats()`, including server\-to\-server delay and server\-to\-end delay. |2026\-10\-21 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |
|Latency analysis |Added support for inserting server timestamp data into SEI messages for all live streams under a domain name space. You can use BytePlus MediaLive Player SDKs or your own SEI parser to calculate and analyze live streaming latency. |2026\-10\-21 |[Inserting server timestamp data into SEI messages](https://docs.byteplus.com/docs/byteplus-media-live/inserting-server-timestamp-data-into-SEI-messages) |
|AI Dubbing and subtitle configuration |* Added support for writing subtitles into SEI messages in live streams.<br><br>* Added support for configuring a callback URL. |2026\-10\-21 |* [AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation)<br><br>* [Managing subtitle configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration) |
|Callback |Added AI Dubbing callbacks. When an AI Dubbing task starts or ends, stream relay succeeds or fails, an alarm is triggered, or subtitles are generated, BytePlus MediaLive sends a callback message to the configured callback URL. These callbacks apply to AI Dubbing tasks and subtitle configurations. |2026\-10\-21 |[Callback description](https://docs.byteplus.com/docs/byteplus-media-live/docs-callback-description#ai-dubbing) |
|Server\-side OpenAPI |* Added support for specifying whether to write subtitles into SEI messages in live streams and for configuring a callback URL when creating an AI Dubbing task or adding or updating a subtitle configuration.<br><br>* Added support for returning SEI and callback configurations when listing subtitle configurations or querying subtitle configuration details. |2026\-10\-21 |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Player SDK for Android |Version 1.52.200.1 was released. |2026\-10\-14 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Version 1.52.200.1\-premium was released. |2026\-10\-14 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## September 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for iOS |Version 1.52.100.4\-premium was released. |2026\-09\-17 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Player SDK for Android |Version 1.52.100.5 was released. |2026\-09\-17 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Watermark |* Added support for dynamic watermarks.<br><br>* Added support for applying watermark configurations to selected transcoded stream or ABR substream suffixes. |2026\-09\-07 |[Managing watermark configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks) |
|Server\-side OpenAPI |Updated watermark APIs to support dynamic watermarks and applying watermark configurations to selected transcoded stream or ABR substream suffixes. |2026\-09\-07 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |

## August 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|SDK management |* Added support for modifying **PackageName**, **Bundle ID**, wildcard domain, or WebOTT application identifier of an SDK application.<br><br>* After an SDK application is deleted, any **PackageName**, **Bundle ID**, wildcard domain, or WebOTT application identifier bound to the application is made available again. |2026\-08\-24 |* [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)<br><br>* [Managing SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses) |
|Player SDK for iOS |Versions 1.51.300.2\-premium and 1.51300.3\-premium were released. |2026\-08\-24 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Player SDK for Android |Version 1.51.300.2 was released. |2026\-08\-24 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Server\-side OpenAPI |Added support for configuring the HTTP request headers included in pull stream requests when a relay task pulls content from a live source or a VOD source. The supported headers are `Referer` and `UserAgent`. |2026\-08\-13 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Player SDK for Android |Version 1.51.200.4 was released. |2026\-08\-04 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Android |Version 1.51.100.8 was released. |2026\-08\-03 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |

## July 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for iOS |Version 1.51.200.4\-premium was released. |2026\-07\-23 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Pull stream address |Added support for generating RTM and RTM\-ABR pull stream addresses for the BytePlus MediaLive Player SDK for Web. These addresses support automatic transcoding, including B\-frame removal and AAC\-to\-Opus audio conversion. |2026\-07\-22 |* [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses)<br><br>* [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)<br><br>* [Playing RTM-ABR streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr#c552533f)<br><br>* [Pulling RTM streams](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |

## June 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for iOS |Version 1.51.100.3\-premium was released. |2026\-06\-26 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|ABR configuration |Added support for the RTM\-ABR protocol type when creating an ABR configuration. |2026\-06\-25 |[Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) |
|Pull stream address |Added support for generating RTM\-ABR addresses. |2026\-06\-25 |* [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses)<br><br>* [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator) |
|Server\-side OpenAPI |Added support for the RTM\-ABR protocol type when creating an ABR configuration. |2026\-06\-25 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Bandwidth limit |Added support for configuring a bandwidth limit and an alert threshold for your domain name for stream pulling. |2026\-06\-08 |[Bandwidth limit](https://docs.byteplus.com/docs/byteplus-media-live/Bandwidth_limit) |
|Concurrent stream limit |Added support for configuring a concurrent stream limit and an alert threshold for your domain name for stream pushing. |2026\-06\-08 |[Concurrent stream limit](https://docs.byteplus.com/docs/byteplus-media-live/Concurrent_stream_limit) |
|Player SDK for Web |Version 2.12.0 was released. |2026\-06\-08 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |
|Player SDK for Android |Version 1.50.300.1 was released. |2026\-06\-01 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Versions 1.50.300\-premium and 1.50.300.3\-premium were released. |2026\-06\-01 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## May 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Interactive live streaming solution |The interactive live streaming solution now only supports pushing streams via the BytePlus RTC SDK. |2026\-05\-27 |* [Interactive live streaming solution overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-interactive-live-streaming-solution-overview)<br><br>* [Implementing interactive live streaming for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-interactive-live-for-android)<br><br>* [Implementing interactive live streaming for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-interactive-live-for-ios) |
|Player SDK for Android |Version 1.50.200.3 was released. |2026\-05\-08 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Version 1.50.200.3\-premium was released. |2026\-05\-08 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## April 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|AI Dubbing |Added support for creating AI Dubbing tasks for live streaming. |2026\-04\-21 |[AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation) |
|Subtitle |* Added support for AI Dubbing mode.<br><br>* Added support for starting subtitle tasks in specific languages by adding parameters to the push stream address. |2026\-04\-21 |[Managing subtitle configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration) |
|Server\-side OpenAPI |* Added AI Dubbing task APIs, including creating, updating, restarting, deleting, querying, and searching tasks.<br><br>* Added an API for getting the AI Dubbing configuration available to the current account.<br><br>* Added AI Dubbing mode support to subtitle configuration APIs, including creating, updating, listing, and querying details of subtitle configurations.<br><br>* Added an API for getting the fonts and languages available to the current account for AI Dubbing mode in subtitle configurations. |2026\-04\-21 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Player SDK for Android |Version 1.50.100.1 was released. |2026\-04\-08 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Version 1.50.100.2\-premium was released. |2026\-04\-08 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## March 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|SDK licenses |* Added support for getting licenses for the Player SDK for Web in the console.<br><br>* A basic license can no longer be upgraded to the premium license upon renewal. |2026\-03\-24 |* [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)<br><br>* [Managing SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses)<br><br>* [SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses) |
|Player SDK for iOS |Version 1.49.300\-premium was released. |2026\-03\-09 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## February 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for Android |Version 1.49.300.4 was released. |2026\-02\-25 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Version 1.49.300.2\-premium was released. |2026\-02\-25 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Transcoding configuration |* Added 4K and 2K quality levels. To configure these levels, contact the BytePlus support team by [creating a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980).<br><br>* The B\-frame setting is no longer supported. B\-frames are now fixed at 0 by default. |2026\-02\-05 |[Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) |
|ABR configuration |Added 4K and 2K quality levels. To configure these levels, contact the BytePlus support team by [creating a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |2026\-02\-05 |[Managing adaptive bitrate configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) |
|Best practice |Added a low\-latency FLV live stream solution for Player SDK for Web. |2026\-02\-03 |[Achieving 2-3s live stream latency with low-latency FLV (Player SDK for Web)](https://docs.byteplus.com/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web) |

## January 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Streams |Supports stopping, disabling, and enabling streams in bulk. |2026\-01\-16 |[Managing streams](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-streams) |
|Player SDK for Android |Version 1.49.100.2 was released. |2026\-01\-09 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for iOS |Version 1.49.100.2\-premium was released. |2026\-01\-09 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Player SDK for Web |Version 2.11.0 was released. |2026\-01\-08 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |

## December 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Recording |Added support for selecting Asia Pacific (Singapore) or Asia Pacific (Johor) as the VOD region. |2025\-12\-22 |[Managing recording configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings) |
|Server\-side OpenAPI |* Added the request parameter `VodRegion` to configure the VOD region.<br><br>* Added the response parameter `VodRegion` to get the VOD region. |2025\-12\-22 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |

## November 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for Web |Version 2.10.3 was released. |2025\-11\-27 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |
|Player SDK for Android |Version 1.48.200.2 was released. |2025\-11\-14 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Web |Version 2.10.2 was released. |2025\-11\-12 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |

## October 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for Android |Version 1.48.100.103 was released. |2025\-10\-28 |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Web |Version 2.10.0 was released. |2025\-10\-21 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |
|Player SDK for Flutter |Version 1.47.300 was released. |2025\-10\-16 |[Player SDK for Flutter release notes](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-release-notes) |
|Player SDK for iOS |Version 1.48.100.4\-premium was released. |2025\-10\-15 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|URL authentication |Added Type A and Type C authentication for domain names for stream pulling, and added support for advanced configurations such as the signature parameter name, timestamp parameter name, and time format. |2025\-10\-14 |[Configuring URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication) |
|Certificates |Optimized the certificate query experience by adding support for multiple search criteria, including domain name, associated domain name, certificate status, and domain status. |2025\-10\-14 |[Managing SSL certificates](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates) |
|Server\-side OpenAPI |Added new authentication types and a parameter for the time format of the timestamp. |2025\-10\-14 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Player SDK for iOS and Android |The Player SDK package editions have changed from **Lite** to **Standard** and from **Interactive** to **Premium**. |2025\-10\-14 |* [SDK introduction](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)<br><br>* [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) |

## September 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Player SDK for iOS |Version 1.47.300\-premium was released. |2025\-10\-10 |[Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|AI LiveInterpret |Added support for the AI LiveInterpret feature, which integrates capabilities such as the Doubao simultaneous interpretation model, multilingual subtitles, digital human lip\-sync, and voice cloning. This enables real\-time conversion of live stream audio into multilingual content. |2025\-09\-18 |[AI Dubbing](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation) |
|Server\-side OpenAPI |* Added support for getting monitoring data, such as the frame rate and bitrate of audio and video, for all or specific origin\-pull streams under a specific domain name for stream pulling within a given time range.<br><br>* Added support for getting the peak count of specific pushed streams, origin\-pull streams, or transcoded streams within a specific time range.<br><br>* Replaced `CreateSnapshotPreset` with [CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) for adding screenshot configurations.<br><br>* Replaced `UpdateSnapshotPreset` with [UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) for updating screenshot configurations.<br><br>* Replaced `ListVhostSnapshotPreset` with [ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) for getting screenshot configuration information. |2025\-09\-15 |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Screenshot configuration |* Added support for JPG image format.<br><br>* Added support for **Overwrite** screenshot type.<br><br>* Deleted the **Callback address for screenshots** field. To configure the screenshot callback address, see [Managing callback configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task). |2025\-09\-15 |[Managing screenshot configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-screenshot-capturing) |
|Player SDK for Web |Version 2.9.2 was released. |2025\-09\-02 |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |

## August 2025

|Feature |Type |Description |Document |
|---|---|---|---|
|Player SDK for Android |Improved and fixed |Version 1.47.300.1 was released. |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Flutter |New |The first official release of BytePlus MediaLive Player SDK for Flutter. |[Player SDK for Flutter release notes](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-release-notes) |
|Player SDK for Android |Updated |Version 1.47.300 was released. |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Android and iOS |Fixed |Version 1.47.200 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Player SDK for Web |Fixed |Version 2.9.1 was released. |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |
|Player SDK for Web |Updated |Version 2.9.0 was released. |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |

## June 2025

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Web |Update |1. Fixed the issue where `userId` was not correctly logged (only affects versions V2.6.1 to V2.7.0). This ensures that log information accurately records the user identifier, facilitating easier issue tracking and debugging.<br><br>2. Fixed an issue where switching resolution or source lines was ineffective when `controls` was set to `false`.<br><br>3. Optimized the playback of RTM streams on certain OPPO mobile devices. This addresses the issue where an error was thrown when playing RTM streams on specific OPPO mobile devices, ensuring a smoother playback experience. |\- |
|Origin pull |New |BytePlus MediaLive console now supports selecting the DASH protocol for third\-party origin pull. |[Managing origin pull configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings) |
|Querying Callback Records |New |The BytePlus MediaLive console now supports querying callback records, allowing you to view and manage historical callback events. |[Querying stream data](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data) |

## May 2025

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Stream Data Query |New |The Stream Data Query feature now includes a new Callback Records module, allowing you to query details of callbacks such as stream start, stream end, recording, and screenshot events. This enhancement improves troubleshooting and data validation efficiency. |[Querying callback records](https://docs.byteplus.com/docs/byteplus-media-live/docs-querying-stream-data#d7ea272c) |

## April 2025

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Server SDK for Node.js |New |The first Server\-side Node.js SDK enables live streaming access and integration for Node.js backends. |[Server SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk) |
|Player SDK for Web |Update |**Documentation Update:**  Added a guide for integrating ABR (Adaptive Bitrate) playback, enabling dynamic quality adjustment based on real\-time network conditions for improved viewing experience. |[Adaptive bitrate streaming](https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr) |

## March 2025

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Web |Update |Introduced RTM playback lag optimization. When the network is unstable, adjusting the buffer latency enhances the viewing experience. |[Best practice](https://docs.byteplus.com/docs/byteplus-media-live/docs-best-practice) |
|Player SDK for Web |New |Version 2.6.1 was released. |[Player SDK for Web: Release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2) |

## January 2025

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Console user guide |Update |* Added support for setting the waiting time for resuming recording after an interruption in MP4 and FLV formats.<br><br>* Changed the value range of the single TS slice duration in HLS format from 5\-30 seconds to 2\-100 seconds. |[Managing recording configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings) |
|OpenAPI |Update |Changed the value range of the request parameter `SliceDuration` from [5,30] to [2,100]. |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Pricing |New |We have introduced new billing items to enhance the functionality of your streaming service. The following features are now available for billing:<br><br><br>1. Subtitles<br><br>2. Stream mixing<br><br>3. VQScore |* [Subtitle](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-subtitle)<br><br>* [Stream mixing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-streammixing)<br><br>* [VQScore](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-vqscore) |
|Player SDK for Android and iOS |New |Version 1.45.100 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## December 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Console user guide |New |You can now configure remote authentication for pull streaming domains on the BytePlus MediaLive console. |[Remote authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/remote-authentication) |
|OpenAPI |New |Added APIs for managing remote authentication configurations. |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|OpenAPI |New |Added an interface to query traffic and bandwidth information for the top N live streams or domains. |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |

## November 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Android |New |Version 1.44.200 was released. |[Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes) |
|Player SDK for Web |New |Version 2.5.1 was released. |[Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2) |
|Console user guide |Update |You can now download log files in batches. |[Querying logs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-logs) |

## September 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|SDK data query |New |You can query and analyze key quality metrics of the client. |[SDK data query](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-clientdata) |
|Adaptive bitrate |Update |You can use adaptive bitrate streaming based on DASH protocol to ensure optimal playback quality based on the viewer's network conditions through the console. |[Managing adaptive bitrate configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) |
|Recording configuration |Update |* Added support for creating recording configurations for transcoded streams.<br><br>* Added support for storing recorded files in BytePlus TOS. |[Managing recording configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-recordings) |
|Screenshot capture configuration |Update |Added support for storing screenshot files in BytePlus TOS. |[Managing screenshot configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-screenshot-capturing) |
|Time shifting configuration |Update |You can now store time\-shifted files in BytePlus TOS. |[Managing time shifting configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-time-shifting) |
|Relay |Update |* Added support for setting the loop playback times for on\-demand videos.<br><br>* Added support for adding watermarks to streamed output videos. |[Configuring a relay task](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay) |
|Player SDK for Web |New |Version 2.5.0 was released. |[Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2) |
|Stream mixing |New |Added APIs for cloud stream mixing tasks. |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |

## August 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Statistics and analysis |New |Added a new batch query API for push stream monitoring data. |[OpenAPI changelog](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1) |
|Relay |Update |You can add a task group in Relay. The group belongs to a project, which allows you to implement sub\-account permission settings based on the project. |[Configuring a relay task](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay) |
|Transcoding configuration |Update |Added advanced parameters to the transcoding configuration. These include options for selecting transcoding trigger criteria and ensuring that transcoded stream parameters do not exceed those of the source stream. |[Managing transcoding configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) |
|HLS Encapsulation |Update |You can insert PDT time tags at specified intervals. |[HLS and LL-HLS](https://docs.byteplus.com/en/docs/byteplus-media-live/hls-and-ll-hsl) |
|Subtitle configuration |New |You can configure automatic speech recognition subtitles for transcoded streams and enable subtitle translation. |[Manage subtitle configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration) |

## July 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Encryption |Update |You can now configure HLS standard encryption live streaming. |* [Managing HLS key acquisition address](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-hls-keyaddress)<br><br>* [Managing encryption configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task) |

## June 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Domain |Update |You can configure the acceleration region for each domain name. |[Adding a domain name](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-domain) |
|SDK management |Update |You can create a web\-type application in the console and obtain its App ID. |[SDK management](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management) |
|Certificates and applications |Update |You can configure projects for certificates and SDK applications. This enables sub\-accounts with project permissions to manage certificates and SDK applications. |* [Managing SSL certificates](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates)<br><br>* [SDK management](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management) |
|Dashboard |Update |You can switch the time zone configuration of the console. |[Interacting with BytePlus MediaLive Dashboard](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-overview) |

## May 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Digital rights management (DRM) |Update |You can use PlayReady for DRM encryption. |[Encrypting your live streams using DRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm) |
|Managing SSL certificates |Updated |Improved the certificate management feature. You can now add certificates by uploading certificate files. |[Managing SSL certificates](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates) |

## April 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Android and iOS |Updated |Updated the demo integration documentation. The push or pull stream address, interactive live streaming room ID, and Token are no longer fixed values and must now be manually configured. |* [Running VeLiveQuickStartDemo for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-android)<br><br>* [Running VeLiveQuickStartDemo for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-running-the-quickstartdemo-for-ios) |
|Player SDK for Android and iOS |Updated |Version 1.41.300 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|HLS encapsulation configuration |New |You can configure the HLS/LL\-HLS segment duration and the number of segments per playlist for streams under the specified domain name. |* [HLS and LL-HLS](https://docs.byteplus.com/en/docs/byteplus-media-live/hls-and-ll-hsl)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|DASH encapsulation configuration |New |You can configure the DASH\-CMAF segment duration and the number of segments per manifest for streams under the specified domain name. |* [DASH and LL-DASH](https://docs.byteplus.com/en/docs/byteplus-media-live/dash-and-ll-dash)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Latency control |New |You can reduce the live streaming latency by configuring server cache for stream pulling over FLV and RTMP. |* [Latency control](https://docs.byteplus.com/en/docs/byteplus-media-live/latency-control)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## March 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Querying stream data |Updated |You can now query ended pull streams for the time, duration and the reason for ending through the console or Open API.<br><br>The values of `errmsg` in the **Stream pushing ends** callback have been updated to communicate the reason more clearly. |* [Querying stream data](https://docs.byteplus.com/en/byteplus-media-live/docs/querying-stream-data)<br><br>* [Callback description](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Offline log format |Updated |The offline log format has been upgraded.<br><br>You may need to update the parsing rules in your log parsing tool accordingly. |* [Log format update](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-offline-log-format-updated)<br><br>* [Querying logs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-logs)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Player SDK for iOS and Android |Updated |Version 1.41.100 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |
|Origin address rewrite |New |You can change the origin address for an on\-demand origin\-pull task through the console or Open API. |* [Origin address rewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-origin-address-rewrite)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Additional HTTP headers in the request |New |You can add additional HTTP headers in the request sent to a third\-party origin server during an origin\-pull task through the console or Open API. |* [HTTP request headers](https://docs.byteplus.com/docs/byteplus-media-live/docs-http-request-headers)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Additional HTTP headers in the response |New |You can add additional HTTP headers in the response sent from an edge server to a client through the console or Open API. |* [HTTP response headers](https://docs.byteplus.com/docs/byteplus-media-live/docs-http-response-headers)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|Adaptive bitrate |New |You can use adaptive bitrate streaming to ensure optimal playback quality based on the viewer's network conditions through the console or Open API. |* [Configuring adaptive bitrate](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)<br><br>* [OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |
|OpenAPI |Updated |New parameters have been added to the response bodies of existing operations. |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## February 07, 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|OpenAPI |New |New endpoints for querying the SSL certificates under your account. |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## January 25, 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Digital rights management (DRM) |New |You can now encrypt your live streams using DRM. |[Encrypting your live streams using DRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm) |
|Geographic restrictions |New |You can now limit requests from specific geographic regions. |[Geographic restrictions](https://docs.byteplus.com/docs/byteplus-media-live/docs-geographic-restrictions) |
|Protocol restrictions |New |You can now limit requests to pull live streams of specific protocols. |[Protocol restrictions](https://docs.byteplus.com/docs/byteplus-media-live/docs-protocol-restrictions) |
|OpenAPI |New |New endpoints for domain access control and DRM\-related features. For details, refer to the OpenAPI changelog. |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## January 17, 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Android and iOS |Updated |Version 1.40.300 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## January 11, 2024

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|UA restrictions |New |You can allow or prevent specific users from accessing your domain name through the value of the User\-Agent (UA) header in the pull\-stream requests. |[UA restrictions](https://docs.byteplus.com/docs/byteplus-media-live/docs-ua-blocklist-and-allowlist) |
|OpenAPI |New |New endpoints for managing UA blocklists and allowlists. For details, refer to the OpenAPI changelog. |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## December 21, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Android and iOS |Updated |Version 1.40.200 was released. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## November 17, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Pricing |Doc update |Additional pricing information has been added for the following:<br><br><br>* Traffic generated within the Chinese mainland<br><br>* [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media) streaming<br><br>* Recording |* [Live-streaming service fees](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-streaming-service-fees)<br><br>* [Recording](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding_2) |
|Pricing |New |* If you choose the monthly billing cycle, you can now use a resource pack to deduct traffic from your monthly bill.<br><br>* Each region is now assigned a deduction factor that is multiplied by the actual traffic when calculating the traffic to deduct from a resource pack. |[Resource packs](https://docs.byteplus.com/docs/byteplus-media-live/docs-resource-packs) |

## November 7, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|BytePlus MediaLive Player SDK |Updated |Version 1.39.300 was released. | |

## October 31, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Rate limit |New |You can now configure the frequency limit for pull\-stream requests associated with a specific domain name. You can use rate limiting to mitigate the risk of Challenge Collapsar (CC) attacks. |[Rate limiting](https://docs.byteplus.com/docs/byteplus-media-live/docs-rate-limiting) |
|Manage domain name |Updated |* You can now manage your resource usage and billing on a per\-project basis by associating your domain name spaces with different projects.<br><br>* You can now associate a domain name space with multiple domain names. |* [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337)<br><br>* [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) |
|SDK management |Updated |You can now purchase a license for the BytePlus MediaLive Player SDKs directly through the console. For pricing details, refer to [SDK licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses). |[SDK management](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management) |
|Origin pull |Updated |You can now create scheduled origin\-pull tasks. The edge servers will continuously pull the content from the origin within a specified time range. |[Configuring an origin-pull task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings) |
|Transcoding |Updated |* OPUS codec is now supported.<br><br>* When configuring a transcoding task, you now have the flexibility to modify the pre\-filled configuration settings after selecting a resolution. |[Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding) |
|OpenAPI |New |New endpoints for managing domain names and value\-added services. For details, refer to the OpenAPI changelog. |[OpenAPI changelog](https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog-1) |

## August 11, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Player SDK for Android and iOS |New |The first official release of BytePlus MediaLive Player SDK for Android and iOS. |* [Player SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)<br><br>* [Player SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes) |

## July 28, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Origin pull |Updated |You can now specify to pull a live stream from an origin server using the HLS streaming protocol. |[Configuring an origin-pull task](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-origin-pull-settings) |
|OpenAPI |New |New endpoints for creating, updating, and querying origin\-pull tasks. |[OpenAPI changelog](https://docs.byteplus.com/en/byteplus-media-live/docs/changelog-1) |

## July 6, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|Callback |New |You can now configure callback notifications through the BytePlus MediaLive console. |[Configuring a callback task](https://docs.byteplus.com/byteplus-media-live/docs/configuring-a-callback-task) |
|Real Time Media |New |You can now use the Real Time Media feature for an optimal viewing experience. Working alongside the BytePlus MediaLive Player SDK, RTM can achieve millisecond latency when streaming to millions of concurrent users. |[Introduction to Real Time Media](https://docs.byteplus.com/byteplus-media-live/docs/introduction-to-real-time-media) |
|Querying stream data |Updated |* Pull stream: you can now query bandwidth, traffic, and the number of online viewers for a specific stream.<br><br>* Push stream: you can now query additional data including the presentation timestamp (PTS) and time intervals between two consecutive frames. |[Querying stream data](https://docs.byteplus.com/en/byteplus-media-live/docs/querying-stream-data) |
|Querying analytic data |Updated |You can now query additional analytic data, including bandwidth, traffic, and the HTTP status codes received. |[Querying analytic data](https://docs.byteplus.com/en/byteplus-media-live/docs/statistical-analysis) |
|Recording |Updated |* You can now store recording files in BytePlus VOD.<br><br>* Two recording options are now available: real\-time recording and recording that automatically resumes after a disconnection.<br><br>* You can query recording files stored in BytePlus VOD. |* [Configuring a recording task](https://docs.byteplus.com/byteplus-media-live/docs/configuring-recordings)<br><br>* [Managing recording files](https://docs.byteplus.com/byteplus-media-live/docs/managing-recordings) |

## February 17, 2023

|**Feature** |**Type** |**Description** |**Document** |
|---|---|---|---|
|SDK management |New |You can now acquire your client SDK licenses and packages through the BytePlus MediaLive console. |[SDK management](https://docs.byteplus.com/byteplus-media-live/docs/sdk-management) |

## November 29, 2022

The first release of BytePlus MediaLive.
