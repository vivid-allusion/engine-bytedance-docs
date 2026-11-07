---
title: "HarmonyOS Next SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/HarmonyOS_Next_SDK_Integration_"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The HarmonyOS Next SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration">HarmonyOS Next SDK Integration</a></div>


<span id="2b0c808f"></span>
# Precautions


* **Supported environments:** 

   
   |Environment |Whether to support |Remarks |
   |---|---|---|
   |SaaS\-cloud native |Supported |The environment has been adapted and the platform is reported as openHarmony.<br><br>If the old privatized version is upgraded, you need to contact BytePlus technical support staff to obtain the new version of the HarmonyOS Next SDK adaptation package. |
   | |Not supported |The environment is not supported or the adaptation is not completed. If you want to integrate early, the platform of the SDK will be reported as Android. |
   

* **SDK Release Notes:** 

   The current HarmonyOS Next SDK is Bate/RC version, Hongmeng system has been officially launched, this SDK is based on Hongmeng HarmonyOS 5.0.0 Release version compilation and packaging, the follow\-up will continue to iterate with the update of Huawei system, the current function adaptation is not a complete version.

   * The features currently supported by the latest version of the HarmonyOS Next SDK include:

      * Custom event tracking/request encryption (default encryption/national secret sm2)/user ID and user attributes/AB shunt experiment/event blacklist/web get through/crash collection (JS layer)/real\-time event tracking verification/custom header settings/full event tracking (beta)/component exposure/multi\-ID caliber

      * DevTools Debugging Tools

         * View event information/View network requests/View access status/Configuration information module/Built\-in scan function

   * See SDK release log details [SDK Update Log](https://docs.byteplus.com/docs/DataFinder/SDK_Update_Log).

   * Multi\-threading/multi\-process is not supported for the time being. The Hongmeng system is special and adopts process isolation between threads, which requires an additional adaptation plan.


<span id="5c199ece"></span>
# Integrated Growth Marketing Suite SDK

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Finder HarmonyOS SDK requires that the minimum access version of Hongmeng is API 12 or above.</div>


<div data-tips="true" data-tips-type="warning"><strong>For specific access methods, please refer to the offline access documentation included with the offline package. Each version may vary slightly.</strong></div>


<span id="1c99d377"></span>
## Obtain the SDK and access method

<span id="8bef1b13"></span>
### SDK download and selection


|Environment |SDK selection |
|---|---|
|SaaS\-cloud native<br><br>Privatization version 492 and above |Please select platform=openHarmony corresponding SDK |
|Privatization versions before 492 |Please select the SDK corresponding to platform = Android |


<span id="a1e1a78a"></span>
### Access

Adding dependencies to the project adds:

```TypeScript
//Such as entry or model, you can actually consider adding it to the root directory (so that all modules in the project can be accessed)
"dependencies": {
  //sdk strong dependency for gzip compression
  "pako": "^2.1.0",
  //When introducing the AppLog component, make sure the component name is this
  "@volcengine/applog": "file:../applogx/applogx.har",
  //Debugging tool (optional)
  "@volcengine/applog_devtools": "file:../applogx/applogx_devtools.har"
}

//overrides are only valid at oh-package.json5 at the root node
"overrides": {
  //rewrite
  "@volcengine/applog": "file:../applogx/applogx.har",
}
```


<span id="641108e1"></span>
## Get the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="98790995"></span>
### SaaS\-cloud\-native


|End type |SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|HarmonyOS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |Not supported yet. |


<span id="e419d2a4"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="9c68f4c0"></span>
## Permission statement

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">OAID is a user pop\-up permission. When you need to collect relevant data, you need to add the OAID permission application code in the application logic.</div>


<div data-tips="true" data-tips-type="warning">Configure in module.json5 under enrty:</div>


```JavaScript
"requestPermissions": [
  {
    // network permission, add when necessary
    "name": "ohos.permission.INTERNET"
  },
  {
    // wifi information acquiring, add when necessary
    "name": "ohos.permission.GET_WIFI_INFO"
  },
  { 
    // Acquire network information, add when necessary
    "name": "ohos.permission.GET_NETWORK_INFO"
  },
  {
    // Asset persistence, recommended to add, related to device ID generation. Failure to declare will result in device ID changes during uninstallation and reinstallation
    "name": "ohos.permission.STORE_PERSISTENT_DATA"
  },
  {
    // oaid permission (optional), recommended to add
    "name": "ohos.permission.APP_TRACKING_CONSENT",
    "reason": "$string:your_reason",
    "usedScene": {
      "abilities": [],
      "when": "inuse"
    }
  },
],
```


<span id="ad0278fa"></span>
# Initialize Growth Marketing Suite SDK

Hongmeng completely separates init from start.


* After init, you can call various methods of the SDK. The SDK does not support event tracking before init, but after init, you can start event tracking and drop off the library.

* The collection of sensitive header information such as oaid starts only after the start, and the data request is only made at this time.

* If AbilityStage is created, you can place init in oncreate of AbilityStage, where you can initialize the SDK, and then call start after the privacy pop\-up.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">AbilityStage is equivalent to Application in Android.   </div>
   

<span id="8d53251d"></span>
## Multiple instances

In the current version, each instance is newly created, so creating a new AppLog corresponds to passing in a different application instance.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

// create new AppLog instance
let appLog1 = new AppLog()
// init sdk inputs the configuration, and after init
appLog1.init(context, new InitConfig('yourAppId1', 'yourChannel')
  // whether open log
  .setLogEnabled(true))
  
// Harmony SDK requires manual invocation of the `start` method to commence the collection of sensitive information and the sending of requests.
appLog1.start()

// create new AppLog instance
let appLog2 = new AppLog()
// init sdk inputs the configuration, and after init
appLog2.init(context, new InitConfig('yourAppId2', 'yourChannel')
  // whether open log
  .setLogEnabled(true))
  
// Harmony SDK requires manual invocation of the `start` method to commence the collection of sensitive information and the sending of requests.
appLog2.start()
```


<span id="3146a8bf"></span>
# Sensitive information collection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since the 1.3.0 version, it is supported to turn off Oaid and operator information collection through the configuration of the following switches.</div>


<span id="8412acfc"></span>
## Turn off Oaid acquisition

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Hongmeng Oaid is authorized by the user, and the application side needs to actively apply for permission. If you apply for permission and the user agrees, the SDK can collect Oaid, and also supports closing Oaid collection with the user's consent.</div>


The OAID information collection of the device is turned on by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOaidEnabled(false)
```


<span id="de7acb74"></span>
## Turn off carrier information collection

The operator information of the device is collected by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOperatorInfoEnabled(false)
```


<span id="c13f4770"></span>
# Configuration Scheme (optional)

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification), configure Scheme, otherwise you can skip this step.

<span id="8f3eb705"></span>
## Method 1, use Devtools built\-in to scan

This method does not require the configuration of a wake\-up protocol.

After integrating Devtools, click on Console \- \> Scan, and follow the process.

<span id="e9d2db98"></span>
## Method 2, traditional scan code jump

At this stage, Hongmeng system browser has supported scanning code jump.

<span id="8c901af2"></span>
### Get URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6ccf7f1355249488cc8ce8cc6ffd4af~tplv-goo7wpa0wc-image.image) </span>

<span id="8f735898"></span>
### Configure URL Scheme

<span id="df124470"></span>
#### Configure the jump protocol (mode 2 added)

```TypeScript
//Configure uris in the main Ability under the entry module:
"uris": [
    {
        //rangersapplog.xxx please replace with the scheme shown in the official documentation
        "scheme": "rangersapplog.xxx",
        "host": "rangersapplog",
        "path": "picker"
    }
]
//Example:
"abilities": [
  {
    "name": "EntryAbility",
    "srcEntry": "./ets/entryability/EntryAbility.ets",
    "description": "$string:EntryAbility_desc",
    "icon": "$media:icon",
    "label": "$string:EntryAbility_label",
    "startWindowIcon": "$media:startIcon",
    "startWindowBackground": "$color:start_window_background",
    "exported": true,
    "skills": [
      {
        //also requires configuration
        "actions": [
          "ohos.want.action.viewData"
        ],
        "uris": [
          {
            //rangersapplog.xxx please replace with the scheme shown in the official documentation
            "scheme": "rangersapplog.xxx",
            "host": "rangersapplog",
            "path": "picker"
          }
        ]
      },
    ]
  }
]
```


<span id="d43a9d17"></span>
#### Add real\-time event tracking startup code (mode 2 adds)

```TypeScript
import { InitConfig } from '@volcengine/applog'

//Add the following code to Ability to configure the jump protocol:
//Add to EntryAbility in the example:
//onNewWant is a callback for startup calls after startup
onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
  //Just pass in the protocol uri.
  appLog.simulate()?.start(want.uri)
}

