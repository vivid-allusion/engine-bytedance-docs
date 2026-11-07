---
title: "Function panels and configurations"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-function-panels-and-configurations"
---

These are the function panels and configuration files for reference.

<span id="60288218"></span>
# Video duet

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecad9b1e57d843a781659536b7930550~tplv-goo7wpa0wc-image.image) </span>


* Resource bundle: `duet.bundle`

* Configuration file: `recorder_duet.json`


```JSON
{
    "data": {
        "tabs": [
            { 
                "uniqueId": "duet0001",
                "titleDict": { // Category information
                    "en": "Default",
                    "zh": "默认"
                },
                "subItems": [
                    {
                        "uniqueId": "duet0003",
                        "titleDict": { // Material text
                            "en": "left and right",
                            "zh": "左右"
                        },
                        "builtInIcon": "eo_duet_zuoyou.png", // Icon name
                        "md5": "",
                        "relativePath": "duet.bundle/zuoyou_7031878287731294252/zuoyou_7031878287731294252", // Download relative path
                        "param": {
                            "path": "duet.bundle/zuoyou_7031878287731294252/zuoyou_7031878287731294252", // Resource loading path
                            "type": 0, // Duet material type
                            "key": "switchButton",
                            "val": 0
                        }
                    }
                ]
            }
        ]
    }
}
```


<span id="5947330c"></span>
# Magic Template

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a84d00a105664fb49d3ea0719471358c~tplv-goo7wpa0wc-image.image) </span>


* Resource bundle: `cutsame.bundle`

* Configuration file: `eo_cutsame.json`


```JSON
{ 
    "data": {
        "tabs": [
            { 
                "uniqueId": "g0001",
                "titleDict": { // Category information
                    "en": "Category 1",
                    "zh": "Category 1"
                },
                "subItems": [
                    {
                        "builtInIcon": "eo_resource_mengwa.jpg", // Image name
                        "builtInVideo": "eo_resource_mengwa.mp4", // Preview video name
                        "relativePath": "cutsame.bundle/mengwa/template.zip", // Download relative path
                        "param": {
                            "path": "cutsame.bundle/mengwa" // Resource load path
                        },
                        "md5": "CB502C5AE2B6359B69E8AAC10FE8EC5E", // Zip package MD5
                        "uniqueId": "CB502C5AE2B6359B69E8AAC10FE8EC5E", // Unique ID
                        "titleDict": { // Template text
                            "zh": "快乐成长吧！",
                            "en": "Happy Growing Up!"
                        },
                        "extra": {
                            "cover": { // Cover image size
                                "width": 720,
                                "height": 1080
                            },
                            "fragments": [ // Variable slot durations
                                {
                                    "duration": 0
                                },
                                {
                                    "duration": 0
                                }
                            ]
                        }
                    }
                ]
            }
        ]
    }
}
```
