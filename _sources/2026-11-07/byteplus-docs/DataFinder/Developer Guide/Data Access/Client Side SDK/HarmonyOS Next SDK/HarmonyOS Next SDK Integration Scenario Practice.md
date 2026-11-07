---
title: "HarmonyOS Next SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/HarmonyOS_Next_SDK_Integration_Scenario_Practice"
---

<span id="d79309ce"></span>
# Initialize related configuration

<span id="4b0ebfaa"></span>
## SDK init

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK does not accept any method calls before init. If you want to call the internal methods of the SDK, you need to init first, and the init method has been processed for compliance. Init will not automatically collect sensitive information and send requests.</div>


<div data-tips="true" data-tips-type="tip"><strong>You can consider sdk init in onCreate of AbilityStage, and sdk start after privacy consent.</strong></div>


```TypeScript
appLog.init(context, config)
```


<span id="80a575d9"></span>
## SDK start

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please do not call start before init. After calling start, the SDK will actually start collecting sensitive information and reporting requests.</div>


```TypeScript
appLog.start()
```


<span id="e4a00fc6"></span>
## Open SDK log

<span id="03d1ff5f"></span>
### SDK internal data output log

```TypeScript
import { InitConfig } from '@volcengine/applog'

let config = new InitConfig('yourAppId', 'yourChannel')
  //Open the SDK log
  .setLogEnabled(true)
```


<span id="1007a120"></span>
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


<span id="4c794b66"></span>
## custom domain name

```TypeScript
import { InitConfig } from '@volcengine/applog'
import { createByDomain } from '@volcengine/applog/src/main/ets/core/base/url/UriConfig'

let config = new InitConfig('yourAppId', 'yourChannel')
  .setUri(createByDomain("your_REPORT_URL"))
```


<span id="ebfe96a3"></span>
## encryption settings

The SDK enables encryption by default, and the built\-in default encryption method is consistent with Android.

If you need to modify the SDK encryption method, it is recommended to insert the corresponding code between init and start to ensure that the encryption method is requested after startup.

<span id="8b7df211"></span>
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


<span id="7867c244"></span>
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


<span id="14b070c6"></span>
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


<span id="45564033"></span>
## Sensitive information collection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since the 1.3.0 version, it is supported to turn off Oaid and operator information collection through the configuration of the following switches.</div>


<span id="185cae0b"></span>
### Turn off Oaid acquisition

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Harmony Oaid is authorized by the user, and the application side needs to actively apply for permission. If you apply for permission and the user agrees, the SDK can collect Oaid, and also supports closing Oaid collection with the user's consent.</div>


The OAID information collection of the device is turned on by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOaidEnabled(false)
```


<span id="27da58cf"></span>
### Turn off carrier information collection

The operator information of the device is collected by default, if you need to turn it off:

```JavaScript
let config = new InitConfig('yourAppId', 'yourChannel')
  .setOperatorInfoEnabled(false)
```


<span id="c984e5ef"></span>
# Events and properties, event public properties

<span id="82a7bf0f"></span>
## Event tracking

The user behavior log takes the form of **event event + attribute params** . Events generally correspond to multiple attributes, or only events have no attributes. Code event tracking schemes are typically designed by data analysts or product operations.


* Code event tracking that only reports events, as follows:


```TypeScript
//Example: Report an event that does not contain properties
//placed in the corresponding position of business logic
appLog.event("event")
```



* Code event tracking for reporting events and corresponding properties, as follows:


```TypeScript
//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
//placed in the corresponding position of business logic
appLog.event("event", {
  "key_string": "value_string",
  "key_int": 10
})
```


<span id="0bd825df"></span>
## event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

Public attribute storage logic is consistent with iOS and is not persistent.

<span id="1ea49e14"></span>
### Set public properties

```TypeScript
/*
 * Example: Set a custom public property with the property name key_public and the property value value_public
 * Please note about customizing "public properties":
 * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute.
 Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail;
 * 2. High-frequency modifications are not recommended, such as once per second.
 */
appLog.setHeaderInfo("key_public", "value_public")
```


<span id="580d46b2"></span>
### Remove public attributes

```TypeScript
// Example: Remove a public property named key_public
appLog.removeHeaderInfo("key_public")
```


<span id="9a42dd8b"></span>
# user_unique_id and user attributes

<span id="757874aa"></span>
## login status change call

Get user information module

```JavaScript
appLog.user()
```


<span id="e04cdb0b"></span>
### Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in. 6.13.0 + version supports calling before initializing AppLog to set the uuid of the logged in user.

```JavaScript
//Set UUID
appLog.user()?.setUserUniqueID("your_uuid")

