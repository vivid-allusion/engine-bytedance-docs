---
title: "Reference: HarmonyOS Next SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_HarmonyOS_Next_SDK_Integration_FAQ"
---

<span id="9275f7ef"></span>
# Support environment

Answer: And the corresponding environment needs to integrate a specific SDK, otherwise there will be problems.


|Environment |Whether to support |Remarks |
|---|---|---|
|Volcano Cloud/Privatization 4.9.2 and later |Supported |The environment has been adapted and the platform is reported as openHarmony.<br><br>**If privatization is upgraded to 4.9.2, you need to replace the sdk to change the platform to Hongmeng** |
|ByteCloud |Not supported |The environment has not been adapted. If you want to integrate early, the platform of the SDK will be reported as Android. |
|Before privatization 4.9.2 |Not supported ||


<span id="b2291748"></span>
# Why do I lose event tracking after I clean my cache?

Answer: The official cache cleaning example will cause AppLog data to be lost together, see: [How do I flush HiLog information?](https://developer.huawei.com/consumer/en/doc/harmonyos-faqs/faqs-performance-analysis-kit-1)

<span id="e0e6b29e"></span>
# Minimum required version of Hongmeng SDK integration

Answer: API12 (Developer Beta3) or above.

<span id="322792a7"></span>
# Does it support AB?

Answer: support.

<span id="9f022eed"></span>
# What is the Pako in the document used for?

Answer: The gzip tool officially recommended by Hongmeng, the current system does not have a ready\-made gzip interface, and it is recommended to use pako dependency. The SDK has request encryption inside, and the encryption is accompanied by gzip, so it is necessary to rely on it.

<span id="15f7ef71"></span>
# Our company has built a private warehouse. Do you want a pako har to provide it?

A: Yes, just ask me for it. In the analogy of pako, online dependence is required. If the customer environment cannot be relied on online, offline packages can be provided.

<span id="288bd975"></span>
# ERROR: ArkTS: ERROR Failed to resolve OhmUrl.

Error Message: Failed to get a resolved OhmUrl for "pako" imported by "/Users/bytedance/Downloads/package/HarmonyAppLogTest/oh_modules/.ohpm/@volcengine+applog@dtz2fnlu+kogyshzrapysfd0wcm=/oh_modules/@volcengine/applog/src/main/ets/core/network/interceptor/CompressAndEncryptInterceptor.js".

Answer: Pako is not dependent.

<span id="cf08de02"></span>
# Why can't Devtools be as easy to use as Android?

Answer: Global floating windows with child window mode are supported

<span id="9ea819e4"></span>
# What features are supported?

Answer: It is mainly based on external documents, and everything written on the documents is supported.


* Custom event tracking/request encryption (default encryption/national secret sm2)/user ID and user properties/AB shunt experiment/event blacklist/web get through/crash collection (JS layer)/real\-time event tracking verification/custom header settings, etc

* DevTools Debugging Tools

   * view event information/view network request/view access status/debug log/configuration information module/built\-in scan and other functions


<span id="1bfc4900"></span>
# When is full event tracking/exposure supported?

A: 1.3.3 \-rc3 version is supported.

<span id="b956ea19"></span>
# Why doesn't Hongmeng SDK have an SSID acquisition method?

Answer: Hongmeng SDK considers gradually removing the SSID maintenance logic on the end, and there is no SSID on the end. The SSID reporting of the event is supplemented by the data flow.

Supplement: 1.3.1 provides ssid logic through the current uuid request, see [Request SSID](https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration_Scenario_Practice#c62f7a0f).

<span id="3cc7ef89"></span>
# What is Hongmeng's reporting strategy?

Answer: The default is also reported once a minute, but there is no specific number of reports, SDK strategy for the new reporting strategy by volume query events (Android/iOS query by the number of queries), each report query about 1M data to report, no longer 200 shall prevail (can be reported as much as possible).

<span id="2e50c8ef"></span>
# Is there a switch for collecting OAID/carrier information?

A: 1.3.0 provides the corresponding switch.

<span id="074cea0c"></span>
# Does it support multithreading/multiprocessing?

Answer: Multi\-threading/multi\-process is not supported for the time being. The Hongmeng system is special and adopts inter\-thread process isolation, which requires an additional adaptation plan.

<span id="4ef10597"></span>
# Integration devtool error

1 ERROR: ArkTS:ERROR Failed to resolve OhmUrl.

Error Message: Failed to get a resolved OhmUrl for "@volcengine/applog" imported by "/Users/bytedance/DevecostudioProjects/SDK50/oh_modules/.ohpm/@volcengine+applog_devtools@7hba3+yrkmv76lfmmoxyslxamstpksemeh++r+9qtz8=/oh_modules/@volcengine/applog_devtools/src/main/ets/plugin/DevTools.js".

**Case 1: AppLog introduces a wrong name**

Answer: The main reason for encountering this problem is that when relying on components, the names of the previous components can actually be written arbitrarily, but the agreement between applog and devtools is specific, which is written as @ **volcengine/applog** . Please check whether the name of the AppLog dependency is written correctly. Please strictly follow the documentation integration.

//Import AppLog strictly by that name

 **"@volcengine/applog"** : "file:../applogx/applogx.har",

"@volcengine/applog_devtools": "file:../applogx/applogx_devtools.har"

**Situation 2: AppLog is depended on in the sub\-module, and the sub\-module is also depended on by other modules and finds an error.** 

Answer: Since Hongmeng does not support dependency passing, the SDK you rely on in a sub\-module cannot be referenced by other modules. Please add dependencies to the corresponding module.

Example: Sub\-modules depend on applog, entry depends on sub\-modules, please also add applog complete dependencies to the entry module.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebf693de1d7f40e9a7634a355bf0d6c3~tplv-goo7wpa0wc-image.image) </span>

<span id="0a8bf6af"></span>
# Cannot read property eventHub of undefined

Answer: The context for initializing the SDK is incorrect.

<span id="c906c4ed"></span>
# Integrated SDK card

A: You can remove Devtools and try again 1.1.0 \-beta2~ 1.1.0 \-beta3 will have this problem, please upgrade to the 1.3.0 \-xxx version later.

<span id="2cb29bb0"></span>
# Could not find  **@volcengine/applog**

A: It may be caused by the upgrade of regular customers. The previous document stated that the import is @ohos/applog. You need to adjust the import name and refer to the latest document.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54c5247bd6e145289de80e04237164b9~tplv-goo7wpa0wc-image.image) </span>

