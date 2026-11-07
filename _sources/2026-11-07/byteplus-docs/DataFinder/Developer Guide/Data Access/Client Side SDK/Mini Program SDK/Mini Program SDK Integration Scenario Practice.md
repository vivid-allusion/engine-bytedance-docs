---
title: "Mini Program SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice"
---

<span id="6ff245df"></span>
# user_unique_id related

<span id="e7ec629e"></span>
## user login settings

For example, the business has an account system and wants the SDK to synchronize user status. You can consider setting user_unique_id to the SDK immediately after the user logs in, and clearing the user_unique_id to the SDK immediately after the user logs out.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: The concept of user login status is a statement from a business perspective. The SDK itself does not have the concept of user login/login. The SDK only cares about whether the user_unique_id has been actively set.</div>


```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

//Set user_unique_id immediately after user login
$$sdk.config({
    user_unique_id: '{{uuid}}', //Values can be considered as properties that can be associated with the user
});

//Clear user_unique_id immediately after user logs out
$$sdk.config({
    user_unique_id: '',
});
```


Also the `2.6.0 +`version of the SDK provides the `setUserUniqueID`method to set user_unique_id.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

//Set user_unique_id immediately after user login
$$sdk.setUserUniqueID('{{uuid}}'); //Values can be considered as properties that can be associated with the user

//Clear user_unique_id immediately after user logs out
$$sdk.setUserUniqueID('');
```


<span id="78b62c1b"></span>
## Use openid/unionid to set as logged in user

In this scenario, you need to first get the openid/unionid (usually these IDs need to carry code for the server level of the business to open the API interface to the Mini Program, such as code2Session, initiate a request, exchange openid, unionid, session_key and other information), and then use the config or setUserUniqueID method to set it to the SDK.

The following is an example of the WeChat Mini Program platform:

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

App({
    //......
    onLaunch() {
        // ......
        wx.login({
            success(res) {
                if (res.code) {
                    wx.request({
                        url: 'https://xxxxxx.com/', //The server level interface of the business itself, to request the Mini Program open API interface in exchange for openid/unionid
                        data: {
                            code: res.code,
                        },
                        success(res) {
                            //want to use openid to set user_unique_id
                            if(res.openid) {
                                $$sdk.config({
                                    user_unique_id: res.openid,
                                });
                            }
                            
                            //or want to use unionid to set user_unique_id
                            if(res.unionid) {
                                $$sdk.config({
                                    user_unique_id: res.unionid,
                                });
                            }
                        }
                    });
                }
            }
        });
    }
});
```


<span id="3b758156"></span>
## User criteria related processing

If you want to set the user aperture, you need to set the user_unique_id_type at the same time as setting the user_unique_id.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

$$sdk.config({
    user_unique_id: 'tangseng',
    user_unique_id_type: 'huoshan', //user_unique_id_type values are prefabricated
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: user_unique_id_type values are pre\-made, ask your project manager or customer success manager.</div>


<span id="c45646a0"></span>
## Multi\-user aperture type processing

If you want to perform multi\-aperture binding, you need to call the bind method after setting the user_unique_id_type while setting the user_unique_id. Note: The SDK version requires 2.11.0 + and is only supported in the SAAS Cloud Native, Private.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At present, only SaaS\-cloud\-native environments and privatized environments support multi\-user capabilities. Before use, you need to contact BytePlus technical support staff to turn on the function switch and complete the multi\-criteria input configuration.</div>


```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

//Phone and email in the example are just examples, and the specific criteria of transmission is determined by the business
$$sdk.bind({
    phone: '130xxxxxxxx',
    email: 'xxx@yyy.com'
}).then((status) => {
    //The value of status is true or false, true means success, false means failure
    //The business performs subsequent processing according to the status, optional processing
});
```


<span id="4d4bb581"></span>
# web_id and H5 related

<span id="47334f49"></span>
## Get the web_id and ssid generated by the SDK by default

The SDK will automatically generate web_id and ssid for you. If you want to get these IDs generated by the SDK by default, you can refer to the following methods.

**Get web_id**

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

$$sdk.on($$sdk.types.Ready, () => {
    const webid = $$sdk.getConfig('web_id');
    console.log('web_id', webid);
});
```


**Get ssid**

> Note: When obtaining the ssid, you actually need to call getToken to obtain the ssid. This method will initiate a request to obtain the ssid in the data flow service of the DataFinder. The ssid is not managed by the SDK side.


```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

$$sdk.getToken().then((ids) => {
    const ssid = ids.ssid;
    console.log('ssid', ssid);
});
```


<span id="cb231913"></span>
## Custom web_id

> In general, you can directly use the Web_id automatically generated by the SDK. In some special scenarios, if you want to use a custom web_id to override the web_id automatically generated by the SDK, you can refer to the following methods.


If you want to override the web_id generated by the SDK by default, you first need to enable `enable_custom_webid: true`during initialization, and then set web_id.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    enable_custom_webid: true,
});
$$sdk.send();
```


After opening, you need the business active config setting web_id.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: When <code>enable_custom_webid: true</code>is enabled, the SDK will wait for the business to actively set web_id, if web_id has not been set, the SDK will not report the event.</div>


web_id value requires either a pure number or a string of all numbers, and the maximum number cannot exceed 2 ^ 64. The web_id of different users should not be the same.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    enable_custom_webid: true,
});
$$sdk.send();