//If you have multi-caliber requirements, you can see the settings below.
//Set UUID + UUIDType
appLog.user()?.setUserUniqueID("your_uuid", "your_uuid_type")
//The setUserUniqueID (uuid) of the single parameter is equivalent to the setUserUniqueID (uuid, lastuuidType) of the double parameter, but the uuidType is not available by default. If you want to empty the uuidType after setting it, you need to set it extra:
appLog.user()?.setUserUniqueID("your_uuid", null)
```


<span id="c658f9a5"></span>
### account login

Called when the account is logged out.

```JavaScript
// Log out of UUID
appLog.user()?.setUserUniqueID(null)

//If you have multi-caliber requirements, you can see the settings below.
// Logout UUID + UUIDType
appLog.user()?.setUserUniqueID(null, null)
```


<span id="f9304726"></span>
## multi\-ID caliber

> since：1.3.3\-rc3。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only SaaS\-cloud native/privatization support, multi\-ID caliber function needs to be opened separately. When using it, you need to report the user ID and ID type, and configure the id_bind relationship at the same time to restore a real user as accurately as possible. For more information and instructions on how to use multi\-ID calibers, see <a href="https://docs.byteplus.com/docs/undefined/6a4ce26a8f7714051e96f4c5">(不发布)Using Multi\-ID Types</a>.</div>


```TypeScript
//example demonstration
appLog.user()?.bind({
  "id_type_1": "id_type_value_1",
  "id_type_2": "id_type_value_2"
}, (result: IDBindParams) => {
  hilog.info(0x0000, 'AppLogH', `IDBindSuccess result: ${JSON.stringify(result)}`)
  //Update user status
  appLog.user()?.setUserUniqueID("id_type_value_1", "id_type_1")
}, (code: number, message: StringOrNull) => {
  hilog.info(0x0000, 'AppLogH', `IDBindFail code: ${code}, message: ${message}`)
})
```


<span id="f95a6d79"></span>
## Set user properties

<span id="bb79d017"></span>
### ProfileSet

Set user properties, override if they exist, and create if they don't.

```TypeScript
appLog.profile()?.set({
  "set1": "value",
  "set2": "value"
})
```


<span id="ac1a9457"></span>
### ProfileSetOnce

Set user properties, if they exist, they are not set, and if they do not exist, they are created. Suitable for first\-time relevant user attributes, such as first visit time, etc.

```TypeScript
appLog.profile()?.setOnce({
  "setOnce": "value"
})
```


<span id="3346987f"></span>
### **ProfileIncrement**

Set the properties of the numeric type to accumulate.

```TypeScript
appLog.profile()?.increment({
  "increment": 1
})
```


<span id="c06dfe26"></span>
### **ProfileAppend**

Set the user properties of the List type to be continuously added to the List.

```TypeScript
appLog.profile()?.append({
  "appendStr": "1",
  "appendNum": 1
})
```


<span id="4248c6ba"></span>
### **ProfileUnset**

Delete the user's attributes.

```TypeScript
appLog.profile()?.unset("set2")
```


<span id="95bb9a75"></span>
# Get platform ID and notifications

<span id="26c5f432"></span>
## Subscribe to DID

```JavaScript
appLog.topicReceiver()?.on(Topic.DidReady, (didInfo) => {
  setTimeout(() => {
    hilog.info(0x0000, 'AppLogH', `AppLog did ready:  ${didInfo["bd_did"]}`)
  })
})

didInfo format:
//device_info_from indicates whether the information is from local or server level request return
//device_info_from: did_from_remote indicates that the data is returned from the server level
//device_info_from: did_from_local indicates that the data is from the local cache
{
    "bd_did": "xxxx",
    "install_id": xxxx,
    "device_info_from": "did_from_remote"
}
```


<span id="c62f7a0f"></span>
## Request SSID

> This section will be supported after 1.3.1.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Invoke timing description: Please start requesting SSID after the internal initialization of the SDK is completed. How to judge that the initialization of the SDK is completed, you can subscribe to HeaderReady.</div>


<span id="9d4e4cb5"></span>
### requestSsidWithCurrUUID

Use the uuid/uuidType values in the current SDK (e.g. multi\-caliber) to request the corresponding SSID.

```TypeScript
//Call requestSsidWithCurrUUID please after HeaderReady
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithCurrUUID()
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})
```


<span id="efd89b7c"></span>
### requestSsidWithSpecifyUUID

Use the developer\-specified uuid/uuidType (if multi\-caliber is involved) values to request the corresponding SSID.

```TypeScript
//Call requestSsidWithSpecifyUUID please after HeaderReady
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithSpecifyUUID("test")
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})

