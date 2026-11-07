---
title: "Android Sample for V4.5.2 and above running introduction"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-android-sample-for-v4-5-2-and-above-running-introduction"
---

Starting from 2023.8.31, applications released on Googleplay require upgrading **target API 31** to support Android 12 and above devices. Therefore, this sample supports target 31 **starting from V4.5.2**

However, due to the new requirements of the local environment configuration after supporting target 31, this section is noted for it.

<span id="2bbdfbbc"></span>
## This version changes


|**Upgrade items** |**Before upgrade** |**After upgrade** |
|---|---|---|
|targetSdkVersion |28 |31 |
|compileSdkVersion |28 |31 |
|buildToolsVersion |28.0.3 |31.0.0 |
|gradle |5.6.4 |7.2 |
|gradle plugin |3.5.3 |7.1.2 |


<span id="60098169"></span>
## Local environment configuration

The ndk version and cmake are the same as the original sample guide.

`cmake 3.6.4111459`

`ndk 21.1.6352462`

If you encounter other versions that cannot compile, please switch the ndk and cmake versions to the specified above.

**The Local Development Environment needs to be upgraded synchronously.** 

<span id="c3df3748"></span>
### Android studio version

Android Studio version requires Bumblebee or above, check see: [https://developer.android.com/build/releases/gradle-plugin](https://developer.android.com/build/releases/gradle-plugin)

<span id="83c22155"></span>
### Java version

Compile sample project, JDK version needs to be upgraded to JDK11

Download link: [https://www.oracle.com/java/technologies/downloads/#java11](https://www.oracle.com/java/technologies/downloads/#java11)

Configuration method: Android Studio \- \> Preference \- \> Build, Execution, Deployment \- \> Build Tools \- \> Gradle configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06419afa40064052970842643fb31c5d~tplv-goo7wpa0wc-image.image) </span>

<span id="73749973"></span>
## Attention

After upgrading target31, some functions before V4.5.2 (mostly related to image quality algorithm) need to be upgraded or adapted, and some props may not be available. For specific details, please consult relevant support or business.
