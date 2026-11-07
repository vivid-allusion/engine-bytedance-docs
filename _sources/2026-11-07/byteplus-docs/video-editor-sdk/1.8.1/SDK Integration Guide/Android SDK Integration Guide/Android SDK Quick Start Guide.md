---
title: "Android SDK Quick Start Guide"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/181AndroidSDKQuickStartGuide"
---

1. ## Configure the compilation environment <span id="Cr8lzUDu"></span>


The following is the recommended environment configuration for BytePlus Video Editor SDK. Please check if it is met in your own project. 

```Kotlin
Gradle: 7.5.1
Android Gradle Plugin: 7.3.1
kotlin: 1.5.30
minSdk: 21
targetSdk: 33
compileSdk: 33
Java Version: 11
```



2. ## Dependency Configuration  <span id="CYlkQx6v"></span>


If you use the gradle.kts file to configure an Android project, refer to [EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f) 6\-2 

Please contact our sales to apply for the account and password of the Maven repository


* Add our maven repository to the settings.gradle of the host project


```C++
dependencyResolutionManagement {    ...
    repositories {        ...
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }        maven {            url "https://artifact.bytedance.com/repository/thrall_ck/"
            credentials {                username = MAVEN_USER_NAME
                password = MAVEN_PASS_WORD
            }            authentication {                digest(BasicAuthentication)
            }        }
        //MAVEN_USER_NAME applied maven account user name
        //MAVEN_PASS_WORD applied maven account password
    }}
```



&nbsp;

   * If you use settings.gradle.kts to integrate, you can refer to[EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f)

* Add SDK dependencies to the build.gradle of your project

   * Version Number:effectOneVersion: 1.8.1


```C++
dependencies {
    api "com.volcengine.effectone:editor-ui:${effectOneVersion}"
    api "com.volcengine.effectone:recorder-ui:${effectOneVersion}"
    //resource loading SDK
    api "com.volcengine.effectone:base-resource:${effectOneVersion}"
    //The above three SDKs share the same version number
    implementation "com.github.bumptech.glide:glide:4.13.2"// DefaultImageLoader), Optional
    implementation "androidx.appcompat:appcompat:1.3.0" //Choose the version according to your project's environment, and 1.3.0 is recommended.
    //Add coroutine dependencies
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.2" //Choose the version according to your project's environment, and 1.5.2 is recommended.
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.2" //Choose the version according to your project's environment, and 1.5.2 is recommended.
}
```



* Other Configurations

   * Add below code to the build.gradle of your project


```Kotlin
android {
    ...
    defaultConfig {
        vectorDrawables.useSupportLibrary = true //Supports VectorDrawable, used when you need to replace the SVG image in Video Editor
        applicationId = "com.volcengine.effectone" //Ensure that the applicationId is consistent with the authorized applicationId, and "com.volcengine.effectone" is used for the demo only.
        ...
    }
    packagingOptions {    jniLibs {        useLegacyPackaging = true    }    pickFirst 'lib/arm64-v8a/libc++_shared.so'
        pickFirst 'lib/armeabi-v7a/libc++_shared.so'
    }
    ...
}
```



   * Add below code to gradle.properties to resolve build conflicts


```Kotlin
android.useAndroidX=true
```



   * Add below code to the AndroidManifest of your project


```Kotlin
<application
    ...
    android:requestLegacyExternalStorage="true"
>
```



   * Add below code to the build.gradle of the project


```Plain Text
/**
 * force dependencies in version.gradle
 * it's     important to force 「effectsdk version」「vesdk version」「nle version」
 * UserGuide: https://docs.gradle.org/current/userguide/dependency_downgrade_and_exclude.html
 */
def hasLibs = rootProject.ext.properties.containsKey("libs")
rootProject.allprojects {    configurations.configureEach {        resolutionStrategy { strategy ->            if (hasLibs) {
                ((Map<String, ?>) rootProject.ext.libs).keySet().each { key ->                    strategy.force rootProject.ext.libs[key]
                }            }
        }    }}
```


 If you are using build.gradle.kts for integration, please refer to [EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f)


3. ## Video Editor SDK Quick Initialization <span id="1GWekqNQ"></span>


