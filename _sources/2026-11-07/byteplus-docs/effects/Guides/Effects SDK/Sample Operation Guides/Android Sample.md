---
title: "Android Sample"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-android-sample"
---

<span id="Sample (for Android) Operating Guide"></span>
# Sample (for Android) Operating Guide

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If your SDK version is <strong>4.2.1 or later</strong>, the <strong>_licenseMode</strong> in the <strong>EffectLicenseHelper.java</strong> is by default <strong>LICENSE_MODE_ENUM.ONLINE_LICENSE</strong>. You can run the sample code successfully without any effort as the online licensing is switched on by default.</div>


<div data-tips="true" data-tips-type="danger">If you would like to use offline licensing, you need to change the <strong>_licenseMode</strong> in the <strong>EffectLicenseHelper.java</strong> to <strong>LICENSE_MODE_ENUM.OFFLINE_LICENSE</strong>, and modify <strong>Config.LICENSE_NAME</strong> to your own trial license matched application ID, with the resource bundles changed to your own matched trial license ones.</div>


<div data-tips="true" data-tips-type="danger">If your SDK version is before 4.2.1, you do not need to switch the license mode as it is offline by default.</div>


<span id="Local Environment Configuration"></span>
### Local Environment Configuration

ndk **21.1.6352462**

cmake **3.6.4111459**

If you use other versions and the compilation fails, switch to the above ndk and cmake versions.

<span id="Instructions for checking the ndk and cmake versions"></span>
### Instructions for checking the ndk and cmake versions

In Android Studio \- Preferences \- System Settings \- Android SDK \- SDK Tools, check the box "Show Package details".

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/129a3a2-dce2ec56-b9ea-431c-bfcf-88dbc34a7731.png) </span>

<span id="Procedure"></span>
### Procedure


1. Decompress androidsample.zip.

2. In Android Studio "Open an Existing Project" and choose the BytedEffects folder (If you are copying the Android project to another directory, copy the files in the androidsample directory as well)


Copy the androidsample directory and its files:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0b3bce3-1.png) </span>

Do not only copy the BytedEffects file:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/d690bb4-2.png) </span>

3. Modify the values for sdk.dir and ndk.dir in the the local.properties file to point to the correct path

```Plain
sdk.dir=/Users/it260503/Library/Android/sdk
ndk.dir=/Users/it260503/Library/Android/sdk/ndk/21.1.6352462
```



4. Run the project.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The application will not run in an emulator and will require a physical device.</div>


<span id="Precautions"></span>
### Precautions

<span id="Do Not Change the gradle Version"></span>
#### Do Not Change the gradle Version

The sample package of the CV SDK contains the specified gradle version. Do not change this version in the sample; otherwise ndk incompatibility or other issues may occur.

<span id="Do Not Change the Application ID"></span>
#### Do Not Change the Application ID

The CV SDK verifies applicationId and requires additional licensing if necessary. If you just run the sample without replacing material to your own resources and license, you'd better do not change the application id.

<span id="License Time"></span>
#### License Time

If the phone time is not within the license period, calls to the CV SDK will fail. For the specific license time, refer to the middle part of com.bytedance.labcv.demo.core.v4.effect.EffectResourceHelper#LICENSE_NAME.

For example, labcv_test_20201201_20210228_com.bytedance.labcv.demo_v4.0.2.0.licbag indicates that the license period is from December 1, 2020 to February 28, 2021.

<span id="Local Sticker (Only for version 4.2.3 and later)"></span>
#### Local Sticker (Only for version 4.2.3 and later)

If you want to load the local stickers when you run the sample of **version 4.2.3 and later** with **your own material**, you need to go to the `com.bytedance.labcv.effect.activity.StickerActivity.java` to switch the default online sticker to the local ones.

```Plain
        //For the example of loading local stickers, use this code instead of the code in the "Remote Material Delivery" section
        List<String> info = new ArrayList<String>(){
            {
                String stickerRootPath = "/storage/emulated/0/Android/data/YourApplicationID/files/assets/resource/StickerResource.bundle/";
                add(mContext.getString(R.string.sticker_landiaoxueying));
                add(stickerRootPath+"stickers/landiaoxueying");
                add(mContext.getString(R.string.sticker_weilandongrizhuang));
                add(stickerRootPath+"stickers/baibianfaxing");
            }
        };
        StickerPage page = stickerPageWithLocalResource(info);
        mFragment.setData(Arrays.asList(page.getTabs()));

       //  Remote Material Delivery
//        mStickerFetch = new StickerFetch();
//        mStickerFetch.setListener(this);
//        try {
//            mStickerFetch.fetchPageWithType(this, mStickerConfig.getType().getName());
//        } catch (PackageManager.NameNotFoundException e) {
//            e.printStackTrace();
//        }
```
