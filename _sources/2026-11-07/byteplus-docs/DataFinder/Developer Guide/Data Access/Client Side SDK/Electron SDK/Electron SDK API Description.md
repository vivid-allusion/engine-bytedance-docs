---
title: "Electron SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Electron_SDK_API_Description"
---

This article introduces the main APIs provided by the Fast Application SDK. You can call the corresponding API in combination with the event tracking planning for event tracking.

<span id="b83be19a"></span>
# initialization


* **Function:**  It is to initialize and configure the SDK instance.

* **Definition:**  constructor (configuration: InitialConfig)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |configuration |```TypeScript```<br>```interface InitialConfig {```<br>```  app_id: number;```<br>```  logLevel?: string; //'info' or'error 'or'silent'.```<br>```  channel?: string; //'cn' or 'sg'```<br>```  channel_domain?: string;```<br>```  enable_ab_test?: boolean;```<br>```  ab_channel_domain?: string;```<br>```  // ...```<br>```}```<br> |Yes |The SDK needs to know which application to report to, which DataFinder service address to report to, and which functional modules to enable, which need to be configured during the initialization of the SDK. |
   

   
   |Parameter classification |**Field** |**Field value type** |**Required** |**Field description** |
   |---|---|---|---|---|
   |**basic parameters** |app_id |number |Yes |The application ID is used to identify the business product, that is, to indicate which application's data is collected by the event tracking. After creating an application in the DataFinder console, the application ID of the corresponding application will be automatically generated for you. Please refer to the operation of obtaining the application ID [Step 2: Obtain the APPID](https://docs.byteplus.com/docs/DataFinder/Electron_SDK_Integration#8c5ac3ed). |
   ||logLevel |string |No |Set the log type.<br><br><br>* Info: Outputs all types of logs.<br><br>* Error: Only log of error type is output.<br><br>* Silent (default): No log output. |
   ||channel |string |No |It is used to set the reporting channel for collecting data. Each application can only set a unique channel. Please set the appropriate channel according to the environment type and geographical situation of the DataFinder service you are currently using:<br><br><br>* **Sg:**  If your current environment is an overseas BytePlus environment, you need to modify the channel value to sg.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   ||channel_domain |string |No |To set which service address to report data to the DataFinder:<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload of the private deployment environment and plan the configuration by yourself. If you are unsure of this address, please contact your project manager or customer success manager. |
   |**AB experiment** |enable_ab_test |boolean |No |Set whether you need to enable the A/B experiment function. After setting it to true, the ab experiment function will be enabled. Later, you need to:<br><br><br>* Configure the offload address (ab_channel_domain) for A/B experiments during integration SDK initialization.<br><br>* Use APIs including getVar, getAllVars, etc. to obtain experimental parameters, etc. A/B experiment related API details please see [AB test Modules and APIs](https://docs.byteplus.com/docs/DataFinder/Electron_SDK_API_Description#850e982c). |
   ||ab_channel_domain |string |No |If the A/B experiment is enabled, you need to set the offload address for the A/B experiment.<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://tab.ab.ap\-southeast\-1.volces.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   
   const $$sdk = new SDK({
       app_id: 1,
       channel: 'cn',
           
       //... more configuration parameters
   });
   ```
   


<span id="43b682a2"></span>
# config


* **Function:**  Call config to make some settings for the event, such as setting public properties, setting user_unique_id, etc. It can be called multiple times, and subsequent settings will override the same previous settings.

* **Definition:**  config (configs?: ConfigParams): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |configs |```TypeScript```<br>```interface ConfigParams {```<br>```  user_unique_id?: string or null;```<br>```  [key: string]: any;```<br>```}```<br> |No |You can set event public properties or user dependencies in the config interface.<br><br><br>* Set the event public property: The event public property will be in the header as a common property for all events, see more details on setting [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Electron_SDK_Integration_Scenario_Practice#19a0bfde).<br><br>* Setting user_unique_id: Please refer to [User login status settings](https://docs.byteplus.com/docs/DataFinder/Electron_SDK_Integration_Scenario_Practice#e7ec629e). |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       app_id: 1,
       channel: 'cn',  
       //... more configuration parameters
   });
   
   //Set event public properties, which will be carried on all subsequent event reports
   $$sdk.config({
       city: '南京', //Nanjing
       nick_name: 'vikings',
   });
   
   //Set user_unique_id
   $$sdk.config({
       user_unique_id: 'zhangsan', //At this time user_unique_id as zhangsan
   });
   
   //Set user_unique_id again, it will overwrite
   $$sdk.config({
       user_unique_id: 'lisi', //At this time user_unique_id is lisi
   });
   ```
   


<span id="68e73ad4"></span>
# event


* **Function:**  Use the event method to report custom events.

* **Definition:**  event (name: string, params: Record < string, string or number or boolean or object or Array \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |name |string |Yes |* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDK internal automatic reporting of event names.<br><br>* It is recommended that event names use lower case uniformly. |
   |params |Record < string, string or number or boolean or object or Array \> |Yes |* It is recommended that attributes use lowercase uniformly.<br><br>* Event property values support number, string, array, object, boolean types. When the data collection is dropped into the DataFinder, the data format will be converted. See more instructions [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).<br><br>* Do not re\-nest objects in event attributes, that is, the attribute value does not accept the object type. If the business data is a nested object type, it can be converted to a String by escaping and then reported. Please see [Example 1: How nested JSON type properties are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2).<br><br>* If you want to express the meaning of event property value null, it is recommended to use `"be_null"`, not `"`or `" "`. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       app_id: 1,
       channel: 'cn',  
       //... more configuration parameters
   });
   
   //Call the event method where the business needs it and report the custom event.
   $$sdk.event('some_event', {
       val: '...',
       path: '...',
   });
   ```
   


<span id="850e982c"></span>
# AB test Modules and APIs

This module provides AB test capabilities and provides a series of methods: `getVar`, `getAllVars`, `getAbSdkVersion`.

<span id="ef1f70cb"></span>
## enable module

Using this module, in addition to the common parameters to be configured during SDK initialization, you also need to turn on the module switch of A/B experiment: `enable_ab_test: true`, and configure the offload address (ab_channel_domain field) of A/B experiment.

```TypeScript
import { SDK } from '@datarangers/sdk-electron';
const $$sdk = new SDK({
    app_id: 1,
    channel: 'cn',  
    //... more configuration parameters
    enable_ab_test: true,
    ab_channel_domain: "https://tab.volces.com", 
});
```


<span id="594025b4"></span>
## modular approach

<span id="d817b8bd"></span>
### getVar


* **Function:**  Get the configuration item value corresponding to the experiment in the AB test configuration, and the SDK will collect the corresponding vid (the business generally does not need to directly care about the vid).

* **Definition:**  getVar (name: string, defaultValue: any, callback: (value: any) = \> void): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |name |string |Yes |The key in the experimental configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tip: The business calls the getVar method, and the SDK will report a preset event <code>abtest_exposure</code>when it finds that there is a corresponding key in the experimental configuration.</div><br> |
   |defaultValue |any |Yes |When there is no corresponding key configuration item in the experimental configuration, the method will return the bottom value. |
   |callback |(value: any) =\> void |No |When the experimental configuration item value is obtained, if there is a callback setting, the callback will be executed, and the experimental configuration item value will be used as the callback parameter. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.getVar('color', 'red', (value) => {
       //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
   });
   ```
   


