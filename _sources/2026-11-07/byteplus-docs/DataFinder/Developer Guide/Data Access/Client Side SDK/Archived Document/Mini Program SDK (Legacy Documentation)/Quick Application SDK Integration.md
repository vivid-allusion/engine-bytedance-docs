---
title: "Quick Application SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Quick_Application_SDK_Integration_"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The SDK integration documentation has been revised, please check the new documentation: <a href="https://docs.byteplus.com/docs/DataFinder/Quick_Application_SDK_Integration">Quick Application SDK Integration</a>.</div>


<span id="_1-集成"></span>
# Step 1 Integration

<span id="_1-1-安装sdk"></span>
## 1.1 Installing the SDK

> Install with npm


```plain
npm install @datarangers/sdk-quick
```


<span id="_2-初始化"></span>
# 2. Initialization

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-初始化sdk示例"></span>
## 2.2 Initializing the SDK example

<span id="_2-2-1-saas业务"></span>
### 2.2.1 SaaS business

```javascript
//Initialize the SDK on the entry page
// app.ux
<script>
import $$Rangers from '@datarangers/sdk-quick';

export default {
    plugins: [
        $$Rangers,
    ],
    sdk: $$Rangers,
    onCreate() {
        $$Rangers.init({
            app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
            log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
            auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
        });
        
        $$Rangers.config({
            app_name: 'xyz Quick Application', //Some predefined properties can be set through config
            app_version: '1.1.1',
        });
        
        $$Rangers.send();
    },
    // ...
    
}
</script>
 
 
Other pages report events, such as:
// index.ux
export default {
    onShow() {
        this.$app.$def.sdk.event('bind_view_tap', {
            'title': 'chart',
        });
    }
};
```


<span id="_2-2-2-私有化业务"></span>
### 2.2.2 Privatization business

Privatization requires a clear data reporting domain name. If you are unsure of this domain name, please contact your project manager or customer success manager.

```javascript
//Initialize the SDK on the entry page
// app.ux
<script>
import $$Rangers from '@datarangers/sdk-quick';

export default {
    plugins: [
        $$Rangers,
    ],
    sdk: $$Rangers,
    onCreate() {
        $$Rangers.init({
            app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
            channel_domain: "{{DOMAIN}}", //Set up a private deployment data upload domain name, if you don't know this address, please contact your project manager or customer success manager
            log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
            auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
        });
        
        $$Rangers.config({
            app_name: 'xyz Quick Application', //Some predefined properties can be set through config
            app_version: '1.1.1',
        });
        
        $$Rangers.send();
    },
    // ...
    
}
</script>
 
 
Other pages report events, such as:
// index.ux
export default {
    onShow() {
        this.$app.$def.sdk.event('bind_view_tap', {
            'title': 'chart',
        });
    }
};
```


<span id="_2-2-3-saas云原生版本业务"></span>
### 2.2.3 SaaS cloud native version business

```javascript
//Initialize the SDK on the entry page
// app.ux
<script>
import $$Rangers from '@datarangers/sdk-quick';

export default {
    plugins: [
        $$Rangers,
    ],
    sdk: $$Rangers,
    onCreate() {
        $$Rangers.init({
            app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
            channel_domain: "https://gator.volces.com", //Set the data to upload the domain name
            log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
            auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
        });
        
        $$Rangers.config({
            app_name: 'xyz Quick Application', //Some predefined properties can be set through config
            app_version: '1.1.1',
        });
        
        $$Rangers.send();
    },
    // ...
    
}
</script>
 
 
Other pages report events, such as:
// index.ux
export default {
    onShow() {
        this.$app.$def.sdk.event('bind_view_tap', {
            'title': 'chart',
        });
    }
};
```


<span id="_3-api说明"></span>
# 3. API description

<span id="_3-1-init"></span>
## 3.1 init

Supported initialization parameters


| |**Field** |**Field value** |**Field description** |
|---|---|---|---|
|**foundation** |app_id |number |Unique identification of business products |
||log |boolean |After setting true, the console will print debug information |
||channel<br><br>Name: report_channel |Enumeration value:<br><br>sg |The reporting channel corresponds to the built\-in reporting domain name and ab experimental domain name. Each application can only set one channel. Please set the appropriate channel according to the specific situation of the product.<br><br>sg means Singapore<br><br>Built\-in reporting domain name<br><br>sg：https://mcs.tobsnssdk.com<br><br>Built\-in ab experimental domain name<br><br>sg：https://toblog.tobsnssdk.com<br><br>Report the domain name as https://mcs.volceapplog.com<br><br>The ab experimental domain name is https://abtest.volceapplog.com |
||channel_domain |string |You can customize the reporting domain name, which will override the channel settings, usually used in a privatized environment |
|**automatic report** |auto_report |boolean |Set true to automatically report predefined events such as app_launch, app_terminate |
|**AB experiment** |enable_ab_test |boolean |After setting true, the ab experiment function will be enabled, including using APIs such as getVar and getAllVars. |
||ab_channel_domain |string |You can customize the ab experimental domain name, which will override the channel settings, usually used in a privatized environment |
||clear_ab_cache_on_user_change |boolean |The default switch user regains the A/B configuration information, and sets the clear_ab_cache_on_user_change configuration item to false if you want to close it. |
|**buffer**<br><br>(Only supported 2.1.0 and above) |enable_buffer |boolean |After setting true, buffering will be turned on |
||buffer_interval |number |Buffer interval, in milliseconds, the default value is 5000, which means that all events in the buffer will be reported after the interval is reached |
||buffer_number |number |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value |
|**cache**<br><br>(Only supported 2.1.0 and above) |enable_cache |boolean |After opening, the event of the failed request will be saved to the storage and reported when the user next enters the Mini Program<br><br>( **Please note: after opening the cache, the data duplication problem will occur due to the supplementary reporting strategy, but the overall probability is small, so the amount will not be large** ) |
|**other** |enable_profile |boolean |After setting true, you can use the profile related api. |


