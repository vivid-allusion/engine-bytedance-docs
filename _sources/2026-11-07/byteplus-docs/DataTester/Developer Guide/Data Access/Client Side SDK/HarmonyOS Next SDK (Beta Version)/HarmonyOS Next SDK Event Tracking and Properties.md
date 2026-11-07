---
title: "HarmonyOS Next SDK Event Tracking and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/HarmonyOS-Next-SDK-Event-Tracking-and-Properties"
---

<span id="28951817"></span>
# User and user attributes

```JavaScript
// get user information sector
appLog.user()
```


<span id="0685d184"></span>
## login status change call

<span id="086fb70e"></span>
### Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in. 6.13.0 + version supports calling before initializing AppLog to set the uuid of the logged\-in user.

```JavaScript
// configure UUID
appLog.user()?.setUserUniqueID("your_uuid")

// If there is a need for multiple calibers, you can refer to the settings below
// configure UUID + UUIDType
appLog.user()?.setUserUniqueID("your_uuid", "your_uuid_type")
// The setUserUniqueID(uuid) with a single parameter is equivalent to the setUserUniqueID(uuid, lastuuidType) with two parameters. However, by default, uuidType does not exist. If uuidType has been set, and want to clear it, additional settings are required:
appLog.user()?.setUserUniqueID("your_uuid", null)
```


<span id="107cad9f"></span>
### Account login

Called when the account is logged out.

```JavaScript
// log out UUID
appLog.user()?.setUserUniqueID(null)

// If there is a need for multiple calibers, you can refer to the settings below
// log out UUID + UUIDType
appLog.user()?.setUserUniqueID(null, null)
```


<span id="dbb785df"></span>
## Multi\-ID caliber

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After 1.3.0 version support, only privatization support, multi\-ID caliber function needs to be opened separately, when using, need to report the user ID, ID type, while configuring the id_bind relationship, as accurately as possible to restore a real user. For more information and instructions on how to use multi\-ID calibers, see <a href="https://www.volcengine.com/docs/56651/1362118">Advanced Features: Multi\-Application/Multi\-Agent/Multi\-ID Types </a>.</div>


```TypeScript
// Instance display
appLog.user()?.bind({
  "id_type_1": "id_type_value_1",
  "id_type_2": "id_type_value_2"
}, (result: IDBindParams) => {
  hilog.info(0x0000, 'AppLogH', `IDBindSuccess result: ${JSON.stringify(result)}`)
  // update user status
  appLog.user()?.setUserUniqueID("id_type_value_1", "id_type_1")
}, (code: number, message: StringOrNull) => {
  hilog.info(0x0000, 'AppLogH', `IDBindFail code: ${code}, message: ${message}`)
})
```


<span id="35480c2f"></span>
## Set user properties

<span id="2f41fe7a"></span>
### ProfileSet

Set user properties, override if they exist, and create if they don't.

```TypeScript
appLog.profile()?.set({
  "set1": "value",
  "set2": "value"
})
```


<span id="35f0ecda"></span>
### ProfileSetOnce

Set user properties, if they exist, they are not set, and if they do not exist, they are created. Suitable for first\-time relevant user attributes, such as first visit time, etc.

```TypeScript
appLog.profile()?.setOnce({
  "setOnce": "value"
})
```


<span id="3f92264c"></span>
### **ProfileIncrement**

Set the properties of the numeric type to accumulate.

```TypeScript
appLog.profile()?.increment({
  "increment": 1
})
```


<span id="d9260f9b"></span>
### **ProfileAppend**

Set the user properties of the List type to be continuously added to the List.

```TypeScript
appLog.profile()?.append({
  "appendStr": "1",
  "appendNum": 1
})
```


<span id="b54a8e1c"></span>
### **ProfileUnset**

Delete the user's attributes.

```TypeScript
appLog.profile()?.unset("set2")
```


<span id="c2ea8cf2"></span>
# Events and event properties

<span id="ab0c536f"></span>
## Event tracking

The user behavior log takes the form of **event event + attribute params** . Events generally correspond to multiple attributes, or only events have no attributes. Code event tracking schemes are typically designed by data analysts or product operations.


* Code event tracking that only reports events, as follows:


```TypeScript
// Example: reporting event, this event does not include property
*// Placed in the corresponding position of business logic
appLog.event("event")
```



* Code event tracking for reporting events and corresponding properties, as follows:


