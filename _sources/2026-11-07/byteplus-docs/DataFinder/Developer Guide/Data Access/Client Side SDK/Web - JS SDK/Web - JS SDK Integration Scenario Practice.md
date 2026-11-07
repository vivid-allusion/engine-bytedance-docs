---
title: "Web/JS SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice"
---

<span id="45e2739a"></span>
# user_unique_id related

<span id="e003d216"></span>
## user login settings

For example, the business has an account system and wants the SDK to synchronize user status. You can consider setting user_unique_id to the SDK immediately after the user logs in, and clearing the user_unique_id to the SDK immediately after the user logs out.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: The concept of user login status is a statement from a business perspective. The SDK itself does not have the concept of user login/login. The SDK only cares about whether the user_unique_id has been actively set.</div>


```TypeScript
//If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the criteria before and after the user logs in.
window.collectEvent('config', {
    user_unique_id: "zhangsan"  
});

//If you want the user to log out when replying to the anonymous state, call when logging out
window.collectEvent('config', {
    user_unique_id: null  
});
```


The SDK also provides a separate `setUserUniqueID`method to set user_unique_id.

```TypeScript
//Set user_unique_id immediately after user login
window.collectEvent('setUserUniqueID'， 'zhangsan'); //Values can be considered as attributes that can be associated with the user

//Clear user_unique_id immediately after user logs out
window.collectEvent('setUserUniqueID'， null); //Values can be considered as attributes that can be associated with the user
```


<span id="ae1a37e8"></span>
## User criteria related processing

If you want to set the user aperture, you need to set the user_unique_id_type at the same time as setting the user_unique_id.

```TypeScript
window.collectEvent('config', {
    user_unique_id: 'zhanshan',
    user_unique_id_type: 'huoshan', //user_unique_id_type values are prefabricated
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: user_unique_id_type values are pre\-made, ask your project manager or customer success manager.</div>


<span id="7122642d"></span>
## Multi\-user aperture type processing

If you want to perform multi\-aperture binding, you need to call the bind method after setting the user_unique_id_type while setting the user_unique_id. Note: The SDK version requires 5.2.0 + and is only supported in the SAAS Cloud Native, Private.

```TypeScript
  //type definition, bind parameter, callback, number of retries
  window.collectEvent(params: Record<string, any>, callback: Function, retry?: boolean) {
```


```TypeScript
window.collectEvent('bindToken',{
    phone: '130xxxxxxxx',
    email: 'xxx@yyy.com'
}, (status) => {
  //The business performs subsequent processing according to the status, optional processing
}, 3);
```


<span id="317fefda"></span>
# APP gets through to H5 to report

If the H5 page is embedded in the client side, you want to report the generated event and attribute data to the client side application uniformly (that is, the data of the H5 page is not reported to the Web application separately through the Web SDK), and reuse the `user_unique_id`set by the client side (to achieve user data access) and public attributes. At this time, you need to integrate the APP\-side SDK and the Web\-side SDK in the client side application and the H5 page respectively, and turn on the H5 page at the same time. Open switch.

The following is an example of turning on the H5 switch in the Web SDK. The H5 switch settings of the client can be found in the corresponding SDK documentation.

```TypeScript
//H5 is embedded in the native terminal and connected
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_native: true 
    //5.1.3 the following version parameter is named Native,
    //5.1.3 the above version is named enable_native, but it is still compatible with Native settings
})
```


If the client side initializes with multiple instances, it may cause the connection to fail. There are two ways to adjust:


1. The client side calls the reporting method and uses the default instance initialization instead of multiple instances.

2. The H5 page manually binds the appids of the following multiple instances. After the init method, the following code is called before the start method.


```TypeScript
window.collectEvent('setNativeAppId', appid)
```



3. Get did/ssid information  **(5.2.10 start support)** 


```HTML
window.collectEvent('getDeviceId', (did) => {
  ....
})
window.collectEvent('getStandardizedServiceId', (ssid) => {
  ....
})
```


<span id="f5056294"></span>
# multi\-instance correlation

Multi\-instance reporting is used to report to multiple applications (multiple appids) on one page, and only one SDK needs to be introduced.

<span id="47105926"></span>
## function settings

```TypeScript
//Example 1, report to appid = {{APPID_1}}

window.collectEvent('init', {
    app_id: {{APPID_1}},
    //..... other initialization configurations
});
window.collectEvent('start');

//Example 2, report to appid = {{APPID_2}}
//Here "finder" can be given any name, as long as the same instance is consistent. It is forbidden to use default, the SDK is occupied.
window.collectEvent('finder.init', {  
    app_id: {{APPID_2}},
    //..... other initialization configurations
});
//Here "finder" can be given any name, as long as the same instance is consistent. It is forbidden to use default, the SDK is occupied.
window.collectEvent('finder.start');
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Currently, only SaaS\-cloud native environment supports multi\-instance, please refer to the multi\-instance usage process <a href="https://docs.byteplus.com/docs/DataFinder/Use_Multiple_Apps">Use Multiple Apps</a>.</div>


* <div data-tips="true" data-tips-type="warning">In the scenario of reporting multi\-instance data on the web side, starting from reporting the data of the second instance, you need to add the prefix of the application name in front of the subsequent calls to the API of the web side and the configuration of event tracking event reporting. Therefore, in the multi\-instance scenario, you can obtain the application name synchronously while obtaining the APPID, which is convenient for configuration during access.</div>


   <div data-tips="true" data-tips-type="warning">Taking the above reporting example as an example, when reporting the data of Example 2, calling the init, start and other APIs needs to be configured as <code>window.collectEvent ('finder.start')</code>, <code>window.collectEvent ('finder.init',...)</code>, where <code>finder</code>is the application name of the reported data for the example.   </div>
   


<span id="4e1336c7"></span>
# Event (including presets), event properties, and event public properties are related

<span id="7f651408"></span>
## Filter event

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


<span id="c3edba60"></span>
## Set event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events. When the page jumps, you need to reload the SDK and reset the required public properties (except for single\-page applications).

```JavaScript
//Example: Set a custom public property with the property name key_public and the property value value_public
window.collectEvent('config', {
   key_public: 'value_public'
});
```


<span id="69818e05"></span>
## page jump report

Please note that when event tracking is designed, it is not recommended to jump to the page immediately after sending the event. In this situation, the reporting request may fail and statistics may be missing. Please consider one of the following two options:

<span id="2013ffa0"></span>
### **beaconEvent**

BeaconEvent will send the event tracking through the browser's feature `sendbeacon`, allowing the page to be closed and still send a small amount of data to the server level, but the data size is limited, usually no more than 64000 bytes.

```javascript
window.collectEvent('beconEvent', 'event', {})
window.location.href = 'https://xxx.com';
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you directly kill the browser or APP, this method will also fail, so try to avoid reporting event tracking in this scenario.</div>


<span id="613038af"></span>
### delayed delivery

Give the event tracking request some time, generally less than 300ms.

```TypeScript
window.collectEvent('test_event');
setTimeout(()=>{
    window.location.href = 'https://xxx.com'
}, 150)
```


<span id="abcf2025"></span>
# SPA Single Page Application

Under normal circumstances, the SPA project only sends a PV once after the SDK is initialized. After opening the SPA, the PV of the new page will be automatically reported when switching the route (if the full event tracking function is turned on, the PV will also be automatically reported when switching the route).

```javascript
window.collectEvent('init', {
  spa: true, //Whether it is a single-page application
  allow_hash: true //V5.1.3 starts to support whether to collect hash routes, the default is false, if it is not a hash route, this parameter is not required
})
```


&nbsp;
