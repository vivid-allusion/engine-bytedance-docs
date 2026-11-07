---
title: "FAQ during Building an Electron App"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1133953"
---

This document offers recommended solutions for a list of common error messages that you may encounter while building and commissioning your app with Electron SDK.

<span id="installation"></span>
## Installation

<span id="connect-etimeout"></span>
### `connect ETIMEOUT`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6dca2cf3c1f45b69048a5f53ef60481~tplv-goo7wpa0wc-image.image) </span>

<span id="recommended-solutions"></span>
#### Recommended solutions


1. Ensure your network connection to the npm host is available.

2. Upgrade your Node.js version.


<span id="npm-err！invalid-version"></span>
### `Npm ERR! Invalid Version`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e0d02fc978c4eeaa200a52bbf9c2110~tplv-goo7wpa0wc-image.image) </span>

<span id="recommended-solutions"></span>
#### Recommended solutions


1. Upgrade your NPM version.

2. Reinstall the dependencies after emptying the node_modules folder.


<span id="packing"></span>
## Packing

<span id="module-parse-failed-unexpected-character-1-0"></span>
### `Module parse failed: Unexpected character '?(1:0)`

"You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file"

<span id="recommended-solutions"></span>
#### Recommended solutions

It seems that you do not have the loader configured correctly.

Refer to the packing settings in the [sample project](https://docs.byteplus.com/en/docs/12/docs-1163793). We recommend you use `native-ext-loader` to pack your project. Copy `node_modules/@byteplus/byteplus-electron-sdk/build/release` to `app/vertc`, and set the loader's `basePath` to `vertc`. Refer to [Pack your application](https://docs.byteplus.com/en/docs/12/docs-108795#_4-pack-your-application) for detailed instructions.

<span id="library-not-loaded"></span>
### `Library not loaded:`

```Plain
Library not loaded:
@rpath/
 Reference from: /Application/BjmantisOnlineclass.app/Contents/Resources/electron-sdk.node
Reason: image not found
    at Object.<anonymous> (2.aa100786.chunk.js:2)
    at Object.<anonymous> (2.aa100786.chunk.js:2)
    at l (index.html:1)
```


<span id="recommended-solutions"></span>
#### Recommended solutions

Ensure the RTC SDK has been packed into your App.

We recommend including RTC SDK in your App folder by executing the copySdkAddon script provided in the [sample project](https://docs.byteplus.com/en/docs/12/docs-1163793). The script copies the SDK native module to `app/vertc`; the same directory must be configured in `native-ext-loader` and `asarUnpack`. Refer to [Pack your application](https://docs.byteplus.com/en/docs/12/docs-108795#_4-pack-your-application) for detailed instructions.

<span id="running"></span>
## Running

<span id="electron-sdk-node-is-not-a-valid-win32-application"></span>
### `electron-sdk.node is not a valid Win32 application`

```Plain
Error:\\?
D:\Users\Administrator\AppData\Local\Programs\ElectronApp\resources\app\node_modules\@bytePlus\bytePlus-electron-sdk\build\Release\electron-sdk.node is not a valid Win32 application
```


<span id="recommended-solutions"></span>
#### Recommended solutions


1. Include the following snippet in the package.json for your project.


```json
"byteplus_electron": {
        "arch": "ia32",
        "prebuilt": true
    }
```



2. For Windows, run the following command to install the proper environment for a 32\-bit Windows device.


```powershell
npm install --arch=ia32 electron 
```


> Proceed with the installation after emptying the node_modules folder.


<span id="getting-systempreferences-is-not-defined-when-checking-the-permission"></span>
### Getting `systemPreferences is not defined` when checking the permission.

<span id="recommended-solutions"></span>
#### Recommended solutions

Import `systemPreferences` to request camera and microphone access on macOS.

```javascript
const { systemPreferences } = require('electron');
```
