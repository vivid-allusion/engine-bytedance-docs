---
title: "Integrating VE SDK using DFM"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-integrating-ve-sdk-using-dfm"
---

Integrating the Video Editor SDK into an Android application using Google Play's Dynamic Feature Module (DFM) allows for reduced initial app download sizes, enhancing user experience, especially for overseas customers. This approach enables specific features, such as the Video Editor, to be downloaded on\-demand rather than as part of the initial app installation.

For more information on Dynamic Feature Modules, refer [here](https://developer.android.com/guide/playcore/feature-delivery/on-demand?hl=zh-cn).

The previous method of integrating the Video Editor SDK as a whole into the Android app led to UI conflicts due to dependencies on UI layers like materials. The new technical solution involves integrating the business layer normally and then excluding dependencies on the underlying libraries.

The size of the Video Editor package is primarily derived from two main components:


* **Underlying dependencies**: Can be integrated using the Dynamic Feature Module (DFM) approach.

   ```Groovy
   exclude group: 'com.bytedance', module: 'effectsdk' 
   exclude group: 'com.bytedance.ugc.framework.libs', module: 'vesdk'
   exclude group: 'com.volcengine.ck.nle', module:'NLEMediaPublic'
   exclude group: 'com.volcengine.ck.nle', module:'NLEEditor'
   exclude group: 'com.volcengine.ck.nle', module:'NLETemplateModel'
   ```
   

   After building the Android App Bundle (AAB), the contents of the package typically include the following:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db57294b22374c799bd5bf700826a172~tplv-goo7wpa0wc-image.image) </span>

* **Assets materials and res icons**: Can be configured for network distribution. For more information, refer to [Android sample SDK deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-android-sample-sdk-deliverables-list).


<span id="565d9849"></span>
# Step 1: Integrate Video Editor SDK into the base modules

Integrate the Video Editor SDK into your base module. For more information on the steps, refer to [Android SDK Quick Start Guide](https://docs.byteplus.com/docs/video-editor-sdk/120-android-sdk-quick-start-guide).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Subsequent integration steps and sample code snippets are aligned with Video Editor version 1.2.0 and later. For integrating with newer versions, refer the documentation specific to those versions.</div>


<span id="4a088dc4"></span>
# Step 2: Removing underlying dependencies from the base module.

```Groovy
// Basic edit  
api("com.volcengine.effectone:editor-ui:${EO_SDK_VERSION}") {
    exclude group: 'com.bytedance', module: 'effectsdk'
    exclude group: 'com.bytedance.ugc.framework.libs', module: 'vesdk'
    exclude group: 'com.volcengine.ck.nle', module:'NLEMediaPublic'
    exclude group: 'com.volcengine.ck.nle', module:'NLEEditor'
    exclude group: 'com.volcengine.ck.nle', module:'NLETemplateModel'
}
// Record
api ("com.volcengine.effectone:recorder-ui:${EO_SDK_VERSION}") {
    exclude group: 'com.bytedance', module: 'effectsdk'
    exclude group: 'com.bytedance.ugc.framework.libs', module: 'vesdk'
    exclude group: 'com.volcengine.ck.nle', module:'NLEMediaPublic'
    exclude group: 'com.volcengine.ck.nle', module:'NLEEditor'
    exclude group: 'com.volcengine.ck.nle', module:'NLETemplateModel'
}
// Resourse SDK
api ("com.volcengine.effectone:base-resource:${EO_SDK_VERSION}") {
    exclude group: 'com.bytedance', module: 'effectsdk'
    exclude group: 'com.bytedance.ugc.framework.libs', module: 'vesdk'
    exclude group: 'com.volcengine.ck.nle', module:'NLEMediaPublic'
    exclude group: 'com.volcengine.ck.nle', module:'NLEEditor'
    exclude group: 'com.volcengine.ck.nle', module:'NLETemplateModel'
}
// Indenpendent on export
// api project(":export")
```


<span id="4c7c59ac"></span>
# Step 3: Creating DFMs


1. Navigate to Android Studio.

2. Click **File** \> **New** \> **New Module**.

3. Click **Dynamic Feature**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/765648d6874d444c8c01e138529e76e8~tplv-goo7wpa0wc-image.image) </span>

