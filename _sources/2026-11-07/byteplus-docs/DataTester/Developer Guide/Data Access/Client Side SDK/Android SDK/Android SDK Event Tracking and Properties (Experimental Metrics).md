---
title: "Android SDK Event Tracking and Properties (Experimental Metrics)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Android-SDK-Event-Tracking-and-Properties-Experimental-Metrics"
---

<span id="c449d7fe"></span>
# 1. Users and user attributes

<span id="44dc195a"></span>
## 1.1 Login state change call

<span id="9bad04d6"></span>
### 1.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in. 6.13.0 + version supports calling before initializing AppLog to set the uuid of the logged\-in user.

```java
// Set the ID of your account system and ensure its uniqueness
// Version 6.13.0+supports calling this method before initializing AppLog
AppLog.setUserUniqueID("your_USER_UNIQUE_ID");
// If multiple instances are used, corresponding instance settings can be used
IAppLogInstance other = Applog.newInstance();
other.setUserUniqueID("{{USER_UNIQUE_ID}}");
```


(6.13.0 + version is not recommended) Set the uuid through this method, and the setting will only take effect on the first cold start. Since AppLog.setUserUniqueID is supported before initialization in 6.13.0 +, it is no longer recommended to use this method to set uuid. It is recommended to use AppLog.setUserUniqueID uniformly.

```java
// when initializing, configure uuid
// Do not use this method on version 6.13.0 and above
config.setUserUniqueId("your_USER_UNIQUE_ID");
```


<span id="d8f16bf6"></span>
### 1.1.2 account Logout

Called when the account is logged out.

```java
// when log out, set uuid as null
AppLog.setUserUniqueID(null); 
// if it is multi-instance, see 7.1.1
```


Please be careful not to miswrite `("null")`or `(")`, otherwise it will affect the binding of data and users.

<span id="b7cd5031"></span>
## 1.2 Setting user properties

<span id="2b61d491"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```java
// Set the ID of your account system and ensure its uniqueness
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", "value"); 
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileSet(paramsObj);
```


<span id="37a11faa"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```java
// Example: Set the user property with the property name key_once and the property value value_once
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key_once", "value_once");
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileSetOnce(paramsObj);
```


<span id="4499dce4"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```java
// Example: Set the user property with the property name key and the property value 1
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", 1);
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileIncrement(paramsObj);
```


<span id="982c7700"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```java
// Example: Set a user property with the property name 'key'. Originally, there was a property value. Now the property value has been added as 'value_append’.
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key", "value_append");
} catch (JSONException e) {
    e.printStackTrace();
}
AppLog.profileAppend(paramsObj);
```


<span id="c85b1428"></span>
### 1.2.5 profileUnset

Delete the user's attributes.

```java
// Example: delete user property, property name is key
AppLog.profileUnset("key");
```


<span id="d539c6d0"></span>
# 2. Obtain experimental parameters

Usually, a shunt request is sent to the shunt service after the SDK is initialized. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.


* Please note the prerequisite for this step: the experiment and associated parameters have been created according to the demand side of the experiment.

* Note that each time getAbConfig is called, an exposure event is reported by default abtest_exposure


```java
AppLog.addDataObserver(new com.bytedance.applog.IDataObserver() {
    
    /**
     * local ID data loading result notification
     * @param did device id
     * @param iid install id
     * @param ssid ssid
     */
    @Override
    public void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid) {
 
    }
 
    /**
     * Notification of registration results and changes in IDs
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param oldDid old version: device id
     * @param newDid server return new device id
     * @param oldIid old version: install id
     * @param newIid server return new install id
     * @param oldSsid old version: ssid
     * @param newSsid server return new ssid
     */
    @Override
    public void onRemoteIdGet(boolean changed, @Nullable String oldDid, 
                        @NonNull String newDid,@NonNull String oldIid, 
                        @NonNull String newIid, @NonNull String oldSsid, 
                        @NonNull String newSsid) {
 
    }
 
    /**
     * Config pull data and compare it with local data for notifications of changes
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param config server return new config content
     */
    @Override
    public void onRemoteConfigGet(boolean changed, @Nullable JSONObject jsonObject) {
 
    }
 
    /**
     * Server pulls AbConfig data and notifies of changes compared to local data
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param abConfig server return new abConfig content
     */
    @Override
    public void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject jsonObject) {
        // For example, the configured AB experiment parameter name is "MyTest", the parameter type is string, the control group parameter value is "groupA", and the experimental group parameter value is "groupB".//The experimental traffic diversion result is obtained through the applog interface.//The first parameter is the experiment name, and the second parameter is the default parameter value when obtaining the experimental traffic diversion result fails, such as default control group parameter value or null.//The return value is the obtained AB experimental traffic diversion result, which is the experimental parameter value.
        String group = AppLog.getAbConfig("MyTest", null);
        if ("groupA".equals(group)) {
          // perform control group logic
        } else if ("groupB".equals(group)) {
          // perform experimental group logic
        } else {
          // others
        }
    }
 
    /**
     *  Vid change notification
     */
    @Override
    public void onAbVidsChange(@NonNull String vids, @NonNull String extVids) {
 
    }
});
```


