---
title: "Android SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Android_SDK_API_Description"
---

This article introduces the main APIs provided by the Android SDK for you. You can call the corresponding API for event tracking in combination with event tracking planning.

<span id="65f25f51"></span>
# AppLog event tracking API introduction

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The external global interface of event tracking supports static calls.</div>


<span id="b83be19a"></span>
## init


* **Function:**  It is to initialize and configure the SDK instance, and the events generated after init will be stored in the local database to ensure that the events will not be lost.

* **Definition:** 

   * void init(@NonNull Context context, @NonNull InitConfig config)

   * void init(@NonNull Context context, @NonNull InitConfig config, Activity activity)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |context |Context |Yes |Application Context |
   |config |InitConfig |Yes |SDK initialization configuration, including AppId, reporting address and other initialization configurations |
   |activity |Activity |No |The SDK internally monitors the activity life cycle to determine the application's front and back\-end status/full event tracking event records (if necessary), etc., so if you initialize the SDK after entering the activity, it is recommended to pass in an additional activity so that the SDK can better count the data you need |
   

* **Example:** 

   ```TypeScript
   //It is recommended to use this method for initialization in Applition
   AppLog.init(context, config);
   
   //It is recommended to use this method to initialize in Activity
   AppLog.init(context, config, activity)
   ```
   


<span id="950f4bb1"></span>
## start


* **Function:**  Launch the SDK, used with initConfig.setAutoStart, often used for privacy compliance.

   * If initConfig.setAutoStart (true), no manual call is required, the SDK starts automatically internally

   * If initConfig.setAutoStart (false), it needs to be called manually, and the SDK will collect sensitive information and request reporting after calling

* **Definition:**  void start ()

* **Example:** 

   ```TypeScript
   //ignore other configurations
   config.setAutoStart(false);
   //init in advance to ensure that events can be dropped locally
   AppLog.init(context, config);
   
   //After the user agrees to the privacy agreement, start is triggered to start collecting user information and reporting events
   AppLog.start();
   ```
   


<span id="43b682a2"></span>
## onEventV3


* **Function:**  Report custom event, Android supports before/after init call.

   * If the cache is called in the application memory before init, up to 300 caches are supported , after more than 300, the earliest cache will be discarded Events will not be stored in the local application database until init is triggered to wait for reporting. If the application has not been init during use, the cached event will be discarded when the application is closed

   * If called after init, the event is directly stored in the local application database and waiting to be reported until the report is successfully deleted.

* **Definition:** 

   * void onEventV3(@NonNull String event)

   * onEventV3(@NonNull String event, @Nullable JSONObject params)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |event |String |Yes |event name |
   |params |JSONObject |No |Event attributes, **it is recommended that custom attributes do not exceed 50kb to avoid affecting the overall data reporting. If the data exceeds 50kb, all custom attributes will be discarded and adjusted to error messages**<br><br>Example of an adjusted error event:<br><br>{<br><br>"params":{<br><br>"description":"event param too large"<br><br>},<br><br>"Event": original event event name,<br><br>} |
   

* **Example:** 

   ```Java
   //Example: Report an event that does not contain properties
   AppLog.onEventV3("event");
   
   //Example: Report an event, which contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //a property of type int, the property name key_int, the property value is 10
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key_string", "value_string");
       paramsObj.put("key_int", 10);
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.onEventV3("event", paramsObj);
   ```
   


<span id="7fccc7c0"></span>
## setUserUniqueID


* **Function:**  Set the user_unique_id, which can be called multiple times, and the subsequent settings will overwrite the same settings as before.

* **Definition:** 

   * void setUserUniqueID(@Nullable String id)

   * void setUserUniqueID(@Nullable String id, @Nullable String type)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |id |String |Yes |UserUniqueID under the user system |
   |type |String |No |The user has multiple calibers, which only involves the use of multiple calibers. |
   

* **Example:** 

   ```Java
   //Non-multi-caliber examples, generally do not require multi-caliber
   //Log in, set the ID of your account system, and ensure its uniqueness
   AppLog.setUserUniqueID("your_USER_UNIQUE_ID");
   //Logout, set uuid to null
   AppLog.setUserUniqueID(null);
   
   //Multi-caliber example
   //Log in, set the ID of your account system, and ensure its uniqueness
   AppLog.setUserUniqueID("your_USER_UNIQUE_ID", "your_USER_UNIQUE_ID_type");
   //Logout, set uuid and uuidType to null at the same time
   AppLog.setUserUniqueID(null, null);
   ```
   


<span id="a608d39d"></span>
## setHeaderInfo


* **Function:**  Set the event public property, which can be called multiple times, and the subsequent setting will overwrite the same setting item before.

   * The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute, so if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail

   * It is recommended that the common attribute be a value that does not recommend high\-frequency changes or invariants

