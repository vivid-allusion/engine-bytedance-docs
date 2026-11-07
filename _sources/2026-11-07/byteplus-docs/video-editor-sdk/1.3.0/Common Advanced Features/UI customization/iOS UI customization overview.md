---
title: "iOS UI customization overview"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-ios-ui-customization-overview"
---

The BytePlus Video Editor SDK is a comprehensive audio and video editing SDK equipped with user interfaces (UIs). Users have the flexibility to customize several UI elements, including theme colors, text, and icons. This level of customization empowers developers to tailor the visual experience of their applications according to their preferences and branding requirements.

<span id="cee4b10f"></span>
# Theme color: color chart

The color chart comes with key\-value pairs for all colors that can be changed in BytePlus Video Editor SDK. For more information, refer to [Video Editor SDK Color Chart](https://docs.byteplus.com/docs/video-editor-sdk/27338).

<span id="18f90471"></span>
## Customizing color

The SDK prioritizes reading custom colors internally. If no custom colors are defined, it uses internal default colors. Custom theme colors can be set using the following API. The color names must match those defined in the color palette table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>dark</code> and <code>light</code> are reserved fields for color styles. The current version only utilizes <code>dark</code>, and switching between them is not supported. Simply use the same color value for custom settings.</div>


**To apply a custom theme color:** 


1. Refer to the color chart for key\-value pairs for all colors.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on Video Editor SDK's color chart, refer to the <a href="https://docs.byteplus.com/docs/video-editor-sdk/27338">Video Editor SDK Color Chart</a>.</div>



2. Apply a custom theme color by calling the following code:


```Swift
EOSDK.setColorDictionary([
    "Primary" : [
        "dark" : "FF0ECDEB", //ARGB
        "light": "FF0ECDEB"
    ],
    "Secondary" : [
        "dark" : "FF0ECDEB",
        "light": "FF0ECDEB"
    ],
]);
```



3. Find the key\-value pair of a control in the UI


For more information, refer to [Customizable UI overview](https://docs.byteplus.com/docs/video-editor-sdk/27321#021e0446).

<span id="71661672"></span>
## Customizing text

The BytePlus Video Editor SDK replaces text using corresponding keys, and it's important that these key names remain unchanged.

For more information, refer to[Customizable UI overview](https://docs.byteplus.com/docs/video-editor-sdk/27321#021e0446).

**To customize the text:** 


1. To modify local text files, locate and edit the `EffectOne-en.strings` and `EffectOne-zh.strings` files within the `EOLocalResources\BuiltInResource\Strings` directory.

2. To modify the configuration in the code, the BytePlus Video Editor SDK prioritizes reading text set directly in the code. Identify the key corresponding to the target text and modify it accordingly.


Below is a sample code snippet:

```Java
//If you need to add other languages, you can obtain the language key using the following function, for example, "zh" for Chinese.
    func getLanguageCode() -> String? {
        let currentLanguage = Locale.preferredLanguages.first
        let components = currentLanguage?.components(separatedBy: "-")
        return components?.first
    }
    
EOSDK.setLocalizationDictionary([
    "zh" : [
        "eo_previeweditor_pop_discard" : "你好", 
        "eo_previeweditor_pop_discard_change": "你好"
    ],
    "en" : [
        "eo_previeweditor_pop_discard" : "hello", 
        "eo_previeweditor_pop_discard_change": "hello"
    ],
]);
```


<span id="c5a19aaa"></span>
## Customizing icons

The BytePlus Video Editor SDK replaces icons based on their corresponding names, and it's crucial that these names remain unchanged.

For more information, refer to[Customizable UI overview](https://docs.byteplus.com/docs/video-editor-sdk/27321#021e0446).

**To customize an icon:** 


1. To replace local icon files, locate and replace the files in the `EOLocalResources\BuiltInResource\Icons`, `EOLocalResources\BuiltInResource\Albums`, and `EOLocalResources\BuiltInResource\Animations` directories.

2. To modify the configuration in the code, the BytePlus Video Editor SDK prioritizes reading icons set directly in the code. Find and replace the names of the target icons accordingly.


Below is a sample code snippet:

```Java

   
var imageDictionary: [String: UIImage] = [:]
   
let image1 = UIImage(named: "image1")
   
imageDictionary["eo_album_list_bar_back"] = image1!
   

   
let image2 = UIImage(named: "image2")
   
imageDictionary["eo_album_list_delete"] = image2!
   

   
EOSDK.setIconDictionary(imageDictionary);
   
```


<span id="021e0446"></span>
# Customizable UI overview

This is a list of all the customizable UI screens within BytePlus Video Editor SDK:


|**Feature** |**Component** |
|---|---|
|Basic components |[Basic components UI customization](https://docs.byteplus.com/docs/video-editor-sdk/27337) |
|Camera |[Camera module UI](https://docs.byteplus.com/docs/video-editor-sdk/27325) |
|Preview Editor |[Preview Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/27330) |
|Track Editor |[Track Editor feature](https://docs.byteplus.com/docs/video-editor-sdk/27286) |
|Draft screen |[Draft mode UI](https://docs.byteplus.com/docs/video-editor-sdk/27323) |
|Music screen |[Music library panel](https://docs.byteplus.com/docs/video-editor-sdk/27331) |
||[Music volume panel](https://docs.byteplus.com/docs/video-editor-sdk/27317) |
||[Sound effects panel](https://docs.byteplus.com/docs/video-editor-sdk/27339) |
|Album screen |[Camera roll selection screen](https://docs.byteplus.com/docs/video-editor-sdk/27324) |
