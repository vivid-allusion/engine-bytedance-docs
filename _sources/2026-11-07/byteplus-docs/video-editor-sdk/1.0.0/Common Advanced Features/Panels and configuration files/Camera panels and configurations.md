---
title: "Camera panels and configurations"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/camera-panels-and-configurations"
---

These are the camera feature panels and configuration files for reference.

<span id="66e8e622"></span>
# Camera–Beauty effects

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1420b8f3c9442ff95b45fca18f9a863~tplv-goo7wpa0wc-image.image) </span>

Use the Camera feature in the BytePlus Video Editor SDK to apply beauty effects to your photos.


* Resource bundle: `ComposeMakeup.bundle`

* Configuration file: `recorder_beauty.json`


```JSON
{
    "data": {
        "tabs": [
            {
                "uniqueId": "b0001",
                "titleDict": { // Tab Name
                    "en": "Beauty Effects",
                    "zh": "基础美颜"
                },
                "requirements": [ // Dependency Models
                    {
                        "relativePath": "ttfacemodel/algo_ggl1pqh_v11.1.model",
                        "md5": "F7360859FEB0EA5DF58DA9860EF9738F"
                    },
                    {
                        "relativePath": "ttfacemodel/algo_ggl1pqhlhmg7p_v14.0.model",
                        "md5": "D342795D110E4230666FB41B413AA638"
                    }
                ],
                "subItems": [ // Sub Nodes
                    {
                        "uniqueId": "b0002",
                        "titleDict": { // Node Title
                            "en": "Buffing",
                            "zh": "磨皮"
                        },
                        "builtInIcon": "eo_resource_beauty_smooth.png", // Icon Name
                        "defaultOn": 1, // Default On
                        "md5": "3F80B6A9EA5F57BCD36A5DD83C3E8BDD", // Remote Resource Package MD5
                        "relativePath": "ComposeMakeup.bundle/ComposeMakeup/beauty_lite_new.zip", // Relative Path for Download
                        "param": { // Parameters used by this effect
                            "intensity": 65,
                            "key": "smooth",
                            "path": "ComposeMakeup.bundle/ComposeMakeup/beauty_lite_new",
                            "range": [
                                0,
                                100
                            ]
                        }
                    }
                ]
            }
        ]
    }
}
```


<span id="12fd6d5e"></span>
# Camera \- Music

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71f449aaf9cc41a38fe27d173aa85337~tplv-goo7wpa0wc-image.image) </span>

Add music to your videos effortlessly using the Camera feature.


* Resource bundle: `music.bundle`

* Configuration file: `eo_music.json`


```JSON
{
    "data": {
        "tabs": [
            {
                "uniqueId": "g0001",
                "titleDict": {
                    "en": "Default",
                    "zh": "默认"
                },
                "subItems": [
                    {
                        "uniqueId": "g0002",
                        "titleDict": {
                            "en": "CarefreeSorrow",
                            "zh": "CarefreeSorrow"
                        },
                        "builtInIcon": "eo_resource_carefreesorrow_7255279633498800129.jpg",
                        "md5": "F4BB42D4BC4D35FFB35422FA050ED8F2",
                        "relativePath": "music.bundle/CarefreeSorrow_7255279633498800129/CarefreeSorrow_7255279633498800129/6991923169107904514.mp3",
                        "param": {
                            "path": "music.bundle/CarefreeSorrow_7255279633498800129/CarefreeSorrow_7255279633498800129/6991923169107904514.mp3"
                        },
                        "subTitleDict": {
                            "en": "unknown",
                            "zh": "未知"
                        },
                        "extra": {
                            "duration": "02:00"
                        }
                    }
                ]
            }
        ]
    }
}
```


<span id="478d464b"></span>
# Camera \- Filters

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4feac3a31c44cf58d9d0531522ab5f0~tplv-goo7wpa0wc-image.image) </span>

Enhance your photos with a variety of filters using the Camera feature.


* Resource bundle: `filter.bundle`

* Configuration file: `recorder_filter.json`


```JSON
{
    "data": {
        "tabs": [
            {
                "uniqueId": "c0001",
                "titleDict": {
                    "en": "Default",
                    "zh": "小项"
                },
                "subItems": [
                    {
                        "uniqueId": "c0002",
                        "titleDict": {
                            "en": "Creamy",
                            "zh": "奶油"
                        },
                        "builtInIcon": "eo_resource_filter_naiyou.png",
                        "md5": "33908964837A38ED547B397F90DC3EE9",
                        "relativePath": "filter.bundle/Filter_02_14.zip",
                        "param": {
                            "intensity": 65,
                            "path": "filter.bundle/Filter_02_14",
                            "range": [
                                0,
                                100
                            ]
                        }
                    }
                ]
            }
        ]
    }
}
```


<span id="5d40dfd1"></span>
# Camera \- Stickers

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c5f423eaa5740ce8d579c71a914cb61~tplv-goo7wpa0wc-image.image) </span>

Add fun stickers to your photos with the Camera feature.


* Resource bundle: `StickerResource.bundle`

* Configuration file: `recorder_sticker.json`


```JSON
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