//Proactively set up web_id at the right time
$$sdk.config({
    web_id: '12345678910',
});
```


In addition, you can also use the `setWebIDviaUnionID`and `setWebIDviaOpenID`methods provided by the SDK to set the web_id.


* `setWebIDviaUnionID`: to meet business users to get the user's unionid to set web_id.

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
       enable_custom_webid: true,
   });
   $$sdk.send();
   
   //Set the web_id after getting the user's unionid
   $$sdk.setWebIDviaUnionID('{{用户的unionid}}');
   ```
   

* `setWebIDviaOpenID`: to meet the business user to obtain the user's openid to set web_id.

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
       enable_custom_webid: true,
   });
   $$sdk.send();
   
   //Set the web_id after getting the user's openid
   $$sdk.setWebIDviaOpenID('{{用户的openid}}'); //user's openid
   ```
   


<span id="f1c46931"></span>
## Associated with H5 page web_id

> The Mini Program itself has many limitations between its internal H5 pages, and the capabilities offered by the Mini Program platform itself are also limited. At present, the SDK only provides web_id to the H5 page.


The SDK provides `createWebViewUrl`and `createWebViewUrlAsync`two methods to pass web_id to H5 pages.


* `createWebViewUrl`: Add web_id pass to the h5 page on the url of the webview component in the Mini Program, it should be noted that this method can only be used after the SDK initialization is completed to guarantee web_id.

   ```HTML
   <!-- webview.wxml -->
   <web-view src="{{ webUrl }}"></web-view>
   ```
   

   ```TypeScript
   // webview.js
   Page({
      data: {
         webUrl: ''
      },
      onLoad(options) {
         let url = 'https://example/demo.html';
         this.setData({
            webUrl: $$sdk.createWebViewUrl(url),
         });
      }
   });
   ```
   

* `createWebViewUrlAsync`: This is the asynchronous version of `createWebViewUrl`, which returns promises, which are not affected by the initialization of the SDK, and will definitely get web_id.

   ```HTML
   <!-- webview.wxml -->
   <web-view src="{{ webUrl }}"></web-view>
   ```
   

   ```TypeScript
   // webview.js
   Page({
      data: {
         webUrl: ''
      },
      onLoad(options) {
         let url = 'https://example/demo.html';
         $$sdk.createWebViewUrlAsync(url).then((webviewUrl) => {
            this.setData({
               webUrl: webviewUrl,
            });
         });
      }
   });
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: The <code>createWebViewUrl</code>and <code>createWebViewUrlAsync</code>methods essentially append web_id parameters to the src of the webview component to achieve the purpose of passing the web_id to the H5 page.</div>


<span id="94fe611c"></span>
# Event (including presets), event properties, and event public properties are related

<span id="7ee332b7"></span>
## Enable preset event reporting