//Only for multi-caliber
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithSpecifyUUID("test", "test_type")
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})
```


<span id="77fbdc1a"></span>
# AB experiment

AB experiment is turned off by default (consistent with Android), if you need to use AB experiment, you need to manually turn it on first.

<span id="a5ba83cb"></span>
## Activate AB experiment function

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//Open AB experiment, it is recommended to call between init and start
appLog.abTest()?.enablePlugin()
appLog.start()
```


<span id="f53b288e"></span>
## Obtain AB experimental server level configuration

```TypeScript
//It is recommended to obtain all experimental results each time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAllAbTestConfigs()
})
```


<span id="a16d654f"></span>
## Perform AB experimental exposure

```TypeScript
//It is recommended to trigger the experiment every time after obtaining the latest AB
appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
    appLog.abTest()?.getAbConfig("ab_key", defaultValue)
})
```


<span id="1580b577"></span>
## Get List of Exposed Experimental VIDs

```TypeScript
appLog.abTest()?.getAbSdkVersion()
```


<span id="2a41e8e0"></span>
## Subscribe to ABS server level offload configuration acquisition

```TypeScript
appLog.topicReceiver()?.on(Topic.ABTestConfigReady, (abTestConfig) => {
  hilog.info(0x0000, 'AppLogH', `AppLog abtest config ready:  ${JSON.stringify(abTestConfig)}`)
})

abTestConfig format:
detailed experiment configuration
{
    "ab": {
        "val": "访问页面 A", // viewpage A
        "vid": "1"
    },
    "ba": {
        "val": "对照版", // comparison version
        "vid": "2"
    },
    "tt": {
        "val": true,
        "vid": "3"
    }
}
```


<span id="fec35033"></span>
## Subscribe to New Exposure Vid Records

```TypeScript
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


<span id="c0f7654e"></span>
# H5 through the introduction

<span id="ada30984"></span>
## Open the embedded H5 page

If your application integrates the Web/JS SDK and the Harmony SDK at the same time, by default, all H5 events will be reported through the Web/JS SDK. If you want the H5 event to be reported by the Harmony SDK, you can use the embedded H5 function to get through. At this time, the events generated on the H5 page will be reported through the Harmony SDK, not in the Web/JS SDK. This kind of takeover reporting scenario will reuse the `user_unique_id`and public properties set by the Harmony side, but also support the uuid/public properties on the web side setting/update side when getting through. Please pay attention to which side of the data is used when getting through. If it is completely subject to the end, you can Remove the uuid/common attribute operation on the web SDK side.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get through the function, the Web/JS SDK and the Harmony SDK need to be integrated and cooperate with each other simultaneously. Web/JS SDK integration please refer to <a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration">Web/JavaScript SDK Integration</a>.</div>



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
   


<span id="2ad2b8d3"></span>
# multi\-instance correlation

In the current version, each instance is newly created, so creating a new AppLog corresponds to passing in a different application instance.

```TypeScript
import { AppLog, InitConfig } from '@volcengine/applog'

Create a new AppLog instance
let appLog1 = new AppLog()
//init sdk pass in the configuration, after init you can
appLog1.init(context, new InitConfig('yourAppId1', 'yourChannel')
  //whether to open the log
  .setLogEnabled(true))
  
//Harmony SDK needs to manually call start to start collecting sensitive information and sending requests
appLog1.start()

Create a new AppLog instance
let appLog2 = new AppLog()
//init sdk pass in the configuration, after init you can
appLog2.init(context, new InitConfig('yourAppId2', 'yourChannel')
  //whether to open the log
  .setLogEnabled(true))
  
//Harmony SDK needs to manually call start to start collecting sensitive information and sending requests
appLog2.start()
```


<span id="fba0fd4b"></span>
# Component Exposure Event Acquisition\-Beta

> Since: 1.3.3 \-rc3, this function depends on system capabilities, and similar lists such as LazyList are not supported for the time being.


Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.

> The current version capabilities are basically aligned with Android, and time exposure configuration and debug views are not supported for the time being.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Can be distinguished by the $exposure_type attribute inside the exposure event:</div>



* <div data-tips="true" data-tips-type="tip">$exposure_type: 0 first exposure</div>


* <div data-tips="true" data-tips-type="tip">$exposure_type: 3 duplicate exposures</div>


* <div data-tips="true" data-tips-type="tip">$exposure_type: 6 Exposure returned from other pages</div>


* <div data-tips="true" data-tips-type="tip">$exposure_type: 7 Background Return Exposure</div>



<div data-tips="true" data-tips-type="tip">If you want to achieve the effect of only exposing the component once, you can filter the first exposure by $exposure_type == 0 in the new exposure callback.</div>


```JavaScript
//Open the plugin
import { AppLog, InitConfig } from '@volcengine/applog'

