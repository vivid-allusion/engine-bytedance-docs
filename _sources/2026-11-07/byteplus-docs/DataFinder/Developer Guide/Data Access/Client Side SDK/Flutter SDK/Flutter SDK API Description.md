---
title: "Flutter SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_API_Description"
---

This article introduces a series of APIs provided by Flutter for you. You can call the corresponding API in combination with event tracking planning for event tracking.
<span id="be192182"></span>
# Main API Description
<span id="d7a3a62d"></span>
## initRangersAppLog

* **Function:** Initialize the SDK.
* **Definition:** static void initRangersAppLog (String appid, String channel, bool enableAb, bool enableEncrypt, bool enableLog, String? host)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |appid |String |Yes |App appid |
   | | | | | \
   |channel |String |Yes |App download/distribution channels, such as iOS generally'App Store' |
   | | | | | \
   |enableAb |bool |Yes |AB test switch |
   | | | | | \
   |enableEncrypt |bool |Yes |Encryption switch |
   | | | | | \
   |enableLog |bool |Yes |native log switch |
   | | | | | \
   |host |String | |Report address |

* **Example:**
   ```Dart
   String appId = '{{APPID}}';
   String channel = 'App Store';
   bool enableAB = false;
   bool enableEncrypt = true;
   bool enableDebugLog = false;
   String? host = 'https://gator.volces.com';
   RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
   ```


<span id="068d02d5"></span>
## addInitParams

* **Function:** Support to add some additional initialization settings, currently support `region `, `autoStart `, `service_vendor `three settings. This method needs to be executed before initRangersAppLog.
* **Definition:** static void addInitParams (Map < String, dynamic > params)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |params |Map<String, dynamic> |Yes |Currently supports `region`, `autoStart`, `service_vendor`three settings |\
   | | | |```Dart |\
   | | | |//example |\
   | | | |Map<String, dynamic> initParams = { |\
   | | | |  'region': 'cn', |\
   | | | |  'autoStart': true, |\
   | | | |  'service_vendor': 'private', |\
   | | | |}; |\
   | | | |``` |\
   | | | | |

* **Example:**
   ```Dart
   //Set region, autoStart
   Map<String, dynamic> initParams = {
     'region': 'cn', //Corresponding to the app_region field reported by the client side, for cases where custom app_region is required
     'autoStart': true, //false-initialization does not start, true-initialization is start, the default is true (for scenarios where init and start need to be separated)
   };
   RangersApplogFlutterPlugin.addInitParams(initParams);
   //You need to execute addInitParams before the following initRangersAppLog
   RangersApplogFlutterPlugin.initRangersAppLog(/*appId, channel, enableAB, enableEncrypt, enableDebugLog, host*/);
   ```

   ```Dart
   //Set service_vendor, you need to set different service_vendor values in different environments
   Map<String, dynamic> initParams = RangersApplogFlutterPlugin.addInitParams({
       //privatized environment, cloud native environment, etc., fixed value private
       'service_vendor': 'private',
       
       //Domestic non-native environment
       // 'service_vendor': '',
       //Overseas byteplus environment
       // 'service_vendor': 'sg',
   });
   RangersApplogFlutterPlugin.addInitParams(initParams);
   //You need to execute addInitParams before the following initRangersAppLog
   RangersApplogFlutterPlugin.initRangersAppLog(/*appId, channel, enableAB, enableEncrypt, enableDebugLog, host*/);
   ```


<span id="4c0d7a3c"></span>
## start

* **Function:** When autoStart is set to false through addInitParams, you need to actively call the start method to inform the SDK to start reporting events.
* **Definition:** static void start ()
* **Example:**
   ```Dart
   // ...
   Map<String, dynamic> initParams = {
     'autoStart': false,
   };
   RangersApplogFlutterPlugin.addInitParams(initParams);
   RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
   
   //then start
   RangersApplogFlutterPlugin.start();
   ```


<span id="99937276"></span>
## setUserUniqueId

