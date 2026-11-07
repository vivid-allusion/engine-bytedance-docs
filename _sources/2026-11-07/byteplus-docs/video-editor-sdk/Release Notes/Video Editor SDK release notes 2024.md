---
title: "Video Editor SDK release notes 2024"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/release-notes-2024"
---

These are the release notes for Video Editor SDK for 2024.

<span id="795ab653"></span>
## v1.6.0—8 November, 2024


|**Feature** |**Type** |**Description** |**Document link** |
|---|---|---|---|
|Track Editor |New |Now supports different aspect ratios, including Original, 9:16, 3:4, 1:1, 4:3, and 16:9. When the canvas ratio is not adjusted, videos can be exported in their original aspect ratio. |N/A |
|Export with watermark |New |Exports from Magic Template and Highlight Clipping now support watermark applications. |N/A |
|Music looping support |New |If the music duration is longer than the video, the end portion of the music is trimmed to match the video length. If the music duration is shorter than the video, the music loops to align with the video. |N/A |
|Stress Testing |Update |Automatically adds the 'slandar' channel ID during testing. |N/A |
|Slandar Lag Monitoring |Update |Integrated lag monitoring and resolved stuttering issues. |N/A |
|Dynamic Library Management |Update |* Automatic packaging of `ve` dynamic libraries when outputting sample source code via Bits.<br><br>* Integrated pipeline for sample source code to include Cut Same Style functionality.<br><br>* Combined static library and dynamic library project setup.<br><br>* Implemented PK150 package testing support. |N/A |
|Package Optimization |Update |* General solution for size\-sensitive clients who can accept feature trimming.<br><br>* Optimized for clients sensitive to package size; trimmed CV and audio components, reducing package size by approximately 30%. |N/A |
|Sample Code by Request |Update |Bits now supports generating sample code on demand. |N/A |
|Foldable Device Optimization |Update |* Increased slot count for Magic Templates.<br><br>* Resolved incomplete display on Magic Templates page.<br><br>* Fixed text being blocked on the export page.<br><br>* Resolved black screen issue after expanding the fold during export.<br><br>* Prevented duplicate exports triggered when folding/unfolding during export. |N/A |
|High\-resolution GIF Selection |Update |Resolved issues with selecting high\-resolution GIFs in the album. |N/A |
|Configurable Parameters for API |Update |* Supported settings: width, height, and file size.<br><br>* Default demo resolution: up to 1080p or less, with both dimensions under 1920 pixels.<br><br>* File size: capped at 150 MB. |N/A |


<span id="8f7da697"></span>
## v1.5.0—10 September, 2024


|**Feature** |**Type** |**Description** |**Document link** |
|---|---|---|---|
|Highlight clipping |New |The phone's photo album contains numerous videos and pictures, but users often find it difficult to select high\-quality, visually appealing, and joyful highlights from this large collection. With Video Editor SDK, users can now input one or more videos or images, and the tool will automatically analyze content using advanced tag recognition, quality assessment, and aesthetic scoring. It identifies the best clips based on these factors, matches them with optimal templates, and seamlessly generates a final video directly on the device. |* Android: [Managing Android highlight clippings](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-android-highlight-clippings)<br><br>* iOS: [Managing iOS highlight clippings](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-ios-highlight-clippings) |
|Magic Template |Update |* **Standard Integration:**  Introduces a new high\-fidelity UI with customizable skins.<br><br>* **Source Code Integration:**  Allows access to UI source code for custom development and further UI enhancements. |N/A |


<span id="f15c8259"></span>
## v1.4.0—12 August, 2024