//If you haven't started the app yet, you want to scan the code for real-time event tracking.
onCreate(want: Want, _: AbilityConstant.LaunchParam): void {
  //Note that it needs to be called after the SDK init.
  //Just pass in the protocol uri.
  appLog.simulate()?.start(want.uri)
}
```


<span id="af865fd7"></span>
# Initialize basic configuration

<span id="a760f4a7"></span>
## SDK init

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK does not accept any method calls before init. If you want to call the internal methods of the SDK, you need to init first, and the init method has been processed for compliance. Init will not automatically collect sensitive information and send requests.</div>


<div data-tips="true" data-tips-type="tip"><strong>You can consider sdk init in onCreate of AbilityStage, and sdk start after privacy consent.</strong></div>


```TypeScript
appLog.init(context, config)
```


<span id="43895e6c"></span>
## SDK start

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please do not call start before init. After calling start, the SDK will actually start collecting sensitive information and reporting requests.</div>


```TypeScript
appLog.start()
```


<span id="a6a8e4bf"></span>
## Open SDK log

<span id="5d4c44ad"></span>
### SDK internal data output log

```TypeScript
import { InitConfig } from '@volcengine/applog'

let config = new InitConfig('yourAppId', 'yourChannel')
  //Open the SDK log
  .setLogEnabled(true)
