---
title: "React Native Player SDK: Integrating the SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart"
---

This article introduces how to integrate the React Native Player SDK into your project.

<span id="d65f117a"></span>
## Development environment


* React Native: 0.70 or higher

* Node: It is recommended to use 18.0 or higher

* System version:

   * iOS 11.0 or higher

   * Android: `minSdkVersion: 23`

* It is recommended to use the latest versions of Visual Studio Code or Android Studio


<span id="8331fde6"></span>
## Prerequisites

Before integrating the SDK, complete the following on the [SDK management](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console:


* Create an app and get the app ID and the English name of the app. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).

* Register for the app, and purchase and download a license for using the Player SDK. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you test your app, use the trail license. The validity period of the trail license is one month and cannot be extended. After the trail license expires, the SDK fails in authentication, and you must apply for a new one. Therefore, do not use the trail license in your online environment.</div>


<span id="3504cd7d"></span>
## Procedure

<span id="6f512bd6"></span>
### Add dependencies

Execute the following command in the root directory of your React Native project:

```Bash
yarn add @byteplus/react-native-vod-player
```


<span id="ed41639c"></span>
### Set up for each platform

Configure Android and iOS separately:

<span id="5f2d3880"></span>
#### Android


1. In the `repositories` section of the `build.gradle` file in the `android` folder of your React Native project, specify the [Maven central repository](https://search.maven.org/) and BytePlus' Maven repository as repository locations:

   ```Groovy
   allprojects {
       repositories {
           google()
           jcenter()
           mavenCentral()
           maven {
               url "https://artifact.byteplus.com/repository/public/"  // byteplus public maven repo
           }
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/"  // some additional dependencies
           }
       }
   }
   ```
   

2. Additionally, you need to add Java 8 support, permission declarations, and obfuscation rules. For details, see [Android Player SDK: Quickstart](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk).


<span id="70881a15"></span>
#### iOS


1. Configure the Pod source in the `Podfile` file in the `ios` folder of your React Native project:

   ```Ruby
   source 'https://github.com/CocoaPods/Specs.git'
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

2. [Disable bitcode](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#step-3-disable-bitcode).


<span id="724bdae3"></span>
### Add license file

Duplicate the license file you obtained and place them in the Android and iOS folders of your React Native project:


* Android: Place it in `android/app/src/main/assets`. If the `assets` folder does not exist, you can create one.

* iOS: Add it to `iOS/DemoApp` by clicking the **Add Files to** icon in Xcode, as shown in the following picture. `DemoApp` is the project name and can be modified according to your actual project name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c71feb2089b4358b5a4d998fb5201b5~tplv-goo7wpa0wc-image.image) </span>


You will need to pass the path of the license file when initializing the SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Bundle ID, Package Name, and App ID of the project should be consistent with the information you provided when applying for a license in the VOD console, otherwise authentication may fail.</div>


<span id="24043128"></span>
## Next steps

Congratulations! You have successfully integrated the Player SDK. Now, let's see how to use the Player SDK to play videos. For more details, please refer to [React Native Player SDK: Basic features](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-features).