<span id="c1637891"></span>
# Upgrade only DevTools prompts Can't find BavEvent?

Answer: Due to the adaptation of new features, AppLog and devtools need to be upgraded to 1.2.0 \-xx version, only upgrading Devtools is not possible.

<span id="4e627d36"></span>
# Import {DevTools} from '@volcengine/applog_devtools' error not found

A: 1.2.0 new version of the program adjustment, no need to manually in each page additional mount, changed to Android's global pop\-up mode, so remove the old integration program, basically the new program without additional mount and open the App can have a floating window, if you enter do not see the switch to the background and then come in you can see (listening window active open Devtools so enter the beginning did not see may be initialization time is relatively late).

<span id="18c69546"></span>
# In the case that the customer already has Bridge, how to deal with the solution in the document when it cannot satisfy the customer?

Answer: The original document had two plans. The other plan supported additional injection bridges, but the implementation of the plan may depend on the customer's own decision.

The first way is that Huawei officially provides, which can inject a specific object into it, but also supports injecting multiple objects, that is, the original plan two, registerJavaScriptProxy can indeed inject multiple, we also provide APIs, but for customers to find their own time to inject, we currently do not have the right time to recommend.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33e14a5b9d3f481480e610f435eb5e71~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40c4a81c2ece4b458e24d71db10b1820~tplv-goo7wpa0wc-image.image) </span>

The official introduction, if you want to use the second way to inject multiple objects, you need to trigger refresh to take effect. Before the second option was verified in the old version, it was feasible. After 5.0, refresh caused the callback onPageBegin to fall into an infinite loop.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/484d42b8867c4c61beaf3d67459ec48b~tplv-goo7wpa0wc-image.image) </span>

The official demo is injected by button and refreshed by button, so this time is up to the customer to control, don't call our registerJsBridge in onPageBegin.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9f7897db7d147bb8dcb5f24b79978de~tplv-goo7wpa0wc-image.image) </span>

So the conclusion is that the customer itself does not have the recommended way to directly inject Bridge, if the customer has its own Bridge will need to find the right time to do injection, we do not have the right time to recommend, we also asked Huawei people, there is no right time, if there is no right time, you can only refer to the official website documents: [registerJavaScriptProxy](https://developer.huawei.com/consumer/en/doc/harmonyos-references/arkts-apis-webview-webviewcontroller#registerjavascriptproxy).

The reason why the second plan is dropped: The original plan is also explained above, the registerJavaScriptProxy of injecting multiple objects must be refreshed to take effect, refresh will cause onPageBegin to call back again, thus falling into an infinite loop, but there is no other suitable existing life cycle suitable treatment.

A relatively low scheme (determine whether it has been loaded by the flag bit):

Possible side effects: Of course, if it is really difficult to deal with customers, I can only recommend this relatively low solution, but it may cause the web pageview to be collected once more due to refresh. The previous version has encountered it, and the new version seems to be gone

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc82c8aefcbe429d9f6776d0a8ac7c09~tplv-goo7wpa0wc-image.image) </span>