To enable automatic reporting of preset events, you need to configure the `auto_report`parameter to true during initialization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: Please refer to the Mini Program preset event <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_Preset_Events_and_Properties">Mini Program Preset Events and Properties</a>, the event name of the custom event should not be renamed with the preset event.</div>



|Parameter |Type |Explain |
|---|---|---|
|auto_report |```TypeScript```<br>```boolean```<br>```    appLaunch?: boolean;```<br>```    appTerminate?: boolean;```<br>```    appError?: boolean;```<br>```    pageShow?: boolean;```<br>```    pageHide?: boolean;```<br>```    pageShare?: boolean;```<br>```    pageFavorite?: boolean;```<br>```    click?: boolean;```<br>```}```<br> |{<br><br>Sets whether the preset event and preset property data provided to you need to be automatically collected (default is false, no collection). Currently supports setting the value of the auto_report to true/false or the value of the specific object (choose one of the two):<br><br><br>* True/false: When set to true, it is equal to setting it to an empty object, and it will automatically collect and report some preset events and properties. The effect is equivalent to:<br><br>   ```TypeScript```<br>```   {```<br>```   appLaunch: true, //Report app_launch event, do not report when false```<br>```   appTerminate: true, //Report app_terminate event, not when false, or not when appLaunch is false```<br>```   appError: true, //Report on_error event, do not report when false```<br>```   pageShow: true, //Report predefine_pageview event, do not report when false```<br>```   pageHide: true, //Report predefine_pageview_hide event, not when false, or not when pageShow is false```<br>```   pageShare: true, //Report on_share event, do not report when false```<br>```   pageFavorite: true, //Report on_addtofavorites event, do not report when false```<br>```   click: false, //Do not report bav2b_click incident, only report when true```<br>```   }```<br>```   ```<br>   <br><br>* When set to object value: You can modify the configuration in the auto_report to specify whether a preset event is collected.<br><br>   * When configuring empty objects: default click events are not collected, app_launch, app_terminate and other events are collected;<br><br>   * If you want to modify the configuration, you only need to configure the acquisition switch of the corresponding field in the object value, and other unconfigured fields will remain in the default state.<br><br>      For example, if you want to collect click events, and the collection status of other events remains the default (collection), the configuration example is as follows:<br><br>   ```TypeScript```<br>```   {```<br>```   click: true, //No need to configure other events without modification```<br>```   }```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to capture click events, after turning on the click field switch in the auto_report, you also need to configure the properties to be captured in the subsequent integration code, see <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#932b065c">capture click events</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">See the details of the preset events and properties supported by the Mini Program side <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_Preset_Events_and_Properties">Mini Program Preset Events and Properties</a>.</div><br> |


Example:


* Do not report click events, but report other preset events, set to true or empty object `{}`can be


```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    auto_report: true,
});
$$sdk.send();
```



* To report all preset events, including click events, click needs to be set to true.


```JavaScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    auto_report: {
        click: true,
    },
});
$$sdk.send();
```



* Report most preset events, but not error events, set appError to false, and other events are similarly set


```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    auto_report: {
        click: true,
        appError: false,
    },
});
$$sdk.send();
```


<span id="932b065c"></span>
## **capture click events**

When click is set to true, the SDK will report bav2b_click event (currently only the bindtap type is supported) when components bound to some event functions are clicked, which will collect the contents of the dataset dataset on the component as parameters. Suppose the following components are set with id = "diandian" and data\-hi = "hello"

```HTML
<view id="diandian" data-hi="hello" bindtap="tapMethod">click me</view>
```


When the component is clicked, the reported bav2b_click event and the collected properties are approximately as follows

```TypeScript
{
    event: 'bav2b_click',
    params: {
        path: 'pages/index/index',
        query_id: 'diandian',
        query_hi: 'hello'
    }
}
```


SDK version 2.12.0 + began to support property filtering ability: initialization parameters increase clickIgnoreProperty, type array, valid in the case of click set to true, the function is to filter the corresponding property in the dataset value of the clicked element, such as setting ['abc', 'xxx'], then all clicked elements with abc or xxx on the property will be filtered out, not collected.

Global setting method, example:

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    auto_report: {
        click: true,
        clickIgnoreProperty: ['imgSrc', '...'],
    },
});
$$sdk.send();
```


Single element setup, example

```HTML
<view bindtap="ontest" data-xxx="xxx-value" data-yyy="yyy-value" data-zzz="zzz-value" data-click-ignore-property="xxx,yyy"></view>
```


<span id="5da28458"></span>
## Add custom properties to preset events


* For `app_launch`, `app_terminate`events: After the SDK is initialized, you can listen to the "ExtendAppLaunch" and "ExtendAppTerminate" messages.

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   
   //extended app_launch event parameters
   $$sdk.on($$sdk.SdkHook.ExtendAppLaunch, (params) => {
       params['xxx'] = '我是额外的xxx参数'; //I am extra xxx parameters
       //can be expanded to multiple
   });
   
   //extended app_terminate event parameters
   $$sdk.on($$sdk.SdkHook.ExtendAppTerminate, (params) => {
       params['zzz'] = '我是额外的zzz参数'; //I am extra zzz parameters
       //can be expanded to multiple
   });
   
   $$sdk.send();
   ```
   

