---
title: "Mini Program SDK Event Tracking and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Mini_Program_SDK_Event_Tracking_and_Properties"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Mini Program SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration">Mini Program SDK Integration</a></div>


> Before reporting events and properties, read the [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).


<span id="_1-用户与用户属性"></span>
# 1. Users and user properties

<span id="_1-1-登录态变化调用"></span>
## 1.1 Login state change call

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```javascript
$$Rangers.config({
    user_unique_id: '{{USER_UNIQUE_ID}}'
});
```


<span id="_1-1-1-setuseruniqueid"></span>
### 1.1.1 setUserUniqueID

2.6.0 + version, you can use the setUserUniqueID method to set the uuid.

```javascript
//set uuid
$$Rangers.setUserUniqueID('{{USER_UNIQUE_ID}}');

//clear the uuid
$$Rangers.setUserUniqueID(null);
```


<span id="_1-2-设置用户属性"></span>
## 1.2 Setting user properties

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note: Before using the profile API, you need to configure <code>enable_profile = true</code>in init.</div>


<span id="_1-2-1-profileset"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```javascript
//Example: Set the user property, the property name is key, and the property value is value
$$Rangers.profileSet({
    key: 'value' //value support string, number, array
});
```


<span id="_1-2-2-profilesetonce"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```javascript
//Example: Set a user property with the property name key_once and the property value value_once
$$Rangers.profileSetOnce({
    key_once: 'value_once' //value support string, number, array
});
```


<span id="_1-2-3-profileincrement"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```javascript
//Example: Set the user property, the property name is key, and the property value is 1
$$Rangers.profileIncrement({
    key: 1
});
```


<span id="_1-2-4-profileappend"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```javascript
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
$$Rangers.profileAppend({
    key: 'value_append'
});
```


<span id="_1-2-5-profileunset"></span>
### 1.2.5 profileUnset

Delete the user's properties.

```javascript
//Example: Delete a user property named key
$$Rangers.profileUnset('key');
```


<span id="_2-事件与事件属性"></span>
# 2. Events and event properties

<span id="_2-1-上报代码埋点"></span>
## 2.1 Reporting code event tracking

User behavior logs are in the form of event + propertyparams. Events typically correspond to multiple properties, or they can only have events without properties. Code event tracking schemes are typically designed by data analysts or product operations. Code event tracking that only reports events, as follows:

```javascript
//Example: Report an event that does not contain properties
//placed in the corresponding position of business logic
$$Rangers.event('event');
```


Code event tracking for reporting events and corresponding properties, as follows:

```javascript
//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
//placed in the corresponding position of business logic
$$Rangers.event('event', {
   key_string: 'value_string',
   key_int: 10
});
```


<span id="_2-2-事件公共属性"></span>
## 2.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="_2-2-1-设置公共属性"></span>
### 2.2.1 set public properties

```javascript
//Example: Set a custom public property with the property name key_public and the property value value_public
$$Rangers.config({
   key_public: 'value_public'
});
```


<span id="_2-2-1-1-setheaderinfo"></span>
#### 2.2.1.1 setHeaderInfo

2.6.0 + version, you can use the setHeaderInfo method to set public properties

```javascript
//Example: Set a custom public property with the property name key_public and the property value value_public
$$Rangers.setHeaderInfo('key_public', 'value_public');
```


<span id="_2-2-1-2-removeheaderinfo"></span>
#### 2.2.1.2 removeHeaderInfo

2.6.0 + version, you can use the removeHeaderInfo method to remove public properties

```javascript
//Example: Removing a custom public property named key_public
$$Rangers.removeHeaderInfo('key_public');
```


<span id="_3-api说明"></span>
# 3. API description

<span id="_3-1-sdk预设公共属性字段"></span>
## 3.1 SDK default public property fields