|**Feature** |**Type** |**Description** |**Document link** |
|---|---|---|---|
|Supports RN integration |New |Video Editor SDK now supports RN integration for both iOS and Android. Added full support for integrating the video editor into React Native projects, enabling seamless cross\-platform development. |* Android: [Creating React Native projects in Android](https://docs.byteplus.com/docs/video-editor-sdk/140-creating-react-native-projects-in-android)<br><br>* iOS: [Creating React Native projects in iOS](https://docs.byteplus.com/docs/video-editor-sdk/140-creating-react-native-projects-in-ios) |
|Android Encoding and Composition parameters |Update |Updates to the default values within the Android Encoding and Composition parameters. |[Android Encoding and Composition Parameters](https://docs.byteplus.com/docs/video-editor-sdk/140-android-encoding-and-composition-parameters) |
|UI customization color keys for the following:<br><br><br>* Camera module UI<br><br>* Preview Editor feature UI<br><br>* Music library panel |Update |Some changes to the UI customization color keys. |* [Camera module UI](https://docs.byteplus.com/docs/video-editor-sdk/140-camera-module-ui)<br><br>* [Preview Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/140-preview-editor-feature-ui)<br><br>* [Music library panel](https://docs.byteplus.com/docs/video-editor-sdk/140-music-library-panel) |


<span id="edc89365"></span>
## v1.3.0—22 July, 2024


|**Feature** |**Type** |**Description** |**Document link** |
|---|---|---|---|
|Magic Template SDK |New |The Magic Template SDK is a powerful toolkit for developers, enabling seamless creation and management of dynamic templates. This release includes a range of features, enhancements, and bug fixes designed to improve usability and performance. |* Android: [Getting started with Android Magic Template](https://docs.byteplus.com/docs/video-editor-sdk/130-getting-started-with-android-magic-template)<br><br>* iOS: [Getting started with iOS Magic Template](https://docs.byteplus.com/docs/video-editor-sdk/130-getting-started-with-ios-magic-template) |


<span id="6348c1ef"></span>
## v1.2.0—4 July, 2024


|**Feature** |**Type** |**Description** |**Document link** |
|---|---|---|---|
|Video Duet |New |Introducing the new Video Duet feature for seamless collaborative video editing and creative layout options. |* Android: [Video Duet function](https://docs.byteplus.com/docs/video-editor-sdk/120-android-camera-module-configuration-and-features#639b4acc)<br><br>* iOS: [Video duet function](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-camera-module-configuration-and-features#7aaa6f56) |
|Configuring the Video Duet sidebar |New |You can configure the Video Duet sidebar according to your requirements. |[Video Duet sidebar customization](https://docs.byteplus.com/docs/video-editor-sdk/120-camera-module-ui#4b91f73c) |
|Scan QR codes for resource imports |New |To facilitate verification of tools and store materials, enhancing delivery efficiency. |N/A |
|Supports the configuration parameters for the number of stickers and sound effects. |New |Added configuration parameters to set the number of stickers, sound effects, and special effects, allowing for greater customization and control over these elements. |* Android: [Configuring additional editor panel parameters](https://docs.byteplus.com/docs/video-editor-sdk/120-android-editor-module-configuration-and-features#46a73036)<br><br>* iOS: [EOVideoEditorViewControllerConfig](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-editor-module-configuration-and-features#da7ddcda) |
|Updated the resource configuration for Online & On\-Demand Download. |Update |Updated the resource import and configuration for online and on\-demand download. |* Android: [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#cc6a13c5)<br><br>* iOS: [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-resources-import-and-configuration#4b2c7388) |
|Updated the server side configuration for partial built\-in and partial online resource import and configuration. |Update |Updated the iOS server side configuration for partial built\-in and partial online resource import and configuration. |[Server configuration](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-resources-import-and-configuration#c1afc545) |
|Updated the initialization code. |Update |Updated the Android initialization code. |[Initializing the camera module](https://docs.byteplus.com/docs/video-editor-sdk/120-android-camera-module-configuration-and-features#54bd2245) |
|Updated the Swift sample code for iOS. |Update |Updated the full Swift sample code for iOS. |[Using the sample code](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-package-deliverables-list#f897d706) |


<span id="51c3385e"></span>
## v1.1.0—20 May, 2024


|**Version** |**Release Date** |**Type** |**Update details** |
|---|---|---|---|
|V1.1.0 |2024\-05\-20 |N/A |* Support basic photo camera and preview editing<br><br>* Support using third\-party and self\-created info stickers. For more details, refer to [Third-party stickers resource import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-third-party-stickers-resource_1_1_0).<br><br>* Add flutter integration sample code (for bridging). For more details, refer to the following:<br><br>   * **Android**: [Integrating VE SDK for Android using Flutter](https://docs.byteplus.com/docs/video-editor-sdk/docs-integrating-ve-sdk-using-flutter_1_1_0).<br><br>   * **iOS**: [Creating iOS flutter projects](https://docs.byteplus.com/docs/video-editor-sdk/docs-creating-ios-flutter-projects_1_1_0).<br><br>* Android<br><br>   * Support obtaining export information via `activity result`.<br><br>   * Asset loading optimization.<br><br>* iOS<br><br>   * Support `navigation push`.<br><br>   * Support compilation on ARM64 simulators (SDK features cannot run on simulators, only compilation is supported). |


<span id="6ed6148a"></span>
## v1.0.0—22 Mar, 2024


|**Version** |**Release Date** |**Type** |**Update details** |
|---|---|---|---|
|V 1.0.0 |2024\-03\-22 |N/A |This is the first version of this document and product. |
