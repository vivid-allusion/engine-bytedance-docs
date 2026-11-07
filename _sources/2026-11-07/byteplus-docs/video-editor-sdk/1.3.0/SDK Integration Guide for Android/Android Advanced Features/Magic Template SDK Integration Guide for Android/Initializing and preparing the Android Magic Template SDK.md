---
title: "Initializing and preparing the Android Magic Template SDK"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-initializing-and-preparing-the-android-magic-template-sdk"
---

<span id="2550230b"></span>
# Step 1: Initializing the a**uthorization** configuration

Set up the authority configuration related to SDK .

<span id="b3af51e8"></span>
#### Sample code


* Place the offline authorization file in the directory of the host project's `app/src/main/assets/License/`.

* Copy the offline authorization file to the App's private directory.


```Kotlin
//According to the filename, copy the offline authorization file to the App's private directory
val licenseFileName = "com.volcengine.effectone.licbag"
val licenseFile = File(EOUtils.pathUtil.internalLicense(), licenseFileName)
if (!licenseFile.exists()) {
    EOUtils.fileUtil.copyAssetFile("license/${licenseFileName}", licenseFile.absolutePath)
}
```



* Initializing authorization configuration.


```Kotlin
val authConfig = EOAuthConfig()
authConfig.offlineLicensePath = "Local Path of authorization File"
val result = EOAuthorization.makeAuthWithConfig(authConfig)
if (result.resCode != EOAuthErrCode.EO_AUTH_SUCCESS) {
    // Authorization failed
} else {
    // Authorization successful
}

// cutSameLicensePath refers to the path of valid files authorized by Magic Template
val cutSameLicensePath = EOAuthorizationInternal.getCutSameLicensePath()
```


<span id="de47327c"></span>
# Step 2: Initializing SDK

After successful authorization initialization, proceed to initialize the configuration related to the Magic Template SDK.

<span id="cfe0a19f"></span>
#### Sample code

```Kotlin
EffectOneConfigList.configure(CutSameUIConfig()) {
    //The Magic Template can be built-in or downloaded by configuring either the `OnlineResourceLoader` or `OfflineResourceLoader`
    it.resourceLoader = OnlineResourceLoader.instance
}
CutSameInit.init()
```


<span id="4f287f92"></span>
# Step 3: Retriving template list

Get the Magic Template list for display and to build TemplateItem for template parsing.

<span id="b783b86d"></span>
#### Sample code

```Kotlin
//Get the configured `CutSameUIConfig`
private val cutsameConfig: CutSameUIConfig? by lazy {
    InnerEffectOneConfigList.getConfig()
}

//Get the template list
val data = withContext(Dispatchers.IO) {
    val key = EOResourcePanelKey.CUTSAME_TEMPLATES.value
    cutsameConfig?.resourceLoader?.loadResourceList(key, key) ?: emptyList()
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/130-android-resources-import-and-configuration">Android resources import and configuration</a> to check how to manage Magic Template materials using the material SDK.</div>


<span id="0b920aa7"></span>
# Step 4: Retrieving TemplateItem

According to the path of the template package, build a `TemplateItem` for template replay.

<span id="741a49c7"></span>
#### API definition

```Kotlin
data class TemplateItem(
    @SerializedName("title") val title: String = "",
    @SerializedName("fragment_count") val fragmentCount: Int = 0,
    @SerializedName("md5") val md5: String = "",
    @SerializedName("zip_path") var zipPath: String = "", //The local path of the zip file, used for offline template
    @SerializedName("unzip_path") var unZipPath: String = "", //The local path of the unzipped file, used for offline templatezip
    @SerializedName("fragments") var fragments: List<TemplateFragment> = emptyList() //Slot information
)
```


<span id="eeda1672"></span>
#### Sample code

```Kotlin
val templateItem = TemplateItem(
    md5 = pathMd5,
    unZipPath = result.absPath
)
```
