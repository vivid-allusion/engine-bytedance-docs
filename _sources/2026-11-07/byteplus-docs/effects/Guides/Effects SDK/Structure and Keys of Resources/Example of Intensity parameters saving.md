---
title: "Example of Intensity parameters saving"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-example-of-intensity-parameters-saving"
---

The intensity of beauty and reshape saving function is dedicated to improving the user experience and matching the requirements of some clients, such as recording the parameters set when the user last entered the preview.

This doc is only written according to the sample code, which is the implementation layer code and is for reference only, you can refer to this part of code for checking how we achieve this function, and code depend on your own project .

<span id="4bae4945"></span>
# Achievement


* This function is used to record some parameters of intensity selected by the user in Beauty&Body Effects module, so that when the user enters this module again, the previous effect is directly displayed.

* For example:

   the user enters the beauty & body effect module, selects the effect of the filter as "soft white", the user returns to the home page, and enters this module again, the effect of "soft white" is shown by default.

* Another example:

   the user enters the picture preview mode in the beauty & body effect module, after selecting a single or multiple beauty effects, returns to the real\-time preview mode, the real\-time preview mode will have the effects selected in the picture preview mode before.

* This version has three modules: beauty & body effect, beauty & body effect pro, and advanced makeup set module to achieve this function.


<span id="5c705ac9"></span>
# Sample code

Since the intensity parameters saving are implementation\-level logic, this document only describes the sample code provided in the sample.

<span id="d65304d8"></span>
## iOS code

This section describes the Intensity parameters saving of the iOS sample code.


* The location of the main updated logic sample code in the sample


```Plain
Effect/Effect/model/LocalParameterSaving/BESaveLocalParameterManager.h[.m]
Effect/Effect/model/LocalParameterSaving/BEDocumentSaveManager.h[.m]
```



* The code location of the main encapsulation logic


```Plain
Effect/Effect/Effect.m
Effect/Effect/ui/base/vc/BEEffectVC.m
```


<span id="ed85b17d"></span>
### 1. Overall process


* Take the module title as the key, the value is the large json structure, which contains the small json structure.

* noFilter: Stores non\-filtered data, a single node key is ID & path.

* filter : Store filter data.

* Finally in the form of json string, saved in the local Document.


<span id="bc8b2820"></span>
### 2. Interface description

<span id="ab92694d"></span>
#### Global Intensity parameters saving function on/off

The code location is in: `Effect/Effect/Effect.m`

```C
#define  BEGLOBISSAVE  1
```


**Parameters:** 

The default value is 1. When it is 1, the save function is turned on; when it is 0, the save function is turned off.

<span id="2c9ea75f"></span>
#### Local module save parameter function on/off

The code location is in: `Effect/Effect/model/LocalParameterSaving/BESaveLocalParameterManager.m`

```C
+ (NSArray<NSString *> *)be_SaveModelTitles
{
    static dispatch_once_t onceToken;
    static NSArray *modelTitles;
    dispatch_once(&onceToken, ^{
        modelTitles = @[
            @"feature_beauty"
            ,@"feature_beauty_pro"
            ,@"feature_style_makeup"
        ];
    });
    return modelTitles;
}
```


**Parameters:** 

If a module needs to enable the local parameter saving function, the title of the module must be added to the modelTitles array. If a module does not need this function, remove the title from this array.

<span id="89aec659"></span>
#### Get locally saved data

The code location is in: `Effect/Effect/ ui /base/ vc /BEEffectVC.m`.

```C
///Get locally saved data
///@param isFilter     whether to get filter data
- (id)reloadLocalDataISFilter:(BOOL)isFilter
```


<span id="4a49255b"></span>
#### The data that needs to be saved locally

The code location is in: `Effect/Effect/ ui /base/ vc /BEEffectVC.m`.

```C
///For subclasses to call, for saving local data
///@param data The data to be saved
///@param isFilter is filter data
- (void)be_saveLocalParameterWith:(id)data ISFilter:(BOOL)isFilter
```


<span id="da93adbc"></span>
#### Update locally saved node strength values

The code location is in: `Effect/Effect/ ui /base/ vc /BEEffectVC.m`.

```C
///Update the strength value of a locally saved node
///@param item node
- (void)be_updateNodeIntensityValue:(BEEffectItem *)item
```


<span id="2da391f9"></span>
#### Delete locally saved parameters

The code location is in: `Effect/Effect/ ui /base/ vc /BEEffectVC.m`.

```C
///Delete locally saved parameters
- (void)be_deleteLocalParameter
```


<span id="7851c9f5"></span>
### 3. Calling example

Take the beauty & body effect module as an example to illustrate the actual implementation of calling the above encapsulation interface.

The location of the sample code in the sample: `Effect/Effect/ ui /effect/ vc /BEBeautyEffectVC.m`.

<span id="c11787f0"></span>
#### Call save interface in click event

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d328eee3fce34af4ae976a37681f4108~tplv-em5hxbkur4-noop.image?width=1874&height=924) </span>

<span id="c7aeb721"></span>
#### Call the update intensity interface in the intensity slip callback event

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/aed40150d3cd4e63998d8fc488f01d9b~tplv-em5hxbkur4-noop.image?width=1742&height=1170) </span>

<span id="e56b94c2"></span>
#### Call get locally saved data interface in initialization or reset event

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/07b6ec01415d4bb580c09ff0e767e59e~tplv-em5hxbkur4-noop.image?width=1732&height=1030) </span>

