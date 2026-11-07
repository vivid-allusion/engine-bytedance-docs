---
title: "Resource Package Structure (V421 and later)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-resource-package-structure-v421-and-later"
---

<span id="ModelResource.bundle"></span>
## ModelResource.bundle

This `bundle` contains many model files for algorithms. When applying algorithms, there needs to be corresponding model files.

<span id="StickerResource.bundle"></span>
## StickerResource.bundle

This `bundle` contains all licensed sticker resource.

<span id="LicenseBag.bundle"></span>
## LicenseBag.bundle

This `bundle` contains license file used for licensing.

<span id="ComposeMakeup.bundle"></span>
## ComposeMakeup.bundle

Most effects related resources are in `ComposeMakeup.bundle`, including beauty effects, face shaping, body shaping and makeup effects.

<span id="Structure Description"></span>
### Structure Description

Here's a list of all the expanding items:

```JSON
.
└── ComposeMakeup
    ├── beauty_4Items                                  // include teeth whitening, eye brightening, laugh line and dark circle 
    ├── beauty_Android_lite                                  // lite beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity
    ├── beauty_Android_standard                 // pro beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity
    ├── beauty_IOS_lite                                      // lite beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity
    ├── beauty_IOS_standard                     // pro beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity
    ├── reshape_lite                                         // lite face shaping, including face, eye, nose, mouth, etc.
    ├── reshape_boy                                         // lite - face shaping - Lower Face Width - handsome, V4.4.3 adds
    ├── reshape_girl                                         // lite - face shaping - Lower Face Width - beauty, V4.4.3 adds
    ├── reshape_nature                                         // lite - face shaping - Lower Face Width - natural, V4.4.3 adds
    |———— reshape_lite_eye_size                    //lite - V4.5.0 adds, face shaping - eye size
    |———— reshape_standard_girl                   // pro face shaping - V4.5.0 adds, slim face beta
    ├── reshape_standard                        // pro face shaping, including face, eye, nose, mouth, etc.
    |---- reshape_standard_boy                    // pro - face shaping - Lower face width - handsome, V4.5.2 adds
    |---- reshape_standard_girl                   // pro - face shaping - Lower face width - beauty, V4.5.2 adds
    |---- reshape_standard_nature                 // pro - face shaping - Lower face width - nature, V4.5.2 adds
    ├── body
    │   └── allslimqy                                  // body shaping: leg length, body slimming
    │   └── allslim                                          // body shaping: leg length, body slimming, head size, leg width, waist, breast, hip, neck, arrm (after SDK version 3931, body shaping is updated to be in this sub-directory, but it can be used for version 390 and above)  
    |    ————— allslim_breast                            //V4.5.0 pro body shaping: breast, hip
    ├── blush                                          // blusher
    │   └── lite                                                         // lite blusher
    │   └── standard                                  // standard blusher, color is adjustable
    ├── eyebrow                                        // eyebrow
    │   └── lite                                                         // lite eyebrow
    │   └── standard                                  // standard eyebrow, color is adjustable
    ├── eyelashes                                      // eyelash, color is adjustable
    ├── eyeshadow                                      // eyeshadow
    ├── eyelight                                      // eyelight
    ├── double_eye_lid                                 // double eyelid
    ├── beauty_eye_surgery                             // aegyo sal, double eyelids（must be used for version 3931 and above）
    ├── facial                                         // contour
    ├── hair                                           // hair dying
    ├── hack                                           // acne removal
    ├── lip                                            // lipstick
    │   └── lite                                                         // lite lipstick
    │   └── standard                                  // standard lipstick, color is adjustable
    ├── pupil                                          // pupil
    ├── palette                                          // palette items
    ├── style_makeup                                          // advanced makeup set: filter, makeup effects                                                                                                 
                                └── qise                                                                                                                         
                                └── xxxx
```


<span id="f1bcb65c"></span>
### Functional classification Catalog

This subsection describes small item folder names according to function classification, not bundle structure. When you can't find the corresponding function's folder during the access process, you can index it according to this subsection.


1. **Basic beauty for buffing/sharpening/clarity**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"beauty_Android_lite"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Functions of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)


* beauty_Android_lite *lite beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity*

* beauty_IOS_lite *lite beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity*

* beauty_Android_standard \*\* *pro beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity*

* beauty_IOS_standard *pro beauty effects, include toning, buffing, sharpening; Version 442 and later added clarity*

