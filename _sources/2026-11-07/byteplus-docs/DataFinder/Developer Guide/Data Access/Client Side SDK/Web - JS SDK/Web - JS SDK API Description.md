---
title: "Web/JS SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JS_SDK_API_Description"
---

This article introduces the main APIs provided by the web for you. You can call the corresponding API for event tracking in combination with event tracking planning.

<span id="57d12e95"></span>
# init


* **Function:**  It is to initialize and configure the SDK instance.

* **Definition:**  init (options: InitParams): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |options |```TypeScript```<br>```interface InitParams {```<br>```  app_id: number;```<br>```  log?: boolean;```<br>```  channel?: 'cn' or 'sg';```<br>```  channel_domain?: string;```<br>```  enable_ab_test?: boolean;```<br>```  // ...```<br>```}```<br> |Yes |The SDK needs to know which application to report to, which DataFinder service address to report to, and which function modules to enable. These need to be configured in the init interface when the SDK is initialized. The parameters and configuration instructions involved in init are shown in the following table. |
   

   
   |Parameter classification |**Field** |**Field value type** |**Required** |**Field description** |
   |---|---|---|---|---|
   |**basic parameters** |app_id |number |Yes |The application ID is used to identify the business product, that is, to indicate which application's data is collected by the event tracking.<br><br><br>* It can usually be configured to automatically generate the app ID for the corresponding app for you after creating an app in the DataFinder console.<br><br>* SaaS\-cloud native environments can also be configured as APP URLs to encrypt APP IDs. |
   ||log |boolean |No |It is used to set whether the log needs to be turned on. When set to true, the console will print debugging information, so that you can verify whether the SDK integration is successful through the log information of the console when integrating the SDK. |
   ||channel |string |No |It is used to set the reporting channel for collecting data. Each application can only set a unique channel. Please set the appropriate channel according to the environment type and geographical situation of the DataFinder service you are currently using:<br><br><br>* **Sg:**  If your current environment is an overseas BytePlus environment, you need to modify the channel value to sg.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   ||channel_domain |string |No |To set which service address to report data to the DataFinder:<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying a private environment. If you do not know this address, please contact your project manager or customer success manager.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">channel_domain after the configuration is complete, you will also need to configure the above address in the Mini Program whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   |**PV event switch** |disable_auto_pv |boolean |No |Sets whether to turn off capture preset PV events \- predefine_pageview events. |
   |**Full event tracking event switch** |autotrack |Boolean or object |No |Set whether to enable the element's auto\-capture ability Click/Exposure ability, see below for details [Full event tracking module](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#467cf272). |
   |**dwell time switch** |enable_stay_duration |boolean |No |Set whether to enable the dwell time capability at the statistics page level, see below for details [Duration of Stay Module and API](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#70894e77). |
   |**Turn on the H5 switch** |enable_native |boolean |No |Set whether to embed H5 and APP for data connection.<br><br>If your page is embedded in an APP in the H5 method, you can integrate the Web\-side SDK and APP\-side SDK separately, and turn on the embedded H5 switch at the same time to achieve unified data reporting to the APP and connect user data. More access practices for H5 scenarios can be found [APP gets through to H5 to report](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#317fefda). |
   |**AB experimental event switch** |enable_ab_test |boolean |No |Set whether you need to enable the A/B experiment function. After setting it to true, the ab experiment function will be enabled. Later, you need to:<br><br><br>* Configure the offload address (ab_channel_domain) of the A/B experiment at the same time during the integration SDK initialization, see the AB module below for details<br><br>* Use APIs including getVar, getAllVars, etc. to obtain experimental parameters, etc. A/B experiment related API details please see [AB test Modules and APIs](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#e15ecfb8). |
   ||ab_channel_domain |string |No |If the A/B experiment is enabled, you need to set the offload address for the A/B experiment.<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address that you plan and configure when deploying the private environment, and add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you are unsure of this address, please contact your project manager or customer success manager. |
   |**anonymous ID** |enable_anonymousid |boolean |No |Whether to enable anonymous ID reporting. Details can be found below [Enable anonymous ID](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#60132fff). |
   |**Custom webid** |enable_custom_webid |boolean |No |Whether to set a custom web_id. If you do not want to use the SDK automatically generated web_id, you want to report custom web_id, you need to open the enable_custom_webid during initialization, and then set the web_id through the config interface, only after setting the web_id will be initialized, web_id value requirements must be a number or a string type full of numbers. Please see for details [Custom webid](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#494e18ff). |
   |**second level domain name** |cross_subdomain |boolean |No |Whether to automatically identify users across subdomains, when set to true, anonymous users using the same browser in multiple subdomains will be automatically recognized as the same user, such as a.yourdomain.com and b.yourdomain.com . |
   ||cookie_domain |string |No |After opening the above configuration, you can configure the cookie domain name that stores tokens or utm parameters. If you need ' a.bytedance.com ' and ' b.bytedance.com ' to collude, pass'. bytedance.com ', if you don't pass it, it will be stored under the current domain name by default |
   ||cookie_expire |number |No |Cookie expiration time, in ms, default 7 days |
   |**single page app** |spa |boolean |No |Sets whether to apply as a single page. |
   ||allow_hash |boolean |No |Sets whether a single\-page app is a hash route. |
   |**encryption**<br><br> **(Privatization support)**  |enable_encryption |boolean |No |Whether to enable data encryption reporting, 5.1.5 the above version of the SDK support, please refer to the following for details [Encryption reporting module](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#71f1de77). |
   ||crypto_publicKey |string |No |Data encryption reported public key, 5.1.5 the above version of the SDK support, please refer to the following [Encryption reporting module](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#71f1de77). |
   ||encryption_type |string |No |The type of data encryption report 5.1.5 supported by the above version of the SDK, please refer to the following for details [Encryption reporting module](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#71f1de77). |
   ||encryption_header |string |No |Data encryption report header, 5.1.5 the above version of the SDK support, please refer to the following [Encryption reporting module](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#71f1de77). |
   |**Report general settings** |max_report |number |No |The maximum number of custom event tracking merge reports, the default is 20. |
   ||timeout |number |No |Event tracking report timeout time, unit ms, default 100000ms |
   ||disable_track_event |boolean |No |Whether to disable all event tracking reports. If you want to temporarily avoid reporting data, it is recommended to use the "stop" interface.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The report cannot be restored after setting the disable_track_event, please operate with caution.</div><br> |
   |**event reissue** |enable_storage |boolean |No |Whether to enable the failure storage? After opening, the failed event tracking will be stored locally, and then try to reissue it.<br><br>5.2.0 version starts to support this configuration parameter, but it is turned off by default until 5.2.6 version starts to turn this feature on by default. |
   ||enable_degrade |boolean |No |Whether to enable the degradation strategy of failed storage. After opening, the failed reissue adopts a backoff strategy to reduce traffic loss.<br><br>5.2.6 and above support. |
   |**Configure delivery** |enable_logsetting |boolean |No |Whether to enable cloud control configuration delivery can control the ability to report events to black and white lists.<br><br>5.1.8 above support. |
   |**SDK monitoring** |enable_observe |boolean |No |Whether to enable the SDK itself to monitor the data collection, used to check the stability of the SDK, 5.2.7 version or above. |
   |**DevTools** |track_enabled |boolean |No |Whether to enable the event tracking collection of devtools itself, the default collection before the 5.2.8 version. |
   |**other** |enable_invalid_config |boolean |No |Whether to allow public parameters to set invalid values, such as null, undefined, etc. 5.2.11 version support. |
   

* **Example:** 

   ```TypeScript
   window.collectEvent('init', {
       app_id: {{APPID}}, Note that the type is a number, not a string.
       channel: 'cn', //For details, please refer to the above preparatory step 3: Obtain the reporting address
       channel_domain: 'https://gator.uba.ap-southeast-1.bytepluses.com', ////For details, please refer to the above preparatory step 3: Obtain the reporting address
       log: true, //true: enable local debug log printing, false: turn off local debug log printing
       ...
   });
   ```
   


<span id="f2a82275"></span>
# start


* **Function:**  After the init initialization call, the start method needs to be called before the SDK starts reporting events. No events are reported until the start method is called.

* **Definition:**  start (): void

* **Example:** 

   ```TypeScript
   window.collectEvent('start');
   ```
   


<span id="ebe0f1cc"></span>
# config


* **Function:**  Call config to make some settings for the event, such as setting public properties, setting user_unique_id, etc. It can be called multiple times, and subsequent settings will override the same previous settings.

* **Definition:**  config (configs?: ConfigParams): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |configs |```TypeScript```<br>```interface ConfigParams {```<br>```  user_unique_id?: string or null;```<br>```  [key: string]: any;```<br>```}```<br> |No |The config contains preset fields such as user ID, user attributes, public attributes, system occupancy, and so on. You can set custom event public properties or user ID dependencies in the config interface.<br><br><br>* Set custom event public properties: The custom event public properties are similar to the preset event public properties and will be in the header as a common property for all events, see details [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#c3edba60).<br><br>* Setting user_unique_id: If there is real\-name ID data in the business system, it can be reported to the user_unique_id field, please refer to [user_unique_id related](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#45e2739a). |
   

* **Example:** 

   ```TypeScript
   
   //Set event public properties, which will be carried on all subsequent event reports
   window.collectEvent('config', {
       city: '南京', //Nanjing
       nick_name: 'vikings',
   });
   
   //Set user_unique_id
   window.collectEvent('config', {
       user_unique_id: 'zhangsan'
   });
   
   //Set user_unique_id again, it will overwrite
   window.collectEvent('config', {
       user_unique_id: 'lisi'
   });
   ```
   


<span id="148a4046"></span>
# Event tracking


* **Definition:**  Event tracking can be reported by event\-params through the CollectEvent method.


<span id="727dbba3"></span>
## single report


* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |event |string |Yes |* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDK internal automatic reporting of event names.<br><br>* It is recommended that event names use lower case uniformly. |
   |params |Record < string, string or number or boolean or object or Array \> |Yes |* It is recommended that attributes use lowercase uniformly.<br><br>* Event property values support number, string, array, object, boolean types. When the data collection is dropped into the DataFinder, the data format will be converted. See more instructions [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).<br><br>* Do not re\-nest objects in event attributes, that is, the attribute value does not accept the object type. If the business data is a nested object type, it can be converted to a String by escaping and then reported. Please see [Example 1: How nested JSON type attributes are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2).<br><br>* If there are no properties, you can leave the params parameter unpassed. |
   

* **Example:** 

   ```TypeScript
   window.collectEvent('event_name', {
       event_key: 'value'
   });
   ```
   


<span id="cd20e36d"></span>
## batch report


* **Logical description:**  Accept an array to report batch events. When the number of array items is greater than 50, the SDK will automatically report multiple times, that is, a single batch can report up to 50 events.

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |events |```TypeScript```<br>```Array<{```<br>```    event: string;```<br>```    params: Record<string, string or number or boolean or object or Array>;```<br>```    local_time_ms?: number;```<br>```}>```<br> |Yes |* The requirements for events and params are the same as those for reporting a single event.<br><br>* local_time_ms value is timestamp, and the default SDK will supplement this field for each event. If you actively set this field, the value you set will prevail. |
   

* **Example:** 

   ```TypeScript
   window.collectEvent([['test1', {name:22}], ['test2', {name:3}]])
   ```
   


<span id="19ad8356"></span>
## Typical error examples (please do not refer to)

```JavaScript
//exception writing
const windowTea = window.collectEvent
windowTea('init')
windowTea('start')
windowTea('test')

This writing method may result in the inability to report events when using async to asynchronous loading of SDK files, due to the following reasons:
The SDK has a pre code:
(function(win, export_obj) {
        win['LogAnalyticsObject'] = export_obj;
        if (!win[export_obj]) {
            function _collect() {
                _collect.q.push(arguments);
            }
            _collect.q = _collect.q or [];
            win[export_obj] = _collect;            
        }
        win[export_obj].l = +new Date();
    })(window, 'collectEvent');
The purpose of this pre code is to ensure that the business execution window.collectEvent does not report an error when the SDK file is not loaded
And save the API for business calls. After the SDK file is loaded, the SDK will reassign window.collectEvent to the actual method
Then proceed to execute the saved API queue in sequence.
Assigning window.cellectEvent to windowTea before the SDK is fully loaded will result in the value of calling windowTea always being the same as this preceding code, making it impossible to truly report the event.
```


<span id="78be439d"></span>
# stop


* **Function:**  Suspend SDK reporting events. After calling this method, the SDK will be suspended and no events will be reported in the future.

* **Example:** 

   ```TypeScript
   window.collectEvent('stop');
   ```
   


<span id="f89c147f"></span>
# reStart


* **Function:**  Restore SDK reporting, generally after calling disableSDK and intend to cancel the suspension, that is, restart SDK reporting, and the reporting event will be resumed later.

* **Example:** 

   ```TypeScript
   window.collectEvent('reStart');
   ```
   


<span id="2726e5e7"></span>
# Page View Events (predefine_pageview)

<span id="84872b46"></span>
## event acquisition switch

predefine_pageview event is called by default, to close:

```TypeScript
window.collectEvent('init', {
   disable_auto_pv: true
});
```


<span id="da957d52"></span>
## manual reporting

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


<span id="f18e5bf5"></span>
## event preset properties


|Field |Type |Required to pass |Explain |
|---|---|---|---|
|url |string |No |Current page address |
|url_path |string |No |Current page path, without protocol and host headers, for example: `/tea/app/10000/behaviorDetail` |
|title |string |No |page title |
|time |number |Yes |timestamp |
|referrer |string |No |Page source, value of document.referrer |


<span id="f928d96d"></span>
## Support for SPA

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


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the spa switch is turned on in the web sdk, the predefine_pageview cannot be triggered in the scenario of h5 opening the app. You can report the pv through the following steps.</div>



1. <div data-tips="true" data-tips-type="warning">Configure disable_auto_pv disable predefine_pageview default calls.</div>


2. <div data-tips="true" data-tips-type="warning">In the routing hook, the predefinePageView method is actively called to report the pv.</div>



<span id="70894e77"></span>
# Duration of Stay Module and API

The time spent on a page (browsing) is a very common indicator in website analysis, used to reflect the length of time users spend browsing certain pages, reflecting the stickiness of users to a website.

<span id="00bb9fe9"></span>
## Function on

If you want to collect data related to the dwell time of the report page, you need to turn on the dwell time function switch when the web SDK is initialized.

```TypeScript

window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_stay_duration: true //true: turn on stay duration
});
```


<span id="40902a1e"></span>
## Report the incident introduction

After turning on the stay time function switch, the relevant duration data will be automatically collected when the page is active or the page is inactive.


* Page active state: The page is in a visual or actionable state.

* Page inactivity: The page is in the background, hidden, minimized, and other invisible states.


<span id="b48faf72"></span>
### predefine_page_alive

When the Dwell function is turned on, predefine_page_alive events will be reported regularly every minute when the page is active, or once when switching to an inactive state. The event property fields reported with the event are as follows:


|Parameter |Data type |Explain |
|---|---|---|
|title |string |Page title |
|url |string |page address |
|url_path |string |page path |
|duration |number |The normal value is 60000, but it is less than or equal to 60000 when switching states, in milliseconds (ms). |


<span id="8e0e46e4"></span>
### auto reset duration

When the route changes, the SDK automatically ends the duration statistics of the current page and reports the alive and close events, and starts the duration statistics of the next page at the same time.

```TypeScript
window.collectEvent('init', {
   spa: true
});
```


If you feel that the parameters obtained by alive or close event tracking when the dwell duration is automatically reset are inaccurate, or you want to control this behavior yourself, you can turn off automatic route monitoring through the settings below.

```javascript
window.collectEvent('init', {
   disable_route_report: true
});
```


Or fix the parameter issue by calling the following API every time you enter a new page.

```TypeScript
//pass in the parameters of the page to be accessed
window.collectEvent('resetStayParams', url_path?: string, title?: string, url?: string);
```


<span id="507818be"></span>
## Analysis method

Select `predefine_page_alive`event on DataFinder ( `page active`event)


* Average screen time: Select `the average length of stay (SUM/UV)`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364e6bdaff2b4d77b2bca93a40474aba~tplv-goo7wpa0wc-image.image) </span>

* Average use time: select `Average by stay time (SUM/PV)`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80a88750155549de8bde6560f97e0bc9~tplv-goo7wpa0wc-image.image) </span>


<span id="08c41e73"></span>
## Validation event tracking

Due to the fact that in most cases, it will be triggered when the page leaves or closes, so the SDK uses the sendBeacon api to send this request. This request needs to be viewed in the network category of the browser console by selecting the ALL category (type ping, xhr for abnormal requests).

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ec9099a90bc5d25381ae4c74c3218326) </span>

<span id="c52de3ad"></span>
# User modules and APIs

This module provides the ability to set user properties, anonymous ID, user type, etc., and provides a series of methods: `setAnonymousId`, `getToken`, `profileSet`, `profileSetOnce`, `profileUnset`, `profileIncrement`, `profileAppend`, `bindToken`, `setWebIDviaUnionID`, `setWebIDviaOpenID`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This module is used to set the user attribute data to be collected. If you want to set the user's real\-name identity user_unique_id, you can use the config parameter to set it. For details, please refer to the interface description document above: <a href="https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_API_Description#ebe0f1cc">config</a>; Scenario practice document: <a href="https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#45e2739a">user_unique_id related</a>.</div>


<span id="5e3f766d"></span>
## Set user properties

<span id="6ada61cc"></span>
### profileSet


* **Function:**  Report user attributes, overwrite attribute fields with new values, set one or more attributes at a time, support array type attribute values.

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. Overwrite property fields with new values, one or more properties can be set at a time, and array type property values are supported. |
   

* **Example:** 

   ```TypeScript
   window.collectEvent('profileSet', {
       key: 'value' //value support string, number, array
   })
   ```
   


<span id="bb992fbc"></span>
### profileSetOnce


* **Function:**  Report the user attribute, according to the attribute field, only set once, if there is already a value, it will not be updated.

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. According to the property field, it is set only once. If it already has a value, it will not be updated. |
   

* **Example:** 

   ```TypeScript
   //Example: Set a user property with the property name key_once and the property value value_once
   window.collectEvent('profileSetOnce', {
       key_once: 'value_once' //value support string, number, array
   })
   ```
   


<span id="a82117dd"></span>
### profileUnset


* **Function:**  Delete the value of a property.

* **Parameters:** 

   
   |Parameter name |Type |Required |explain |
   |---|---|---|---|
   |key |string |Yes |Deleted user property value. |
   

* **Example:** 

   ```TypeScript
   window.collectEvent('profileUnset', 'key')
   ```
   


<span id="8a0323d1"></span>
### profileIncrement


* **Function:**  Increases the numeric property by the specified value, which can be a negative number.

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record<string, number\> |Yes |Increased user property value. Increments a numeric property by the specified value, which can be negative. |
   

* **Example:** 

   ```TypeScript
   //Example: Set the user property, the property name is key, and the property value is 1
   window.collectEvent('profileIncrement', {
       key: 1
   })
   ```
   


<span id="8b7fe0f7"></span>
### profileAppend


* **Function:**  When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array.

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array. |
   

* **Example:** 

   ```TypeScript
   //Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
   window.collectEvent('profileAppend', {
       key: 'value_append'
   })
   ```
   


<span id="eb4d476b"></span>
## Get user ID: getToken

Obtain the token information of the SDK, which contains web_id, ssid, user_unique_id information. If you need to obtain the ID information of the SDK and make other settings, you can do the following:

```TypeScript
window.collectEvent('getToken', (token) => {
    The token data content is similar to the following:
    {
        "web_id":"6748002161499735560",
        "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
        "user_unique_id":"xxx",
    }
  });
```


<span id="e3ad1a7f"></span>
## Custom anonymous ID

If you have anonymous user ID data in your business system and want to report this data to DataFinder as an anonymous user ID, rather than using the web ID automatically generated by DataFinder to identify the anonymous user, then you can enable the anonymous user ID function. After enabling the function of anonymous user ID, the web ID will no longer be requested and reported in the future, and will be replaced by the anonymous ID you reported.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Anonymous IDs have no environmental restrictions on the web SDK switch settings, but when used on the final DataFinder, the following restrictions apply:</div>



* <div data-tips="true" data-tips-type="warning">SaaS\-cloud native environments support this feature.</div>


* <div data-tips="true" data-tips-type="warning">In a privatized environment, if the unified ID service has been turned on, it can be used directly; if not, you need to contact the technical support staff for configuration, and it can be used after completion.</div>



<span id="60132fff"></span>
### Enable anonymous ID

```TypeScript
window.collectEvent('init', {
   enable_anonymousid: true
})
```


<span id="840e7f8e"></span>
### ID setAnonymousId

```TypeScript
window.collectEvent('setAnonymousId', 'xxxx')
```


<span id="494e18ff"></span>
## Custom webid

To change the default web id of the SDK, please set `enable_custom_webid: true`when initializing the SDK, and then set the custom web id through setWebIDviaUnionID or setWebIDviaOpenID.

```TypeScript
window.collectEvent('init', {
    enable_custom_webid: true
});
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When enableCustomWebid is enabled, you must call setWebIDviaUnionID or setWebIDviaOpenID to set webid before the SDK will continue to execute the subsequent process.</div>


* <div data-tips="true" data-tips-type="warning">This scenario is suitable for the H5 page to open in the WeChat Mini Program, and you need to pass WeChat's unionID or openID to the H5 page.</div>



<span id="23eda759"></span>
### setWebIDviaUnionID

```TypeScript
window.collectEvent('setWebIDviaUnionID', 'ssss')
```


<span id="4a97dbfd"></span>
### setWebIDviaOpenID

```TypeScript
window.collectEvent('setWebIDviaOpenID', 'ssss')
```


<span id="0b993992"></span>
## bindToken

If you have multiple calibers identified by real\-name IDs, you can use the multi\-ID caliber function to report the user real\-name IDs of multiple calibers to DataFinder, and then call the bindToken interface to bind multiple real\-name IDs, and finally MAPPING the same user to the same user unique identifier ssid.

The example of using bindToken is as follows, please refer to the complete multi\-ID aperture access practice [Multi-user aperture type processing](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Integration_Scenario_Practice#7122642d).

```TypeScript
window.collectEvent('bindToken', {
   key: value,
   key2: value2
}, (result) => {
  //bind the returned value
})
```


<span id="467cf272"></span>
# Full event tracking module

In comparison to custom event tracking, full event tracking can automatically monitor user visits, clicks, and other behaviors, and then automatically report relevant event tracking.

<span id="baa8d457"></span>
## enable module

```TypeScript
window.collectEvent('init', {
    // ...... Other initialization configurations
    autotrack: true
});
```


<span id="16ef063b"></span>
## Configuration parameter description


|Autotrack built\-in object |Data type |Explain |
|---|---|---|
|text |Boolean |Whether to collect the text of the element, the default collection |
|svg |Boolean |Whether to collect svg elements, not by default |
|track_attr |[String], string array |Configure click element custom properties |
|collect_url |Function, function |Configure whether to collect a certain page, return the element click event that will really collect the current page, and return false to indicate that the current page is not collected. After setting this function, if the content is empty, it will return false. If the function is not set, the default is to collect all pages. |
|pv |Boolean |Whether to enable pv event (bav2b_page, bav2b_page_statistics) reporting of full event tracking, the default is true, false is disabled. |
|click |Boolean |Whether to enable click event (bav2b_click) reporting for full event tracking, the default is true, false is disabled |
|beat |int |Configure the time interval for heartbeat event reporting in milliseconds (ms). |
|exposure |Boolean |Exposure event (bav2b_exposure) acquisition, the default false, pass true to open the exposure event collection, please see the detailed description below. |


```TypeScript
window.collectEvent('init', {
    autotrack: {
      text: false, //do not collect element text
      svg: true, //capture svg elements
      track_attr: ['attr1', 'attr2'],
      collect_url: () => {
        if (location.href === 'xxx') {
           //If the page address is xxx, it will not be collected.
           return false
        }
        //Other page collection
        return true
      },
      exposure: {
         ratio: 0.5, //Element exposure area ratio 0-1, default 0.5, exposure after element area display exceeds 50%
         stay: 3000, //element exposure waiting time, unit ms, default does not wait, direct exposure
      }
    }
})
```


<span id="5de28afa"></span>
## Report custom properties

<span id="418f2b5b"></span>
### way one

After turning on full event tracking, support the collection of custom attributes. The code is as follows:

```javascript
window.collectEvent('init', {
    autotrack: {
       track_attr: ['attr1', 'attr2']
    }
})
```


```HTML
// SDK will collect the properties and property values of att1 and attr2
<div attr1='ss'  attr2='ddd'></div>
```


<span id="f5564d84"></span>
### Mode two

```TypeScript
window.collectEvent('init', {
   autotrack: {
     custom_attr: 'datastring' //The value can be any string, as long as it corresponds to the element
   }
})
```


```TypeScript
<div id="test" datastring="%7B%22id%22%3A2%2C%22name%22%3A3%7D">test property collection</div>
```


```TypeScript
The raw value of datastring is
{
  id:2,
  name:3
}

fill the dom needed collecting through encodeURIComponent(JSON.stringify({id:2, name:3}))
```


<span id="c713aacd"></span>
## Set the capture parent attribute

In some front\-end frameworks, certain components that are used can be used if attributes that need to be collected are added to the component, and when a child element tag is newly generated within the component after final compilation. **5.2.10 version is supported**

```HTML
window.collectEvent('init', {
  autotrack: {
    track_attr: ['test'],
    track_parents: true, // Whether to search for the properties of the parent element
    track_parents_level: 2 // The maximum number of layers to find the parent element, which means finding up to 2 layers, defaults to 1 layer, and the maximum of 3 layers  }
 }
```


<span id="6846fce7"></span>
## Set capture page range

After turning on full event tracking, support setting which pages need to be collected and which pages do not need to be collected

```javascript
window.collectEvent('init', {
    autotrack: {
      collect_url: () => {
        if (location.href === 'xxx') {
           //If the page address is xxx, it will not be collected.
           return false
        }
        //Other page collection
        return true
      }
    }
})
```


<span id="5a7bfcb7"></span>
## Set up element acquisition

If an element itself cannot be captured, you can set attributes for the SDK to capture

```HTML
<div data-tea-container="true"></div>
```


<span id="62fa3535"></span>
## Set element not to collect

If an element does not need to be collected, you can set attributes for the SDK to filter the element

```HTML
<div data-tea-ignore="true"></div>
```


<span id="5a6893f2"></span>
## exposure event

<span id="441ef945"></span>
### Enable exposure event tracking

```JavaScript
window.collectEvent('init', {
    autotrack: {
      exposure: true //You can directly pass true and go to the default settings.
      exposure: {
        radio: 0.5 //Element exposure ratio, 0-1, default 0.5, that is, exposure when the element display area exceeds 50%
        stay: 3000, //element exposure waiting time, unit ms, default does not wait, direct exposure
        eventName: 'exposure'， //You can customize the reported exposure event name, the default is bav2b_exposure
        //Only one of the above two conditions can be set. If both are set, it needs to be met at the same time before reporting.
        callback: (data) => {
         //You can modify the data, data is the attribute of the exposure report, and you can also add
          data.element_class_name = 'sijie'
          return data
        }
      }
    }
})
```


<span id="f0fd0351"></span>
### Set Exposure Element

```HTML
// element to be exposed
<div data-exposure>I am element to be exposed</div>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An element is exposed only if it contains the data\-exposure attribute.</div>


<span id="4d382afc"></span>
### custom exposure event name

In addition to setting the global exposure event name directly during initialization, you can also modify it for each element.

```HTML
// this element will report exposure event named custom_exposure
<div data-exposure data-exposure-event="custom_exposure"></div>
```


<span id="28751125"></span>
### Reference: exposure_type Attribute Description

Exposure event (exposure) data report will carry $exposure_type field, which represents the type of exposure, there are the following:


* $exposure_type: 0 first exposure

* $exposure_type: 3 duplicate exposures

* $exposure_type: 6 Exposure returned from other pages

* $exposure_type: 7 Background Return Exposure


<span id="e4641fd8"></span>
## Slide event

<span id="b44eb14a"></span>
### function on

Turning on slide event collection will capture the scrolling behavior of a specific element.

```TypeScript
window.collectEvent('init', {
   autotrack: {
      scroll: {
        distance: 200 //It will not be reported until the continuous sliding distance exceeds 200px. Sliding and stopping does not count.
        callback: (data) => {
         //You can modify the data, data is the property reported by sliding
          return data
        }
      }
   }
})
```


```TypeScript
//Elements that need to be collected for sliding events
<div id="test" data-scroll='true'>I want to slide</div>
```


<span id="9410ac32"></span>
### Custom slide event name

Exposure event name Default: `$bav2b_slide`, custom event name has the following 2 ways


* **effective globally**

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         scroll: {
           eventName: 'customscroll'
         }
      }
   })
   ```
   

* **Binding elements take effect**

   ```JavaScript
   //Report custom event customscroll
   <div id="test" data-scroll data-scroll-event="customscroll" style="width:200px;height:200px;">
     <div style="width:2000px;height:200p0x;">I am the true slide element</div>
   </div>
   ```
   

* **Slide direction property: direction**

   ```JavaScript
   $direction:1 slide upward
   $direction:2 slide downward
   $direction:3 slide left
   $direction:4 slide right
   The scrolling direction here refers to the direction in which the scrollbar slides
   ```
   

* **Slide offset property: offset**

   The initialization values are all 0, the downward slide is positive, and the upward slide is negative

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8af5e014f0ae43dfbfc1339a590d9d7e~tplv-goo7wpa0wc-image.image) </span>


<span id="1ef7bbcd"></span>
## Reference: web\-side full event tracking event introduction


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page view event |Trigger the report after the page is opened |
|bav2b_click |element click event |Trigger a report after clicking on a page element |
|bav2b_page_statistics |page access event |Trigger the report after the page is opened |
|bav2b_beat |page heartbeat event |The report will be triggered after 500ms after the page is opened, closed, or the page scrolling stops. |
|bav2b_exposure |element exposure event |The appearance of elements that need to be exposed in the visible area will trigger a report |


<span id="fff8ca10"></span>
### bav2b_page

Page view events are reported when a page is opened or when routing changes. The reporting time is divided into independent pages and SPAs (single\-page applications). For independent pages, it will be reported once after the page is opened and the SDK initialization is completed. If it is a SPA page, it will be reported once after the SDK initialization is completed, and once when clicking to switch the page. The main data collected are some parameters of page browsing, which are used to analyze page browsing behavior.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bb4533a0481c26753f5a22ff06206870) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|url |Current page address |
|page_title |page title |
|page_path |page path |
|page_host |Page hosting |
|page_total_height |total page height |
|page_total_width |total page width |
|scroll_height |page scroll bar height |
|scroll_width |page scrollbar width |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|refer_page_title |Previous page title |
|refer_page_duration_ms |Last page visit time |
|refer_page_key |Previous page key |
|refer_page_manual_key |The previous page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|is_first_time |Whether to visit for the first time |


<span id="02b709db"></span>
### bav2b_click

Element click events are reported when a page click occurs.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4f1a5de5dbc5fa2d30c1e3bb23f487ce) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|element_path |element path |
|positions |element position |
|element_title |element title |
|element_id |Element ID |
|element_class_name |Element class name |
|element_type |element type |
|element_width |element width |
|element_height |element height |
|touch_x |Click position X coordinate |
|touch_y |Click position Y coordinate |
|page_start_ms |page opening time |
|since_page_start_ms |The time since the page opened when the click occurred |
|page_path |page title |
|page_host |Page hosting |


<span id="668262a3"></span>
### bav2b_page_statistics

Page access events are reported when the page is accessed. After the page is opened, it is reported once after the SDK initialization is completed (both the independent page and the SPA are reported only once). The data collected is mainly statistical information on page loading time and page width, which is used to analyze page loading statistics and other information.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_76edd8b2282e7a3a749d23c8332a3df0) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|page_init_cost_ms |Time spent on page opening |
|refer_page_key |Previous page key |
|refer_page_manual_key |The previous page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |


<span id="e3b58631"></span>
### bav2b_beat

The page heartbeat event is accessed on the page, stopped for 500ms after scrolling the page, and reported once when leaving the page.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a774d3073abf9754c76361692f03fde9) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|beat_type |Beat type, 0: leave page, 1: scroll stop, 3: visit page |
|page_title |page title |
|page_viewport_width |Page visual window width |
|page_viewport_height |Page viewable window height |
|page_total_height |total page height |
|page_total_width |total page width |
|scroll_height |page scroll bar height |
|scroll_width |page scrollbar width |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|since_page_start_ms |The time from the time the page was opened when the event occurred |


<span id="3abe27b5"></span>
### bav2b_exposure

An element exposure event is reported when an element scrolls into the visible area and meets the exposure ratio. Repeated scrolling in the visible area will only be counted once, and will not be exposed again until it is removed from the visible area and then scrolled.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">V5.1.1 and above are supported.</div>


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_874a8e461639f3b7f1864c8e9960fdfe.png) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|element_path |element path |
|positions |element position |
|element_title |element title |
|element_id |Element ID |
|element_class_name |Element class name |
|element_type |element type |
|element_width |element width |
|element_height |element height |
|touch_x |Click position X coordinate |
|touch_y |Click position Y coordinate |
|page_start_ms |page opening time |
|since_page_start_ms |The time since the page opened when the click occurred |
|page_path |page title |
|page_host |Page hosting |


<span id="4a5f43e7"></span>
## Reference: web\-side full event tracking collection element filtering rules


|**Element type** |**Whether to collect** |
|---|---|
|HTML, header, body, footer, script, link, ifram, svg etc |Do not collect |
|Div, span, a, p, img, ul, li, etc |acquisition |
|element nodeType is not equal to 1 (non\-visual element tags) |Do not collect |
|Displayed as none |Do not collect |
|The clicked element has more than 2 layers (with multiple layers of child elements). |Do not collect |
|When the element level exceeds 2 layers, but the element is a container element (a, button, or user\-specified label attribute'teaContainer ',' data\-tea\-container ') |acquisition |


<span id="991e0228"></span>
# AB test Modules and APIs

This module provides AB test capabilities and provides a range of methods: `getVar`, `getAllVars`, `getAbSdkVersion`, `setExternalAbVersion`.

<span id="749d7b9b"></span>
## enable module

Using this module, when the SDK is initialized, in addition to the common parameters to be configured in the init interface, the module switch of A/B experiment needs to be turned on: `enable_ab_test: true`, and the shunt address (ab_channel_domain field) of A/B experiment needs to be configured at the same time.

```TypeScript
window.collectEvent('init', {
    enable_ab_test: true,
    ab_channel_domain: 'https://gator.uba.ap-southeast-1.bytepluses.com',
    enable_multilink: false,//Whether to enable multi-link experiment, the default is false
    enable_ab_visual: false, //Whether to enable visual experiment, the default is false
    ab_timeout: 10000//Timeout time of shunt request, default 10000ms
    disable_ab_reset: false //Whether to prohibit re-obtaining the configuration information of A/B experiments when switching users, the default is false
    ...
});
```


<span id="6fc8819a"></span>
## modular approach

<span id="aa40e0a8"></span>
### getVar


* **Function:**  Get the configuration item value corresponding to the experiment in the AB test configuration, and the SDK will collect the corresponding vid (the business generally does not directly care about the vid). After hitting the experiment, it will automatically report a `abtest_exposure`event.

* **Parameter:** 

   
   |Parameter name |Type |Required |Explain |
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
   


<span id="af8a5711"></span>
### getAllVars


* **Function:**  Get all the configuration information of ab experiment.

* **Parameter:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |callback |(data: any) =\> void |No |If a callback is set, the callback will be executed, and all the experimental configuration data will be used as the parameters of the callback.<br><br>The experimental configuration data structure is approximately as follows:<br><br>```TypeScript```<br>```{```<br>```    aa: {```<br>```        val: 'aa-value',```<br>```        vid: '11'```<br>```    },```<br>```    test_before_6d: {```<br>```        val: 'test_before_6d-value',```<br>```        vid: '22'```<br>```    },```<br>```    bb: {```<br>```        val: 'bb-value',```<br>```        vid: '33'```<br>```    }```<br>```}```<br> |
   

* **Example:** 

   `TypeScript window.collectEvent('getAllVars', (data) => { //Get all experimental configuration information The data value is approximately as follows: /* { aa: { val: 'aa-value', vid: '11' }, test_before_6d: { val: 'test_before_6d-value', vid: '22' }, bb: { val: 'bb-value', vid: '33' }, } */ });`


<span id="027f5529"></span>
### getAbSdkVersion


* **Function:**  Get the exposed experiment, the returned result is the vid of all exposed experiments, connected with commas, format for example: 123,234,678

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |string |VIDs of all exposure experiments, linked with commas, in the format for example: 123,234,678 |
   

* **Example:** 

   ```TypeScript
   //vids value is similar to 123,234,678
   const vids = window.collectEvent('getAbSdkVersion');
   ```
   


<span id="cdb6e443"></span>
### setExternalAbVersion


* **Role:**  Manually set up additional AB test configurations.

* **Parameter:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |vids |String or null |Yes |Format requirements for vids: Concatenate vids values with commas, something like '123,234,678'.<br><br><br>* Additional experimental configuration vids set up in this way are merged into the vids obtained through getVar processing.<br><br>* When called multiple times, the last set of additional experimental configuration vids overrides the previous ones.<br><br>* When null is set, the SDK clears the set of additional experimental configuration vids without affecting the vids obtained through getVar processing. |
   

* **Example:** 

   * Set up additional experimental configurations

      ```TypeScript
      //Manually set additional
      window.collectEvent('setExternalAbVersion', '25,225,2225');
      ```
      


<span id="71f1de77"></span>
# Encryption reporting module

When accessing the Web SDK, if you want to encrypt the reported data, you can use the data encryption reporting function, which currently supports the use of national secret encryption.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When accessing the Web SDK, the following conditions must be met to use the encryption function:</div>



* <div data-tips="true" data-tips-type="warning">SDK version requirements: Please upgrade the Web SDK to the latest version of the official website (minimum supported version 5.1.6 +).</div>


* <div data-tips="true" data-tips-type="warning">DataFinder environment requirements: Currently only the DataFinder private environment supports encryption settings, but not the SaaS environment.</div>


* <div data-tips="true" data-tips-type="warning">Web page browser version requirements: Browsers below IE11 are not supported.</div>



<span id="890cf44b"></span>
## Encryption enabled

```TypeScript
 The following parameters must be set
   window.collectEvent('init', {
      enable_encryption: true,
      crypto_publicKey: 'xxxxx', //Encrypt the public key, the public key must start with 04
      encryption_type: 'sm', //Encryption type, currently only sm type is supported
      encryption_header: 'gm_sm2' //Encrypted request header type, currently only supports gm_sm2 type
   })
```


After encryption is turned on, the data will be reported in the form of national secret encryption

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fca0acf112732e148d980f663f6938c.png) </span>

<span id="f1a11f74"></span>
## Applicable interface

This feature applies to the following interfaces


1. Data reporting /list

2. User attribute reporting /profile/list

3. Device Registration /webid

4. ab experimental /abtest_config

5. request ssid /tobid

    &nbsp;


<span id="online-decryption"></span>
## online decryption

Encrypted data can be decrypted [online ](https://the-x.cn/cryptography/Sm2.aspx)on this website.

<span id="769abaa3"></span>
# lifecycle module

You can configure whether to listen for broadcasts of an SDK lifecycle, and messages applicable to the SDK runtime are used to obtain SDK status.


* Monitor broadcasts of an SDK lifecycle

   ```JavaScript
   window.collectEvent('on', 'ready', (data) => {
      //I heard that the sdk is ready, do something
      //Some messages have data, some do not
   })
   ```
   

* Cancel listening to the broadcast

   ```JavaScript
   //Cancel listening to the ready broadcast
   window.collectEvent('off', 'ready') 
   ```
   


<span id="5c4d3a83"></span>
## message list

Please check [Reference: Web/JavaScript SDK FAQ](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ).

<span id="3877b677"></span>
# event tracking module

This module provides the ability to track an event.

For example, tracking video playback time\-consuming data, but do not want to trigger data reporting every time the video operation, only need to report the data in the video playback process when the video is over, at this time you can use the tracking event module to mark Start when the video is clicked End when the broadcast is over, and report the data of all intermediate processes at the end.

<span id="7c54a9d8"></span>
## startTrackEvent

Start tracking an event.

```javascript
//Start tracking play events
window.collectEvent('startTrackEvent', 'play')
```


Calling this method does not report the play event.

<span id="e719f7fd"></span>
## endTrackEvent

To finish tracking an event, you can pass in the event and event properties.

```javascript
//Start tracking play events
window.collectEvent('endTrackEvent', 'play', {
  name: '播放结束了' // play is over
})
```


The play event is not finally reported until this event is called, with the duration parameter, which is the time elapsed during the entire play event.

<span id="b30b10fd"></span>
## pauseTrackEvent

Pause listening for an event.

```javascript
//Pause tracking of play events
window.collectEvent('pauseTrackEvent', 'play')
```


<span id="e4eb0610"></span>
## resumeTrackEvent

Restart listening for an event.

```javascript
//retrace the play event
window.collectEvent('resumeTrackEvent', 'play')
```


&nbsp;
