---
title: "Android SDK Event Tracking and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Android_SDK_Event_Tracking_and_Properties"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Android SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration">Android SDK Integration</a></div>


> Before reporting events and properties, please read the [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification)introduction.


<span id="_1-用户与用户属性"></span>
# 1. Users and user properties

<span id="_1-1-登录态变化调用"></span>
## 1.1 Login state change call

<span id="_1-1-1-账户登录"></span>
### 1.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in. 6.13.0 + version supports calling before initializing AppLog to set the uuid of the logged in user.

```java
//Set the ID of your account system and ensure its uniqueness
//6.13.0 + version supports this method to be called before initializing AppLog
AppLog.setUserUniqueID("your_USER_UNIQUE_ID");
```


(6.13.0 + version is not recommended) Set the uuid through this method, and the setting will only take effect on the first cold start. Since AppLog.setUserUniqueID is supported before initialization in 6.13.0 +, it is no longer recommended to use this method to set uuid. It is recommended to use AppLog.setUserUniqueID uniformly.

```java
//set uuid during initialization
//6.13.0 + version do not use this method
config.setUserUniqueId("your_USER_UNIQUE_ID");
```


<span id="_1-1-2-账户登出"></span>
### 1.1.2 Account Logout

Called when the account is logged out.

```java
//Set uuid to null when logging out
AppLog.setUserUniqueID(null);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Do not miswrite <code>("null")</code>or <code>(")</code>, otherwise it will affect the binding relationship between data and users.</div>


<span id="_1-2-设置用户属性"></span>
## 1.2 Setting user properties

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Child process calls are not supported. Please ensure that the calling process is the main process when calling.</div>


<span id="_1-2-1-profileset"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```java
//Example: Set the user property, the property name is key, and the property value is value
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", "value");
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileSet(paramsObj);
```


<span id="_1-2-2-profilesetonce"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they are not set, and if they do not exist, they are created. Suitable for first\-time relevant user properties, such as first visit time, etc.

```java
//Example: Set a user property with the property name key_once and the property value value_once
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key_once", "value_once");
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileSetOnce(paramsObj);
```


<span id="_1-2-3-profileincrement"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```java
//Example: Set the user property, the property name is key, and the property value is 1
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", 1);
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileIncrement(paramsObj);
```


<span id="_1-2-4-profileappend"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```java
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", "value_append");
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileAppend(paramsObj);
```


<span id="_1-2-5-profileunset"></span>
### 1.2.5 profileUnset

Delete the user's properties.

```java
//Example: Delete a user property named key
AppLog.profileUnset("key");
```


<span id="_2-事件与事件属性"></span>
# 2. Events and event properties

<span id="_2-1-上报代码埋点"></span>
## 2.1 Reporting code event tracking

The user behavior log takes the form of **event event + property params** . Events generally correspond to multiple properties, or only events have no properties. Code event tracking schemes are typically designed by data analysts or product operations.


* Code event tracking that only reports events, as follows:

   ```java
   //Example: Report an event that does not contain properties
   //placed in the corresponding position of business logic
   AppLog.onEventV3("event");
   ```
   

* Code event tracking for reporting events and corresponding properties, as follows:

   ```java
   //Example: Report an event, which contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //a property of type int, the property name key_int, the property value is 10
   //placed in the corresponding position of business logic
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key_string", "value_string");
       paramsObj.put("key_int", 10);
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.onEventV3("event", paramsObj);
   ```
   


<span id="_2-2-事件公共属性"></span>
## 2.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="_2-2-1-设置公共属性"></span>
### 2.2.1 set public properties

```java
 /* * Example: Set a custom public property with the property name key_public and the property value value_public * Please note about customizing "public properties": * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail; * 2. High-frequency modifications are not recommended, such as once per second. */
 Map<String,Object> headerMap = new HashMap<String, Object>();
 headerMap.put("key_public", "value_public");
 AppLog.setHeaderInfo((HashMap<String, Object>)headerMap);
```


<span id="_2-2-2-移除公共属性"></span>
### 2.2.2 Remove Public Property

```java
//Example: Remove a public property named key_public
AppLog.removeHeaderInfo("key_public");

