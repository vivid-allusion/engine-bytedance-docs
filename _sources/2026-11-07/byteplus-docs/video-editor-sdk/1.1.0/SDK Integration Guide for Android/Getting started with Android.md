---
title: "Getting started with Android "
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android_1_1_0"
---

<span id="8ff74eb5"></span>
# Integration overview

Learn about the integration overview of BytePlus Video Editor SDK that you must fulfill before you integrate it into your Android project.

<span id="13ddd4bf"></span>
## Development environment

The following table shows the required development environment for BytePlus Video Editor SDK:


|**Development Environment** |**Version** |
|---|---|
|Gradle |7.5.1 |
|Android Gradle Plugin |7.3.1 |
|kotlin |1.5.30 |
|minSdk |21 |
|targetSdk |33 |
|compileSdk |33 |
|Java Version |11 |


<span id="293b9023"></span>
## Third\-party library dependencies

The following table shows the required versions of third\-party library dependencies for BytePlus Video Editor SDK:


|**Library** |**dependency** |**Version** |
|---|---|---|
|Jetpack |androidx.appcompat:appcompat |1.3.0 |
||androidx.lifecycle:lifecycle\-viewmodel |2.3.1 |
|Material |com.google.android.material:material |1.2.0 |
|kotlinx.coroutines |org.jetbrains.kotlinx:kotlinx\-coroutines\-android |1.5.2 |
||org.jetbrains.kotlinx:kotlinx\-coroutines\-core |1.5.2 |
|StatusBar |com.geyifeng.immersionbar:immersionbar |3.2.2 |
||com.geyifeng.immersionbar:immersionbar\-ktx |3.2.2 |
|JSON resolution |com.google.code.gson:gson |2.9.0 |


<span id="384499c0"></span>
## Available languages

Chinese and English are supported. More languages can be added as needed.

<span id="e26583f8"></span>
## Obtaining a license

To obtain a trial or official license of BytePlus Video Editor SDK, contact the BytePlus Video Editor SDK team.

<span id="cfee56b4"></span>
## Supported media formats

These are the supported media formats in BytePlus Video Editor SDK:


|**Type** ||**Video** |**Image** |**Audio** |
|---|---|---|---|---|
|Input |* File Types<br><br>* Container Formats |* .mp4<br><br>* .mov |* .jpg<br><br>* .png<br><br>* .gif |* .mp3<br><br>* .aac<br><br>* .wav |
||Format |* H.264<br><br>* H.265 |N/A |N/A |
|Output |* File Types<br><br>* Container Formats |.mp4 |N/A |N/A |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to support other media formats in your project, reach out to the BytePlus Video Editor SDK team for more information.</div>


<span id="43f5cc8f"></span>
## SDK package sizes

These are the SDK packages offered in Video Editor SDK and their sizes:


|**SDK** |**Total Size** |**Class Size** |**arm64\-v8a** |**armeabi\-v7a** |
|---|---|---|---|---|
|EffectSDK |25.4 MB |140 KB |13.8 MB |11.5 MB |
|VESDK |21.2 MB |1.03 MB |10.6 MB |9.56 MB |
|NLESDK |2.69 MB |326 KB |1.32 MB |1.04 MB |
|Camera and editor |1.38 MB |845 KB |1.38 MB |1.38 MB |
|Total |50.67 MB |2.34 MB |27.1 MB |23.48 MB |


<span id="f3e7f46b"></span>
## Runtime Permissions

You have to request for the following permissions:


* Camera.

* Microphone.

* Photos and videos

* Music and audio.


