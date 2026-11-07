---
title: "iOS Access Privacy Configuration PrivacyInfo.xcprivacy"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/iOS_Access_Privacy_Configuration_PrivacyInfo_xcprivacy"
---

According to the latest privacy protection policy of Apple's App Store update/listing APP, if you use DataFinder's iOS SDK for data collection, you need to provide the APP and SDK\-related privacy profile (PrivacyInfo.xcprivacy) at the same time, explaining how the App handles user data. This article provides you with the privacy profile description of DataFinder's iOS SDK. You need to integrate the privacy profile description of the SDK into your APP according to the actual sub\-library used.

<span id="6aa0a638"></span>
# Get Finder's PrivacyInfo.xcprivacy

Click the attachment link below to download the PrivacyInfo.xcprivacy attachment for DataFinder's iOS SDK.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0639ad6970e04398b4f1f67416697aaa~tplv-goo7wpa0wc-image.image" name="PrivacyInfo.xcprivacy">PrivacyInfo.xcprivacy</Attachment>


&nbsp;

After downloading to your local, you can open to view the configuration details of PrivacyInfo.xcprivacy, which will comment out some sub\-libraries that are not used by all users. You need to manually remove the comments according to the actual usage. If you use some special sub\-libraries, you need to manually modify them. For details, please refer to the following **View and Modify PrivacyInfo.xcprivacy** .

<span id="791a75d4"></span>
# View and modify PrivacyInfo.xcprivacy

PrivacyInfo.xcprivacy in DataFinder lists the privacy data collected by the iOS SDK and the privacy API used, which defaults to the minimum set of sublibraries involved by all users.

```JavaScript
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        'Core'
    ]
```


When using the UITracker sublibrary, Exception sublibrary, or Unique sublibrary, you need to manually uncomment the content of the corresponding sublibrary in PrivacyInfo.xcprivacy.

<span id="8760fe2c"></span>
## UITracker sublibrary

This sub\-library is generally used for full event tracking function. If you use this sub\-library, you need to add the following content to the NSPrivacyCollectedDataTypes (this part of the content is commented out by default in the PrivacyInfo.xcprivacy file of DataFinder, you can manually release the relevant comments).

```XML
<! -- If using UITracker sublibrary, please release NSPrivacyCollectedDataTypeProductInteraction -- >
<dict>
    <key>NSPrivacyCollectedDataType</key>
    <string>NSPrivacyCollectedDataTypeProductInteraction</string>
    <key>NSPrivacyCollectedDataTypeLinked</key>
    <true/>
    <key>NSPrivacyCollectedDataTypeTracking</key>
    <false/>
    <key>NSPrivacyCollectedDataTypePurposes</key>
    <array>
        <string>NSPrivacyCollectedDataTypePurposeAnalytics</string>
    </array>
</dict>
```


<span id="8b8feaa9"></span>
## Exception sublibrary

This sub\-library is generally used for exception collection function. If you use this sub\-library, you need to add the following content to the NSPrivacyCollectedDataTypes (this part of the content is commented out by default in the PrivacyInfo.xcprivacy file of DataFinder, you can manually release the relevant comments).

```XML
<! -- If the Exception sublibrary is used, release NSPrivacyCollectedDataTypeCrashData -- >
<dict>
    <key>NSPrivacyCollectedDataType</key>
    <string>NSPrivacyCollectedDataTypeCrashData</string>
    <key>NSPrivacyCollectedDataTypeLinked</key>
    <true/>
    <key>NSPrivacyCollectedDataTypeTracking</key>
    <false/>
    <key>NSPrivacyCollectedDataTypePurposes</key>
    <array>
        <string>NSPrivacyCollectedDataTypePurposeAnalytics</string>
    </array>
</dict>
```


<span id="66dc1968"></span>
## Unique sublibrary

This sublibrary is generally used for idfa data collection. If you use this sublibrary, you need to enable NSPrivacyTracking and set TrackingDomains. The default NSPrivacyTracking property is turned off.

Please do the following in the PrivacyInfo.xcprivacy file


1. Remove DataFinder default NSPrivacyTracking and NSPrivacyTrackingDomains configuration (comment out the relevant content).

   ```XML
   <! -- If you use a Unique sublibrary, please comment out the following configuration NSPrivacyTracking, NSPrivacyTrackingDomains -- >
   <key>NSPrivacyTracking</key>
   <false/>
   <key>NSPrivacyTrackingDomains</key>
   <array/>
   ```
   

2. Reconfigure NSPrivacyTracking as follows (this part of the content is commented out by default in the PrivacyInfo.xcprivacy file of DataFinder, you can manually release the relevant comments).

   ```XML
   <! -- If you use a Unique sublibrary, release the following NSPrivacyTracking, NSPrivacyTrackingDomains -- >
   <key>NSPrivacyTracking</key>
   <true/>
   ```
   

