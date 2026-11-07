---
title: "Web/JS SDK Event Tracking and Properties (Experimental Metrics)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Web-JS-SDK-Event-Tracking-and-Properties-Experimental-Metrics"
---

> Before reporting events and properties, read the Data Format [Supported Data Formats (Custom Events/Properties)](https://docs.byteplus.com/docs/DataTester/Supported-Data-Formats-Custom-Events-Properties)Introduction.


<span id="3ddc3d4a"></span>
# 1. Users and user properties

<span id="b52f3505"></span>
## 1.1 Login state change call

<span id="88bb4279"></span>
### 1.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```javascript
window.collectEvent('config', {
    user_unique_id: "{{USER_UNIQUE_ID}}"  
});
```


<span id="3b88b015"></span>
### 1.1.2 Account Logout

Called when the account is logged out.

```plain
window.collectEvent('config', {
    user_unique_id: null 
});
```


<span id="d43168bc"></span>
## 1.2 Setting user properties

<span id="aca7709e"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```javascript
// Set the ID of your account system and ensure its uniqueness
window.collectEvent('profileSet', {
    key: 'value' // Values support strings, numbers, and arrays
})
```


<span id="16b60cb2"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```javascript
// Example: Set the user property with the property name key_once and the property value value_once
window.collectEvent('profileSetOnce', {
    key_once: 'value_once' // Values support strings, numbers, and arrays
})
```


<span id="dde4ecef"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```javascript
// Example: Set the user property with the property name key and the property value 1
window.collectEvent('profileIncrement', {
    key: 1
})
```


<span id="e93bc5af"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```javascript
// Example: Set a user property with the property name 'key'. Originally, there was a property value. Now the property value has been added as 'value_append’.
window.collectEvent('profileAppend', {
    key: 'value_append'
})
```


<span id="323e33ce"></span>
### 1.2.5 profileUnset

Delete the user's properties.

```javascript
// Example: delete user property, property name is key
window.collectEvent('profileUnset', 'key')
```


<span id="63c3c061"></span>
## 1.3 Anonymous ID

An anonymous user ID is used instead of webid's functionality. After enabling the setting of anonymous user ID, webid is no longer requested and reported, and the anonymous ID is replaced uniformly.

<span id="b68740ac"></span>
### 1.3.1 Enable anonymous ID

```javascript
//example
window.collectEvent('init', {
   enable_anonymousid: true
})
```


<span id="997e3166"></span>
### 1.3.2 Set anonymous ID

```JavaScript
//example
window.collectEvent('setAnonymousId', 'xxxx')
```


<span id="a02bdc4e"></span>
# 2. Obtain experimental parameters

"A/B testing" usually sends a shunt request ('/service/2/abtest_config/') to the shunt service after the SDK is initialized. After obtaining the result of the shunt service, the client side development can complete the code branch according to the result parameter of the shunt.


* Please note the preconditions of this step: the experiment and related parameters have been created according to the demand side of the experiment.


```javascript
window.collectEvent('getVar', 'ab-key', 'ab-default-value', (value) => { 
//ab-key is the key of the experimental parameter, the user develops the code branch, and the ab-default-value is the bottom line when the abnormality is abnormal. The suggestion is consistent with the control group value.
    //The following is the business code
    window.collectEvent('send business metric event')
})
```


GetVar is an asynchronous method, and the callback of getVar will only be executed after the result of the ab experiment is returned, so if you want the business custom event indicators to also bring vid, you need to call the business custom event in the callback of getVar. The complete code is as follows:

```javascript
window.collectEvent('getVar', 'abcdefg', 'default', (res)=> {
   window.collectEvent('custom event')
   // Thus, your custom event will has the corresponding ab_sdk_version while reporting
})
```


Note: In the web and Mini Program, "A/B test" will automatically report an exposure event ( **abtest_exposure** ) after calling getVar successfully. If the business does not have a custom indicator event as a statistic, you can use **abtest_exposure** as an internal process to enter the group of users related statistics.

<span id="6b1aa799"></span>
# 3. Report experimental metrics (behavioral events)

The experimental metric calculation in "A/B Testing" relies on the event log in the Finder. The example code is as follows:


* See also the Finder SDK integration documentation "Reporting event tracking logs" section:


<span id="c550e2da"></span>
## 3.1 Reporting an incident

User behavior logs are in the form of event + property params. Events typically correspond to multiple properties, or they can only have events without properties. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

```javascript
// Example: reporting event, which does not include property
// Placed in the corresponding position of business logic
window.collectEvent('event');
```


Code event tracking for reporting events and corresponding properties, as follows:

```javascript
// Example: reporting event, which includes teo properties
//      a string type property, with property name key_string, and property value value_string
//.     a int type property, with property name key_int, and property value 10
// Placed in the corresponding position of business logic
window.collectEvent('event', {
   key_string: 'value_string',
   key_int: 10
});
```


<span id="b274607c"></span>
## 3.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="d84f2752"></span>
### 3.2.1 Set public properties

```javascript
// Example: set custom public property with property name key_public and  property value value_public
window.collectEvent('config', {
   key_public: 'value_public'
});
```


<span id="fce1a8a9"></span>
## 3.3 Report event tracking before page jump

Please note that when event tracking is designed, it is not recommended to jump to the page immediately after sending the event. In this situation, the reporting request may fail, and statistics may be missing. Please consider one of the following two options:


1. Use `beconEvent`.

   `beconEvent`will send the event tracking through the browser's feature `sendbeacon`to compensate for data reporting as much as possible.


```plain
window.collectEvent('beconEvent', 'event', {})
window.location.href = 'https://xxx.com';
```


Add a delay to give `Ajax`some time.

```plain
window.collectEvent('event');
setTimeout(()=>{
    window.location.href = 'https://xxx.com'
}, 150)
```


<span id="889df105"></span>
# 4. API Description

<span id="db0188e9"></span>
## 4.1 config(paramsObj)

The config command is used to set up reporting custom fields and some configuration items.


* It needs to be called after init.

* Can be called multiple times, the new configuration will be merged with the old configuration, and the settings with the same name will be overwritten (equivalent to Object.assign)

* Parameter is an object

   * Parameter classification:

      * SDK own configuration items and debugging related fields

      * User ID related fields

      * User properties (public properties),

         * preset

         * custom

      * Event properties common to events


```plain
// 1. first call, all events sending this time include cn and Monday

window.collectEvent('config', {
    language: 'cn',
    weeks: 'Monday',
})
// 2.  second call, all events sending this time include en and Monday

window.collectEvent('config', {
    language: 'en',
})
```


The config contains preset fields such as user ID, user properties, public properties, system occupancy, and so on. The following fields are fields occupied by the SDK, each field has a specific meaning, and the priority of the field can be set higher than the default assignment of the SDK.


|Type |Field |Value type |Field description |Example |
|---|---|---|---|---|
| | | | | |
|user ID |user_unique_id |string |User unique identifier. When no user_unique_id is set, it is set to web_id. |When the business party sets \* to the following values, it will be ignored. 【'null', 'undefined', '0', '', 'None'】 |
|public property |device_model |string |Equipment model |3.3.4 start, do a simple ua parsing for mobile end. Such as: (iPhone/iPad/mi1 metal/SM\-A8000/etc.) |
|public property |os_name |string |Operating System |Sdk report by default: windows/mac/android/ios |
|public property |os_version |string |operating system version |SDK default reporting |
|public property |platform |string |platform type |Default reporting wap/web |
|public property |browser |string |Browser name |default report |
|public property |browser_version |string |Browser version |default report |
|public property |language |string |browser language |default report |
|public property |referrer |string |Forward Address |default report |
|public property |referrer_host |string |Forward Domain Name |default report |
|public property |resolution |string |resolution |default report |
|public property |screen_height |number |Screen height |default report |
|public property |screen_width |number |screen width |default report |
|public property |sdk_version |string |ByteFinder\-sdk version |default report |
|public property |timezone |int |Time Zone |default report |
|public property |region |string |region |The business party sets it up by itself |
|public property |traffic_type |string |traffic type | |
|public property |utm_source |string |promotion source |SDK default capture |
|public property |utm_campaign |string |promotional activities |SDK default capture |
|public property |utm_medium |string |promotion media |SDK default capture |
|public property |utm_content |string |promotional content |SDK default capture |
|public property |utm_term |string |promotion keywords |SDK default capture |
|system occupied |custom | | | |


<span id="a75e255c"></span>
## 4.2 Page View Events

<span id="8a964d83"></span>
### 4.2.1 SDK default call

predefine_pageview event is invoked by default, please refer to Section 3.4 for closing.

<span id="652b600a"></span>
### 4.2.2 Business call manually

Call this method to actively report a PV event with the same type of parameter as the event property of a normal event.

If a custom event property is passed in, it will be merged with the default event property; if there is a property with the same name, the default property will be overwritten.

```plain
window.collectEvent("predefinePageView")
window.collectEvent("predefinePageView", {/**...*/})
// cover default property

window.collectEvent("predefinePageView", {
    url: 'xxx',
    url_path: 'xxx'
    // ...
})
```


<span id="14e5c65d"></span>
### 4.2.3 Event preset properties


|Field |Type |Must pass |Description |Value example |
|---|---|---|---|---|
|url |string |No |Current page address | |
|url_path |string |No |Current page path, excluding protocol and host headers |/tea/app/10000/behaviorDetail |
|title |string |No |page title |Home |
|time |number |Yes |timestamp | |
|referrer |string |No |Page source, value of document.referrer | |


<span id="e5177bef"></span>
### 4.2.4 Support for SPA

Because by default, the SDK will only report a PV event after the page is loaded and initialization is completed, but the SPA page will have multiple page routes, and the SDK will only load once on the main page, so it will not initiate PV when switching pages, resulting in no PV data for subsequent pages. Therefore, the SPA parameters can be enabled, and the SDK will report the PV again when the route changes.

```plain
window.collectEvent("init", {
    spa: true
})
```


Of course, there may be some page parameters that are not up to date when the SDK listens to route changes. You can also manually report the PV when the route changes. Example of react:

```plain
// <Router history={history} onUpdate={onUpdate}>

function onUpdate() {
    window.collectEvent("predefinePageView")
}
```


<span id="97a227bc"></span>
## 4.3 Obtaining various IDs generated by the platform

Get the token information of the SDK, which contains web_id, ssid, user_unique_id information. If you need to obtain the ID information of the SDK and make other settings, you can do the following:

```plain
window.collectEvent('getToken', (token) => {
    //token data contents are like below:
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


<span id="d02b2cd3"></span>
## 4.4 Start the experiment and experiment\-related methods

<span id="167de0c9"></span>
### enable module

Using this module, when the SDK is initialized, in addition to the common parameters to be configured in the init interface, the module switch of A/B experiment needs to be turned on: `enable_ab_test: true`, and the shunt address (ab_channel_domain field) of A/B experiment needs to be configured at the same time.

```TypeScript
window.collectEvent('init', {
    enable_ab_test: true,
    ab_channel_domain: 'https://tab.volces.com',
    enable_multilink: false,//Whether to enable multi-link experiment, the default is false
    enable_ab_visual: false, //Whether to enable visual experiment, the default is false
    ab_timeout: 10000//Timeout time of shunt request, default 10000ms
    disable_ab_reset: false //Whether to prohibit re-obtaining the configuration information of A/B experiments when switching users, the default is false
    ...
});
```


<span id="1fd15830"></span>
### getVar: Get experimental parameters


* Method: getVar

* **Function:**  Get the configuration item value corresponding to the experiment in the AB test configuration, and the SDK will collect the corresponding vid (the business generally does not directly care about the vid). After hitting the experiment, it will automatically report a `abtest_exposure`event.

* **Parameter:** 

   
   |Parameter name |Type |Required |Description |
   |---|---|---|---|
   |name |string |Yes |The key in the experimental configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tip: The business calls the getVar method, and the SDK will report a preset event <code>abtest_exposure</code>when it finds that there is a corresponding key in the experimental configuration.</div><br> |
   |defaultValue |any |Yes |When there is no corresponding key configuration item in the experimental configuration, the method will return the bottom value. |
   |callback |(value: any) =\> void |No |When the experimental configuration item value is obtained, if there is a callback setting, the callback will be executed, and the experimental configuration item value will be used as the callback parameter. |
   

* **Example:** 

   ```TypeScript

   ```Plain Text
   window.collectEvent('getVar',' color', 'red', (value) => {
       //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
   });
   ```
   ```
   


<span id="7ad32bf5"></span>
### getAllVars: Get all the configuration information for the experiment


* Method: getAbSdkVersion

* **Function:**  Get the exposed experiment, the returned result is the vid of all exposed experiments, connected with commas, format for example: 123,234,678

* **Return value:** 

   
   |Type |Description |
   |---|---|
   |string |VIDs of all exposure experiments, linked with commas, in the format for example: 123,234,678 |
   

* **Example:** 

   ```TypeScript
   //vids value is similar to 123,234,678
   const vids = window.collectEvent('getAbSdkVersion');
   ```
   


<span id="7b30c733"></span>
### getAbSdkVersion: Get the Experimental Version ID

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">AB test must call the API to obtain experimental parameters (see the <strong>++Getting Experimental Parameters ++</strong>section for details). You can use this API to obtain the Version IDs (vids) of all user exposures or hit experiments, which do not report abtest_exposure exposures.</div>


```JSON
window.collectEvent('getAbSdkVersion', function(vids) {
    // vids
});
```


<span id="65aaff4c"></span>
### setExternalAbVersion: Manually set up additional AB test configurations


* Method: setExternalAbVersion

* **Role:**  Manually set up additional AB test configurations.

* **Parameter:** 

   
   |Parameter name |Type |Required |Description |
   |---|---|---|---|
   |vids |String or null |Yes |Format requirements for vids: Use commas to concatenate vids values, something like '123,234,678'.<br><br><br>* Additional experimental configuration vids set up in this way are merged into the vids obtained through getVar processing.<br><br>* When called multiple times, the last set of additional experimental configuration vids overrides the previous ones.<br><br>* When null is set, the SDK clears the set of additional experimental configuration vids without affecting the vids obtained through getVar processing. |
   

* **Example:** 

   * Set up additional experimental configurations

      ```TypeScript
      //Manually set additional
      window.collectEvent('setExternalAbVersion', '25,225,2225');
      ```
      


<span id="8e8e15e7"></span>
## 4.5 Custom webid

To change the default webid of the SDK, please set `enableCustomWebid: true`when the SDK is initialized, and then set it through setWebIDviaUnionID or setWebIDviaOpenID. The example is as follows:

```javascript
window.collectEvent('init', {
    enableCustomWebid: true
});
window.collectEvent('setWebIDviaUnionID', 'ssss')
window.collectEvent('setWebIDviaOpenID', 'ssss')
```


It should be noted that when enableCustomWebid is set, you must call setWebIDviaUnionID or setWebIDviaOpenID to set webid before the SDK will continue to execute the subsequent process.

This scenario is suitable for the H5 page to open in the WeChat Mini Program, and you need to pass WeChat's unionID or openID to the H5 page.

<span id="4bbcd82f"></span>
### 4.6 Open the mask layer

Open a global mask layer on the page (equivalent to a white screen), when you need to modify the UI of the page with AB test, to prevent the user from seeing obvious UI changes, you can use it. Note that when you manually open the mask layer, be sure to close it manually.

Open mask layer

```bash
window.collectEvent('openOverlayer')
```


Close mask layer

```bash
window.collectEvent('closeOverlayer')
```
