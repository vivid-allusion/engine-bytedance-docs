---
title: "RedNote Mini Program SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/RedNote_Mini_Program_SDK_Integration"
---

<span id="18809a3b"></span>
# Step 1 Integration

**2.12.0 version starts to support Xiaohongshu Mini Program**

<span id="a296419b"></span>
## 1.1 Installing the SDK

> Install using npm.


```shell
npm install @datarangers/sdk-mp
```


<span id="92e28126"></span>
## 1.2 Domain name configuration preparation

> Configure in "Mini Program Background \- Development \- Development Settings \- Server Domain Name", for details, please refer to the corresponding official documentation of the Mini Program.


* **SaaS business** : Add https://mcs.[tobsnssdk.com](https://mcs.tobsnssdk.com/) to the "request legal domain" in the background of the Mini Program.

* **Privatization business** : Add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you don't know this domain name, please contact your project manager or customer success manager.

* **SaaS cloud native business** : Add https://gator.volces.com to the "request legal domain" in the background of the Mini Program.


<span id="08706e41"></span>
## 1.3 Old version upgrade

Please note that if it is a SaaS business, when upgrading the SDK to the latest version (2.x.x version), you need to add https://mcs.[tobsnssdk.com](https://mcs.tobsnssdk.com/) to the "request legal domain name" in the background of the Mini Program, and the added https://mcs.ctobsnssdk.com should not be removed immediately.

<span id="0113b897"></span>
# 2. Initialization

<span id="986793a9"></span>
## 2.1 Get the appid.

Before starting the integration, you first need to have an application in the group. Before integrating the SDK, you need to obtain the appid information of the corresponding application.


* In the SaaS\-cloud native scenario, you can view your appid in "Project Center" \- \> "Project Management" \- \> "Project Details" \- \> "Details" of the access application \- \> "Application ID", see for details [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ab998769481435b836292947ba52372~tplv-goo7wpa0wc-image.image) </span>


<span id="977789f7"></span>
## 2.2 Initializing the SDK example

<span id="1254e6a7"></span>
### 2.2.1 SaaS \- Cloud Native Business

```javascript
// Initialize SDK on the entry page
// app.js
import $$Rangers from '@datarangers/sdk-mp';

$$Rangers.init({
    app_id: 0000, // Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    channel_domain: "https://gator.volces.com", // set data report domain‘
    log: true, // After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
    auto_report: true, // Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
});
$$Rangers.config({
    mp_name: 'xyz Mini Program', // Some predefined properties can be set through config
    mp_version: '1.1.1',
});
$$Rangers.send();

App({
    onLaunch: function () {
        this.$$Rangers = $$Rangers;
    
        // If you want to set the user ID, such as using open_id to identify the user, you can set the value to user_unique_id after obtaining the open_id
        this.$$Rangers.config({
            user_unique_id: 'acquired open_id', //can be open_id, can also be union_id and other business sense can be used to identify the user uniqueness value
        });

        // Call the event method to report a specific event
        this.$$Rangers.event('test_event', {
            from: 'launch', // Supports arbitrary properties, values support numbers, strings, etc
        });
    }
});
 
// Other pages report events, such as:
// pages/index/index.js
Page({
    onLoad() {
        getApp().$$Rangers.event('bind_view_tap', {
            'title': 'chart',
        });
    }
});
```


<span id="9e51ab7d"></span>
### 2.2.2 Privatization business

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
});
$$Rangers.config({
    mp_name: 'xyz Mini Program', //Some predefined properties can be set through config
    mp_version: '1.1.1',
});
$$Rangers.send();