If you want to pull the experimental shunt results in real time, you can manually trigger the experimental configuration update through the pullABTestConfigs method  **(multiple calls within 10 seconds will only trigger one request)** 

```plaintext
AppLog.pullAbTestConfigs();//This feature requires version 6.7.0 or above
// After executing this interface, if experimental data is pulled,  IDataObserver.onRemoteAbConfigGet callback will be triggered.
```


<span id="dfb0e188"></span>
# 3. Report experimental metrics (user behavior events)

<span id="fee0ff79"></span>
## 3.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

```java
// Example: reporting event, which does not include property
// Placed in the corresponding position of business logic
AppLog.onEventV3("event");
```


Code event tracking for reporting events and corresponding properties, as follows:

```java
// Example: reporting event, which includes teo properties
//      a string type property, with property name key_string, and property value value_string
//      a int type property, with property name key_int, and property value 10
// Placed in the corresponding position of business logic
JSONObject paramsObj = new JSONObject();
try {
    paramsObj.put("key_string", "value_string"); 
    paramsObj.put("key_int", 10);
} catch (JSONException e) { 
    e.printStackTrace();
}
AppLog.onEventV3("event", paramsObj);
```


<span id="ac4406b4"></span>
## 3.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="fb84fd54"></span>
### 3.2.1 Set public properties

```java
/* 
 * Example: set custom public property with property name key_public and  property value value_public
 * Please note that about custom “public property”：
 * 1. The reporting mechanism is to submit with each log sending, and the default log sending frequency is 1 minute.
 *    So if you continuously modify custom public properties within one minute, the last modification before sending the log shall prevail; 
 * 2. It is not recommended to make frequent modifications, such as modifying once per second.
 */
 Map<String,Object> headerMap = new HashMap<String, Object>();
 headerMap.put("key_public", "value_public");
 AppLog.setHeaderInfo((HashMap<String, Object>)headerMap);
```


<span id="3c8c708e"></span>
### 3.2.2 Remove Public Attributes

```java
// Example: Removing a public property named key_public
AppLog.removeHeaderInfo("key_public");

// Remove all set public properties by passing null
AppLog.setHeaderInfo(null);
```


<span id="ae4f79f4"></span>
# 4. Obtain platform ID and notification

<span id="8ac32387"></span>
## 4.1 Obtaining the platform generated ID

```java
// Please start retrieving after 3 seconds of initialization completion, otherwise it may return empty
String ssid = AppLog.getSsid(); // get SSID
String did = AppLog.getDid(); // get device bddid
```


<span id="9eb31fdb"></span>
## 4.2 Obtaining the SDK version number

```java
// SDK version format is X.X.X
String sdk_version = AppLog.getSdkVersion();
```


<span id="8f3ea4b3"></span>
## 4.3 Obtaining the Experimental Version ID

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">AB test must call the API to obtain experimental parameters (see the <strong>++Getting Experimental Parameters ++</strong>section for details). You can use this API to obtain the Version IDs (vids) of all user exposures or hit experiments, which do not report abtest_exposure exposures.</div>


```JSON
AppLog.getAbSdkVersion();
```


<span id="f652e05c"></span>
## 4.4 Switch account settings to send data

When switching accounts, switch the data sending method at the same time

```java
AppLog.setPrivacyMode(true); //Default is false, set to true, no collection, no reporting
```