* **Function:** Set user login status. Set user_unique_id value after initialization and the SDK will save it, so it only needs to be set when changes occur.
* **Definition:** static void setUserUniqueId (String? userUniqueID)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |userUniqueID |String |Yes, null. |When null, exit user mode |

* **Example:**
   * Login user mode
   ```Dart
   RangersApplogFlutterPlugin.setUserUniqueId("{{USER_UNIQUE_ID}}")
   ```

   * Exit user mode
   ```Dart
   RangersApplogFlutterPlugin.setUserUniqueId(null)
   ```


<span id="b2d173ef"></span>
## onEventV3

* **Function:** Report the event, it can only be called after initialization.
* **Definition:** static void onEventV3 (String eventName, Map < String, dynamic >? params)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |eventName |String |Yes |Event name, cannot empty string |
   | | | | | \
   |params |Map<String, dynamic> | |event parameters |\
   | | | |```Dart |\
   | | | |{ |\
   | | | |    "key_string": "value_string", |\
   | | | |    "key_int": 10 |\
   | | | |} |\
   | | | |``` |\
   | | | | |

* **Example:**
   ```Dart
   //Example: Report event event_name , the event does not contain properties
   RangersApplogFlutterPlugin.onEventV3("event_name");
   
   //Example: Report event event_name with two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //a property of type int, the property name key_int, the property value is 10
   RangersApplogFlutterPlugin.onEventV3("event_name", {
       "key_string": "value_string",
       "key_int": 10
   });
   ```


<span id="c939db2b"></span>
## setHeaderInfo

* **Role:** Set custom public properties.
* **Definition:** static void setHeaderInfo (Map < String, dynamic > customHeader)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |customHeader |Map<String, dynamic> |Yes |Custom report value, generally need to pass NSString or number, or nil |

* **Example:**
   ```Dart
   //Set a custom public property, the property name is key_public, and the property value is value_public
   RangersApplogFlutterPlugin.setHeaderInfo({
       "key_public": "value_public"
   });
   ```


<span id="237d27fa"></span>
## removeHeaderInfo

* **What:** Removes custom public properties.
* **Definition:** static void removeHeaderInfo (String key)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |key |String |Yes |Custom report key |

* **Example:**
   ```Dart
   //Example: Remove a public property named key_public
   RangersApplogFlutterPlugin.removeHeaderInfo("key_public");
   ```


<span id="d8bb9e74"></span>
## getDeviceId

* **Function:** Get the platform ID.
* **Definition:** static Future < String? > getDeviceId () async
* **Return value:**
   
   | | | \
   |Type |Explain |
   |---|---|
   | | | \
   |Future<String?> |This method is asynchronous and returns a Future. |

* **Example:**
   ```Dart
   //Please start fetching after 3 seconds of initialization completion, otherwise it may return empty
   String did = await RangersApplogFlutterPlugin.getDeviceId();
   ```


<span id="0daa2e24"></span>
# AB test API Description
The SDK provides AB test capabilities and provides a series of methods: getAbSdkVersion, getAllAbTestConfig, getABTestConfigValueForKey.
<span id="79c73ebc"></span>
## Open AB test
```Swift
//Open AB test
bool enableAB = true;
RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
```

