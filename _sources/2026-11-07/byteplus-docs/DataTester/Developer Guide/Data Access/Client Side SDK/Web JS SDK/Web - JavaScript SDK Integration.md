---
title: "Web/JavaScript SDK Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Web-JavaScript-SDK-Integration"
---

<span id="一-概述"></span>
# Overview

"A/B Testing" does not provide a separate SDK on the Web/H5/WAP side, but relies on the A/B Testing related interface in the RangersAppLog Web SDK. The RangersAppLog SDK has two main interfaces related to A/B testing:


* Experimental group shunt interface.

* Indicator reporting (event tracking report) interface.

* Unlike other terminals, when web/h5 does experiments to modify page elements (visual experiments), it may be necessary to mask the tested page or element before the experimental parameters are returned, so as not to affect the user experience of page jumps.


The SDK supports programming experiments, visualization experiments, and multi\-link experiments.

<span id="二-集成sdk"></span>
# 1. Integrated SDK

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>This document is for SDK versions 5.0 and above</strong></div>



* <div data-tips="true" data-tips-type="warning">If you have already integrated the RangerAppLog web SDK, you can skip this section.</div>


* <div data-tips="true" data-tips-type="warning">If not, please refer to the following:</div>


   * <div data-tips="true" data-tips-type="warning">Please note that the variable name above version 5.0 is LogAnalyticsObject, and before version 5.0 is TeaAnalyticsObject.</div>


   * <div data-tips="true" data-tips-type="warning">Also, please note that your version must be greater than or equal to V5.0.0.</div>



Copy the corresponding code snippet and place it as high as possible in the label. If you use the privatized version, please refer to Section 1.2. The purpose of this code is to:


* Defines a global function `window.collectEvent`that can be used to configure and send events. (To avoid conflicts with other global variable names, `collectEvent`can be replaced with any custom variable name)

* Introduce a script file of the SDK.


<span id="_1-2-安装代码-私有化版本"></span>
### 1.1 Installation code (privatized version)

The privatization version needs to get the private address of the JS file, usually in `{{domain}}/minio.byterangers.onpremise .docor.static/collect-privacy-v5.1.12.js`If you don't know this address, please contact your project manager or customer success manager.

If you use the private deployment version, please refer to the following code.

```html
<script>    
(function(win, export_obj) {
    win['LogAnalyticsObject'] = export_obj;
    if (!win[export_obj]) {
        var _collect = function() {
            _collect.q.push(arguments);
        }
        _collect.q = _collect.q || [];
        win[export_obj] = _collect;                
    }
    win[export_obj].l = +new Date();
})(window, 'collectEvent');
</script>
<script async src="{{domain}}/minio.byterangers.onpremise.docor.static/collect-privity-v5.1.12.js"></script>
```


You can also use the private address provided by Volcano.

```html
<script async src="https://lf3-data.volccdn.com/obj/data-static/log-sdk/collect/5.0/collect-privity-v5.1.12.js"></script>
```


If you can't integrate remotely, please contact your project manager or customer success manager, or you can directly download the above js file for offline import.

<span id="_2-初始化-sdk"></span>
## 2. Initialize the SDK

<span id="_2-1-获取appid"></span>
### 2.1 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-获取数据上送地址"></span>
### 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk-saas版本"></span>
### 2.3 Initializing the SDK

<span id="3a2b8282"></span>
### 2.3.1 Privatization version

If you use the private deployment version, please refer to the following code to initialize the SDK.

```javascript
window.collectEvent('init', {
    app_id: {{APPID}}, //Refer to Section 2.1 to obtain, note that the type is number, not string
    channel_domain: '{{REPORT_URL}}', //Set the private deployment data upload address, refer to Section 2.2 to obtain
    ab_channel_domain: '{{REPORT_URL}}' //Set up a privatized domain name, usually the data upload address, refer to Section 2.2 to obtain
    log: true, //true: open log, false: close log
    autotrack: false, //Full event tracking switch, true on, false off
    enable_ab_test: true, //boolean type, whether to enable the A/B experiment function
    enable_ab_visual: false, //boolean type, on demand, off by default, whether to enable the visual editing mode function of A/B experiments
    enable_multilink: false, //boolean type, open on demand, closed by default, whether to enable the multi-link experiment function of A/B experiment, the default is false
    multilink_timeout_ms:1000 //number type, the time to close the mask layer in the multi-link experiment of A/B experiment, the default is 500 milliseconds
});
//Here you can add code such as setting uuid and setting public properties
window.collectEvent('start'); //Notify the SDK that it is set up and can actually start sending events.
```


<span id="0a54eefd"></span>
### 2.4 Configuration completed

After initialization, you need to notify the SDK that it is set up and can actually start sending events.