For more information, refer to [Request runtime permissions](https://developer.android.com/training/permissions/requesting).

<span id="706d2e38"></span>
# Getting started with VE SDK—Android

The getting started guide for the VE SDK on Android offers developers a streamlined approach to integrating video editing capabilities. It includes a list of deliverables, sample code instructions, and guidance on running the provided sample code.

<span id="7b9e3b64"></span>
## Android SDK deliverables list

The following items are included in the Android SDK package:


* The BytePlus Video Editor SDK for Android demo source code.

* The license file.

* Editing resources.

* Built\-in resource icons.


<span id="1112a3d4"></span>
## Running the sample code

Get hands\-on with the BytePlus Video Editor SDK by downloading our sample project and running it in an Android environment. Dive into the SDK's functionality and explore seamless integration possibilities. You can proceed to run the sample code in your iOS project by following the steps below.

**To run the sample code in Android:** 


1. Download and decompress EffectOneSample.zip from the deliverables list.

2. Start Android Studio.

3. In Android Studio, select **File** \> **New** \> **Import Project**.

4. Navigate to the location where you extracted the project.

5. Select the project folder.

6. Click **OK** to import the project.


<span id="aefb9f99"></span>
# Integrating the SDK for Android

This integratio guide provides Android developers with a concise introduction to integrating the VE (Video Editor) SDK into their Android applications. It offers step\-by\-step instructions on setting up the necessary dependencies, initializing the VE SDK, and implementing video editing functionalities such as trimming, merging, applying filters, adding text overlays, and more. The Quickstart serves as a helpful reference for developers looking to enhance their Android applications with powerful video editing capabilities using the VE SDK.


1. Setting up the development environment.

2. Configuring the Maven repository.

3. Configuring dependencies.

4. Initializing the SDK.


<span id="877b19e7"></span>
## Step 1: Setting up development environment

Verify if your project complies with the recommended development environment for the BytePlus Video Editor SDK. For detailed information on the suggested development environment, refer [here](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#development-environment).

<span id="a54824c0"></span>
## Step 2: Configuring the Maven repository

Configure the Maven repository for your project setup.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you were to configure your Android project with the <code>settings.gradle.kts</code>file, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/docs-configuring-libraries-and-dependencies-using-gradle_1_1_0">Configuring repositories and dependencies using gradle</a> for more information.</div>


**To configure the Maven repository:** 


1. Create a Maven account if you're not on the internal network.

2. Add the Maven source to the `settings.gradle` file of your Android project.

   * **If you are on the external network, modify the** **`settings.gradle`file to look like this:** 

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This version of Video Editor SDK is 1.1.1.      </div>
      

      ```Kotlin
      dependencyResolutionManagement {
          ...
          repositories {
              ...
              maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
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
              //MAVEN_USER_NAME refers to the Maven username that you have obtained.
              //MAVEN_PASS_WORD refers to the password for the Maven username that you have obtained.
          }
      }
      ```
      


<span id="b61e2bed"></span>
## Step 3: Configuring dependencies

Configure dependencies for your project through the following steps:


1. Add the following dependencies to the `build.gradle` file in your project:

   ```JSON
   def effectOneVersion="1.1.1"
   dependencies {
       api "com.volcengine.effectone:editor-ui:${effectOneVersion}"
       api "com.volcengine.effectone:recorder-ui:${effectOneVersion}"
       //The resource loading SDK.
       api "com.volcengine.effectone:base-resource:${effectOneVersion}"
       //The three SDKs above share the same version. 
       implementation "com.github.bumptech.glide:glide:4.13.2"// The default dependency for photo(DefaultImageLoader), which can be added as needed.
       implementation "androidx.appcompat:appcompat:1.3.0" //Specify the desired version according to your hosted development environment. Suggested version: 1.3.0.
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.2" //Specify the desired version according to your hosted development environment. Suggested version: 1.5.2.
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.2" //Specify the desired version according to your hosted development environment. Suggested version: 1.5.2.
   }
   }
   ```
   

2. In the same file, complete the following steps:

   1. Add the following line to your`build.gradle` file.

      ```Kotlin
      android {
          ...
          defaultConfig {
              vectorDrawables.useSupportLibrary = true //Set the SDK to support vectorDrawable. This library can be used when you need to replace SVG photos with EffectOneSDK.
              applicationId = "com.volcengine.effectone" //Ensure the package name is consistent with the name of the authorized package. 
              ...
          }
          packagingOptions {
              jniLibs {
                  useLegacyPackaging = true
              }
              pickFirst 'lib/arm64-v8a/libc++_shared.so'
              pickFirst 'lib/armeabi-v7a/libc++_shared.so'
          }
          ...
      }
      ```
      

   2. Add the following line to your `gradle.properties` file to resolve building conflict:

      ```Kotlin
      android.useAndroidX=true
      android.enableJetifier=true 
      ```
      

3. Add the following line to your `AndroidManifest` file:

   ```Kotlin
   <application
       ...
       android:requestLegacyExternalStorage="true"
   >
   ```
   


For more information on `build.gradle.kts` integration, refer to [Configuring dependencies in app/build.gradle.kts file](https://docs.byteplus.com/docs/video-editor-sdk/docs-configuring-libraries-and-dependencies-using-gradle_1_1_0#4cb7c2f8).

<span id="b81e11eb"></span>
## Step 4: Initializing the SDK

The initialization process of the VE SDK includes several key features. Developers can import built\-in resources, licenses, configuration files, and icons to enhance their video editing capabilities. The SDK also provides the `EOQuickInitHelper` class for streamlined initialization. This comprehensive guide ensures a smooth start to utilizing the VE SDK's powerful video editing functionalities. For more information, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-resources-import-and-configuration_1_1_0).

The initialization process includes the following:


* Importing built\-in resources.

   * Importing a license.

   * Importing built\-in resources and configuration files.

   * Importing built\-in icons.

* Importing EOQuickInitHelper class.

* Initializing and launching the camera screen.

* Launching the editor screen separately.

* Launching the draft screen.

* Exporting a video.

   * Activity configuration.

   * Video export sample code.

   * Reusing the demo export screen.


<span id="a1bfc2fc"></span>
### Importing built\-in resources

You can import the following built\-in resources:


* License.

* Built\-in resources and configuration files.

* Built\-in icons.


<span id="ce452733"></span>
#### Importing a license

Decompress the license package `license.zip` retrieved from the deliverables list and place it under the `/app/src/main/assets/license/` directory of your Android project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8acdd1df924c46cf8f6ac68267a5d38e~tplv-goo7wpa0wc-image.image) </span>

<span id="19b5b114"></span>
#### Importing built\-in resources and configuration files

Unzip the built\-in material resources `EffectResource.zip` and place the contents in `{Host_Project}/src/main/assets/EffectResource/ directory`. The directory structure should be as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d0a91247336496cac231790f0d2d39c~tplv-goo7wpa0wc-image.image) </span>

<span id="c7b784be"></span>
#### Importing built\-in icons

Unzip the `Resource_icons.zip` file containing the built\-in icons from the delivery document. Move the contents of the icons folder to the `{Host_Project}/src/main/res/drawable-xxhdpi/` directory.

The directory structure of the `drawable-xxhdpi` folder in the main project is shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d52b07af577442da6f89ece3fb96c59~tplv-goo7wpa0wc-image.image) </span>