The SDK will send a shunt request to the shunt service after initialization. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.
:::warning
* Prerequisites for this step: The experiment and related parameters have been created according to the demand side of the experiment, see [Creating an Experiment ](https://www.volcengine.com/docs/6287/65809#_4-1-%E5%88%9B%E5%BB%BA%E5%AE%9E%E9%AA%8C)for details.
* Each time getABTestConfigValueForKey is called, an exposure event is reported by default abtest_exposure
:::
<span id="fcc01dd4"></span>
## getABTestConfigValueForKey

* **Function:** Get the configuration value of the AB test, which can only be called after initialization.
* **Definition:** static Future < dynamic > getABTestConfigValueForKey (String key, dynamic defaultValue) async
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |key |String |Yes |AB test configured key |
   | | | | | \
   |defaultValue |dynamic |Yes |Default value, if not configured, or not enabled AB test returns the default value |

* **Return value:**
   
   | | | \
   |Type |Explain |
   |---|---|
   | | | \
   |Future<dynamic> |This method is asynchronous and returns a Future. |

* **Example:**
   ```Dart
   String value = await RangersApplogFlutterPlugin.getABTestConfigValueForKey('ab_test_key');
   ```


<span id="b65f217f"></span>
## getAbSdkVersion

* **Function:** Get the exposed AB test configuration vids, which can only be called after initialization.
* **Definition:** static Future < String? > getAbSdkVersion () async
* **Return value:**
   
   | | | \
   |Type |Explain |
   |---|---|
   | | | \
   |Future<String?> |This method is asynchronous and returns a Future. |

* **Example:**
   ```Dart
   String value = await RangersApplogFlutterPlugin.getAbSdkVersion();
   ```


<span id="d9a359e3"></span>
## getAllAbTestConfig

* **Function:** Get all the configuration items of the AB test, which can only be called after initialization.
* **Definition:** static Future < Map < dynamic, dynamic >? > getAllAbTestConfig () async
* **Return value:**
   
   | | | \
   |Type |Explain |
   |---|---|
   | | | \
   |Future<Map<dynamic, dynamic>?> |This method is asynchronous and returns a Future. |

* **Example:**
   ```Swift
   Map<dynamic, dynamic> configs = await RangersApplogFlutterPlugin.getAllAbTestConfig();
   ```


<span id="86c82366"></span>
# User Attributes Features API Description
Provides the ability to set user properties and provides a series of methods: profileSet, profileSetOnce, profileUnset, profileIncrement, profileAppend.
<span id="2eb3011d"></span>
## profileSet

* **Function:** Set user properties, overwrite if they exist, and create if they don't exist.
* **Definition:** static void profileSet (Map < String, dynamic > profileDict)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |profileDict |Map<String, dynamic> |Yes |Parameter dictionary values can only be of the following types: string, integer, floating-point, string array |

* **Example:**
   ```Dart
   RangersApplogFlutterPlugin.profileSet({"key": "value"});
   ```


<span id="f0fba200"></span>
## profileSetOnce

* **Function:** Set user properties, do not set if they exist, create if they do not exist, suitable for first-time related user properties, such as first access time. Unlike the profileSet interface, if a profile has been successfully set through the profileSetOnce interface, it is invalid to call the profileSetOnce interface again on the profile.
* **Definition:** static void profileSetOnce (Map < String, dynamic > profileDict)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |profileDict |Map<String, dynamic> |Yes |Parameter dictionary values can only be of the following types: string, integer, floating-point, string array |

* **Example:**
   ```Dart
   RangersApplogFlutterPlugin.profileSetOnce({"key_once": "value_once"});
   ```


<span id="958365b9"></span>
## profileIncrement

* **Function:** Set the properties of the numeric type to accumulate.
* **Definition:** static void profileIncrement (Map < String, dynamic > profileDict)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |profileDict |Map<String, dynamic> |Yes |Can only increment integers (can be negative integers). If a floating-point number is passed in, the SDK will ignore it. |

* **Example:**
   ```Dart
   RangersApplogFlutterPlugin.profileIncrement({"key": 1});
   ```


<span id="8dc1f600"></span>
## profileAppend

* **Function:** Set the user properties of the List type, which can be continuously added to the List.
* **Definition:** static void profileAppend (Map < String, dynamic > profileDict)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |profileDict |Map<String, dynamic> |Yes |The value of the parameter dictionary can only be a string or a string array. |

* **Example:**
   ```Dart
   RangersApplogFlutterPlugin.profileAppend({"key": "value_append"});
   ```


<span id="b3c52257"></span>
## profileUnset

* **Function:** Delete the user's attributes.
* **Definition:** static void profileUnset (String key)
* **Parameters:**
   
   | | | | | \
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   | | | | | \
   |key |String |Yes |The name of the profile to unset |

* **Example:**
   ```Dart
   RangersApplogFlutterPlugin.profileUnset("key");
   ```
