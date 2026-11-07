---
title: "iOS resources import and configuration"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-resource-import-and-configuration_1_1_0"
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


* [Camera module UI](https://docs.byteplus.com/docs/video-editor-sdk/camera-module-ui_1_1_0).

* [Preview Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/preview-editor-ui_1_1_0).

* [Track Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/track-editor-feature-ui_1_1_0).


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

**This code configures the following:** 


1. Sets the download directory for resources using `EOSDK.setResourceBaseDir()`.

2. Configures server\-side download domain names and paths for obtaining configuration files, downloading special effects, and downloading models using `EORemoteAddrConfig`.

3. Sets the prefix of icons deployed on the server side.

4. Passes the configured remote address configuration to EOSDK using `EOSDK.setRemoteAddrConfig()`.


<span id="294ddf27"></span>
### Full code sample

```JSON
// Configure a download directory for resources. All downloaded resources will be saved and decompressed using the configured download directory. 
EOSDK.setResourceBaseDir(EOSDK.getEODocumentRootDir() + "/download_dir")

// Configure the server-side download domain name and the download path.
let addrConfig = EORemoteAddrConfig(
    configDomain: "http://test.com", // Configure the domain used to obtain the configuration file.
    configPath: "/eo/config", // Configure the path used to obtain the configuration file.
    resourceDomain: "http://test.com",  // The domain used to download special effects.
    resourcePath: "/eo/resource",  // The path used to download special effects.
    modelDomain: "http://test.com",  // The domain used to download models.
    modelPath: "/eo/model")  // The path used to download models.
       
// Configure the prefix of icon deployed in the server side.
addrConfig.iconUrlPrefix = "http://test.com/icons/"

// Pass the configuration to EOSDK.
EOSDK.setRemoteAddrConfig(addrConfig)

// Use the online configuration
EOSDK.useRemoteConfig(true, useRemoteResource: true)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The resource package EffectResource does not need to be built into the project of the app.</div>


<span id="32c45d82"></span>
### Related operations

This section outlines several mobile device configuration operations and concepts:

<span id="e09924c1"></span>
#### **Retrieving the configuration file**

To retrieve the configuration file, `configDomain` and `configPath` parameters are utilized to set the request parameters. For instance, upon completing the preceding configuration, a configuration file request is triggered as needed: `http://test.com/eo/config?panel_key=panel_name`. Here, `panel_name` denotes the panel's name, identical to the filename in `Panel_configs`.

<span id="5eb0cbdb"></span>
#### **Downloading resources and models**

`resourceDomain` and `resourcePath` facilitate the download of special effect resources, while `modelDomain` and `modelPath` handle model resource downloads. During resource retrieval, the BytePlus Video Editor SDK initiates a request based on the domain and path parameters. It includes `x-para-download-file-name` in the request header to identify the target filename, consistent with that in `RemoteResource`.

<span id="055f02cf"></span>
#### **Retrieving icons**

To access necessary icons for all resources, navigate to the `Resource_icons` folder. Once configured, the BytePlus Video Editor SDK retrieves icons during loading using the provided `iconUrlPrefix` and `iconName`. For example, if configured as `http://test.com/icons/eo_resource_my_icon.png`, the SDK fetches the icon from this URL.

<span id="ca15b083"></span>
#### **Request headers**

BytePlus Video Editor SDK adds the following headers to configuration files and resources requests:


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|x\-para\-auth\-token |String |your_auth_token |Authentication token for connecting to the Para Cloud Platform. If not required, leave it empty. |
|x\-para\-pkg\-name |String |com.example.app |The package name of the application. |
|x\-para\-platform |String |iOS or Android |The platform on which the application operates, either iOS or Android. |
|x\-para\-pkg\-version |String |1.0.0 |The Video Editor SDK version number. |
|x\-para\-download\-file\-name |String |example_resource_file |The filename of the resource to be downloaded, matching the filename in `RemoteResource`. |


<span id="31ad81fa"></span>
## Server configuration

For streamlined resource management, extract configuration details based on client preferences to seamlessly deploy specific files. Stream special effects and model resources back to the client using extracted filename information, and deploy icons according to client configurations, ensuring continued access post\-deployment.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deployment, refrain from performing any operations on the resource package, including modification, decompression, and compression. Performing such actions may result in download failures.</div>


<span id="12c0a5c6"></span>
### **Deploy Configuration Files**

This process outlines how configuration files are retrieved based on client requests, specifically focusing on extracting the necessary information and accessing the corresponding files.

To fulfill client requests efficiently, the system begins by extracting the `panel_key` field information from the query submitted by the client. Leveraging client\-side configuration, this information is then utilized to pinpoint the specific configuration file requested. The system navigates to the designated `Panel_configs` folder and retrieves the corresponding configuration file based on the extracted `panel_key` field value. For instance, if the `panel_key` field value is "*recorder_beauty,* " the system retrieves the corresponding configuration file named "*recorder_beauty.json*." Finally, the retrieved file is promptly returned to the client, ensuring a seamless and accurate response to their query.

<span id="6f28ecb5"></span>
### **Deploy Special Effects and Model Resources**

In this deployment framework, client\-side configuration plays a pivotal role, as it governs the process from start to finish. Initially, the system extracts crucial information, particularly the `x-para-download-file-name field`, from the client's request header. This extracted filename serves as a key identifier for locating the requested file within the designated RemoteResource folder. Once identified, the file is streamed back to the client, enabling seamless downloading. This centralized approach ensures that all resources earmarked for deployment are efficiently managed and readily accessible, streamlining the overall process.

<span id="346ef7ba"></span>
### **Deploy Icons**

In this deployment setup, the server operates in accordance with the client's configuration, facilitating the deployment of all required icons from the Resource_icons folder. For example, if the client specifies the `iconUrlPrefix` as *http://test.com/icons/* , the server ensures that icons can be accessed via URLs like *http://test.com/icons/eo_resource_my_icon.png*. Thus, clients can easily fetch specific icons such as "*eo_resource_my_icon.png*" using the provided URL structure.

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

Integrate the resource package into the project as per the "built\-in" scenario. Then, configure network parameters along with paths for both the built\-in resource package and the downloadable resource package.

The code is as follows:

```JSON
// Configure the server-side download domain name and the download path.
let addrConfig = EORemoteAddrConfig(
    configDomain: "http://test.com", // Configure the domain used to obtain the configuration file.
    configPath: "/eo/config", // Configure the path used to obtain the configuration file.
    resourceDomain: "http://test.com",  // The domain used to download special effects.
    resourcePath: "/eo/resource",  // The path used to download special effects.
    modelDomain: "http://test.com",  // The domain used to download models.
    modelPath: "/eo/model")  // The path used to download models.
    
// Configure the prefic of icon deployed at the server side.
addrConfig.iconUrlPrefix = "http://test.com/icons/"

// Pass the configuration to EOSDK.
EOSDK.setRemoteAddrConfig(addrConfig)

// Configure the root directory of resources.
EOSDK.setResourceBaseDir(EOSDK.defaultResourceDir(localBundle().bundlePath))

// Configure the directory of built-in resources.
EOSDK.setBuiltInResourceDir(localBundle().bundlePath)

// Configure the root directory of configuration files.
EOSDK.setResourceDefaultBuiltInConfig(EOSDK.defaultPanelConfigDir(localBundle().bundlePath))

// Use the online configuration
EOSDK.useRemoteConfig(true, useRemoteResource: true)
```


<span id="c1afc545"></span>
## Server configuration

Deploy resources on the server as needed. For more information, refer to the [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-resource-import-and-configuration_1_1_0#4b2c7388) or [Resource Import and Configuration—Online and one-time deployment](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-resource-import-and-configuration_1_1_0#81fb68bd).