<span id="fac072cb"></span>
### Importing the EOQuickInitHelper class


1. Use the following code to create an `EOQuickInitHelper` class in your project. This class helps with the initialization of the BytePlus Video Editor SDK.

   ```Java
   //The QuickInit interface.
   interface IQuickInit {
       //The name of the license file must be the same as that of the licence file placed under the "assets/license" folder.
       var licenseFileName: String
       
       //Complete the initialization of EffectOneSDK and ResourceManager.
       fun initApplication(application: Application)  
       
       //Copy content within the assets file into your computer, complete authorization and initialize the EffectOneSDK.
       fun prepareAndInit(callback: (Boolean, String) -> Unit)
       
       /*efore launching the camera, you need to apply for permissions to use the camera and the auido recorder. The SDK supports applying for these permissions through FragmentActivity.
           If the host activity is not derived from FragmentActivity, after you apply for relevant permissions, you need to call EORecordActivity.startRecord(activity) to launch the camera page. */
       fun startRecorder(activity: FragmentActivity)
       
       /*Before launching the album, you need to apply for permissions to save photos to the album. The SDK supports applying for these permissions through FragmentActivity.
        If the host activity is not derived from FragmentActivity, after you apply for relevant permissions, you need to call EORecordActivity.startRecord(activity) to launch the camera page.*/
       fun startEditorFromAlbum(activity: FragmentActivity)
       
       //Launch the draft module.
       fun startDraft(activity: ComponentActivity)
   }
   class EOQuickInitHelper: IQuickInit {
       ...
   }
   ```
   