<span id="1a7946fd"></span>
## 4.5 Introduction to Common Callbacks: Obtaining Various Notifications

The SDK provides the addDataObserver method to obtain various notifications, which is recommended to be placed in the Application.

```java
public static void addDataObserver(IDataObserver listener)
```


Set the callbacks for iid, ssid, did, abconfig to load from local and server successfully.

The parameters of the IDataObserver interface method are described as follows:

```java
// step1: Add a dataset observation callback, where 'this' refers to the class that implements the IDataObserver
AppLog.addDataObserver(this);
// step2: After obtaining the data through the onIdLoaded or onRemoteIdGet function of IDataObserver, use the following methods:
Default instance: Applog.getDid() / use multi-instance: IAppLogInstance.getDid()


// IDataObserver main functions and parameters introduction:
//  - did、iid、ssid all can be obtained through this callback
//  - server side configuration acquisition
//  - ab experiment configuration acquisition
public interface IDataObserver {
    /**
     * local ID data loading result notification
     * @param did device id
     * @param iid install id
     * @param ssid data description id
     */
    void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid);

    /**
     * Notification of registration results and changes in IDs
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param oldDid local old oldDid, could be empty
     * @param newDid server return with new device id
     * @param newIid server return with new install id
     * @param newSsid server return with new data description id
     */
    void onRemoteIdGet(boolean changed, @Nullable String oldDid, @NonNull String newDid,
                       @NonNull String oldIid, @NonNull String newIid, 
                       @NonNull String oldSsid, @NonNull String newSsid);

    /**
     * Config pull data and compare it with local data for notifications of changes
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param config server return with new config content
     */
    void onRemoteConfigGet(boolean changed, @Nullable JSONObject config);

    /**
     * Server pulls AbConfig data and notifies of changes compared to local data
     * Only the main process will be called
     * @param changed Is it different from local cache
     * @param abConfig server return with new abConfig content
     */
    void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject abConfig);

    /**
     * Notification of changes in vid set exposed in client ab experiment
     * @param vids Client AB experiment exposure vid set
     * @param extVids external vid set for external settings
     */
    void onAbVidsChange(@NonNull String vids, @NonNull String extVids);
}
```


<span id="1d25952c"></span>
# 5. Default public attribute fields

The SDK collects the following information by default and as a public user attribute, it can be grouped and filtered in the growth analysis (DataFinder).


|Field name |Field type |Parameter name |
|---|---|---|
|os |string |Equipment system, the corresponding product attributes are os_name. |
|os_version |string |operating system version |
|app_version |string |App version |
|app_version_minor |string |Secondary version number, App four\-digit version number, requires initialization calls such as: config.setVersionMinor (1.2.3) |
|channel |string |Download channel (can be overwritten after setting), the corresponding product attribute is app_channel. |
|device_model |string |Equipment model |
|region |string |Operating system region |
|language |string |system language |
|sdk_version |string |SDK version |
|timezone |int |Time Zone |
|timezone_offset |int |Time zone offset, corresponding to the in\-product attribute tz_offset. |
|timezone_name |string |Time Zone Name |
|sim_region |string |SIM card region |
|carrier |string |operator |
|resolution |string |resolution |
|device_brand |string |Equipment brand |
|access |string |network type |


<span id="ec790b3b"></span>
# 6. View exposure event capture

> This feature is supported after 6.10.1 +, and it is recommended to use Exposure to initialize the SDK early, such as in Application.


Users need to manually flag exposure events for a View. When this View appears within the visible range of the screen, an exposure event is automatically triggered.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>6.16.0 the following versions, only one exposure event will be triggered after entering the page, and the Views in the 6.16.0 and above pages will trigger multiple exposures according to different behaviors.</strong></div>


<div data-tips="true" data-tips-type="tip">Can be distinguished by the $exposure_type attribute inside the exposure event:</div>


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
<Tab zoneid="rH6i4Na4vk" title="6.16.2 and above">
<TabTitle>6.16.2 and above</TabTitle>

