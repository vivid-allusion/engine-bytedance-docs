---
title: "iOS License Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ios-license-guide"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following uses the special effects demo 3.9.0 as an example, and the paths may vary depending on your actual project.</div>


<span id="Step 1: Use the obtained license and material files to replace the resource files in byted_effect_ios/iossample/ByteEffects/Resource."></span>
## Step 1: Use the obtained license and material files to replace the resource files in byted_effect_ios/iossample/ByteEffects/Resource.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/112dd59-1.png) </span>

<span id="Step 2: Change LICENSE_NAME in the BEResourceHelper.m class to the currently used license file name."></span>
## Step 2: Change LICENSE_NAME in the BEResourceHelper.m class to the currently used license file name.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/4012de4-2.png) </span>

<span id="If the licensing fails, troubleshoot as follows:"></span>
### If the licensing fails, troubleshoot as follows:


* Check whether the system time of the mobile phone is correct.

* Check whether the bundle ID matches the licensed package name.

* Check whether the license path is correct and correctly read by the SDK.

* If the problem persists, check the error type logs output with the following tags:


**bef_effect_ai, SMASH_E_LOG, and EffectSDK** .

Then check the corresponding description and solution provided in [Error Code Table](https://byteplus-docs.readme.io/effects/docs/error-code-table).
