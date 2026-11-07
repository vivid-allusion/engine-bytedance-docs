---
title: "WeChat Mini Program SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/WeChat_Mini_Program_SDK_Integration"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Mini Program SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration">Mini Program SDK Integration</a></div>


<span id="_1-集成"></span>
# Step 1 Integration

<span id="_1-1-安装sdk"></span>
## 1.1 Installing the SDK

> Install using npm.


```shell
# 2.14.0 is the current newest version
npm install @datarangers/sdk-mp
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The WeChat Mini Program main package is limited to 2MB. When the SDK package is large, it can be imported in the following two ways:</div>



* <div data-tips="true" data-tips-type="tip">When uploading, choose not to upload non\-dependent files.</div>


* <div data-tips="true" data-tips-type="tip">The index.js file can also be used normally when taken out alone. It should be noted that the disadvantage of this use is that multiple instances are not supported.</div>



<span id="_1-2-域名配置准备"></span>
## 1.2 Obtain the reporting address and configure the Mini Program whitelist

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type, and add the data reporting address to the "request legal domain name" in the background of the Mini Program. If the reporting address is set incorrectly, you will not be able to report and query the data normally in the future.

<span id="1063a202"></span>
### Get the data reporting address

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="a4dcc123"></span>
#### SaaS\-cloud\-native


|End type |SaaS\-cloud native<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Mini Program |* https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* To add a whitelist to the Mini Program: https://gator.uba.ap\-southeast\-1.bytepluses.com |* `channel: 'sg'`<br><br>* To add a whitelist to the Mini Program: https://mcs.tobsnssdk.com |


<span id="3b7c1e89"></span>
#### Privatized environment

In the private deployment scenario, you need to obtain the data upload address that you plan and configure when deploying the private environment, and add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="b1136ab7"></span>
### Configure Mini Program Whitelist

For configuration in "Mini Program Background \- Development \- Development Settings \- Server Domain Name", please refer to the corresponding official documentation of the Mini Program, such as the [WeChat Mini Program documentation](https://developers.weixin.qq.com/miniprogram/en/dev/framework/ability/network.html).

<span id="_2-初始化"></span>
# 2. Initialization

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.

Before starting the integration, you first need to have an application in the group. Before integrating the SDK, you need to obtain the appid information of the corresponding application.

<span id="_2-2-初始化sdk示例"></span>
## 2.2 Initializing the SDK example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the initialization example, <code>import $$Rangers from '@datarangers/sdk-mp';</code>is a singleton export. Except for some special loading mechanisms of the framework itself, it is usually the same instance for multiple imports.</div>


<span id="_2-3-引入调试工具-devtools组件-可选"></span>
## 2.3 Introducing Debugging Tools \- DevTools Component (Optional)

`DevTools`is a component that assists developers or testers in the Debug environment to verify in\-app event tracking and troubleshoot SDK access issues. For detailed access documentation, please refer to: [Mini Program event tracking power builder ](https://www.volcengine.com/docs/76880/1033616).

<span id="_3-api说明"></span>
# 3. API description

<span id="_3-1-init"></span>
## 3.1 init

Init is used to set the switch parameters of the SDK function module. The supported initialization parameters are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS cloud native version or privatization V4.4.0 or above, DataFinder supports SDK settings through server level distribution, including reporting timing, full event tracking switch, etc. . The following is the initialization configuration of the Mini Program SDK during initialization, and you can also adjust the configuration later in the DataFinder console.</div>



| |**Field** |**Field value** |**Field description** |
|---|---|---|---|
|**Foundation** |app_id |number |Unique identification of business products |
||log |boolean |After setting true, the console will print debug information |
||channel<br><br>Name: report_channel |Enumeration value:<br><br>cn、sg |The reporting channel corresponds to the built\-in reporting domain name and ab experimental domain name. Each application can only set one channel. Please set the appropriate channel according to the specific situation of the product.<br><br><br>* Cn: Indicates domestic (default value), at this time:<br><br>   * Built\-in data reporting domain name: See the section Obtaining reporting addresses, above.<br><br>   * Built\-in ab experimental shunt domain name: https://abtest.volceapplog.com .<br><br>* Sg: represents Singapore, at this time:<br><br>   * Built\-in data reporting domain name: See the section Obtaining reporting addresses, above.<br><br>   * Built\-in ab experimental shunt domain name: https://toblog.tobsnssdk.com . |
||channel_domain |string |You can customize the reported domain name, which will override the channel settings, usually used in a privatized environment |
|**automatic report** |auto_report |boolean |Set true to automatically report predefined events such as app_launch, app_terminate, predefine_pageview, on_share |
|**AB experiment** |enable_ab_test |boolean |After setting true, the ab experiment function will be enabled, including using APIs such as getVar and getAllVars. |
||ab_channel_domain |string |You can customize the ab experimental domain name, which will override the channel settings, usually used in a privatized environment |
||clear_ab_cache_on_user_change |boolean |The default switch user retrieves the A/B configuration information, and sets the clear_ab_cache_on_user_change configuration item to false if you want to close it. |
|**buffer**<br><br>(Only supported 2.5.0 and above) |enable_buffer |boolean |After setting true, buffering will be turned on |
||buffer_interval |number |Buffer interval, in milliseconds, the default value is 5000, which means that all events in the buffer will be reported after the interval is reached |
||buffer_number |number |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value |
|**cache**<br><br>(Only supported 2.5.0 and above) |enable_cache |boolean |After opening, the event of the failed request will be saved to the storage and reported when the user next enters the Mini Program<br><br>( **Please note: after opening the cache, the data duplication problem will occur due to the supplementary reporting strategy, but the overall probability is small, so the amount will not be large** ) |
|**other** |enable_profile |boolean |After setting true, you can use the profile related api. |
||enable_filter_crawler |boolean |After setting true, events will no longer be reported in the crawler scene (scene: 1129) |
||enable_custom_webid |boolean |First, open enable_custom_webid when initializing, and then set web_id through config. Only after setting web_id will the initialization be completed. The value of web_id must be a number or a string type with all numbers.<br><br>$$Rangers.init({<br><br>enable_custom_webid: true,<br><br>});<br><br>$$Rangers.config({<br><br>web_id: '9876543210',<br><br>}); |


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

The config method is used to set custom fields related to the event, which can be called multiple times. Later settings will overwrite the same property fields as before.


| |**Field** |**Type** |**Explain** |**Example** |
|---|---|---|---|---|
|**user** |user_unique_id |string |Use the business's own user id to set user_unique_id |$$Rangers.config({<br><br>user_unique_id: 'zhangsan',<br><br>}); |
|**custom** |custom properties |string/number |When a property is a public property field, the property will have a clear location under the header<br><br>When a property is not a public property field, it will be placed under custom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


Example:

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

Example:

```javascript
Parameters: None
//return value: void
$$Rangers.send();
```


<span id="_3-4-event"></span>
## 3.4 event

For event reporting, see the event naming specification [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).


* If you want to express the meaning of event property value null, it is recommended to use "be_null", not "or".


Example:

```javascript
//Parameters: name: string, params: object
//return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```
