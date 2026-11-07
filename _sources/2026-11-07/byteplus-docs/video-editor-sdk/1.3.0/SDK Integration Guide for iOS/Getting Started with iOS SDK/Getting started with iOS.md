---
title: "Getting started with iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-getting-started-with-ios"
---

Explore essential iOS integration requirements and learn how to run sample code effectively in this topic.

<span id="NU1benUbph"></span>
# Integration requirements overview

Learn about the prerequisites of BytePlus Video Editor SDK before you integrate it into your iOS project.

<span id="qnMWoIkOUU"></span>
## Development environment

These are the development environment requirements that must be met:


* **Device**: iPhone 6s or later

* **Swift**: no version requirement (All components are implemented in Objective\-C.)

* **Xcode**: 14.0 or later

* **iOS**: 9.0 or later

* **Languages**: Objective\-C and Swift

* **CocoaPods**: 1.11.3 or later


<span id="JUGeu9DT0L"></span>
## Obtaining a license

To obtain a test or official license of the BytePlus Video Editor SDK, contact your BytePlus Video Editor SDK team.

<span id="bUbWeaIA2v"></span>
## Available languages

Chinese and English are supported. More languages can be added as needed.

<span id="J8q0cK1uRx"></span>
## Supported media formats

These are the supported media formats within BytePlus Video Editor SDK:


|**Type** ||**Video** |**Image** |**Audio** |
|---|---|---|---|---|
|Input |* File Types<br><br>* Container Formats |* .mp4<br><br>* .mov |* .jpg<br><br>* .png<br><br>* .gif |* .mp3<br><br>* .aac<br><br>* .wav |
||Format |* H.264<br><br>* H.265 |N/A |N/A |
|Output |* File Types<br><br>* Container Formats |.mp4 |N/A |N/A |


<span id="ad8a7fca"></span>
## SDK deliverables list

For more information on the SDK packages, refer to [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/27326).

<span id="e62ZFPNDTt"></span>
## SDK package sizes

The following table details the various BytePlus Video Editor SDK package sizes:


|**Categories** |**Built into the App** | **.zip Package Size** |**Description** |
|---|---|---|---|
|BytePlus Video Editor SDK |Yes |22.4MB |Arm64 architecture |
|Display resources that UI components depend on |Yes |0.4 MB |Icons, text, and configuration files |
|Editing resources that UI components depend on |No |Large in size. We recommend that you put them online. |Stickers, filters, fonts, special effects, licenses, and algorithmic models |


<span id="kae0LyfI8X"></span>
# Running the sample code

Get hands\-on with the BytePlus Video Editor SDK by downloading our sample project and running it in an iOS environment. Dive into the SDK's functionality and explore seamless integration possibilities.

**To run the sample code:** 


1. Install Ruby on your Mac and run the following command in Terminal to install CocoaPods:

   ```C++
   sudo gem install cocoapods  
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on methods to install CocoaPods, refer <a href="https://cocoapods.org/">here</a>.   </div>
   

2. Download the sample code. Reach out to the BytePlus Video Editor SDK team if you have not downloaded the sample code.

3. Open the `EffectOne-iOS` folder of the sample code.

   Replace `path/to/EffectOne-iOS` with the actual path to your project.

   ```C++
   cd {path}/to/EffectOne-iOS  
   ```
   

4. Open the command line and run `pod install --repo-update` and `open EffectOne-iOS.xcworkspace` commands.

   ```C++
   pod install --repo-update
   open EffectOne-iOS.xcworkspace   
   ```
   

   If the following error occurs when installing pod, run the `gem update xcodeproj` command to resolve this.

   ```C++
   ### Error
   ```
   

   RuntimeError \- [Xcodeproj] Unknown object version (56).

   /Library/Ruby/Gems/2.6.0/gems/xcodeproj\-1.21.0/lib/xcodeproj/project.rb:228:in `initialize_from_file' /Library/Ruby/Gems/2.6.0/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:113:in`open'

   ```Plain Text
   
   ```
   

5. In Xcode, click **TARGETS** \> **EffectOne** \> **Signing & Capabilities** \> **Signing**.

6. Enter your own developer certificate in the **Signing Certificate Apple Development** field.

7. You can proceed to run the demo project.