<span id="fdc0bd6e"></span>
# Is the x86 emulator supported?

A: 25.3 has been supported, the corresponding version 1.3.1.

<span id="ffe20042"></span>
# When the customer integrates Devtools, his pop\-up window shows an error, and the pop\-up window content is displayed in Devtools.

Answer: There may be a problem with the customer obtaining the window object. LastWindow does not distinguish between the main window and sub\-windows. It is recommended to change window.getLastWindow to context.windowStage.getMainWindowSync ().

<span id="caaf569d"></span>
# SDK packaged version

Answer: Only the latest two packages are recorded


* 1.2.0 based on 810 packaging, since 9.30 is released, it is based on 810, because 900 is released on 10.8

* 1.3.0 based on 910 packages

* 1.1.0 based on 910 packages

* 1.3.1 based on 5.0.9


<span id="55fd0cb0"></span>
# ERROR: Bytecode HARs: [@volcengine/applog, @volcengine/applog_devtools, @volcengine/applog] not supported when useNormalizedOHMUrl is not true. \* Try the following: \> Please check useNormalizedOHMUrl in the project\-level build\-profile.json5 file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/253399e7db9345ab8392071682643d7d~tplv-goo7wpa0wc-image.image) </span>

Answer: Add this configuration in the root directory and compatibleSdkVersion adjusted to 12.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d76cbab17b164932a9194db6dc5ae60a~tplv-goo7wpa0wc-image.image) </span>

Reason for adding this configuration ([Building a Bytecode HAR](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-hvigor-build-har-V5#section179161312181613)):


1. The compiled product has the bytecode compiled in advance, so it can improve the efficiency of application\-side compilation

2. The project after Ide 800 is turned on by default, which is the trend on Huawei's side.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/257be64473b7487a88570f906b847241~tplv-goo7wpa0wc-image.image) </span>

<span id="c3a93874"></span>
# Whether to support meta services

Answer: It has been supported after 25.3 months

<span id="1039600f"></span>
# 1.3.0 Version offline integration pako found error

Answer: Add the overrides configuration to force the designation of the offline version or a specific version (such as the private warehouse version of Minsheng).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b85200bc2684479a0a8a5ba31ae1463~tplv-goo7wpa0wc-image.image) </span>

<span id="f6e61348"></span>
# What types of incident reports are accepted?

Answer: The event custom attribute is of EventRecord type, which is a custom type. Other types are not supported because the SDK needs to do type checking to avoid receiving types that cannot be parsed, so the SDK restricts the receiving types.

1.1.0 EventRecord = Record<string, number | string | boolean\>

1.2.0 EventRecord = Record<string, number | string | boolean | string[]\>

<span id="c0fdc317"></span>
# How to resolve application content errors displayed to Devtools?

Answer:

<span id="77cf2ae3"></span>
### Option one:

Check which Window the specific content is mounted on. For example, the system window.getLastWindow does not distinguish between the main window of the child window. If you need to correctly mount the content to the main window, it is recommended to directly obtain the main window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc89c9ba661f4f0ebbf71abf8029690d~tplv-goo7wpa0wc-image.image) </span>

If you need to mount to a specific child window, it is recommended to obtain it by window name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bcd187cecd34313a53b629461ae7e82~tplv-goo7wpa0wc-image.image) </span>

<span id="1ec5c2b8"></span>
### Option two:

If the first solution is not good, you can upgrade to the 130\-rc1 version, turn off the sub\-window mode, and use the page mount method.

<span id="0921ce4d"></span>
# Why did you upgrade the SDK and find that there is no change? Why didn't you see the required function?

Answer: Please sync.

<span id="4fff0eb0"></span>
# DevEco Studio 5.0.1 Release 5.0.5 .300 integration devtools startup crash error

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90e3887b411b4609a001d9ca85d70d47~tplv-goo7wpa0wc-image.image) </span>

Answer: The product compiled by the new version has changed, and it is necessary to provide the product compiled based on the new version.

<span id="65168a00"></span>
# New version of IDE ready\-to\-use Devtools error

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df2ec6158ca944d19fd142540f7e42e9~tplv-goo7wpa0wc-image.image) </span>

Answer: Remember to override applog, and override to the oh\-package.json5 of the root node.

<span id="c73fa302"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
