---
title: "WeChat Mini Program SDK Integration (Universal)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/WeChat-Mini-Program-SDK-Integration-Universal"
---

<span id="7b43b25d"></span>
# Supported Mini Programs

The current mainstream Mini Programs can refer to this article for SDK integration, access and report the data corresponding to the Mini Program, mainly including:


* WeChat Mini Program

* Alipay Mini Program

* Baidu Mini Program

* JD.com Mini Program

* QQ Mini Program

* DingTalk Mini Program

* Xiaohongshu Mini Program

* ByteDance Mini Program

* We Mini Program


The data access operations of various Mini Programs are basically the same. The follow\-up will take WeChat Mini Program as an example to introduce the Data Transmission Service operation guidance of Mini Program. If there are differences in the operation of various Mini Program platforms, they will win the bidding in the corresponding document.

<span id="_1-集成"></span>
# Step 1 Integration

<span id="_1-1-安装sdk"></span>
## **1.1 Installing the SDK**

> Install with npm


```plain
npm install @datarangers/sdk-mp
```


<span id="_1-2-域名配置准备"></span>
## **1.2 Domain name configuration preparation**

For configuration in "Mini Program Background \- Development \- Development Settings \- Server Domain Name", you can refer to the corresponding official documentation of the Mini Program. For example, the WeChat Mini Program can refer to the [official website documentation of WeChat Mini Program](https://developers.weixin.qq.com/miniprogram/en/dev/framework/ability/network.html). The domain names for different environment configurations are as follows.


* **Privatization business:**  Add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you don't know this domain name, please contact your project manager or customer success manager.


<span id="_1-4-旧版本说明"></span>
## **1.3 Old version description**

If you integrate an older version of the SDK (below 2.0), you need to add [https://mcs.ctobsnssdk.com ](https://mcs.ctobsnssdk.com)and [https://toblog.ctobsnssdk.com ](https://toblog.ctobsnssdk.com)to the request whitelist of the WeChat open API.

<span id="_2-初始化"></span>
# 2. Initialization

<span id="_2-1-获取appid"></span>
## **2.1 Get the appid**

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-初始化sdk示例"></span>
## **2.2 Initializing the SDK Example**

<span id="7157ce32"></span>
### 2.2.1 Privatization

Privatization requires a clear data reporting domain name. If you are unsure of this domain name, please contact your project manager or customer success manager.

```javascript
//Initialize the SDK on the entry page
// app.js
import $$Rangers from '@datarangers/sdk-mp';
$$Rangers.init({
    app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    channel_domain: "{{DOMAIN}}", //Set up a private deployment data upload domain name, if you don't know this address, please contact your project manager or customer success manager
    log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
    auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
    enable_ab_test: true, //start ab experiment
    ab_channel_domain: "{{ABTEST_DOMAIN}}", //Set the ab shunt interface domain name, the default is channel_domain setting
});
$$Rangers.config({
    mp_name: 'xyz Mini Program', //Some predefined properties can be set via config mp_version: '1.1.1',
    mp_version: '1.1.1',
});
$$Rangers.send();

App({
    onLaunch: function () {
        this.$$Rangers = $$Rangers;
    
        //If you want to set the user ID, such as using open_id to identify the user, you can set the value to user_unique_id after obtaining the open_id
        this.$$Rangers.config({
            user_unique_id: 'open_id that already got', //can be open_id, can also be union_id and other business sense can be used to identify the user uniqueness value
        });
        //Call the event method to report a specific event
        this.$$Rangers.event('test_event', {
            from: 'launch', //Supports arbitrary properties, values support numbers, strings, etc
        });
    }
});
 
Other pages report events, such as:
// pages/index/index.js
Page({
    onLoad() {
        getApp().$$Rangers.event('bind_view_tap', {
            'title': 'chart',
        });
    }
});
```


<span id="787557d6"></span>
### 2.2.4 Multi\-instance initialization (optional)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Different instances have different app_id requirements.</div>


```JavaScript
//Import the SDK class (constructor)
import SDK from '@datarangers/sdk-mp/esm/sdk';

//use the new operation on the constructor to generate instance 1
const $$sdk1 = new SDK();
//other API calls are exactly the same
$$sdk1.init({
    app_id: 1338,
});
$$sdk1.config({});
$$sdk1.send();

//use the new operation on the constructor to generate instance 2
const $$sdk2 = new SDK();
//other API calls are exactly the same
$$sdk2.init({
    app_id: 1339, //app_id cannot be the same as other instances
});
$$sdk2.config({});
$$sdk2.send();
```


<span id="fbd70a11"></span>
## 2.3 Introducing Debugging Tools \- DevTools Component (Optional)

`DevTools`is a component that assists developers or testers in the Debug environment to verify in\-app event tracking and troubleshoot SDK access issues.