```TypeScript
// Example: reporting event, this event includes two properties
*// a string type property, with property name key_string, and property value value_string
*// a int type property, with property name key_int, and property value 10
*// Placed in the corresponding position of business logic
appLog.event("event", {
  "key_string": "value_string",
  "key_int": 10
})
```


<span id="ff43a4dc"></span>
## Event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="cfece86b"></span>
### Set public properties

```TypeScript
/* 
 * Example: set custom public property with property name key_public and  property value value_public
 * Please note that about custom “public property”：
 * 1. The reporting mechanism is to submit with each log sending, and the default log sending frequency is 1 minute.
 *    So if you continuously modify custom public properties within one minute, the last modification before sending the log shall prevail; 
 * 2. It is not recommended to make frequent modifications, such as modifying once per second.
 */
appLog.setHeaderInfo("key_public", "value_public")
```


<span id="0f819917"></span>
### Remove public attributes

```TypeScript
// Example: Removing a public property named key_public
appLog.removeHeaderInfo("key_public")
```


<span id="6f377434"></span>
# Subscription platform ID

<span id="d901d252"></span>
## Subscribe Did Ready

```JavaScript
appLog.topicReceiver()?.on(Topic.DidReady, (didInfo) => {
  setTimeout(() => {
    hilog.info(0x0000, 'AppLogH', `AppLog did ready:  ${didInfo["bd_did"]}`)
  })
})

didInfo format:
// device_info_from indicates whether the information is from the local or server-side request return
// device_info_from: did_from_remote indicates that the data is returned from the server
// device_info_from: did_from_local indicates that the data comes from the local cache
{
    "bd_did": "xxxx",
    "install_id": xxxx,
    "device_info_from": "did_from_remote"
}
```


<span id="5f24e54b"></span>
# Component Exposure Event Capture

Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">1.2.0 later versions support, users need to manually flag and listen to the exposure events of a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.</div>


> The current version capabilities are basically aligned with Android, and time exposure configuration and debug views are not supported for the time being.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Can be distinguished by the $exposure_type attribute inside the exposure event:</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 0 first exposure</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 3 duplicate exposures</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 6 Exposure returned from other pages</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 7 Background Return Exposure</div>


<div data-tips="true" data-tips-type="tip">If you want to achieve the effect of only exposing the component once, you can filter the first exposure by $exposure_type == 0 in the new exposure callback.</div>


```JavaScript
//  Need to add an ID to the component
Button('Test', { stateEffect: true, type: ButtonType.Capsule })
  .id("test_btn"))

//  Please start monitoring after page is built. If the input is too early and the corresponding component cannot be found through the NodeId, exposure cannot be processed
//  Start exposure monitoring and pass the ID to the SDK during exposure to determine which component needs to be monitored for exposure
appLog.exposure()?.observeByNodeId("test_btn", this.getUIContext(), {
    //  Optional, the default is "$bav2b_exposure"
    eventName: "custom_exposure",
    //  Optional, custom exposure event property
    properties: {
        "test": "test"
    },
    //  Optional, exposure configuration, effective exposure area and exposure event recall
    //  Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
    //  Exposure event callback: When an exposure event is triggered, the callback will carry properties related to the current exposure event, which can be customized and appended, and supports filtering
    config: {
        exposureCallback: (param) => {
          //  Support adding custom properties in callbacks
          //  true keep exposure events
          return true
        }
    }
})

//  Stop exposure monitoring appropriately, such as leaving the page or other logic
appLog.exposure()?.disposeByNodeId("test_btn")
```


<span id="d83da2be"></span>
# Full event tracking \-beta

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">1.2.0 later version support, since Hongmeng no longer recommends route page routing, the main push Navigation component navigation, so the SDK is mainly Navigation component navigation.</div>


> Tab switching monitoring is not supported for the time being. At present, the system Tab monitoring is not perfect, and Tab entry and exit cannot be monitored. Only Tab switching can be monitored.


```JavaScript
onWindowStageCreate(windowStage: window.WindowStage): void {
  // It is recommended to open while EntryAbility loadContent, so that achieve a more complete lifecycle of the page
  windowStage.loadContent('pages/Index', (err, data) => {
    appLog.bav()?.enablePlugin(windowStage.getMainWindowSync().getUIContext(), {
      // whether collect page leave event
      enablePageLeaveEvent: true,
      // whether collect component click event
      enableClickEvent: true
    })
  })
}
```
