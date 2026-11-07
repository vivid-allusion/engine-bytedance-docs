---
title: "Sample debug common settings "
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-e0jc23stjs"
---

Due to the need to replace the assets of sample, debug the sample and see the effect many times in various scenarios, including the process of access testing, this document is specifically designed to summarize and sort out common settings in this debugging sample scenario.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This scenario refers to a scenario where you simply use our provided sample to run trial/official materials to reproduce issue, verify the function, or view the effect. For accessing SDK, please refer to the quick access doc and interface description.</div>


<div data-tips="true" data-tips-type="warning">How to run the sample, please refer to the sample operation guide, if you use the delivered assets and license, please change the bundle ID/application ID to yours in the sample project.</div>


<span id="50e020e1"></span>
## Change the license to yours in sample

First, you need to replace the license and change license config in the sample.

<span id="a2733578"></span>
### **iOS**


1. Change the path of `LICENSE_NAME` in **Config.h**


```C
// Change the file name to your own license file
#define LICENSE_NAME ((const char 
        *)"labcv_test_20220715_20221231_com.effectsar.labcv.demo_4.4.0.licbag")
```



2. Turn off default online license setting.

   1. If the SDK version is v4.2.1, you need to change the `LICENSE_MODE` in **BEEffectLicenseHelper.mm** to `OFFLINE_LICENSE`.

   2. If the SDK is v4.2.3 or above, you need to change the `LICENSE_MODE` in **BELicenseHelper.mm** to `OFFLINE_LICENSE`.

   3. No need to check this setting if the SDK version is before v4.2.1.

3. Modify the bundle ID in Signing&Capabilities in the app settings to the bundle ID of your own developer given in the license authorization.


<span id="cd57a3c6"></span>
### **Android**


1. Change the path of `LICENSE_NAME` in **Config.java**


```Java
// Change the file name to your own license file
    public static final String LICENSE_NAME = "labcv_test_20220715_20221231_com.effectsar.labcv.demo_4.4.0.licbag";
```



2. Turn off default online license setting.

   1. If the SDK version is v4.2.1 or later, you need to change the `_licenseMode` in **EffectLicenseHelper.java** to `LICENSE_MODE_ENUM.OFFLINE_LICENSE`.

   2. No need to check this setting if the SDK version is before v4.2.1.

3. Modify the application ID in build.gradle in the app module to the application ID of your own developer given in the license authorization.


<span id="7f6a0abb"></span>
## Algorithm models replace

Starting from **V4.4.3**, the algorithm model in sample is delivered by the server by default, there will be some misunderstandings when clients debugging sample with delivered material.

This chapter explains how to debug with delivered algorithm models.

<span id="91b58125"></span>
### iOS

**Only run in the sample**

If you simply put your assets and run the sample:

Put the model in the **modelResource/online_model** directory and compile, as shown in the picture:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d0c1c5df68c410081fae536132b5498~tplv-goo7wpa0wc-image.image" width="376px" /></div>


**Upgrade SDK**

If you are using an earlier version, want to upgrade to V4.4.3 and above, and you have copied the **BEEffectResourceHelper.m** file to your project.

You need to modify the code to read the algorithm model.

```C
//Comment out these lines in the code
// - (const char *)modelDirPath
// {
//     NSString *documentDir = [[[NSFileManager defaultManager] URLForDirectory:NSDocumentDirectory inDomain:NSUserDomainMask appropriateForURL:nil create:YES error:nil] path];
//     return [[documentDir stringByAppendingString:@"/BDCV_ModelResource"] UTF8String];
// }

//Add these lines after the comment out code
- (const char *)modelDirPath {
    return [[[NSBundle mainBundle] pathForResource:@"ModelResource" ofType:BUNDLE] UTF8String];
}
```


<span id="ca3ba0d1"></span>
### Android

**Only run in the sample**

If you simply put your assets and run the sample:

Put the model in the **modelResource/online_model** directory and compile, as shown in the picture:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bad361d75c204bd09bdd1f1d0982047e~tplv-goo7wpa0wc-image.image" width="598px" /></div>


**Upgrade SDK**

