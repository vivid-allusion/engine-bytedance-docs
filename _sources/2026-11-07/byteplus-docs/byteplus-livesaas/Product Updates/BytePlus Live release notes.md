---
title: "BytePlus Live release notes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-byteplus_live_changelog"
---

Find all changes to the console, APIs, and SDKs for BytePlus Live here.

## October 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for iOS |Added support for integrating the SDK using Swift Package Manager (SPM). |2026\-10\-23 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|AI Live |Added support for pushing AI Live streams to Shopee via RTMP. With the Live Connector browser extension, you can also sync viewer comments from a Shopee livestream to your BytePlus AI live room, allowing your AI figure to generate and speak replies based on your configured knowledge base and prompts. |2026\-10\-10 |[Going live on Shopee via RTMP](https://docs.byteplus.com/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp) |
|AI Live |Added support for generating livestream scripts with AI. In the script editor, you can use AI script generation to create text scripts or product scripts from interactive prompts, and then apply the generated content to your live room.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2935c7392c634a4f851c4dc8e5dd754a~tplv-goo7wpa0wc-image.image) |2026\-10\-01 |[Generating livestream scripts](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts) |

## September 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|AI Live |Added support for green screen matting when training AI avatars. Upload a video shot against a green screen and select **Green screen matting** to obtain an avatar with a transparent background. Also added support for live room decoration with static images, GIFs, overlay videos, and cutaway videos. You can change live room decorations by scenario so the visuals switch with different script lines. |2026\-09\-23 |* [Managing the material library](https://docs.byteplus.com/docs/byteplus-livesaas/manage-live-room-visual-materials)<br><br>* [Decorating a live room](https://docs.byteplus.com/docs/byteplus-livesaas/decorating-a-live-room)<br><br>* [Training avatar and voice](https://docs.byteplus.com/docs/byteplus-livesaas/training_digital_human_and_voice) |
|AI Live |Added support for embedding the AI Live console into your own web pages through an iframe. Using STS temporary credentials, you can embed pages such as the AI Live control page, room list, model training, product library, knowledge base, and service center, so your users can access AI Live capabilities without leaving your platform. |2026\-09\-18 |[Using an iframe to embed the AI Live console](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console) |

