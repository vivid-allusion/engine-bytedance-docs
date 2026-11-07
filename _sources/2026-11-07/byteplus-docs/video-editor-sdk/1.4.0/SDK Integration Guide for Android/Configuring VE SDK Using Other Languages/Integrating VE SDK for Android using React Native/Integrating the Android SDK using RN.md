---
title: "Integrating the Android SDK using RN"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-integrating-the-android-sdk-using-rn"
---

This topic describes how to add dependencies, configure permissions, and link native modules in your Android React Native (RN) project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific Android integration configuration, refer to the standard integration documentation: <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-android-sdk-quick-start-guide">Android SDK Quick Start Guide</a>. This topic covers the details of native integration and bridging, as well as important considerations.</div>


<span id="7f9a8f42"></span>
# **Prerequisities**

Before you begin with creating React Native projects, ensure that the following requirements have been met:


* Downloaded Android Studio.

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to [Android sample SDK deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/140-android-sample-sdk-deliverables-list).

* Set up your RN environment. For more information, refer to the [RN developers guide](https://reactnative.dev/docs/set-up-your-environment?platform=ios).

* Completed the steps in: [Configuring React Native projects in Android](https://docs.byteplus.com/docs/video-editor-sdk/29918).

* Completed steps 1\-4 in: [Android SDK Quick Start Guide](https://docs.byteplus.com/docs/video-editor-sdk/140-android-sdk-quick-start-guide).


<span id="9b11dd1a"></span>
# Adding RN bridge interface files

RN bridge interface files are used to connect React Native JavaScript code with native Android code. They facilitate communication between the two, allowing JavaScript to call native methods and vice versa. This enables React Native apps to utilize platform\-specific features and functionality not available in JavaScript alone.

Add RN bridge interface files using `RNEffectModule.kt` for handling RN events and `EOReactNativePackage.kt` for module registration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1582021742c04e8f96e55cfeb2b66775~tplv-goo7wpa0wc-image.image) </span>

<span id="c7cd17dc"></span>
## `RNEffectModule.kt`

```Kotlin
package com.volcengine.effectone

import androidx.fragment.app.FragmentActivity 
import com.facebook.react.bridge.ReactApplicationContext
import com.facebook.react.bridge.ReactContextBaseJavaModule
import com.facebook.react.bridge.ReactMethod
import com.volcengine.effectone.business.EODuetInitHelper
import com.volcengine.effectone.business.EOQuickInitHelper
import com.volcengine.effectone.business.R
import com.volcengine.effectone.utils.runOnUiThread
import com.volcengine.effectone.widget.EOToaster

class RNEffectModule(reactContext: ReactApplicationContext?) :
    ReactContextBaseJavaModule(reactContext) {

    companion object {
        private const val TAG = "RNEffectModule"
    }

    private val reactContext = reactContext

    override fun getName(): String {
        return "RNEffectModule"
    }

    @ReactMethod
    fun reacNativeWithActionName(actionName: String) {
        runOnUiThread {
            when (actionName) {
                "Record" -> {
                    if (MainActivity.authResult) {
                        reactContext?.currentActivity?.let {
                            EOQuickInitHelper.startRecorder(it as FragmentActivity)
                        }
                    } else {
                        reactContext?.currentActivity?.let {
                            EOToaster.show(it, R.string.eo_frontpage_auth_fail)
                        }
                    }
                }
                "Draft" -> {
                    if (MainActivity.authResult) {
                        reactContext?.currentActivity?.let {
                            EOQuickInitHelper.startDraft(it as FragmentActivity)
                        }
                    } else {
                        reactContext?.currentActivity?.let {
                            EOToaster.show(it, R.string.eo_frontpage_auth_fail)
                        }
                    }
                }
                "Duet" -> {
                    if (MainActivity.authResult) {
                        reactContext?.currentActivity?.let {
                            EODuetInitHelper.startDuet(it as FragmentActivity)
                        }
                    } else {
                        reactContext?.currentActivity?.let {
                            EOToaster.show(it, R.string.eo_frontpage_auth_fail)
                        }
                    }
                }
            }
        }
    }
}
```


<span id="4b2c5f34"></span>
## `EOReactNativePackage.kt`

```Kotlin
package com.volcengine.effectone

import android.view.View
import com.facebook.react.ReactPackage
import com.facebook.react.bridge.NativeModule
import com.facebook.react.bridge.ReactApplicationContext
import com.facebook.react.uimanager.ReactShadowNode
import com.facebook.react.uimanager.ViewManager

class EOReactNativePackage: ReactPackage {

    override fun createNativeModules(reactApplicationContext: ReactApplicationContext): MutableList<NativeModule> {
        return mutableListOf(RNEffectModule(reactApplicationContext))
    }

    override fun createViewManagers(p0: ReactApplicationContext): MutableList<ViewManager<View, ReactShadowNode<*>>> {
        return mutableListOf()
    }
}
```


<span id="e2d25da7"></span>
# Android RN best practices

These are some best practices that you can use when integrating the Android RN project.

<span id="ef4f1f7c"></span>
## Using `EOQuickInitHelper.kt`

When starting screens with `EOQuickInitHelper.kt`, make sure to run this code on the UI or main thread because it involves permission requests. Also, pass `FragmentActivity` as the parameter. If you're using `ReactActivity()`, you can cast it to `FragmentActivity` to meet this requirement.

```Kotlin
 @ReactMethod
    fun reacNativeWithActionName(actionName: String) {
        runOnUiThread {
            when (actionName) {
                "Record" -> {
                    if (MainActivity.authResult) {
                        reactContext?.currentActivity?.let {
                            EOQuickInitHelper.startRecorder(it as FragmentActivity)
                        }
                    } else {
                        reactContext?.currentActivity?.let {
                            EOToaster.show(it, R.string.eo_frontpage_auth_fail)
                        }
                    }
                }
                ......
            }
        }
    }
```


<span id="1a46dfe6"></span>
## Configuring JDK and Kotlin versions

Check that your JDK and Kotlin versions match those supported by React Native. Update the `version.gradle` file to set the correct versions. In `gradle.properties`, set `org.gradle.java.home` to the path of your JDK. This ensures that your development environment and project JDK are compatible.

<span id="e5d15351"></span>
## Configuring Maven repositories

In the `settings.gradle` file, set the Maven repository mode to `RepositoriesMode.PREFER_SETTINGS`. This setting makes sure that the repository configurations you set are used during the build.\

```Kotlin
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.PREFER_SETTINGS)
    repositories {
        google()
        mavenCentral()
        maven {
            url 'https://artifact.bytedance.com/repository/Volcengine/'
        }
        maven {
            url "https://artifact.bytedance.com/repository/thrall_ck/"
            credentials {
                username = MAVEN_USER_NAME
                password = MAVEN_PASS_WORD
            }
            authentication {
                digest(BasicAuthentication)
            }
        }
    }
}

......
```


<span id="05d2e0a5"></span>
## Configuring Maven for SDK access

When running the demo, set `MAVEN_USER_NAME` and `MAVEN_PASS_WORD` to access the Video Editor SDK. These credentials are required to download the SDK from the Maven repository. Without them, you won’t be able to get the SDK.