let appLog = new AppLog()
let config = new InitConfig('yourAppId', 'yourChannel')
appLog.init(context, config)
//Open the exposure plugin
appLog.exposure()?.enablePlugin()
appLog.start()

//use plugins
//You need to add an ID to the component.
Button('Test', { stateEffect: true, type: ButtonType.Capsule })
  .id("test_btn"))

//Please start monitoring after the page is built. If the input is too early and the corresponding component cannot be found through NodeId, the exposure cannot be processed.
//Start exposure monitoring, and pass the ID to the SDK during exposure to determine which component's exposure needs to be monitored
appLog.exposure()?.observeByNodeId("test_btn", this.getUIContext(), {
    //Optional, default is "$bav2b_exposure"
    eventName: "custom_exposure",
    //Optional, custom exposure event properties
    properties: {
        "test": "test"
    },
    //Optional, exposure configuration, effective exposure area and exposure event callback
    //Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
    //Exposure event callback: When an exposure event is triggered, the callback will carry properties related to the current exposure event, which can be customized and appended, and supports filtering
    config: {
        exposureCallback: (param) => {
          //Support adding custom properties to callbacks
          //true keep exposure events
          return true
        }
    }
})

Discontinue exposure monitoring when appropriate, such as leaving the page or other logic
appLog.exposure()?.disposeByNodeId("test_btn")
```


<span id="6c5cbd76"></span>
# Full event tracking \-beta

> Since: 1.3.3 \-rc3, this feature depends on system capabilities, and some components may not support listening, such as the Tab component.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since Harmony no longer recommends route page routing, it mainly pushes Navigation component navigation, so the SDK is mainly based on Navigation component navigation.</div>


> Tab switching monitoring is not supported for the time being. At present, the system Tab monitoring is not perfect. It is impossible to monitor Tab entry and exit, but only Tab switching.


```JavaScript
onWindowStageCreate(windowStage: window.WindowStage): void {
  //It is recommended to enable EntryAbility loadContent to complete the page lifecycle
  windowStage.loadContent('pages/Index', (err, data) => {
    appLog.bav()?.enablePlugin(windowStage.getMainWindowSync().getUIContext(), {
      //Whether to collect the page departure event
      enablePageLeaveEvent: true,
      //Whether to collect component click events
      enableClickEvent: true
    })
  })
}
```


<span id="fc45bb72"></span>
# acquisition duration event

> This section will be supported after 1.3.1.


Events with time attributes can use the duration event capture interface, such as capturing video playback duration events. Example:

```JavaScript
//Called when the video starts playing
applog.eventPlugin()?.startDurationEvent("play");

//Called when the video is paused
applog.eventPlugin()?.pauseDurationEvent("play");

//Called when the video continues to play
applog.eventPlugin()?.resumeDurationEvent("play");

//Called at the end of playback, a play event will be reported at this time, with a $event_duration attribute (the playback time is recorded, in milliseconds)
applog.eventPlugin()?.stopDurationEvent("test", {
      "key": "value"
})

//Support custom duration event name, the default event name is the first parameter of the method
applog.eventPlugin()?.stopDurationEvent("play", {
      "key": "value"
}, "custom_play")
```


<span id="2d06e283"></span>
# Other scenarios

<span id="f71b8160"></span>
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


<span id="dce022a3"></span>
## Switch account settings Data sending method

Like Android, when privacy mode is turned on, the SDK stops receiving events and discards them, and stops sending network requests.

```Java
applog.eventPlugin()?.setPrivacyMode(true); //The default is false, and it is true after setting. If it is not collected, it will not be reported.
```


<span id="0e5ea7c6"></span>
## Configuration Scheme (optional)

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification), configure Scheme, otherwise you can skip this step.

<span id="d5cd1f14"></span>
### Method 1, use Devtools built\-in to scan

This method does not require the configuration of a wake\-up protocol.

After integrating Devtools, click on Console \- \> Scan, and follow the process.

<span id="950a9d87"></span>
### Method 2, traditional scan code jump

At this stage, Harmony system browser has supported scanning code jump.

<span id="337429f6"></span>
### Get URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/380b7a6cec9c4b8b9b461fa7bf8334a3~tplv-goo7wpa0wc-image.image) </span>

<span id="15452677"></span>
### Configure URL Scheme

<span id="65d8a779"></span>
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


<span id="68e3dff2"></span>
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