//Remove all set public properties by passing null
AppLog.setHeaderInfo(null);
```


<span id="_3-获取平台id与通知"></span>
# 3. Obtain platform ID and notification

<span id="_3-1-获取平台生成id"></span>
## 3.1 Obtaining the platform generated ID

```java
//It is recommended to refer to "How to obtain parameters such as DID" for the correct acquisition time.
String ssid = AppLog.getSsid(); //Get SSID
String did = AppLog.getDid(); //get device bddid
```


<span id="_3-2-获取sdk版本号"></span>
## 3.2 Obtaining the SDK version number

```java
//The SDK version number format is X.X.X
String sdkVersion = AppLog.getSdkVersion();
```


<span id="_3-3-切换账号设置数据发送方式"></span>
## 3.3 Switch account settings to send data

When switching accounts, switch the data transmission method at the same time.

```java
AppLog.setPrivacyMode(true); //The default is false, and it is true after setting. If it is not collected, it will not be reported.
```


<span id="_3-4-获取各类通知"></span>
## 3.4 Obtain various notifications

The SDK provides the addDataObserver method to obtain various notifications, which is recommended to be placed in the Application.

```java
public static void addDataObserver(IDataObserver listener)
```


Set the callbacks for iid, ssid, did, abconfig to load from local and server successfully.

The parameters of the IDataObserver interface method are described as follows:

```java
import com.bytedance.applog.IDataObserver;

AppLog.addDataObserver(new com.bytedance.applog.IDataObserver() {

    /**     * Local ID data loading result notification     *@param did device id     *@param iid install id     *@param ssid ssid     */
    @Override
    public void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid) {

    }

    /**     Notify registration results and ID changes     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param oldDid original device id     *@param newDid server returns new device id     *@param oldIid original install id     *@param newIid server returns the new install id     *@param oldSsid original ssid     *@param newSsid server returns new ssid     */
    @Override
    public void onRemoteIdGet(boolean changed, @Nullable String oldDid, @NonNull String newDid, @NonNull String oldIid, @NonNull String newIid, @NonNull String oldSsid, @NonNull String newSsid) {

    }

    /**     * Config pulls data, and notifies changes compared with local data     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param Config server returns new config content     */
    @Override
    public void onRemoteConfigGet(boolean changed, @Nullable JSONObject config) {

    }

    /**     * The server pulls AbConfig data and notifies changes compared with local data     Only the main process will be called     *@param Changed whether it is different from the local cache     *@param abConfig server returns new abConfig content     */
    @Override
    public void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject abConfig) {
        Log.i("---测试---返回全部进组信息",""+ jsonObject.toString());
    }

    /**     * Vid change notification     */
    @Override
    public void onAbVidsChange(@NonNull String vids, @NonNull String extVids) {

    }
});
```


<span id="_4-默认公共属性字段"></span>
# 4. Default public property fields

The SDK collects the following information by default and as a public user property, it can be grouped and filtered in the growth analysis (DataFinder).


|Field name |Field type |Parameter name |
|---|---|---|
|os |string |Equipment system, the corresponding product properties are os_name. |
|os_version |string |operating system version |
|app_version |string |App version |
|app_version_minor |string |Secondary version number, App four\-digit version number, requires initialization calls such as: config.setVersionMinor (1.2.3) |
|channel |string |Download channel (can be overwritten after setting), the corresponding product property is app_channel. |
|device_model |string |Equipment model |
|region |string |Operating system region |
|language |string |system language |
|sdk_version |string |SDK version |
|timezone |int |Time Zone |
|timezone_offset |int |Time zone offset, corresponding to the in\-product property tz_offset. |
|timezone_name |string |Time Zone Name |
|sim_region |string |SIM card region |
|carrier |string |operator |
|resolution |string |resolution |
|device_brand |string |Equipment brand |
|access |string |network type |


<span id="_5-view曝光事件采集"></span>
# 5. View Exposure Event Capture

> This feature is supported after 6.10.1 +, and it is recommended to use Exposure to initialize the SDK early, such as in Application.


Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>6.16.0 the following versions, only one exposure event will be triggered after entering the page, and the Views in the 6.16.0 and above pages will trigger multiple exposures according to different behaviors.</strong></div>


<div data-tips="true" data-tips-type="tip">Can be distinguished by the $exposure_type property inside the exposure event:</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 0 first exposure</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 3 duplicate exposures</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 6 Exposure returned from other pages</div>


<div data-tips="true" data-tips-type="tip">$exposure_type: 7 Background Return Exposure</div>


<div data-tips="true" data-tips-type="tip">If you want the effect to be exposed only once before 6.16.0 later versions, you can filter the first exposure by $exposure_type == 0 in the new exposure callback.</div>


In the initialization configuration, the exposure configuration switch can be turned on. How to turn it on:

```java
config.setExposureEnabled(true);
```


After enabling the configuration, add exposure monitoring to the View that needs to be exposed. Example code:


<Tabs>
<Tab zoneid="mqtVuPhxMM" title="6.16.2 及以上">
<TabTitle>6.16.2 及以上</TabTitle>

```Java
View banner = findViewById(R.id.banner);
// Optional, custom Export event property
JSONObject properties = new JSONObject();
properties.put("custom_key", "custom_value");
// Optional, default is "$bav2b_exposure"
String eventName = "custom_exposure";

