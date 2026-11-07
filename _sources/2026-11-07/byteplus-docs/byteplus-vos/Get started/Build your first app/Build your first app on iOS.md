---
title: "Build your first app on iOS"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-ios-"
---

To build an iOS application with interactive live streaming and video playback capabilities, you can follow this step\-by\-step guide to run the VideoOne demo project. This document walks you through the entire process, from completing prerequisites and configuring your project to compiling and running the app on a physical device.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">GitHub demo project does not include all features available in the demo app, such as beauty AR. Refer to the solution implementation guides for instructions on how to implement these features. If you need further assistance, please contact your <a href="https://console.byteplus.com/workorder/create">technical support</a>.</div>


<span id="5a07e3aa"></span>
## Prerequisites

Complete the following tasks before you start. We recommend that you keep a centralized record of the information gained after completing each task for easy reference during project setup.

Some tasks are for specific features and can be skipped if you do not need them. For example, if you only want to use video playback, you do not need to activate BytePlus RTC and BytePlus MediaLive services.


|**Task** |**Relevant feature** |**Task instruction** |**Information gained upon completion** |
|---|---|---|---|
|1. Register a BytePlus account.<br><br>2. Create an access key for the account. |All features |* [Signing up for a BytePlus account](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account)<br><br>* [Creating an access key](https://docs.byteplus.com/byteplus-platform/docs/creating-an-accesskey) |* Access Key ID (AK)<br><br>* Secret Access Key (SK) |
|1. Activate the BytePlus RTC service.<br><br>2. Create an RTC app. |* Interactive live streaming<br><br>* RTC API Example |* [Before Using RTC Service](https://docs.byteplus.com/byteplus-rtc/docs/69865) |* AppId<br><br>* AppKey |
|1. Activate the BytePlus MediaLive service.<br><br>2. Create a MediaLive app and obtain a license.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already created a BytePlus VOD app, bind the existing app instead of creating a new one.   </div><br>    |Interactive live streaming |* [Activating the MediaLive service](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#activating-the-medialive-service)<br><br>* SDK management<br><br>   * [Creating an SDK application](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)<br><br>   * [Accessing your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license) |* App ID<br><br>* BytePlus MediaLive SDK license file |
|1. Activate the BytePlus VOD service.<br><br>2. Create a VOD app and obtain a license.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have already created a BytePlus MediaLive app, bind the existing app instead of creating a new one.   </div><br>    |Video playback |* [Step 1: Enable the BytePlus VOD service](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started#step-1-enable-the-byteplus-vod-service)<br><br>* [Application management](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management)<br><br>* [License management](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) |* App ID<br><br>* BytePlus VOD SDK license file |


<span id="bfda08e6"></span>
### System requirements


* Xcode 14.0 or higher

* CocoaPods 1.10.0 or higher

* A physical mobile device that runs iOS 13.0 or higher.


<span id="74286d48"></span>
## Procedures

Some tasks are specific to certain features and can be skipped if you do not need to experience those particular features. For example, if you want to experience interactive live streaming only, you do not need to complete the setup for video playback.

<span id="9d161712"></span>
### Cloning the project

Follow the steps below to clone the demo project:


1. Go to GitHub and clone the [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions) repository.

2. Open Terminal, and change the current directory to `Client/iOS`, which is the root directory of the project.

3. Move the license files that you have acquired in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section to the `Component/AppConfig/License` directory. You may need to rename the license files if you have several licenses with the same file name.

4. Run `pod install` to install dependencies.


<span id="32bcb285"></span>
### Setting the app server


1. Under the root directory of the project, open the`VideoOne.xcworkspace` file in Xcode.

2. Navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file in Xcode.

3. Specify the address of your app server:

   * To use the app server provided by BytePlus, set the `ServerUrl` field to `https://videocloud.byteplusapi.com/videoone_opensource`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This address is for testing purposes only, and cannot be used in a production environment.      </div>
      

   * To deploy your own app server, follow the instructions in [Deploying the app server](https://docs.byteplus.com/docs/byteplus-vos/docs-backend-deployment-guide), and then set the `ServerUrl` field to `http://{your_server_address}:{port_number}/videoone_opensource`.


<span id="60922590"></span>
### Setting your project


1. In Xcode, log in with your Apple ID.

2. Refer to [Assign a project to a team](https://help.apple.com/xcode/mac/current/#/dev23aab79b4) to configure app signing.

3. Set **Bundle Identifier**. If you have applied for the BytePlus MediaLive SDK license or BytePlus VOD SDK license, the bundle identifier must be identical to the name you used during the license application.

4. If you are using Xcode 15, you must complete an additional build setting configuration:

   1. Navigate to the **TARGETS** page, and switch to the **Build Settings** tab.

   2. Search for the **Other Linker Flags** setting.

   3. Double\-click the value area on the **Other Linker Flags** row.

   4. In the pop\-up window, click the  **+**  button and add the `-ld64` linker flag.


<span id="a1e62caa"></span>
### Setting up for RTC

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This task is required if you want to use the interactive live streaming feature.</div>


In Xcode, navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file. Configure the following fields with the values you obtained in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section. The information is used for authentication when the client communicates with the BytePlus RTC service.


|**Field name** |**Description** |**Example** |
|---|---|---|
|RTCAPPID |The **AppId** of your BytePlus RTC app. |123456\*\*\*\*\*\*\*\*3deb567a86 |
|RTCAPPKey |The **AppKey** of your BytePlus RTC app. |1bfaa8e\*\*\*\*\*\*\*\*fjb6j6hhde68c07d |
|AccessKeyID |The **Access Key ID (AK)**  of your BytePlus account. |AKAPZ7\*\*\*\*\*\*\*\*FLB0D38CM8DK49SO39D83KD820DFK4k9 |
|SecretAccessKey |The **Secret Access Key (SK)**  of your BytePlus account. |8dk39vK\*\*\*\*\*\*\*\*k7D93KDHS8DJSLud830DJEO37EI3UDK37WODKu3oQ |


<span id="f15de15f"></span>
### Setting up for MediaLive

<span id="b758f198"></span>
#### Preparing domain names

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This task is required if you want to use the interactive live streaming feature.</div>



|**Subtask** |**Task instruction** |**Required information** |
|---|---|---|
|**Add domain names.** <br><br>You should add at least two domain names, one for stream pushing, and the other for stream pulling. |[Adding domain names](https://docs.byteplus.com/en/byteplus-media-live/docs/domain?version=v1.0#bb9e1337) |* domain name for stream pushing<br><br>* domain name for stream pulling |
|**Add a CNAME record for your domain name.** <br><br>After you add a domain name, a BytePlus MediaLive domain name will be automatically assigned to your domain name. You must add a CNAME record for your domain name to point to the assigned BytePlus MediaLive domain name. |[Adding a CNAME record](https://docs.byteplus.com/en/byteplus-media-live/docs/adding-a-cname-record?version=v1.0) |/ |
|**Enable URL authentication.** <br><br>To maintain secure stream pushing and prevent unauthorized downloads of live\-stream information, you can enable URL authentication. This step provides protection against unauthorized use of domain names. |[URL authentication](https://docs.byteplus.com/en/byteplus-media-live/docs/url-authentication?version=v1.0) |* Primary key |
|**Configure a transcoding template.** <br><br>You can transcode the original live stream to meet the viewing requirements of different users. |[Configuring a transcoding task](https://docs.byteplus.com/en/byteplus-media-live/docs/configuring-transcoding) |* AppName |


<span id="cf1eeec6"></span>
#### Setting stream addresses

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This task is required if you want to experience the interactive live streaming scene.</div>


In Xcode, navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file and fill in the corresponding fields with the information obtained in the previous step. The information is used for concatenating the push and pull stream addresses.


|**Field name** |**Description** |**Example** |
|---|---|---|
|LivePullDomain |http://{domain_name}, where "domain_name" represents the **domain name for stream pulling**. |`http://pull-demo.com` |
|LivePushDomain |rtmp://{domain_name}, where "domain_name" represents the **domain name for stream pushing**. |`rtmp://push-demo.com` |
|LivePushKey |The **Primary key** for URL authentication. |`XED45d5dDLSH********KDFD` |
|LiveAppName |The **AppName** for which you have configured a transcoding template. |`videoone_demo` |


<span id="2c5d644a"></span>
#### Integrating the license

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This task is required if you want to experience either interactive live streaming scene or live streaming\-related functions.</div>


Follow the steps below to integrate the BytePlus MediaLive SDK license:


1. In Xcode, navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file.

2. Set the following fields:



|**Field name** |**Description** |**Example** |
|---|---|---|
|LiveAPPID |The **App ID** of the MediaLive app you created or bound in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section. |5\*\*\*\*1 |
|LiveLicenseName |The name of the **BytePlus MediaLive SDK license file** you obtained in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section. |livelicense.lic |



3. Refer to [Generating stream addresses](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator) to prepare push and pull streaming URLs.


<span id="047a3955"></span>
### Setting up for VOD

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This task is required if you want to experience the video playback scene and related functions.</div>


Follow the steps below to integrate the BytePlus VOD SDK license:


1. In Xcode, navigate to `Pods/Development Pods/AppConfig` and open the `BuildConfig.h` file.

2. Set the following fields:

   
   |**Field name** |**Description** |**Example** |
   |---|---|---|
   |VODAPPID |The **App ID** of the VOD app you created or bound in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section. |5\*\*\*\*1 |
   |VODLicenseName |The name of the **BytePlus VOD SDK license file** you obtained in the [Prerequisites](https://docs.byteplus.com/en/docs/28/8552#prerequisites) section. |vodlicense.lic |
   


<span id="02dbf3ad"></span>
### Compiling the project


1. Connect the mobile device to your computer, and set it as the target device in Xcode.

2. Click **Product** \> **Run** to initiate the compilation process.


<span id="cc07540a"></span>
### Trying the app

If the compilation process completes without any errors, the VideoOne app will be installed on the connected mobile device and you will be directed to the login screen automatically. Log in to the app with your email, then you can start exploring different scenarios and functions provided in the app.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using a free Apple developer account, you may need to adjust the settings on your mobile device to allow apps from untrusted developers to run. In most cases, you can go to <strong>Settings</strong> \> <strong>General</strong> \> <strong>Device Management</strong> to trust the developer certificate.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fbbafc47ec843529888b307d1af14f2~tplv-goo7wpa0wc-image.image) </span>

<span id="f5f5fc6f"></span>
## Understanding the code

The directory tree of the demo project is as follows:

```Plain
. 
├── VideoOne                           # Entry point of the project 
└── Pods 
    ├── Podfile 
    └── Development Pods 
        ├── App                        # Entry point of the demo app 
        ├── AppConfig                  # App configurations 
        ├── LoginKit                   # Login          
        ├── ToolKit                    # Common tools  
        ├── InteractiveLive            # The interactive live streaming solution 
        │   ├── Common                 # Common components 
        │   └── Feature                # Features 
        │       ├── Controller 
        │       ├── Model 
        │       └── View 
        ├── RTCAPIExample               # The RTC API Example solution 
        │   ├── QuickStart            
        │   ├── VideoManager
        │   ├── AudioManager       
        │   └── ...                    # Many other RTC features       
        ├── MediaLive                   # The MediaLive solution 
        │   ├── Entry                   # Entrance
        │   ├── MediaLive.podspec
        │   ├── Pull                    # Live stream pulling
        │   ├── Push                    # Live stream pushing
        │   ├── Resources               # Multilingual copywriting
        │   ├── ScreenCapture           # Screen-sharing stream pushing
        │   ├── VELCommon               # Common tools
        │   └── VELSettings             # Configuration related to stream pushing and pulling
        └── VideoPlaybackEdit          # The video playback and editing solution     
            ├── FeedVideo              # Mid-form video 
            ├── LongVideo              # Long-form video 
            └── ShortVideo             # Short-form video 
            └── SingleFunction         # Code for separate functions 
                 ├── PlayList          # Video playlist 
# Screen capture protection
                 ├── SmartSubtitles    # Smart subtitling 
                 ├── VideoPlayback     # Other playback-related functions 
```