The SDK will assign values to some fields by default in `config ({})`, and these fields set by the SDK by default can be overridden. Please note that the nickname, avatar, and geographical information of the "Share User" function in the growth analysis product need to be reported by you on your own initiative.


|**Field** |**Type** |**Explain** |**Is it automatically set?**  |**Example** |
|---|---|---|---|---|
|device_brand |string |Equipment brand |automatic |"iPhone" |
|device_model |string |Equipment model |automatic |"iPhone 7" |
|os_name |string |Client side system |automatic |"ios" |
|os_version |string |Client side/OS version |automatic |"iOS 10.0.1" |
|screen_width |number |screen width |automatic |375 |
|screen_height |number |Screen height |automatic |812 |
|resolution |string |screen definition |automatic |"375x812" |
|access |string |network type |automatic |"wifi" |
|language |string |system language |automatic |"zh_CN" |
|app_version |string |Business Mini Program Version |automatic |"2.5.0" |
|device_id |number |Device ID |Business party settings |67834512 |
|nick_name |string |nickname |Business party settings |"Zhang San." |
|gender |string |Gender |Business party settings |"male" |
|avatar_url |string |avatar |Business party settings |"https://xxx" |
|timezone |number |Time Zone |Business party settings |8 |
|tz_offset |number |time zone offset |Business party settings |\-28800 |


<span id="_3-2-获取平台生成的各种id"></span>
## 3.2 Obtain various IDs generated by the platform

Obtain the token information of the SDK, which contains web_id, ssid, user_unique_id information.

```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; Bind to the global app for other pages to call.
    this.$$Rangers.getToken((token) => { 
        //token data content for example:
        // {
        //    "web_id":"6748002161499735560",
        //    "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
        //    "user_unique_id":"xxx",
        // }
    })
    // ...
  }
});
```


<span id="_3-3-自定义webid-以及-与小程序内h5页面打通"></span>
## 3.3 Customize webid and connect with the H5 page in the Mini Program

<span id="_3-3-1-自定义webid"></span>
### 3.3.1 custom webid

To change the SDK's default webid, first initialize with `enable_custom_webid: true`enabled, and then set web_id via config.

```javascript
$$Rangers.init({
    //Other initialization configurations
    enable_custom_webid: true, //Open enable_custom_webid at initialization
});
```


Once turned on, config web_id at other times.

```javascript
$$Rangers.config({
    web_id: '11111111111111', //The value of webid requires a pure number or a string type that is all numbers
});
```


You can also use the `setWebIDviaUnionID`and `setWebIDviaOpenID`methods provided by the SDK to set web_id


* `setWebIDviaUnionID Set`the unionid of the Mini Program user to web_id


```javascript
$$Rangers.setWebIDviaUnionID('{{unionid of Mini Program user}}');
```



* `setWebIDviaOpenID`sets the openid of the Mini Program user to web_id


```javascript
$$Rangers.setWebIDviaOpenID('{{openid of Mini Program user}}');
```


It should be noted that when the custom webid is enabled, the webid must be actively set before the SDK can actually initialize and continue the subsequent process. This scenario is suitable for the H5 page to open in the WeChat Mini Program. You need to pass WeChat's unionID or openID to the H5 page.

<span id="_3-3-2-与小程序内h5页面打通"></span>
### 3.3.2 connect with the H5 page in the Mini Program

Use the `createWebViewUrl`and `createWebViewUrlAsync`two methods provided by the SDK to pass the web_id to the H5 page to achieve the purpose of getting through


* `createWebViewUrl`, add web_id on the url of the webview component in the Mini Program and pass it to the h5 page. It should be noted that this method can only be used after the SDK initialization is completed to ensure that there must be web_id


```javascript
// webview.wxml
<web-view src="{{ webUrl }}"></web-view>

// webview.js
Page({
   data: {
      webUrl: ''
   },
   onLoad(options) {
      let url = 'https://example/demo.html';
      this.setData({
         webUrl: $$Rangers.createWebViewUrl(url),
      });
   }
});
```



