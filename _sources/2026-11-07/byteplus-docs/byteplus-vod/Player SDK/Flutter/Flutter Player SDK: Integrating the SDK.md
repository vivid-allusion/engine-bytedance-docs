---
title: "Flutter Player SDK: Integrating the SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-quickstart"
---

This article introduces how to integrate the Flutter Player SDK into your project.

## Development environment

* Flutter stable channel 3.0.0 or higher

* Dart 2.17.0 or higher

* System version:

   * iOS 11.0 or higher

   * Android 4.1 or higher (`minSdkVersion: 16`). The SDK requires armv7 or arm64 architectures

   > **Warning**

   > We recommend testing on actual devices as simulators may lack features or have performance issues.

* It is recommended to use the latest versions of Visual Studio Code or Android Studio.

## Prerequisites

Before integrating the SDK, complete the following on the [SDK management](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console:

* Create an app and get the app ID and the app's English name. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).

* Register your app, and then purchase and download a license for the Player SDK. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

> **Note**

> When you test your app, use the trial license. The validity period of the trial license is one month and cannot be extended. After the trial license expires, the SDK fails in authentication, and you must apply for a new one. Therefore, do not use the trial license in your production environment.

## Project structure

The project structure of the Flutter SDK is as follows:

```Shell
├── CHANGELOG.md
├── LICENSE
├── README.md
├── analysis_options.yaml
├── android
├── example
├── ios
├── lib
├── pubspec.lock
├── pubspec.yaml
└── vod_player_flutter.iml
```

The key folders are explained in the following table:

|Folder |Description |Required |
|---|---|---|
|`lib` |Plugin layer developed based on the native SDK. |Yes |
|`android` |Native code and player SDK for Android. |Yes |
|`ios` |Native code and player SDK for iOS. |Yes |
|`example` |Flutter player demo. |No |

## Procedure

### Add dependencies

The Flutter SDK supports two ways of adding dependencies: remote and local.

#### (Recommended) Method 1: Remote dependency

1. In the terminal, navigate to the root directory of your Flutter project and run the following command to install the dependency:

   ```Shell
   flutter pub add byteplus_vod:^1.52.101
   ```

2. Based on the edition you are integrating, add the following code to the `pubspec.yaml` file of your project:

   * For Standard Edition, add the following code:

      ```YAML
      byteplus_vod: 
        sub_spec: standard
      ```

   * For Premium Edition, add the following code:

      ```YAML
      byteplus_vod: 
        sub_spec: premium
      ```

      After adding the dependency, the `pubspec.yaml` file will contain the following code:

      ```YAML
      dependencies:
          byteplus_vod: <SDK_VERSION>
      ```

#### Method 2: Local Dependency

1. Go to the [download](https://pub.dev/packages/byteplus_vod) page and download the latest version of the SDK package to your local machine, then extract it.

2. Copy the SDK folder to your project directory.

3. Add the `byteplus_vod` dependency in the `pubspec.yaml` file as shown below:

   ```YAML
   dependencies:
       flutter:
           sdk: flutter
       # Replace <SDK_PATH> with the file path of the SDK in your project
       byteplus_vod: 
           path: <SDK_PATH>
   byteplus_vod: 
       sub_spec: premium
   ```

### Set up for each platform

Configure Android and iOS separately:

#### Android

In your project's `build.gradle` file, specify the [Maven central repository](https://search.maven.org/) and BytePlus' Maven repository as repository locations, as shown below:

```Groovy
allprojects {
    repositories {
        google()
        jcenter()
        // Maven central repository
        mavenCentral()
        maven {
            url "https://artifact.bytedance.com/repository/Volcengine/"
        }
        maven { 
            url "https://artifact.byteplus.com/repository/public/" 
        }
    }
}
```

You also need to add Java 8 support, permission declarations, and obfuscation rules. For details, see [Android Player SDK: Integrating the SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-integration-android).

#### iOS

1. [Disable bitcode](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#step-3-disable-bitcode).

2. Configure Pod source. Add the following source to the Podfile in your Xcode project:

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```

### Add license file

Place the license file you obtained in the assets directory of your Flutter project. You will need to pass the path of the license file when initializing the SDK.

```Ruby
assets
└── VEVod.lic
```

> **Warning**

> The Bundle ID, Package Name, and App ID of the project must be consistent with the information you provided when applying for a license in the VOD console; otherwise, authentication will fail.

## Next steps

Congratulations! You have successfully integrated the Player SDK. Now, let's see how to use the Player SDK to play videos. For more details, please refer to [Flutter Player SDK: Basic features](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-basic-features).
