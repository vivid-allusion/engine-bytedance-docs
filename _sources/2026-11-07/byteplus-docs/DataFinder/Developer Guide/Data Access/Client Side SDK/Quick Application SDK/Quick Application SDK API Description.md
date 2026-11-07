---
title: "Quick Application SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Quick_Application_SDK_API_Description"
---

This article introduces the main APIs provided by the Fast Application SDK. You can call the corresponding API in combination with the event tracking planning for event tracking.

<span id="b83be19a"></span>
# init


* **Function:**  It is to initialize and configure the SDK instance.

* **Definition:**  nit (options: InitParams): void

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |options |```TypeScript```<br>```interface InitParams {```<br>```  app_id: number;```<br>```  log?: boolean;```<br>```  channel?: 'cn' or 'sg';```<br>```  channel_domain?: string;```<br>```  auto_report?: boolean;```<br>```  enable_ab_test?: boolean;```<br>```  // ...```<br>```}```<br> |Yes |The SDK needs to know which application to report to, which DataFinder service address to report to, and which function modules to enable. These need to be configured in the init interface when the SDK is initialized. The parameters and configuration instructions involved in init are shown in the following table. |
   

   
   |Parameter classification |**Field** |**Field value type** |**Required** |**Field description** |
   |---|---|---|---|---|
   |**basic parameters** |app_id |number |Yes |The application ID is used to identify the business product, that is, to indicate which application's data is collected by the event tracking. After creating an application in the DataFinder console, the application ID of the corresponding application will be automatically generated for you. Please refer to the operation of obtaining the application ID [Step 2: Obtain the APPID](https://docs.byteplus.com/docs/DataFinder/Quick_Application_SDK_Integration#8c5ac3ed). |
   ||log |boolean |No |It is used to set whether the log needs to be turned on. When set to true, the console will print debugging information, so that you can verify whether the SDK integration is successful through the log information of the console when integrating the SDK. |
   ||channel |string |No |It is used to set the reporting channel for collecting data. Each application can only set a unique channel. Please set the appropriate channel according to the environment type and geographical situation of the DataFinder service you are currently using:<br><br><br>* **Sg:**  If your current environment is an overseas BytePlus environment, you need to modify the channel value to sg.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you are not sure what type of environment you are currently using, please refer to the <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>documentation to check and confirm.</div><br> |
   ||channel_domain |string |No |To set which service address to report data to the DataFinder:<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload of the private deployment environment and plan the configuration by yourself. If you are unsure of this address, please contact your project manager or customer success manager. |
   |**automatic report** |auto_report |boolean |No |Sets whether the preset event and preset property data provided to you need to be automatically collected (default is false, no collection). |
   |**AB experiment** |enable_ab_test |boolean |No |Set whether you need to enable the A/B experiment function. After setting it to true, the ab experiment function will be enabled. Later, you need to:<br><br><br>* Configure the offload address (ab_channel_domain) for A/B experiments during integration SDK initialization.<br><br>* Use APIs including getVar, getAllVars, etc. to obtain experimental parameters, etc. A/B experiment related API details please see [AB test Modules and APIs](https://docs.byteplus.com/docs/DataFinder/Quick_Application_SDK_API_Description#43c874f6). |
   ||ab_channel_domain |string |No |If the A/B experiment is enabled, you need to set the offload address for the A/B experiment.<br><br><br>* SaaS\-Cloud Native (Overseas: Johor): https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* Privatization:<br><br>   In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager. |
   ||clear_ab_cache_on_user_change |boolean |No |If the A/B experiment is enabled, you can set whether you need to re\-obtain the configuration information of the A/B experiment when switching users. If you want to close it, set the clear_ab_cache_on_user_change configuration item to false, and the default is true. |
   |**buffer**<br><br>(Only supported 2.2.0 and above) |enable_buffer |boolean |No |After setting true, buffering is turned on. |
   ||buffer_interval |number |No |Buffer interval, in milliseconds, the default value is 5000, meaning that all events in the buffer will be reported after the interval is reached. |
   ||buffer_number |number |No |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value. |
   |**cache**<br><br>(Only supported 2.2.0 and above) |enable_cache |boolean |No |After opening, the event of the failed request will be saved to the storage and reported when the user enters the mini\-game next time. |
   |**other** |enable_profile |boolean |No |After setting true, you can use the profile related API, which is mainly used to set the data collection related to user properties, see the details [User Attributes Module and API](https://docs.byteplus.com/docs/DataFinder/Quick_Application_SDK_API_Description#9b071c87). |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-quick';
   
   $$sdk.init({
       app_id: 1,
       channel: 'cn',
       log: true,
           
       //... more configuration parameters
   });
   ```
   


<span id="43b682a2"></span>
# send


* **Function:**  After the init initialization call, the send method needs to be called before the SDK starts reporting events. No events are reported until the send method is called.

* **Definition:**  send (): void

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-quick';
   
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
   |configs |```TypeScript```<br>```interface ConfigParams {```<br>```  user_unique_id?: string or null;```<br>```  [key: string]: any;```<br>```}```<br> |No |You can set event public properties or user dependencies in the config interface.<br><br><br>* Set the event public property: The event public property will be in the header as a common property for all events, see more details on setting [Set event public properties](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#19a0bfde).<br><br>* Setting user_unique_id: Please refer to [user_unique_id related](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#6ff245df). |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-quick';
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
   |params |Record < string, string or number or boolean or object or Array \> |Yes |* It is recommended that attributes use lowercase uniformly.<br><br>* Event property values support number, string, array, object, boolean types. When the data collection is dropped into the DataFinder, the data format will be converted. See more instructions [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification).<br><br>* Do not re\-nest objects in event attributes, that is, the attribute value does not accept the object type. If the business data is a nested object type, it can be converted to a String by escaping and then reported. Please see [Example 1: How nested JSON type properties are reported and used for filtering and grouping](https://docs.byteplus.com/docs/DataFinder/Property_Custom_Grouping_and_Properties#1fafd5b2).<br><br>* If you want to express the meaning of event property value null, it is recommended to use `"be_null"`, not `"`or `" "`. |
   

* **Example:** 

   ```TypeScript
   import $$sdk from '@datarangers/sdk-quick';
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       app_id: 1338,
       channel: 'cn',
       log: true,
       auto_report: true,
       
       //... more configuration parameters
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
# AB test Modules and APIs

This module provides AB test capabilities and provides a range of methods: `getVar`, `getAllVars`, `getAbSdkVersion`, `setExternalAbVersion`.

<span id="ef1f70cb"></span>
## enable module

Using this module, when the SDK is initialized, in addition to the common parameters to be configured in the init interface, the module switch of A/B experiment needs to be turned on: `enable_ab_test: true`, and the shunt address (ab_channel_domain field) of A/B experiment needs to be configured at the same time.

```TypeScript
import $$sdk from '@datarangers/sdk-quick';
$$sdk.init({
    // ...
    enable_ab_test: true,
    ab_channel_domain: "https://tab.volces.com", 
});
$$sdk.send();
```


In addition, it also supports setting whether the configuration information (clear_ab_cache_on_user_change field) of A/B experiment needs to be re\-acquired when switching users. For details, please refer to [init](https://docs.byteplus.com/docs/DataFinder/Android_SDK_API_Description#b83be19a)the A/B experiment section in the interface.

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
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
      });
      $$sdk.send();
      
      $$sdk.getVar('color', 'red', (value) => {
          //When there is a color experiment in the configuration, the value is the value corresponding to the color in the configuration, otherwise the value is red
      });
      ```
      

   * Return to Promise

      ```TypeScript
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
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
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
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
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
      });
      $$sdk.send();
      
      $$sdk.getAllVars().then((data) => { 
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
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
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
      });
      $$sdk.send();
      
      //Manually set additional
      $$sdk.setExternalAbVersion('25,225,2225');
      ```
      

   * Clear additional experimental configurations

      ```TypeScript
      import $$sdk from '@datarangers/sdk-quick';
      $$sdk.init({
          // ...
      });
      $$sdk.send();
      
      //clear the extra
      $$sdk.setExternalAbVersion(null);
      ```
      


<span id="9b071c87"></span>
# User Attributes Module and API

This module provides the ability to set user properties and provides a series of methods: `profileSet`, `profileSetOnce`, `profileUnset`, `profileIncrement`, `profileAppend`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This module is used to set the user attribute data to be collected. If you want to set the user's real\-name identity user_unique_id, you can use the config parameter to set it. See <a href="https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_#bb21600c">Set up a custom user</a>.</div>


<span id="13499d28"></span>
## enable module

With this module, you need to enable the corresponding parameter in the init interface when the SDK initializes the settings: `enable_profile: true`.

```TypeScript
import $$sdk from '@datarangers/sdk-quick';
$$sdk.init({
    // ...
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
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
   import $$sdk from '@datarangers/sdk-quick';
   $$sdk.init({
       // ...
   });
   $$sdk.send();
   
   $$sdk.profileAppend({
       trade: '篮球',//basketball
       interests: ['钓鱼'],//fishing
   });
   ```
   


&nbsp;