App({
    onLaunch: function () {
        this.$$Rangers = $$Rangers;
    
        //If you want to set the user ID, such as using open_id to identify the user, you can set the value to user_unique_id after obtaining the open_id
        this.$$Rangers.config({
            user_unique_id: 'acquired open_id', //can be open_id, can also be union_id and other business sense can be used to identify the user uniqueness value
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


<span id="c6c273f0"></span>
## 2.3 Introducing Debugging Tools \- DevTools Component (Optional)

`DevTools`is a component that assists developers or testers in the Debug environment to verify in\-app event tracking and troubleshoot SDK access issues. For detailed access documentation, please refer to: [Mini Program event tracking power builder ](https://www.volcengine.com/docs/76880/1033616).

<span id="665a78d7"></span>
# 3. API description

<span id="ba9d2061"></span>
## 3.1 init

The supported initialization parameters are as follows:


| |**Field** |**Field value** |**Field description** |
|---|---|---|---|
|**foundation** |app_id |number |Unique identification of business products |
||log |boolean |After setting true, the console will print debug information |
||channel<br><br>Name: report_channel |Enumeration value:<br><br>sg |The reporting channel corresponds to the built\-in reporting domain name and ab experimental domain name. Each application can only set one channel. Please set the appropriate channel according to the specific situation of the product.<br><br>sg means Singapore<br><br>Built\-in reporting domain name<br><br>sg：https://mcs.tobsnssdk.com<br><br>Built\-in ab experimental domain name<br><br>sg：https://toblog.tobsnssdk.com<br><br>Report the domain name as https://mcs.volceapplog.com<br><br>The ab experimental domain name is https://abtest.volceapplog.com |
||channel_domain |string |You can customize the reported domain name, which will override the channel settings, usually used in a privatized environment |
|**automatic report** |auto_report |boolean |Set true to automatically report predefined events such as app_launch, app_terminate, predefine_pageview, on_share |
|**AB experiment** |enable_ab_test |boolean |After setting true, the ab experiment function will be enabled, including using APIs such as getVar and getAllVars. |
||ab_channel_domain |string |You can customize the ab experimental domain name, which will override the channel settings, usually used in a privatized environment |
||clear_ab_cache_on_user_change |boolean |The default switch user regains the A/B configuration information, and sets the clear_ab_cache_on_user_change configuration item to false if you want to close it. |
|**buffer**<br><br>(Only supported 2.5.0 and above) |enable_buffer |boolean |After setting true, buffering will be turned on |
||buffer_interval |number |Buffer interval, in milliseconds, the default value is 5000, which means that all events in the buffer will be reported after the interval is reached |
||buffer_number |number |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value |
|**cache**<br><br>(Only supported 2.5.0 and above) |enable_cache |boolean |After opening, the event of the failed request will be saved to the storage and reported when the user next enters the Mini Program<br><br>( **Please note: after opening the cache, the data duplication problem will occur due to the supplementary reporting strategy, but the overall probability is small, so the amount will not be large** ) |
|**other** |enable_profile |boolean |After setting true, you can use the profile related api. |
||enable_filter_crawler |boolean |After setting true, no more events will be reported in the crawler scene (scene: 1129) |
||enable_custom_webid |boolean |First, open enable_custom_webid when initializing, and then set web_id through config. Only after setting web_id will the initialization be completed. The value of web_id must be a number or a string type with all numbers.<br><br>$$Rangers.init({<br><br>enable_custom_webid: true,<br><br>});<br><br>$$Rangers.config({<br><br>web_id: '9876543210',<br><br>}); |


Example

```javascript
// parameter: InitParams
// return value: void
$$Rangers.init({
    app_id: 1338,
    log: true,
    auto_report: true,
    enable_ab_test: true,
    clear_ab_cache_on_user_change: true,
    // ...
});
```


<span id="fbbdae94"></span>
## 3.2 config

The config method can be called multiple times, and later settings override the same property fields as before.


| |**Field** |**Type** |**Explain** |**Example** |
|---|---|---|---|---|
|**user** |user_unique_id |string |Use the business's own user id to set user_unique_id |$$Rangers.config({<br><br>user_unique_id: 'zhangsan',<br><br>}); |
|**custom** |custom properties |string/number |When a property is a public property field, the property will have a clear location under the header<br><br>When a property is not a public property field, it will be placed under custom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


Example:

```javascript
// parameter: ConfigParams
// return value: void
$$Rangers.config({
    city: '南京', //Nanjing
    custom_name: 'vikings',
    // ...
});
```


<span id="6b186839"></span>
## 3.3 send

After the initialization setting is completed, the send method must be called before the SDK is truly initialized, and no data will be reported before.

Example:

```javascript
// parameter: null
// return value: void
$$Rangers.send();
```


<span id="61b7b103"></span>
## 3.4 event

Incident reporting.

Event naming convention:


* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDK internal automatic reporting of event names.

* It is recommended that event names and properties be lowercase.

* Event property values accept only number and string types.

* Do not re\-nest object in event properties, that is, the property value does not accept the object type.

* If you want to express the meaning of event property value null, it is recommended to use "be_null", not "or".


Example:

```javascript
// parameter: name: string, params: object
// return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```