Example

```javascript
//Parameter: InitParams
//return value: void
$$Rangers.init({
    app_id: 0000,
    log: true,
    auto_report: true,
    enable_ab_test: true,
    clear_ab_cache_on_user_change: true,
    // ...
});
```


<span id="_3-2-config"></span>
## 3.2 config

The config method can be called multiple times, and subsequent settings will overwrite the same property fields as before


| |**Field** |**Type** |**Explain** |**Example** |
|---|---|---|---|---|
|**user** |user_unique_id |string |Use the business's own user id to set user_unique_id |$$Rangers.config({<br><br>user_unique_id: 'zhangsan',<br><br>}); |
|**custom** |Custom properties |string/number |When the property is a public property field, the property will have a clear location under the header<br><br>When the property is not a public property field, it will be placed under custrom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


Example

```javascript
//Parameters: ConfigParams
//return value: void
$$Rangers.config({
    city: '南京', //Nanjing
    custom_name: 'vikings',
    // ...
});
```


<span id="_3-3-send"></span>
## 3.3 send

After the initialization setting is completed, the send method must be called before the SDK is truly initialized, and no data will be reported before.

Example

```javascript
Parameters: None
//return value: void
$$Rangers.send();
```


<span id="_3-4-event"></span>
## 3.4 event

Incident reporting.

Event naming convention:


* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDKs to automatically report event names

* It is recommended to use lowercase for event names and properties

* Event property values accept only number and string types

* Do not nest objects in event properties, i.e. property values do not accept object types

* If you want to express the meaning of the event property value null, it is recommended to use "be_null", not "or"


Example

```javascript
//Parameters: name: string, params: object
//return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```


<span id="_3-5-获取相关信息api"></span>
## 3.5 Access to relevant information API

<span id="_3-5-1-gettoken"></span>
### 3.5.1 getToken

Get the relevant IDs of the SDK, including web_id, user_unique_id, ssid, etc

getToken(callback: (value: Record<string, string | number\>) =\> void): void

getToken(): Promise<Record<string, string | number\>\>

Example

```javascript
//way 1
//Parameter: (value: Record < string, string | number >) = > void
//return value: void
$$Rangers.getToken((value) => {
    //The value is approximately as follows:
    /*{        
        web_id: '1234567',
        user_unique_id: 'abcdefg',
        ssid: 'xxx-yyy-zzz',
        // ...
    }*/
});

//way 2
Parameters: None
//Return value: Promise < Record < string, string | number > >
$$Rangers.getToken().then((value) => {
    //The value is approximately as follows:
    /*
    {
        web_id: '1234567',
        user_unique_id: 'abcdefg',
        ssid: 'xxx-yyy-zzz',
        // ...
    } 
    */
});
```


<span id="_3-5-2-getconfig"></span>
### 3.5.2 getConfig

Get the set public properties, including properties automatically obtained by the SDK, etc

getConfig(key?: string): Record<string, any\>

Example

```javascript
//Parameter: string optional
//Return value: Record < string, any >
const allConfig = $$Rangers.getConfig();
//allConfig values are approximately as follows
/*{    device_brand: 'xxx',    device_model: 'yyy',    // ...    city: 'nanjing',    custom: {        current_name: 'mini',        // ...    }}*/

const deviceBrand = $$Rangers.getConfig('device_brand');
//deviceBrand may have a value or may be undefined
```


<span id="_3-6-ab实验api"></span>
## 3.6 AB test API

> After enable_ab_test needs to be turned on, the following ab\-related methods are effective

>  


<span id="_3-6-1-getallvars"></span>
### 3.6.1 getAllVars

Get all the configuration information of ab experiment

getAllVars(callback: (value: any) =\> void): void

getAllVars(): Promise

Example

