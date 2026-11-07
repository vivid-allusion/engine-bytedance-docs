---
title: "Sample Operation Guide - iOS - VE"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-operation-guide-ios-ve-v.4.0.2"
---

<span id="46f1643e"></span>
# Local environment

Components required:


* CocoaPods

* Xcode


<span id="b7737869"></span>
# Procedure


1. Unzip **VE\-iOS\-2.2\-20210617.zip**.

2. Open the folder and run **pod repo update**.

3. Run **pod install**.

4. Open **TTVideoEditorDemo.xcworkspace**.


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/a170e2bbfac14e57bbecea8346eaaaae~tplv-em5hxbkur4-noop.image) </span>

<span id="711aee9d"></span>
# Precautions:

<span id="2c41061e"></span>
### Do not change the bundle ID

The VE SDK adopts an authentication mechanism that verifies the bundle ID. If necessary, you may apply for additional authorization.

<span id="22059856"></span>
### Pay attention to the authorization period

If the time on your mobile device is not within the authorization period, the VE SDK cannot run on the device. For example, in **pathForResource:@"ve_test_20210222_20210822_com.IESVideoEditor.demo.inhouse_v1.0.1"ofType:@"licbag"]** , the authorization period is **2021/02/22 \- 2021/08/22**.