* For `predefine_pageview`, `predefine_pageview_hide`Events: Listen to "ExtendPageShow" and "ExtendPageHide" messages in the onLoad method of each page (Page). In order to avoid multiple listening caused by multiple execution of the onLoad of the page, it is best to remove the corresponding listening (off) in onUnload.

   ```TypeScript
   //a certain page
   Page({
       //Other code......
       pageShowHook(params) {
           //First determine whether it is the current page, assuming the current page is pages/index
           if (params.path.indexOf('pages/index') !== -1) {
               params['abc'] = '我是额外的abc参数';
               //can be expanded to multiple
           }
       },
       pageHideHook(params) => {
           //First determine whether it is the current page, assuming the current page is pages/index
           if (params.path.indexOf('pages/index') !== -1) {
               params['def'] = '我是额外的def参数';
               //can be expanded to multiple
           }
       },
       onLoad() {
           //Other code......
           
           //extended predefine_pageview event parameters
           $$sdk.on($$sdk.SdkHook.ExtendPageShow, this.pageShowHook);
           
           //extended predefine_pageview_hide event parameters
           $$sdk.on($$sdk.SdkHook.ExtendPageHide, this.pageHideHook);
       },
       onUnload() {
           //Other code......
           
           //Remove listening for predefine_pageview events
           $$sdk.off($$sdk.SdkHook.ExtendPageShow, this.pageShowHook);
           
           //Remove listening for predefine_pageview_hide events
           $$sdk.off($$sdk.SdkHook.ExtendPageHide, this.pageHideHook);
       },
       
       //Other code......
   });
   ```
   


<span id="19a0bfde"></span>
## Set event public properties

Using the config method, you can set public properties that will be carried on all subsequent event reports.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

//Set event public properties, which will be carried on all subsequent event reports
$$sdk.config({
    city: '南京', //Nanjing
    nick_name: 'vikings',
});
```


In addition, the `2.6.0 +`version of the SDK provides `setHeaderInfo`and `removeHeaderInfo`methods to handle event public properties.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
});
$$sdk.send();

//Set the public property city, the value is Nanjing
$$sdk.setHeaderInfo('city', '南京');

//Remove public property city
$$sdk.removeHeaderInfo('city');
```


SDK internally preset some public property fields, these fields predefined field names, as listed in the following table, some of the fields, SDK will automatically try to obtain after initialization, and other fields need to be set by the business side, such as `nick_name`, `gender`, `avatar_url`These SDK can not be automatically obtained, you need to take the initiative to set.


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


<span id="d346cc4a"></span>
# Mini Program Subcontracting Scenario

<span id="d5f0381a"></span>
## Use in Mini Program Subcontracting

When using the default instance, a preset event plug\-in is included. When the plug\-in exists, the SDK listens to the relevant lifecycle hooks of the Mini Program's App/Page, and the SDK also waits for the relevant lifecycle hooks to fire, such as the App's onLaunch.

In the subcontract, when the SDK is initialized, the app's onLaunch has been triggered, so you need to "tell" the SDK to "skip" and wait for the trigger, and turn on `enable_skip_launch: true`when initializing the configuration.

