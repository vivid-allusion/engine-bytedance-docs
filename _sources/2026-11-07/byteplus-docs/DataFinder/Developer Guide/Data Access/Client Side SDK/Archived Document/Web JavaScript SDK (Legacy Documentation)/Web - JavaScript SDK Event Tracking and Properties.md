---
title: "Web/JavaScript SDK Event Tracking and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JavaScript_SDK_Event_Tracking_and_Properties"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Web/JS SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration">Web/JavaScript SDK Integration</a></div>


> Before reporting events and attributes, please read the [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification)introduction.


<span id="_1-用户与用户属性"></span>
# 1. Users and user attributes

<span id="_1-1-登录态变化调用"></span>
## 1.1 Login state change call

<span id="_1-1-1-账户登录"></span>
### 1.1.1 Account login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```javascript
window.collectEvent('config', {
    user_unique_id: "{{USER_UNIQUE_ID}}"  
});
```


<span id="_1-1-2-账户登出"></span>
### 1.1.2 Account Logout

Called when the account is logged out.

```javascript
window.collectEvent('config', {
    user_unique_id: null 
});
```


<span id="_1-2-设置用户属性"></span>
## 1.2 Setting user properties

<span id="_1-2-1-profileset"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```javascript
//Example: Set the user property, the property name is key, and the property value is value
window.collectEvent('profileSet', {
    key: 'value' //value support string, number, array
})
```


<span id="_1-2-2-profilesetonce"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```javascript
//Example: Set a user property with the property name key_once and the property value value_once
window.collectEvent('profileSetOnce', {
    key_once: 'value_once' //value support string, number, array
})
```


<span id="_1-2-3-profileincrement"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```javascript
//Example: Set the user property, the property name is key, and the property value is 1
window.collectEvent('profileIncrement', {
    key: 1
})
```


<span id="_1-2-4-profileappend"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```javascript
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
window.collectEvent('profileAppend', {
    key: 'value_append'
})
```


<span id="_1-2-5-profileunset"></span>
### 1.2.5 profileUnset

Delete the user's attributes.

```javascript
//Example: Delete a user attribute named key
window.collectEvent('profileUnset', 'key')
```


&nbsp;

<span id="_2-事件与事件属性"></span>
# 2. Events and event properties

<span id="_2-1-上报代码埋点"></span>
## 2.1 Reporting code event tracking

<span id="160d002a"></span>
### Instructions for use

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.


* Code event tracking that only reports events, as follows:

   ```javascript
   //Example: Report an event that does not contain properties
   //placed in the corresponding position of business logic
   window.collectEvent('test_event');
   ```
   

* Code event tracking for reporting events and corresponding properties, as follows:

   ```javascript
   //Example: Report an event, which contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //. A property of type int, the property name key_int, the property value is 10
   //placed in the corresponding position of business logic
   window.collectEvent('test_event', {
      key_string: 'value_string',
      key_int: 10
   });
   ```
   


<span id="24a73132"></span>
### Precautions


* It is recommended that event names and properties be lowercase.

   * Event naming only supports letters, numbers and underscores, do not use init, start and other SDK internal API names.

   * Please refer to the data type of the event attribute value [1. Property data types](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#_1-%E5%B1%9E%E6%80%A7%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B); do not use nested object in the event attribute, that is, the attribute value does not support the object type for the time being, and can be converted to string for reporting.

* Do not assign window.collectEvent to a temporary variable. Assignment may result in failure to report or error.


<span id="5fcdb65c"></span>
### Error example (please do not refer to)

```TypeScript
//exception writing
const windowTea = window.collectEvent
windowTea('init')
windowTea('start')
windowTea('test')

This coding method may result in the inability to report events when using async to asynchronous loading of SDK files, due to the following reasons:
there is a pre code of SDK:
(function(win, export_obj) {
        win['LogAnalyticsObject'] = export_obj;
        if (!win[export_obj]) {
            function _collect() {
                _collect.q.push(arguments);
            }
            _collect.q = _collect.q || [];
            win[export_obj] = _collect;            
        }
        win[export_obj].l = +new Date();
    })(window, 'collectEvent');