The following describes the method of quickly integrating Video Editor SDK using the Kotlin language and Android's native FragmentActivity, with built\-in authorization/resource files. For integration with other languages and frameworks, please refer to  [ other integration methods ](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f#doxcnreMKiiopLuCcJro5byZDeh).  For other integration methods of authorization and resource management,  please refer to [EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f)


1. ### Import built\-in resourcees  <span id="gbJwkuV6"></span>

1. #### Import authentication file <span id="slvaFhDm"></span>


Unzip the authentication file\-\-lisence.zip from the delivery documents and place it in your project/app/src/main/assets/License/ directory 

<div style="text-align: center">
<img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a1e0e3a5a1d86e1f1d42d9fc919ffa58.png" width="1154px" /></div>



2. #### Import built\-in resources, configurations, and icons  <span id="zwtY8OIe"></span>


Unzip the built\-in resource\-\-EffectResource.zip from the delivery document, and place the contents under the EOResource file into {your project}/src/main/assets/EffectResource/. The directory structure is as follows: 

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_02e6b40c5dfa62573570e361b357152d.png) </span>


2. ### Import EOQuickInitHelper <span id="0A88WVet"></span>

* Provide an EOQuickInitHelper class to assist integrators in quickly completing the initialization of Video Editor SDK


```Java
//QuickInit API
interface IQuickInit {
    //complete initialization of Video Editor SDK and ResourceManager
    fun initApplication(application: Application)
    //Complete authentication and configuration initialization
    fun prepareAndInit(callback: (Boolean, String) -> Unit)
    
    //Complete shooting, editing resource configuration
    fun initConfigs()
    
    //Other extended resource configurations
    fun extendResourceConfig()
    
    /*Starting the camera requires applying for camera and recording permissions. The SDK supports permission application through FragmentActivity. 
      If the host Activity does not inherit from FragmentActivity, you need to apply for the permissions yourself first, 
      and then call EORecordActivity.startRecord(activity). For reference, see the section on starting the shooting page.*/
    fun startRecorder(activity: FragmentActivity)
    
    //Starting a duet requires applying for camera, recording, and storage permissions, and the SDK supports applications through FragmentActivity.
    fun startDuet(activity: FragmentActivity)
    
    //Start the draft page
    fun startDraft(activity: ComponentActivity)
    
    /*Starting the album requires applying for storage permissions, and the SDK supports permission application through FragmentActivity. 
      If the host Activity does not inherit from FragmentActivity, you need to apply for the permissions yourself first, 
      and then call EORecordActivity.startRecord(activity). For reference, see the section on starting the shooting page.*/
    fun startEditorFromAlbum(activity: FragmentActivity)
    
    //Starting the "Cut the Same" function requires applying for storage permissions, and the SDK supports permission application through FragmentActivity.
    fun startCutSame(activity: FragmentActivity)
    
    //Starting the highlight moment requires applying for storage permission, and the SDK supports applications through FragmentActivity.
    fun startHLM(activity: FragmentActivity)
    
    //Starting the Moment Album requires applying for storage permission, and the SDK supports applications through FragmentActivity.
    fun startMoment(activity: FragmentActivity)
}
class EOQuickInitHelper: IQuickInit {
    ...
}
```


&nbsp;

<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ee2cf200acb4654df42cb86feca6cded.kt" name="EOQuickInitHelper.kt">EOQuickInitHelper.kt</Attachment>



&nbsp;

* Download EOQuickInitHelper.kt to your project, and modify the applicationId to the corresponding applicationId of your project

* For the implementation of each step within EOQuickInitHelper, please refer to the document[EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f)



&nbsp;

3. ### Initialize and start the shooting page <span id="AyHPmF17"></span>


***~~<ins>Image to be uploaded here</ins>~~***

Calling the corresponding method of QuickInitHelper in the host project can complete the initialization of the Video Editor SDK (built\-in resources) and start the shooting page. 

```Kotlin
class SampleApplication: Application() {
    override fun onCreate() {
        super.onCreate()
        EOQuickInitHelper.licenseFileName = "com.volcengine.effectone.licbag" //替换成自己的liscence名
        EOQuickInitHelper.initApplication(this)
    }
}
```


Initialize and start shooting

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



&nbsp;

4. ### Launch the editing page separately <span id="JidpJfY3"></span>


You can also directly launch the editing page from the photo album after the initialization is completed.