2. Download `EOQuickInitHelper.kt` to the host project and change the package name to match the host's package.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53eb0f3aec2a468bbd7a139b8f974b5f~tplv-goo7wpa0wc-image.image" name="EOQuickInitHelper.kt">EOQuickInitHelper.kt</Attachment>
   

&nbsp;

   For more information on the implementation details of the `EOQuickInitHelper.kt` class, refer to the following:

   * [Integrating VE SDK using Java](https://docs.byteplus.com/docs/video-editor-sdk/docs-integrating-ve-sdk-using-java_1_1_0).

   * [Integrating VE SDK using Jetpack Compose](https://docs.byteplus.com/docs/video-editor-sdk/docs-integrating-ve-sdk-using-jetpack-compose_1_1_0).

   * [Configuring repositories and dependencies using gradle](https://docs.byteplus.com/docs/video-editor-sdk/docs-configuring-libraries-and-dependencies-using-gradle_1_1_0).

3. Open the`EOQuickInitHelper.kt` file and replace the package name with your desired package name.

4. Add coroutine dependencies to the `build.gradle` file of the host module.

   ```Kotlin
   dependencies {
       ...
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.2" //Specify the desired version according to your hosted development environment. Suggested version: 1.5.2.
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.2" //Specify the desired version according to your hosted development environment. Suggested version: 1.5.2.
   }
   ```
   


<span id="1103eb43"></span>
### Initializing and launching the camera screen

To initialize built\-in resources and launch the camera screen, call the corresponding methods of `QuickInitHelper` in the host project. If no application is created in the project, you can create one yourself.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afc1a23105842da9c3d7d5219052dde~tplv-goo7wpa0wc-image.image) </span>

**Method definition**

```Kotlin
class SampleApplication: Application() {
    override fun onCreate() {
        super.onCreate()
        EOQuickInitHelper.licenseFileName = "com.volcengine.effectone.licbag" //Replace this with your own license name.
        EOQuickInitHelper.initApplication(this)
    }
}
```


**Sample code**

```Kotlin
class MainActivity : FragmentActivity() {
    private lateinit var startRecordBtn: View
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
        EOQuickInitHelper.prepareAndInit {
            startRecordBtn.setOnClickListener {
                EOQuickInitHelper.startRecorder(this)
            }
        }
        ...
    }
}
```


<span id="afe291b4"></span>
### Launching the editor screen separately

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e46f2f5f92894ffaaf3e8ac84cce81ea~tplv-goo7wpa0wc-image.image) </span>

You can launch the editor screen directly from the album after initialization.

```Kotlin
class MainActivity : FragmentActivity() {
    private lateinit var startEditorBtn: View
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
        EOQuickInitHelper.prepareAndInit {
            startEditorBtn.setOnClickListener { 
                EOQuickInitHelper.startEditorFromAlbum(this)
            }
        }
        ...
    }
}
```


<span id="e974fdbc"></span>
### Launching the draft screen

BytePlus Video Editor SDK allows you to save videos that are being edited into the draft box. You can call the following API to go to the draft box to preview or restore a video and continue to edit it.

```Kotlin
// Launch the draft screen.
EOQuickInitHelper.startDraft(activity)
```


<span id="bebd5939"></span>
### Exporting videos

You can use the following code samples to configure features related to video export.

<span id="1737852f"></span>
#### Export video activity configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e942d950cc7464db9d250f4c838774f~tplv-goo7wpa0wc-image.image) </span>

In BytePlus Video Editor SDK, the `action` field is used to configure the export screen.

**To configure the export screen:** 


1. Open the `AndroidManifest.xml` file of your host project.

2. Locate the `<activity>` tag where you want to configure the export screen.

3. Replace the existing `<activity>` tag with the provided sample code:

   ```JSON
   <activity
       android:name=".export.ExportActivity"
       android:exported="true"
       android:screenOrientation="portrait"
       android:theme="@style/Theme.EffectOne">
       <intent-filter>
          <action android:name="com.volcengine.effectone.Launch.EOExport" />
           <category android:name="android.intent.category.DEFAULT" />
       </intent-filter>
   </activity>
   ```
   

4. Save the `AndroidManifest.xml` file to apply the changes.

   By adding this code snippet, you have specified the `ExportActivity` as the Activity to be launched when the `com.volcengine.effectone.Launch.EOExport` action is triggered. Now, when you trigger the export action and navigate to the editor screen, tapping **Next** will launch the configured export screen, allowing you to customize the export process based on the video export information contained in the Intent object.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27183c2bc3824e7eb5aaceb26ad145ae~tplv-goo7wpa0wc-image.image) </span>