## August 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|AI Live |Added support for the following features:<br><br><br>* **AI Rewrite**: Once enabled, BytePlus Live uses AI to extend your original script after it has been read and automatically saves the generated content, allowing the AI host to continue with fresh content without repetition.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50421a278e504c74bbe9278872e30b0c~tplv-goo7wpa0wc-image.image)<br><br>* **Audience interaction**: The AI host can proactively respond to audience activities, such as joining the livestream, liking, sharing, and following.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4b36f2893864a29a0ada23a1ee55070~tplv-goo7wpa0wc-image.image)<br><br>* **Pre\-live content check**: Before going live, BytePlus Live provides a **Start Live** setup flow to check your content and ensure it is ready for livestreaming.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c18cb9f094484693b43c0e6359c3f601~tplv-goo7wpa0wc-image.image)<br><br>* **LIVE hours**: You can set a livestream duration, after which the livestream automatically ends. |2026\-08\-28 |[Starting an AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-livestream) |
|Web Viewer SDK |Released version 2.0.31, which updates CSS styles. |2026\-08\-12 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## July 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|AI Live |AI Live enables you to run always\-on, unattended livestreams for your e\-commerce store, so you can keep selling and engaging shoppers 24/7. It uses an AI figure, cloned from a real person, to host the stream, present products from sources like TikTok Shop or Shopify, and answer audience questions in real time. You can now enjoy a **free trial**. |2026\-07\-31 |[AI Live overview](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-overview) |
|Product cards |Added support for the multi\-environment direct URL feature. You can now configure up to 5 environments, each identified by a User Agent, and set a separate direct URL for each environment on every product card.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a82ea836309945ee9a64e8b27890db2a~tplv-goo7wpa0wc-image.image) |2026\-07\-23 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Live templates |Added support for configuring product card multi\-UA, Like, and Popular display in live templates. |2026\-07\-23 |[Creating and using live templates](https://docs.byteplus.com/docs/byteplus-livesaas/live-templates) |
|Server\-side OpenAPI |Added the `UAInfo` and `DirectUrls` parameters to [GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi) and [UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi) to support the multi\-environment direct URL feature for product cards. |2026\-07\-23 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Released version 2.0.30, which adds support for the product card multi\-environment direct URL feature and for configuring Like and Popular display in live templates. Starting from this version, the resource domain has been changed to `https://res.gcloudcache.com/bp-fe`. |2026\-07\-23 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|API Endpoint |Updated the recommended BytePlus Live API endpoint to `https://livesaas.byteplusapi.com`. The original endpoint, `https://open.byteplusapi.com`, remains available. |2026\-07\-10 |* [API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes)<br><br>* [Announcement on the BytePlus Live API Endpoint Update](https://docs.byteplus.com/docs/byteplus-livesaas/endpoint-update) |
|AI Livestream Analysis |Added support for analyzing livestream videos with AI\-powered segmentation, transcripts, analysis tags, and segment\-level optimization suggestions. |2026\-07\-03 |[AI Live analysis](https://docs.byteplus.com/docs/byteplus-livesaas/AI-Live-analysis) |

## April 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for iOS |Published version 1.66.1. |2026\-04\-28 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.66.3. |2026\-04\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|BytePlus Live app |Improved the Account Login page. |2026\-04\-16 |* [Live streaming from an iOS phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone)<br><br>* [Live streaming from an Android phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone) |
|Server\-side OpenAPI |Added support for managing some interaction tools. |2026\-04\-01 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |

## February 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Web Viewer SDK |Published version 2.0.27\-beta.4. |2026\-02\-02 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## January 2026

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Server\-side OpenAPI |Added support for showing the start time and the end time of a live stream corresponding to the playback video in [ActivityAutoReplayCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityautoreplaycallback). |2026\-01\-27 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Server\-side OpenAPI |Deprecated the [ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) which forbids streams of specific live sources in a live room. |2026\-01\-14 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 2.0.27\-beta.2 and 2.0.27\-beta.3. |2026\-01\-12 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Web Viewer SDK |Published version 2.0.27. |2026\-01\-06 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## December 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Web Viewer SDK |Published version 2.0.25, which adds some parameters and events to help you implement your own logic for popularity display and products. |2025\-12\-10 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## November 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for iOS |Published version 1.65.2. |2025\-11\-25 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.65.2. |2025\-11\-25 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.65.1. |2025\-11\-17 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.65.1. |2025\-11\-17 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Prize library |Added the **Prize library** page for prize management.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39c6f735aa444d16a949a6ee7d9cbd8d~tplv-goo7wpa0wc-image.image) |2025\-11\-12 |[Managing prizes in the prize library](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-prizes-in-prize-library) |
|Roles |* Added **Media library** \> **Prize library** \> **View only** or **Edit** permissions for the role.<br><br>* Added the user range that a role can access or manage prizes. |2025\-11\-12 |[Adding IAM users, organizations, or roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles) |
|Multi\-language |Support for more language types for the viewing page:<br><br><br>* Tagalog<br><br>* Khmer<br><br>* Lao<br><br>* Burmese<br><br>* Malay<br><br>* Hindi<br><br>* French<br><br>* German<br><br>* Italian |2025\-11\-12 |* [Configuring multiple languages for the viewing page](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-multiple-languages-for-the-viewing-page)<br><br>* [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area) |
|Gift rewards |Updated the maximum character limit for gift names in each language to 50. |2025\-11\-12 |[Rewarding hosts with gifts](https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts) |
|Playbacks |Updated the maximum number of playback videos that can be released to 200. |2025\-11\-12 |[Managing playbacks](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploading-a-video-on-demand-vod) |
|Server\-side OpenAPI |* Support for more language types for live rooms.<br><br>* Added support for managing prizes under your account, including adding, updating, deleting, and retrieving prize information. |2025\-11\-12 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 2.0.24, which adds support for more language types. |2025\-11\-12 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.65.0, which adds support for more language types. |2025\-11\-12 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for Flutter |Published version 1.65.0\-1, which adds support for displaying Flutter widgets. |2025\-11\-12 |[Viewer SDK for Flutter release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-release-notes) |
|Live Streaming SDK for Android |Published version 1.65.0. |2025\-11\-12 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.65.0, which adds support for configuring the floating window image view, setting the preferred language, and adding more language types. |2025\-11\-12 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.65.0. |2025\-11\-12 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |

## October 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for Android |Published version 1.64.1. |2025\-10\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.23, which adds support for customizing product information and the playback list on the viewing page. |2025\-10\-16 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Demo |Added support for actively enabling the PiP feature, updating the URLs in PiP, muting and unmuting the live video, and adjusting the PiP window size. |2025\-10\-16 |[Embedding the live room H5 page into your mobile React Native app](https://docs.byteplus.com/docs/byteplus-livesaas/react-native-demo) |

## September 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for iOS |Published version 1.64.0, which supports log reporting for playback. |2025\-09\-25 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.64.0, which supports log reporting for publishing. |2025\-09\-25 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.64.0, which adapts to the Android 16 KB feature and supports log reporting for playback. |2025\-09\-25 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.64.0, which is compatible with BytePlus Effects SDK v4.7.2, adapts to the Android 16 KB feature, and supports log reporting for publishing. |2025\-09\-25 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.22. |2025\-09\-18 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for iOS |Published version 1.63.0, which optimizes the type definition of information that prize winners must enter. |2025\-09\-09 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.63.0. |2025\-09\-09 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.63.0. |2025\-09\-09 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.63.0. |2025\-09\-09 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.21. |2025\-09\-05 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## August 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Quick start |Added a 3\-step quick\-start guide to help new users create and start a livestream. |2025\-08\-28 |[Starting your first live stream](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream) |
|Live template |Added 3 system live templates, each of which contains typical configurations for different scenarios, including E\-commerce, Live marketing, and Online education. |2025\-08\-28 |[Creating and using live templates](https://docs.byteplus.com/docs/byteplus-livesaas/live-templates) |
|Web Viewer SDK |Published version 2.0.20, which added some events to help you implement your own logic for gifts. |2025\-08\-28 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for iOS |Published version 1.62.1, which optimizes the product card click callback logic. |2025\-08\-26 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.62.1. |2025\-08\-26 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Product card |The character limit for product names and descriptions in product cards is increased to 255 per language. |2025\-08\-12 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Server\-side OpenAPI |The character limit for `Title` and `Remark` in product cards is increased to 3315. |2025\-08\-12 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for Android |Published version 1.62.0. |2025\-08\-12 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.62.0, which increases the character limit for product names and descriptions in product cards to 255 per language. |2025\-08\-12 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.62.0. |2025\-08\-12 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.62.0, which increases the character limit for product names and descriptions in product cards to 255 per language. |2025\-08\-12 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 2.0.19, which adds the `shareUrl` parameter to support custom shared URLs for the live room. |2025\-08\-12 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|BytePlus Live app |Optimized the user experience of the product card feature. |2025\-08\-12 |* [Live streaming from an iOS phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone)<br><br>* [Live streaming from an Android phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone) |

## July 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for Android |Published version 1.61.4. |2025\-07\-30 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.61.4. |2025\-07\-30 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.61.3, which includes support for customizing properties such as line spacing, corner radius, and text color for the pinned comment and comments. |2025\-07\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.61.3. |2025\-07\-28 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.61.2, which includes support for customizing properties such as line spacing, corner radius, and text color for the pinned comment and comments. |2025\-07\-28 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.61.2. |2025\-07\-28 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Billing |Support for subscribing to the feature version and resource packages on the console. |2025\-07\-17 |[Subscription method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods#48f4bdcd) |
|Server\-side OpenAPI |Support for getting live rooms created by a specific account, the URL of the live room's cover image in portrait mode, and the account used to create the live room. |2025\-07\-17 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|iframe |Support for using an iframe to embed the console. |2025\-07\-15 |[Using an iframe to embed the console](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-console) |
|Media library |* Support for storing videos under specific categories in the video library.<br><br>* Support for data isolation of videos and cloud clip projects uploaded or created by different IAM users. |2025\-07\-15 |* [Managing videos in the video library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-videos-in-the-video-library)<br><br>* [Managing videos in temporary storage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-videos-in-the-media-library)<br><br>* [Managing playbacks](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploading-a-video-on-demand-vod)<br><br>* [Adding IAM users, organizations, or roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles) |
|Server\-side OpenAPI |* Support for getting the STS signature for a specific account in BytePlus Live, and then you can use an iframe to embed functional modules of the BytePlus Live console into your own page.<br><br>* Support for getting information of videos in the video library or temporary storage under the media library, including the video ID and name.<br><br>* Support for transferring videos from temporary storage to a specific category in the video library for permanent storage.<br><br>* Support for getting information about the default category or a specific category and their subcategories under your account. |2025\-07\-15 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for Android |Published version 1.60.0, which optimizes the UI style of the real\-time lucky draw feature on the viewing page. |2025\-07\-15 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.60.0. |2025\-07\-15 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.60.0, including optimizations to the UI style of the real\-time lucky draw feature on the viewing page. |2025\-07\-15 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.60.0. |2025\-07\-15 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 2.0.17, which added some parameters and events to help you implement your own logic for gifts and products. |2025\-07\-15 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Demo |Simplified the development process by automatically implementing picture\-in\-picture (PiP), autoplay, and other features in your mobile Native and React Native apps, without the need to manually trigger Web events. |2025\-07\-01 |* [Embedding the live room H5 page into your mobile React Native app](https://docs.byteplus.com/docs/byteplus-livesaas/react-native-demo)<br><br>* [Embedding the live room H5 page into your mobile Native app](https://docs.byteplus.com/docs/byteplus-livesaas/native-app-demo) |
|Web Viewer SDK |Published version 2.0.16. |2025\-07\-01 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.59.0. |2025\-07\-01 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.59.0. |2025\-07\-01 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.59.0. |2025\-07\-01 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.59.0. |2025\-07\-01 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |

## June 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for Flutter |Published version 1.58.0\-1, which removed some dependencies for iOS, added support for configuring whether to enable the autoplay feature, and added support for the picture\-in\-picture (PiP) feature. |2025\-06\-23 |[Viewer SDK for Flutter release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-release-notes) |
|Demos of Web Viewer SDK |Added demos for PCs. When viewers open the web page, the first player in the video list automatically plays the video. When they hover over any other player, that player starts playing the video automatically. After viewers stop hovering over all players, the last hovered player’s video continues playing. |2025\-06\-16 |[Autoplay demos of Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos) |
|Viewer SDK for Android |Published version 1.58.0 to support setting whether the PiP window pauses playing the video when the screen is locked. |2025\-06\-04 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.58.0, which improves some Thai UI text. |2025\-06\-04 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.58.0. |2025\-06\-04 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.58.0, which improves some Thai UI text. |2025\-06\-04 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |

## May 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Live Streaming SDK for iOS |Published version 1.57.0, which improves SDK log reporting to enhance troubleshooting. |2025\-05\-20 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.57.0, which improves SDK log reporting to enhance troubleshooting. |2025\-05\-20 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.57.0, which improves SDK log reporting to enhance troubleshooting. |2025\-05\-20 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.57.1, which improves SDK log reporting to enhance troubleshooting. |2025\-05\-20 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.15, which includes support for customizing the error page displayed when the total peak concurrent users (PCU) of all your live rooms with the status of **Live** under your account exceeds the concurrency upper limit. |2025\-05\-15 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|BytePlus Live app |* Support for switching the app language to the following:<br><br>   * Simplified Chinese<br><br>   * English<br><br>   * Japanese<br><br>   * Traditional Chinese<br><br>   * Korean<br><br>   * Thai<br><br>   * Vietnamese<br><br>   * Arabic<br><br>   * Turkish<br><br>   * Spanish<br><br>   * Indonesian<br><br>   * Portuguese<br><br>   * Russian<br><br>* With the multiple languages and comment translation features enabled, the host can send comments in multiple languages to improve the accuracy of the host's comments in different languages.<br><br>* With the multiple languages feature enabled, support for setting the following content in multiple languages to display them in the corresponding language on the viewing page.<br><br>   * Live room name<br><br>   * Live room description<br><br>   * Host account name<br><br>   * Product name<br><br>   * Current price<br><br>   * Original price<br><br>   * Product URL |2025\-05\-12 |* [Live streaming from an iOS phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone)<br><br>* [Live streaming from an Android phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone) |
|Live Streaming SDK for iOS |Published version 1.56.1. |2025\-05\-06 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.56.1. |2025\-05\-06 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |

## April 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Multi\-platform streaming |Prerecorded videos do not support the multi\-platform streaming feature. |2025\-04\-29 |* [Synchronizing a live stream from BytePlus Live to third-party platforms](https://docs.byteplus.com/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms)<br><br>* [Starting prerecorded videos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-the-carousel) |
|Live Streaming SDK for iOS |Published version 1.56.0, including support for setting the SDK language type and customizing the text displayed in the SDK. |2025\-04\-29 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.56.0, including changes to the initialization method. |2025\-04\-29 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.56.0, including support for setting the SDK language type and customizing the text displayed in the SDK. |2025\-04\-29 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.56.0. |2025\-04\-29 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.55.1. |2025\-04\-16 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.55.1. |2025\-04\-16 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.55.2. |2025\-04\-15 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.55.2, which includes support for kicking viewers out of the live room and banning viewers' IP addresses. |2025\-04\-15 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.55.0. |2025\-04\-15 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.55.0, which includes support for kicking viewers out of the live room and banning viewers' IP addresses. |2025\-04\-15 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.54.2.<br><br>> **注意**<br><br><br>> The Live Streaming SDK for Android versions 1.49.0 \- 1.54.1 have issues with log event reporting. To avoid affecting the troubleshooting of online issues, please upgrade these versions to 1.54.2.<br> |2025\-04\-07 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.54.2.<br><br>> **注意**<br><br><br>> The Viewer SDK for Android versions 1.49.0 \- 1.54.1 have issues with log event reporting. To avoid affecting the troubleshooting of online issues, please upgrade these versions to 1.54.2.<br> |2025\-04\-07 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.54.1. |2025\-04\-03 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.54.1. |2025\-04\-03 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.54.0, which modifies the SDK version suffix when importing the Live Streaming SDK. |2025\-04\-01 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.54.0, which modifies the SDK version suffix when importing the Viewer SDK and includes support for setting the maximum number of characters allowed in the comment text box. |2025\-04\-01 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.54.0. |2025\-04\-01 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.54.0, which includes support for setting the maximum number of characters allowed in the comment text box and setting the color of the text entered in the comment text box. |2025\-04\-01 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |

## March 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Demos of Web Viewer SDK |Added a demo in the scenario where you swipe left and right on the phone to automatically play the video when its player is fully displayed. |2025\-03\-28 |[Autoplay demos of Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos) |
|Web Viewer SDK |Published version 2.0.13, which includes support for setting whether to disable the comment text box, specifying the placeholder text for the disabled comment text box, and customizing the style of the disabled comment text box. |2025\-03\-19 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Live Streaming SDK for Android |Published version 1.53.0. |2025\-03\-18 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.53.0, which includes support for customizing the comment text box and the style of the comment area. |2025\-03\-18 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.53.0. |2025\-03\-18 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.53.0, which includes support for customizing the comment text box and the style of the comment area. |2025\-03\-18 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.52.1, which includes support for following the host, as well as additional language support for Korean, Thai, Vietnamese, Arabic, Turkish, Spanish, Indonesian, Portuguese, and Russian. |2025\-03\-04 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.52.0. |2025\-03\-04 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.52.0, which includes support for following the host, as well as additional language support for Korean, Thai, Vietnamese, Arabic, Turkish, Spanish, Indonesian, Portuguese, and Russian. |2025\-03\-04 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |

## February 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|BytePlus Live app |Added support for synchronizing comment deletions across the console and other pages. |2025\-02\-26 |* [Live streaming from an iOS phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone)<br><br>* [Live streaming from an Android phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone) |
|Server\-side OpenAPI |Support for sorting live rooms based on specific rules and order, and filtering live rooms based on category tag values. |2025\-02\-25 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Live Streaming SDK for Android |Published version 1.51.1 to support synchronizing comment deletions across the console and other pages. |2025\-02\-24 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.51.1. |2025\-02\-24 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.51.1 to support synchronizing comment deletions across the console and other pages. |2025\-02\-24 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.51.1. |2025\-02\-24 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Server\-side OpenAPI |* Support for pinning a product to the top of the menu and displaying it in a floating window on the viewing page, or restoring the product to its original position under the menu and removing it from the floating window display on the viewing page.<br><br>* Added the callback `ActivityExplainProductCallBack`, which is triggered when a product in your live room is in any of the following situations:<br><br>   * Pinned to the top of the menu and displayed in a floating window on the viewing page.<br><br>   * Restored to its original position under the menu and no longer displayed in a floating window on the viewing page. |2025\-02\-20 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for Android |Published version 1.51.0, which includes support for setting whether to display the strikethrough on the list price. |2025\-02\-18 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.51.0. |2025\-02\-18 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.51.0, which includes support for setting whether to display the strikethrough on the list price. |2025\-02\-18 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |

## January 2025

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Free trial version |Changed the free trial period from 14 days to 1 month and the watch time from 120 minutes to 3000 minutes. |2025\-01\-24 |* [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods)<br><br>* [Starting your first live stream](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream) |
|BytePlus Live app |* Optimized the login page of the app.<br><br>* Fixed some issues. |2025\-01\-23 |* [Live streaming from an iOS phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone)<br><br>* [Live streaming from an Android phone](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone) |
|Live Streaming SDK for Android |Published version 1.50.0. |2025\-01\-21 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.50.0 to support setting the font size and color of the popularity tag text. |2025\-01\-21 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.50.0. |2025\-01\-21 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.50.0, which includes support for configuring the popularity icon, and the font, font size, and color of the popularity tag text. |2025\-01\-21 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Server\-side OpenAPI |Support for filtering host accounts based on the external platform ID. |2025\-01\-16 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Live Streaming SDK for Android |Published version 1.49.0, which includes modifications to the parameters of the method for joining the live room. |2025\-01\-08 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.49.0. |2025\-01\-08 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.49.0, which includes changes to both the URL for importing the SDK and the BPLive dependency to add when integrating the SDK. |2025\-01\-08 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.49.0, which includes changes to both the URL for importing the SDK and the BPLive dependency to add when integrating the SDK. |2025\-01\-08 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |

## December 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Service activation |Optimized the process for activating the BytePlus Live service. |2024\-12\-24 |[Step 1: Activate the BytePlus Live service](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream) |
|Menu for product cards |If an error message (the value of the `Message` parameter in your in\-house API) is returned after BytePlus Live calls your in\-house API, the error message will be displayed on the app integrated with the Live Streaming SDK for iOS or Android. |2024\-12\-24 |[Response parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Live Streaming SDK for Android |Published version 1.48.0. |2024\-12\-24 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.48.0. |2024\-12\-24 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS |Published version 1.48.0. |2024\-12\-24 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.48.0. |2024\-12\-24 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.47.3, which includes support for displaying the custom floating view component in the upper\-right corner of the live room. |2024\-12\-10 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.47.3, which includes support for displaying a custom floating view in the upper\-right corner of the live room. |2024\-12\-10 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.47.3. |2024\-12\-10 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 2.0.11, which includes an improvement in emoji display speed. |2024\-12\-10 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Menu for product cards |Updated the feature of the in\-house product library.<br><br><br>* To prevent the issue where no products are returned due to the number of products in your system exceeding the specified upper limit, you can contact BytePlus Live technical support to add your BytePlus account to the allowlist. Then, you can return filtered products based on the new parameter `FilterName` in your in\-house API. For more information, see [Process](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#32f5a471).<br><br>* If an error message (the value of the `Message` parameter in your in\-house API) is returned after BytePlus Live calls your in\-house API, the error message will be displayed on the console. For more information, see [Response parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream). |2024\-12\-05 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Demo of Web Viewer SDK |Improved the auto\-play demo to support loading live rooms corresponding to category tag values when viewers tap a tab on the viewing page. You can implement this by completing the following steps:<br><br><br>1. Add category tag values to live rooms on the console.<br><br>2. Call `ListActivityFeedInfosAPI`. You can now get the list of category tags in each live room by calling this API.<br><br>3. When viewers tap a tab on the viewing page, call your in\-house API with the `ActivityTag` value set to the category tag value corresponding to the tab. |2024\-12\-05 |* [Classifying live rooms](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos)<br><br>* [ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |
|iframe |* Added parameters to customize the embedded page.<br><br>* Added events. You can perform your own subsequent actions after detecting a specific event. |2024\-12\-05 |* [Using an iframe to embed the viewing page](https://docs.byteplus.com/docs/byteplus-livesaas/docs-embedding-a-viewing-page-with-iframe)<br><br>* [Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-parameters)<br><br>* [Events](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events)<br><br>* [Type definitions](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions) |
|Viewer SDK for iOS |Published version 1.47.2 to support using the static library version of TTSDK. |2024\-12\-03 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.47.2 to support using the static library version of TTSDK. |2024\-12\-03 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |

## November 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for Flutter |Published the first version of the Viewer SDK for Flutter. |2024\-11\-29 |* [Integrating the Viewer SDK for Flutter](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-flutter)<br><br>* [Feature implementation](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation)<br><br>* [Type definitions](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions) |
|Viewer SDK for Android |Published version 1.47.2, which includes support for setting whether the floating ad displays a white border and background. |2024\-11\-26 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.47.1. |2024\-11\-26 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.47.1. |2024\-11\-26 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.47.1. |2024\-11\-26 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Server\-side OpenAPI |Support for getting the product library information of one or more live rooms at a time. |2024\-11\-21 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Server\-side OpenAPI |* Support for setting the rules and order for sorting the returned live rooms.<br><br>* Support for adding a host account, updating the information of an existing host account, deleting a host account, and getting information of host accounts under your account.<br><br>* Support for updating the host account associated with a live room and configuring whether to enable the account settings feature in the live room.<br><br>* When getting information of the host account associated with a specific live room, added a response parameter to indicate whether viewers are allowed to follow the host on the viewing page. |2024\-11\-07 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Live room sorting |The console now supports the following rules to sort live rooms:<br><br><br>* Creation time ascending<br><br>* Creation time descending<br><br>* Start time ascending<br><br>* Start time descending<br><br>* Live first<br><br>* Over first<br><br><br>The default order is to sort by live room status in ascending order (Live, Preview, Playback, Over) first, and then to sort by start time in descending order within each status.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be866e8d50ae44b08f6d26ffd022b991~tplv-goo7wpa0wc-image.image) |2024\-11\-07 |\- |
|Viewer SDK for Android |Published version 1.46.3 to support setting whether to display a gradient overlay at the top of the live room in portrait mode. If your video background is white, displaying the gradient overlay can make the white text at the top of the live room more visible. |2024\-11\-07 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## October 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for Android |Published version 1.46.2, now compatible with Android 15. |2024\-10\-31 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.46.2, now compatible with Android 15. |2024\-10\-31 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.46.1, now compatible with iOS 18. |2024\-10\-31 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.46.1, now compatible with iOS 18. |2024\-10\-31 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.46.1. |2024\-10\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.46.1. |2024\-10\-28 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.46.0, including the following new features:<br><br><br>* Added support for customizing the Now Playing information.<br><br>* Added support for setting whether to respond to user actions in the Now Playing information section.<br><br><br>The Now Playing information section for media that your app plays is as follows.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/431054e406a74ac2bbe857ece5b7af0a~tplv-goo7wpa0wc-image.image) |2024\-10\-24 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.46.0. |2024\-10\-24 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.46.0. |2024\-10\-24 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Demo of Web Viewer SDK |Improved the demo, including:<br><br><br>* Added support for loading specific live rooms when viewers tap a tab on the viewing page.<br><br>* Added the request parameter `ActivityTag` in the in\-house API to load specific live rooms when viewers tap a tab on the viewing page.<br><br>* Added support for customizing whether to hide all the tabs on the viewing page and display all the live rooms in the list.<br><br>* Added support for playing the video in picture\-in\-picture mode in your app when viewers return to the live room list from the video detail page.<br><br>* Decreased the blank screen duration when navigating from the live room list to the video detail page. |2024\-10\-21 |[Autoplay demos of Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos) |
|Multiple languages on the viewing page |Added support for the following languages on the viewing page, as well as comment translations between all languages supported on the viewing page.<br><br><br>* Thai<br><br>* Vietnamese<br><br>* Arabic<br><br>* Turkish<br><br>* Spanish<br><br>* Indonesian<br><br>* Portuguese<br><br>* Russian |2024\-10\-15 |* [Configuring multiple languages for the viewing page](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-multiple-languages-for-the-viewing-page)<br><br>* [Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream)<br><br>* [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area) |
|Web Viewer SDK |Published version 2.0.6, including the following new features:<br><br><br>* Added support for the following languages on the viewing page:<br><br>   * Thai<br><br>   * Vietnamese<br><br>   * Arabic<br><br>   * Turkish<br><br>   * Spanish<br><br>   * Indonesian<br><br>   * Portuguese<br><br>   * Russian<br><br>* Added support for configuring the default language for the viewing page. The page will be set to the configured default language when viewers join the live room, regardless of their browsers' default language on PCs or their system language on mobile devices.<br><br>* Added methods to get the languages supported by the viewing page and to switch to the specified language if you have your own button for switching languages on the viewing page. |2024\-10\-15 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.45.0, which includes improvements to the UI style of a live room in portrait mode. |2024\-10\-15 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.45.0, which includes improvements to the UI style of a live room in portrait mode. |2024\-10\-15 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.45.0. With the live stream start time feature enabled on the BytePlus Live console or by calling a server\-side API, the host can only start a live stream after the specified start time. |2024\-10\-15 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.45.0. With the live stream start time feature enabled on the BytePlus Live console or by calling a server\-side API, the host can only start a live stream after the specified start time. |2024\-10\-15 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Starting a live stream |Added the start time switch. With the switch turned on, you can only start a live stream after the specified start time. |2024\-10\-10 |[Starting a live stream only after a specific time](https://docs.byteplus.com/docs/byteplus-livesaas/starting-a-live-stream-only-after-a-specific-time) |
|Live streaming from your web browser |Support for configuring the interaction tools that the host can manage on the live streaming page. |2024\-10\-10 |[Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser) |
|Server\-side OpenAPI |* Support for configuring whether to enable the live stream start time feature. Once enabled, you can only start a live stream after the specified start time.<br><br>* Support for configuring whether to allow the host to manage only the specified interaction tools on the live streaming page in a web browser.<br><br>* Support for configuring which interaction tools the host can manage on the live streaming page in a web browser.<br><br>* Support for getting all the above\-mentioned configurations.<br><br>* Added the error code `200027`. |2024\-10\-10 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |

## September 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Menu for product cards |Support for not displaying specific products in Shopify product library. |2024\-09\-26 |[Not displaying specific products in Shopify product library](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream#bd977a0e) |
|Server\-side OpenAPI |Added the [ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) to get the basic information of all the existing live rooms under your BytePlus account and IAM users, including the cover image, virtual popularity, host account, and creation time. |2024\-09\-26 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Demo of Web Viewer SDK |After running the auto\-play demo, you can scroll up and down the viewing page on your phone. When a player is fully displayed, the live video, preview, or playback will automatically play. |2024\-09\-26 |[Autoplay demos of Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos) |
|Check\-in |* Changed the unit of check\-in duration from minutes to seconds.<br><br>* Added support for sending a check\-in at a scheduled time.<br><br>* Support for kicking out viewers who fail to check in on time. |2024\-09\-12 |[Sending a check-in](https://docs.byteplus.com/docs/byteplus-livesaas/sending-a-check-in) |
|Web Viewer SDK |Published version 2.0.5 to optimize the check\-in feature, including changing the unit of check\-in duration from minutes to seconds and kicking out viewers who fail to check in on time. |2024\-09\-12 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.44.0 to support the check\-in feature. |2024\-09\-12 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.44.0, including support for the check\-in feature. |2024\-09\-12 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.44.0. |2024\-09\-12 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 2.0.4. |2024\-09\-05 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for iOS |Published version 1.43.3. |2024\-09\-04 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.43.3. |2024\-09\-04 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.43.4. |2024\-09\-04 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## August 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Multi\-platform streaming |[Document update] Added the section on how to synchronize a live stream to Instagram. |2024\-08\-28 |[Instagram](https://docs.byteplus.com/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms) |
|Viewer SDK for Android |Published version 1.43.3. |2024\-08\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.3 to support customizing the style and background color of icons in live rooms in portrait mode. |2024\-08\-23 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for iOS |Published version 1.43.2 to add a property for configuring whether to display the button for closing the live room during screen clearing. |2024\-08\-22 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.43.2. |2024\-08\-22 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.43.2 to add a method for configuring whether to display the button for closing the live room during screen clearing. |2024\-08\-22 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.43.1. |2024\-08\-20 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Menu for product cards |* Support for managing product libraries and adding products from product libraries.<br><br>* Added the shopping cart icon on mobile devices in landscape mode. |2024\-08\-15 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Server\-side OpenAPI |Added and updated some OpenAPIs. |2024\-08\-15 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for iOS |Published version 1.43.0, including support for displaying the shopping cart icon in landscape mode. |2024\-08\-15 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.43.0, including support for adding products from product libraries and customizing beauty AR effects, filters, and stickers. |2024\-08\-15 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.43.0, including support for displaying the shopping cart icon in landscape mode. |2024\-08\-15 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.43.0, including support for adding products from product libraries and customizing beauty AR effects, filters, and stickers. |2024\-08\-15 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.2 to support displaying the shopping cart icon on mobile devices in landscape mode. |2024\-08\-15 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for iOS |Published version 1.42.1. |2024\-08\-06 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.42.1. |2024\-08\-06 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.42.1. |2024\-08\-06 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Co\-host |* Optimized the UI.<br><br>* Changed the default view from gallery view to presenter view. |2024\-08\-06 |[Starting a co-host with guests](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-video-chat) |
|Viewer SDK for iOS |Published version 1.42.0. |2024\-08\-01 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.42.0. |2024\-08\-01 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.42.0. |2024\-08\-01 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## July 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|BytePlus Live console |Optimized the UI of the menu for chat interaction, the **Security control** page, and the **Live control** page. |2024\-07\-23 |* [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area)<br><br>* [Configuring security control](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-security-control)<br><br>* [Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming)<br><br>* [Liking a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-liking-a-live-stream-or-comment)<br><br>* [Muting all the viewers](https://docs.byteplus.com/docs/byteplus-livesaas/docs-muting-viewers)<br><br>* [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address)<br><br>* [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming)<br><br>* [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser) |
|Server\-side OpenAPI |* Added the callback `ActivityClickReservationCallBack`.<br><br>* Added the API `GetActivityReservationAPIV2`. |2024\-07\-23 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for iOS |Published version 1.41.0. |2024\-07\-23 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.41.0. |2024\-07\-23 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.41.0. |2024\-07\-23 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Web Viewer SDK |Published version 2.0.1. |2024\-07\-23 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Web Viewer SDK |Published version 2.0.0. |2024\-07\-09 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## June 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Viewer SDK for iOS |Published version 1.40.1. |2024\-06\-28 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.40.1. |2024\-06\-28 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.40.0, including adding some callbacks, optimizing the UI style, and changing parameters in some methods. |2024\-06\-27 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.40.0, including support for automatically ending the live stream based on the BytePlus Live server\-side configuration. |2024\-06\-27 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Cloud clips |Added support for the cloud clips feature. |2024\-06\-26 |* [Editing a video in cloud clips](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-video-in-cloud-clips)<br><br>* [Editing a live video](https://docs.byteplus.com/docs/byteplus-livesaas/editing-a-live-video) |
|Media library |* Support for uploading multiple videos at a time.<br><br>* Optimized the UI. |2024\-06\-26 |* [Managing videos in the video library](https://docs.byteplus.com/docs/byteplus-livesaas/managing-videos-in-the-video-library)<br><br>* [Managing videos in temporary storage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-videos-in-the-media-library) |
|Viewer SDK for iOS |Published version 1.40.0, including support for displaying the menu for graphics in portrait mode, optimizing the UI style, and adding some properties and methods. |2024\-06\-26 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.40.0, including support for automatically ending the live stream based on the BytePlus Live server\-side configuration. |2024\-06\-26 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Server\-side OpenAPI |Added parameters `EndTime` and `IsAutoEndEnable`. |2024\-06\-25 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Automatically end a live stream |Added support for automatically ending a live stream. |2024\-06\-25 |[Automatically ending a live stream](https://docs.byteplus.com/docs/byteplus-livesaas/automatically-ending-a-live-stream) |
|Web Viewer SDK |Published version 1.3.8, which includes the removal of `byteplus` following `mobile/` or `pc/` from the URL when importing CSS and JS resources. |2024\-06\-25 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.39.3. |2024\-06\-18 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Server\-side OpenAPI |Changed both the maximum value and default value of the `ForbidTime` parameter from 7 × 24 × 60 × 60 to 31 × 24 × 60 × 60. |2024\-06\-12 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for Android |Published version 1.39.2. |2024\-06\-12 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android |Published version 1.39.1, including support for optimizing the SDK package size, configuring whether to display specific buttons, setting the callback for comment area customization, and setting whether to support editing the cover image in landscape mode and the title of the live room. |2024\-06\-11 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.39.1 to add some methods. |2024\-06\-11 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.39.0 to update the BPLive dependencies you must add when integrating the SDK. |2024\-06\-07 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.39.0 to update the BPLive dependencies you must add when integrating the SDK, and support configuring whether to display specific buttons, whether to support editing live room information, and customizing the comment cell. |2024\-06\-07 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Billing |* Added the live concurrent viewers package.<br><br>* Support for viewing ultra\-low latency related resource usage. |2024\-06\-07 |* [Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods)<br><br>* [Viewing resource usage and purchase records](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewing-resource-usage) |
|Ultra\-low latency |Support the ultra\-low latency feature. |2024\-06\-07 |* [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming)<br><br>* [Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming)<br><br>* [Pushing streams (Using OBS as an example)](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pushing-streams)<br><br>* [Viewing data of a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics)<br><br>* [Viewing Live room data](https://docs.byteplus.com/docs/byteplus-livesaas/docs-checking-your-streaming-statistics) |
|Web Viewer SDK |Published version 1.3.3 to support the ultra\-low latency feature. |2024\-06\-07 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Server\-side OpenAPI |Added the callback [ActivityQuestionChatCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityquestionchatcallback) and the following API operations.<br><br><br>* [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi)<br><br>* [GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi)<br><br>* [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi)<br><br>* [ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi) |2024\-06\-06 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 1.3.2. |2024\-06\-06 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## May 2024

|Feature |Description |Release Date |Related Documents |
|---|---|---|---|
|Live streaming from your web browser |Support for configuring whether to display the co\-host feature, viewing page address, or lock preview feature on the live streaming page. |2024\-05\-31 |[Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser) |
|Server\-side OpenAPI |* Added [GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi).<br><br>* Added some request and response parameters. |2024\-05\-31 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Viewer SDK for iOS |Published version 1.35.0 to enhance compatibility. |2024\-05\-30 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.35.0. |2024\-05\-30 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Live streaming from your web browser |* Support for sharing the whiteboard.<br><br>* Support for sharing documents and pictures. |2024\-05\-20 |* [Sharing the whiteboard](https://docs.byteplus.com/docs/byteplus-livesaas/sharing-the-whiteboard)<br><br>* [Sharing documents and pictures](https://docs.byteplus.com/docs/byteplus-livesaas/sharing-documents-and-pictures)<br><br>* [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser) |
|Live streaming from your web browser |* Support for selecting the OBS virtual camera.<br><br>* Added the menu for Q&A. |2024\-05\-11 |[Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser) |
|BytePlus Live console |* Added the following features:<br><br>   * Quiz<br><br>   * Annoucement<br><br>   * Prize library<br><br>   * Channels<br><br>   * Trial watch<br><br>   * Secondary viewing restriction<br><br>   * Viewer list<br><br>   * Menu for embedded link<br><br>   * Allowlist viewing restriction<br><br>   * Host account library<br><br>   * Anonymous comments<br><br>   * Repeated login prevention<br><br>   * Comment report<br><br>* Support for kicking out a viewer and blocking a viewer's IP address.<br><br>* Support for sending interactive content such as questionnaires, check\-ins on the live streaming page in a web browser.<br><br>* Optimized real\-time lucky draws, including features like the ability to configure participation conditions, allowlists, and blocklists, among others.<br><br>* Support for allowing viewers to follow a host account.<br><br>* Support for sending non\-anonymous questionnaires.<br><br>* Support for configuring the number of times to play carousel videos.<br><br>* Support for configuring where the floating product card is displayed on the viewing page for PCs.<br><br>* Support for adding product notes for product cards and pinning a product card to the top of the menu for product cards. |2024\-05\-10 |* [Sending a quiz](https://docs.byteplus.com/docs/byteplus-livesaas/sending-a-quiz)<br><br>* [Sending an announcement](https://docs.byteplus.com/docs/byteplus-livesaas/sending-an-announcement)<br><br>* [Managing the interaction area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area)<br><br>* [Live streaming from your web browser](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser)<br><br>* [Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream)<br><br>* [Managing the chat area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area)<br><br>* [Configuring security control](https://docs.byteplus.com/docs/byteplus-livesaas/configuring-security-control)<br><br>* [Kicking a viewer out or blocking a viewer's IP address](https://docs.byteplus.com/docs/byteplus-livesaas/kicking-a-viewer-out-or-blocking-a-viewer-s-IP-address)<br><br>* [Associating a host account to a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account)<br><br>* [Viewing Live room data](https://docs.byteplus.com/docs/byteplus-livesaas/docs-checking-your-streaming-statistics)<br><br>* [Viewing data of a live room](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics)<br><br>* [Viewing the data dashboard](https://docs.byteplus.com/docs/byteplus-livesaas/viewing-the-data-dashboard)<br><br>* [OAuth 2.0](https://docs.byteplus.com/docs/byteplus-livesaas/docs-oauth-2-0) |
|Server\-side OpenAPI |Added some request and response parameters. |2024\-05\-10 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 1.3.1. |2024\-05\-10 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## April 2024

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Gift rewards |Optimized the gift rewards feature, including:<br><br><br>* Adjusted the default gifts.<br><br>* Improved the gift effects.<br><br>* Viewers can now send gifts when a live room is in the **Live**, **Playback**, or **Over** status, not just during the live broadcast. |2024\-04\-29 |[Rewarding hosts with gifts](https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts) |
|Web Viewer SDK |Published version 1.1.22 to optimize the gift rewards feature, including:<br><br><br>* Adjusted the default gifts.<br><br>* Improved the gift effects.<br><br>* Allows viewers to send gifts when a live room is in the **Live**, **Playback**, or **Over** status, instead of only in the **Live** status. |2024\-04\-29 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.32.0 to add the gift rewards feature. |2024\-04\-29 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS |Published version 1.34.0, including adding the gift rewards feature. |2024\-04\-29 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.34.0. |2024\-04\-29 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewing restriction \> Custom authentication login |Support for adding the `Sign`, `Nickname`, `UserId`, and `Timestamp` parameters to your cookies for the solution used to avoid a second login after a user logs in to your own account system. |2024\-04\-28 |[Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions) |
|Billing |If you want to have more custom features and larger packages except for those listed on the [BytePlus Live console](https://console.byteplus.com/livesaas/product), contact the sales representative for help. |2024\-04\-23 |[Subscription billing method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods) |
|Data dashboard |Support for displaying data in dimensions of provinces and cities in the **User portrait** section of data dashboard. |2024\-04\-22 |[Data dashboard](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics) |
|Menu for interaction tools |Optimized the UI and experience of the menu for interaction tools on the console. |2024\-04\-18 |* [Managing the interaction area](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area)<br><br>* [Sending a vote](https://docs.byteplus.com/docs/byteplus-livesaas/docs-initiating-a-vote)<br><br>* [Sending a check-in](https://docs.byteplus.com/docs/byteplus-livesaas/sending-a-check-in)<br><br>* [Sending a real-time lucky draw](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-real-time-lucky-draw)<br><br>* [Sending a questionnaire](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-questionnaire) |
|Viewer SDK for Android |Published version 1.31.1 to support optimizing the SDK package size. |2024\-04\-15 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS and Live Streaming SDK for iOS |Published version 1.33.0 to support optimizing the SDK package size. |2024\-04\-15 |* [Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes)<br><br>* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 1.1.21. |2024\-04\-09 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## March 2024

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Viewer SDK for Android |Published version 1.30.6. |2024\-03\-28 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Viewer SDK for iOS and Live Streaming SDK for iOS |Published version 1.32.2. |2024\-03\-27 |* [Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes)<br><br>* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.30.5. |2024\-03\-27 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Primary/Backup stream |Support the primary/backup stream feature. |2024\-03\-27 |[Managing live sources](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming) |
|Sensitive words |Support for ignoring spaces and specific special characters in comments and nicknames when matching sensitive words with the **Fuzzy matching** switch turned on. |2024\-03\-14 |[Blocking sensitive words](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-sensitive-words) |
|Carousel |Support for starting or ending the carousel for all the channels at a time. |2024\-03\-14 |[Starting the carousel](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-the-carousel) |
|Product cards |Support for adding multiple product cards at a time, exporting the information of all product cards, and changing the redirect image for all added and to\-be\-added product cards in a menu for product cards. |2024\-03\-14 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Playbacks |Increased the maximum duration for a playback to 12 hours. |2024\-03\-14 |[Why is the playback content incomplete?](https://docs.byteplus.com/docs/byteplus-livesaas/docs-playback-faq#45baa631) |
|Viewer SDK for iOS and Live Streaming SDK for iOS |Published version 1.32.1. |2024\-03\-11 |* [Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes)<br><br>* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.30.4. |2024\-03\-11 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## February 2024

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Product cards |Support for adding the product category to a product card. |2024\-02\-29 |[Managing product cards](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|Server\-side OpenAPI |* Added an API operation to get the list of live room templates under your BytePlus account.<br><br>* Added the parameter `TagName`. |2024\-02\-29 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Live Streaming SDK for iOS |Published version 1.32.0 to support changing the basic information of a live room, managing products, and other features. |2024\-02\-29 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.32.0 to support displaying the live room description in portrait mode. |2024\-02\-29 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for Android |Published version 1.30.0 to support changing the basic information of a live room, managing products, and other features. |2024\-02\-29 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.30.3 to support displaying the live room description in portrait mode. |2024\-02\-29 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## January 2024

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Viewer SDK for iOS |Published version 1.26.0, which includes the following new features, among other improvements:<br><br><br>* Customizing shared address<br><br>* Countdown<br><br>* Booking a live stream<br><br>* Switching between different venues<br><br>* Invitation poster<br><br>* System notifications<br><br>* Welcome message<br><br>* Risk warning<br><br>* Fullscreen watermark<br><br>* Questionnaires<br><br>* Voting<br><br>* Real\-time lucky draws |2024\-01\-24 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Live Streaming SDK for iOS |Published version 1.26.0. |2024\-01\-24 |[Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.30.0, which includes the following new features, among other improvements:<br><br><br>* Customizing shared address<br><br>* Countdown<br><br>* Booking a live stream<br><br>* Switching between different venues<br><br>* Invitation poster<br><br>* System notifications<br><br>* Welcome message<br><br>* Risk warning<br><br>* Fullscreen watermark<br><br>* Questionnaires<br><br>* Voting<br><br>* Real\-time lucky draws |2024\-01\-23 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Server\-side OpenAPI |Added API operations to get the live streaming quality data. |2024\-01\-23 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Player logo |Support displaying the player logo in portrait mode on mobile devices. |2024\-01\-18 |*  |
|Web Viewer SDK |Published version 1.1.14 to support displaying the player logo in portrait mode on mobile devices. |2024\-01\-18 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## December 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Brand account |Support for adding an external platform ID when configuring the brand account information. |2023\-12\-21 |[Adding a brand account](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account) |
|Server\-side OpenAPI |Added API operations to update and get the brand account information in a live room. |2023\-12\-21 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 1.1.13 to support displaying the player logo in landscape mode on mobile devices. |2023\-12\-14 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## November 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Decorating live rooms |Support for configuring the portrait cover in a live room. |2023\-11\-30 |[Decoration material guidelines](https://docs.byteplus.com/docs/byteplus-livesaas/docs-graphics-guide-for-live-streaming) |
|Live room data |Optimized the UI and logic for live room data. |2023\-11\-30 |[Data statistics](https://docs.byteplus.com/en/byteplus-livesaas/docs/data-statistics?version=v1.0#3c85b475) |
|Server\-side OpenAPI |* Added API operations to get live room data under your BytePlus account.<br><br>* Added the parameter `VerticalCoverImageUrl`. |2023\-11\-30 |[API release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web Viewer SDK |Published version 1.1.12 to support displaying different covers in landscape and portrait modes on mobile devices. |2023\-11\-30 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Sensitive words |* Support for blocking phone numbers in Singapore, Japan, Korea, Indonesia, and Thailand.<br><br>* Support for making sensitive words case\-insensitive. |2023\-11\-27 |[Blocking sensitive words](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-sensitive-words) |
|URL blocking |Support for blocking URLs in comments and nicknames. |2023\-11\-27 |[Blocking URLs](https://docs.byteplus.com/docs/byteplus-livesaas/docs-blocking-urls) |
|Portrait mode |Support for synchronizing color configurations on the BytePlus Live console to live rooms in portrait mode. |2023\-11\-16 |[Portrait mode FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/docs-portrait-mode-faqs) |
|Vote |Optimized the voting style on the viewing page. |2023\-11\-16 |[Initiating a vote](https://docs.byteplus.com/docs/byteplus-livesaas/docs-initiating-a-vote) |
|Web Viewer SDK |Published version 1.1.11. |2023\-11\-16 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Viewer SDK for Android |Published version 1.10.9, compatible with Android 14. |2023\-11\-13 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |

## October 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Billing splitting |Support for billing splitting. |2023\-10\-31 |Viewing usage and bills by organization |
|Authorization |Support for managing organizations in the **Authorization** module. |2023\-10\-31 |[Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles) |
|Web Viewer SDK |Published version 1.1.10. |2023\-10\-16 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Web Viewer SDK |Published version 1.1.8. |2023\-10\-10 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |

## September 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Live Streaming SDK for Android |Published version 1.26.0 to support switching between default frame rate and high frame rate modes, and setting the high frame rate mode as the default. |2023\-09\-27 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |

## August 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Web Viewer SDK |Published version 1.1.7. |2023\-08\-24 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|SDK for Go |The first release of the SDK for Go. |2023\-08\-11 |[Server-side SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-server-side_SDK_changelog) |
|Live Streaming SDK for Android and Live Streaming SDK for iOS |Published version 1.25.2 to support deleting all the comments from the live streaming page and the viewing page. |2023\-08\-04 |* [Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes)<br><br>* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |
|Viewer SDK for iOS |Published version 1.25.2. |2023\-08\-04 |[Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Viewer SDK for Android |Published version 1.10.7. |2023\-08\-04 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for Android and Live Streaming SDK for iOS |Published version 1.25.1. |2023\-08\-01 |* [Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes)<br><br>* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes) |

## July 2023

|**Feature** |**Description** |**Release Date** |**Related Documents** |
|---|---|---|---|
|Web Viewer SDK |Published version 1.1.6. |2023\-07\-31 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
|Live Streaming SDK for Android |Published version 1.25.0. |2023\-07\-20 |[Live Streaming SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-android-release-notes) |
|Viewer SDK for Android |Published version 1.10.6. |2023\-07\-20 |[Viewer SDK for Android release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-release-notes) |
|Live Streaming SDK for iOS and Viewer SDK for iOS |Published version 1.25.0. |2023\-07\-20 |* [Live Streaming SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/live-streaming-sdk-for-ios-release-notes)<br><br>* [Viewer SDK for iOS release notes](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-release-notes) |
|Web Viewer SDK |Published version 1.1.5. |2023\-07\-20 |[Web Viewer SDK release notes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog) |
