---
title: "Android resources import and configuration"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-resources-import-and-configuration_1_1_0"
---

This topic covers the process of bringing external resources into the system and configuring them for optimal functionality.

<span id="f431e8a7"></span>
# Android package deliverables list


|**Folder** |**File** |**File Type** |**Description** |
|---|---|---|---|
|EffectResource |transitions.bundle |Transition resources |Available during track editing. |
||ModelResource.bundle |Model resources |The models relied on by special effects. |
||tone.bundle |Voice\-changing resources |Available on the voice\-changing panel of the preview editor module. |
||sound.bundle |Sound effects |Available during track editing. |
||sticker.bundle |Informational sticker pack |Available on the informational sticker panel of the preview editor module. |
||ve_effect.bundle |Special effect resources |Available on the special effects panel of the preview editor module. |
||ComposeMakeup.bundle |Beauty effect resources |Available on the beauty effects panel of the camera module. |
||StickerResource.bundle |Facial sticker packs |Available on the camera module's sticker panel and the preview editor module's facial sticker panel. |
||fonts.bundle |Font resources |Available on the text panel of the preview editor. |
||music.bundle |Music resources |Available on the music panel of the camera, preview editor, and track editor modules. |
||* filter.bundle<br><br>* ve_filter.bundle |Filter resources |Available on the filter panel of the camera and preview editor modules. |
||Resource_icons |Resource icons |Icons of all resources, available on the panel for display. |
||Panel_configs |Configuration files |Used to clarify the relations between panels. |
|RemoteResource |N/A |On\-demand resources for self\-deployment |Used for server deployment and unnecessary when resources are built into the project. |
|License |N/A |License file |Used for app authentication. |


<span id="06fcd427"></span>
## **Configuration files for panels**

For more information, refer to the following:


* [Camera module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-camera-module-configuration-and-features_1_1_0).