&nbsp;

Launch the editing page from the photo album

```Kotlin
class MainActivity : FragmentActivity() {
    private lateinit var startEditorBtn: View
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
        EOQuickInitHelper.prepareAndInit {
            startEditorBtn.setOnClickListener {     EOQuickInitHelper.startEditorFromAlbum(this)
            }
        }
        ...
    }
}
```



5. ### Draft  <span id="b765dKAs"></span>


Video Editor supports saving the video being edited as a draft, and you can jump to the draft page via the following interface to preview the draft or restore the video editing state from the draft

```Kotlin
//start the draft page
EOQuickInitHelper.startDraft(activity)
```



6. ### Export Video <span id="0AtvdR0K"></span>

1. #### Export Activity Configuration <span id="7rtZQF5u"></span>


Video Editor configures the export page through an action. In the host's AndroidManifest.xml, select an Activity and configure the action as "com.volcengine.effectone.Launch.EOExport".

After clicking Next on the preview editing page, it will jump to this page, and the video export information will be carried in the Intent.<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_90a1ff8ed77fc45d7a0e0541de2f2519.png) </span>

&nbsp;

```Kotlin
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



2. #### Sample code for exporting video Activity is as follows: <span id="UKJrP6sL"></span>


```Kotlin
class ExportActivity: FragmentActivity() {
    private lateinit var eoExportManager: EOExportManager
    private lateinit var exportActionView:View? = null
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        //>>>> step1 初始化EOExportManager
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
        //>>>> step2 导出
        eoExportManager.exportVideo(
            outputPath = exportFilePath,
            outputSetting = EOOutputVideoSettings(),
            exportListener = EOExportDefaultListener()
        )
    }
}
```



&nbsp;

3. #### Reuse the export page of Video Editor Demo <span id="cFnpNFZM"></span>

* **UI Reuse**


The SampleCode in the delivery document provides an export page that includes functions such as video preview, cover selection, and export parameter configuration. You can directly use it in its entirety as source code and adjust the UI and functionality according to requirements. 

***~~<ins>Image to be uploaded here</ins>~~***

&nbsp;

The steps are as follows: 


* Download and unzip the SampleCode source code from the delivery document

* Create a new Android library module: export in the host project<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b5e99e29977541f066f88337e9607e30.png) </span>

* Reference the newly created module in the host project<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a32812a78d586aa85469700fc3866c99.png) </span>

* Copy the EffectOneSample\-xxx/export/src directory to the export module directory

* Add the required dependencies in export/build.gradle


```Kotlin

dependencies {
    ...
    implementation "com.geyifeng.immersionbar:immersionbar:3.2.2"
    implementation "com.geyifeng.immersionbar:immersionbar-ktx:3.2.2"
    implementation "com.volcengine.effectone:editor-ui:${effectOneVersion}"
    //glide 依赖    implementation "com.github.bumptech.glide:glide:4.13.2"
    implementation "androidx.appcompat:appcompat:1.3.0"
    implementation "com.google.android.material:material:1.6.0"
    implementation "androidx.constraintlayout:constraintlayout:2.1.4"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.7.0"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.0"
    
}
```



* Change the activity in export/AndroidManifest.xml to the correct package name<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_44911af0876ef0fa71af1430dcf6a915.png) </span>

* The export page is launched through an implicit method, where action and category are configured in the Activity of the business itself in the AndroidManifest.xml file 


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



* Run the project, and fix some package name errors in the R files of the imported module according to the error messages in Android Studio Build


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_611cbd82fa87a0f89d369593f51e11d9.png) </span>


4. #### Interface Details <span id="CiAAao6H"></span>


You can also use EOExportManager to develop your own export page, the detailed interface documentation is as follows:[EffectOne-Android 视频导出接口介绍](https://bytedance.larkoffice.com/docx/A3ogdjxYkoREIdx6S8ScZc3wnTb)


&nbsp;

4. ## EffectOne Advanced Features <span id="xVbxkryN"></span>


By now, you have completed the Quick Start of Video Editor SDK and can find the video you just exported in the photo album! If you want to further understand some advanced features of Video Editor,  please refer to [EffectOne Android 功能详解](https://bytedance.larkoffice.com/docx/Mfl3dOTcqoP4kAxf6BOcCjMLn5f)
