---
title: "HarmonyOS Next SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/HarmonyOS_Next_SDK_API_Description"
---

This article introduces a series of APIs provided by HarmonyOS for you. You can call the corresponding API in combination with event tracking planning for event tracking.

<span id="be192182"></span>
# Core API Description

<span id="d7a3a62d"></span>
## init


* **Function:**  Initialize the SDK instance, depending on the ability context, so the call timing is suitable for the onCreate life cycle.

* **Definition:**  nit (context: common. Context, initConfig: InitConfig): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |context |common.Context |Yes |Ability context |
   |initConfig |InitConfig |Yes |SDK internal implementation manages initialization configuration classes |
   

* **Example:** 

   ```TypeScript
   class EntryAbility extends UIAbility {
       onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
           Create a new AppLog instance
           let appLog = new AppLog()
           //Hongmeng sdk channel as optional parameter
           let config = new InitConfig('yourAppId', 'yourChannel')
             //whether to open the log
             .setLogEnabled(true)
             //If it is reported to cloud native, you can set the reporting address to cloud native domain name
             .setUri(createByDomain('https://gator.volces.com'))
             
           //init sdk pass in the configuration, after init you can
           appLog.init(this.context, config)
           
           // ...
       }    
       // ...
   }
   ```
   


<span id="068d02d5"></span>
## start


* **Function:**  Let the SDK instance start to really prepare to perform event reporting, and the calling time is after init.

* **Definition:**  start (): void

* **Example:** 

   ```TypeScript
   class EntryAbility extends UIAbility {
       onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
           Create a new AppLog instance
           // ...
           //init sdk pass in the configuration, after init you can
           appLog.init(context, config)
           
           //Hongmeng SDK needs to manually call start to start collecting sensitive information and sending requests
           appLog.start()
       }    
       // ...
   }
   ```
   


<span id="b2d173ef"></span>
## event


* **Function:**  Report the event, it can only be called after initialization.

* **Definition:**  event (eventName: string, params?: EventRecord): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |eventName |string |Yes |Event name, cannot be nil or empty string |
   |params |EventRecord<br><br>= Record<string, number |string |boolean |
   

* **Example:** 

   ```TypeScript
   //Example: Report event event_name, the event does not contain properties
   //placed in the corresponding position of business logic
   appLog.event('event_name')
   
   //Example: Report event event_name, the event contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //a property of type int, the property name key_int, the property value is 10
   //placed in the corresponding position of business logic
   appLog.event('event_name', {
     'key_string': 'value_string',
     'key_int': 10
   })
   ```
   


<span id="c939db2b"></span>
## setHeaderInfo


* **Role:**  Set custom public properties (non\-persistent).

* **Definition:**  setHeaderInfo (key: string, value: ObjectValue): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |custom public property name |
   |value |ObjectValue<br><br>= number |string |boolean |
   

* **Example:** 

   ```TypeScript
   /*
    * Example: Set a custom public property with the property name key_public and the property value value_public
    * Please note about customizing "public properties":
    * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute.
    Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail;
    * 2. High-frequency modifications are not recommended, such as once per second.
    */
   appLog.setHeaderInfo('key_public', 'value_public')
   ```
   


<span id="237d27fa"></span>
## removeHeaderInfo


* **What:**  Removes custom public properties.