// After 6.16.2, exposure supports detection by area and time, and provides exposure callback for event processing
// Optional, exposure configuration, effective exposure area, visual debugging switch, effective exposure time, and exposure event callback
// Effective exposure area: the ratio of the effective exposure of the View display area is set to 0 by default, with a value of 0-1
// Visual debugging switch: default is set to false, do not enable online. After enabling, the exposed View will have a red background border added for debugging purposes
// Effective exposure time: View time for effective exposure, default is 0, unit: ms
// Exposure event callback: When triggering an exposure event, a callback will be carried with the relevant properties of the current exposure event, which can be custom added and support filtering
ViewExposureConfig config = new ViewExposureConfig(0.5F, false, 200, viewExposureParam -> {
      try {
            // Add custom properties in callbacks
            viewExposureParam.getExposureParam().put("key", "value");
            // print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            // Filter the current exposure event when an exception occurs
            return false;
      }
      // true retain exposure events
    return true;
});
ViewExposureData<ViewExposureConfig> callbackData = new ViewExposureData<>(eventName, null, config);

// start monitoring View exposure event, field viewExposureManager defined by AppLog.getViewExposureManager(), for details, see chapter 5.2 Exposure detection frequency configuration
viewExposureManager.observeViewExposure(banner, data);
// cancel monitoring
viewExposureManager.disposeViewExposure(banner);
```



</Tab>
<Tab zoneid="yNftNJ0RVa" title="6.16.2 and pervious">
<TabTitle>6.16.2 and pervious</TabTitle>

```Java
View banner = findViewById(R.id.banner);
// Optional, custom Export event property
JSONObject properties = new JSONObject();
properties.put("custom_key", "custom_value");
// Optional, default is "$bav2b_exposure"
String eventName = "custom_exposure";

// Versions before 6.16.2: Exposure only supports detecting exposure by area
// Optional, exposure configuration, effective exposure area, and visual debugging switch
// Effective exposure area:  the ratio of the effective exposure of the View display area is set to 0 by default, with a value of 0-1
// Visual debugging switch: default is set to false, do not enable online. After enabling, the exposed View will have a red background border added for debugging purposes
ViewExposureConfig config = new ViewExposureConfig(0.5F, false);
ViewExposureData data = new ViewExposureData(eventName, properties, config);

