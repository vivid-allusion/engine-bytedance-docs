---
title: "HarmonyOS Next SDK Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/HarmonyOS-Next-SDK-Integration"
---

<span id="4e941206"></span>
# Precautions


* **Supported environments**:

   
   |Environment |Whether to support |Remarks |
   |---|---|---|
   |Privatization 4.9.2 version |Supported |The environment has been adapted and the platform is reported as openHarmony.<br><br>If the old privatized version is upgraded, you need to contact BytePlus technical support staff to obtain the new version of the HarmonyOS Next SDK adaptation package. |
   |Privatization versions before 4.9.2 |Not supported |The environment is not supported or the adaptation is not completed. If you want to integrate early, the platform of the SDK will be reported as Android. |
   

* **SDK Release Notes:** 

   The current HarmonyOS Next SDK is Beta/RC version. HarmonyOS system has been officially launched, this SDK is based on HarmonyOS HarmonyOS 5.0.0 Release version compilation and packaging, the follow\-up will continue to iterate with the update of Huawei system, the current function adaptation is not a complete version.

   * The features currently supported by the latest version of the HarmonyOS Next SDK include:

      * Custom event tracking/request encryption (default encryption/national secret sm2)/user ID and user attributes/AB shunt experiment/event blacklist/web get through/crash collection (JS layer)/real\-time event tracking verification/custom header settings/full event tracking (beta)/component exposure/multi\-ID caliber

      * DevTools Debugging Tools

         * View event information/View network requests/View access status/Configuration information module/Built\-in scan function

   * See SDK release log details [SDK Changelog](https://docs.byteplus.com/docs/DataTester/SDK-Changelog).

   * Multi\-threading/multi\-process is not supported for the time being. The HarmonyOS system is special and adopts process isolation between threads, which requires an additional adaptation plan.


<span id="1f9f932a"></span>
# Integrated Growth Marketing Suite SDK

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">HarmonyOS SDK requires that the minimum access version of HarmonyOS is API 12 or above.</div>


<span id="5e1f3396"></span>
## Obtain the SDK and access method

Obtain the SDK and access method: You need to contact BytePlus technical support to obtain it.

<span id="c8501d97"></span>
## Permission statement

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">OAID is a user pop\-up permission. When you need to collect relevant data, you need to add the OAID permission application code in the application logic.</div>


<div data-tips="true" data-tips-type="warning">Configure in module.json5 under enrty:</div>


```JavaScript
"requestPermissions": [
  {
    // web permission, mandatory
    "name": "ohos.permission.INTERNET"
  },
  {
    // wifi information acquisition, mandatory
    "name": "ohos.permission.GET_WIFI_INFO"
  },
  { 
    // acquire web information, mandatory
    "name": "ohos.permission.GET_NETWORK_INFO"
  },
  {
    // Asset persistence, recommended to add, related to deviceid generation. Failure to declare will result in changes to deviceid during uninstallation and reinstallation
    "name": "ohos.permission.STORE_PERSISTENT_DATA"
  },
  {
    // oaid permission(optional), recommended to add
    "name": "ohos.permission.APP_TRACKING_CONSENT",
    "reason": "$string:your_reason",
    "usedScene": {
      "abilities": [],
      "when": "inuse"
    }
  },
],
```


<span id="0c21b839"></span>
# Initialize Growth Marketing Suite SDK

HarmonyOS completely separates init from start.


* After init, you can call various methods of the SDK. The SDK does not support event tracking before init, but after init, you can start event tracking and drop off the library.

* The collection of sensitive header information such as oaid starts only after the start, and the data request is only made at this time.

* If AbilityStage is created, you can place init in oncreate of AbilityStage, where you can initialize the SDK, and then call start after the privacy pop\-up.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">AbilityStage is equivalent to Application in Android.</div>


<span id="84c2772c"></span>
## **Privatization**

```JavaScript
import { AppLog, InitConfig } from '@volcengine/applog'

// create new AppLog instance
let appLog = new AppLog()
// HarmonyOS sdk channel can be optional parameters
let config = new InitConfig('yourAppId', 'yourChannel')
  // Whether to open log
  .setLogEnabled(true)
  // Set up a private deployment data reporting address
  .setUri(createByDomain("your_REPORT_URL"))
// init sdk pass in configuration, available after init
appLog.init(context, config)

// The HarmonyOS SDK needs to manually call start to begin collecting sensitive information and sending requests
appLog.start()
```


<span id="edccc3c0"></span>
## Multiple instances

In the current version, each instance is newly created, so creating a new AppLog corresponds to passing in a different application instance.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

// create new AppLog instance
let appLog1 = new AppLog()
// init sdk pass in configuration, available after init
appLog1.init(context, new InitConfig('yourAppId1', 'yourChannel')
  // Whether to open log
  .setLogEnabled(true))
  
// The HarmonyOS SDK needs to manually call start to begin collecting sensitive information and sending requests
appLog1.start()

// create new AppLog instance
let appLog2 = new AppLog()
// init sdk pass in configuration, available after init
appLog2.init(context, new InitConfig('yourAppId2', 'yourChannel')
  // Whether to open log
  .setLogEnabled(true))
  
// The HarmonyOS SDK needs to manually call start to begin collecting sensitive information and sending requests
appLog2.start()
```


<span id="2236f3aa"></span>
# Sensitive information collection

<span id="6dd2102a"></span>
## Turn off Oaid acquisition

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HarmonyOS Oaid is authorized by the user, and the application side needs to actively apply for permission. If you apply for permission and the user agrees, the SDK can collect Oaid, and also supports closing Oaid collection with the user's consent.</div>


The OAID information collection of the device is turned on by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOaidEnabled(false)
```


<span id="690879e4"></span>
## Turn off carrier information collection

The operator information of the device is collected by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOperatorInfoEnabled(false)
```


<span id="84522d88"></span>
# Configuration Scheme (optional)

To use [real-time event tracking detection](https://www.volcengine.com/docs/84129/1261787), configure Scheme, otherwise you can skip this step.

<span id="8fe95d97"></span>
## Method 1. use Devtools built\-in to scan

This method does not require the configuration of a wake\-up protocol.

After integrating Devtools, click on Console \- \> Scan, and follow the process.

<span id="81ff1c1b"></span>
## Method 2. traditional scan code jump

At this stage, HarmonyOS system browser supports scanning code jump.

<span id="5fff1dd0"></span>
### Get URL Scheme

Scheme is generally in the form `of rangersapplog.xxxxx.`

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="26e037ec"></span>
### Configure URL Scheme

<span id="54a078be"></span>
#### Configure the jump protocol (mode 2 added)

```TypeScript
// Configure uris in the main Ability of entry sector:
"uris": [
    {
        // rangersapplog.xxx please repalce with scheme displayed in offical document  
        "scheme": "rangersapplog.xxx",
        "host": "rangersapplog",
        "path": "picker"
    }
]
// Example:
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
        // Also need to be configured
        "actions": [
          "ohos.want.action.viewData"
        ],
        "uris": [
          {
            // rangersapplog.xxx please repalce with scheme displayed in offical document  
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


<span id="8de0081f"></span>
#### Add real\-time event tracking startup code (mode 2 adds)

```TypeScript
import { InitConfig } from '@volcengine/applog'

// Add the following code to the Ability section of the jump protocol configuration:
// Add the following to the EntryAbility in the example:
// onNewWant after startup, there is a startup call callback
onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
  // pass in protocol uri would be ok
  appLog.simulate()?.start(want.uri)
}

// If you want to scan the code for real-time tracking before launching the App
onCreate(want: Want, _: AbilityConstant.LaunchParam): void {
  // Note that you need to call after SDK init
  // pass in uri would be ok
  appLog.simulate()?.start(want.uri)
}
```


<span id="493a89fd"></span>
# Initialize basic configuration

<span id="ed4042a3"></span>
## SDK init

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK does not accept any method calls before init. If you want to call the internal methods of the SDK, you need to init first, and the init method has been processed for compliance. Init will not automatically collect sensitive information and send requests.</div>


<div data-tips="true" data-tips-type="tip"><strong>You can consider sdk init in onCreate of AbilityStage, and sdk start after privacy consent.</strong></div>


```TypeScript
appLog.init(context, config)
```


<span id="4d0ca641"></span>
## SDK start

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please do not call start before init. After calling start, the SDK will actually start collecting sensitive information and reporting requests.</div>


```TypeScript
appLog.start()
```


<span id="6ddfcd7a"></span>
## Open SDK log

<span id="4802a856"></span>
### SDK internal data output log

```TypeScript
import { InitConfig } from '@volcengine/applog'

let config = new InitConfig('yourAppId', 'yourChannel')
  // open SDK log
  .setLogEnabled(true)
```


<span id="951eb0ad"></span>
### The application takes over the print log itself

```TypeScript
import { InitConfig } from '@volcengine/applog'

let config = new InitConfig('yourAppId', 'yourChannel')
  // open SDK log first
  .setLogEnabled(true)
  // Implement log takeover method
  .setLogger({
    log: (_: hilog.LogLevel, __: string, msg: string, err?: Error) => {
        hilog.debug(0x0100, 'AppLogH_test', `${msg} ${err ? JSON.stringify(err) : ""}`)
    }
})
```


<span id="127a6253"></span>
## Custom domain name

```TypeScript
import { InitConfig } from '@volcengine/applog'
import { createByDomain } from '@volcengine/applog/src/main/ets/core/base/url/UriConfig'

let config = new InitConfig('yourAppId', 'yourChannel')
  .setUri(createByDomain("your_REPORT_URL"))
```


<span id="27264efd"></span>
## Encryption settings

The SDK enables encryption by default, and the built\-in default encryption method is consistent with Android.

If you need to modify the SDK encryption method, it is recommended to insert the corresponding code between init and start to ensure that the encryption method is requested after startup.

<span id="755ff8c0"></span>
### Default encryption

No additional settings are required.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// No need to add by default, encryption is enabled by default
appLog.encrypt()?.enablePlugin()
// Switch to the default encryption mode. It is recommended to call before start, because start starts the request
appLog.encrypt()?.useDefaultEncrypt()
appLog.start()
```


<span id="520bf26c"></span>
### State Secret SM2

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This encryption method is currently only supported in the privatized version.</div>


```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// No need to add by default, encryption is enabled by default
appLog.encrypt()?.enablePlugin()
// Switch to the SM2 asymmetric encryption which requires manually passing in the public key
appLog.encrypt()?.useSm2Encrypt("your_public_key")
appLog.start()
```


<span id="0c0d0948"></span>
### Turn off SDK encryption

For the debugging stage, SDK encryption can be turned off to facilitate packet capture to check whether the data is normal.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// close encryption
appLog.encrypt()?.disablePlugin()
appLog.start()
```


<span id="5b19b366"></span>
## Open the embedded H5 page

If your application integrates the Web/JS SDK and the Harmony SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Harmony SDK, you can use the embedded H5 function to get through. At this time, the events generated on the H5 page will be reported through the Harmony SDK, not in the Web/JS SDK. This kind of takeover reporting scenario will reuse the `user_unique_id`and public properties set by the Harmony side, but also support the uuid/public properties on the web side setting/update side when getting through. Please pay attention to which side of the data is used when getting through. If it is completely subject to the end, you can remove the uuid/common attribute operation on the web SDK side.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function requires the Web/JS SDK and Harmony SDK to integrate and cooperate with each other at the same time, and the current version of the Web/JS SDK blocks the H5 full event tracking function by default after getting through, because the reporting is taken over by the Harmony SDK at this time. If you still want to collect H5 full event tracking, you need to check Section 5.7: Native collection of H5 full event tracking. Web/JS SDK Integration Refer to <a href="https://www.volcengine.com/docs/84129/1261745">Web/JavaScript SDK Integration</a> and Section 3.4.</div>



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


<span id="7ec4df62"></span>
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


<span id="ecd0646e"></span>
## Activate crash capture

The current SDK supports collecting JS crashes through errorManager, and the internal SDK is turned off by default.

```TypeScript
let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// Proactively enable JS Crash collection
appLog.crash()?.enablePlugin()
appLog.start()
```


<span id="ecebffce"></span>
# AB experiment

AB experiment is turned off by default (consistent with Android), if you need to use AB experiment, you need to manually turn it on first.

<span id="ac66047a"></span>
## Activate the AB experiment function

```JavaScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
// Enable AB testing, it is recommended to call between init and start
appLog.abTest()?.enablePlugin()
appLog.start()
```


<span id="dedb68f8"></span>
## Obtain AB experimental server level configuration

```JavaScript
//It is recommended to obtain all experimental results each time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAllAbTestConfigs()
})
```


<span id="8b071317"></span>
## Perform AB experimental exposure

```JavaScript
//It is recommended to trigger the experiment every time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAbConfig("ab_key", defaultValue)
})
```


<span id="6b468153"></span>
## Get List of Exposed Experimental VIDs

```JavaScript
appLog.abTest()?.getAbSdkVersion()
```


<span id="86d5ef5b"></span>
## Subscribe to ABS server level offload configuration acquisition

```JavaScript
appLog.topicReceiver()?.on(Topic.ABTestConfigReady, (abTestConfig) => {
  hilog.info(0x0000, 'AppLogH', `AppLog abtest config ready:  ${JSON.stringify(abTestConfig)}`)
})

abTestConfig format:
It is detailed experimental configuration
{
    "ab": {
        "val": "visit page A",
        "vid": "1"
    },
    "ba": {
        "val": "control version",
        "vid": "2"
    },
    "tt": {
        "val": true,
        "vid": "3"
    }
}
```


<span id="9f445f52"></span>
## Subscribe to New Exposure Vid Records

```JavaScript
appLog.topicReceiver()?.on(Topic.ABTestVidChanged, (vids) => {
  hilog.info(0x0000, 'AppLogH', `AppLog abtest vids:  ${JSON.stringify(vids)}`)
})

vids format:
{
  // Newly exposed vid
  "new_vid":"1",
  // Already exposed vid set(including newest)
  "vids":"1"
}
```


<span id="b948e342"></span>
# DevTools

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK provides DevTools tools that enable easy observation of some of the SDK's operating information during development.</div>


<span id="1890d973"></span>
## Devtools integration

Initialize the SDK and register the DevTools plug\-in (the **initialization method is the same as the old and new versions).** 

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'
import { DevTools } from '@volcengine/applog_devtools'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)

// register DevTools plugin
DevTools.applyDevTools(appLog)

appLog.start()

export {
    appLog
}
```


<span id="04ffcaae"></span>
## How to use the new version: 1.2.0 and above

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">How to use the new version: 1.2.0 and above</div>


<div data-tips="true" data-tips-type="tip"><strong>The new version of Devtools implements the same global levitation capability as Android (using the sub\-window function), so it can be used directly without additional mounting.</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>If the old version is upgraded, the previous usage method needs to be removed.</strong></div>


<div data-tips="true" data-tips-type="tip">The new version monitors onWindowStageActive. If the SDK is initialized late, it may miss the monitoring. You can switch between the front and background and display it. Normally, there is no need to manually call the display.</div>


```Go
//  If need to manually open, you can manually call:
Devtools.show(windowStage: window.WindowStage)

//  support manually close:
Devtools.close()
```


<span id="60a82008"></span>
## Old version usage: 1.0.0/1.1.0 version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The old version of Devtools is not a global floating window like Android, and it needs to be mounted on the corresponding page.</div>


Mount the DevTools component on the required page, it is recommended to mount it on the root component.

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


<span id="f4e7b82d"></span>
# Reference: Data reporting process and mechanism

Default is reported once a minute, but there is no specific number of reports, SDK strategy for the new reporting strategy by volume query events (Android/iOS by the number of queries), each report query about 1M data to report, no longer 200 shall prevail (can be reported as much as possible).