3. Reconfigure NSPrivacyTrackingDomains (this part is commented out by default in the PrivacyInfo.xcprivacy file of DataFinder, you can manually release the relevant comments).

   
   |**DataFinder environment type** |**Modification example** |
   |---|---|
   |SaaS\-cloud native environment |```XML```<br>```<key>NSPrivacyTrackingDomains</key>```<br>```<! -- Cloud native version, please use this paragraph -- >```<br>```<array>```<br>```    <string>gator-tracking.datafinder.volces.com</string>```<br>```    <string>tab-tracking.abtest.volces.com</string>```<br>```</array>```<br> |
   |Privatized environment |```XML```<br>```<key>NSPrivacyTrackingDomains</key>```<br>```<! -- privatized version, please configure your idfa request domain name here -- >```<br>```<array>```<br>```    <string>your tracking domain</string>```<br>```</array>```<br><br><br>Where `your tracking domain`needs to be changed to your idfa dedicated request domain. |
   


<span id="616d8793"></span>
# Access PrivacyInfo.xcprivacy configuration to APP

Insert the SDK PrivacyInfo.xcprivacy file that meets your APP business scenario into your APP. The following provide you with two access methods, which you can refer to on demand.

If you need to configure the PrivacyInfo.xcprivacy file separately in the SDK, you can skip this section and proceed to the next section.

<span id="bce42166"></span>
## Access method 1: Merge into the app's privacy configuration (recommended)

In most scenarios, it is recommended that you directly merge the privacy configuration of the SDK into the privacy configuration of the app. That is, directly merge the PrivacyInfo.xcprivacy file of the SDK into the PrivacyInfo.xcprivacy file of the App. The operation reference is as follows.


1. Right\-click and select Open AS \-\- \> Source Code to open the PrivacyInfo.xcprivacy file of the SDK.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15bd5a39941c437b947c0047d553fe90~tplv-goo7wpa0wc-image.image" width="566px" />   </div>
   

2. Copy the content under NSPrivacyAccessedAPITypes and NSPrivacyCollectedDataTypes to the corresponding location in the PrivacyInfo.xcprivacy file of the App.

   
   |NSPrivacyAccessedAPITypes Location Example |NSPrivacyCollectedDataTypes Location Example |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d09ebb8d6db846a7a214696304d26444~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/459415f4f5cd4544861ccc3503a6f1df~tplv-goo7wpa0wc-image.image) </span> |
   

3. If IDFA data is used, you will also need to copy the content under NSPrivacyTrackingDomains.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d0bf8b62564aaa991d9a3f3e935c9b~tplv-goo7wpa0wc-image.image" width="686px" />   </div>
   

4. Once the PrivacyInfo.xcprivacy file is configured, make sure it is imported in Build Phases \-\- \> Copy Bundle Resources.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79770a870dbe47ccad1aebcbd8aa5b4f~tplv-goo7wpa0wc-image.image" width="580px" />   </div>
   


<span id="642a125b"></span>
## Access Mode 2: Use a separate SDK privacy configuration

If you are manually introducing our offline installation package and encapsulating the installation package as a framework or pod dependency, it is recommended to use this method for configuration.


* If we re\-encapsulate our SDK as a framework, we can place the PrivacyInfo.xcprivacy file directly in the framework directory.

* If we re\-encapsulate our SDK as a pod dependency, configure the PrivacyInfo.xcprivacy file in the pod's resource_bundles.


<span id="69f85faa"></span>
# Modify the SDK integration code and configure the privacy domain name

If idfa data is used and Unique sublibraries are used, you need to modify the SDK integration configuration and configure the request domain name of idfa as follows.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>The minimum version of the SDK that supports private domain configuration is 6.16.6.</strong></div>


<span id="0cfae280"></span>
### SaaS version

Upgrade the SDK to 6.16.6 version without additional configuration.

<span id="5af6a74a"></span>
### cloud native version

Introducing dependencies in a Podfile

```JavaScript
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        'Unique',
    ]
```


Introduction of IDFA headers

```objectivec
#import <RangersAppLog/BDAutoTrack+IDFA.h>
```


After SDK initialization, configure the IDFA dedicated domain name

```objectivec
//Cloud native mode
config.serviceVendor = BDAutoTrackServiceVendorPrivate;
[BDAutoTrack setRequestHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
    return @"https://gator.volces.com";
}];

//initialize sdk
[BDAutoTrack sharedTrackWithConfig:config];

//Configure the idfa dedicated domain name
[BDAutoTrack.sharedTrack setRequestIDFAHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
    return @"https://gator-tracking.datafinder.volces.com";
}];

//start sdk
[BDAutoTrack.sharedTrack startTrack];
```


<span id="942b33cd"></span>
### privatized version

In the privatization scenario, the dedicated domain name of IDFA is provided by the user, and the domain name rules only need to be different from the originally reported domain name.


* The dedicated domain name of idfa can be the same as the IP pointed to by the original domain name.

* The dedicated domain name of idfa can use the same main domain as the original domain name.


Introducing dependencies in a Podfile

```JavaScript
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        'Unique',
    ]
```


Introduction of IDFA headers

```objectivec
#import <RangersAppLog/BDAutoTrack+IDFA.h>
```


After SDK initialization, configure the IDFA dedicated domain name

```JavaScript
//privatization model
config.serviceVendor = BDAutoTrackServiceVendorPrivate;
[BDAutoTrack setRequestHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
    return @"{{REPORT_URL}}";
}];

//initialize sdk
[BDAutoTrack sharedTrackWithConfig:config];

//Configure the idfa dedicated domain name
[BDAutoTrack.sharedTrack setRequestIDFAHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
    return @"{{IDFA_REPORT_URL}}";
}];

//start sdk
[BDAutoTrack.sharedTrack startTrack];
```