**Description: Before the** `start`method is called, events can also be reported, these events are cached in memory and not really sent to the server level; until the `start`call, the cached events will be combined with the set user properties and other parameters into a complete event structure, and then sent to the server level through network requests. `The`event sent after the start method call is directly merged with the parameters and then sent to the server level.

```javascript
//This line of code must be added after the initialization configuration is completed, otherwise the SDK will not send the data
window.collectEvent('start');
```


<span id="c3bd2bd2"></span>
## 2.5 Using debugging tools

5.1.4 the above version supports debugging event tracking.

Set the following parameters during initialization:

```JavaScript
window.collectEvent('init', {
  //....
  enable_debug: true //Close this parameter before going live
})
```


At the same time, add the following parameters after the page URL that needs to be verified (**5.1.7 later versions can not add the following parameters**):

```JavaScript
?open_devtool_web=true&app_id=${appid} //your appid.
```


<span id="_3-初始化基本配置"></span>
## 3. Initialize the basic configuration

The following are common initialization configurations. When configuring, refer to Section 2.3/2 and add it to `window.collectEvent ('init', {/ *...* /})`.

<span id="_3-1-全埋点设置开关"></span>
### 3.1 Full event tracking setting switch

The full event tracking switch is off by default.

```javascript
//Enable full event tracking
window.collectEvent('init', {
    // ...... Other initialization configurations
    autotrack: true
})
```


<span id="_3-2-查看日志打印"></span>
### 3.2 View log printing

Log printing is turned off by default.

```javascript
//Print detailed log information on the console to assist in troubleshooting
window.collectEvent('init', {
    // ...... Other initialization configurations
    log: true
})
```


<span id="_3-3-ab功能相关"></span>
### 3.3 AB Function Related

```javascript
window.collectEvent('init', {
    enable_ab_test: true, //boolean type, whether to enable the A/B experiment function
    enable_ab_visual: false, //boolean type, on demand, off by default, whether to enable the visual editing mode function of A/B experiments
    enable_multilink: false, //boolean type, open on demand, closed by default, whether to enable the multi-link experiment function of A/B experiment, the default is false
    multilink_timeout_ms:1000 //number type, the time to close the mask layer in the multi-link experiment of A/B experiment, the default is 500 milliseconds
    auto_exposure_expriment: false //boolean type, on demand, off by default, whether to automatically expose the full amount of experiments 5.1.10 version support
})
```


<span id="33c680de"></span>
### 3.4 Automatic Exposure Full

```JavaScript
window.collectEvent('init', {
    enable_ab_test: true, //boolean type, whether to enable the A/B experiment function
    auto_exposure_expriment: false //boolean type, on demand, off by default, whether to automatically expose the full amount of experiments 5.1.10 version support
})
```


**After opening, the SDK will automatically expose all experiments (except multi\-link experiments and visual experiments) according to the experimental results issued, and there is no need to call the getVar method. 5.1.10 version will start to support it.** 

<span id="_3-4-禁止ab数据重置"></span>
### 3.5 Prohibit AB data reset

Whether to disable reset of AB data when changing user_unique_id. It is usually used to convert the anonymous state to the real\-name state. Switch between multiple users, please do not turn on.

Reason: When setting the user_unique_id through the config method, the SDK will judge that if the user_unique_id has changed, the cache of the previous AB data will be deleted at this time, and the AB shunt request will be reinitiated. In this process, if there is data reported, it may not be able to bring vid.

```javascript
window.collectEvent('init', {
    // ...... Other initialization configurations
    disable_ab_reset: true  | false //default false
})
```


<span id="_3-5-关闭pv事件上报"></span>
### 3.56 Turn off pv event reporting

When visiting the page, the SDK will report a pv event (event name predefine_pageview) by default, and this preset event will be reported by default. To turn off, disable this event in the initialization configuration.

```javascript
//Print detailed log information on the console to assist in troubleshooting
window.collectEvent('init', {
    // ...... Other initialization configurations
    disable_auto_pv: true //Turn on the switch to disable PV reporting
})
```


<span id="_3-6-内嵌h5页打通原生端"></span>
### 3.7 Embedded H5 page to open the native side (client side)

After the client side opens the embedded H5 page, the events generated on the embedded H5 page will be reported through the client side SDK, not the js SDK, and the `user_unique_id`and public properties set by the client side will be reused. At this point, you also need to turn on the open switch on the H5 page of the integrated JSSDK.