If you are using an earlier version, want to upgrade to V4.4.3 and above, and you have copied the **AlgorithmResourceHelper.java** file to your project.

You need to modify the code to read the algorithm model.

```Java
//Comment out these lines in the code
// public String getModelPath(){
//         return new File(getResourcePath(), "model").getAbsolutePath();
//     }

//     private String getModelPath(String modelName) {
//         return new File(getModelPath(), modelName).getAbsolutePath();
//     }

//Add these lines after the comment out code
private String getModelPath(String modelName) {
        return new File(new File(getResourcePath(), "ModelResource.bundle"), modelName).getAbsolutePath();
    }
```


<span id="a80dbc59"></span>
## Testing stickers in sample

Starting from **V4.4.3**, the stickers in sample are delivered by the server by default, there will be some misunderstandings when clients debugging sample with delivered material.

This chapter explains how to debug with delivered stickers.

<span id="ebe4277a"></span>
### **iOS**

**V4.4.3 and later**


1. Put the stickers under the **StickerResource.bundle/stickers** folder. If there is no such folder, you can create a new one in the bundle.

2. In **BEStickerVC.m** under the `viewDidLoad` release test local sticker comments, and comment out the code for delivering stickers from server.


```C
- (void)viewDidLoad {
    [super viewDidLoad];
    self.transformBool = NO;
    self.msgcapBool = NO;
    
//  Release this line for testing local stickers
    [self.stickerBoardView setGroups:[self loadLocalStickerResource]];

// Comment out these code of delivering stickers from server
    // NSString *categoryKey = self.effectConfig.title;
    // self.dataManager.delegate = self;
    // [self.dataManager effectDataManagerWithCategoryKey:categoryKey];
}
```


**V4.2.3 to V4.4.2**


1. Put the stickers under the **StickerResource.bundle/stickers** folder. If there is no such folder, you can create a new one in the bundle.

2. In **BEStickerVC.m** under `viewDidLoad`, comment out the code for delivering stickers from server, add the path of a single sticker.


```C
// BEStickerVC.m
- (void)viewDidLoad {
  [super viewDidLoad];
   // Release this line for testing local stickers
  [self.stickerBoardView setGroups:[self stickerPageWithLocalResource:@[
    @"test", @"../sticker/stickername"
  ]].tabs];
  //Comment out this line of delivering stickers from server
//  [_stickerFetch fetchPageWithType:self.effectConfig.stickerConfig.type];
}
```


<span id="07eb4c3c"></span>
### **Android**

**V4.5.0 and later**


1. Change `ENABLE_ASSETS_SYNC` to `false` in **Config.java**

2. Put the sticker folder you need to test under **StickerResource.bundle/local** directory, or if there is no local directory, create a new local folder under bundle. As shown in the figure:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90e9b44bc5a8435bb271140ef3746fc9~tplv-goo7wpa0wc-image.image) </span>

**V4.3.1 to V4.4.3**


1. Put the sticker folder you need to test under **StickerResource.bundle/local** directory, or if there is no local directory, create a new local folder under bundle. As shown in the figure:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad430c991d054caebe125412562c7f69~tplv-goo7wpa0wc-image.image" width="497px" /></div>


**V4.2.3 and V4.3.0**

Search and find the following code in **StickerActivity.java** to add a single sticker that needs to be debugged.

```Java
// com.bytedance.labcv.effect.activity.StickerActivity.java
List<String> info = new ArrayList<String>(){
    {
        //Set up the local test stickers here. Add "Title" and "Path" strings to each sticker in turn
        String stickerRootPath = "/storage/emulated/0/Android/data/com.bytedance.labcv.demo/files/Documents/resource/";
        add(mContext.getString(R.string.sticker_landiaoxueying));
        add(stickerRootPath+"stickers_landiaoxueying");
        add(mContext.getString(R.string.sticker_weilandongrizhuang));
        add(stickerRootPath+"stickers_weilandongrizhuang");
        add(mContext.getString(R.string.sticker_tiaowuhuoji));
        add(stickerRootPath+"stickers_tiaowuhuoji");
    }
};
```
