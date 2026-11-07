---
title: "Reference: Mini Program SDK Package File Structure Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Mini_Program_SDK_Package_File_Structure_Description"
---

<span id="bcf18b9b"></span>
## File list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">As the functions of the SDK continue to iterate, there may be more package files, but the entire directory structure and core files remain essentially unchanged.</div>



|Package file schematic |Package file description |
|---|---|
|root directory<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85ef237508ec49e1ac2f6bf8db55f3fc~tplv-goo7wpa0wc-image.image) </span> |`Package.json`: Configuration information for the package.<br><br>`README.md`: The basic introduction file of the SDK.<br><br>`Index.js`: entry file, es module type, provides export default instance, consistent with 1.x version.<br><br>`Index.d.ts`: is the typescript type file of the default instance exported by index.js.<br><br>`Index.umd.js`: entry file, umd module type, provides export default instance, consistent with 1.x version.<br><br>`Index.umd.d.ts`: is the typescript type file of the default instance exported by index.umd.js.<br><br>`Sdk.d.ts`: The typescript type file of the SDK class, which will be imported and used by other d.ts files.<br><br>`ESM`: Indicates that the files in it are of the es module type.<br><br><br>* `Sdk.js`: Export the SDK class, use all the built\-in plug\-ins by default, and try to support Mini Program multiple platforms at the same time, that is, it can be used on WeChat Mini Program platform, Byte Mini Program platform, Alipay Mini Program platform and other platforms at the same time.<br><br>* `Base.js`: Export SDK classes, but only use some core plug\-ins, and try to support Mini Program multiple platforms at the same time. It can be regarded as the basic version of sdk.js, and optional plug\-ins are removed.<br><br>* `Wx.js`: Similar to base.js, export the basic version of the SDK class, but only support the WeChat Mini Program platform.<br><br>* `Tt.js`: Similar to base.js, exports the base version of the SDK class, but only supports the Byte Mini Program platform.<br><br>* `My.js`: Similar to base.js, export the basic version of the SDK class, but only support the Alipay Mini Program platform.<br><br>* `Qq.js`: Similar to base.js, exports the base version of the SDK class, but only supports the qq Mini Program platform.<br><br>* `Swan.js`: Similar to base.js, export the basic version of the SDK class, but only support the Baidu Mini Program platform.<br><br>* `Xhs.js`: Similar to base.js, export the basic version of the SDK class, but only support the Xiaohongshu Mini Program platform.<br><br>* `Ks.js`: Similar to base.js, exports the base version of the SDK class, but only supports the Kuaishou Mini Program platform.<br><br>* `Jd.js`: Similar to base.js, exports the base version of the SDK class, but only supports the JD.com Mini Program platform.<br><br>* `Tb.js`: Similar to base.js, export the basic version of the SDK class, but only support the Taobao Mini Program platform.<br><br>* `X.d.ts`: a typescript file with the same name as js.<br><br>* `Plugin`: Plugin directory, the plugin file provided by the SDK by default, and the corresponding typescript type file.<br><br><br>`Umd`: indicates that the files in it are all of the umd module type, except for the different module types, the others are the same as esm. |
|Root/esm/plugin<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a13d21480c4d4c9b8284d34a6481c2c1~tplv-goo7wpa0wc-image.image) </span> |`ESM`: Plugin directory, the plugin file provided by the SDK by default, and the corresponding typescript type file.<br><br><br>* `ab.js`: ab experimental function plug\-in, you need to use enable_ab_test parameters to open, after opening the SDK will request the experimental configuration to the ab experimental interface after the initialization is completed, the business can use the api such as getVar to carry out the experimental exposure, the SDK will automatically report abtest_exposure specific events, and the vid of the exposed experiment will also be brought with you when reporting on subsequent events. The default export instance already contains the plug\-in.<br><br>* `Auto.js`: The predefined event automatic reporting plug\-in needs to be opened with auto_report parameters. After opening, the SDK will monitor the relevant life cycle of the Mini Program and obtain relevant information, and automatically report the corresponding predefined events. The default export instance already contains the plug\-in.<br><br>* `compensate.js`: cache plug\-in, after using this plug\-in, the SDK will automatically cache the event tracking that fails to be reported due to network problems to storage and report it after the next SDK initialization. The default export instance already contains the plug\-in.<br><br>* `Utm.js`: ad/ad analysis plugin, start\-up collection utm_source, utm_medium and other related parameters. The default export instance already contains the plug\-in.<br><br>* `Robot.js`: Crawler plug\-in, if it is judged that it is a crawler, it will not report the event, which is currently only valid for the WeChat Mini Program platform.<br><br>* `Encrypt.js`: Encryption plugin, currently only supports state secret encryption, and relies on the corresponding version of the data flow service to support.<br><br>* `Exposure .js`: element exposure plug\-in, automatically collect element exposure events by configuring relevant parameters for elements.<br><br>* `Verify .js`: event tracking real\-time verification plugin, which can be used for event tracking real\-time verification.<br><br>* `X.d.ts`: typescript type file with the same name js<br><br><br>(Some other plug\-ins are left over from history, and the business generally does not involve "personal" use of them, so you can leave it alone.) |