* [Preview Editor panels and configurations](https://docs.byteplus.com/docs/video-editor-sdk/preview-editor-panels-and-configurations_1_1_0).

* [Track Editor panels and configuration](https://docs.byteplus.com/docs/video-editor-sdk/track-editor-panels-and-configurations_1_1_0).


<span id="cc6a13c5"></span>
# **Resource configuration (online and on\-demand download)** 

This topic focuses on configuring resources by obtaining them through online and on\-demand downloads for efficient utilization.

<span id="a5932193"></span>
## **Scenario**


* **Scenario**: Download corresponding resources only when clicking on a specific function item.

* **Advantages**: Reduces package size; Avoids prolonged download time caused by downloading all resources at once.


<span id="6e6ca6b5"></span>
## **Mobile configuration**

Mobile configuration involves setting up various parameters and paths essential for downloading resources and accessing server\-side components in a mobile application. This includes specifying the download directory for resources, configuring server\-side domains and paths for obtaining configuration files, downloading special effects, and accessing models. Additionally, the configuration may involve defining prefixes for icons deployed on the server side. Overall, mobile configuration ensures seamless integration and efficient resource management within the mobile application environment.

The resource package does not need to be built into the project of the app:

```Kotlin
//  Configure the server's download domain, download path, and headers
val domainConfig = EORemoteAddressConfig(
    "http://test.com", "/eo/config",
    "http://test.com", "/eo/resource",
    "http://test.com", "/eo/model",
   
    "http://test.com/icons/" // Configure the icon prefix deployed on the server
)
val config = EOResourceConfig.Builder()
    .setDomainConfig(domainConfig) // This configuration is required when using online materials
    .setResourceSavePath(EOUtils.pathUtil.internalResource()) // Configure the resource download path, where all downloaded resources will be downloaded and decompressed
    .setSysLanguage(Locale.getDefault().language)
    .setNetWorker(DefaultNetWorker()) // Required when using online resources
    .build()

// Initialize the material SDK
EOResourceManager.init(config)

// Fetch panel configuration, set localOnly to false
EOResourceManager.syncLoadConfigByPanelKey(id, localOnly)

// Download materials
EOResourceManager.syncLoadResourceByItem(item)
```


<span id="77a455fd"></span>
### **Related operations**

This section outlines several mobile device configuration operations and concepts:

<span id="95478b3e"></span>
#### **Retrieving the configuration file**

To retrieve the configuration file, `configDomain` and `configPath` parameters are utilized to set the request parameters. For instance, upon completing the preceding configuration, a configuration file request is triggered as needed: `http://test.com/eo/config?panel_key=panel_name`. Here, `panel_name` denotes the panel's name, identical to the filename in `Panel_configs`.

<span id="a55f1227"></span>
#### **Downloading resources and models**

`resourceDomain` and `resourcePath` facilitate the download of special effect resources, while `modelDomain` and `modelPath` handle model resource downloads. During resource retrieval, the BytePlus Video Editor SDK initiates a request based on the domain and path parameters. It includes `x-para-download-file-name` in the request header to identify the target filename, consistent with that in `RemoteResource`.

<span id="f97a0d18"></span>
#### **Retrieving icons**

To access necessary icons for all resources, navigate to the `Resource_icons` folder. Once configured, the BytePlus Video Editor SDK retrieves icons during loading using the provided `iconUrlPrefix` and `iconName`. For example, if configured as `http://test.com/icons/eo_resource_my_icon.png`, the SDK fetches the icon from this URL.

<span id="f3c8f6ad"></span>
#### **Request headers**

BytePlus Video Editor SDK adds the following headers to configuration files and resources requests:


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|x\-para\-auth\-token |String |your_auth_token |Authentication token for connecting to the Para Cloud Platform. If not required, leave it empty. |
|x\-para\-pkg\-name |String |com.example.app |The package name of the application. |
|x\-para\-platform |String |iOS or Android |The platform on which the application operates, either iOS or Android. |
|x\-para\-pkg\-version |String |1.0.0 |The Video Editor SDK version number. |
|x\-para\-download\-file\-name |String |example_resource_file |The filename of the resource to be downloaded, matching the filename in RemoteResource. |


<span id="fd3375ad"></span>
#### EORemoteAddressConfig

```JavaScript
data class EORemoteAddressConfig(
// The domain for fetching configurations, e.g., http://www.xxx.com
var configDomain: String = "",
// The path for fetching configurations, e.g., api/config
var configPath: String = "",

 // The domain for fetching resources
var downloadDomain: String = "",
// The path for fetching resources
var downloadPath: String = "",

// The domain for fetching models
var modelDownloadDomain: String = "",
// The path for fetching models
var modelDownloadPath: String = "",

// Headers required for fetching resources (optional, configure as needed)
var header: Map<String, String>? = null,

// Custom icon download address (optional, configure as needed)
// If the customer does not want to use the download address in the icon field of configJson, they can specify the download domain for all icons by adding iconUrlPrefix. The complete download address is iconUrlPrefix + builtInIcon
var iconUrlPrefix: String? = null
```


<span id="7b7d40c7"></span>
### Server configuration

The server configuration involves deploying various resources and files to meet the requirements of client requests. This includes deploying configuration files, special effects and model resources, as well as icons. The process entails extracting necessary information from client requests, such as panel keys and file names, and ensuring that the requested resources are made available for download. Additionally, the server must ensure proper organization and accessibility of resources in designated folders to facilitate efficient retrieval and deployment.


|**Action** |**Description** |
|---|---|
|Deploy Configuration Files |* Based on client\-side configuration, extract the `panel_key` field information from the client's request query to obtain the name of the requested configuration file.<br><br>* For example, if the extracted panel_key is "recorder_beauty", it indicates that the requested configuration file is `recorder_beauty.json`. At this point, return the content of this file to the client.<br><br>* All configuration files are located in the Panel_configs folder. |
|Deploy Special Effects and Model Resources |* Based on client\-side configuration, extract the `x-para-download-file-name` field information from the client's request header to obtain the filename to be downloaded, and stream the file back to the client for download.<br><br>* All resources to be deployed are located in the RemoteResource folder. |
|Deploy Icons |* Based on client\-side configuration, deploy all icon resources. The icons to be deployed are located in the Resource_icons folder.<br><br>* For example, if the client configures `iconUrlPrefix` as `http://test.com/icons/`, the server should ensure that `http://test.com/icons/eo_resource_my_icon.png` can fetch the icon named `eo_resource_my_icon.png`. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After delivery, refrain from making any modifications, decompression, or compression of resource packages, as it may result in download failures.</div>


<span id="385a7638"></span>
# **Resource Import and Configuration—online and one\-time deployment**

This feature enables users to import resources and configure settings with the option for both online access and one\-time deployment, streamlining the process efficiently.

<span id="e2d7b484"></span>
## **Scenario**


* **Scenario**: The client downloads all resources, models, icons, and configuration files at the same time.

* **Benefit**: This reduces the package size, simplifies the server deployment, and requires less network interaction.


<span id="ee4f0bee"></span>
## Mobile configuration

Before using any SDK project, ensure that all resources are downloaded and extracted to the custom directory `TARGET_PATH`:

```JSON
// You need to add the implementation to read the panel configuration file in EOQuickInitHelper initConfigs() as follows:
DefaultLocalResourceLoader.instance.localConfigsLoader = object : LocalConfigsLoader {
    private val configsPathMap : Map<String, String> = mutableMapOf<EOResourcePanelKey, String>().apply {
        put(EOResourcePanelKey.PREVIEW_EDITOR_EFFECT, "${TARGET_PATH}/preview_editor_effect.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FILTER, "${TARGET_PATH}/preview_editor_filter.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FONT, "${TARGET_PATH}/preview_editor_font.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_INFO_STICKER, "${TARGET_PATH}/preview_editor_info_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "${TARGET_PATH}/eo_music.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_STICKER, "${TARGET_PATH}/preview_editor_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_VOICE, "${TARGET_PATH}/preview_editor_tone.json")
        put(EOResourcePanelKey.RECORDER_BEAUTY, "${TARGET_PATH}/recorder_beauty.json")
        put(EOResourcePanelKey.RECORDER_FILTER, "${TARGET_PATH}/recorder_filter.json")
        put(EOResourcePanelKey.RECORDER_MUSIC, "${TARGET_PATH}/eo_music.json")
        put(EOResourcePanelKey.RECORDER_STICKER, "${TARGET_PATH}/recorder_sticker.json")
        put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "${TARGET_PATH}/eo_music.json")
        put(EOResourcePanelKey.TRACK_EDITOR_SOUND, "${TARGET_PATH}/track_editor_sound.json")
        put(EOResourcePanelKey.TRACK_EDITOR_TRANSITION, "${TARGET_PATH}/track_editor_transition.json")
    }.map {
        it.key.value to it.value
    }.toMap()
    override fun loadConfigs(panelKey: String, type: String): String? {
        val value = configsPathMap.getValue(panelKey) ?: return null
        // Read the panel configuration file content from the downloaded configuration file
        return EOUtils.fileUtil.readJsonFile("${TARGET_PATH}/${value}")
    }
}

val config = EOResourceConfig.Builder()
    .setResourceSavePath(${TARGET_PATH}) // Configure the resource saving path, which can be customized
    .build()

// Initialize the media SDK 
EOResourceManager.init(config)

// Set localOnly to true when fetching panel configurations
EOResourceManager.syncLoadConfigByPanelKey(id, localOnly)

// Download resources
EOResourceManager.syncLoadResourceByItem(item)
```


<span id="91dc3c34"></span>
## Server configuration

Align with the request from the client and return the resource package for download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you compress the resource package <code>EffectResource</code> into a <code>.zip</code> file for download.</div>


<span id="a4a74d37"></span>
# Resource import and configuration (built\-in)

Import and configure built\-in resources for Video Editor SDK by defining a download directory, setting resource and configuration directories, and importing resources with ease.

<span id="49ddea40"></span>
## Scenario


* **Scenario**: The resource package is built into the project.

* **Benefit**: The resource package can be used offline and does not need to be deployed on the server.


<span id="7005ee7d"></span>
## Mobile configuration

Integrate the EffectResource folder into the `EOLocalResources.bundle` and package it into the app for BytePlus Video Editor SDK's special effects.

**For mobile configuration:** 


1. Place the EffectResource folder directly into the assets directory and package it into the app.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7137715ca8134328bef626bb4d4ac8d5~tplv-goo7wpa0wc-image.image) </span>

2. Copy all icons from the `Resource_icons` folder to the `res/drawable-xxhdpi` directory in your project.

3. Before using any SDK effects, perform the following configuration.

   ```JSON
   // You need to add the implementation to read the panel configuration file in EOQuickInitHelper initConfigs() as follows:
    DefaultLocalResourceLoader.instance.localConfigsLoader = object : LocalConfigsLoader {
       private val configsPathMap : Map<String, String> = mutableMapOf<EOResourcePanelKey, String>().apply {
           put(EOResourcePanelKey.PREVIEW_EDITOR_EFFECT, "Panel_configs/preview_editor_effect.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_FILTER, "Panel_configs/preview_editor_filter.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_FONT, "Panel_configs/preview_editor_font.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_INFO_STICKER, "Panel_configs/preview_editor_info_sticker.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "Panel_configs/eo_music.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_STICKER, "Panel_configs/preview_editor_sticker.json")
           put(EOResourcePanelKey.PREVIEW_EDITOR_VOICE, "Panel_configs/preview_editor_tone.json")
           put(EOResourcePanelKey.RECORDER_BEAUTY, "Panel_configs/recorder_beauty.json")
           put(EOResourcePanelKey.RECORDER_FILTER, "Panel_configs/recorder_filter.json")
           put(EOResourcePanelKey.RECORDER_MUSIC, "Panel_configs/eo_music.json")
           put(EOResourcePanelKey.RECORDER_STICKER, "Panel_configs/recorder_sticker.json")
           put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "Panel_configs/eo_music.json")
           put(EOResourcePanelKey.TRACK_EDITOR_SOUND, "Panel_configs/track_editor_sound.json")
           put(EOResourcePanelKey.TRACK_EDITOR_TRANSITION, "Panel_configs/track_editor_transition.json")
       }.map {
           it.key.value to it.value
       }.toMap()
       override fun loadConfigs(panelKey: String, type: String): String? {
           val value = configsPathMap.getValue(panelKey) ?: return null
          //  Read the panel configuration file content from the downloaded configuration file.
           return EOUtils.fileUtil.readJsonFromAssets(AppSingleton.instance, "${EOUtils.pathUtil.assetsResourcePath}/${value}")
       }
   }
   val config = EOResourceConfig.Builder()
      
       .setResourceSavePath(EOUtils.pathUtil.internalResource()) // Configure the resource save path
      
       .build()
      
   // Initialize the media SDK 
   EOResourceManager.init(config)
         
   // Set localOnly to true when fetching panel configurations
   EOResourceManager.syncLoadConfigByPanelKey(id, localOnly)
         
   // Download resources 
   EOResourceManager.syncLoadResourceByItem(item)
      
   ```
   


<span id="0362ae78"></span>
# Resource import and configuration (partial built\-in and online)

Configure resource imports, combining partial built\-in and partial online components for efficient functionality.

<span id="7b67536b"></span>
## Scenario


* **Scenario**: Some resources are built\-in to speed up resource loading, while others are deployed online to reduce the package size.

* **Benefit**: This balances the loading speed and package size.


<span id="f0c2ef18"></span>
## Mobile configuration

Integrate the resource package into the project as per the "built\-in" scenario. Then, configure network parameters along with paths for both the built\-in resource package and the downloadable resource package.

**For mobile configuration:** 


1. Place the `EffectResource` folder directly into the assets directory of your project and package it with the App.

2. Set network\-related parameters, the path for the embedded resource package, and the path for downloading resource packages


```JSON
// You need to add the implementation to read the panel configuration file in EOQuickInitHelper initConfigs() as follows:
 DefaultLocalResourceLoader.instance.localConfigsLoader = object : LocalConfigsLoader {
    private val configsPathMap : Map<String, String> = mutableMapOf<EOResourcePanelKey, String>().apply {
        put(EOResourcePanelKey.PREVIEW_EDITOR_EFFECT, "Panel_configs/preview_editor_effect.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FILTER, "Panel_configs/preview_editor_filter.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FONT, "Panel_configs/preview_editor_font.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_INFO_STICKER, "Panel_configs/preview_editor_info_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_STICKER, "Panel_configs/preview_editor_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_VOICE, "Panel_configs/preview_editor_tone.json")
        put(EOResourcePanelKey.RECORDER_BEAUTY, "Panel_configs/recorder_beauty.json")
        put(EOResourcePanelKey.RECORDER_FILTER, "Panel_configs/recorder_filter.json")
        put(EOResourcePanelKey.RECORDER_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.RECORDER_STICKER, "Panel_configs/recorder_sticker.json")
        put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.TRACK_EDITOR_SOUND, "Panel_configs/track_editor_sound.json")
        put(EOResourcePanelKey.TRACK_EDITOR_TRANSITION, "Panel_configs/track_editor_transition.json")
    }.map {
        it.key.value to it.value
    }.toMap()
    override fun loadConfigs(panelKey: String, type: String): String? {
        val value = configsPathMap.getValue(panelKey) ?: return null
       //  Read the panel configuration file content from the downloaded configuration file.
        return EOUtils.fileUtil.readJsonFromAssets(AppSingleton.instance, "${EOUtils.pathUtil.assetsResourcePath}/${value}")
    }
}   
   
// Configure server download domain and download path, headers.
   
val domainConfig = EORemoteAddressConfig(
    "http://test.com", "/eo/config", 
    "http://test.com", "/eo/resource",
    "http://test.com", "/eo/model"
    "http://test.com/icons/" // Configure the icon prefix deployed on the server.
   
)  
val config = EOResourceConfig.Builder()
    .setDomainConfig(domainConfig) // Required for using online materials.
    .setResourceSavePath(EOUtils.pathUtil.internalResource()) // Configure the resource download path where all downloaded resources will be downloaded and uncompressed
    .setSysLanguage(Locale.getDefault().language)
    .build()
 
// Initialize the material SDK. 
EOResourceManager.init(config)
 
// Set localOnly to false when fetching panel configurations. 
EOResourceManager.syncLoadConfigByPanelKey(id, localOnly)
  
// Download materials. 
EOResourceManager.syncLoadResourceByItem(item) 
```


<span id="6f37e3e6"></span>
## Server configuration

Depending on the deployment scenario, refer to either of the following:


* [Resource configuration (online and on-demand download)](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-resources-import-and-configuration_1_1_0#resource-configuration-online-and-on-demand-download)

* [Resource Import and Configuration—Online and one-time deployment](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-resources-import-and-configuration_1_1_0#resource-import-and-configuration%E2%80%94online-and-one-time-deployment)


<span id="eca2aaf4"></span>
## Third\-party information stickers

For more information, refer to [Third-party stickers resource import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-third-party-stickers-resource_1_1_0).

<span id="9ffa13f8"></span>
# Code references

These are the code references for resource import and configuration.

<span id="c3b2d60b"></span>
## Key class introduction

These are the classes used during resource import and configuration:


* EOResourceManager

* EOResourceConfig

* IEOResourceItem

* DefaultLocalResourceLoader


<span id="f1090418"></span>
### EOResourceManager

The EOResourceManager is provided by the EffectOne SDK to facilitate the management and configuration of resources required for features such as stickers, effects, and filters. This SDK simplifies the process of integrating and managing resources for developers.

Key capabilities of the EOResourceManager include:


* Synchronous/asynchronous copying of offline resources.

* Synchronous/asynchronous fetching and parsing of panel configuration JSON.

* Synchronous/asynchronous fetching of resource packages, including automatic retrieval of dependent models, automatic integration of online/offline resources, and the ability to fetch single/multiple sets of resources at once.


<span id="79df824e"></span>
### EOResourceConfig

Here's a breakdown of the configuration options for the EOResourceManager:


|**Parameter** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|setDomainConfig |EORemoteAddressConfig |No |Configuration for the resource domain: required for online resources, not for offline resources. |
|setResourceSavePath |String |Yes |Path to store resources. |
|SysLanguage |String |No |System language. |
|setNetWorker |String |No |Add network implementation. It is required when using online resources. |


<span id="1bb10782"></span>
### IEOResourceItem

The `IEOResourceItem` interface is crucial within the Video Editor SDK SDK, as all functionalities such as filters, stickers, rely on resources for implementation. This interface provides a universal interface for describing various types of resources. Clients can customize their implementation of `IEOResourceItem` according to their needs, thereby allowing them to customize the tabs, order, icons, names, and other elements of the shooting and editing panels within the EffectOne SDK.

By default, the `EOResourceManager` automatically constructs corresponding `ResourceItem` objects based on the configuration files of each panel, relieving clients from having to worry about this aspect.


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|uniqueId |String |Yes |12345 |Unique ID of the current resource |
|title |String |Yes |Sticker |Title of the resource (language set by the user) |
|icon |String |No |http://example.com/icon.png |URL of the online resource icon |
|builtInIcon |String |No |offline_icon.png |Filename of the offline resource icon |
|defaultOn |Int |No |1 |Whether the resource is enabled |
|absPath |String |Yes |/storage/emulated/0/MyApp/Stickers |Absolute path to the local storage of the resource |
|subItems |List |No |N/A |Structure of sub\-items for the current resource |
|params |Map<String,Any\>? |No | |Parameters required when using the resource |
|extra |Map<String,String\>? |No | |Additional parameters required for music\-related resources |


<span id="c30c6324"></span>
### DefaultLocalResourceLoader

`DefaultLocalResourceLoader` is an essential component of the Video Editor SDK, as each panel within the SDK requires the integration partner to implement the logic for loading resources within the host application. If the integration partner chooses to use the `EOResourceManager`, they can utilize the following default implementation of the `ResourceLoader`.

```JSON
/**
ResourceLoader for loading local resources in the material SDK.
*/
class DefaultLocalResourceLoader : ResourceLoader {
companion object {
val instance = DefaultLocalResourceLoader()
}
override suspend fun loadResourceList(id: String, type: String): List {
return EOResourceManager.syncLoadConfigByPanelKey(id, localOnly).tabs
}
override suspend fun loadResourceItem(item: IEOResourceItem): IEOResourceItem? {
return EOResourceManager.syncLoadResourceByItem(item)?.resourceItem
}
override fun checkResourceExist(item: IEOResourceItem): Boolean {
return EOResourceManager.resourceLoaded(item)
}
}
```


<span id="c016f455"></span>
## Interface sample code

```Kotlin
interface IEOResourceItem {
    val uniqueId: String
    var title: String
    var tips: String?
    var icon: String
    var builtInIcon: String

    //0:Close，1:Open
    var defaultOn: Int
    var absPath: String
    var subItems: List?
    var params: Map?
    var extra: Map?
}
```