This pre code is to ensure that when the SDK file is not loaded, the business can execute `window.collectEvent` without errors and save the business-called API. 
After the SDK file is fully loaded, the SDK will reassign `window.collectEvent` to the actual method, and then sequentially execute the saved API queue.
The business assign the value of window.collectEvent to windowTea when SDK is not fully loaded, which will lead to the value of windowTea will always be this pre code, instead of reporting events.
```


<span id="_2-2-事件公共属性"></span>
## 2.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events. When the page jumps, you need to reload the SDK and reset the required public properties (except for single\-page applications).

<span id="_2-2-1-设置公共属性"></span>
### 2.2.1 set public properties

```javascript
//Example: Set a custom public property with the property name key_public and the property value value_public
window.collectEvent('config', {
   key_public: 'value_public'
});
```


<span id="_2-3-页面跳转前上报埋点"></span>
## 2.3 Report event tracking before page jump

Please note that when event tracking is designed, it is not recommended to jump to the page immediately after sending the event. In this situation, the reporting request may fail and statistics may be missing. Please consider one of the following two options:


1. Use `beconEvent`.

   `beconEvent`will send the event tracking through the browser's feature `sendbeacon`to compensate for data reporting as much as possible.

   ```javascript
   window.collectEvent('beconEvent', 'event', {})
   window.location.href = 'https://xxx.com';
   ```
   

2. Add a delay to give `Ajax`some time.

   ```javascript
   window.collectEvent('test_event');
   setTimeout(()=>{
       window.location.href = 'https://xxx.com'
   }, 150)
   ```
   


<span id="_3-api说明"></span>
# 3. API description

<span id="_3-1-config-paramsobj"></span>
## 3.1 config(paramsObj)

The config command is used to set up reporting custom fields and some configuration items.


* It needs to be called after init.

* Can be called multiple times, the new configuration will be merged with the old configuration, and the settings with the same name will be overwritten (equivalent to Object.assign).

* The parameter is an object.

   Parameter classification:

   * SDK own configuration items and debugging related fields

   * User ID related fields

   * User Attributes (Public Attributes)

      * preset

      * custom

   * Event properties common to events


```javascript
//1. The first call

window.collectEvent('config', {
    language: 'cn',
    weeks: 'Monday',
})
window.collectEvent('send')
//2. The events sent at this time all include cn, Monday.

//3. Second call

window.collectEvent('config', {
    language: 'en',
})
//4. The events sent at this time all include en, Monday.
```


The config contains preset fields such as user ID, user attributes, public attributes, system occupancy, and so on. The following fields are fields occupied by the SDK, each field has a specific meaning, and the priority of the field can be set higher than the default assignment of the SDK.


|Type |Field |Value type |Field description |Example |
|---|---|---|---|---|
|user ID |user_unique_id |string |User unique identity. When no user_unique_id is set, it is set to web_id. |When the business party sets \* to the following values, it will be ignored. 【'null', 'undefined', '0', '', 'None'】 |
|public attribute |device_model |string |Equipment model |3.3.4 start, do simple ua analysis for mobile end, such as: iphone/ipad/mi1 metal/SM\-A8000/, etc. |
|public attribute |os_name |string |Operating System |Sdk report by default: windows/mac/android/ios |
|public attribute |os_version |string |operating system version |SDK default reporting |
|public attribute |platform |string |platform type |Default reporting wap/web |
|public attribute |browser |string |Browser name |default report |
|public attribute |browser_version |string |Browser version |default report |
|public attribute |language |string |browser language |default report |
|public attribute |referrer |string |Forward Address |default report |
|public attribute |referrer_host |string |Forward Domain Name |default report |
|public attribute |resolution |string |resolution |default report |
|public attribute |screen_height |number |Screen height |default report |
|public attribute |screen_width |number |screen width |default report |
|public attribute |sdk_version |string |ByteFinder\-sdk version |default report |
|public attribute |timezone |int |Time Zone |default report |
|public attribute |region |string |region |The business party sets it up by itself |
|public attribute |traffic_type |string |traffic type | |
|public attribute |utm_source |string |promotion source |SDK default capture |
|public attribute |utm_campaign |string |promotional activities |SDK default capture |
|public attribute |utm_medium |string |promotion media |SDK default capture |
|public attribute |utm_content |string |promotional content |SDK default capture |
|public attribute |utm_term |string |promotion keywords |SDK default capture |
|system occupancy |custom | | | |


<span id="_3-2-页面浏览事件"></span>
## 3.2 Page View Events

<span id="_3-2-1-sdk-默认调用"></span>
### 3.2.1 SDK default call

predefine_pageview event is invoked by default, to close, please refer to [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_) Section 3.3.

<span id="_3-2-2-业务手动调用"></span>
### 3.2.2 business call manually

Call this method to actively report a PV event with the same type of parameter as the event property of a normal event.

If a custom event property is passed in, it will be merged with the default event property; if there is a property with the same name, the default property will be overwritten.

```javascript
window.collectEvent("predefinePageView")
window.collectEvent("predefinePageView", {/**...*/})
//Override the default properties

