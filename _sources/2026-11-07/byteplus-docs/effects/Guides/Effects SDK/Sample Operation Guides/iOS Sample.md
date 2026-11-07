---
title: "iOS Sample"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ios-sample"
---

<span id="Sample (for iOS) Operating Guide"></span>
# Sample (for iOS) Operating Guide

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">If your SDK version is <strong>4.2.1 or later</strong>, the <strong>LICENSE_MODE</strong> in the <strong>BELicenseHelper.mm</strong> is by default <strong>ONLINE_LICENSE</strong>. You can run the sample code successfully without any effort as the online licensing is switched on by default.</div>


<div data-tips="true" data-tips-type="danger">If you would like to use offline licensing, you need to change the <strong>LICENSE_MODE</strong> in the <strong>BELicenseHelper.mm</strong> to <strong>OFFLINE_LICENSE</strong>, and modify <strong>LICENSE_NAME</strong> in <strong>Config.h</strong> to your own trial license matched application ID, with the resource bundles changed to your own matched trial license ones.</div>


<div data-tips="true" data-tips-type="danger">If your SDK version is before 4.2.1, you do not need to switch the license mode as it is offline by default.</div>


<span id="Local Environment Configuration"></span>
### Local Environment Configuration

Components to be installed:


* CocoaPods

* Xcode


<span id="Procedure"></span>
### Procedure


1. Decompress iossample.zip.

2. Open the folder and execute "pod repo update".

3. Execute "pod install".

4. Open BytedEffects.xcworkspace.


<span id="Precautions"></span>
### Precautions

<span id="Do Not Change the Bundle ID"></span>
#### Do Not Change the Bundle ID

The CV SDK verifies bundle IDs and requires additional licensing if necessary. If you just run the sample without replacing material to your own resources and license, you'd better do not change the bundle id.

<span id="License Time"></span>
#### License Time

If the phone time is not within the license period, calls to the CV SDK will fail. For the specific license time, refer to the middle part of BEResourceHelper#LICENSE_NAME. For example, labcv_test_20201201_20210228_com.bytedance.labcv.demo_ v4.0.2.0.licbag indicates that the license period is from December 1, 2020 to February 28, 2021.

<span id="Load local stickers (Only for version 4.2.3 and later)"></span>
#### Load local stickers (Only for version 4.2.3 and later)

If you want to load the local stickers when you run the sample of **version 4.2.3 and later** with **your own material**, you need to go to the `BEStickerVC` to switch the default online sticker to the local ones.

```objectivec
// BEStickerVC.m
- (void)viewDidLoad {
  [super viewDidLoad];
   
  [self.stickerBoardView setGroups:[self stickerPageWithLocalResource:@[
    @"test", @"../sticker/stickername"
  ]].tabs];
//  [_stickerFetch fetchPageWithType:self.effectConfig.stickerConfig.type];
}
```


`BEStickerVC` provides a method `stickerPageWithLocalResource` for quickly generating a local resource, you need to pass in an array of strings, the contents of the array are sticker name, sticker path, sticker name2, sticker path2 in that order. Use this method to generate a `BEStickerPage` and then pass it directly to `stickerBoardView`.
