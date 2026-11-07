---
title: "Android Sample SDK Deliverables List"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-android-sample-sdk-deliverables-list"
---

The directory structure of sample code files is as follows:

```Java
-EffectOneSample
---version.gradle
---settings.gradle
---gradlew.bat  
---gradlew 
---gradle.properties
---gradle
---export
---business
---build.gradle
---app-custom-style
---app
```


<span id="a7ca8ad6"></span>
## Editing resources

To retrieve editing resources, reach out to the BytePlus Video Editor SDK team.

<span id="810199ca"></span>
## Built\-in resource icons

To retrieve built\-in resource icons, reach out to the BytePlus Video Editor SDK team.

<span id="469a3d84"></span>
## Sample code introduction

The app, business, and export modules are included in the sample code files. Detailed descriptions of these modules are listed as follows:

<span id="75c99a2a"></span>
### App module

The app module is the shell project. You can initialize EffectOneSDK in `EffectOneApp` by using the following code.

```Kotlin
class EffectOneApp : Application() {
    override fun onCreate() {
        super.onCreate()
        EOQuickInitHelper.licenseFileName = "com.volcengine.effectone.licbag"
        EOQuickInitHelper.initApplication(this)
        EffectOneExportActivity.copyWaterMark(this)
    }
} 
```


<span id="b84394e7"></span>
### Business module

The business module is the main project to call functional modules such as the camera and draft. Its core code is encapsulated in `EOQuickInitHelper`. For more information about API implementation, refer to EffectOneSDK features.

The `EOQuickInitHelper` class looks like this:

```Kotlin
interface IQuickInit {
    //The name of the license file must be the same as that of the license file placed under the assets/license folder. 
    var licenseFileName: String
    
    //Complete the initialization of EffectOneSDK and ResourceManager.
    fun initApplication(application: Application)  
    
    //Copy content within the assets file into your computer, complete authorization and initialize the EffectOneSDK.
    fun prepareAndInit(activity: ComponentActivity, callback: (result: Boolean)-> Unit) 
    
    /*Before launching the camera, you need to apply for permissions to use the camera and auido recorder. The SDK supports applying for these permissions through FragmentActivity.
        If the host activity is not derived from FragmentActivity, after you apply for relevant permissions, you need to call EORecordActivity.startRecord(activity). For more information, refer here.*/
    fun startRecorder(activity: FragmentActivity)
    
    /*Before launching the album, you need to apply for permissions to save photos to the album. The SDK supports applying for these permissions through FragmentActivity.
     If the host activity is not derived from FragmentActivity, after you apply for relevant permissions, you need to call EORecordActivity.startRecord(activity). For more information, refer here.*/
    fun startEditorFromAlbum(activity: FragmentActivity)
    
    //Launch the draft page.
    fun startDraft(activity: ComponentActivity)
}
class EOQuickInitHelper: IQuickInit {
    ...
}
```


In `EffectOneMainFragment`, use `EOQuickInitHelper` to copy resources in assets to the file system, complete the authentication, and initialize all levels of panels. Then, bind an event to launch the camera or draft page.

```Kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    if (!VersionHelper.envIsReady()) {
        EOQuickInitHelper.prepareAndInit(requireActivity()) {
            VersionHelper.setVersion()
        }
    }
}

override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    view.findViewById<TextView>(R.id.main_version_view).apply {
        text = "${requireContext().getString(R.string.eo_frontpage_version)}:${getVersionName()}"
    }
    view.findViewById<View>(R.id.main_title).setOnLongClickListener {
        try {
            startActivity(Intent("effect_one_inside_page").apply {
                setPackage(AppSingleton.instance.packageName)
            })
        } catch (e: ActivityNotFoundException) {
            e.printStackTrace()
        }
        return@setOnLongClickListener true
    }

    view.findViewById<View>(R.id.main_editor).setOnClickListener {
        VersionHelper.checkEnv {
            EOQuickInitHelper.startRecorder(requireActivity())
        }
    }

    view.findViewById<View>(R.id.main_templates).setOnClickListener {
        EOToaster.show(requireActivity(), R.string.eo_frontpage_magictemplates_toast)
    }

    view.findViewById<View>(R.id.main_draft).setOnClickListener {
        VersionHelper.checkEnv {
            EOQuickInitHelper.startDraft(requireActivity())
        }
    }
}
```


<span id="2793b5f1"></span>
### Export module

In addition to video export, the export module in BytePlus Video Editor SDK also provides features such as frame extraction, preview, and settings, facilitating the customization of the export page. For more information, see `*EffectOneExportFragment*` in the sample code.

&nbsp;
