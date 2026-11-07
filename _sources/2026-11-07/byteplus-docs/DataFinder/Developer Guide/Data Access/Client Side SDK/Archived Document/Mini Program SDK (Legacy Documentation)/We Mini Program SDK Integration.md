---
title: "We Mini Program SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/We_Mini_Program_SDK_Integration"
---

<span id="_1-集成"></span>
# Step 1 Integration

<span id="_1-1-安装sdk"></span>
## 1.1 Installing the SDK

> Install with npm


```shell
npm install @datarangers/sdk-mp
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


1. Place the initialization of the SDK in a separate file and export the instance


```javascript
//Assume that the separate file is named sdk.js
import SDK from '@dp/sdk-mp/esm/we';

const $$sdk = new SDK();
$$sdk.init({
    app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
});
$$Rangers.config({
    mp_name: 'xyz Mini Program', //Some predefined properties can be set through config
    mp_version: '1.1.1',
});
$$sdk.send();

export default $$sdk;
```



2. Then import the instance in the JavaScript of different pages and customize the report.


```javascript
import React, { useEffect } from 'react';
// ...
import $$sdk from '../sdk';

export default function PageMain() {

  useEffect(() => {
    $$sdk.event('test', {
      haha: 1
    })
  }, []);

  return (
    <div className={css.App}>...</div>
  );
}
```


<span id="_2-2-2-私有化业务"></span>
### 2.2.2 Privatization business

Privatization requires a clear data reporting domain name. If you are unsure of this domain name, please contact your project manager or customer success manager.


1. Place the initialization of the SDK in a separate file and export the instance


```javascript
//Assume that the separate file is named sdk.js
import SDK from '@dp/sdk-mp/esm/we';

const $$sdk = new SDK();
$$sdk.init({
    app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    channel_domain: "{{DOMAIN}}", //Set up a private deployment data upload domain name, if you don't know this address, please contact your project manager or customer success manager
    log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
});
$$Rangers.config({
    mp_name: 'xyz Mini Programni Program', //Some predefined properties can be set through config
    mp_version: '1.1.1',
});
$$sdk.send();

export default $$sdk;
```



2. Then import the instance in the JavaScript of different pages and customize the report.


```javascript
import React, { useEffect } from 'react';
// ...
import $$sdk from '../sdk';

export default function PageMain() {

  useEffect(() => {
    $$sdk.event('test', {
      haha: 1
    })
  }, []);

  return (
    <div className={css.App}>...</div>
  );
}
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
||channel_domain |string |You can customize the reported domain name, which will override the channel settings, usually used in a privatized environment |
|**AB experiment** |enable_ab_test |boolean |After setting true, the ab experiment function will be enabled, including using APIs such as getVar and getAllVars. |
||ab_channel_domain |string |You can customize the ab experimental domain name, which will override the channel settings, usually used in a privatized environment |
||clear_ab_cache_on_user_change |boolean |The default switch user regains the A/B configuration information, and sets the clear_ab_cache_on_user_change configuration item to false if you want to close it. |
|**buffer** |enable_buffer |boolean |After setting true, buffering will be turned on |
||buffer_interval |number |Buffer interval, in milliseconds, the default value is 5000, which means that all events in the buffer will be reported after the interval is reached |
||buffer_number |number |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value |
|**cache** |enable_cache |boolean |After opening, the event of the failed request will be saved to the storage and reported when the user next enters the Mini Program |
|**other** |enable_profile |boolean |After setting true, you can use the profile related api. |


Example

```javascript
//Parameter: InitParams
//return value: void
$$Rangers.init({
    app_id: 1338,
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
|**custom** |custom properties |string/number |When a property is a public property field, the property will have a clear location under the header<br><br>When the property is not a public property field, it will be placed under custrom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


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

* It is recommended that event names and attributes be lowercase

* Event property values accept only number and string types

* Do not nest objects in event properties, that is, the property value does not accept the object type

* If you want to express the meaning of event property value null, it is recommended to use "be_null", not "or"


Example

```javascript
//Parameters: name: string, params: object
//return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```


<span id="_4-使用插件"></span>
# Step 4 Use plugins


* Open AB test


```javascript
import SDK from '@dp/sdk-mp/esm/we';
import AB from '@dp/sdk-mp/esm/plugin/ab';
SDK.usePlugin(AB);

const $$sdk = new SDK();
$$sdk.init({
    app_id: 0000,
    log: true,
    enable_ab_test: true, //start ab experiment
});
$$Rangers.config({
    mp_name: 'xyz Mini Program',
    mp_version: '1.1.1',
});
$$sdk.send();

export default $$sdk;
```



* Enable buffering, caching


```javascript
import SDK from '@dp/sdk-mp/esm/we';
import Compensate from '@dp/sdk-mp/esm/plugin/compensate';
SDK.usePlugin(Compensate);

const $$sdk = new SDK();
$$sdk.init({
    app_id: 0000,
    log: true,
    enable_buffer: true, //turn on buffering
    enable_cache: true, //enable cache
});
$$Rangers.config({
    mp_name: 'xyz Mini Program',
    mp_version: '1.1.1',
});
$$sdk.send();

export default $$sdk;
```
