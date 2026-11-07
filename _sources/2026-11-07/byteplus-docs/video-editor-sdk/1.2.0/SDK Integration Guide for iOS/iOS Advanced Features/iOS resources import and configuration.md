---
title: "iOS resources import and configuration"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-ios-resources-import-and-configuration"
---

This topic covers the process of bringing external resources into the system and configuring them for optimal functionality.

<span id="1d8866a0"></span>
# Resource information list


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


<span id="4dae9034"></span>
## Configuration files for panels

For more information, refer to


* [Camera panels and configurations](https://docs.byteplus.com/docs/video-editor-sdk/120-camera-panels-and-configurations).

* [Preview Editor panels and configurations](https://docs.byteplus.com/docs/video-editor-sdk/120-preview-editor-panels-and-configurations).

* [Track Editor panels and configuration](https://docs.byteplus.com/docs/video-editor-sdk/120-track-editor-panels-and-configurations).


<span id="4b2c7388"></span>
# Resource configuration (online and on\-demand download)

This topic focuses on configuring resources by obtaining them through online and on\-demand downloads for efficient utilization.

<span id="5b39f1e7"></span>
## Scenario


* **Scenario**: Resources are downloaded only when a function is clicked.

* **Benefits**: This reduces the package size and avoids downloading all resources at a time, which is time\-consuming.


<span id="c6169a7e"></span>
## Mobile configuration

Mobile configuration involves setting up various parameters and paths essential for downloading resources and accessing server\-side components in a mobile application. This includes specifying the download directory for resources, configuring server\-side domains and paths for obtaining configuration files, downloading special effects, and accessing models. Additionally, the configuration may involve defining prefixes for icons deployed on the server side. Overall, mobile configuration ensures seamless integration and efficient resource management within the mobile application environment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The resource package <code>EffectResource</code> does not need to be built into the project of the app.</div>


**This code configures the following:** 


1. Define the `EOResourceRequestBuilderProtocol` and implement `EOCustomRequestBuilderImpl`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Implement a custom class for the <code>EOResourceRequestBuilderProtocol</code> interface to define requests for fetching configurations, downloading resources, and loading icon URLs, which the SDK will call at the appropriate time to obtain the corresponding requests.   </div>
   

   ```objectivec
   @protocol EOResourceRequestBuilderProtocol <NSObject>
   
   @required
   // Custom request for corresponding panel configuration data
   // This method is called to get the request when fetching panel configurations
   - (NSURLRequest * _Nullable)buildConfigURLRequestByPanelKey:(NSString * _Nullable)panelKey resourceInfo:(NSDictionary * _Nullable)resource;
   
   // Custom request URL for image resources
   // This method is called to get the URL when loading each icon. If it returns null, the SDK will try to load the image file from the local path
   - (NSString * _Nullable)iconUrlString:(NSString * _Nullable)iconName;
   
   // Custom resource download request
   // This method is called to get the download request when downloading resources
   - (NSURLRequest * _Nullable)buildResourceDownloadRequestByRelativePath:(NSString * _Nullable)relativePath
                                                                  isModel:(BOOL)isModel
                                                             resourceInfo:(NSDictionary * _Nullable)resource;
   @end
   
   class EOCustomRequestBuilderImpl: NSObject, EOResourceRequestBuilderProtocol {
       ...
   }
   ```
   

2. Set the Custom Class Object to EOSDK like the following:

   ```objectivec
   // Set the custom class object to EOSDK
   EOInjectContainer.shared().resourceRequestBuilderImpl = EOCustomRequestBuilderImpl()
   ```
   

3. Set the resource loading base path using the following code:

   ```objectivec
   // Set the resource loading base path, and the downloaded resources will also be placed under this path
   EOSDK.setResourceBaseDir(EOSDK.getEODocumentRootDir() + "/download_dir")
   ```
   

4. Set the loading mode to online mode using the following:

   ```objectivec
   // Set the loading mode to online mode
   EOSDK.useRemoteConfig(true, useRemoteResource: true)
   ```
   


<span id="e09924c1"></span>
## Server configuration

For streamlined resource management, extract configuration details based on client preferences to seamlessly deploy specific files. Stream special effects and model resources back to the client using extracted filename information, and deploy icons according to client configurations, ensuring continued access post\-deployment.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deployment, refrain from performing any operations on the resource package, including modification, decompression, and compression. Performing such actions may result in download failures.</div>


To deploy the resources on the server as specified, ensuring that each request aligns with the resources provided, follow these steps based on the definitions in your `EOResourceRequestBuilderProtocol` implementation:


* **Deploy configuration files**: Use resources from the `Panel_configs` directory under `EffectResource` in the delivered asset package.

* **Deploy material and model resources**: Utilize resources from the `RemoteResource` directory under the delivered asset package.

* **Deploy icon resources**: Use resources from the `Resource_icons` directory under `EffectResource` in the delivered asset package.


According to the definitions in your implementation of the `EOResourceRequestBuilderProtocol` class, deploy configuration files, resources, and icon graphics separately to ensure that each request corresponds precisely to its respective resource.

For example,


* Upload the `RemoteResource`, `EffectResource/Panel_configs`, and `EffectResource/Resource_icons` directories from the delivered asset package to a file server.

* In your implementation of the `EOResourceRequestBuilderProtocol` class, point to each corresponding resource accordingly.


<span id="81fb68bd"></span>
# Resource Import and Configuration—Online and one\-time deployment

This feature enables users to import resources and configure settings with the option for both online access and one\-time deployment, streamlining the process efficiently.

<span id="a6eb4ba0"></span>
## Scenario


* **Scenario**: The client downloads all resources, models, icons, and configuration files at the same time.

* **Benefit**: This reduces the package size, simplifies the server deployment, and requires less network interaction.


<span id="e41eb269"></span>
## Mobile configuration

The resource package EffectResource does not need to be built into the project of the app.

The EffectResource package doesn't require inclusion in the app project. The client handles its download independently. Before utilizing any SDK project, ensure all resources are downloaded and decompressed. Follow the configuration provided in the example below:

```JSON
// Define the download directory for the SDK resources 
let downloadDir = EOSDK.getEODocumentRootDir() + "/download_dir"

// Set the base directory for downloaded and unzipped resources
EOSDK.setResourceBaseDir(EOSDK.defaultResourceDir(downloadDir))

// Set the directory for configuration files after download and unzipping
EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(downloadDir))

// Use the online configuration
EOSDK.useRemoteConfig(true, useRemoteResource: true)
```


This code sets up the download directory for the SDK resources, configures the destination directory for downloaded and unzipped resources, and sets the directory for configuration files after download and unzipping. Ensure that the download directory is correctly specified for the SDK to function properly.

<span id="b25bc521"></span>
## Server configuration

Align with the request from the client and return the resource package for download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you compress the resource package EffectResource into a .zip file for download.</div>


<span id="a1517208"></span>
# Resource import and configuration (built\-in)

Import and configure built\-in resources for Video Editor SDK by defining a download directory, setting resource and configuration directories, and importing resources with ease.

<span id="8abde8ec"></span>
## Scenario


* **Scenario**: The resource package is built into the project.

* **Benefit**: The resource package can be used offline and does not need to be deployed on the server.


<span id="7f0e1a47"></span>
## Mobile configuration

Integrate the EffectResource folder into the `EOLocalResources.bundle` and package it into the app for BytePlus Video Editor SDK's special effects. Apply the required configuration before using the SDK's special effects:

```JSON
// Configure the root directory of resources
EOSDK.setResourceBaseDir(EOSDK.defaultResourceDir(localBundle().bundlePath))
 
// Configure the root directory of configuration files
EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(localBundle().bundlePath))
```


<span id="eb5e7850"></span>
# Resource import and configuration (partial built\-in and partial online)

Configure resource imports, combining partial built\-in and partial online components for efficient functionality.

<span id="284a0f52"></span>
## Scenario


* Scenario: Some resources are built\-in to speed up resource loading, while others are deployed online to reduce the package size.

* Benefit: This balances the loading speed and package size.


<span id="88b81b77"></span>
## Mobile configuration

Integrate the resource package into the project as per the "built\-in" scenario. Following that, set the built\-in resource path.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on online request parameters, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/120-ios-resources-import-and-configuration#4b2c7388">Resource configuration (online and on\-demand download)</a>.</div>


**The code configures as follows:** 


1. Set the built\-in resource path:

   ```objectivec
   // Set the built-in resource path
   EOSDK.setBuiltInResourceDir(localBundle().bundlePath)
   ```
   

2. Set the resource root path. Online assets will be downloaded here, and built\-in assets will be copied here before use.

   ```objectivec
   // Set the resource root path
   EOSDK.setResourceBaseDir(EOSDK.defaultResourceDir(localBundle().bundlePath))
   ```
   

3. Set the configuration file loading path. If not configured, it will attempt to fetch the configuration file from the remote server.

   ```objectivec
   // Set the configuration file loading path
   EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(localBundle().bundlePath))
   ```
   

4. Configure the SDK to use online mode.

   ```objectivec
   // Configure to use the online mode.
   EOSDK.useRemoteConfig(true, useRemoteResource: true)
   ```
   


<span id="c1afc545"></span>
## Server configuration

Deploy resources on the server as needed. For more information, refer to the [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-resources-import-and-configuration#4b2c7388) or [Resource Import and Configuration—Online and one-time deployment](https://docs.byteplus.com/docs/video-editor-sdk/120-ios-resources-import-and-configuration#81fb68bd).

.
