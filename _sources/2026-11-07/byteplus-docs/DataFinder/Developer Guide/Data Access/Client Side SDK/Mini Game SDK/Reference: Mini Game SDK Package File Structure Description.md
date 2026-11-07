---
title: "Reference: Mini Game SDK Package File Structure Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Mini_Game_SDK_Package_File_Structure_Description"
---

<span id="bcf18b9b"></span>
## File list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">As the functions of the SDK continue to iterate, there may be more package files, but the entire directory structure and core files remain essentially unchanged.</div>



|Package file schematic |Package file description |
|---|---|
|root directory<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2c6253dcf5c4e67984af9b24becd325~tplv-goo7wpa0wc-image.image) </span> |`Package.json`: Configuration information for the package.<br><br>`README.md`: The basic introduction file of the SDK.<br><br>`Index.js`: entry file, es module type, provides export default instance.<br><br>`Index.d.ts`: is the typescript type file of the default instance exported by index.js.<br><br>`Index.umd.js`: entry file, umd module type, provides export default instance.<br><br>`Index.umd.d.ts`: is the typescript type file of the default instance exported by index.umd.js.<br><br>`Sdk.d.ts`: The typescript type file of the SDK class, which will be imported and used by other d.ts files.<br><br>`ESM`: Indicates that the files in it are of the es module type.<br><br><br>* `Sdk.js`: export SDK class, the default use of all built\-in plug\-ins, itself as much as possible to support small game multi\-platform, that is, at the same time in WeChat small game platform, Byte small game platform, Baidu small game platform and other platforms.<br><br>* `Base.js`: export SDK class, but only use some core plug\-ins, itself is also try to support small games at the same time multi\-platform, can be seen as the basic version of sdk.js, remove the optional plug\-ins.<br><br>* `Wx.js`: Similar to base.js, export the basic version of the SDK class, but only support the WeChat mini\-game sequence platform.<br><br>* `Tt.js`: Similar to base.js, exports the base version of the SDK class, but only supports the ByteDance platform.<br><br>* `Qq.js`: Similar to base.js, export the basic version of the SDK class, but only support the qq small game platform.<br><br>* `Swan.js`: Similar to base.js, export the basic version of the SDK class, but only support Baidu small game platform.<br><br>* `Qg.js`: Similar to base.js, exports the basic version of the SDK class, but only supports fast game platforms.<br><br>* `X.d.ts`: a typescript file with the same name as js.<br><br>* `Plugin`: Plugin directory, the plugin file provided by the SDK by default, and the corresponding typescript type file.<br><br><br>`Umd`: indicates that the files in it are all of the umd module type, except for the different module types, the others are the same as esm. |
|Root/esm/plugin<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b500d51c534a9993c9998cc65d1b60~tplv-goo7wpa0wc-image.image) </span> |`ESM`: Plugin directory, the plugin file provided by the SDK by default, and the corresponding typescript type file.<br><br><br>* `ab.js`: ab experimental function plug\-in, you need to use enable_ab_test parameters to open, after opening the SDK will request the experimental configuration to the ab experimental interface after the initialization is completed, the business can use the api such as getVar to carry out the experimental exposure, the SDK will automatically report abtest_exposure specific events, and the vid of the exposed experiment will also be brought with you when reporting on subsequent events. The default export instance already contains the plug\-in.<br><br>* `Auto.js`: Predefined event automatic reporting plug\-in, need to use auto_report parameters to open, after opening the SDK will monitor the game related life cycle and obtain relevant information, and automatically report the corresponding predefined events. The default export instance already contains the plug\-in.<br><br>* `compensate.js`: cache plug\-in, after using this plug\-in, the SDK will automatically cache the event tracking that fails to be reported due to network problems to storage and report it after the next SDK initialization. The default export instance already contains the plug\-in.<br><br>* `Utm.js`: ad/ad analysis plugin, start\-up collection utm_source, utm_medium and other related parameters. The default export instance already contains the plug\-in.<br><br>* `X.d.ts`: typescript type file with the same name js<br><br><br>(Some other plug\-ins are left over from history, and the business generally does not involve "personal" use of them, so you can leave it alone.) |


<span id="e2a25722"></span>
## **Further explanation**


1. `Index.js`is a final bundle file that contains all the code for SDK functionality and does not itself depend on any other files. Other files in the package are "refinement" files provided for various usage scenarios, such as the entry files of different platforms, such as various plug\-in files, in order to meet the "customized" usage methods required by different scenarios, `index.js`does not rely on them. `Index.umd.js is`the same as `index.js`, but the module type of the file is different, `index.js`is the esm module type, `index.umd.js`is the umd module type.

2. The SDK exports a default instance that contains "almost" all of the SDK's features, including most plug\-ins. When importing in different places, it is usually the same instance, unless it is imported multiple times in different subcontracts.

   ```TypeScript
   import $$sdk from '@datarangers/sdk-qg';
   ```
   

   `$$Sdk`is the default instance of SDK export.

3. `esm/sdk.js`The exported SDK "class" contains "almost" all SDK functions and most plugins. The default instance is instantiated using it, which is new.

   ```TypeScript
   import SDK from '@datarangers/sdk-qg/esm/sdk';
   const $$sdk = new SDK();  
   
   //equal to this default instance
   // import $$sdk from '@datarangers/sdk-qg';
   ```
   

4. `esm/base.js`Exports are also SDK "classes", but only include important basic SDK functions and only core plugins. `esm/sdk.js`essentially "inherits" `esm/base.js`and tries to include most plugins.

   Although it is a base "class", `init`, `config`, `send`, `event`and other APIs are no different from sdk "classes".

   ```TypeScript
   import BaseSDK from '@datarangers/sdk-qg/esm/base';
   const $$baseSdk = new BaseSDK(); 
   $$baseSdk.init({
       app_id: 0000,
       log: true,
   });
   $$baseSdk.send();
   $$baseSdk.event('test', {});
   ```
   

   If you need the capabilities of a plugin, you can customize the export of that plugin and register it. For example, the AB plugin:

   ```TypeScript
   import BaseSDK from '@datarangers/sdk-qg/esm/base';
   
   //Import ab plugin and register
   import AB from '@datarangers/sdk-qg/esm/plugin/ab';
   BaseSDK.usePlugin(AB);
   
   const $$baseSdk = new BaseSDK(); 
   $$baseSdk.init({
       app_id: 0000,
       log: true,
       //enable ab function
       enable_ab_test: true, 
   });
   $$baseSdk.send();
   $$baseSdk.event('test', {});
   ```
   

5. If you think the package size of the SDK is relatively large, you need to consider the following methods:

   * With the default import SDK approach, only `index.js`is theoretically packaged into the final mini\-game application package.

   * If you feel that the main package size of your mini\-game is already relatively large, you can consider using the SDK in the mini\-game subcontract.

   * If you want to further reduce the volume, you can refer to the description of `esm/base.js`in paragraph 4 above.
