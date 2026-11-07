---
title: "Android SDK Quick Start Guide"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-android-sdk-quick-start-guide"
---

This integration guide provides Android developers with a concise introduction to integrating the BytePlus Video Editor (VE) SDK into their Android applications. It offers step\-by\-step instructions on setting up the necessary dependencies, initializing the VE SDK, and implementing video editing functionalities such as trimming, merging, applying filters, adding text overlays, and more. This Quick Start Guide serves as a helpful reference for developers looking to enhance their Android applications with powerful video editing capabilities using VE SDK.


1. Setting up the development environment.

2. Configuring the Maven repository.

3. Configuring dependencies.

4. Initializing the SDK.


<span id="baf0d703"></span>
## Step 1: Setting up development environment

Verify if your project complies with the recommended development environment for the BytePlus Video Editor SDK. For detailed information on the suggested development environment, refer to [Development environment](https://docs.byteplus.com/docs/video-editor-sdk/140-getting-started-with-android#13ddd4bf).

<span id="fe0a0f4a"></span>
## Step 2: Configuring the Maven repository

Configure the Maven repository for your project setup.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you were to configure your Android project with the <code>settings.gradle.kts</code>file, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-configuring-repositories-and-dependencies-using-gradle">Configuring repositories and dependencies using gradle</a> for more information.</div>


**To configure the Maven repository:** 


1. Create a Maven account if you're not on the internal network.

2. Add the Maven source to the `settings.gradle` file of your Android project.

   * **If you are on the external network, modify the** **`settings.gradle`file to look like this:** 

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This version of Video Editor SDK is 1.4.0+.      </div>
      

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
              // MAVEN_USER_NAME refers to the Maven username that you have obtained.
              //MAVEN_PASS_WORD refers to the password for the Maven username that you have obtained.
          }
      }
      ```
      


<span id="46263d88"></span>
## Step 3: Configuring dependencies

Configure dependencies for your project through the following steps:


1. Add the following dependencies to the `build.gradle` file in your project:

   ```JSON
   dependencies {
       api "com.volcengine.effectone:editor-ui:${effectOneVersion}"
       api "com.volcengine.effectone:recorder-ui:${effectOneVersion}"
       // Material loading SDK
       api "com.volcengine.effectone:base-resource:${effectOneVersion}"
       // The above three SDKs share the same version number
       implementation "com.github.bumptech.glide:glide:4.13.2" // Default image library dependency (DefaultImageLoader), optional
       implementation "androidx.appcompat:appcompat:1.3.0" // Choose the version based on the host environment, recommended 1.3.0
       // Add coroutine dependencies
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.2" // Choose the version based on the host environment, recommended 1.5.2
       implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.2" // Choose the version based on the host environment, recommended 1.5.2
   }
   ```
   

2. In the same file, complete the following steps:

   1. Add the following line to your`build.gradle` file.

      ```Kotlin
      android {
          ...
          defaultConfig {
              vectorDrawables.useSupportLibrary = true // Support vectorDrawable, used when you need to replace SVG images in Video Editor SDK
              applicationId = "com.volcengine.effectone" // Ensure the package name matches the authorized package name; the internal test authentication file uses this package name
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
   


For more information on `build.gradle.kts` integration, refer to [Configuring dependencies in app/build.gradle.kts file](https://docs.byteplus.com/docs/video-editor-sdk/140-configuring-repositories-and-dependencies-using-gradle#4cb7c2f8).

<span id="ad2101e9"></span>
## Step 4: Initializing the SDK

The initialization process of the VE SDK includes several key features. Developers can import built\-in resources, licenses, configuration files, and icons to enhance their video editing capabilities. The SDK also provides the `EOQuickInitHelper` class for streamlined initialization. This comprehensive guide ensures a smooth start to utilizing the VE SDK's powerful video editing functionalities. For more information, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/140-android-resources-import-and-configuration).

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


<span id="aa897d85"></span>
### Step 4.1: Importing built\-in resources

You can import the following built\-in resources:


* License.

* Built\-in resources and configuration files.

* Built\-in icons.


<span id="d1577a5d"></span>
#### Importing a license

Decompress the license package `license.zip` retrieved from the deliverables list and place it under the `/app/src/main/assets/license/` directory of your Android project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8acdd1df924c46cf8f6ac68267a5d38e~tplv-goo7wpa0wc-image.image) </span>

<span id="4c2593ad"></span>
#### Importing built\-in resources and configuration files

Unzip the built\-in material resources `EffectResource.zip` and place the contents in `{Host_Project}/src/main/assets/EffectResource/ directory`. The directory structure should be as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d0a91247336496cac231790f0d2d39c~tplv-goo7wpa0wc-image.image) </span>

<span id="1db65d84"></span>
#### Importing built\-in icons

Unzip the `Resource_icons.zip` file containing the built\-in icons from the delivery document. Move the contents of the icons folder to the `{Host_Project}/src/main/res/drawable-xxhdpi/` directory.

The directory structure of the `drawable-xxhdpi` folder in the main project is shown in the following figure:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d52b07af577442da6f89ece3fb96c59~tplv-goo7wpa0wc-image.image) </span>