// start monitoring View exposure event, field viewExposureManager defined by AppLog.getViewExposureManager(), for details, see chapter 5.2 Exposure detection frequency configuration
viewExposureManager.observeViewExposure(banner, data);
// cancel monitoring
viewExposureManager.disposeViewExposure(banner);
```



</Tab>
</Tabs>


<span id="_5-1-设置全局曝光配置"></span>
## 5.1 Setting up the global exposure configuration

<span id="ba26a6dc"></span>
### 5.1.1 Global Exposure Configuration Introduction


<Tabs>
<Tab zoneid="HHm8zjCPGx" title="6.16.2 and later">
<TabTitle>6.16.2 and later</TabTitle>

```Java
// After 6.16.2, exposure supports detection by area and time, and provides exposure callback for event processing
// Optional, exposure configuration, effective exposure area, visual debugging switch, effective exposure time, and exposure event callback
// Effective exposure area:  the ratio of the effective exposure of the View display area is set to 0 by default, with a value of 0-1
// Visual debugging switch: default is set to false, do not enable online. After enabling, the exposed View will have a red background border added for debugging purposes
// Effective exposure time: View time for effective exposure, default is 0, unit: ms
// Exposure event callback: When triggering an exposure event, a callback will be carried with the relevant properties of the current exposure event, which can be custom added and support filtering
ViewExposureConfig config = new ViewExposureConfig(0.5F, false, 200, viewExposureParam -> {
      try {
            // add custom property in callbacks
            viewExposureParam.getExposureParam().put("key", "value");
            // print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            // Filter the current exposure event when an exception occurs
            return false;
      }
      // true retain exposure events
    return true;
});
```



</Tab>
<Tab zoneid="tppO4zfQsO" title="versions before 6.16.2">
<TabTitle>versions before 6.16.2</TabTitle>

```Java
// Versions before 6.16.2: Exposure only supports detecting exposure by area
// Optional, exposure configuration, effective exposure area, and visual debugging switch
// Effective exposure area:  the ratio of the effective exposure of the View display area is set to 0 by default, with a value of 0-1
// Visual debugging switch: default is set to false, do not enable online. After enabling, the exposed View will have a red background border added for debugging purposes
ViewExposureConfig config = new ViewExposureConfig(0.5F, false);
```



</Tab>
</Tabs>


<span id="3291057a"></span>
### 5.1.2 all configuration updates


<Tabs>
<Tab zoneid="wpMZCbqzJ8" title="6.15.2 及以上">
<TabTitle>6.15.2 及以上</TabTitle>

```Java
// After 6.15.2, use ViewExposureManager to replace InitConfig.setViewExposureConfig
// please call after SDK init
AppLog.getViewExposureManager().updateViewExposureConfig(config);
```



</Tab>
<Tab zoneid="diFXHn9vBo" title="6.15.2 以下">
<TabTitle>6.15.2 以下</TabTitle>

```Java
// set global exposure configuration by InitConfig before 6.15.2
config.setViewExposureConfig(config);
```



</Tab>
</Tabs>


<span id="_5-2-曝光检测频率配置"></span>
## 5.2 Exposure detection frequency configuration

In some special scenarios, exposure may not be triggered due to the continuous redrawing of the page. Currently, two new exposure detection strategies are added for selection, which can be dynamically adjusted:

```java
//6.16.2 added
//Default detection strategy, if there are multiple frequent triggers, exposure detection will be triggered 100ms after the last trigger
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.DEBOUNCE);

//Added detection strategy, if there are multiple frequent triggers, exposure detection will be triggered every 500ms
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.THROTTLE);
```


<span id="_6-全埋点事件"></span>
# 6. Full event tracking

> This section is supported after 6.9.0 +.


<span id="05b9cc2e"></span>
## Enable full event tracking

<span id="a5ede472"></span>
### Full event tracking switch

After turning on the full event tracking event collection switch, preset events such as page events and View click events will be collected by default. See the SDK code for full event tracking [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_).

<span id="061b2803"></span>
### Preset event list and reporting logic


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page visit |Trigger the report after the page is opened |
|$bav2b_page_leave |page leave |Trigger a report after leaving the page |
|bav2b_click |View element click event |Trigger a report after clicking on a page element |


Of which:


* bav2b_page: Contains source page related properties (refer_page_xx), when the application is cold start, such property values will be empty, and the page will be filled with source page information in the new page after the page jump.

* $bav2b_page_leave: contains the page stay time property ($page_duration), at this time, the length is calculated to record the page entry and exit timestamp. If the corresponding timestamp cannot be calculated due to the normal acquisition of the page stay time value, the default value of 1s will be assigned as the bottom value.


For more detailed descriptions of each preset event and related event properties, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

<span id="061b2803"></span>
### DataFinder console on

After the SDK is set up, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.

<span id="_6-1-自定义页面事件属性"></span>
## 6.1 Customizing page event properties

In addition to the preset properties of each preset event, DataFinder also supports two ways to configure custom properties of page events (bav2b_page):  **@PageMeta annotation** and **implementation of IPageMeta interface** .

<span id="_6-1-1-pagemeta注解-已废弃"></span>
### 6.1.1 @PageMeta annotation (deprecated)

`@PageMeta`annotation supports custom headers and paths, add the annotation and configuration parameters on an Activity or Fragment, for example:

```java
@PageMeta(path = "/mypath", title = "自定义页面") //custom page
public class MyActivity extends Activity {

}
```


<span id="_6-1-2-实现ipagemeta接口"></span>
### 6.1.2 implement IPageMeta interface (recommended)

`The IPageMeta`interface class supports custom headers, paths, and properties with a higher priority than `@PageMeta`. Implement the interface and corresponding functions on an Activity or Fragment, for example:

```java
public class MyActivity extends Activity implements IPageMeta {
    @Override
    public String title() {
        return "自定义页面"; //custom page
    }
    
