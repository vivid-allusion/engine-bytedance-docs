---
title: "Configuring repositories and dependencies using gradle"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-configuring-repositories-and-dependencies-using-gradle"
---

This topic covers how to configure repositories and dependencies in Gradle for your Android project.

<span id="a8b93fac"></span>
# Prerequisities

Ensure you have imported the required dependencies and integrated Video Editor SDK into your project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using <code>ComponentActivity</code> as your host instead of <code>FragmentActivity</code>, the Android runtime permission\-related interfaces provided in <code>EOQuickInitHelper</code> cannot be used. You can refer to the source code of <code>EOQuickInitHelper.kt</code>and implement them. For more information on requesting runtime permissions in Android, refer <a href="https://developer.android.com/training/permissions/requesting">here</a>.</div>


<span id="82646b6d"></span>
# Configuring repositories and dependencies in `setting.gradle.kts` file

For more information on the Maven authentication differences between the `.gradle.kts` file and the `.gradle` file, refer to **Example 30** in the [Declaring repositories](https://docs.gradle.org/8.4/userguide/declaring_repositories.html).

**To configure the Maven repository in** **`setting.gradle.kts`** ** file**:


1. Configure the URL and credentials of the following repositories:

   ```Java
   // In the setting.gradle.kts file, use the following configurations:
   dependencyResolutionManagement {
       ...
       repositories {
           ...
           maven("https://artifact.bytedance.com/repository/thrall_ck/") {
               credentials {
                   username = MAVEN_USER_NAME
                   password = MAVEN_PASS_WORD
               }
               authentication {
                   create<BasicAuthentication>("basic")
               }
           }
           maven("https://artifact.bytedance.com/repository/thrall_cv/") {
               credentials {
                   username = MAVEN_USER_NAME
                   password = MAVEN_PASS_WORD
               }
               authentication {
                   create<BasicAuthentication>("basic")
               }
           }
       }
   }
   ```
   


<span id="4cb7c2f8"></span>
# Configuring dependencies in `app/build.gradle.kts` file


1. Add the following dependencies to your`build.gradle.kts` file:

   ```Java
   def effectOneVersion="1.0.0"
   dependencies {
       api("com.volcengine.effectone:editor-ui:${effectOneVersion}")
       api("com.volcengine.effectone:recorder-ui:${effectOneVersion}")
       //The resource loading SDK
       api("com.volcengine.effectone:base-resource:${effectOneVersion}")
       //The three SDKs above share the same version. 
       implementation("com.github.bumptech.glide:glide:4.13.2")// The default dependency for photo(DefaultImageLoader), which can be added as needed.
       implementation("androidx.appcompat:appcompat:1.3.0") //Specify the desired version according to your hosted development environment. Suggested version: 1.3.0.
   }
   ```
   

2. In the same file, add the following line to the file:

   ```Java
   android {
       ...
       defaultConfig {
           ...
           vectorDrawables.useSupportLibrary = true // Set the SDK to support vectorDrawable. This library can be used when you need to replace SVG photos with EffectOneSDK.
           applicationId = "com.volcengine.effectone" //Ensure the package name is consistent with the name of the authorized package. 
       }
       packaging { 
           ...
           jniLibs {
               useLegacyPackaging = true
           }
           jniLibs.pickFirsts.add("lib/arm64-v8a/libc++_shared.so")
           jniLibs.pickFirsts.add("lib/armeabi-v7a/libc++_shared.so")
       }
   
   }
   ```
   


<span id="ab4ffec8"></span>
# Configuring gradle.properties

```Kotlin
android.useAndroidX=true 
android.enableJetifier=true 
```