* **Definition:**  emoveHeaderInfo (key: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |Custom report key |
   

* **Example:** 

   ```TypeScript
   //Example: Remove a public property named key_public
   appLog.removeHeaderInfo('key_public')
   ```
   


<span id="c504efce"></span>
## topicReceiver


* **Function:**  SDK implements a set of subscription publishing mechanism. If you want to subscribe to some specific events inside SDK, you need to call topicReceiver to get the TopicReceiver object of the instance first.

* **Definition:**  topicReceiver (): TopicReceiver | null

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |TopicReceiver |The TopicReceiver class implements the mechanism of subscription publishing, which is roughly as follows<br><br>```TypeScript```<br>```TopicReceiver {```<br>```  abstract on(type: Topic, hook: DispatcherCallback): void```<br>```  abstract once(type: Topic, hook: DispatcherCallback): void```<br>```  abstract stickyOn(type: Topic, hook: DispatcherCallback): void```<br>```  abstract stickyOnce(type: Topic, hook: DispatcherCallback): void```<br>```  abstract off(type: Topic, hook?: DispatcherCallback): void```<br>```}```<br> |
   

* **Example:** 

   ```TypeScript
   appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
       // ...
   })
   ```
   


<span id="59fc82b5"></span>
# InitConfig API Description

InitConfig is a class that specializes in managing SDK initialization configuration, providing a series of methods to set initialization configuration items.

<span id="1344fc33"></span>
## InitConfig


* **Role:**  Instantiates an administrative initialization configuration item object.

* **Definition:**  constructor (appId: string, channel?: string)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |appId |string |Yes |App ID |
   |channel |string |No |Channel, set by the business itself |
   

* **Example:** 

   ```TypeScript
   let config = new InitConfig('yourAppId', 'yourChannel')
   ```
   


<span id="f8805806"></span>
## setLogEnabled


* **Function:**  Whether to open the SDK run log.

* **Definition:**  setLogEnabled (logEnabled: boolean): InitConfig

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |logEnabled |boolean |Yes |Whether to open the SDK run log. |
   

* **Example:** 

   ```TypeScript
   let config = new InitConfig('yourAppId', 'yourChannel')
     //whether to open the log
     .setLogEnabled(true)
   ```
   


<span id="d9d1ddbb"></span>
## setUri


* **Function:**  Set the reporting domain name.

* **Definition:**  setUri (uri: URiConfig): InitConfig

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |uri |URiConfig |Yes |The value of URI is a domain name.<br><br>The SDK provides `createByDomain`to assist in processing domain names, generating a series of request addresses that need to be used internally, including event reporting request addresses, activation request addresses, etc. |
   

* **Example:** 

   ```TypeScript
   let config = new InitConfig('yourAppId', 'yourChannel')
     //Set the domain name, through createByDomain can help generate a series of internal request addresses
     .setUri(createByDomain("https://gator.volces.com"))
   ```
   


<span id="a82079fe"></span>
## setOaidEnabled


* **Function:**  oaid acquisition switch.

* **Definition:**  setOaidEnabled (enabled: boolean): InitConfig

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enabled |boolean |Yes |OAID acquisition switch. |
   

* **Example:** 

   ```TypeScript
   let config = new InitConfig('yourAppId', 'yourChannel')
     //Open to get oaid.
     .setOaidEnabled(true)
   ```
   


<span id="72638170"></span>
## setOperatorInfoEnabled


* **Function:**  operator information collection switch.

* **Definition:**  setOperatorInfoEnabled (enabled: boolean): InitConfig

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enabled |boolean |Yes |Operator information collection switch. |
   

* **Example:** 

   ```TypeScript
   let config = new InitConfig('yourAppId', 'yourChannel')
     //Open to get oaid.
     .setOperatorInfoEnabled(true)
   ```
   


<span id="0daa2e24"></span>
# User Plugin API Description

User information plug\-in, set up and get user information, such as user_unique_id. The way to obtain user information plug\-ins is as follows:

```TypeScript
appLog.user()
```


<span id="fdf5a85f"></span>
## setUserUniqueID


* **Role:**  Set user_unique_id field.

* **Definition:**  setUserUniqueID (uuid: string | null, uuidType?: string | null): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |uuid |string |null |Yes, null. |
   |uuidType |string |null |No<br><br>When the value is not null, the SDK sets the value to the internally maintained user_unique_id_type field; similarly, when null, the SDK will empty the value of the user_unique_id_type field; |
   

* **Example:** 

   ```TypeScript
   //Set UUID
   appLog.user()?.setUserUniqueID("your_uuid")
   
   //If you have multi-caliber requirements, you can see the settings below.
   //Set UUID + UUIDType
   appLog.user()?.setUserUniqueID("your_uuid", "your_uuid_type")
   //The setUserUniqueID (uuid) of the single parameter is equivalent to the setUserUniqueID (uuid, lastuuidType) of the double parameter, but the uuidType is not available by default. If you want to empty the uuidType after setting it, you need to set it extra:
   appLog.user()?.setUserUniqueID("your_uuid", null)
   
   //Log out of UUID
   appLog.user()?.setUserUniqueID(null)
   
   //If you have multi-caliber requirements, you can see the settings below.
   //Logout UUID + UUIDType
   appLog.user()?.setUserUniqueID(null, null)
   ```
   


<span id="9cac155c"></span>
## getUserUniqueID


* **Role:**  Get the value of the user_unique_id field maintained internally by the SDK.

* **Definition:**  getUserUniqueID (): string | null

* **Example:** 

   ```TypeScript
   //Get the current UUID
   const uuid = appLog.user()?.getUserUniqueID()
   ```
   


<span id="c7296b39"></span>
## getUserUniqueIDType


* **Role:**  Get the value of the user_unique_id_type field maintained internally by the SDK.

* **Definition:**  getUserUniqueIDType (): string | null

* **Example:** 

   ```TypeScript
   //Get the current UUIDType
   const uuidType = appLog.user()?.getUserUniqueIDType()
   ```
   


<span id="b2333e41"></span>
# AB test Function Plugin API Description

The SDK provides AB test capabilities, providing AB test plugin, which contains a series of methods: getAbConfig, getAbSdkVersion, getAllAbTestConfigs. The way to get AB test plugin is as follows:

```TypeScript
appLog.abTest()
```


<span id="fcc01dd4"></span>
## getAbConfig


* **Function:**  Get AB test configuration value.

* **Definition:**  getAbConfig < T \> (key: string, defaultValue: T): T

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |NSString |Yes |AB test configured key |
   |defaultValue |T extends \*\*\*\* string |boolean |number |
   

* **Example:** 

   ```TypeScript
   //It is recommended to trigger the experiment every time after obtaining the latest AB
   appLog.topicReceiver().on(Topic.ABTestConfigReady, (_) => {
       appLog.abTest()?.getAbConfig("ab_key", defaultValue)
   })
   ```
   


<span id="b65f217f"></span>
## getAbSdkVersion


* **Function:**  Get the vids of the exposed AB test configuration.

* **Definition:**  getAbSdkVersion (): string

* **Example:** 

   ```TypeScript
   appLog.abTest()?.getAbSdkVersion()
   ```
   


<span id="d9a359e3"></span>
## getAllAbTestConfigs


* **Role:**  Get all configuration items for AB test.

* **Definition:**  getAllAbTestConfigs (): Record < string, ABTestItem \>

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |Record<string, ABTestItem\> |similar value<br><br>```JSON```<br>```{```<br>```    "ab": {```<br>```        "val": "访问页面 A",```<br>```        "vid": "1"```<br>```    },```<br>```    "ba": {```<br>```        "val": "对照版",```<br>```        "vid": "2"```<br>```    },```<br>```    "tt": {```<br>```        "val": true,```<br>```        "vid": "3"```<br>```    }```<br>```}```<br> |
   

* **Example:** 

   ```TypeScript
   appLog.topicReceiver()?.on(Topic.ABTestConfigReady, (abTestConfig) => {
     hilog.info(0x0000, 'AppLogH', `AppLog abtest config ready:  ${JSON.stringify(abTestConfig)}`)
   })
   /*abTestConfig format:Is the specific experimental configuration{    "ab": {        "Val": "Visit page A",        "vid": "1"    },    "ba": {        "Val": "Comparison",        "vid": "2"    },    "tt": {        "val": true,        "vid": "3"    }}*/
   ```
   


<span id="86c82366"></span>
# User Attributes Features Plugin API Description

Provides the ability to set user properties and provides a series of methods: profileSet, profileSetOnce, profileUnset, profileIncrement, profileAppend. The way to get the user properties plug\-in is as follows:

```TypeScript
appLog.profile()
```


<span id="2eb3011d"></span>
## set


* **Function:**  Set user properties, overwrite if they exist, and create if they don't exist.

* **Definition:**  set (profile: EventRecord): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profile |EventRecord<br><br>= Record<string, number |string |boolean |
   

* **Example:** 

   ```TypeScript
   appLog.profile()?.set({
     "set1": "value",
     "set2": "value"
   })
   ```
   


<span id="f0fba200"></span>
## setOnce


* **Function:**  Set user properties, do not set if they exist, create if they do not exist, suitable for first\-time related user properties, such as first access time. Unlike the set interface, if a profile has been successfully set through the setOnce interface, it is invalid to call the setOnce interface again on the profile.

* **Definition:**  setOnce (profile: EventRecord): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profile |EventRecord<br><br>= Record<string, number |string |boolean |
   

* **Example:** 

   ```TypeScript
   appLog.profile()?.setOnce({
     "setOnce": "value"
   })
   ```
   


<span id="958365b9"></span>
## increment


* **Function:**  Set the properties of the numeric type to accumulate.

* **Definition:**  increment (profile: ProfileIncrementType): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profile |ProfileIncrementType<br><br>= Record<string, number\> |Yes |Can only increment integers (can be negative integers). If a floating\-point number is passed in, the SDK will ignore it. |
   

* **Example:** 

   ```TypeScript
   appLog.profile()?.increment({
     "increment": 1
   })
   ```
   


<span id="8dc1f600"></span>
## append


* **Function:**  Set the user properties of the collection type, which can be continuously added to the collection.

* **Definition:**  append (profile: ProfileAppendType): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profile |ProfileAppendType<br><br>= Record<string, number |string\> |Yes |
   

* **Example:** 

   ```TypeScript
   appLog.profile()?.append({
     "appendStr": "1",
     "appendNum": 1
   })
   ```
   


<span id="b3c52257"></span>
## unset


* **Function:**  Delete the user's attributes.

* Definition: unset (profileKey: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileKey |NSString |Yes |The name of the profile to unset |
   

* **Example:** 

   ```TypeScript
   appLog.profile()?.unset("set2")
   ```
   


<span id="3a47e9f2"></span>
# Component Exposure Function Plugin API Description\-beta

> Since: 1.3.3 \-rc3, this function depends on system capabilities, and similar lists such as LazyList are not supported for the time being.


Provides the ability to set component exposure acquisition, providing some methods: observeByNodeId, disposeByNodeId. The way to obtain the component exposure plug\-in is as follows:

```TypeScript
appLog.exposure()
```


<span id="56568e27"></span>
## observeByNodeId


* **Role:**  Monitor element exposure by component ID.

* **Definition:**  observeByNodeId (id: string, context: UIContext, data?: ExposureData)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |id |string |Yes |Component ID |
   |context |UIContext |Yes |Ability context |
   |data |ExposureData |No |The ExposureData type is roughly as follows<br><br>```TypeScript```<br>```interface ExposureData {```<br>```  //Customizable exposure event name```<br>```  eventName?: string```<br>```  //Custom exposure event properties can be added```<br>```  properties?: EventRecord```<br>```  //Independent exposure configuration```<br>```  config?: ExposureConfig```<br>```}```<br> |
   

* **Example:** 

   ```TypeScript
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
   ```
   


<span id="2dca80cb"></span>
## disposeByNodeId


* **Function:**  Turn off the exposure of the corresponding component.

* **Definition:**  disposeByNodeId (id: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |id |string |Yes |Component ID |
   

* **Example:** 

   ```TypeScript
   Discontinue exposure monitoring when appropriate, such as leaving the page or other logic
   appLog.exposure()?.disposeByNodeId("test_btn")
   ```