4. Enter the relevant DFM information including the **Base Application Module**, **Module name**, and so on.

5. Click **Finish**.

   The DFM is created.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60ce7a6b427a458d9fc2e5419c844a05~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to make adjustments or want to customize the configurations for your DFMs. If adjustments are needed, refer <a href="https://developer.android.com/guide/playcore/feature-delivery/on-demand?hl=zh-cn">here</a>.   </div>
   

<span id="0e65fe89"></span>
# Step 4: Adding DFM dependencies

In the DFM's `build.gradle`file, add the following dependencies:

```SQL
dependencies {  
    implementation project(":app") 
    implementation 'com.google.android.play:feature-delivery-ktx:2.1.0'
    implementation("com.bytedance.ugc.framework.libs:vesdk:${versions["vesdk"]}")
    implementation("com.bytedance:effectsdk:${versions["effectsdk"]}")

    implementation "com.volcengine.ck.nle:NLEMediaPublic:${versions["nle_version"]}"
    implementation "com.volcengine.ck.nle:NLEEditor:${versions["nle_version"]}"
    implementation "com.volcengine.ck.nle:NLETemplateModel:${versions["nle_version"]}"
}
```


<span id="e367e1f3"></span>
# Step 5: Adding export features to DFM

The following is an example of adding export features to DFM. For a full list of the export capabilities, refer to [Export function APIs](https://docs.byteplus.com/docs/video-editor-sdk/150-export-function-apis). In the `AndroidManifest.xml` file, you configure the export activity by defining an intent filter that includes the action `com.volcengine.effectone.Launch.EOExport`. This setup allows the system to recognize when to launch the export activity as part of the DFM (Dynamic Feature Module) functionality.

**To add export features to DFM:** 


1. Navigate to `AndroidManifest`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddec0151e5f244958c215ea4e4d0113c~tplv-goo7wpa0wc-image.image) </span>

2. In `AndroidManifest`，add the export activity `<action*android:name*="com.volcengine.effectone.Launch.EOExport" />`.

   ```XML
   <manifest xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:dist="http://schemas.android.com/apk/distribution">
   
       <dist:module
           dist:instant="false"
           dist:title="@string/title_dynamicfeature">
           <dist:delivery>
               <dist:on-demand />
           </dist:delivery>
           <dist:fusing dist:include="true" />
       </dist:module>
       <application
           android:maxAspectRatio="2.4"
           android:extractNativeLibs="true">
           <activity
               android:name=".ExportActivity"
               android:exported="true"
               android:screenOrientation="portrait"
               android:theme="@style/Theme.EffectOne">
               <intent-filter>
                   <action android:name="com.volcengine.effectone.Launch.EOExport" />
                   <category android:name="android.intent.category.DEFAULT" />
               </intent-filter>
           </activity>
       </application>
   </manifest>
   ```
   

3. Define the `ExportActivity` class, which extends `AppCompatActivity`. This activity will handle the user interface and the export process.

   ```Kotlin
   class ExportActivity: AppCompatActivity() {
       private var eoExportManager: EOExportManager? = null
        
       override fun attachBaseContext(newBase: Context?) {
           super.attachBaseContext(newBase)
           SplitCompat.installActivity(this)
       }
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.dynamic_export)
           eoExportManager = EOExportManager.init(this, null) {
               LogKit.i("ExportActivity", "export result $it")
           }
           findViewById<View>(R.id.export)?.apply {
               setOnClickListener {
                   doExport()
               }
           }
       }
   
       private fun doExport() {
   
           val dateFormat = SimpleDateFormat("yyyyMMdd-HHmmss", Locale.getDefault())
           val exportFileName = "eo-${dateFormat.format(Date())}.mp4"
           val dir =
               "${Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_MOVIES)}${File.separator}${
                   AppSingleton.instance.applicationInfo.loadLabel(AppSingleton.instance.packageManager)
               }"
           val savePath = File(dir, exportFileName)
           eoExportManager?.exportVideo(outputPath = savePath.absolutePath,
               outputSetting = EOOutputVideoSettings().apply {
   
                   // For low-end devices or models that fail to export, enable the soft decoding method by default.
   
                   useSoftwareDecode = true
                   //Hard-coded, enabled by default.
                   useHWEncoder = true
   
               },
               exportListener = EOExportListener()
           )
       }
   }
   ```
   