<span id="3913019b"></span>
#### Export activity configuration sample code

```Kotlin
class ExportActivity: FragmentActivity() {
    private lateinit var eoExportManager: EOExportManager
    private lateinit var exportActionView:View? = null
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        //>>>> step1 Initialize EOExportManager
        eoExportManager = EOExportManager.init(this@ExportActivity) { suc ->
            if (!suc) {
                requireActivity().finish()
            }
        }

        exportActionView?.setOnClickListener {
            runExportAction()
        }
    }

    private fun runExportAction() {
        val saveDir =
            Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DCIM).absolutePath
        val dateFormat = SimpleDateFormat("yyyyMMdd-HHmmss", getDefault())
        val exportFileName = "sample-${dateFormat.format(Date())}.mp4"
    
        val exportFilePath = "$saveDir${File.separator}$exportFileName"
        //>>>> step2 Export
        eoExportManager.exportVideo(
            outputPath = exportFilePath,
            outputSetting = EOOutputVideoSettings(),
            exportListener = EOExportDefaultListener()
        )
    }
}
```


<span id="d3d2a278"></span>
#### Reusing the VE export screen demo code sample

The sample code in the deliverables covers the features of the export screen, including video preview, cover image selection, and parameter settings. You can directly use the sample code and adjust the UI and features as needed.

**To reuse the UI:** 


1. Download and decompress the Sample Code file from the deliverables.

2. Create a module named `export` in Android Library (select the version and package name as needed).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5931ad5ce5a043e1aa1e0848c4b0f9f6~tplv-goo7wpa0wc-image.image) </span>

3. Reference the newly created module in the host project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20607b7b24e5461c94c3294d20edda83~tplv-goo7wpa0wc-image.image) </span>

4. Copy the `EffectOneSample-xxx/export/src` directory to the export module.

5. Add required dependencies to the export/build.gradle file.

   ```Kotlin
   def effectOneVersion="1.1.1"
   dependencies {
       ...
       implementation "com.geyifeng.immersionbar:immersionbar:3.2.2"
       implementation "com.geyifeng.immersionbar:immersionbar-ktx:3.2.2"
       implementation "com.volcengine.effectone:editor-ui:${effectOneVersion}"
       //glide dependencies
       implementation "com.github.bumptech.glide:glide:4.13.2"
       implementation "androidx.appcompat:appcompat:1.3.0"
       implementation "com.google.android.material:material:1.6.0"
       implementation "androidx.constraintlayout:constraintlayout:2.1.4"
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.7.0"
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.0"
       
   }
   ```
   

6. Replace the name of the activity in `export/AndroidManifest.xml` with the correct package name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9a7c76c6cf74c4b8258ea6dc6854555~tplv-goo7wpa0wc-image.image) </span>

7. As the export screen is pulled implicitly, you must configure the `action` and `category` fields in the `<activity>` tag of `AndroidManifest.xml`.

   ```Kotlin
       <activity
           android:name=".EffecONeExportActivty"
           android:exported="true"
           android:screenOrientation="portrait"
           <intent-filter>
               <action android:name="com.volcengine.effectone.Launch.EOExport" />
               <category android:name="android.intent.category.DEFAULT" />
           </intent-filter>
       </activity>
   ```
   

8. Run the project and resolve the unresolved reference R issues for the imported module based on the error message in the Android Studio build.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ad23def1fd94325899830513d605f68~tplv-goo7wpa0wc-image.image) </span>


For more information on export video UI configurations, refer to [Initializing EOExportManager](https://docs.byteplus.com/docs/video-editor-sdk/docs-initializing-EOExportManager_1_1_0) to get started.
