---
title: "Web/JavaScript SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JavaScript_SDK_Integration_"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Web/JS SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration">Web/JavaScript SDK Integration</a></div>


<span id="55ecd0bb"></span>
# Background information

This article introduces the main process and code samples of integrating the Web JS SDK for you. You can conduct SDK integration tests based on the text, and then flexibly use the currently supported event tracking and attribute capabilities according to business needs (see [Web/JavaScript SDK Event Tracking and Properties](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Event_Tracking_and_Properties)). In addition, the FAQ document also summarizes the content about SDK logic, typical scenario usage consultation, and fault/error troubleshooting for you. You can refer to it.


|Reporting logic and storage strategy |Web SDK capabilities and usage consulting |Fault/error troubleshooting |
|---|---|---|
|* [Web SDK data reporting strategy](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#web-sdk%E6%95%B0%E6%8D%AE%E4%B8%8A%E6%8A%A5%E7%AD%96%E7%95%A5)<br><br>* [web_id request logic](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#7b35371d)<br><br>* [Web SDK session id generation and storage logic](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#947f0f89)<br><br>* [User ID Storage Logic for Web SDK](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#72c328fa)<br><br>* [bav2b_beat page heartbeat event collection logic](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#91bd55b6) |* [Web multi-page application integration SDK, public property should be reported for each page?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#a7af2cac)<br><br>* [Web micro frontend project, the main application and sub-applications are connected to different applications (app_id different), is there any solution in this scenario?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#e87db7e3)<br><br>* [When there are multiple web page domains, how to connect the WebID across domain names to keep the WebID unchanged?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#ff586623)<br><br>* [Does the Web SDK have the ability to collect page crashes?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#d1fd8b0f)<br><br>* …… |* [Element exposure events (element exposure events are not experimental exposures) cannot be reported in IE browser](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#1696a3c3)<br><br>* [When integrating the Web SDK configuration multi-link experiment, it prompts that the SDK is not installed. How to deal with it?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#218947f6)<br><br>* [Forward address referrer is empty how to check?](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#%E5%89%8D%E5%90%91%E5%9C%B0%E5%9D%80referrer%E4%B8%BA%E7%A9%BA%E5%A6%82%E4%BD%95%E6%8E%92%E6%9F%A5%EF%BC%9F) |
|For more FAQs see [Reference: Web/JavaScript SDK FAQ](https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ) |||


<span id="_1-集成增长营销套件sdk"></span>
# 1. Integrated Growth Marketing Suite SDK

Copy the corresponding code snippet and place it as high as possible in the label. If you use the SaaS version, please refer to Section 1.1; if you use the privatized version, please refer to Section 1.2. The purpose of this code is to:


* Defines a global function `window.collectEvent`that can be used to configure and send events. (To avoid conflicts with other global variable names, `collectEvent`can be replaced with any custom variable name)

* Introduce a script file of the SDK.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following code for installing the SDK is a code example suitable for mainstream newer versions of browsers. The current browser versions supported by Web JS, and the installation points of lower versions of IE and Google Chrome can be modified and adjusted based on the following code examples and FAQ documents: <a href="https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#9f315aed">What browsers does the Web SDK support?</a>, <a href="https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#8085048d">Is the web SDK compatible with old versions of IE browsers?</a>, <a href="https://docs.byteplus.com/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ#ae2ec3b2">Is the web SDK compatible with old versions of Google Chrome?</a>.</div>


<span id="_1-1-安装代码-saas版本"></span>
## 1.1 Installation code (SaaS version)

If you use the SaaS deployment version, please refer to the following code.

```html
<script>    
//The function of this code is to cache the APIs called in the business code in the array q when the SDK main file is not loaded, and then take them out and execute them after the SDK main file is loaded.
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
<script async src="https://lf3-data.volccdn.com/obj/data-static/log-sdk/collect/5.0/collect-rangers-v5.2.6.js"></script>
```


<span id="2677d98b"></span>
## 1.3 Precautions

The location of the scripts and JavaScript files introduced above cannot be changed, otherwise the data may not be reported.

<span id="_2-初始化增长营销套件sdk"></span>
# 2. Initialize the Growth Marketing Suite SDK

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="4b582e9a"></span>
### SaaS\-cloud\-native


|End type |SaaS\-cloud native<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Web JS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |`channel: 'sg'` |


<span id="79c0c9cb"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk"></span>
## 2.3 Initializing the SDK

&nbsp;

<span id="90401da8"></span>
## 2.4 **Configuration completed**

After initialization, you need to notify the SDK that it is set up and can actually start sending events.

```javascript
//This line of code must be added after the initialization configuration is completed, otherwise the SDK will not send the data
window.collectEvent('start');
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Before the start</code>method is called, events can also be reported, which are cached in memory and not really sent to the server level; until the <code>start</code>call, the cached events will be combined with the set user properties and other parameters into a complete event structure, and then sent to the server level through network requests. <code>The</code>events sent after the start method call are directly merged and sent to the server level.</div>


<span id="_2-5-使用调试工具"></span>
## 2.5 **Using debugging tools**

5.1.4 above versions support local/online direct debugging event tracking, please check the [debugging tool ](https://www.volcengine.com/docs/76880/1033615)for details.

Add the following parameters after the page URL that needs to be verified:

```javascript
?open_dev_tool=true&app_id=${appid}
```


<span id="_3-初始化基本配置"></span>
# 3. Initialize the basic configuration

The following are common initialization configurations. When configuring, refer to Section 2.3/2 and add it to `window.collectEvent ('init', {/ *...* /})`.

<span id="_3-1-全埋点设置开关"></span>
## 3.1 Full event tracking setting switch

The full event tracking switch is off by default. For more features and configuration, please refer to Section 2 of the Web/JS SDK Classification Features [Web/JS SDK Classification Function](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Classification_Function).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.</div>



* <div data-tips="true" data-tips-type="tip">SaaS\-cloud native and privatization scenarios: Go to Project Center \> Project Management \> SDK Settings and make sure the full event tracking switch is turned on.</div>



```javascript
//Enable full event tracking
window.collectEvent('init', {
    // ...... Other initialization configurations
    autotrack: true
})
```


<span id="_3-2-查看日志打印"></span>
## 3.2 View log printing

Log printing is turned off by default.

```javascript
//Print detailed log information on the console to assist in troubleshooting
window.collectEvent('init', {
    // ...... Other initialization configurations
    log: true
})
```


<span id="_3-3-关闭pv事件上报"></span>
## 3.3 Turn off PV event reporting

When visiting the page, the SDK will report a pv event (event name predefine_pageview) by default, and this preset event will be reported by default. To turn off, disable this event in the initialization configuration.

Please refer to the details of the preset pv event [Web Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Web_Preset_Events_and_Properties).

```javascript
//Print detailed log information on the console to assist in troubleshooting
window.collectEvent('init', {
    // ...... Other initialization configurations
    disable_auto_pv: true //Turn on the switch to disable PV reporting
})
```


<span id="_3-4-内嵌h5页打通原生端"></span>
## 3.4 Embedded H5 page to open the native side (client side)

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


<div data-tips="true" data-tips-type="warning">The client side also needs to be initialized, please refer to <a href="https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_">Android SDK Integration</a>Section 4.6 and <a href="https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration">(Legacy Documentation)iOS SDK Integration</a>Section 4.6 respectively.</div>


**If the client side initializes with multiple instances, it may cause the connection to fail. There are two ways to adjust:** 


1. The client side calls the reporting method and uses the default instance initialization instead of multiple instances.

2. The H5 page manually binds the appids of the following multiple instances. After the init method, the following code is called before the start method.


```TypeScript
window.collectEvent('setNativeAppId', appid)
```


<span id="_3-5-初始化配置一览表"></span>
## 3.5 Initialization configuration list


|Field |Is it necessary |Field value |Field description |Examples/Remarks |
|---|---|---|---|---|
|app_id |Yes |Apply in advance. Number type |Unique identification of business products | |
|channel |No |Optional values: cn, sg |Report channel identifier. Choose one channel_domain. |Domestic, Singapore, Eastern United States |
|channel_domain |No |Legitimate domain name. String. |Choose one of the two channels. After setting this item, the channel item will be ignored. Customize the reported domain name and its path prefix. |https://xx.ccc.yy |
|log |No |Boolean type. Default false. |Whether to print detailed log information on the console. |It is recommended to open |
|disable_auto_pv |No |Boolean type. Default false. |Whether to prohibit the SDK from reporting the default PV | |
|disable_sdk_monitor |No |Boolean type. Default false. |It is used to prevent the reporting of self\-monitoring events after the SDK is started, (but the reporting of error logs is not currently prohibited.) | |
|autotrack |No |Boolean type. Default false. |Enables no event tracking reports. |Please refer to the full event tracking document for specific capabilities. |
|enable_stay_duration |No |Boolean type. Default false. |Turn on dwell time. |Please refer to the length of stay document for details. |
|cross_subdomain |No |Boolean type. Default false. |Whether to automatically identify users across subdomains, when set to true, anonymous users using the same browser in multiple subdomains will be automatically recognized as the same user, such as a.yourdomain.com and b.yourdomain.com . | |
|cookie_domain |No |String type |After opening the above configuration, you can configure the cookie domain name that stores tokens or utm parameters. If you need ' a.bytedance.com ' and ' b.bytedance.com ' to collude, pass'. bytedance.com ', if you don't pass it, it will be stored under the current domain name by default | |
|cookie_expire |No |Number type, default 7 days (in ms) |cookie expiration time | |
|max_report |No |Number type, default 20 |Custom event tracking number of combined reports | |
|reportTime |No |Number type, default 30ms |Event tracking reports the time interval of the asynchronous queue | |
|configPersist |No |Number type, default 0 |Set the config parameter whether persistent storage is required |0: not required; 1: session\-level storage; 2: localstorage persistent storage |
|timeout |No |Number type, default 100000ms |Timeout for event tracking reports | |
|enable_native (5.1.3 version below Native) |No |Boolean type |Whether to report to the native sdk |After opening, all event tracking and config settings will be completed through the native SDK, and the 5.1.3 version or above is also compatible with Native settings. |
|spa |No |Boolean type |Whether to enable the monitoring of route changes |After opening, when the route changes, the PV and dwell time will be re\-reported. |
|disable_track_event |No |Boolean type |event disable parameter |Once turned on, all event tracking is no longer reported |
|enable_custom_webid |No |Boolean type |Whether to use custom webid | |
|allow_hash |No |Boolean type |Supports listening for hash routes |5.1.3 above support |
|enable_debug |No |Boolean type |Whether to enable debug mode |5.1.4 above support |
|enable_anonymousid |No |Boolean type |Whether to report an anonymous ID |5.1.5 above support |
|enable_encryption |No |Boolean type |Whether to turn on data encryption and reporting |5.1.5 the above support, please refer to the encrypted document for details |
|crypto_publicKey |No |String type |The public key for data encryption and reporting |5.1.6 the above support, please refer to the encrypted document for details |
|encryption_type |No |String type |Types of data encryption |5.1.6 the above support, please refer to the encrypted document for details |
|encryption_header |No |String type |Data encryption request header |5.1.6 the above support, please refer to the encrypted document for details |
|enable_storage |No |Boolean type |Whether to enable the failure storage? After opening, the failed event tracking will be stored locally.<br><br>Reissue next time you open the page. |5.2.0 support, 5.2.6 this parameter is enabled by default |
|remote_file_protocol |No |String type |Fixed value, http or https, used to set the protocol for loading third\-party js files, the default is https |5.2.4 above support |
|enable_degrade |No |Boolean type |Whether to enable the degradation strategy of failed storage. After opening, the backoff strategy is used for failed reissue to reduce traffic loss. |5.2.6 and above support |


<span id="_4-测试验证"></span>
# 4. Test Verification

<span id="_4-1-初始化完成"></span>
## 4.1 Initialization is complete

Run your page in the browser, open the log and pay attention to the console information. After the SDK is successfully initialized, the following information will be printed: your appid, current user information, and the version number of the current SDK. For example:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_34199ce01c700760e03e1e7e48e02e88) </span>

When you see this information, it means that the SDK is functioning normally.

<span id="_4-2-埋点请求正常"></span>
## 4.2 The event tracking request is normal

After the SDK is initialized, an event tracking predefine_pageview event is automatically reported.

You can see the `list`request in the `network`of the browser console. For example:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_596a741684784b00695e06eb55421cc0) </span>

Click on the request to see the full event tracking data. For example:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_977777cc7f5f9ad38190556e44797511) </span>

Example after this network request is successful:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7fc6fba32793705890e62a55320e0c7f) </span>

If you do not have the above console log, or network request, or the return code of the network request is not 0 (common error codes are \-2, \-100, etc.), please contact technical support.

&nbsp;

&nbsp;

[Project Management - SDK Settings](https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings).