* **Definition:** 

   * void setHeaderInfo(HashMap<String, Object\> custom)

   * void setHeaderInfo(String key, Object value)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |custom |HashMap<String, Object\> |Yes |For setting public properties in batches |
   |key |string |Yes |For a single set of public properties, the key is the public property name |
   |value |Object |Yes |For a single set of public properties, value is the public property value |
   

* **Example:** 

   ```TypeScript
   //batch setting
   HashMap<String,Object> headerMap = new HashMap<String, Object>();
   headerMap.put("key_public", "value_public");
   AppLog.setHeaderInfo(headerMap);
   
   //single setting
   AppLog.setHeaderInfo("key_public", "value_public");
   ```
   


<span id="73b75e64"></span>
## removeHeaderInfo


* **Role:**  Removes event public properties.

* **Definition:**  void removeHeaderInfo (String key)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |String |Yes |For a single set of public properties, the key is the public property name |
   

* **Example:** 

   ```TypeScript
   //Example: Remove a public property named key_public
   AppLog.removeHeaderInfo("key_public");
   
   //Remove all set public properties by passing null
   //Equivalent to setting null when setting will empty all public properties
   AppLog.setHeaderInfo(null);
   ```
   


<span id="c5906b8c"></span>
## setEncryptAndCompress


* **Function:**  Set whether the request is compressed and encrypted, which is turned on by default.

