---
title: "HarmonyOS NEXT Upload SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-harmonyos-upload-sdk-quickstart"
---

This page introduces how to integrate the HarmonyOS NEXT Upload SDK, including environment preparation and integration operations.

<span id="3928c463"></span>
## Environment requirements


* Operating system: HarmonyOS Next Developer Beta2 and above

* Development tools: DevEco\-Studio


<span id="28df68e5"></span>
## Add repositories

Create the `.ohpmrc` file in the root directory of the project and configure the OpenHarmony third\-party library center and BytePlus repository address.

```Plain
registry=https://ohpm.openharmony.cn/ohpm/
@bytedance:registry=https://artifact.byteplus.com/repository/byted-ohpm/
```


<span id="957eaf40"></span>
## Add SDK dependencies

Add SDK dependencies to the `on-package.json5` file under the `/entry` directory of the module that requires the upload SDK.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Replace <code>x.x.x-bp</code> with the version number. To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-harmonyos-upload-sdk-changelog">HarmonyOS NEXT Upload SDK: Release notes</a>.</div>


```JSON
"dependencies": {
  "@bytedance/bduploader": "x.x.x-bp"
}
```