<span id="afed1b44"></span>
### Step 4.2: Importing the EOQuickInitHelper class


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
       
       / *Before launching the album, you need to apply for permissions to save photos to the album. The SDK supports applying for these permissions through FragmentActivity.
        If the host activity is not derived from FragmentActivity, after you apply for relevant permissions, you need to call EORecordActivity.startRecord(activity) to launch the camera page.*/
       fun startEditorFromAlbum(activity: FragmentActivity)
       
       // Launch the draft module.
       fun startDraft(activity: ComponentActivity)
   }
   class EOQuickInitHelper: IQuickInit {
       ...
   }
   ```
   

2. Download `EOQuickInitHelper.kt` to the host project and change the package name to match the host's package.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/357a9a9fe94e430a81eea28592701064~tplv-goo7wpa0wc-image.image" name="EOQuickInitHelper.kt">EOQuickInitHelper.kt</Attachment>
   

3. Open the`EOQuickInitHelper.kt` file and replace the package name with your desired package name.

   For more information on the implementation details of the `EOQuickInitHelper.kt` class, refer to the following:

   * [Integrating VE SDK using Java](https://docs.byteplus.com/docs/video-editor-sdk/130-integrating-ve-sdk-using-java).

   * [Integrating VE SDK using Jetpack Compose](https://docs.byteplus.com/docs/video-editor-sdk/130-integrating-ve-sdk-using-jetpack-compose).

   * [Configuring repositories and dependencies using gradle](https://docs.byteplus.com/docs/video-editor-sdk/130-configuring-repositories-and-dependencies-using-gradle).


<span id="633a2ad8"></span>
### Step 4.3: Initializing and launching the camera screen

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


<span id="045fdc49"></span>
### Step 4.4: Launching the editor screen separately

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


<span id="c13ed3e4"></span>
### Step 4.5: Launching the draft screen

BytePlus Video Editor SDK allows you to save videos that are being edited into the draft box. You can call the following API to go to the draft box to preview or restore a video and continue to edit it.

```Kotlin
//  Launch the draft screen.
EOQuickInitHelper.startDraft(activity)
```


<span id="30003b8e"></span>
### Step 4.6: Exporting videos

You can use the following code samples to configure features related to video export.

<span id="4e252961"></span>
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


<span id="cfced406"></span>
#### Export activity configuration sample code

```Kotlin
class ExportActivity: FragmentActivity() {
    private lateinit var eoExportManager: EOExportManager
    private lateinit var exportActionView:View? = null
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        //>>>> step 1: Initialize EOExportManager
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
        //>>>> step 2: Export
        eoExportManager.exportVideo(
            outputPath = exportFilePath,
            outputSetting = EOOutputVideoSettings(),
            exportListener = EOExportDefaultListener()
        )
    }
} 
```


<span id="9eb10be1"></span>
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


For more information on export video UI configurations, refer to [Initializing EOExportManager](https://docs.byteplus.com/docs/video-editor-sdk/140-initializing-eoexportmanager) to get started.