* **Definition:**  void setEncryptAndCompress (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Whether the request is compressed and encrypted, it is turned on by default. |
   

* **Example:** 

   ```TypeScript
   //Enable request compression encryption
   AppLog.setEncryptAndCompress(true);
   
   //Close Request Compression Encryption
   AppLog.setEncryptAndCompress(false);
   ```
   


<span id="33db8b05"></span>
## getDid


* **Function:**  Get the device_id of the current device.

   * You may not be able to get a valid value, because device_id is returned by the device service. If you use it, it is recommended to configure AppLog.addDataObserver to use it

* **Definition:**  String getDid ()

* **Return value:** 



|Type |Explain |
|---|---|
|String |The current device device_id, issued by the device service |



* **Example:** 

   ```TypeScript
   String did = AppLog.getDid();
   ```
   


<span id="2e94d9e9"></span>
## getSsid


* **Function:**  Get the SSID corresponding to the current user.

   * It may not be possible to get a valid value, because the SSID is returned by the device service. If you use it, it is recommended to configure AppLog.addDataObserver to use it.

* **Definition:**  String getSsid ()

* **Parameters:** 

   
   |Type |Explain |
   |---|---|
   |String |The current device SSID is issued by the device service. |
   

* **Example:** 

   ```TypeScript
   String ssid = AppLog.getSsid();
   ```
   


<span id="9bfc4a6c"></span>
## addDataObserver / removeDataObserver


* **Function:**  Add/remove all kinds of data callback monitoring, use together.

* **Definition:** 

   * void addDataObserver(IDataObserver listener)

   * void removeDataObserver(IDataObserver listener)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |IDataObserver |Yes |Monitor SDK initialization/device registration request/AB experiment pull/SDK server level configuration/ABVid changes |
   

* **Example:** 

   ```TypeScript
   //Add a dataset observation callback, this refers to the class that implements IDataObserver
   AppLog.addDataObserver(this);
   
   //IDataObserver main function introduction and parameter introduction:
   //- did, iid, ssid can all be obtained through this callback
   //- server level configuration fetch
   //- ab experiment configuration acquisition
   public interface IDataObserver {
       /**
   * Local id data loading result notification, call back after initializing the local cache, call back every time initialization     *@param did device id
        *@param iid install id
        *@param ssid ssid
        */
       void onIdLoaded(@NonNull String did, @NonNull String iid, @NonNull String ssid);
   
       /**
   * Notify the registration result, as well as the ID change, and call back after each device registration is triggered     Only the main process will be called
        *@param Changed whether it is different from the local cache
        *@param oldDid Local old oldDid, possibly empty
        *@param newDid server returns new device id
        *@param newIid server returns the new install id
        *@param newSsid server returns new ssid
        */
       void onRemoteIdGet(boolean changed, @Nullable String oldDid, @NonNull String newDid,
                          @NonNull String oldIid, @NonNull String newIid, 
                          @NonNull String oldSsid, @NonNull String newSsid);
   
       /**
        * Config pulls data, and notifies changes compared with local data
        Only the main process will be called
        *@param Changed whether it is different from the local cache
        *@param Config server returns new config content
        */
       void onRemoteConfigGet(boolean changed, @Nullable JSONObject config);
   
       /**
        * The server pulls AbConfig data and notifies changes compared with local data
        Only the main process will be called
        *@param Changed whether it is different from the local cache
        *@param abConfig server returns new abConfig content
        */
       void onRemoteAbConfigGet(boolean changed, @NonNull JSONObject abConfig);
   
       /**
        * Notification of client side ab exposure vid collection changes
        *@param Vids client side ab experiment exposure vid collection
        *@param extVids external vid collection of external settings
        */
       void onAbVidsChange(@NonNull String vids, @NonNull String extVids);
   }
   ```
   


<span id="d6b4a795"></span>
## setGPSLocation


* **Function:**  Append GPS related custom properties to the event.

* **Definition:**  void setGPSLocation (float longitude, float latitude, String geoCoordinateSystem)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |longitude |float |Yes |longitude |
   |latitude |float |Yes |latitude |
   |geoCoordinateSystem |String |Yes |coordinate system<br><br>GeoCoordinateSystemConst is a static coordinate system<br><br>WGS84 Earth coordinate system<br><br><br>* GCJ02 Mars coordinate system<br><br>* BD09 Baidu coordinate system<br><br>* BDCS Beidou coordinate system |
   

* **Example:** 

   ```TypeScript
   //GeoCoordinateSystemConst is a static class of coordinate system
   //WGS84 Earth coordinate system
   //GCJ02 Mars coordinate system
   //BD09 Baidu coordinate system
   //BDCS Beidou coordinate system
   //This function only supports 6.10.1 and above versions
   AppLog.setGPSLocation(18.00f, 18.00f, GeoCoordinateSystemConst.WGS84);
   ```
   


<span id="c73f46c7"></span>
# InitConfig SDK Configuration API Introduction

<span id="79aa64b8"></span>
## setLogEnable


* Function: \*\*\*\* Whether to open the SDK log, it is closed by default.

* Definition: setLogEnable (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |log switch |
   

* Example:

   ```TypeScript
   //Open the SDK log
   config.setLogEnable(true);  
     
   //Close the SDK log
   config.setLogEnable(false);  
   ```
   


<span id="cb9f165f"></span>
## setLogger


* **Function:**  Take over the internal log content of the SDK, and the subsequent output will be handled by the developer. You need to cooperate with setLogEnable to open the log first.

* **Definition:**  void setLogger (ILogger logger)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |logger |ILogger |Yes |SDK internal log callback |
   

* **Example:** 

   ```TypeScript
   //Open the log first
   config.setLogEnable(true); 
   //Take over log printing
   config.setLogger(new ILogger() {
       @Override
       public void log(String s, Throwable throwable) {
           Log.d("AppLog------->: ", "" + s);
       }
   });
   ```
   


<span id="49c49981"></span>
## setAutoStart


* **Function:**  Whether to automatically start the SDK, automatically start by default, if it involves delayed start, you can first init to configure autoStart false, and manually call AppLog.start () when sensitive information can be collected and requests are reported.

* **Definition:**  void setAutoStart (boolean autoStart)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |autoStart |boolean |Yes |Whether to start the SDK after init. |
   

* **Example:** 

   ```TypeScript
   //The SDK automatically completes the initialization after AppLog.init, and starts collecting sensitive information + sending requests when init.
   config.setAutoStart(true);    
   
   //The SDK does not continue to initialize after AppLog.init, and waits for AppLog.start to start collecting sensitive information + sending requests
   config.setAutoStart(false); 
   AppLog.init(context, config);
   //Call start at the appropriate time to actually start the SDK (e.g. after agreeing to the privacy agreement)
   AppLog.start()   
   ```
   


<span id="02af76d8"></span>
## setUriConfig


* Function: Set the SDK request domain name.

* Definition: void setUriConfig (UriConfig config)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |config |UriConfig |Yes |Request domain name configuration |
   

* Example:

   ```TypeScript
   String host = "xxxx";
   //The second parameter of createByDomain does not need to be set, just null.
   config.setUriConfig(UriConfig.createByDomain(host, null));    
   ```
   


<span id="d957c49a"></span>
## setAbEnable


* **Function:**  Whether to turn on the AB experiment function, turn it off by default.

* **Definition:**  void setAbEnable (boolean enable)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |AB experimental switch |
   

* **Example:** 

   ```TypeScript
   //Start the AB experiment
   config.setAbEnable(true);
   
   Close the AB experiment
   config.setAbEnable(false);
   ```
   


<span id="5bb46460"></span>
## enableDeferredALink


* **Function:**  Turn on Tracer ad monitoring function, turn it off by default.

* **Definition:**  void enableDeferredALink ()

* **Example:** 

   ```TypeScript
   // Enable Tracer ad monitoring function
   config.enableDeferredALink()
   ```
   


<span id="4e69e678"></span>
## disableDeferredALink


* **Function:**  Turn off the Tracer ad monitoring function, which is turned off by default.

* **Definition:**  void disableDeferredALink ()

* **Example:** 

   ```TypeScript
   //Turn off Tracer ad monitoring function
   config.disableDeferredALink()
   ```
   


<span id="4bf5cffc"></span>
## setExposureEnabled


* **Function:**  Whether the element exposure function is turned off by default.

* **Definition:**  void setExposureEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Elemental exposure capability switch |
   

* **Example:** 

   ```TypeScript
   //Enable element exposure ability
   config.setExposureEnabled(true);
   
   //turn off element exposure capability
   config.setExposureEnabled(false);
   ```
   


<span id="94209be2"></span>
## setAutoTrackEnabled


* **Function:**  Whether to turn on full event tracking collection, it is turned on by default.

   * Full event tracking includes three event tracking: page entry, page exit, and element click.

   * Android full event tracking needs to integrate RangersAppLog\-All\-xx version, and requires integrated RangersAppLog\-All\-plugin plugin

   * The page exits because the default does not collect setAutoTrackEventType cooperation is required

* **Definition:**  void setAutoTrackEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Full event tracking acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Enable full event tracking
   config.setAutoTrackEnabled(true);
   
   //turn off full event tracking
   config.setAutoTrackEnabled(false);
   ```
   


<span id="bee3f343"></span>
## setAutoTrackFragmentEnabled


* **Function:**  Whether to turn on the related full event tracking collection of the Fragment page, it is turned off by default.

* **Definition:**  void setAutoTrackFragmentEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Fragment page full event tracking capture switch |
   

* **Example:** 

   ```TypeScript
   //This function is recommended 6.17.6 version and above
   //Open the relevant full event tracking collection of the Fragment page
   config.setAutoTrackFragmentEnabled(true);
   
   //Close the related full event tracking of the Fragment page
   config.setAutoTrackFragmentEnabled(false);
   ```
   


<span id="446ff1b6"></span>
## setAutoTrackEventType


* **Function:**  Set the full event tracking collection type, the default collection page enters and clicks on elements.

* **Definition:**  void setAutoTrackEventType (int type)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |setAutoTrackEventType |int |Yes |Set the full event tracking collection type, the call form is AutoTrackEventType.xxx , and the value will be mapped to the pre\-declared int value:<br><br><br>* Configured as: AutoTrackEventType. *PAGE* , indicating that the collection of full event tracking page events is enabled by default.<br><br>* Configured as: AutoTrackEventType. *CLICK* , indicating that the collection of all buried point click events is enabled by default.<br><br>* Configured as: AutoTrackEventType. *PAGE_LEAVE* , indicating that the collection of full event tracking page leaves the event, which is closed by default.<br><br>* Configured as: AutoTrackEventType. *ALL* , indicating that all events are collected for full event tracking. |
   

* **Example:** 

   ```TypeScript
   //default configuration
   config.setAutoTrackEventType(AutoTrackEventType.PAGE | AutoTrackEventType.CLICK);
   
   //All collection, page entry + page exit + element click
   AppLog.setEncryptAndCompress(AutoTrackEventType.ALL);
   ```
   


<span id="288d24f3"></span>
## setMacEnable


* **Function:**  Whether to turn on mac collection, the default collection.

* **Definition:**  void setMacEnable (boolean enable)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |MAC acquisition switch |
   

* **Example:** 

   ```TypeScript
   //enable mac acquisition
   config.setMacEnable(true);
   
   //turn off mac acquisition
   config.setMacEnable(false);
   ```
   


<span id="a460cc7c"></span>
## setImeiEnable


* **Function:**  Whether to turn on imei collection, the default collection.

* **Definition:**  void setImeiEnable (boolean enable)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |IMEI acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Open imei acquisition
   config.setImeiEnable(true);
   
   //close imei acquisition
   config.setImeiEnable(false);
   ```
   


<span id="77b04ca2"></span>
## setOaidEnabled

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">OAID is important device tracking information. Turning off OAID will affect Tracer attribution. Please consider using Tracer with caution</div>



* **Function:**  Whether to turn on oaid collection, the default collection.

* **Definition:**  void setOaidEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |OAID acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Open oaid acquisition
   config.setOaidEnabled(true);
   
   //turn off oaid collection
   config.setOaidEnabled(false);
   ```
   


<span id="a1ed597c"></span>
## setAndroidIdEnabled

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Closing the Android ID will affect the device_id generation logic, resulting in inconsistent device_id uninstall and reinstall.</div>


<div data-tips="true" data-tips-type="warning">Subsequent documentation will be abbreviated device_id did.</div>



* **Function:**  Whether to enable AndroidId collection, the default collection.

* **Definition:**  void setAndroidIdEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |AndroidId acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Enable AndroidId collection
   config.setAndroidIdEnabled(true);
   
   //Disable AndroidId collection
   config.setAndroidIdEnabled(false);
   ```
   


<span id="dd701d70"></span>
## setIccIdEnabled


* **Function:**  Whether to turn on iccid collection, the default collection.

* **Definition:**  void setIccIdEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |ICCID acquisition switch |
   

* **Example:** 

   ```TypeScript
   //enable iccid acquisition
   config.setIccIdEnabled(true);
   
   //turn off iccid acquisition
   config.setIccIdEnabled(false);
   ```
   


<span id="341656c6"></span>
## setSerialNumberEnable


* **Function:**  Whether to turn on mac collection, the default collection.

* **Definition:**  void setSerialNumberEnable (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |SN serial number acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Enable SN serial number acquisition
   config.setSerialNumberEnable(true);
   
   //Turn off SN serial number acquisition
   config.setSerialNumberEnable(false);
   ```
   


<span id="844db3f9"></span>
## setGaidEnabled


* **Function:**  Whether to turn on mac collection, do not collect by default.

   * The cn version does not collect by default, and the global default collects.

   * Before collecting, it will also see if there is a com.google.android .gms: play\-services dependency. If not, it will not be collected.

* **Definition:**  void setGaidEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enabled |boolean |Yes |GAID acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Enable gaid collection
   config.setGaidEnabled(true);
   
   //turn off gaid collection
   config.setGaidEnabled(false);
   ```
   


<span id="9b224654"></span>
## setOperatorInfoEnabled


* **Function:**  Whether to turn on operator information collection, default collection.

* **Definition:**  void setOperatorInfoEnabled (boolean enabled)

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enabled |boolean |Yes |Operator information acquisition switch |
   

* **Example:** 

   ```TypeScript
   //Turn on operator information collection
   config.setOperatorInfoEnabled(true);
   
   //Turn off operator information collection
   config.setOperatorInfoEnabled(false);
   ```
   


<span id="b4ce587b"></span>
## setCPUAbiEnabled


* Function: Whether to enable cpu architecture collection, default collection.

* Definition: void setCPUAbiEnabled (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |CPU architecture acquisition switch |
   

* Example:

   ```TypeScript
   //Open the cpu architecture
   config.setCPUAbiEnabled(true);
   
   //Close the CPU architecture
   config.setCPUAbiEnabled(false);
   ```
   


<span id="46e8bf81"></span>
## setDisplayDensityAndDpiEnabled


* Function: Whether to turn on screen information collection, the default collection.

* Definition: void setDisplayDensityAndDpiEnabled (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Screen information acquisition switch |
   

* Example:

   ```TypeScript
   //Turn on screen information collection
   config.setDisplayDensityAndDpiEnabled(true);
   
   //Turn off screen information collection
   config.setDisplayDensityAndDpiEnabled(false);
   ```
   


<span id="c5b75e32"></span>
## setScreenOrientationEnabled


* Function: Whether to turn on the screen direction acquisition, the default acquisition.

* Definition: void setEncryptAndCompress (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Screen orientation capture |
   

* Example:

   ```TypeScript
   //Turn on screen orientation capture
   config.setScreenOrientationEnabled(true);
   
   //Turn off screen orientation capture
   config.setScreenOrientationEnabled(false);
   ```
   


<span id="8930cdca"></span>
## setTrackCrashType


* Function: Crash event collection configuration, not collected by default.

* Definition: void setTrackCrashType (int options)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |options |int |Yes |crash event acquisition configuration |
   

* Example:

   ```TypeScript
   //Enable Java Collapse
   config.setTrackCrashType(AppCrashType.JAVA);
   
   //Close Java Collapse
   config.setTrackCrashType(0);
   ```
   


<span id="a40f2071"></span>
## setEncryptor


* Function: Set custom encryption\-related logic.

   * Privatization V4.4.0 version supports the request encryption of the national secret SM2 algorithm

* Definition:

   * void setEncryptor(IEncryptor encryptor)

   * void setEncryptor(IEncryptor encryptor, String encryptorType)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |encryptor |IEncryptor |Yes |Whether the request is compressed and encrypted, it is turned on by default. |
   |encryptorType |String |No | |
   

* Example:

   ```TypeScript
   //sm2 encryption
   Sm2Helper sm2Helper = new Sm2Helper(yourPublicKey);
   config.setEncryptor(new IEncryptor() {
       @Override
       public byte[] encrypt(byte[] data, int size) {
           //Convert the original data to encrypted data
           return sm2Helper.encrypt(data, size);
       }
       //The encryption type will be put into Content-Type, which needs to be agreed with the private deployment.
   }, sm2Helper.encryptorType());
   ```
   


<span id="d988c720"></span>
## setPicker


* Function: Set the ring selector, which is required when using the ring selector.

* Definition: void setPicker (IPicker picker)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |picker |IPicker |Yes |Circle selector configuration |
   

* Example:

   ```TypeScript
   //Set the ring selector
   config.setPicker(new Picker(this, config));
   ```
   


<span id="960f75cc"></span>
## setH5BridgeEnable


* Function: Whether to turn on h5 to get through, it will not be turned on by default.

   Attention:

   * H5 connection only supports native WebView and Tencent X5

   * H5 connection means that h5 is integrated on the end and the Finder Web SDK is integrated in h5. I hope that the Web SDK in the App is also carried out through the upper caliber of the App on the end.

   * Before getting through: Web SDK/Android SDK generate separate events and report them separately

   * After getting through: the events/changes generated by the Web SDK are synchronized to the end, and finally reported on the App side

* Definition: void setH5BridgeEnable (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |H5 open the acquisition switch |
   

* Example:

   ```TypeScript
   //Open h5 to open
   config.setH5BridgeEnable(true);
   
   //close h5 and get through
   config.setH5BridgeEnable(false);
   ```
   


<span id="9171af12"></span>
## setH5BridgeAllowlist


* Function: Set the whitelist list of H5 to get through, setH5BridgeAllowlist/setH5BridgeAllowAll choose one of the two settings, the default is empty.

* Definition: void setH5BridgeAllowlist (List < String \> h5BridgeAllowlist)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |h5BridgeAllowlist |List |Yes |H5 whitelist list allowed to get through |
   

* Example:

   ```TypeScript
   //Configure the whitelist allowed to get through
   config.setH5BridgeAllowlist(Arrays.asList("xxxx"));
   ```
   


<span id="14dff8e1"></span>
## setH5BridgeAllowAll


* Function: Do not do domain name verification when H5 gets through, setH5BridgeAllowlist/setH5BridgeAllowAll choose one of the two settings, and close by default.

   * If setH5BridgeAllowAll is closed, it will determine whether the current h5 domain name is configured in the setH5BridgeAllowlist

   * Determine whether the current h5 is allowed to get through, first determine setH5BridgeAllowAll, if true, try to get through directly, if false, determine whether the setH5BridgeAllowlist is configured with the current h5 as a whitelist

* Definition: void setH5BridgeAllowAll (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |Determine whether to allow non\-verification |
   

* Example:

   ```TypeScript
   //Allow all h5 domains to get through
   config.setH5BridgeAllowAll(true);
   
   //Turn off allow all, and further verification is required to see if it gets through.
   config.setH5BridgeAllowAll(false);
   ```
   


<span id="ca6d3643"></span>
## setH5CollectEnable


* Function: Whether to collect the full event tracking of H5, it is turned off by default.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature can be used independently without the need to integrate a Web/JavaScript SDK.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature is available 6.14.4 version, and the current H5 full event tracking only supports page entry events and click events.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature only supports native WebView and Tencent X5.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The old version of the Web SDK can not collect H5 full event tracking, you need to initialize the matching settings.   </div>
   

* Definition: void setH5CollectEnable (boolean enabled)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |enable |boolean |Yes |H5 full event tracking acquisition switch |
   

* Example:

   ```TypeScript
   //Enable H5 full event tracking
   config.setH5CollectEnable(true);
   
   //Turn off H5 full event tracking
   config.setH5CollectEnable(false);
   ```
   


<span id="7748b04e"></span>
## setCustomOaidCallback


* Function: Set the custom injection Oaid, which is not implemented by default and is collected internally by the SDK.

   * If you have high requirements for Oaid collection rate and have your own Oaid collection method, you can use your own Oaid by injection.

* Definition: void setCustomOaidCallback (DynamicValueCallback < String \> callcack)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |callcack |boolean |Yes |oaid callback |
   

* Example:

   ```TypeScript
   //6.16.11 version added
   InitConfig config = new InitConfig("yourAPPID", "yourCHANNEL");
   //Key point: Make sure to start collecting user information only after starting
   config.setAutoStart(false);
   //Key point: setting custom Oaid custom setting callbacks
   config.setCustomOaidCallback(new DynamicValueCallback<String>() {
       @Override
       public String get() {
           //Customize the fetch logic, if no callback is set or the callback returns "/null, go with the built-in Oaid fetch logic
           return getCustomOaid();
       }
   });
   //Omit other SDK configurations
   //Initialize once
   //It is recommended to use this method for initialization in Applition
   AppLog.init(this, config);
   //It is recommended to use this method for initialization in Activity
   AppLog.init(this, config, activity);
   
   //Key point: Since setAutoStart false is set, you need to manually call the start trigger SDK, please call it after getting oaid
   //start the actual collection of user information + report:
   AppLog.start()；
   ```
   


<span id="a9dfd686"></span>
# AB test features and API introduction

The SDK provides AB experimental capabilities and provides a series of methods: getAbConfig, getAbSdkVersion, getAllAbTestConfigs, setExternalAbVersion, pullAbTestConfigs

<span id="ef1f70cb"></span>
## Start AB experiment

To use the function, you need to turn on the corresponding parameters when initializing the SDK settings:

```TypeScript
//omit other configurations
config.setAbEnable(true);
AppLog.init(context, config);
```


<span id="594025b4"></span>
## AB experimental method

<span id="d817b8bd"></span>
### getAbConfig


* Function: Obtain the configuration item value corresponding to the experiment in the AB experiment configuration, and the SDK will collect the corresponding vid (business generally does not need to directly care about the vid).

* Definition: < T \> T getAbConfig (String key, T defaultValue)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |String |Yes |The key in the experimental configuration |
   |defaultValue |T generics, which infer the return type from the passed in |Yes |When there is no corresponding key configuration item in the experimental configuration, the method will return the bottom value |
   

* Return value:

   
   |type |Explain |
   |---|---|
   |T |Return the experimental result corresponding to the experimental key. If there is no corresponding experiment, return the passed defaultValue as the bottom line. |
   

* Example:

   ```TypeScript
   //By ab_key corresponding experiment, and it is considered that it returns a String type, if there is no corresponding experiment to return default_value
   String result = AppLog.getAbConfig("ab_key", "default_value");
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: Business call getAbConfig method, SDK found the experimental configuration has a corresponding key, will report a preset event abtest_exposure.</div>


<span id="a8ffb70c"></span>
### getAllAbTestConfigs


* Function: Obtain all configuration information of AB experiment.

* Definition: JSONObject getAllAbTestConfigs ()

* Return value:

   
   |Type |Explain |
   |---|---|
   |JSONObject |Returns all experimental results, if not pulled to the experiment returns an empty JSONObject. |
   

* Example:

   ```TypeScript
   //By ab_key corresponding experiment, and it is considered that it returns a String type, if there is no corresponding experiment to return default_value
   JSONObject abConfigs = AppLog.getAllAbTestConfigs();
   ```
   


<span id="747c0c72"></span>
### getAbSdkVersion


* Function: Get the exposed experiment, and the returned result is the vid of all exposed experiments, connected with commas, example: 123,234,678

* Definition: String getAbSdkVersion ()

* Return value:

   
   |Type |Explain |
   |---|---|
   |String |All vids of exposure experiments, connected with commas, example: 123,234,678 |
   

* Example:

   ```TypeScript
   //vids value is similar to 123,234,678
   String vids = AppLog.getAbSdkVersion();
   ```
   


<span id="483aa0a6"></span>
### setExternalAbVersion


* Function: Manually set up additional AB experimental configurations.

* Definition: void setExternalAbVersion (@NonNull String version)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |version |String |Yes |Format requirements for version: Concatenate version values with commas, something like '123,234,678'.<br><br>Additional experimental configuration vids set in this way will be merged into the vids obtained through getAbConfig processing<br><br>When called multiple times, it will be merged and deduplicated through Set storage |
   

* Example:

   ```TypeScript
   //Additional settings vid
   AppLog.setExternalAbVersion("123")
   ```
   


<span id="2f61cc66"></span>
### pullAbTestConfigs


* Function: Manually trigger a request for AB experiment results to pull the latest experiment.

* Definition:

   * void pullAbTestConfigs();

   * void pullAbTestConfigs(int timeout, IPullAbTestConfigCallback callback);

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |timeout |int |No |timeout |
   |callback |IPullAbTestConfigCallback |No |Pull result callback, including pull success or pull failure<br><br>void onRemoteConfig(@Nullable JSONObject config);<br><br><br>* Pull to experimental results<br><br>   void onTimeoutError();<br><br>* Pull experiment timeout<br><br>   void onThrottle(long remainingTime);<br><br>* Pull intervals are too frequent, triggering limits |
   

* Example:

   ```TypeScript
   //no callback
   AppLog.pullAbTestConfigs();
   
   //there is a callback
   AppLog.pullAbTestConfigs(
           5000,
           new IPullAbTestConfigCallback() {
               @Override
               public void onRemoteConfig(JSONObject config) {
                   Log.i("pull", config == null ? "": config.toString());
               }
   
               @Override
               public void onTimeoutError() {
                   Log.e("pull", "errr");
               }
   
               @Override
               public void onThrottle(long remainingTime) {
                   Log.e("pull", "errr " + remainingTime);
               }
   });
   ```
   


<span id="9b071c87"></span>
# User Attributes Module and API Introduction

Provides the ability to set user properties and provides a series of methods: profileSet, profileSetOnce, profileUnset, profileIncrement, profileAppend.

<span id="13499d28"></span>
## user property method

<span id="ee27c8d3"></span>
### profileSet


* Function: Overwrite the attribute field with a new value, you can set one or more attributes at a time, and support array type attribute values.

* Definition: void profileSet (JSONObject jsonObject)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |jsonObject |JSONObject |Yes | |
   

* Example:

   ```TypeScript
   //Example: Set the user property, the property name is key, and the property value is value
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key", "value");
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.profileSet(paramsObj);
   ```
   


<span id="5730c462"></span>
### profileSetOnce


* Function: According to the attribute field, it is only set once. If it already has a value, it will not be updated.

* Definition: void profileSetOnce (JSONObject jsonObject)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |jsonObject |JSONObject |Yes | |
   

* Example:

   ```TypeScript
   //Example: Set a user property with the property name key_once and the property value value_once
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key_once", "value_once");
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.profileSetOnce(paramsObj);
   ```
   


<span id="da1a75e1"></span>
### profileUnset


* Function: Delete the value of a property.

* Definition: void profileUnset (String key)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |String |Yes | |
   

* Example:

   ```TypeScript
   //Example: Delete a user attribute named key
   AppLog.profileUnset("key");
   ```
   


<span id="519a82f2"></span>
### profileIncrement


* Function: Increases the numeric property by the specified value, which can be a negative number.

* Definition: void profileIncrement (JSONObject jsonObject)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |jsonObject |JSONObject |Yes | |
   

* Example:

   ```Java
   //Example: Set the user property, the property name is key, and the property value is 1
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key", 1);
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.profileIncrement(paramsObj);
   ```
   


<span id="3e37c5e5"></span>
### profileAppend


* Function: When the property does not exist, create the property and set it. If it is an array type property, the value will be appended to the array.

* Definition: void profileAppend (JSONObject jsonObject)

* Parameter:

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |jsonObject |JSONObject |Yes | |
   

* Example:

   ```TypeScript
   //Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
   JSONObject paramsObj = new JSONObject();
   try {
       paramsObj.put("key", "value_append");
   } catch (JSONException e) {
       e.printStackTrace();
   }
   AppLog.profileAppend(paramsObj);
   ```
   


<span id="6590c90e"></span>
# Element exposure function and API introduction

<span id="b9cbd328"></span>
## Enable element exposure

This feature is supported after 6.10.1 +, and it is recommended to use Exposure to initialize the SDK early, such as in Application.


1. Configure in InitConfig during SDK initialization.

   ```TypeScript
   //omit other configurations
   config.setExposureEnabled(true);
   AppLog.init(context, config);
   ```
   


<span id="cac3efe8"></span>
## Set Global Exposure Configuration

<span id="186d9a1e"></span>
### Introduction to Global Exposure Configuration


|configuration item |Type |default value |Explain |supported version |
|---|---|---|---|---|
|effective exposure area |float |1f |Effective exposure area configuration, configured as a percentage, 1f indicates that exposure is triggered when the component is 100% visible. |6.10.1+ |
|Visual debug switch |boolean |false |The visual debug switch will add a border to the component, with red indicating exposure and yellow indicating unexposed. |6.10.1+ |
|effective exposure time |long |0 |Effective residence time, in ms, for example, you can set the component to stay more than 3000ms before exposure. |6.16.2+ |
|exposure event callback |(ViewExposureParam) \-\> Boolean | **{**  true  **}**  |The callback after the component is exposed supports adding new properties, or filtering for specific exposure events. Returning true indicates that the event is retained, and returning false indicates that the event is discarded. |6.16.2+ |


**6.16.2 and above**

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
            //Print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            Filter the current exposure event when an exception occurs
            return false;
      }
      //true keep exposure events
    return true;
});
```


**6.16.2 below**

```Java
//Before 6.16.2: Exposure only supports exposure detection by area
//Optional, exposure configuration, effective exposure area and visual debugging switch
//Effective exposure area: The ratio of the display area of the effectively exposed View, the default is 0, and the value is 0-1.
//Visual debugging switch: Default false, do not turn it on on the line. After turning it on, the exposed View will increase the background red border for debugging.
ViewExposureConfig config = new ViewExposureConfig(0.5F, false);

```


<span id="d981ea27"></span>
### Global Exposure Configuration Update

**6.15.2 and above**

```Java
//6.15.2 adjusted to the ViewExposureManager to replace the previous InitConfig.setViewExposureConfig method
//Please call after SDK init
AppLog.getViewExposureManager().updateViewExposureConfig(config);
```


**6.15.2 below**

```Java
//Set global exposure configuration via InitConfig before 6.15.2
config.setViewExposureConfig(config);
```


<span id="cc930726"></span>
## Exposure detection frequency configuration

In some special scenarios, exposure may not be triggered due to the continuous redrawing of the page. Currently, two new exposure detection strategies are added for selection, which can be dynamically adjusted:

```Java
//6.16.2 added
//Default detection strategy, if there are multiple frequent triggers, exposure detection will be triggered 100ms after the last trigger
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.DEBOUNCE);

//Added detection strategy, if there are multiple frequent triggers, exposure detection will be triggered every 500ms
AppLog.getViewExposureManager().updateExposureCheckStrategy(ExposureCheckType.THROTTLE);
```


<span id="5cf4a99f"></span>
## Component exposure usage

After enabling the configuration, add exposure monitoring to the View that needs to be exposed. Example code:

**6.16.2 and above**

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
            //Print exposure type
            Log.d("Exposure", "ExposureType: " + viewExposureParam.getExposureParam().get("$exposure_type"));
      } catch (JSONException e) {
            Filter the current exposure event when an exception occurs
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


**6.16.2 below**

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