```Java
View banner = findViewById(R.id.banner);
//Optional, custom exposure event properties
JSONObject properties = new JSONObject();
properties.put("custom_key", "custom_value");
//Optional, default is "$bav2b_exposure"
String eventName = "custom_exposure";

//After 6.16.2: Exposure supports detection by area + time, and provides exposure callback for event processing
//Optional, exposure configuration, effective exposure area, visual debugging switch, effective exposure time and exposure event callback
//Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
//Visual debugging switch: Default false, do not turn it on on the line. After turning it on, the exposed View will increase the background red border for debugging.
//Effective exposure time: View time for effective exposure, default is 0, in ms
//Exposure event callback: When an exposure event is triggered, the callback will carry properties related to the current exposure event, which can be customized and appended, and supports filtering
ViewExposureConfig config = new ViewExposureConfig(0.5F, false, 200, viewExposureParam -> {
      try {
            //add custom properties to the callback
            viewExposureParam.getExposureParam().put("key", "value");
            //print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            //Filter the current exposure event when an exception occurs
            return false;
      }
      //true keep exposure events
    return true;
});
ViewExposureData<ViewExposureConfig> callbackData = new ViewExposureData<>(eventName, null, config);

//Start listening to the View exposure event, the viewExposureManager field is defined by AppLog.getViewExposureManager (), see the Exposure Detection Frequency Configuration chapter for details
viewExposureManager.observeViewExposure(banner, data);
//cancel listening
viewExposureManager.disposeViewExposure(banner);
```



</Tab>
<Tab zoneid="iYEEuNC4IL" title="6.16.2 below">
<TabTitle>6.16.2 below</TabTitle>

```Java
View banner = findViewById(R.id.banner);
//Optional, custom exposure event properties
JSONObject properties = new JSONObject();
properties.put("custom_key", "custom_value");
//Optional, default is "$bav2b_exposure"
String eventName = "custom_exposure";

//Before 6.16.2: Exposure only supports exposure detection by area
//Optional, exposure configuration, effective exposure area and visual debugging switch
//Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
//Visual debugging switch: Default false, do not turn it on on the line. After turning it on, the exposed View will increase the background red border for debugging.
ViewExposureConfig config = new ViewExposureConfig(0.5F, false);
ViewExposureData data = new ViewExposureData(eventName, properties, config);

//Start listening to the View exposure event, the viewExposureManager field is defined by AppLog.getViewExposureManager (), see the Exposure Detection Frequency Configuration chapter for details
viewExposureManager.observeViewExposure(banner, data);
//cancel listening
viewExposureManager.disposeViewExposure(banner);
```



</Tab>
</Tabs>


<span id="57904dc2"></span>
## 6.1 Setting Global Exposure Configuration

<span id="5bbf48cb"></span>
### 6.1.1 global exposure configuration introduction:


<Tabs>
<Tab zoneid="Aotmz68Xb8" title="6.16.2 and above">
<TabTitle>6.16.2 and above</TabTitle>

```Java
//After 6.16.2: Exposure supports detection by area + time, and provides exposure callback for event processing
//Optional, exposure configuration, effective exposure area, visual debugging switch, effective exposure time and exposure event callback
//Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
//Visual debugging switch: Default false, do not turn it on on the line. After turning it on, the exposed View will increase the background red border for debugging.
//Effective exposure time: View time for effective exposure, default is 0, in ms
//Exposure event callback: When an exposure event is triggered, the callback will carry properties related to the current exposure event, which can be customized and appended, and supports filtering
ViewExposureConfig config = new ViewExposureConfig(0.5F, false, 200, viewExposureParam -> {
      try {
            //add custom properties to the callback
            viewExposureParam.getExposureParam().put("key", "value");
            //print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            //Filter the current exposure event when an exception occurs
            return false;
      }
      //true keep exposure events
    return true;
});
```



</Tab>
<Tab zoneid="l22FFlD2MS" title="6.16.2 below">
<TabTitle>6.16.2 below</TabTitle>

```Java
//Before 6.16.2: Exposure only supports exposure detection by area
//Optional, exposure configuration, effective exposure area and visual debugging switch
//Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
//Visual debugging switch: Default false, do not turn it on on the line. After turning it on, the exposed View will increase the background red border for debugging.
ViewExposureConfig config = new ViewExposureConfig(0.5F, false);
```



</Tab>
</Tabs>


<span id="e3cbdd6d"></span>
### 6.1.2 all configuration updates