<span id="e2a25722"></span>
## **Further explanation**


1. `Index.js`is a final bundle file that contains all the code for SDK functionality and does not itself depend on any other files. Other files in the package are "refinement" files provided for various usage scenarios, such as the entry files of different platforms, such as various plug\-in files, in order to meet the "customized" usage methods required by different scenarios, `index.js`does not rely on them. `Index.umd.js is`the same as `index.js`, but the module type of the file is different, `index.js`is the esm module type, `index.umd.js`is the umd module type.

2. The SDK exports a default instance that contains "almost" all of the SDK's features, including most plug\-ins. When importing in different places, it is usually the same instance, unless it is imported multiple times in different subcontracts.

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   ```
   

   `$$Sdk`is the default instance of SDK export.

3. `esm/sdk.js`The exported SDK "class" contains "almost" all SDK functions and most plugins. The default instance is instantiated using it, which is new.

   ```TypeScript
   import SDK from '@datarangers/sdk-mp/esm/sdk';
   const $$sdk = new SDK();  
   
   //equal to this default instance
   // import $$sdk from '@datarangers/sdk-mp';
   ```
   

4. `esm/base.js`Exports are also SDK "classes", but only include important basic SDK functions and only core plugins. `esm/sdk.js`essentially "inherits" `esm/base.js`and tries to include most plugins.

   Although it is a base "class", `init`, `config`, `send`, `event`and other APIs are no different from sdk "classes".

   ```TypeScript
   import BaseSDK from '@datarangers/sdk-mp/esm/base';
   const $$baseSdk = new BaseSDK(); 
   $$baseSdk.init({
       app_id: 0000,
       log: true,
   });
   $$baseSdk.send();
   $$baseSdk.event('test', {});
   ```
   

   If you need the capabilities of a plugin, you can customize the export of that plugin and register it. For example, the auto plug\-in (collecting preset events):

   ```TypeScript
   import BaseSDK from '@datarangers/sdk-mp/esm/base';
   
   //import auto plugin and register
   import Auto from '@datarangers/sdk-mp/esm/plugin/auto';
   BaseSDK.usePlugin(Auto);
   
   const $$baseSdk = new BaseSDK(); 
   $$baseSdk.init({
       app_id: 0000,
       log: true,
       //Enable the auto function
       auto_report: true,
   });
   $$baseSdk.send();
   $$baseSdk.event('test', {});
   ```
   

   For example, the verify plugin (for event tracking real\-time verification):

   ```TypeScript
   import BaseSDK from '@datarangers/sdk-mp/esm/base';
   
   //Import the verify plugin and register
   import Verify from '@datarangers/sdk-mp/esm/plugin/verify';
   BaseSDK.usePlugin(Verify);
   
   const $$baseSdk = new BaseSDK(); 
   $$baseSdk.init({
       app_id: 0000,
       log: true,
       // ......
   });
   $$baseSdk.send();
   $$baseSdk.event('test', {});
   ```
   

5. If you think the package size of the SDK is relatively large, you need to consider the following methods:

   * When using the default way of importing the SDK, in theory only `index.js`is packaged into the final Mini Program application package (in the Mini Program developer tools, you need to check "Filter no dependencies when uploading", the location of this check: Mini Program developer tools \- \> Details \- \> Local settings).

   * If you feel that the main package of the Mini Program is already relatively large, you can consider using the SDK in the Mini Program subcontract. For details on how to use it in the subcontract, please refer to the "Use in the Mini Program Subcontract" content in the "Function Use in Various Scenarios" of this document.

   * If you want to further reduce the volume, you can refer to the description of `esm/base.js`in paragraph 4 above.