```javascript
//way 1
//Parameter: (value: any) = > void
//return value: void
$$Rangers.getAllVars((value) => {
    //The value is approximately as follows:
    /*
    {      
       aa: { val: 'aa-value', vid: '11' },
      test_before_6d: { val: 'test_before_6d-value', vid: '22' },
      bb: { val: 'bb-value', vid: '33' },
    }
    */
});

//way 2
Parameters: None
//Return value: Promise < any >
$$Rangers.getAllVars().then((value) => { 
    //The value is approximately as follows:
    /*
    {
      aa: { val: 'aa-value', vid: '11' },
      test_before_6d: { val: 'test_before_6d-value', vid: '22' },
      bb: { val: 'bb-value', vid: '33' }, 
    }    
    */ 
});
```


<span id="_3-6-2-getvar"></span>
### 3.6.2 getVar

Get the value corresponding to the experiment in the ab experiment configuration

getVar(name: string, defaultValue: any, callback: (value: any) =\> void): void

getVar(name: string, defaultValue: any): Promise

Example

```javascript
//way 1
//Parameters: string, any, (value: any) = > void
//return value: void
$$Rangers.getVar('color', 'red', (value) => {
    //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
});

//way 2
Parameters: string, any
//Return value: Promise < any >
$$Rangers.getVar('color', 'red').then((value) => { 
    //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
});
```


<span id="_3-7-profile相关api"></span>
## 3.7 Profile related API

> User property settings, you need to open enable_profile, the following profile\-related methods are valid

>  


<span id="_3-7-1-profileset"></span>
### 3.7.1 profileSet

Overwrite the property field with a new value, one or more properties can be set at a time, and array type property values are supported

profileSet(params: Record<string, string | number | Array\>): void

Example

```javascript
//Parameters: Record < string, string | number | Array < string > >
//return value: void
$$Rangers.profileSet({
    trade: '篮球', //basketball
    interests: ['篮球', '跑步', '摄影'], //basketball, running, photographing
});
```


<span id="_3-7-2-profilesetonce"></span>
### 3.7.2 profileSetOnce

According to the property field, it is set only once. If it already has a value, it will not be updated.

profileSetOnce(params: Record<string, string | number | Array\>): void

Example

```javascript
//Parameters: Record < string, string | number | Array < string > >
//return value: void
$$Rangers.profileSetOnce({
    trade: '篮球', //basketball
});
```


<span id="_3-7-3-profileunset"></span>
### 3.7.3 profileUnset

Delete the value of a property

profileUnset(key: string): void

Example

```javascript
//Parameter: string
//return value: void
$$Rangers.profileUnset('trade');
```


<span id="_3-7-4-profileincrement"></span>
### 3.7.4 profileIncrement

Increments a numeric property by the specified value, which can be negative

profileIncrement(params: Record<string, number\>): void

Example

```javascript
//Parameters: Record < string, number >
//return value: void
$$Rangers.profileIncrement({
    age: 10,
    money: -10000,
});
```


<span id="_3-7-5-profileappend"></span>
### 3.7.5 profileAppend

When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array

profileAppend(params: Record<string, string | number | Array\>): void

Example

```javascript
//Parameters: Record < string, string | number | Array < string > >
//return value: void
$$Rangers.profileAppend({
    trade: '篮球', //basketball
    interests: ['钓鱼'], //fishing
});
```


<span id="f5de54f1"></span>
# 4. Specific uses of some platforms

<span id="6f50f17d"></span>
## 4.1 Huawei Quick Application

Huawei Express App does not support the ability of "Framework Front\-end Plugin" (for details, please refer to the "Framework Front\-end Plugin" section in " [this document ](https://doc.quickapp.cn/framework/script.html)"), that is, the use of plugin settings in app.ux is invalid.

If you want to collect preset events, you need to use the following methods:


> 1. DataFinder SDK Version Requirements 2.3.0 +

> 2. And listen to the application display in the quick application. The minPlatformVersion configuration in the manifest .json of the quick application needs to be 1065 and above to trigger.


First initialize the SDK in the app.ux entry file and wrap the exported object using the SDK's instance method `mixinApp`.

```XML
<script>
// app.ux
import $$Rangers from '@datarangers/sdk-quick';
$$Rangers.init({
    app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
    auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
});

$$Rangers.config({
    app_name: 'xyz Quick Application', //Some predefined properties can be set through config
    app_version: '1.1.1',
});

$$Rangers.send();

export default $$Rangers.mixinApp({
    sdk: $$Rangers,
    onCreate() {
        // ...
    },
    // ...
    
});
</script>
```


Then in the page, the export object of the page needs to be wrapped to collect the access and exit events of the page. The packaging process is as follows:

```XML
<script>
// xxx.ux
export default getApp().$$Rangers.mixinPage({
    // ...
    // ...
    // ...
});
</script>
```


Manually reporting events on the page is still the same

```XML
<script>
// xxx.ux
export default getApp().$$Rangers.mixinPage({
    // ...
    onShow() {
        this.$app.$def.sdk.event('bind_view_tap', {
            'title': 'chart',
        });
    }
});
</script>
```