<span id="9b4fd9a0"></span>
## Android code

This section describes the Intensity parameters saving of the Android sample code.


* New classes for the local database


```Plain
com.bytedance.labcv.common.database.LocalParamHelper
com.bytedance.labcv.common.database.LocalParamManager
```



* Provides interfaces for directly saving and reading local data for the functions of beauty, face shaping, body shaping and advanced makeup

   `com.bytedance.labcv.effect.manager.LocalParamDataManager`


<span id="5213c060"></span>
### 1. Overall process

Create a local sqlite database, and create a table for beauty & body effect, beauty & body effect pro, and advanced makeup set.

Parameter data storage follows the following principles:


1. Each record in the database corresponds to a call to the SDK interface.

* There are 5 interfaces for sdk to set material effects: `updateComposerNodeIntensity`, `updateFilterIntensity`, `setSticker`, `setRenderCacheTexture`, `sendMessage`; each call of the above 5 interfaces will correspond to the addition, deletion and update of a record in a database.

* One Makeup Pro material will correspond to the records in 4 databases (intensity, color R, G, B); one style makeup material will correspond to the records in 2 databases (filters, touch\-ups).

2. The database will only clear the records in the table during the "restore reset" operation, and other operations will only add and update records, but will not delete records.

* The goal is to completely save the state of all accumulated operations of the user.

3. The sequence number of database records indicates the order in which the user first set a function.

* This will ensure that in the records read from the database, the four records will strictly correspond to the four effects of intensity, color R, G, and B in order.

4. For the scene of continuous adjustment of the slider, the status is only written to the database when the slider was last set.

5. In the case of mutual exclusion between functions, the demo code should manually manage the mutual exclusion status between fields between different records in the database.

6. After the demo enables the local storage function, preview the initial state of opening, save the state when exiting the background, save the state after returning to the home page, save the state of exiting the application, and save the state of entering the picture mode and returning, all based on the state recorded in the database prevail.

7. The running state of the demo (including the UI and memory storage) should be able to achieve a one\-to\-one correspondence with the state of the database, that is, it is required that all necessary demo running states can be completely stored in the database, or the The database restores the running state of the demo unambiguously.


<span id="d9dc6637"></span>
### 2. Calling example

Each time the android side sample function is turned on (preview the initial state of opening, state saving when exiting the background, state saving after returning to the home page, state saving when exiting the application, state saving when entering picture mode and returning), it will load data from the database twice., the first time will restore the effect state of sdk , and the second time will restore the UI state from the data. The changes in the database occur at three time points: item selection, intensity/color value change, and reset.

<span id="3cc1efe0"></span>
#### Initialization phase

Restore the effect state of the sdk during the initialization phase of the BaseEffectActivity.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/3a0e6753b5c6481ebb9b09e0b73c8568~tplv-em5hxbkur4-noop.image?width=2072&height=1408) </span>

<span id="60461e12"></span>
#### Open function

When the function is turned on (preview the initial state of opening, save the state when exiting the background, save the state after returning to the home page, save the state of exiting the application, and save the state of entering the picture mode and returning) refresh the UI state.

UpdateLocalParam method for EffectFragment

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/35a06104753341b28d9c15bc2f5d03c5~tplv-em5hxbkur4-noop.image?width=1942&height=1076) </span>

StyleMakeupFragment's updateLocalParam method

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/14820090e7e74212ac59e27f3cf5f16b~tplv-em5hxbkur4-noop.image?width=2082&height=1516) </span>

<span id="fb18d93a"></span>
#### Item selection, status update

onFilterSelected、onProgressEnd、onColorSelected、resetToDefault in the class EffectFragment

onItemClick、removeOrAddItem in the class BeautyFaceFragment

onBeautySelect、resetDefault、onProgressEnd in the class StyleMakeupFramgent

See the above methods, the content under the LocalParamDataManager.useLocalParamStorage () condition judgment

<span id="cf5a6b5b"></span>
### 4. Parameter store field description

The stored data structure is as follows:

```java
public class LocalParam{
        public String category;    //Indicates what sdk interface the clip calls to set the effect
        public String path;   //material path
        public String key;   //key field
        public float intensity;   //intensity value
        public int arg0;    //parameter 0
        public long arg1;   //parameter 1
        public long arg2;   //parameter 2
        public String arg3;    //parameter 3
        public boolean selected;    //whether selected
        public boolean effect;    //whether it takes effect
}
```


Various types of materials share this data structure, and the meanings of different types of materials corresponding to each field are shown in the following table:


|**Type** |**Field** |**Combination Beautification** |**Filters** |**Stickers** |**Messages** |
|---|---|---|---|---|---|
|String |category |"composer_node" |"filter" |"sticker" |"msg" |
|String |path |path |path |path |path |
|String |key |Key |*  |RenderKey |*  |
|float |intensity |intensity value |intensity value |*  |*  |
|int |arg0 |single/bi\-directional regulation |*  |*  |arg0 |
|long |arg1 |Select color number |*  |*  |arg1 |
|long |arg2 |*  |*  |*  |arg2 |
|String |arg3 |*  |*  |*  |arg3 |
|boolean |selected |whether selected |whether selected |whether selected |whether selected |
|boolean |effect |whether to take effect |whether to take effect |whether to take effect |whether to take effect |