<span id="a8ffb70c"></span>
### getAllVars


* **Function:**  Get all the configuration information of ab experiment.

* **Definition:**  getAllVars (callback: (data: any) = \> void): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |callback |(data: any) =\> void |No |If a callback is set, the callback will be executed, and all the experimental configuration data will be used as the parameters of the callback.<br><br>The experimental configuration data structure is approximately as follows:<br><br>```TypeScript```<br>```{```<br>```    aa: {```<br>```        val: 'aa-value',```<br>```        vid: '11'```<br>```    },```<br>```    test_before_6d: {```<br>```        val: 'test_before_6d-value',```<br>```        vid: '22'```<br>```    },```<br>```    bb: {```<br>```        val: 'bb-value',```<br>```        vid: '33'```<br>```    }```<br>```}```<br> |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.getAllVars((data) => {
       The data value is approximately as follows:
       /*    {      aa: { val: 'aa-value', vid: '11' },      test_before_6d: { val: 'test_before_6d-value', vid: '22' },      bb: { val: 'bb-value', vid: '33' },    }    */
   });
   ```
   


<span id="747c0c72"></span>
### getAbSdkVersion


* **Function:**  Get the exposed experiment, the returned result is the vid of all exposed experiments, connected with commas, format for example: 123,234,678

* **Definition:**  getAbSdkVersion (): string

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |string |VIDs of all exposure experiments, linked with commas, in the format for example: 123,234,678 |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   const vids = $$sdk.getAbSdkVersion();
   //vids value is similar to 123,234,678
   ```
   


<span id="5b92710a"></span>
# User Attributes Module and API

This module provides the ability to set user properties and provides a series of methods: `profileSet`, `profileSetOnce`, `profileUnset`, `profileIncrement`, `profileAppend`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This module is used to set the user attribute data to be collected. If you want to set the user's real\-name identity user_unique_id, you can use the config parameter to set it.</div>


<span id="6c478257"></span>
## modular approach

<span id="78aa3702"></span>
### profileSet


* **Function:**  Overwrite the property field with a new value, set one or more properties at a time, support array type property values.

* **Definition:**  profileSet (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. Overwrite property fields with new values, one or more properties can be set at a time, and array type property values are supported. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.profileSet({
       trade: '篮球', //basketball
       interests: ['篮球', '跑步', '摄影'], //basketball, running, photographing
   });
   ```
   


<span id="cc0d2538"></span>
### profileSetOnce


* **Function:**  According to the property field, it is only set once, and if it already has a value, it will not be updated.

* **Definition:**  profileSetOnce (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. According to the property field, it is set only once. If it already has a value, it will not be updated. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.profileSetOnce({
       trade: '篮球', //basketball
   });
   ```
   


<span id="c17f289c"></span>
### profileUnset


* **Function:**  Delete the value of a property.

* **Definition:**  profileUnset (key: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |Deleted user property value. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.profileUnset('trade');
   ```
   


<span id="76c04d81"></span>
### profileIncrement


* **Function:**  Increases the numeric property by the specified value, which can be a negative number.

* **Definition:**  profileIncrement (params: Record < string, number \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record<string, number\> |Yes |Increased user property value. Increments a numeric property by the specified value, which can be negative. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk. profileIncrement({
       age: 10,
       money: -10000,
   });
   ```
   


<span id="630a3378"></span>
### profileAppend


* **Function:**  When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array.

* **Definition:**  profileAppend (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array. |
   

* **Example:** 

   ```TypeScript
   import { SDK } from '@datarangers/sdk-electron';
   const $$sdk = new SDK({
       // ...
   });
   
   $$sdk.profileAppend({
       trade: '篮球', //basketball
       interests: ['钓鱼'], //fishing
   });
   ```
   


&nbsp;