2. **Face shaping**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"reshape_lite"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Functions of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)


* reshape_lite *lite face shaping items are all in this folder*

* reshape_standard *pro face shaping items are all in this folder, V442 added*

* beauty_4Items *include teeth whitening, eye brightening, laugh line and dark circle*

* reshape_lite_eye_size *lite special eye size item, only has eye size, V450 added*

* reshape_boy *lite special lower face width, only has lower face width, V443 added*

* reshape_girl *lite special lower face width, only has lower face width, V443 added*

* reshape_nature *lite special lower face width, only has lower face width, V443 added*

* reshape_standard_boy \*\* *pro special lower face width, only has lower face width, V452 added*

* reshape_standard_girl \*\* *pro special lower face width, only has lower face width, V452 added*

* reshape_standard_nature *pro special lower face width, only has lower face width, V452 added*

3. **Body shaping**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"body/allslim"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Functions of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)


* body

   * allslimqy \*\* *body shaping: leg length, body slimming*

   * allslim *body shaping: leg length, body slimming, head size, leg width, waist, breast, hip, neck, arm (after SDK version 3931, body shaping is updated to be in this sub\-directory, but it can be used for version 390 and above)* 

   * allslim_breast *pro body shaping: breast&hip, V452 added*

4. **Makeup**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"lip/lite/doushafen"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Function of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)

Because there are so many makeup items, you can refer to section **Makeup items index** for details.


5. **Palette**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"palette/color"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Functions of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)


* palette

   * color *function Temperature, Saturation, Shadow, Fade*

   * contrast *function Contrast*

   * light *function Hue, Light, Highlight, Sensation*

   * particle *function Particle*

   * vignette *function Vignette*

6. **Advanced makeup set**


The node path can be specified by the folder name when you call it, such as `mEffectManager.setComposeNodes(new String[]{"style_makeup/aidou"});`, and the small items are controlled using the key. Specific keys can be viewed in the documentation: [Functions of resource keys (V421 and later)](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later)

Because there are so many items, you can refer to the section **Makeup items index** for details.

<span id="dce845ce"></span>
### Makeup items index


|**folder path & folder name** |||**function name** |
|---|---|---|---|
|lip |lite |doushafen |Puree Pink |
|||fuguhong |Vintage Red |
|||meizise |Plam Red |
|||shanhuse |Coral Red |
|||shaonvfen |Girlish Pink |
|||sironghong |Velvet Red |
|||xiguahong |Watermelon Red |
|||xiyouse |Pomelo Red |
|||yuanqiju |Vivid Orange |
|||zangjuse |Dark Orange |
||standard |liangze |Flash |
|||wumian |Foggy |
|||yaochun |Bitten |
|||yunran |Polishing |
|blush |lite |mitao |Peach |
|||qiaopi |Joyful |
|||richang |Daily |
|||shaishang |Sunburn |
|||tiancheng |Sweet orange |
|||weixun |Tipsy |
|||xinji |Calculating |
||standard |mitao |Peachy |
|||qise |Tinct |
|||rixi |Japanese |
|||shaishang |Sunburn |
|||suzui |Hangover |
|||weixun |Tipsy |
|||yuanqi |Vivid |
|facial |jingzhi |\ |Dedicate |
||fajixian |\ |Hairline |
||gaoguang |\ |Highlight |
||xiaov |\ |V line |
||ziran |\ |Natural |
|eyebrow |lite |BK01 |Heavy & black |
|||BK02 |Black |
|||BK03 |Thin & black |
|||BR01 |Brown |
||standard |biaozhun |Standard |
|||liuye |Lanceted |
|||rongrong |Furry |
|||yesheng |Wild |
|eyeshadow |wanxiahong |\ |Sunset red |
||shaonvfen |\ |Girllish pink |
||qizhifen |\ |Gorgeous pink |
||meizihong |\ |Plum red |
||jiaotangzong |\ |Caramel brown |
||yuanqiju |\ |Vivid orange |
||naichase |\ |Milktea brown |
||bingtangshanzha |\ |Hawthorn |
||dadizong |\ |Ground brown |
||hanxi |\ |Korean |
||nvshen |\ |Beauty |
||xingzi |\ |Apricot |
|pupil |hunxuezong |\ |Mixed brown |
||kekezong |\ |Cocoa brown |
||mitaofen |\ |Peach pink |
||shuiguanghei |\ |Waterlight black |
||xingkonglan |\ |Star blue |
||chujianhui |\ |First sight grey |
||huilv |\ |Celadon |
||huoxing |\ |Mars |
||huitong |\ |Grey |
||xinxinzi |\ |Xinxin |
||yuansheng |\ |Orignal |
|hair |anlan |\ |Dark blue |
||molv |\ |Dark green |
||shenzong |\ |Dark brown |
|eyelashes |chibang |\ |Wingy |
||juanqiao |\ |Curling |
||manhua |\ |Manga |
||xiachui |\ |Drooping |
||ziran |\ |Natural |
|eyelight |juguangdeng |\ |Spotlight |
||yueyaguang |\ |Moonglow |
||ziranguang |\ |Natural |
|wocan |chulian |\ |First love |
||manhuayan |\ |Cartoon eyes |
||suyan |\ |Without makeup |
||taohua |\ |Peach |
||xiachui |\ |Droop |
||ziran |\ |Natural |


