---
title: "Resource Package Structure"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-resource-package-structure"
---

<span id="Resource Package Structure"></span>
# Resource Package Structure

<span id="ModelResource.bundle"></span>
## ModelResource.bundle

This bundle contains model files for different algorithms. The corresponding model file is required when applying each algorithm.

<span id="StickerResource.bundle"></span>
## StickerResource.bundle

This bundle contains licensed sticker resources.

<span id="LicenseBag.bundle"></span>
## LicenseBag.bundle

This bundle contains licensed files.

<span id="ComposeMakeup.bundle"></span>
## ComposeMakeup.bundle

Most special effect resources are in ComposeMakeup.bundle, including face beautification, micro shaping, body shaping and face makeup.

<span id="Structure Description"></span>
### Structure Description

```Plain
.
└── ComposeMakeup
    ├── beauty_4Items                          // teeth whitening, eye brighting, smile line, dark circle
    ├── beauty_Android_camera                  // camera beautification effects including skin whitening, buffing, sharpening
    ├── beauty_Android_live                    // live stream beautification effects including skin whitening, buffing, sharpening
    ├── beauty_IOS_camera                      // camera beautification effects including skin whitening, buffing, sharpening
    ├── beauty_IOS_live                        // live stream beautification effects including skin whitening, buffing, sharpening
    ├── blush                                  // blush
    ├── body
    │   └── allslimqy                          // body shaping including long leg, body slimming
    │   └── allslim                            // body shaping including long leg, slim body, small head, slim leg, slim waist, breast, crotch, neck, slim arm（Body shaping was updated to this subfolder after version 3931，but avaliable for version 390 and above）   
    ├── composer
    ├── eyebrow                                // eyebrow
    ├── eyeshadow                              // eye shadow
    ├── beauty_eye_surgery                     // aegyo sal, double eyelids（only avaliable for version later than 3931） 
    ├── facial                                 // face contour
    ├── hair                                   // hair dye
    ├── lip                                    // lipstick
    ├── pupil                                  // pupil
    ├── reshape_camera                         // camera mirco shaping effects，including slim face, lift face, small face, big eye, rotated eye, cheek, jaw, lean nose, long nose, chin, forehead, mouth shape, smile, eye space, eye move, mouth move
    └── reshape_live                           // live streaming mirco shaping effects，including slim face, lift face, small face, big eye, rotated eye, cheek, jaw, lean nose, long nose, chin, forehead, mouth shape, smile, eye space, eye move, mouth move
```


<span id="Functionality Description"></span>
### Functionality Description

.config_file exmaple：

```Plain
[

    "whiten",

    "sharp",

    "smooth"

]
```


File content is a Json list, each element links to a functionality key.

<span id="FilterResource.bundle"></span>
## FilterResource.bundle

This bundle contains licensed filter resources.

<span id="Filter Index"></span>
### Filter Index

Each filter has a unique index, you can find the filter index by filter names (e.g. Filter_01_38 corresponds to filter with index 1).

Below is the query table. Keys are the 'Pingin' name of filters (Chinese phonetic alphabet) in sample. Values are the corresponding index value of each filter.

```Plain
{
 "roubai": 1,    
"baixi": 1,    
"naiyou": 2,    
"yangqi": 3,    
"jiegeng": 4,    
"luolita": 5,   
 "mitao": 6,   
 "makalong": 7,   
 "paomo": 8,   
 "yinghua": 9,   
 "qiannuan": 10,   
 "wuyu": 11,   
 "beihaidao": 12,    
"riza": 13,    
"xiyatu": 14,    
"jingmi": 15,    
"jiaopian": 16,    
"nuanyang": 17,    
"jiuri": 18,    
"hongchun": 19,    
"julandiao": 20,    
"tuise": 21,    
"heibai": 22,    
"wenrou": 23,    
"lianaichaotian": 24,    
"chujian": 25,    
"andiao": 26,    
"naicha": 27,    
"soft": 28,    
"xiyang": 29,    
"lengyang": 30,    
"haibianrenxiang": 31,   
 "gaojihui": 32,   
 "haidao": 33,    
"qianxia": 34,    
"yese": 35,    
"hongzong": 36,    
"qingtou": 37,    
"ziran2": 38,    
"suda": 39,    
"jiazhou": 40,    
"shise": 41,    
"chuanwei": 42,    
"meishijiaopian": 43,    
"hongsefugu": 44,    
"lvtu": 45,    
"nuanhuang": 46,   
 "landiaojiaopian": 47
}
```