```


<span id="3c44d765"></span>
### The application takes over the print log itself

```TypeScript
import { InitConfig } from '@volcengine/applog'

let config = new InitConfig('yourAppId', 'yourChannel')
  //You also need to open the SDK log first.
  .setLogEnabled(true)
  //Implement the log takeover method
  .setLogger({
    log: (_: hilog.LogLevel, __: string, msg: string, err?: Error) => {
        hilog.debug(0x0100, 'AppLogH_test', `${msg} ${err ? JSON.stringify(err) : ""}`)
    }
})
```


<span id="a743933c"></span>
## Custom domain name

```TypeScript
import { InitConfig } from '@volcengine/applog'
import { createByDomain } from '@volcengine/applog/src/main/ets/core/base/url/UriConfig'

let config = new InitConfig('yourAppId', 'yourChannel')
  .setUri(createByDomain("your_REPORT_URL"))
```


<span id="d15ec284"></span>
## Encryption settings

The SDK enables encryption by default, and the built\-in default encryption method is consistent with Android.

If you need to modify the SDK encryption method, it is recommended to insert the corresponding code between init and start to ensure that the encryption method is requested after startup.

<span id="26fc5cd5"></span>
### Default encryption

No additional settings are required.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//No need to add by default, encryption is turned on by default
appLog.encrypt()?.enablePlugin()
//Switch to the default encryption method, it is recommended to call before start, because start starts the request
appLog.encrypt()?.useDefaultEncrypt()
appLog.start()
```


<span id="a0b3fe99"></span>
### State Secret SM2

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This encryption method is currently only supported in the privatized version.</div>


```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//No need to add by default, encryption is turned on by default
appLog.encrypt()?.enablePlugin()
//Switch to State Secret SM2 asymmetric encryption, you need to manually pass in the public key
appLog.encrypt()?.useSm2Encrypt("your_public_key")
appLog.start()
```


<span id="8a8ff7a7"></span>
### Turn off SDK encryption

For the debugging stage, SDK encryption can be turned off to facilitate packet capture to check whether the data is normal.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//turn off encryption
appLog.encrypt()?.disablePlugin()
appLog.start()
```


<span id="14de2aa0"></span>
## Open the embedded H5 page

If your application integrates the Web/JS SDK and the Harmony SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Harmony SDK, you can use the embedded H5 function to get through. At this time, the events generated on the H5 page will be reported through the Harmony SDK, not in the Web/JS SDK. This kind of takeover reporting scenario will reuse the `user_unique_id`and public properties set by the Harmony side, but also support the uuid/public properties on the web side setting/update side when getting through. Please pay attention to which side of the data is used when getting through. If it is completely subject to the end, you can Remove the uuid/common attribute operation on the web SDK side.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function requires the Web/JS SDK and Harmony SDK to integrate and cooperate with each other at the same time, and the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, because the reporting is taken over by the Harmony SDK at this time. If you still want to collect H5 full event tracking, you need to check Section 5.7: Native collection of H5 full event tracking. Web/JS SDK Integration Refer to <a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_">Web/JavaScript SDK Integration</a> and Section 3.4.</div>



* Initialize the SDK


```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// ...
appLog.start()

export {
    appLog
}
```



* Use on Web Components


<span id="77c2787e"></span>
### Method 1: Use javaScriptProxy injection

```TypeScript
import web_webview from '@ohos.web.webview'
import { appLog } from './applog'

@Component
export struct Webview {
    controller: web_webview.WebviewController = new web_webview.WebviewController()
    bridgeProxyInfo = appLog.bridge()!.injectJsBridgeByJsProxy()
    