<Tabs>
<Tab zoneid="hdbOzfOzuR" title="6.15.2 and above">
<TabTitle>6.15.2 and above</TabTitle>

```Java
// After 6.15.2: adjust it to ViewExposureManager to replace the previous InitConfig.setViewExposureConfig method
// please call after SDK init
AppLog.getViewExposureManager().updateViewExposureConfig(config);
```



</Tab>
<Tab zoneid="KTvV4cU3FJ" title="6.15.2 below">
<TabTitle>6.15.2 below</TabTitle>

```Java
// Before 6.15.2, set global exposure configuration through InitConfig
config.setViewExposureConfig(config);
```



</Tab>
</Tabs>


<span id="0e1122d9"></span>
## 6.2 Exposure detection frequency configuration

In some special scenarios, exposure may not be triggered due to the continuous redrawing of the page. Currently, two new exposure detection strategies are added for selection, which can be dynamically adjusted:

```java
// 6.16.2 newly added
// The default detection strategy will trigger exposure detection 100ms after the last trigger if there are multiple frequent triggers
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.DEBOUNCE);

// Newly added detection strategy: if the detection strategy is frequently triggered multiple times, it will trigger exposure detection every 500ms
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.THROTTLE);
```


<span id="9e228858"></span>
# 7. Full event tracking

> This section is supported after 6.9.0 +.


After turning on the full event tracking event collection switch, page events and View click events will be collected by default.

<span id="a7e600be"></span>
## 7.1 Customizing page event properties

There are 2 custom configuration properties for page events ($bav2b_page):  **@PageMeta annotation** and **implementation of IPageMeta interface** .

<span id="5eab84dc"></span>
### 7.1.1 @PageMeta annotation (deprecated)

`@PageMeta`annotation supports custom headers and paths, add the annotation and configuration parameters to an Activity or Fragment, for example:

```java
@PageMeta(path = "/mypath", title = "custom page")
public class MyActivity extends Activity {

}
```


<span id="4d28c303"></span>
### 7.1.2 Implement IPageMeta interface (recommended)

`The IPageMeta`interface class supports custom headers, paths, and attributes with a higher priority than `@PageMeta`. Implement the interface and corresponding functions on an Activity or Fragment, for example:

```java
public class MyActivity extends Activity implements IPageMeta {
    @Override
    public String title() {
        return "custom page";
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


<span id="b2f42077"></span>
## 7.2 Customizing View Click Event Properties

<span id="9e3bd277"></span>
### 7.2.1 Set the element ID of the view

Support setting an element ID for the specified View object, string is enough, example:

```java
AppLog.setViewId(view, "myElementId");
```


<span id="c5af35a7"></span>
### 7.2.2 Set View properties

Supports setting property values for the specified View object, example:

```java
JSONObject props = new JSONObject();
try {
    props.put("key", "value");
} catch (Exception e) {
}
AppLog.setViewProperties(view, props);
```


<span id="5693e81c"></span>
## 7.3 Ignoring full event tracking events

<span id="9a694f35"></span>
### 7.3.1 Ignore specific page access events

Supports omitting full event tracking events for specific Activities or Fragments, example:

```java
AppLog.ignoreAutoTrackPage(MyActivity.class, MyFragment.class);
```


<span id="d4b00c2e"></span>
### 7.3.2 Ignore Click Events for Specific Views


* Ignore the click event of the specified View object, example:

   ```java
   AppLog.ignoreAutoTrackClick(findViewById(R.id.button1));
   ```
   

* Ignore click events of the specified View type, example:

   ```java
   // Ignore all click events of Switch components
   AppLog.ignoreAutoTrackClickByViewType(Switch.class);
   ```
   


<span id="45c34e88"></span>
## 7.4 Manually capturing page events

Supports manual collection of page events and properties for specific Activity and Fragment objects. Example:

```java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackPage(MyActivity.this, params);
```


<span id="c0114922"></span>
## 7.5 Manually Collect View Click Events

Supports manual collection of click events and properties for a specific View. Example:

```java
JSONObject params = new JSONObject();
try {
    params.put("param1", "test");
} catch (JSONException e) {
}
AppLog.trackClick(myView, params);
```


<span id="15160d09"></span>
# 8. Collection time events

> This section functions in 6.10.1 +


```Java
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