```javascript
//H5 is embedded in the native terminal and connected
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_native: true 
    //5.1.3 the following version parameters are Native,
    //5.1.3 the above version is changed to enable_native, but still compatible with Native settings
})
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The client side also needs to be initialized, please refer to the Android and iOS Integration Development Guidelines respectively.</div>


**If the client side initializes with multiple instances, it may cause the connection to fail. There are two ways to adjust:** 


1. The client side calls the reporting method and uses the default instance initialization instead of multiple instances.

2. The H5 page manually binds the appids of the following multiple instances. After the init method, the following code is called before the start method.


```TypeScript
window.collectEvent('setNativeAppId', appid)
```


<span id="_3-7-初始化配置一览表"></span>
### 3.8 Initialization configuration list


|Field |Is it necessary |Field value |Field description |Examples/Remarks |
|---|---|---|---|---|
|app_id |Yes |Apply in advance. Number type |Unique identification of business products | |
|channel |No |Optional values: cn, sg, va |Report channel identifier. Choose one channel_domain. |Domestic, Singapore, Eastern United States |
|channel_domain |No |Legitimate domain name. String. |Choose one of the two channels. After setting this item, the channel item will be ignored. Customize the reported domain name and its path prefix. |[https://xx.ccc.yy](https://xx.ccc.yy) |
|ab_channel_domain |No |Legitimate domain name. String. |Privatized domain name<br><br>When this parameter is set, ab experiment obtains the domain name based on this parameter. |[https://xx.ccc.yy](https://xx.ccc.yy) |
|log |No |Boolean type. Default false. |Whether to print detailed log information on the console. |It is recommended to open |
|enable_ab_test |Yes |Boolean type. Default false. |Whether to turn on the A/B experiment function | |
|enable_ab_visual |No |Boolean type. Default false. |Whether to start a visual experiment<br><br>When this parameter is set, the ab experiment executes the visual logic when it reads the visual configuration<br><br>The premise is that the main switch of the enable_ab_test must be turned on | |
|enable_multilink |No |Boolean type. Default false. |Whether to start the multi\-link experiment<br><br>Note: To open the multi\-link experiment, you need to turn on the premise of AB test, and the main switch of enable_ab_test must be turned on | |
|multilink_timeout_ms |No |Number type |Default time to close mask layer in multi\-link experiment<br><br>Default: 500 milliseconds<br><br>The premise is that the main switch of the enable_ab_test must be turned on |ebable_ab_test:true<br><br>enable_multilink: true,<br><br>multilink_timeout_ms:3000 |
|disable_auto_pv |No |Boolean type. Default false. |Whether to prohibit the SDK from reporting the default PV | |
|disable_sdk_monitor |No |Boolean type. Default false. |It is used to prevent the reporting of self\-monitoring events after the SDK is started, (but the reporting of error logs is not currently prohibited.) | |
|autotrack |No |Boolean type. Default false. |Enables no event tracking reports. |Please refer to the full event tracking document for specific capabilities. |
|enable_stay_duration |No |Boolean type. Default false. |Turn on dwell time. |Please refer to the length of stay document for details. |
|cross_subdomain |No |Boolean type. Default false. |Whether to automatically identify users across subdomains, when set to true, anonymous users who use the same browser in multiple subdomains will be automatically recognized as the same user, such as in the case of a. [yourdomain.com ](http://yourdomain.com)and b. [yourdomain.com ](http://yourdomain.com). | |
|cookie_domain |No |String type |After opening the above configuration, you can configure the cookie domain name that stores the token or utm parameters. If you need'a. [bytedance.com ](http://bytedance.com)'and'b. [bytedance.com ](http://bytedance.com)' to collude, pass in '. [bytedance.com ](http://bytedance.com)'. If you don't pass it, it will be stored under the current domain name by default | |
|cookie_expire |No |Number type, default 7 days (in ms) |cookie expiration time | |
|max_report |No |Number type, default 20 |Custom event tracking number of combined reports | |
|reportTime |No |Number type, default 30ms |Event tracking reports the time interval of the asynchronous queue | |
|configPersist |No |Number type, default 0 |Set the config parameter whether persistent storage is required |0: not required; 1: session\-level storage; 2: localstorage persistent storage |
|timeout |No |Number type, default 100000ms |Timeout for event tracking reports | |
|enable_native (5.1.3 version below Native) |No |Boolean type |Whether to report to the native sdk |Once turned on, all event tracking and config settings will be done through the native SDK |
|spa |No |Boolean type |Whether to enable the monitoring of route changes |After opening, when the route changes, the PV and dwell time will be re\-reported. |
|disable_track_event |No |Boolean type |event disable parameter |Once turned on, all event tracking is no longer reported |
|enable_custom_webid |No |Boolean type |Whether to use custom webid | |
|allow_hash |No |Boolean type |Supports listening for hash routes |5.1.3 and above versions support |
|ab_cross |No |Boolean type |Whether AB data is stored across domain names |5.1.3 and above versions support |
|ab_cookie_domain |No |String type |After AB data cross\-domain name storage is turned on, the stored domain name |5.1.3 and above versions support |
|disable_ab_reset |No |Boolean type |Reset ab data after setting uuid |5.1.3 and above versions support |
