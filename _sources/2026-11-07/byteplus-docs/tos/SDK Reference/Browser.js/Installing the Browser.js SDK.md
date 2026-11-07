---
title: "Installing the Browser.js SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-the-browser-js-sdk"
---

This article outlines the preparatory steps and installation procedures for the Browser.js SDK.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparatory Work


* Access via STS: Since the AccessKey of a BytePlus account grants permissions to all APIs, if you deploy on the client side, it is recommended to use STS for temporary access to TOS. For more information, please refer to [Using STS Temporary AK/SK+Token to Access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Configure Cross\-Origin Resource Sharing (CORS): For detailed instructions, please refer to [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).

   When accessing TOS directly via a browser, the CORS configuration rules are required as follows:

   
   |Parameter |Description |
   |---|---|
   |Origin |Set a precise domain name (for example, `https://console.volcengine.com`) or a wildcard asterisk (\*). |
   |Operation methods |Please select different Methods according to the actual usage scenario. For example, set to **PUT** when performing multipart uploads; set to **DELETE** when deleting files. |
   |Allow\-Headers |Set to`*`  |
   |Expose\-Headers |Set to `ETag`, `x-tos-request-id`, and `x-tos-version-id`. |
   

&nbsp;


<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK Download Link

TOS Browser.js SDK source code address: please refer to [TOS Browser.js SDK](https://github.com/volcengine/ve-tos-js-sdk).

<span id=".5pSv5oyB55qE5rWP6KeI5Zmo"></span>
## Supported Browsers

The following browsers are supported by the TOS Browser.js SDK:


* Internet Explorer version 10 and above

* Edge

* Mainstream versions of Chrome, Firefox, and Safari

* Default browsers of mainstream versions of the Android, iOS, and Windows Phone operating systems


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Due to the specific constraints of the browser environment, the TOS Browser.js SDK cannot utilize the following features:


* Operating Local Files: Browsers cannot directly access the local file system. It is recommended to use pre\-signed URLs to download files.

* Since TOS temporarily does not support cross\-origin requests related to Buckets, it is recommended that you perform Bucket\-related operations in the [TOS Console](https://console.byteplus.com/tos).


<span id=".5a6J6KOFLXNkaw=="></span>
## Install the SDK

<span id=".5rWP6KeI5Zmo5byV5YWl"></span>
### Browser Introduction

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">As some browsers do not support Promise, you need to include a Promise compatibility library during installation. For example, IE10 and IE11 require the inclusion of <code>promise-polyfill</code>.</div>


* <div data-tips="true" data-tips-type="warning">The method of incorporating online resources relies on the stability of CDN servers. Therefore, it is recommended to adopt offline integration, either by utilizing local resources or by building the resources independently.</div>


* Introduction of Online Resources

   ```html
   <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
   ```
   

* Incorporating local resources

   ```html
   <script src="./tos.umd.production.min.js"></script>
   ```
   


Utilize the TOS object in the code.

```html
<script type="text/javascript">
  const client = new TOS({
    accessKeyId: 'Your Access Key',
    accessKeySecret: 'Your Secret Key',
    stsToken: 'Your Session Token',
    region: 'Your Region',
    bucket: 'Your Bucket',
  });
</script>
```


<span id=".5L2_55SoLW5wbS15YXJuLeWuieijhS1zZGs="></span>
### Installing the SDK via npm or yarn


* Install using `npm`

   ```bash
   npm i @volcengine/tos-sdk
   ```
   

* Install using `yarn`

   ```bash
   yarn add @volcengine/tos-sdk
   ```
   


After successful installation, you can use import or require to import. You can use the following commands to import the SDK. Note that there are differences between importing modules using ES6 import statements and CommonJS (CJS) import commands.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When using <code>import</code> or <code>require</code>, you need to use relevant bundling tools in the development environment, such as <code>webpack</code>, <code>browserify</code>, etc.</div>



* Use `import` to perform an import

   ```javascript
   import TOS from '@volcengine/tos-sdk';
   ```
   

* Use `require` to import

   ```javascript
   const { TOS } = require('@volcengine/tos-sdk');
   ```
   


Use the TOS object in the code.

```html
<script type="text/javascript">
  const client = new TOS({
    accessKeyId: 'Your Access Key',
    accessKeySecret: 'Your Secret Key',
    stsToken: 'Your Session Token',
    region: 'Your Region',
    bucket: 'Your Bucket',
  });
</script>
```