<span id="2e02cd42"></span>
## FilterResource.bundle

<span id="List of filter index"></span>
### List of filter index

Every filter has a corresponding index, index can be found via filter resource name. For example, index for **Filter_01_38** is **1**. Below is the query list. For each element in the list, the key is the English name of filter, the pinyin name of filter (also the string name in the sample), and value is the index of corresponding filter folder.


|**English Name (UI in demo)**  |**Pinyin Name (String name in sample)**  |**Index of Resource Folder** |
|---|---|---|
|snow white |"roubai" or "baixi" |1 |
|creamy |"naiyou" |2 |
|oxygen |"yangqi" |3 |
|grandiflorum |"jiegeng" |4 |
|doll |"luolita" |5 |
|peach |"mitao" |6 |
|macaron |"makalong" |7 |
|foam |"paomo" |8 |
|sakura |"yinghua" |9 |
|mousse |"qiannuan" |10 |
|story |"wuyu" |11 |
|hokkaido |"beihaidao" |12 |
|japan magazine |"riza" |13 |
|seattle |"xiyatu" |14 |
|quite |"jingmi" |15 |
|film |"jiaopian" |16 |
|sun |"nuanyang" |17 |
|old days |"jiuri" |18 |
|red lips |"hongchun" |19 |
|orange blue |"julandiao" |20 |
|color fading |"tuise" |21 |
|black and white |"heibai" |22 |
|gentle |"wenrou" |23 |
|sweet love |"lianaichaotian" |24 |
|first sight |"chujian" |25 |
|dark |"andiao" |26 |
|bubble tea |"naicha" |27 |
|soft |"soft" |28 |
|sunset |"xiyang" |29 |
|cool oxygen |"lengyang" |30 |
|beach portrait |"haibianrenxiang" |31 |
|advanced grey |"gaojihui" |32 |
|island |"haidao" |33 |
|early summer |"qianxia" |34 |
|night |"yese" |35 |
|red brown |"hongzong" |36 |
|clear |"qingtou" |37 |
|natural |"ziran2" |38 |
|soda |"suda" |39 |
|california |"jiazhou" |40 |
|yummy |"shise" |41 |
|spicy |"chuanwei" |42 |
|movie |"meishijiaopian" |43 |
|vintage red |"hongsefugu" |44 |
|journey |"lvtu" |45 |
|warm yellow |"nuanhuang" |46 |
|blue film |"landiaojiaopian" |47 |
|Pale |“lengbaipi” |48 |
|Lucency |"touliang" |49 |
|Bright Orange |"liangju" |50 |
|Walnut |"hutaomu" |51 |
|Dark Brown |"shenhe" |52 |
|Dracula |"degula" |53 |
|Maroon |"lise" |54 |
|Coconut Forest |"yelin" |55 |
|Warm Food |"nuanshi" |56 |
|Sparkling Water |"qipaoshui" |57 |
|Cuisine |"liaoli" |58 |
|Grill |"tanshao" |59 |
|Kyoto |"jingdu" |60 |
|Coast |"haian" |61 |
|Green |"lvyan" |62 |
|Evening Sakura |"wanying" |63 |
|Green Orange |"qingcheng" |64 |
|Love of City |"aizhicheng" |65 |
|CT |"CT" |66 |
|EK |"EK" |67 |
|FJ |"FJ" |68 |
|Black Gold |"heijin" |69 |
|Hepburn |"heben" |70 |
