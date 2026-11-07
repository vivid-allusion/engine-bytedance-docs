---
title: "Mini Program SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Mini_Program_SDK_API_Description"
---

This article introduces the main API provided by Mini Program. You can call the corresponding API in combination with event tracking planning for event tracking.

<span id="b83be19a"></span>
# init


* **Function:**  It is to initialize and configure the SDK instance.

* **Definition:**  init (options: InitParams): void

* **Parameters:** 

   
   |Parameter name |type |Required |Explain |
   |---|---|---|---|
   |options |Options can set multiple parameters of init.<br><br>```TypeScript```<br>```interface InitParams {```<br>```  app_id: number;```<br>```  log?: boolean;```<br>```  channel?: 'cn'; //'cn' or'sg'```<br>```  channel_domain?: string;```<br>```  auto_report?: boolean; //boolean or Object```<br>```  enable_ab_test?: boolean;```<br>```  // ...```<br>```}```<br> |Yes |The SDK needs to know which application to report to, which DataFinder service address to report to, and which function modules to enable. These need to be configured in the init interface when the SDK is initialized. The parameters and configuration instructions involved in init are shown in the following table. |
   

   
   |Parameter classification |**Field** |**Field value type** |**Required** |**Field description** |
   |---|---|---|---|---|
   |**basic parameters** |app_id |number |Yes |The application ID is used to identify the business product, that is, to indicate which application's data is collected by the event tracking. After creating an application in the DataFinder console, the application ID of the corresponding application will be automatically generated for you. Please refer to the operation of obtaining the application ID [Step 2: Obtain the APPID](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration#8c5ac3ed). |
   ||log |boolean |No |It is used to set whether the log needs to be turned on. When set to true, the console will print debugging information, so that you can verify whether the SDK integration is successful through the log information of the console when integrating the SDK. |
   ||channel |string |No |It is used to set the reporting channel for collecting data. Each application can only set a unique channel. Please set the appropriate channel according to the environment type and geographical situation of the DataFinder service you are currently using:<br><br><br>* **Sg:**  If your current environment is an overseas BytePlus environment, you need to modify the channel value to sg.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   ||channel_domain |string |No |To set which service address to report data to the DataFinder:<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address that you plan and configure when deploying the private environment, and add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you are unsure of this address, please contact your project manager or customer success manager.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">channel_domain after the configuration is complete, you will also need to configure the above address in the Mini Program whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   |**automatic report** |auto_report |boolean/Object |No |Sets whether the preset event and preset property data provided to you need to be automatically collected (default is false, no collection). Currently supports setting the value of the auto_report to true/false or the value of the specific object (choose one of the two):<br><br><br>* True/false: When set to true, it is equal to setting it to an empty object, and it will automatically collect and report some preset events and properties. The effect is equivalent to:<br><br>   ```TypeScript```<br>```   {```<br>```       appLaunch: true, //Report app_launch event, do not report when false```<br>```       appTerminate: true, //Report app_terminate event, not when false, or not when appLaunch is false```<br>```       appError: true, //Report on_error event, do not report when false```<br>```       pageShow: true, //Report predefine_pageview event, do not report when false```<br>```       pageHide: true, //Report predefine_pageview_hide event, not when false, or not when pageShow is false```<br>```       pageShare: true, //Report on_share event, do not report when false```<br>```       pageFavorite: true, //Report on_addtofavorites event, do not report when false```<br>```       pageTabItemTap: true, //report on_tabbartap event, do not report when false```<br>```       click: false, //Do not report bav2b_click incident, only report when true```<br>```   }```<br>```   ```<br>   <br><br>* When set to object value: You can modify the configuration in the auto_report to specify whether a preset event is collected.<br><br>   * When configuring empty objects: default click events are not collected, app_launch, app_terminate and other events are collected;<br><br>   * If you want to modify the configuration, you only need to configure the acquisition switch of the corresponding field in the object value, and other unconfigured fields will remain in the default state.<br><br>      For example, if you want to turn off appError and pageShare, and keep the acquisition state of other events as the default (acquisition), the configuration example is as follows:<br><br>   ```TypeScript```<br>```   auto_report: {```<br>```       appError: false,```<br>```       pageFavorite: false,```<br>```       //No need to configure other events without modification```<br>```   }```<br>```   ```<br>   <br><br>   For example, if you want to collect click events, and the collection status of other events remains the default (collection), the configuration example is as follows:<br><br>   ```TypeScript```<br>```   auto_report: {```<br>```       click: true, //No need to configure other events without modification```<br>```   }```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to capture click events, after turning on the click field switch in the auto_report, you also need to configure the properties to be captured in the subsequent integration code, see <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#932b065c">capture click events</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">See the details of the preset events and properties supported by the Mini Program side <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_Preset_Events_and_Properties">Mini Program Preset Events and Properties</a>.</div><br> |
   |**AB experiment** |enable_ab_test |boolean |No |Set whether you need to enable the A/B experiment function. After setting it to true, the ab experiment function will be enabled. Later, you need to:<br><br><br>* Configure the offload address (ab_channel_domain) for A/B experiments during integration SDK initialization.<br><br>* Use APIs including getVar, getAllVars, etc. to obtain experimental parameters, etc. A/B experiment related API details please see [AB test Modules and APIs](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#e15ecfb8). |
   ||ab_channel_domain |string |No |If the A/B experiment is enabled, you need to set the offload address for the A/B experiment.<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://tab.ab.ap\-southeast\-1.volces.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address that you plan and configure when deploying the private environment, and add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you are unsure of this address, please contact your project manager or customer success manager.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ab_channel_domain after the configuration is complete, you will also need to configure the above address in the Mini Program whitelist.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   ||clear_ab_cache_on_user_change |boolean |No |If the A/B experiment is enabled, you can set whether you need to re\-obtain the configuration information of the A/B experiment when switching users. If you want to close it, set the clear_ab_cache_on_user_change configuration item to false, and the default is true. |
   |**buffer**<br><br>(Only supported 2.5.0 and above) |enable_buffer |boolean |No |After setting true, buffering is turned on.<br><br>See the data collection reporting process on the Mini Program side [Reference: SDK core runtime flow](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration#bff9c28d). |
   ||buffer_interval |number |No |Buffer interval, in milliseconds, the default value is 5000, meaning that all events in the buffer will be reported after the interval is reached. |
   ||buffer_number |number |No |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value. |
   |**cache**<br><br>(Only supported 2.5.0 and above) |enable_cache |boolean |No |After opening, the event of the failed request is stored in the storage and reported the next time the user enters the Mini Program.<br><br><br>* Version 2.5.0~ 2.1.4.2 , the default value of this parameter is false, to use this function, you need to explicitly set the parameter value to true<br><br>* Starting from version 2.14.3, the default value of this parameter is true, and the function can be used automatically without setting |
   |**other** |enable_profile |boolean |No |After setting true, you can use the profile related API, which is mainly used to set the data collection related to user properties, see the details [User Attributes Module and API](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#9b071c87). |
   ||enable_filter_crawler |boolean |No |Set whether to collect data in the crawler scenario:<br><br><br>* Set to true: According to the judgment result of the Mini Program platform on the event\-triggered scene, if it is a crawler scene (for example, the scene value scene: 1129 returned by the WeChat Mini Program), the reported event will no longer be collected; if it is not a crawler scene, the data will be collected normally.<br><br>* Set to false: Whether it is a crawler scene or not, collect data normally. |
   ||enable_custom_webid |boolean |No |Whether to set a custom web_id. If you do not want to use the SDK automatically generated web_id, you want to report custom web_id, you need to open the enable_custom_webid during initialization, and then set the web_id through the config interface, only after setting the web_id will be initialized, web_id value requirements must be a number or a string type full of numbers. Please see for details [Custom web_id](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#cb231913). |
   ||element exposure |The Mini Program SDK supports the acquisition of element exposure event data. You can turn on the element exposure switch during initialization and configure the acquisition data of element exposure. For details, please refer to [Element Exposure Module and API](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#6590c90e). |||
   ||Security compliance |The Mini Program SDK supports the use of national secret encryption to encrypt requests. Encryption (enable_encrypt, encrypt_type, etc.) is achieved by setting encryption\-related fields during initialization. Please refer to [Request for encryption](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#1e9d6964). |||
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   
   $$sdk.init({
       app_id: 1,
       channel: 'cn',
       log: true,
       auto_report: true,
       
       //... more configuration parameters
   });
   ```
   


<span id="43b682a2"></span>
# send


* **Function:**  After the init initialization call, the send method needs to be called before the SDK starts reporting events. No events are reported until the send method is called.

* **Definition:**  send (): void

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   
   $$sdk.init({
       // ...
   });
   
   $$sdk.send();
   ```
   


<span id="7fccc7c0"></span>
# config


* **Function:**  Call config to make some settings for the event, such as setting public properties, setting user_unique_id, etc. It can be called multiple times, and subsequent settings will override the same previous settings.

* **Definition:**  config (configs?: ConfigParams): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |configs |```TypeScript```<br>```interface ConfigParams {```<br>```  user_unique_id?: string or null;```<br>```  user_unique_id_type?: string;```<br>```  [key: string]: any;```<br>```}```<br> |No |You can set event public properties or user dependencies in the config interface.<br><br><br>* Set the event public property: The event public property will be in the header as a common property for all events, see more details on setting [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#19a0bfde).<br><br>* Setting user_unique_id: Please refer to [user_unique_id related](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#6ff245df). |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
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


* **Function:**  Use the event method to report custom events. This method supports single event mode and batch event mode reporting.


<span id="9f12605b"></span>
## single event


* **Definition:**  event (name: string, params: Record < string, string or number or boolean or object or Array \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |name |string |Yes |* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDK internal automatic reporting of event names.<br><br>* It is recommended that event names use lower case uniformly. |
   |params |Record < string, string or number or boolean or object or Array \> |Yes |* It is recommended that attributes use lowercase uniformly.<br><br>* Event property values support number, string, array, object, boolean types. When the data collection is dropped into the DataFinder, the data format will be converted. See more instructions [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).<br><br>* Do not re\-nest objects in event attributes, that is, the attribute value does not accept the object type. If the business data is a nested object type, it can be converted to a String by escaping and then reported. Please see [Example 1: How nested JSON type properties are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2).<br><br>* If there are no properties, you can leave the params parameter unpassed. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
   //Call the event method where the business needs it and report the custom event.
   $$sdk.event('some_event', {
       val: '...',
       path: '...',
   });
   ```
   


<span id="850e982c"></span>
## batch event


* **Logical description:**  Accept an array to report batch events. When the number of array items is greater than 30, the SDK will automatically report multiple times, that is, a single batch can report up to 30 events.

* **Definition:**  event (events: Array < {event: string; params: Record < string, string or number or boolean or object or Array \>; local_time_ms?: number;} \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |events |```TypeScript```<br>```Array<{```<br>```    event: string;```<br>```    params: Record<string, string or number or boolean or object or Array>;```<br>```    local_time_ms?: number;```<br>```}>```<br> |Yes |* The requirements for events and params are the same as those for reporting a single event.<br><br>* local_time_ms value is timestamp, and the default SDK will supplement this field for each event. If you actively set this field, the value you set will prevail. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       app_id: 1338,
       channel: 'cn',
       log: true,
       auto_report: true,
       
       //...... more configuration parameters
   });
   $$sdk.send();
   
   //Call the event method where the business needs it and report the custom event.
   $$sdk.event([
       {
           event: 'event1', 
           params: {param: '1'},
       },
       {
           event: 'event2', 
           params: {param2: '2', param2Other: '2-other'},
           local_time_ms: 1580892161098,
       },
       // ...
       {
           event: 'event30', 
           params: {param30: '30', param30Other: '30-other'},
           local_time_ms: 1580892214276,
       },
   ]);
   ```
   


<span id="43c874f6"></span>
# setUserUniqueID


* **Function:**  Set the user_unique_id, which can be called multiple times, and the subsequent settings will overwrite the same settings as before. Version requirements 2.6.0 +.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Using the setUserUniqueID interface to set user_unique_id the same effect as using the config interface to set user_unique_id, essentially the setUserUniqueID interface is also the config method called internally.   </div>
   

* **Definition:**  setUserUniqueID (uuid: string or null): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |uuid |String or null |Yes |For more user_unique_id scenarios, see [user_unique_id related](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#6ff245df). |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   //Set user_unique_id immediately after user login
   $$sdk.setUserUniqueID('{{uuid}}'); //Values can be considered as attributes that can be associated with the user
   
   //Clear user_unique_id immediately after user logs out
   $$sdk.setUserUniqueID('');
   ```
   


<span id="a608d39d"></span>
# setHeaderInfo


* **Function:**  Set the event public property, which can be called multiple times, and the subsequent setting will overwrite the same setting item before. Version requirements 2.6.0 +.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Setting public properties using the setHeaderInfo interface has the same effect as setting public properties using the config interface. In essence, the setHeaderInfo interface is also a config method called internally.   </div>
   

* **Definition:**  setHeaderInfo (key: string, value: any): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |Public property name. See more configuration practices for event public properties [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#19a0bfde). |
   |value |any |Yes |Public attribute value. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk.setHeaderInfo('nick_name', 'zhangsan');
   ```
   


<span id="73b75e64"></span>
# removeHeaderInfo


* **Role:**  Removes event public properties. Version requirements 2.6.0 +.

* **Definition:**  removeHeaderInfo (key: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |Public property name. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
   $$sdk.removeHeaderInfo('nick_name');
   ```
   


<span id="a9dfd686"></span>
# disableSDK


* **Function:**  Suspend SDK reporting events. After calling this method, the SDK will be suspended and no events will be reported in the future. Version requirements 2.11.0 +.

* **Definition:**  disableSDK (): void

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
   $$sdk.disableSDK();
   ```
   


<span id="42d29839"></span>
# enableSDK


* **Function:**  Cancel the suspension of SDK reporting, generally after calling the disableSDK and intending to cancel the suspension, that is, restart the SDK reporting, and the reporting event will be resumed later. Version requirements 2.11.0 +.

* **Definition:**  enableSDK (): void

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
   //The $$sdk.disableSDK () was called earlier;
   $$sdk.enableSDK();
   ```
   


<span id="e15ecfb8"></span>
# AB test Modules and APIs

This module provides AB test capabilities and provides a range of methods: `getVar`, `getAllVars`, `getAbSdkVersion`, `setExternalAbVersion`.

<span id="ef1f70cb"></span>
## enable module

Using this module, when the SDK is initialized, in addition to the common parameters to be configured in the init interface, the module switch of A/B experiment needs to be turned on: `enable_ab_test: true`, and the shunt address (ab_channel_domain field) of A/B experiment needs to be configured at the same time.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ...
    enable_ab_test: true,
    ab_channel_domain: "https://tab.volces.com", 
});
$$sdk.send();
```


In addition, it also supports setting whether the configuration information (clear_ab_cache_on_user_change field) of A/B experiment needs to be re\-acquired when switching users. For details, please refer to [init](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_API_Description#b83be19a)the A/B experiment section in the interface.

<span id="594025b4"></span>
## modular approach

<span id="d817b8bd"></span>
### getVar


* **Function:**  Get the configuration item value corresponding to the experiment in the AB test configuration, and the SDK will collect the corresponding vid (the business generally does not need to directly care about the vid).

* **Definition:** 

   getVar(name: string, defaultValue: any, callback: (value: any) =\> void): void

   getVar(name: string, defaultValue: any): Promise

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |name |string |Yes |The key in the experimental configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tip: The business calls the getVar method, and the SDK will report a preset event <code>abtest_exposure</code>when it finds that there is a corresponding key in the experimental configuration.</div><br> |
   |defaultValue |any |Yes |When there is no corresponding key configuration item in the experimental configuration, the method will return the bottom value. |
   |callback |(value: any) =\> void |No |When the experimental configuration item value is obtained, if there is a callback setting, the callback will be executed, and the experimental configuration item value will be used as the callback parameter. |
   

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |Promise |When the callback parameter is not set, the method returns a promise. |
   

* **Example:** 

   * Use the callback function approach.

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      $$sdk.getVar('color', 'red', (value) => {
          //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
      });
      ```
      

   * Return to Promise

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      $$sdk.getVar('color', 'red').then((value) => { 
          //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
      });
      ```
      


<span id="a8ffb70c"></span>
### getAllVars


* **Function:**  Get all the configuration information of ab experiment.

* **Definition:** 

   getAllVars(callback: (data: any) =\> void): void

   getAllVars(): Promise

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |callback |(data: any) =\> void |No |If a callback is set, the callback will be executed, and all the experimental configuration data will be used as the parameters of the callback.<br><br>The experimental configuration data structure is approximately as follows:<br><br>```TypeScript```<br>```{```<br>```    aa: {```<br>```        val: 'aa-value',```<br>```        vid: '11'```<br>```    },```<br>```    test_before_6d: {```<br>```        val: 'test_before_6d-value',```<br>```        vid: '22'```<br>```    },```<br>```    bb: {```<br>```        val: 'bb-value',```<br>```        vid: '33'```<br>```    }```<br>```}```<br> |
   

* **Return value:** 

   
   |Type |Explain |
   |---|---|
   |Promise |When no callback parameter is set, the method returns a promise. |
   

* **Example:** 

   * Use callback function method

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      $$sdk.getAllVars((data) => {
          //The data value is approximately as follows:
          /*
          {
             aa: { val: 'aa-value', vid: '11' },
            test_before_6d: { val: 'test_before_6d-value', vid: '22' },
            bb: { val: 'bb-value', vid: '33' },    
          }
          */
      });
      ```
      

   * Return to Promise

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      $$sdk.getAllVars().then((data) => { 
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
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   const vids = $$sdk.getAbSdkVersion();
   //vids value is similar to 123,234,678
   ```
   


<span id="483aa0a6"></span>
### setExternalAbVersion


* **Role:**  Manually set up additional AB test configurations.

* **Definition:**  setExternalAbVersion (vids: string or null): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |vids |String or null |Yes |Format requirements for vids: Concatenate vids values with commas, something like '123,234,678'.<br><br><br>* Additional experimental configuration vids set up in this way are merged into the vids obtained through getVar processing.<br><br>* When called multiple times, the last set of additional experimental configuration vids overrides the previous ones.<br><br>* When null is set, the SDK clears the set of additional experimental configuration vids without affecting the vids obtained through getVar processing. |
   

* **Example:** 

   * Set up additional experimental configurations

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      //Manually set additional
      $$sdk.setExternalAbVersion('25,225,2225');
      ```
      

   * Clear additional experimental configurations

      ```TypeScript
      import $$sdk from '@datarangers/sdk-mp';
      $$sdk.init({
          // ......
      });
      $$sdk.send();
      
      //clear the extra
      $$sdk.setExternalAbVersion(null);
      ```
      


<span id="9b071c87"></span>
# User Attributes Module and API

This module provides the ability to set user properties and provides a series of methods: `profileSet`, `profileSetOnce`, `profileUnset`, `profileIncrement`, `profileAppend`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This module is used to set the user attribute data to be collected. If you want to set the user's real\-name identity user_unique_id, you can use the config parameter to set it. See <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration#bb21600c">Set up a custom user</a>.</div>


<span id="13499d28"></span>
## enable module

With this module, you need to enable the corresponding parameter in the init interface when the SDK initializes the settings: `enable_profile: true`.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
$$sdk.init({
    // ......
    enable_profile: true,
});
$$sdk.send();
```


<span id="e1364485"></span>
## modular approach

<span id="ee27c8d3"></span>
### profileSet


* **Function:**  Overwrite the property field with a new value, set one or more properties at a time, support array type property values.

* **Definition:**  profileSet (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. Overwrite property fields with new values, one or more properties can be set at a time, and array type property values are supported. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk.profileSet({
       trade: '篮球', //basketball
       interests: ['篮球', '跑步', '摄影'], //basketball, running, photographing
   });
   ```
   


<span id="5730c462"></span>
### profileSetOnce


* **Function:**  According to the property field, it is only set once, and if it already has a value, it will not be updated.

* **Definition:**  profileSetOnce (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. According to the property field, it is set only once. If it already has a value, it will not be updated. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk.profileSetOnce({
       trade: '篮球', //basketball
   });
   ```
   


<span id="da1a75e1"></span>
### profileUnset


* **Function:**  Delete the value of a property.

* **Definition:**  profileUnset (key: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |string |Yes |Deleted user property value. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk.profileUnset('trade');
   ```
   


<span id="519a82f2"></span>
### profileIncrement


* **Function:**  Increases the numeric property by the specified value, which can be a negative number.

* **Definition:**  profileIncrement (params: Record < string, number \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record<string, number\> |Yes |Increased user property value. Increments a numeric property by the specified value, which can be negative. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk. profileIncrement({
       age: 10,
       money: -10000,
   });
   ```
   


<span id="3e37c5e5"></span>
### profileAppend


* **Function:**  When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array.

* **Definition:**  profileAppend (params: Record < string, string or number or Array < string \> \>): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |params |Record < string, string or number or Array < string \> \> |Yes |Set user property value. When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-mp';
   $$sdk.init({
       // ......
   });
   $$sdk.send();
   
   $$sdk.profileAppend({
       trade: '篮球', //basketball
       interests: ['钓鱼'],  //fishing
   });
   ```
   


<span id="6590c90e"></span>
# Element Exposure Module and API

<span id="b9cbd328"></span>
## enable module

The required SDK version 2.13.0 +. To use this module, you first need to import the element exposure plug\-in and register it, and then turn on the relevant parameters during SDK initialization.


1. Import the exposure plug\-in and use the SDK instance to integrate the exposure plug\-in;

2. When initializing the SDK, use `enable_exposure`to explicitly open exposure acquisition, and then configure `exposure_config`parameters to specify exposure parameters.


```TypeScript
import $$sdk from '@datarangers/sdk-mp';

//Import element exposure plugin and register
import Exposure from '@datarangers/sdk-mp/esm/plugin/exposure';
$$sdk.usePlugin(Exposure);

$$sdk.init({
    // ...
    
    //You need to open enable_exposure first, and then configure exposure_config
    enable_exposure: true,
    exposure_config: {
        tags: ['logsdk-exposure'],
        rate: 0.5,
        duration: 3,
        bis: false,
    },
    //If it is developed using the taro framework, you need to explicitly set the framework.
    framework: {
        taro: Taro,
    }
});
$$sdk.send();
```


<span id="cac3efe8"></span>
## configuration parameter description


1. enable_exposure: Whether to open exposure capture, the default value is false, set to true to open exposure capture.

2. exposure_config: Exposure acquisition specific parameter configuration items, including class_tags, rate, stay_duration, need_repeat specific reference table.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">exposure_config set as a global parameter in init can be overridden by exposure parameters added separately on the component and configuration parameters for exposure via the API.   </div>
   

   ```TypeScript
   $$sdk.init({
       // ......
       
       //You need to open enable_exposure first, and then configure exposure_config
       enable_exposure: true,
       exposure_config: {
           tags: ['logsdk-exposure'],
           rate: 0.5,
           duration: 3,
           bis: false,
       },
   });
   ```
   

   
   |Configuration item |Type |Default value |Explain |
   |---|---|---|---|
   |tags |array |['logsdk\-exposure'] |The exposure tag is the value of the class attribute of the component. |
   |rate |number |0 |The visible scale of the exposure, with values ranging from 0 to 1. 0 means that exposure is satisfied as long as it is exposed; 1 means that the component needs to be fully exposed to satisfy exposure. |
   |duration |number |0 |Duration of effective stay in seconds. |
   |bis |boolean |false |Whether to allow repeated exposure acquisition. |
   

3. Framework: If you are developing with the taro framework, you need to explicitly set the framework.

   ```TypeScript
   $$sdk.init({
       // ......
       
       //If it is developed using the taro framework, you need to explicitly set the framework.
       framework: {
           taro: Taro,
       },
   });
   ```
   

   
   |Configuration item |Type |Default value |Explain |
   |---|---|---|---|
   |framework |Object |null |Applications developed using the Taro framework need to set this property when enabling exposure capture, with a fixed value of.<br><br>```TypeScript```<br>```{```<br>```  taro: Taro```<br>```}```<br> |
   


<span id="a8bacbf0"></span>
## Configure Exposure Component

Meet these three scenarios: the `configuration of the global component unified scene`, `the configuration of the page component unified scene`, and the `component adds the exposure parameter scene separately`.

<span id="8d0dac8e"></span>
### Configuration Unified Scenario for Global Components

Add a "class" tag to any page component, the value of "class" is one of the tags in the exposure_config configured at init time, and the default value is "logsdk\-exposure" if no tags are configured. Then set the required attribute data\-logsdk\-exposure\-event\-name= "Exposure Event Name", and the event name itself meets the name requirements for reporting the event.


* default value

   ```JavaScript
   $$sdk.init({
       // ......
       
       enable_exposure: true,
       exposure_config: {
           rate: 0.5,
           duration: 3,
           bis: false,
       },
   });
   ```
   

   ```XML
   <view class="logsdk-exposure" data-logsdk-exposure-event-name="woshibaoguang"></view>
   ```
   

* custom value

   ```JavaScript
   $$sdk.init({
       // ......
       
       enable_exposure: true,
       exposure_config: {
           tags: ['my-app-exposure-tag'],
           rate: 0.5,
           duration: 3,
           bis: false,
       },
   });
   ```
   

   ```HTML
   <view class="my-app-exposure-tag"  data-logsdk-exposure-event-name="woshibaoguang"></view>
   <!--use logsdk-exposure is still OK, it is the default value-->
   <view class="logsdk-exposure"  data-logsdk-exposure-event-name="woshibaoguang"></view>
   ```
   


<span id="11e66b9b"></span>
### Configuration Unified Scenario for Page Components

Add the "class" tag on the component in the page, set the attribute "data\-logsdk\-exposure\-option" configuration parameters

```JavaScript
Page({
  data: {
    option: {
      exposure_config: {
        rate: 0,
        duration: 0,
        bis: false
      },
      event_name: "exposure_name",
      event_properties: {
        haha: "属性haha的值", //value of property haha
        enen: "属性enen的值", //value of property enen
        // ...
      }
    }
  }
});
```


```XML
<view class="logsdk-exposure" data-logsdk-exposure-option="{{option}}"></view>
```



|Configuration item |Type |Default value |Explain |
|---|---|---|---|
|exposure_config |Object |No |Same as the initial exposure configuration. |
|event_name |string |Yes |The name of the exposure event must be set before it will be reported. |
|event_properties |Object |No |Custom properties of the exposure event, the content of the properties is the same as the custom event properties |


<span id="611be8df"></span>
### Separate addition of exposure parameters for components

Add a "class" tag to the component on the page and set the specific exposure parameter properties

```XML
<view 
    class="logsdk-exposure" 
    data-logsdk-exposure-config-rate="0"
    data-logsdk-exposure-config-duration="3"
    data-logsdk-exposure-config-bis="true"
    data-logsdk-exposure-event-name="test"
    data-logsdk-exposure-event-property-haha="haha"
 ></view>
```



|Configuration item |Type |Required |Describe |
|---|---|---|---|
|data\-logsdk\-exposure\-config\-rate |number |No |exposure ratio |
|data\-logsdk\-exposure\-config\-duration |number |No |exposure dwell time |
|data\-logsdk\-exposure\-config\-bis |boolean |No |Is the exposure repeated? |
|data\-logsdk\-exposure\-event\-name |string |Yes |The name of the exposure event must be set before it will be reported. |
|data\-logsdk\-exposure\-event\-property\-\* |string |No |Custom properties of the exposure event, the content of the properties is the same as the custom event properties |


<span id="54216d1e"></span>
## element exposure using API

<span id="69dd73b6"></span>
### addObserver


* **Function:**  Exposure monitor for the specified element.

* **Definition:**  addObserver (tag: string, config?: OuterRawConfig, listener?: Listener): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |tag |string |Yes |Exposure markers, component classes |
   |config |OuterRawConfig<br><br>```TypeScript```<br>```type OuterRawConfig = {```<br>```  rate: number;```<br>```  duration: number;```<br>```  bis: boolean;```<br>```  component?: any;```<br>```};```<br> |No |same exposure acquisition configuration |
   |listener |Listener<br><br>```TypeScript```<br>```type Listener = {```<br>```  canExposure?: (tag: string, props: Record<string, any>) => boolean;```<br>```  doneExposure?: (tag: string, props: Record<string, any>) => void;```<br>```};```<br> |No |Callback when the current exposure component triggers an exposure event<br><br><br>* canExpose: Whether to trigger the exposure event callback<br><br>* doneExpose: Exposure callback triggered |
   

* **Example:** 

   ```JavaScript
   $$sdk.addObserver(
       '组件class值',  //value of component class
       {
           rate: 0.5,
           duration: 0,
           bis: false
       },
       {
           canExposure: function(tag, properties){
               //tag is the exposure tag of the currently exposed component
               //properties to expose the component's information and the component's exposure custom properties
               //returns true if an exposure event is triggered
               //return false if no exposure event is triggered
               return true
           },
           doneExpose: function(tag, properties){
               //tag is the exposure tag of the currently exposed component
               //properties to expose the component's information and the component's exposure custom properties
           }
       }
   );
   ```
   


<span id="e35d39e5"></span>
### removebserver


* **Function:**  emoves exposure listening for the specified element.

* **Definition:**  removebserver (tag: string): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |tag |string |Yes |Exposure markers, component classes |
   

* **Example:** 

   ```JavaScript
   $$sdk.removebserver('组件class值'); //value of component class
   ```
   


<span id="29a0c254"></span>
## Recommended usage in some scenarios

<span id="5f2e110a"></span>
### Used in the Taro framework

First, create a rangers.js (or .ts) file that encapsulates the initialization code for the SDK.

```TypeScript
import $$sdk from '@datarangers/sdk-mp';
import Exposure from '@datarangers/sdk-mp/esm/plugin/exposure';
$$sdk.usePlugin(Exposure);

$$sdk.init({
    // ...
    
    //You need to open enable_exposure first, and then configure exposure_config
    enable_exposure: true,
    exposure_config: {
        tags: ['logsdk-exposure'],
        rate: 0.5,
        duration: 3,
        bis: false,
    },
    //If it is developed using the taro framework, you need to explicitly set the framework.
    framework: {
        taro: Taro,
    }
});
$$sdk.send();

export default $$sdk;
```


Then import rangers.js (or .ts) into the app.js (or .ts) entry file.

```Go
//Try to introduce it at the front of the entrance
import $$sdk from './rangers';

// ...
```


Then introduce rangers.js (or .ts) into the page.js (or .ts) page, and use the relevant methods of the SDK instance.

```TypeScript
// page.js
import React, { useEffect } from 'react';
import { View } from '@tarojs/components';
import Taro, { useDidShow, useDidHide } from '@tarojs/taro';
import $$sdk from './rangers';

function Index() {
  // You can use all React Hooks.
  useEffect(() => {});

  //corresponding to onShow
  useDidShow(() => {
      //It needs to be used in nextTick, after Taro is rendered
      Taro.nextTick(() => {
          $$sdk.addObserver('my-exposure-tag', {
            rate: 0.5,
            duration: 0,
            bis: false
          });
      });
  });

  //corresponding to onHide
  useDidHide(() => {
      $$sdk.removObserver('my-exposure-tag');
  });

  return <View className="index my-exposure-tag" data-logsdk-exposure-event-name="event-test" />
}

export default Index;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: If the project itself supports the use of globalData (taroGlobalData in React, setGlobalDataPlugin in Vue, see the Taro official document https://docs.taro.zone/docs/come\-from\-miniapp/), then you can mount the SDK instance ($$sdk object) to globalData, so that you can get the SDK instance ($$sdk object) through globalData in other pages, there is no need to use the above method to create rangers.js file, which will be more convenient.</div>


<span id="97fcdcff"></span>
### Dynamic rendering scene

```XML
<!-- page.wxml -->
<view class="logsdk-exposure" wx:for="{{items}}" wx:key="index" data-logsdk-exposure-event-name="{{item.event}}">
  {{index}}: {{item.event}}
</view>
```


```TypeScript
// page.js
import $$sdk from './rangers';

Page({
    data(){
        return {
            items: [],
        };
    },
    onShow(){
        //Simulate interface request to obtain data
        fetch().then((datas) => {
            /* The data is roughly as follows
            datas = [{event: 'test1'}, {event: 'test2'}]
            */
            this.setData({items: datas}, () => {
                $$sdk.addObserver('logsdk-exposure', {
                    rate: 0.5,
                    duration: 0,
                    bis: false
                });
            });
        });
    },
});
```
