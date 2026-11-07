---
title: "Third-party stickers resource import and configuration"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-third-party-stickers-resource-import-and-configuration"
---

Video Editor SDK supports the importing of third\-party information stickers through built\-in and online resource import methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure that you are familiar with the <a href="https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration">Android resources import and configuration</a> process before you proceed with importing third\-party stickers.</div>


Video Editor SDK supports the following file formats:


* JPG.

* PNG.

* JPEG.

* GIF.


<span id="38122e4b"></span>
# Resource import and configuration—Built\-in

Import and configure built\-in third\-party sticker resources for Video Editor SDK by defining a download directory, setting resource and configuration directories, and importing resources with ease.

**To import and configure built\-in resources:** 


1. Modify the built\-in configuration file path to the following:`EffectResource/Panel_configs/preview_editor_info_sticker.json`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee251e6baecb40feafc1656337bcb977~tplv-goo7wpa0wc-image.image) </span>

2. Add custom sticker data.

   ```Kotlin
   {
       "uniqueId": "f0012",// Based on existing increment （f0011 -->f0012)
       "titleDict": {//Language support and sticker title
           "en": "Kovensy",
           "zh": "Kovensy"
       },
       "builtInIcon": "eo_resource_kovensy_7165698429472342129.gif",//Offline built-in material display cover image 
    
       "md5": "a7d7058c2970d71349e96d70d6bb8b03",//For online materials, server-side MD5 verification is optional.
       "relativePath": "sticker.bundle/Kovensy_7165698429472342129/Kovensy_7165698429472342129.zip",//For online materials, the relative path to download the material locally.
       "param": {
           "path": "sticker.bundle/Kovensy_7165698429472342129/Kovensy_7165698429472342129/63076f5a10049f964f38d4ccaf9afa37.gif"// The local path for storing the material.
       }
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5837e5270d146caa3e803190913b387~tplv-goo7wpa0wc-image.image) </span>

3. Import `EffectResource` built\-in resources.

   According to the built\-in configuration file `EffectResource/Panel_configs/preview_editor_info_sticker`, the path field in the new data structure is: `"path":"sticker.bundle/Kovensy_7165698429472342129/Kovensy_7165698429472342129/63076f5a10049f964f38d4ccaf9afa37.gif"`.

   When you import your own custom stickers, the file path will be given with specific locations and extensions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure that the path is consistent with the configuration in json   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fc217206b924dad908c30563aa58823~tplv-goo7wpa0wc-image.image) </span>

4. Add `buildInIcon`.

   This is mainly used for displaying offline material thumbnails. If the `icon` field is not configured for third\-party information stickers supported by Video Editor SDK, it will be loaded from the drawable directory. Make sure the resource name matches the one configured in the JSON (`preview_editor_info_sticker.json`) file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1013382375244f7883320002fe94c419~tplv-goo7wpa0wc-image.image) </span>


<span id="b03dbc6f"></span>
# Resource import and configuration—Partial built\-in and online

Import and configure built\-in and online third\-party sticker resources for Video Editor SDK by defining a download directory, setting resource and configuration directories, and importing resources with ease. Ensure the the following conditions are met:


* For online resources, ensure that the relativePath in the configuration file (.zip file's md5) is correctly configured.

* The `relativePath` can also directly end with JPG, PNG, JPEG, or GIF.


For more information, refer to [Resource import and configuration (built-in)](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#a4a74d37) and [Resource import and configuration (partial built-in and online)](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#0362ae78).

`configDomain` and `configPath` are used to set the request parameters of the configuration file. For example, after the above configuration, a request for the configuration file will be initiated at the appropriate time: `http://test.com/eo/config panel_key = panel_name`. Among them, `panel_name` is the corresponding panel name, which corresponds one\-to\-one with the file name in the `Panel_configs`.

<span id="84f1c953"></span>
# Resource import and configuration—On\-demand download

For more information, refer to [Resource configuration (online and on-demand download)](https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration#cc6a13c5).

.