    @Override
    public String path() {
        return "/mypath";
    }
    
    @Override
    public JSONObject pageProperties() {
        JSONObject params = new JSONObject();
        try {
            params.put("key", "value");
        } catch (JSONException e) {
            
        }
        return params;
    }
}
```


<span id="_6-2-自定义view点击事件属性"></span>
## 6.2 Custom View Click Event Properties

In addition to the preset properties for each preset event, DataFinder also supports setting custom properties for click events (bav2b_click).

<span id="_6-2-1-设置view的元素id"></span>
### 6.2.1 set the element ID of the view

Support setting an element ID for the specified View object, string is enough, example:

```java
AppLog.setViewId(view, "myElementId");
```


<span id="_6-2-2-设置view的属性"></span>
### 6.2.2 set View properties

Supports setting property values for the specified View object, example:

```java
JSONObject props = new JSONObject();
try {
    props.put("key", "value");
} catch (Exception e) {
}
AppLog.setViewProperties(view, props);
```


<span id="_6-3-忽略全埋点事件"></span>
## 6.3 Ignore full event tracking events

<span id="_6-3-1-忽略特定的页面访问事件"></span>
### 6.3.1 ignore specific page access events

Supports omitting full event tracking events for specific Activities or Fragments, example:

```java
AppLog.ignoreAutoTrackPage(MyActivity.class, MyFragment.class);
```


<span id="_6-3-2-忽略特定view的点击事件"></span>
### 6.3.2 Ignore Click Events for Specific Views


* Ignore the click event of the specified View object, example:

   ```java
   AppLog.ignoreAutoTrackClick(findViewById(R.id.button1));
   ```
   

* Ignore click events of the specified View type, example:

   ```java
   //Ignore click events for all Switch components
   AppLog.ignoreAutoTrackClickByViewType(Switch.class);
   ```
   


<span id="_6-4-手动采集页面事件"></span>
## 6.4 Manually capturing page events

Supports manual collection of page events and properties for specific Activity and Fragment objects. Example:

```java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackPage(MyActivity.this, params);
```


<span id="_6-5-手动采集view点击事件"></span>
## 6.5 Manually Collect View Click Events

Supports manual collection of click events and properties for a specific View. Example:

```java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackClick(myView, params);
```


<span id="_7-采集时长事件"></span>
# 7. Collection time events

> This section is supported after 6.10.1 +.


Events with time properties can use the duration event capture interface, such as capturing video playback duration events. Example:

```java
//Called when the video starts playing
AppLog.startDurationEvent("play");

//Called when the video is paused
AppLog.pauseDurationEvent("play");

//Called when the video continues to play
AppLog.resumeDurationEvent("play");

//Called at the end of playback, a play event will be reported at this time, with a $event_duration attribute (the playback time is recorded, in milliseconds)
JsonObject params = new JsonObject() 
//You can fill in your own custom parameters in params
AppLog.stopDurationEvent("play", params);
//After 6.16.10, the event name of the self-contained custom duration event, the default event name is the first parameter of the method
AppLog.stopDurationEvent("play", params, "custom_play");
```