```TypeScript
//Initialize the SDK in the subcontract
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ...
    enable_skip_launch: true,
});
$$sdk.send();
```


<span id="8016efeb"></span>
# application instance correlation

<span id="d3ad2d12"></span>
## Using multiple instances

To use multiple instances, you need to import the SDK class, the SDK constructor, which is an SDK file located in the ESM directory in the SDK package.

```TypeScript
import SDK from '@datarangers/sdk-mp/esm/sdk';
```


Tip: The following is the default instance of the SDK, not the SDK constructor. Notice that the imported files are different.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
```


Example:

```TypeScript
import SDK from '@datarangers/sdk-mp/esm/sdk';

//use the new operation on the constructor to generate instance 1
$$sdk1 = new SDK();
$$sdk1.init({
    app_id: 1,
    // ...
});
$$sdk1.send();


//use the new operation on the constructor to generate instance 2
$$sdk2 = new SDK();
$$sdk2.init({
    app_id: 2, //app_id cannot be the same as other instances
    // ...
});
$$sdk2.send();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip:</div>



* <div data-tips="true" data-tips-type="tip">The app_id requirements of different instances cannot be the same.</div>


* <div data-tips="true" data-tips-type="tip">At present, only SaaS\-cloud\-native environments and privatized environments support multi\-application capabilities. Before use, you need to contact BytePlus technical support staff to turn on the function switch and bind multiple applications in the DataFinder project. See the end\-to\-end operation guide for multiple applications <a href="https://docs.byteplus.com/docs/DataFinder/Use_Multiple_Apps">Use Multiple Apps</a>.</div>



<span id="d795cda9"></span>
## Custom selection of internal plugins

The instances exported by the SDK by default contain as many plug\-in features as possible. After using the custom selection plug\-in, the built instance will be smaller in size than the default exported instance. If your business wants to customize which plug\-ins to use, consider the following usage options.


1. First import the SDK base class file: esm/base.js

2. Then import the corresponding plugin file as needed: esm/plugin/xxx.js

3. Register the plugin to the SDK base class: Use the usePlugin static method of the SDK class

4. Then instantiate the SDK, followed by initialization settings


```JavaScript
//import the basic class
import BaseSDK from '@datarangers/sdk-mp/esm/base';

//Import required plugins, such as AB test plugins
import Ab from '@datarangers/sdk-mp/esm/plugin/ab';
BaseSDK.usePlugin(Ab);

//Instantiate the SDK
const $$sdk = new BaseSDK();
$$sdk.init({
    //Please change to your own app_id
    app_id: 0,
    enable_ab_test: true，//start ab experiment
});
$$sdk.send();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip:</div>


<div data-tips="true" data-tips-type="tip"><code>Import $$sdk from '@datarangers/sdk-mp'</code>, <code>$$sdk</code>is an instance generated by default.</div>


<div data-tips="true" data-tips-type="tip"><code>Import SDK from '@datarangers/sdk-mp/esm/sdk'</code>, the <code>SDK</code>is a class constructor that contains almost all functions, and the above <code>$$sdk</code>essentially executes <code>new SDK ()</code>.</div>


<div data-tips="true" data-tips-type="tip"><code>Import BaseSDK from '@datarangers/sdk-mp/esm/base'</code>, <code>BaseSDK</code>is also a class constructor, containing the most basic functions, other functions need to cooperate with the corresponding plugin can, plugin needs to use <code>usePlugin</code>registration. Compared with the <code>BaseSDK</code>, the above <code>SDK</code>essentially registers almost most of the plug\-ins by default.</div>


<span id="1efa7842"></span>
## Mini Program Single Platform Usage

The instances exported by the SDK by default are as compatible as possible with the current mainstream Mini Program platforms, such as WeChat, Alipay, Douyin, Baidu, Xiaohongshu, QQ, DingTalk, etc. If the business makes it clear that its Mini Program application will only be released to a certain platform, such as WeChat, you can consider using the following methods to specify which platform's entry file is selected. It is important to note that a single platform entry file contains only basic functionality, and to use more capabilities, you need to actively import and register the corresponding plug\-ins.

```JavaScript
//Import a specific Mini Program platform entry file
import WXSDK from '@datarangers/sdk-mp/esm/wx';

