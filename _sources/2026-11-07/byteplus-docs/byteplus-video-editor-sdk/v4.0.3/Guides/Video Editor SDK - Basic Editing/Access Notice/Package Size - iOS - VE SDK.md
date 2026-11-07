---
title: "Package Size - iOS - VE SDK"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-package-size-ios-ve-sdk"
---

<span id="Size details of the VEToB960-iOS package"></span>
## Size details of the VEToB960\-iOS package


| |armv7 |arm64 |
|---|---|---|
|size in Payload |59 MB |63.5 MB |
|size in IPA |19 MB |19.6 MB |


<span id="Minimize the package size"></span>
## Minimize the package size


1. Delete the asset files and model files that you do not need. You can use the provided model files as needed.

2. The package supports two frameworks: ARMv7 and ARM64. You can delete the files related to the framework that you do not need. For example, if you need to integrate the package into a 64\-bit framework, you can delete the files related to the ARMv7 framework.


In Xcode, complete the configurations marked in the following figure.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/bb0f4a3590734089b73d6ac5896e9fc6~tplv-em5hxbkur4-noop.image?width=2604&height=1518) </span>