* `createWebViewUrlAsync`, this is the asynchronous version of `createWebViewUrl`, returns promise, not affected by SDK initialization, will definitely get web_id


```javascript
// webview.wxml
<web-view src="{{ webUrl }}"></web-view>

// webview.js
Page({
   data: {
      webUrl: ''
   },
   onLoad(options) {
      let url = 'https://example/demo.html';
      $$Rangers.createWebViewUrlAsync(url).then((webviewUrl) => {
         this.setData({
            webUrl: webviewUrl,
         });
      });
   }
});
```


<span id="_3-4-预置事件自动上报"></span>
## 3.4 Automatic reporting of preset events

Use preset event automatic reporting, you need to configure the `auto_report`parameter to true during initialization. It is recommended that you enable this event. Note: The event name of a custom event should not be the same as the preset event. Mini Program Preset Events Please refer to: [Mini Program Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_Preset_Events_and_Properties).

<span id="_3-4-1-开启说明"></span>
### 3.4.1 opening instructions

Set auto_report parameters through the init method to enable the function


|Parameter |Parameter value type |Explain |
|---|---|---|
|auto_report |boolean<br><br>or<br><br>{<br><br>appLaunch?: boolean;<br><br>appTerminate?: boolean;<br><br>appError?: boolean;<br><br>pageShow?: boolean;<br><br>pageHide?: boolean;<br><br>pageShare?: boolean;<br><br>pageFavorite?: boolean;<br><br>click?: boolean;<br><br>} |Default value is false<br><br>Can be set to true or object<br><br>When set to true, it is equal to setting to empty object {}, which is also equal to setting as follows<br><br>{<br><br>appLaunch: true,//report app_launch event, not when false<br><br>appTerminate: true,//Report app_terminate event, not when false, or not when appLaunch is false<br><br>appError: true,//report on_error event, not report when false<br><br>pageShow: true,//report predefine_pageview event, do not report when false<br><br>pageHide: true,//Report predefine_pageview_hide event, not reported when false, or the event will not be reported when pageShow is false<br><br>pageShare: true,//report on_share event, not report when false<br><br>pageFavorite: true,//Report on_addtofavorites event, not when false<br><br>Click: false,//do not report bav2b_click event, only report when true<br><br>} |


<span id="_3-4-2-接入代码示例"></span>
### 3.4.2 Access Code Sample


* Do not report click events, but report other predefined events, set to true or empty object {}


```javascript
const $$Rangers = require('@datarangers/sdk-mp'); 
$$Rangers.init({
    // ... Other initialization configurations
    //or auto_report: {}
    auto_report: true
}); 
$$Rangers.send();
```



* To report all predefined events, including click events, click needs to be set to true.


```javascript
const $$Rangers = require('@datarangers/sdk-mp'); 
$$Rangers.init({
    // ... Other initialization configurations
    auto_report: {
        click: true
    }
}); 
$$Rangers.send();
```



* Report most predefined events, but not error events, set appError to false, and other events are similarly set


```javascript
const $$Rangers = require('@datarangers/sdk-mp'); 
$$Rangers.init({
    // ... Other initialization configurations
    auto_report: {
        click: true,
        appError: false
    }
}); 
$$Rangers.send();
```


<span id="_3-4-3-关于点击事件"></span>
### 3.4.3 about click events

When click is set to true, the SDK will report bav2b_click event (currently only the bindtap type is supported) when components bound to some event functions are clicked, which will collect the contents of the dataset dataset on the component as parameters. Suppose the following components are set with id = "diandian" and data\-hi = "hello"

```html
<view id="diandian" data-hi="hello" bindtap="tapMethod">点我</view>
```


When the component is clicked, the reported bav2b_click events and collected parameters are approximately as follows

```json
{
  event: 'bav2b_click',
  params: {
    path: 'pages/index/index',
    query_id: 'diandian',
    query_hi: 'hello'
  }
}
```


**Property filtering**

Version requirements: 2.12.0 and above

The initialization parameter increases clickIgnoreProperty, a type array, which is valid when click is set to true. The function is to filter the corresponding properties in the dataset value of the clicked element, such as setting ['abc', 'xxx'], then all the clicked elements with abc or xxx on the property will be filtered out and will not be collected.


* **Global settings**


```JavaScript
$$Rangers.init({
    // ...
    auto_report: {
        click: true,
        clickIgnoreProperty: ['imgSrc', '...'],
    }
});
```



* **Single element settings**


```HTML
// example as below
<view bindtap="ontest" data-xxx="xxx-value" data-yyy="yyy-value" data-zzz="zzz-value" data-click-ignore-property="xxx,yyy"></view>
```


<span id="_3-5-多实例使用方式"></span>
## 3.5 Multi\-instance usage

It is important to note that the app_id needs of different instances are different.

```javascript
//Import the SDK class (constructor)
import SDK from '@datarangers/sdk-mp/esm/sdk';

//use the new operation on the constructor to generate instance 1
const $$Rangers1 = new SDK();
//other API calls are exactly the same
$$Rangers1.init({
    app_id: 1338,
});
$$Rangers1.config({});
$$Rangers1.send();

//use the new operation on the constructor to generate instance 2
const $$Rangers2 = new SDK();
//other API calls are exactly the same
$$Rangers2.init({
    app_id: 1339, //app_id cannot be the same as other instances
});
$$Rangers2.config({});
$$Rangers2.send();
```


<span id="_3-6-在飞书小组件中的使用方式"></span>
## 3.6 How to use Lark widgets

Note that in the Lark widget scenario, preset event reporting is not supported (i.e. auto_report parameter setting is invalid). Version requirements: 2.9.0 +

```javascript
import Sdk from '@datarangers/sdk-mp/esm/block';
//If you need functions such as ab plugins, you need to load the plugins manually
import AbPlguin from '@datarangers/sdk-mp/esm/plugin/ab';
Sdk.usePlugin(AbPlugin);
//If you need the functions of other plugins, it is the same as the ab plugin above

const $$Rangers = new Sdk();
$$Rangers.init({
   //...
});
$$Rangers.config({});
$$Rangers.send();
// ....
```


<span id="9d039753"></span>
## 3.7 Multi\-caliber binding processing

Version requirements: 2.11.0 +, only SaaS cloud native, private support.

```TypeScript
//Phone and email in the example are only examples, and the specific transmission is determined by the business
$$Rangers.bind({
    phone: '130xxxxxxxx',
    email: 'xxx@yyy.com'
}).then((status) => {
    //The business performs subsequent processing according to the status, optional processing
});
```


<span id="_4-小程序第三方框架适配"></span>
# 4. Mini Program third\-party framework adaptation

For automatic event reporting (app_launch, app_terminate, etc.), the SDK is compatible with `taro`and `uni-app`third\-party frameworks. This compatibility requires that the SDK version is higher than 1.1.1.

<span id="_4-1-taro框架使用方式"></span>
## 4.1 How to use the taro framework


* Import the SDK via import in app.jsx

* Initialize the SDK before the App class


<span id="_4-2-uni-app框架使用方式"></span>
## 4.2 Usage of the uni\-app framework


* Introducing the SDK via import in main.js

* Initialize the SDK before the App class


<span id="_4-3-预置事件上报排查"></span>
## 4.3 Preset event reporting for investigation

If you find that some automatic events have not been reported, you can check the following situations:


* Place the initialization of the SDK at the front of the project entrance as much as possible.

* The third\-party framework requires a relatively new version, taro, uni\-app (other third\-party frameworks have not yet been specially compatible and may not support it);

* At the same time, other SDKs with similar functions are introduced. In this case, we try to initialize our SDK after other SDKs (but it still needs to be in front of the App class).
