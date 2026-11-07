---
title: "Android resources import and configuration"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-android-resources-import-and-configuration"
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


* [Camera panels and configurations](https://docs.byteplus.com/docs/video-editor-sdk/120-camera-panels-and-configurations).

* [Preview Editor panels and configurations](https://docs.byteplus.com/docs/video-editor-sdk/120-preview-editor-panels-and-configurations).

* [Track Editor panels and configuration](https://docs.byteplus.com/docs/video-editor-sdk/120-track-editor-panels-and-configurations).


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

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before proceeding with mobile configuration, take note of the following:</div>



* <div data-tips="true" data-tips-type="tip"><code>EffectResource</code> does not need to be embedded in the App project.</div>


* <div data-tips="true" data-tips-type="tip">Before using any project, configure <code>EOResourceConfig</code> to complete network\-related initialization.</div>



**Parameters**


|**Parameters** |**Type** |**Description** |**Recommended Value** |**Additional Notes** |
|---|---|---|---|---|
|resourceSavePath |String |Local path where the material is saved after download. |EOUtils.pathUtil.internalResource() | |
|sysLanguage |String |Language for displaying material names. Default supports Simplified Chinese (zh) and English (en); other languages require configuration in the config. |Locale.getDefault().language | |
|netWorker |INetWorker |Network request proxy. |DefaultNetWorker() |Implemented in EOQuickInithelper using OKHTTP to initiate network requests. |
|requestBuilder |IRequestBuilder |Proxy for building network requests. |Implemented based on customer scenarios:<br><br><br>* Building requests to download materials.<br><br>* Retrieving requests for online icons.<br><br>* Building requests for panel configuration. |Sample code:<br><br>```Plain```<br>```interface IRequestBuilder {```<br>```    fun buildDownloadResourceRequest(relativePath: String, isModel: Boolean, node: Any?): RequestInfo```<br>```    fun getIconUrl(buildInIcon: String): String?```<br>```    fun buildPanelConfigRequest(panelKey: String): RequestInfo```<br>```}```<br> |


<span id="67b719a2"></span>
### Defining requests using `IRequestBuilder`

`IRequestBuilder` allows you to define custom network requests tailored to your application's specific needs, ensuring you fetch the correct configuration, materials, and previews from the server. You should use the `IRequestBuilder` interface to create requests needed to fetch configuration files, material zip files, and preview images.

**Sample code**:

```Kotlin
        // Specify the directory for saving resource files and the language for resource usage
        val config = EOResourceConfig.Builder()
            .setResourceSavePath(EOUtils.pathUtil.internalResource())
            .setSysLanguage(Locale.getDefault().language)
            .setNetWorker(DefaultNetWorker()) // Configuration required for using online resources
            .setRequestBuilder(object: IRequestBuilder)
//            .setDomainConfig(EORemoteAddressConfig())  // Deprecated, replace with setRequestBuilder(EORemoteAddressConfig()) if previously used
//            .setRequestBuilder(DomainRequestBuilder(EORemoteAddressConfig()))
            .build()
```


<span id="2a71ff4f"></span>
### Using `OnlineResourceLoader`

`OnlineResourceLoader` enables the application to load resources from an online source instead of relying on local resources. This is crucial for applications that need to update content dynamically or have resources that are too large to include in the app package.

When configuring panels on various pages, use `OnlineResourceLoader` instead of `DefaultLocalResourceLoader` in EOQuickInitHelper. The sample code is as follows:

```Kotlin
class EOQuickInitHelper {
    ...
    fun initApplication(application: Application) {
        ...

        // Specify the directory for saving resource files and the language for resource usage
        val config = EOResourceConfig.Builder()
            .setResourceSavePath(EOUtils.pathUtil.internalResource())
            .setSysLanguage(Locale.getDefault().language)
            .setNetWorker(DefaultNetWorker()) // Configuration required for using online resources
            .setRequestBuilder(object: IRequestBuilder)
//            .setDomainConfig(EORemoteAddressConfig())  // Deprecated, replace with setRequestBuilder(EORemoteAddressConfig()) if previously used
//            .setRequestBuilder(DomainRequestBuilder(EORemoteAddressConfig()))
            .build()

        // Initialize the resource SDK
        EOResourceManager.init(config)
        
        ...
    }
    
    private fun initConfigs() {

        // Overall configuration for the recording module
        EffectOneConfigList.configure(RecorderInitConfig()) {
            it.finishAction = { activity, list, musicItem ->
                val options = ActivityOptionsCompat.makeCustomAnimation(activity, 0, 0)
                EditorMainActivity.startEditorActivityFromRecord(activity, list.map { resourceItem ->
                    com.volcengine.easyeditor.api.MediaItem(
                        path = resourceItem.path,
                        type = if (resourceItem.type == RecordMediaType.VIDEO) MediaType.VIDEO else MediaType.IMAGE,
                        duration = resourceItem.duration,
                        speed = resourceItem.speed
                    )
                } as ArrayList<com.volcengine.easyeditor.api.MediaItem>, options.toBundle(), musicItem)
            }
            it.albumConfig = AlbumConfig(
                allEnable = true,
                imageEnable = true,
                videoEnable = true,
                maxSelectCount = EffectOneSdk.albumMaxSelectedCount,
                // maxDuration Unit: ms
                maxDuration = 60 * 60 * 1000L,
                finishClazz = StartEditorFinishImpl::class.java
            )
        }
        
        val loader = OnlineResourceLoader()
        // Common panel configurations for editing and shooting
        // Filter panel
        EffectOneConfigList.configure(FilterUIConfig()) {
            it.resourceLoader = loader
        }
        // Face effect panel
        EffectOneConfigList.configure(EOBaseStickerUIConfig()) {
            it.resourceLoader = loader
        }
        // Music panel
        EffectOneConfigList.configure(EOBaseMusicUIConfig()) {
            it.resourceLoader = loader
        }

        // Special panel configurations for recording
        // Beauty panel
        EffectOneConfigList.configure(BeautyUIConfig()) {
            it.resourceLoader = loader
            it.defaultBeautyAction = {
                EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_BEAUTY.value, true).tabs
            }
        }
        // Duet panel
        EffectOneConfigList.configure((RecorderDuetUIConfig())) {
            it.resourceLoader = loader
            it.defaultDuetAction = {
                EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_DUET.value, true).tabs
            }
        }

        // Special panel configurations for editing
        // Info sticker panel
        EffectOneConfigList.configure(InfoStickerUIConfig()) {
            it.resourceLoader = loader
        }
        // Text panel
        EffectOneConfigList.configure(TextStickerUIConfig()) {
            it.resourceLoader = loader
        }
        // Video effects panel
        EffectOneConfigList.configure(EffectPanelUIConfig()) {
            it.resourceLoader = loader
        }
        // Audio effects panel
        EffectOneConfigList.configure(AudioFilterUIConfig()) {
            it.resourceLoader = loader
        }
        // Transition panel
        EffectOneConfigList.configure(TransitionUIConfig()) {
            it.resourceLoader = loader
        }
    }
}
```


<span id="77a455fd"></span>
## Server configuration

The server configuration involves deploying various resources and files to meet the requirements of client requests. This includes deploying configuration files, special effects and model resources, as well as icons. The process entails extracting necessary information from client requests, such as panel keys and file names, and ensuring that the requested resources are made available for download. Additionally, the server must ensure proper organization and accessibility of resources in designated folders to facilitate efficient retrieval and deployment.

<span id="7f193dca"></span>
### Deploying configuration files

Based on the RequestBuilder configuration, extract the `panel_key` field information from the client's request to obtain the configuration file name for the request.

```Kotlin
fun buildPanelConfigRequest(panelKey: String): RequestInfo 
```


**Parameters**


|**Parameters** |**Type** |**Description** |
|---|---|---|
|panelKey |String |The key corresponding to the panel. For example, if `panelKey` is "recorder_sticker", it indicates that the configuration file to be retrieved is `recorder_sticker.json`. The server returns the content of this file to the client. |
|RequestInfo |Data class |A data class representing the request information with fields: `domain`, `path`, `requestType`, `headerMap`, `body`, and `contentType`. |
|Panel_configs |String |All configuration files are located in the `Panel_configs` folder within the delivered documentation. |
|DefaultNetWorker.execute(requestInfo: RequestInfo) |Method |Implementation of the request behavior is handled in the execute method of DefaultNetWorker, which processes the `RequestInfo` object to execute the request. |


**Sample request code**

```Kotlin
data class RequestInfo(
    val domain: String? = "https://your panel host address",
    val path: String? = "/recorder_beauty",
    val requestType: RequestType = RequestType.GET, // Corresponding to API request
    val headerMap: Map<String, String>? = null,
    val body: ByteArray? = null,
    val contentType: String? = null
)
```


**Sample response**

```Kotlin
{
    "data": {
        "tabs": [
            {
                "uniqueId": "d0001",
                "titleDict": {
                    "en": "2D",
                    "zh": "2D"
                },
                "subItems": [
                    {
                        "uniqueId": "d0002",
                        "titleDict": {
                            "en": "Autumn Leaves",
                            "zh": "金秋叶舞"
                        },
                        "builtInIcon": "eo_resource_jinqiuyewu_7048762992175349791.png",
                        "md5": "F18FDFFD6DB904FFBE465909F0867959",
                        "relativePath": "StickerResource.bundle/jinqiuyewu_7048762992175349791.zip",
                        "param": {
                            "path": "StickerResource.bundle/jinqiuyewu_7048762992175349791"
                        },
                        "requirements": [
                            {
                                "relativePath": "ttfacemodel/algo_ggl1pqh_v11.1.model",
                                "md5": "F7360859FEB0EA5DF58DA9860EF9738F"
                            },
                            {
                                "relativePath": "ttfacemodel/algo_ggl1pqhlhmg7p_v14.0.model",
                                "md5": "D342795D110E4230666FB41B413AA638"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhl4hpkg6_v5.0.model",
                                "md5": "194F4C038CD35A4E07FF378DE97B8709"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhlpgg754kgh_v8.0.model",
                                "md5": "8CDD9000E4DE6111E21B148B3BFA2D5B"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhlpgg754kghlgt4_v7.0.model",
                                "md5": "4FFDB764F2EC8876B615A6865330E96C"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhlpgg754kghlhmg7p_v3.0.model",
                                "md5": "EA8D1F0BCEE6B8DC4DE8AC2693C85FE2"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhlpgg754kghlhmi_v1.0.model",
                                "md5": "93BB53B5394184A0495A278F7A801C3A"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl1pqhlpgg754kghlpah_v2.0.model",
                                "md5": "9EB2F0B32B36C71220AE4645144596DA"
                            },
                            {
                                "relativePath": "ttfaceattrmodel/algo_ggl4hpkg6lpgg7e_v2.0.model",
                                "md5": "2C2DC971E4F7567D09D26F870965043B"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvl4tml7ha_v12.0.model",
                                "md5": "9D85DE071360FDF2EF16BB89D7153B6C"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvl75ca_v1.1.model",
                                "md5": "1588A926866EF9A5367F23ADD9F0C2A5"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvl97_v3.2.model",
                                "md5": "A55AFDBBD45B1C84E33E2EA3A6859368"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvlahugk7h_v11.0.model",
                                "md5": "D5B8890589D61D738EB3AC050AC3716A"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvlahugk7hlgt4_v11.2.model",
                                "md5": "068E6D58EE05EA0250C2E96852DEBAA7"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvlsi_v6.0.model",
                                "md5": "130183E2A6880A627AFF4E86874E580B"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvlsibv_v2.0.model",
                                "md5": "97807B3D18A6D77D86E8DF96CEA386C7"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvluha_v2.0.model",
                                "md5": "DDDC9206CD2C70310C803E226E0F0A02"
                            },
                            {
                                "relativePath": "handmodel/algo_ggl0pcvlvhg_v11.0.model",
                                "md5": "208FF7DC0FE017C029D32D38646AC4F2"
                            }
                        ],
                        "tipsDict": {
                            "en": "Take out your hand",
                            "zh": "伸出手掌"
                        }
                    }
                ]
            }
        ]
    }
}
```


<span id="e6c62e06"></span>
### Deploying effects and model resources

You can deploy effect and model resources using the server.

Based on the `RequestBuilder` configuration, retrieve the relative path of the file to be downloaded from your request and stream the file back to you for downloading.

```Kotlin
fun buildDownloadResourceRequest(relativePath: String, ext: panelKey: Sting, isModel: Boolean, node: Any?): RequestInfo
```


**Parameters**


|**Parameters** |**Type** |**Description** |
|---|---|---|
|relativePath |String |Corresponds to the relative path of each material item in the `PanelConfig` returned by the server in the `PanelConfigRequest`. Accessing this path allows the recipient to deploy the material zip package to a server or CDN. |
|isModel |Boolean |Indicates whether the resource is a model. |
|node |Any |Detailed attributes corresponding to each item. Not necessary for attention. |
|RemoteResource |String |All resources that need deployment are located in the `RemoteResource` folder. |
|DefaultNetWorker.execute(requestInfo: RequestInfo) |Method |Implementation of the download behavior is handled in the execute method of DefaultNetWorker, which processes the RequestInfo object to execute the download request. |


**Sample request code**

```Kotlin
data class RequestInfo(
    val domain: String? = "https://your resource host address",
    val path: String? = "/StickerResource.bundle/jinqiuyewu_7048762992175349791.zip", // Corresponds to the relative path of an item in config.json
    val requestType: RequestType = RequestType.FILE, // Indicates a download request
    val headerMap: Map<String, String>? = null,
    val body: ByteArray? = null,
    val contentType: String? = null
)
// Returns data for downloading the corresponding zip package
```


<span id="f08762ea"></span>
### Deploying icon resources

Retrieve the icon URL based on the RequestBuilder configuration.

```Kotlin
fun getIconUrl(buildInIcon: String， panelKey: Sting): String?
```


**Parameters**


|**Parameters** |**Type** |**Description** |
|---|---|---|
|buildInIcon |String |The filename of the built\-in icon, such as `eo_resource_jinqiuyewu_7048762992175349791.png`. |
|panelKey |String |The key associated with the panel. |


For example, if the `builtInIcon` in the configuration (`config`) is `eo_resource_jinqiuyewu_7048762992175349791.png`, it returns the corresponding online address of the icon: `http://your icon host/eo_resource_jinqiuyewu_7048762992175349791.png`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The actual downloading of images is handled by Glide within <code>DefaultImageLoader</code> in <code>EOQuickInitHelper</code>.</div>


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
// In the EOQuickInitHelper's initConfigs() method, you need to add the implementation to read the panel configuration files. Refer to the following example:

DefaultLocalResourceLoader.instance.localConfigsLoader = object : LocalConfigsLoader {
    private val configsPathMap: Map<String, String> = mutableMapOf<EOResourcePanelKey, String>().apply {
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
        // Read the panel configuration file content from the downloaded configuration files
        return EOUtils.fileUtil.readJsonFile("${TARGET_PATH}/${value}")
    }
}

val config = EOResourceConfig.Builder()
    .setResourceSavePath(${TARGET_PATH}) // Configure the resource save path, which can be customized by the user
    .build()

// Initialize the resource SDK
EOResourceManager.init(config)

// Set localOnly to true when fetching panel configurations (one-time downloads are also considered offline resources by the resource SDK)
EOResourceManager.syncLoadConfigByPanelKey(id, localOnly)

// Download resources
EOResourceManager.syncLoadResourceByItem(item)
```


<span id="91dc3c34"></span>
## Server configuration

Align your network requests to provide your resource package for downloads.

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


* [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#cc6a13c5).

* [Resource Import and Configuration—online and one-time deployment](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#385a7638).


<span id="eca2aaf4"></span>
## Third\-party information stickers

For more information, refer to [Third-party stickers resource import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/120-third-party-stickers-resource-import-and-configuration).

<span id="9ffa13f8"></span>
# Code references

These are the code references for resource import and configuration.

<span id="c3b2d60b"></span>
## Key class introduction

These are the classes used during resource import and configuration:


* EOResourceManager.

* EOResourceConfig.

* IEOResourceItem.

* DefaultLocalResourceLoader.


<span id="f1090418"></span>
### EOResourceManager

The `EOResourceManager` is provided by the Video Editor SDK to facilitate the management and configuration of resources required for features such as stickers, effects, and filters. This SDK simplifies the process of integrating and managing resources for developers.

Key capabilities of the `EOResourceManager` include:


* Synchronous/asynchronous copying of offline resources.

* Synchronous/asynchronous fetching and parsing of panel configuration JSON.

* Synchronous/asynchronous fetching of resource packages, including automatic retrieval of dependent models, automatic integration of online/offline resources, and the ability to fetch single/multiple sets of resources at once.


<span id="1bb10782"></span>
### IEOResourceItem

The `IEOResourceItem` interface is crucial within the Video Editor SDK, as all functionalities such as filters, stickers, rely on resources for implementation. This interface provides a universal interface for describing various types of resources. Clients can customize their implementation of `IEOResourceItem` according to their needs, thereby allowing them to customize the tabs, order, icons, names, and other elements of the shooting and editing panels within the Video Editor SDK.

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
|params |Map? |No | |Parameters required when using the resource |
|extra |Map? |No | |Additional parameters required for music\-related resources |


<span id="75c1c073"></span>
### OnlineResourceLoader

The `OnlineResourceLoader` class implements the `ResourceLoader` interface to manage loading and checking of resources from an online source using Video Editor SDK. It provides methods to load a list of resources based on a panel ID and type, retrieve individual resource items, and check if a specific resource item exists. The loading operations are synchronous and ensure efficient resource management within the application.

```Kotlin
class OnlineResourceLoader : ResourceLoader {
    override suspend fun loadResourceList(id: String, type: String): List<IEOResourceItem> {
        return EOResourceManager.syncLoadConfigByPanelKey(id, false).tabs
    }

    override suspend fun loadResourceItem(item: IEOResourceItem): IEOResourceItem? {
        return if (EOResourceManager.syncLoadResourceByItem(item)?.resValue == 0) {
            EOResourceManager.syncLoadResourceByItem(item)?.resourceItem
        } else {
            null
        }
    }

    override fun checkResourceExist(item: IEOResourceItem): Boolean {
        return EOResourceManager.resourceLoaded(item)
    }
}
```


<span id="c30c6324"></span>
### DefaultLocalResourceLoader

`DefaultLocalResourceLoader` is an essential component of the Video Editor SDK, as each panel within the SDK requires the integration partner to implement the logic for loading resources within the host application. If the integration partner chooses to use the `EOResourceManager`, they can utilize the following default implementation of the `ResourceLoader`.

```Kotlin
/**
ResourceLoader for loading local resources in the material SDK.
*/ 
var localConfigsLoader = object : LocalConfigsLoader {
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
            put(EOResourcePanelKey.RECORDER_DUET, "Panel_configs/recorder_duet.json")
        }.map {
            it.key.value to it.value
        }.toMap()
        override fun loadConfigs(panelKey: String, type: String): String? {
            val value = configsPathMap.getValue(panelKey) ?: return null
            return EOUtils.fileUtil.readJsonFromAssets(AppSingleton.instance, "${EOUtils.pathUtil.assetsResourcePath}/${value}")
        }

    }
    companion object {
        val instance = DefaultLocalResourceLoader()
    }



    override suspend fun loadResourceList(id: String, type: String): List<IEOResourceItem> {
        if (!EOResourceManager.hasLocalConfigJson(id)) {
            localConfigsLoader.loadConfigs(id, type)?.let {
                EOResourceManager.setLocalConfigJson(id, it)
            }
        }
        return EOResourceManager.syncLoadConfigByPanelKey(id, true).tabs
    }

    override suspend fun loadResourceItem(item: IEOResourceItem): IEOResourceItem? {
        return EOResourceManager.syncLoadResourceByItem(item)?.resourceItem
    }

    override fun checkResourceExist(item: IEOResourceItem): Boolean {
        return EOResourceManager.resourceLoaded(item)
    }
}

interface LocalConfigsLoader {
    fun loadConfigs(panelKey: String, type: String): String?
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
    var subItems: List<IEOResourceItem>?
    var params: Map<String, Any>?
    var extra: Map<String, String>?
}
```
