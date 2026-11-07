---
title: "HarmonyOS Next SDK Event Tracking and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/HarmonyOS_Next_SDK_Event_Tracking_and_Properties"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The HarmonyOS Next SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration">HarmonyOS Next SDK Integration</a></div>


<span id="f9630876"></span>
# User and user attributes

```JavaScript
//Get user information module
appLog.user()
```


<span id="5b4c2c9f"></span>
## Login status change call

<span id="dc31b648"></span>
### Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the criteria before and after the user logs in. 6.13.0 + version supports calling before initializing AppLog to set the uuid of the logged in user.

```JavaScript
//Set UUID
appLog.user()?.setUserUniqueID("your_uuid")

//If you have multi-criteria requirements, you can see the settings below.
//Set UUID + UUIDType
appLog.user()?.setUserUniqueID("your_uuid", "your_uuid_type")
//The setUserUniqueID (uuid) of the single parameter is equivalent to the setUserUniqueID (uuid, lastuuidType) of the double parameter, but the uuidType is not available by default. If you want to empty the uuidType after setting it, you need to set it extra:
appLog.user()?.setUserUniqueID("your_uuid", null)
```


<span id="cbeb60af"></span>
### Account login

Called when the account is logged out.

```JavaScript
// Log out of UUID
appLog.user()?.setUserUniqueID(null)

//If you have multi-criteria requirements, you can see the settings below.
// Logout UUID + UUIDType
appLog.user()?.setUserUniqueID(null, null)
```


<span id="7c6df339"></span>
## Set user properties

<span id="1420ad7f"></span>
### ProfileSet

Set user properties, override if they exist, and create if they don't.

```TypeScript
appLog.profile()?.set({
  "set1": "value",
  "set2": "value"
})
```


<span id="3fd33c92"></span>
### ProfileSetOnce

Set user properties, if they exist, they are not set, and if they do not exist, they are created. Suitable for first\-time relevant user attributes, such as first visit time, etc.

```TypeScript
appLog.profile()?.setOnce({
  "setOnce": "value"
})
```


<span id="a46d1475"></span>
### **ProfileIncrement**

Set the properties of the numeric type to accumulate.

```TypeScript
appLog.profile()?.increment({
  "increment": 1
})
```


<span id="83b8727c"></span>
### **ProfileAppend**

Set the user properties of the List type to be continuously added to the List.

```TypeScript
appLog.profile()?.append({
  "appendStr": "1",
  "appendNum": 1
})
```


<span id="f1beecd0"></span>
### **ProfileUnset**

Delete the user's attributes.

```TypeScript
appLog.profile()?.unset("set2")
```


<span id="17e2c7d3"></span>
# Events and event properties

<span id="4c833d29"></span>
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


<span id="4cc3b7e4"></span>
## Event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="f166818c"></span>
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


<span id="e42dbff8"></span>
### Remove public attributes

```TypeScript
// Example: Remove a public property named key_public
appLog.removeHeaderInfo("key_public")
```


<span id="bc0b7464"></span>
# Platform ID

<span id="07e460b1"></span>
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


<span id="86ebd246"></span>
## Request SSID

> This section will be supported after 1.3.1.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Invoke timing description: Please start requesting SSID after the internal initialization of the SDK is completed. How to judge that the initialization of the SDK is completed, you can subscribe to HeaderReady.</strong></div>


<span id="786c90f5"></span>
### requestSsidWithCurrUUID

Use the uuid/uuidType values in the current SDK (e.g. multi\-criteria) to request the corresponding SSID.

```TypeScript
//Call requestSsidWithCurrUUID please after HeaderReady
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithCurrUUID()
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})
```


<span id="0fa518d7"></span>
### requestSsidWithSpecifyUUID

Use the developer\-specified uuid/uuidType (if multi\-criteriaa is involved) values to request the corresponding SSID.

```TypeScript
//Call requestSsidWithSpecifyUUID please after HeaderReady
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithSpecifyUUID("test")
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})

//Only for multi-criteria
applog.topicReceiver()?.stickyOnce(Topic.HeaderReady, async () => {
  let ssid = await applog.user()?.requestSsidWithSpecifyUUID("test", "test_type")
  hilog.info(0x0000, 'AppLogH', `AppLog ssid:  ${ssid}`)
})
```


<span id="781888ff"></span>
# Component Exposure Event Capture

> This section is supported after 1.2.0 & 1.3.1 \-all.


Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.</div>


> The current version capabilities are basically aligned with Android, and time exposure configuration and debug views are not supported for the time being.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Can be distinguished by the $exposure_type attribute inside the exposure event:</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 0 first exposure</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 3 duplicate exposures</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 6 Exposure returned from other pages</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 7 Background Return Exposure</div>


<div data-tips="true" data-tips-type="tip">If you want to achieve the effect of only exposing the component once, you can filter the first exposure by $exposure_type == 0 in the new exposure callback.</div>


```JavaScript
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


<span id="0ed3b8d3"></span>
# Full event tracking \-beta

> This section is supported after 1.2.0 & 1.3.1 \-all.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since Hongmeng no longer recommends route page routing, it mainly pushes Navigation component navigation, so the SDK is mainly based on Navigation component navigation.</div>


> Tab switching monitoring is not supported for the time being. At present, the system Tab monitoring is not perfect. It is impossible to monitor Tab entry and exit, but only Tab switching.


```JavaScript
onWindowStageCreate(windowStage: window.WindowStage): void {
  //It is recommended to enable EntryAbility loadContent to complete the page lifecycle
  windowStage.loadContent('pages/Index', (err, data) => {
    appLog.bav()?.enablePlugin(windowStage.getMainWindowSync().getUIContext(), {
      //Whether to capture the page departure event
      enablePageLeaveEvent: true,
      //Whether to collect component click events
      enableClickEvent: true
    })
  })
}
```


<span id="a4bd19f0"></span>
# Switch account settings Data sending method

Like Android, when privacy mode is turned on, the SDK stops receiving events and discards them, and stops sending network requests.

```Java
applog.eventPlugin()?.setPrivacyMode(true); //The default is false, and it is true after setting. If it is not collected, it will not be reported.
```


<span id="be387146"></span>
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