window.collectEvent("predefinePageView", {
    url: 'xxx',
    url_path: 'xxx'
    // ...
})
```


<span id="_3-3-3-事件预置属性"></span>
### 3.3.3 event preset properties


|Field |Type |Must pass |Explain |Value example |
|---|---|---|---|---|
|url |string |No |Current page address | |
|url_path |string |No |Current page path, excluding protocol and host headers |/tea/app/10000/behaviorDetail |
|title |string |No |page title |Home |
|time |number |Yes |timestamp | |
|referrer |string |No |Page source, value of document.referrer | |


<span id="_3-3-4-对spa的支持"></span>
### 3.3.4 support for SPA

Because by default, the SDK will only report a PV event after the page is loaded and initialization is completed, but the SPA page will have multiple page routes, and the SDK will only load once on the main page, so it will not initiate PV when switching pages, resulting in no PV data for subsequent pages. Therefore, the SPA parameters can be enabled, and the SDK will report the PV again when the route changes.

```javascript
window.collectEvent("init", {
    spa: true
})
```


Of course, there may be some page parameters that are not up to date when the SDK listens to route changes. You can also manually report the PV when the route changes. Example of react:

```javascript
// <Router history={history} onUpdate={onUpdate}>

function onUpdate() {
    window.collectEvent("predefinePageView")
}
```


<span id="_3-3-获取平台生成的各种id"></span>
## 3.3 Obtaining various IDs generated by the platform

Obtain the token information of the SDK, which contains web_id, ssid, user_unique_id information. If you need to obtain the ID information of the SDK and make other settings, you can do the following:

```javascript
window.collectEvent('getToken', (token) => {
    The token data content is similar to the following:
    {
        "web_id":"6748002161499735560",
        "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
        "user_unique_id":"xxx",
    }
    window.collectEvent('test', {
      id: web_id/ssid
    })
});
```


<span id="_3-4-自定义webid"></span>
## 3.4 Custom webid

To change the default webid of the SDK, please set `enable_custom_webid: true`when the SDK is initialized, and then set it through setWebIDviaUnionID or setWebIDviaOpenID. The example is as follows:

```javascript
window.collectEvent('init', {
    enable_custom_webid: true
});
window.collectEvent('setWebIDviaUnionID', 'ssss')
window.collectEvent('setWebIDviaOpenID', 'ssss')
```


It should be noted that when enableCustomWebid is set, you must call setWebIDviaUnionID or setWebIDviaOpenID to set webid before the SDK will continue to execute the subsequent process.

This scenario is suitable for the H5 page to open in the WeChat Mini Program, and you need to pass WeChat's unionID or openID to the H5 page.

<span id="04de1357"></span>
## 3.5 Monitoring Lifecycle

You can configure whether to listen for broadcasts of a certain SDK lifecycle.


* On: Listen to the broadcast of an SDK lifecycle

   ```JavaScript
   window.collectEvent('on', 'ready', (data) => {
      //I heard that the sdk is ready, do something
      //Some messages have data
   })
   ```
   

* Off: cancel listening to the broadcast

   ```JavaScript
   //Cancel listening to the ready broadcast
   window.collectEvent('off', 'ready') 
   ```
   


<span id="b76a44ea"></span>
## 3.6 Event filtering

You can call filterEvent to filter the event. After calling, the event will be processed by filterEvent before being reported. If no value is returned, the original eventData is reported.

```JavaScript
window.collectEvent('filterEvent', (eventData) => {
//Please modify it according to the data structure of eventData.
  eventData[0].events.forEach(event => {
     // dosomething
  })
  return eventData This step is necessary
})
```