//Import required plugins, such as AB test plugins
import Ab from '@datarangers/sdk-mp/esm/plugin/ab';
WXSDK.usePlugin(Ab);

//Instantiate the SDK
const $$sdk = new WXSDK();
$$sdk.init({
    //Please change to your own app_id
    app_id: 0,
    enable_ab_test: true，//start ab experiment
});
$$sdk.send();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip:</div>


<div data-tips="true" data-tips-type="tip">In the SDK package, there are files such as wx.js, tt.js, dd.js, etc. in the esm directory, which represent a certain platform entrance, wx, tt, dd respectively</div>


<span id="69ad68e1"></span>
# Security compliance related

<span id="1e9d6964"></span>
## Request for encryption

At present, only state\-secret encryption methods are supported.

Encryption relies on the national secret algorithm library and requires businesses to install it themselves.

```Shell
npm install --save miniprogram-sm-crypto
```


To enable national secret encryption in the SDK, the following relevant parameters need to be set:


|**Parameter name** |**Parameter meaning** |**Type** |**Default value** |
|---|---|---|---|
|enable_encrypt |Whether to turn on encryption |boolean |false |
|encrypt_type |encryption type |string<br><br>Enumeration values: 'normal', 'sm' |'normal'<br><br>National secret encryption needs to be set to: 'sm' |
|encrypt_public_key |encrypted public key |string |'04BA9E229380DC0E41E10839B0C52A4763D3EDFE8903F3B8E81395523381E03AA995D295BD4A4088792E4785B224F7837EB4D2C7C05973C7AE8687A35ACAE470A0' |
|encrypt_header |Encrypted country secret header field |string |'gm_sm2' |


Example:

```TypeScript
import SDK from '@datarangers/sdk-mp/esm/sdk';

//use encryption plugin
import EncryptPlugin from '@datarangers/sdk-mp/esm/plugin/encrypt';
SDK.usePlugin(Ab);

//Instantiate the SDK
const $$sdk = new SDK();
$$sdk.init({
    // ...
    
    //These are the national secret encryption parameters
    enable_encrypt: true,
    encrypt_type: 'sm',
    encrypt_public_key: '设置公钥', //Set public key
    encrypt_header: '', //National Secret currently defaults to gm_sm2
});
$$sdk.send();
```


<span id="b3b3d3c9"></span>
# UTM related

<span id="dd314453"></span>
## UTM Tracking

By default, the SDK tries to get utm\-related parameters from applet startup parameters: `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`. If obtained, these parameters are placed in the event public property, and will be carried on all subsequent event reports. The ability is automatically turned on, and the business does not require any processing.

<span id="6fb1e18b"></span>
# Other Scenario Practices

<span id="b36c4ba7"></span>
## Lark widget application practice

Note that in the Lark widget scenario, preset event reporting is not supported (i.e. auto_report parameter setting is invalid). SDK version requirements: 2.9.0 +

```JavaScript
//Import a separate entry class for the Lark widget
import BlockSDK from '@datarangers/sdk-mp/esm/block';

//Import required plugins, such as AB test plugins
import Ab from '@datarangers/sdk-mp/esm/plugin/ab';
BlockSDK.usePlugin(Ab);

//Instantiate the SDK
const $$sdk = new BlockSDK();
$$sdk.init({
    //Please change to your own app_id
    app_id: 0,
    enable_ab_test: true，//start ab experiment
});
$$sdk.send();
```


<span id="34266c0b"></span>
## How to use it in special environments

If the business project for some reason does not support the use of npm packages, or third\-party dependencies, or even does not have a build packaging process, you can consider using the umd module files provided by the SDK.


* Copy the index.umd.js file in the SDK package to the project.


```TypeScript
const $$sdk = require('{{相对路径}}/index.umd.js'); //relative path
$$sdk.init({
    //Please change to your own app_id
    app_id: 0,
    enable_ab_test: true，//start ab experiment
});
$$sdk.send();
```