    build() {
        Web({ src: $rawfile('webview.html'), controller: this.controller })
          .javaScriptAccess(true)
          .javaScriptProxy({
            object: this.bridgeProxyInfo.object,
            name: this.bridgeProxyInfo.name,
            methodList: this.bridgeProxyInfo.methodList,
            controller: this.controller,
          })
    }
}
```


<span id="187d19cc"></span>
## Activate crash capture

The current SDK supports collecting JS crashes through errorManager, and the internal SDK is turned off by default.

```TypeScript
let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//Actively start JS Crash collection
appLog.crash()?.enablePlugin()
appLog.start()
```


<span id="2b73c8f6"></span>
# AB experiment

AB experiment is turned off by default (consistent with Android), if you need to use AB experiment, you need to manually turn it on first.

<span id="06c36b76"></span>
## Activate AB experiment function

```JavaScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//Open AB experiment, it is recommended to call between init and start
appLog.abTest()?.enablePlugin()
appLog.start()
```


<span id="9adfacb2"></span>
## Obtain AB experimental server level configuration

```JavaScript
//It is recommended to obtain all experimental results each time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAllAbTestConfigs()
})
```


<span id="7dddafc8"></span>
## Perform AB experimental exposure

```JavaScript
//It is recommended to trigger the experiment every time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAbConfig("ab_key", defaultValue)
})
```


<span id="d604294c"></span>
## Get List of Exposed Experimental VIDs

```JavaScript
appLog.abTest()?.getAbSdkVersion()
```


<span id="b04a0d2b"></span>
## Subscribe to ABS server level offload configuration acquisition

```JavaScript
appLog.topicReceiver()?.on(Topic.ABTestConfigReady, (abTestConfig) => {
  hilog.info(0x0000, 'AppLogH', `AppLog abtest config ready:  ${JSON.stringify(abTestConfig)}`)
})

abTestConfig format:
detailed test configuration
{
    "ab": {
        "val": "访问页面 A", //view page A
        "vid": "1"
    },
    "ba": {
        "val": "对照版", //comparison version
        "vid": "2"
    },
    "tt": {
        "val": true,
        "vid": "3"
    }
}
```


<span id="ba68403e"></span>
## Subscribe to New Exposure Vid Records

```JavaScript
appLog.topicReceiver()?.on(Topic.ABTestVidChanged, (vids) => {
  hilog.info(0x0000, 'AppLogH', `AppLog abtest vids:  ${JSON.stringify(vids)}`)
})

vids format:
{
  //The latest exposed vid
  "new_vid":"1",
  //Exposed vid collection (including the latest)
  "vids":"1"
}
```


<span id="78d156d3"></span>
# DevTools

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK provides DevTools tools that enable easy observation of some of the SDK's operating information during development.</div>


<span id="928b8d68"></span>
## Devtools integration

Initialize the SDK and register the DevTools plug\-in (the **initialization method is the same as the old and new versions** )

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'
import { DevTools } from '@volcengine/applog_devtools'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)

//Register DevTools plugin
DevTools.applyDevTools(appLog)

appLog.start()

export {
    appLog
}
```


<span id="55b0bdec"></span>
## How to use the new version: 1.2.0 and above

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">How to use the new version: 1.2.0 and above</div>


<div data-tips="true" data-tips-type="tip"><strong>The new version of Devtools implements the same global levitation capability as Android (using the sub\-window function), so it can be used directly without additional mounting.</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>If the old version is upgraded, the previous usage method needs to be removed.</strong></div>


<div data-tips="true" data-tips-type="tip">The new version monitors onWindowStageActive. If the SDK is initialized late, it may miss the monitoring. You can switch between the front and background and display it. Normally, there is no need to manually call the display.</div>


```Go
//If you need to open it manually, you can call it manually:
Devtools.show(windowStage: window.WindowStage)

//Support manual shutdown:
Devtools.close()
```


<span id="fcf40e0e"></span>
## Old version usage: 1.0.0/1.1.0 version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The old version of Devtools is not a global floating window like Android, and it needs to be mounted on the corresponding page.</div>


Mount the DevTools component on the required page, it is recommended to mount it on the root component

```TypeScript
import DevToolsPage from '@volcengine/applog_devtools'

@Entry
@Component
struct Index {
  // ...
  
  build() {
    Column() {
      // ...
      
      DevToolsPage()
    }
  }
}
```


<span id="d68fe538"></span>
# Reference: Data reporting process and mechanism

Default is reported once a minute, but there is no specific number of reports, SDK strategy for the new reporting strategy by volume query events (Android/iOS query by the number of queries), each report query about 1M data to report, no longer 200 shall prevail (can be reported as much as possible).