4. Create an `EOExportListener` class to handle the events and results of the export process.

   ```Kotlin
   
   open class EOExportListener(  
   //    private var eoRootUIViewModel: EffectOneExportRootUIViewModel
   ) : EOExportDefaultListener() {
   
       override fun onDone(outputPath: String) {
           LogKit.d(TAG, "onCompileDone() outputPath  $outputPath")
   //        eoRootUIViewModel.exportActionState.postValue(ExportActionState.SUCCESS)
       }
   
       override fun onError(error: Int, msg: String?, ) {
           LogKit.d(TAG, "onCompileError() called with: error = $error, msg = $msg")
   //        eoRootUIViewModel.exportActionState.postValue(ExportActionState.FAIlED(error, msg))
       }
   
       override fun onProgress(progress: Float) {
           LogKit.d(TAG, "onCompileProgress() : progress = ${progress.times(100).roundToInt()}")
   //        eoRootUIViewModel.exportActionState.postValue(ExportActionState.LOADING(progress.times(100).roundToInt()))
       }
   
   }
   ```
   


<span id="e0319b32"></span>
# Step 6: Integrating and loading native libraries

After a Dynamic Feature Module (DFM) is installed, it may depend on native libraries (.so files) for additional functionality. Proper integration and loading of these libraries are crucial for the seamless operation of the DFM.


1. Once the DFM module is installed, ensure that all required native libraries are correctly referenced and loaded into the application.

2. Utilize the `SplitInstallManager` to handle the installation and management of DFMs. Refer to the [official Google documentation](https://developer.android.com/guide/playcore/feature-delivery/on-demand?hl=zh-cn) for detailed usage instructions.

3. Verify that the Application class is extended from `SplitCompatApplication`, which is necessary for handling split installations.

4. Implement a listener within the `SplitInstallManager` to monitor the installation status of the DFM.

   ```Kotlin
   class EffectOneApp : SplitCompatApplication()  
   ```
   

5. List all required native libraries (.so files) and load them using `SplitInstallHelper.loadLibrary` after the DFM is installed.

6. Provide logic to handle different states such as `INSTALLED`, `DOWNLOADING`, and potentially others, to ensure the application responds appropriately.


**Full sample code:** 

```Kotlin
splitInstallManager.registerListener { 
 
            Log.i("MainActivity", "split id is: ${it.sessionId()}")
            val status = it.status()
            when(status) {

                SplitInstallSessionStatus.INSTALLED -> {

                    Log.e("MainActivity", "split INSTALLED")
                    if (BuildCompat.isAtLeastO()) {
                        // Updates the app’s context with the code and resources of the
                        // installed module.
                        SplitInstallHelper.updateAppInfo(this)

                        val soList = listOf("c++_shared",
                            "bytevc0",
                            "ByteVC1_dec",
                            "ttcrypto",
                            "ttboringssl",
                            "ttffmpeg",
                            "yuv",
                            "bdaudioeffect",
                            "gaia_lib",
                            "AGFX",
                            "effect",
                            "ttvesdk",
                            "NLEEditorJni")
                        soList.forEach {
                            LogKit.e(TAG, "native load lib : $it", null)
                            SplitInstallHelper.loadLibrary(this@SplashActivity, it)
                        }
                        postOnUiThread {
                            Log.i(TAG, "installed moudles ${splitInstallManager.installedModules.first()}")
                            startActivity(Intent()
                                .setClass(this, EffectOneMainActivity::class.java)
//                                .setClassName("com.volcengine.effectone", "com.example.dynamicfeature.EffectOneMainActivity")
                            )

                        }
                    }


                }
                SplitInstallSessionStatus.DOWNLOADING -> {
                    Log.e("MainActivity", "split DOWNLOADING")
                }
            }
        }
```


&nbsp;
