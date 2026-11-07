---
title: "Java SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Java_SDK_API_Description"
---

Interface definition Please refer to: [Java SDK interface definition](https://github.com/volcengine/datarangers-sdk-java/blob/main/datarangers-sdk-core/src/main/java/com/datarangers/collector/EventCollector.java).

<span id="8c953840"></span>
# sendEvent

**Function:**  Report an incident

**Definition:**  This method has multiple interface definitions, and the function is the same, but the parameters are different.

```Java
void sendEvent(String userUniqueId, int appId, Map<String, Object> custom, String eventName, Map<String, Object> eventParams,long localTimeMs);
void sendEvent(String userUniqueId, int appId, Map<String, Object> custom, String eventName, Map<String, Object> eventParams);
void sendEvent(Header header, String eventName, Map<String, Object> eventParams);
void sendEvent(Header header, String eventName, Map<String, Object> eventParams, long localTimeMs);
```


**Parameter description:** 


|Parameter name |Type |Explain |
|---|---|---|
|userUniqueId |string |The unique identity of the user needs to ensure that the same user is globally unique in this application, that is, it needs to be consistent with the client side report and cannot be null. |
|appId |int |App ID |
|custom |map |Event public property, cannot be null |
|eventName |string |Event name, cannot be null |
|eventParams |map |Event property, cannot be null |
|localTimeMs |long |The local timestamp where the time occurred. If it is not passed, it will be generated locally by the sdk itself. |
|header |Header |The reported header parameter, by calling `HeaderV3.Builder ().build ()`to build a header.<br><br><br>* The **userUniqueId** and **appId** in the header must be passed, others are not required.<br><br>* The parameters supported by the header can be referred to [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API). |


<span id="6f9e6525"></span>
# sendEvents

**Function:**  Report events, the interface supports multiple events

**Definition:**  `void sendEvents (Header header, List < Event > events)`

**Parameter description:** 


|Parameter name |Type |Explain |
|---|---|---|
|header |Header |The reported header parameter, by calling `HeaderV3.Builder ().build ()`to build a header.<br><br><br>* The **userUniqueId** and **appId** in the header must be passed, others are not required.<br><br>* The parameters supported by the header can be referred to [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API). |
|events |List |It is not recommended that you build the event array yourself. We recommend using the `EventsBuilder`class to construct multiple events and calling the build method to generate the event array. |


<span id="953bdc03"></span>
# user property related interface

**Function:**  Set user properties, different methods have different functions


|Function name |Effect |
|---|---|
|profileSet |Set user properties, override if they exist, and create if they don't. |
|profileSetOnce |Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.<br><br>Unlike the profileSet interface, if a profile has been successfully set through the profileSetOnce interface, it is invalid to call the profileSetOnce interface again on the profile. |
|profileIncrement |Set the properties of the numeric type to accumulate. |
|profileAppend |Set the user properties of the List type to be continuously added to the List. |
|profileUnset |Delete the user's attributes. |


**Definition:**  There are multiple interfaces related to profile, and the parameter meanings are the same.

```Java
void profileSet(String userUniqueId, int appId, Map<String, Object> profiles);
void profileSetOnce(String userUniqueId, int appId, Map<String, Object> profiles);
void profileIncrement(String userUniqueId, int appId, Map<String, Object> profiles);
void profileAppend(String userUniqueId, int appId, Map<String, Object> profiles);
void profileUnset(String userUniqueId, int appId, List<String> profileNames);
void profileSet(Header header, Map<String, Object> profiles)
void profileSetOnce(Header header, Map<String, Object> profiles);
void profileIncrement(Header header, Map<String, Object> profiles);
void profileAppend(Header header, Map<String, Object> profiles);
void profileUnset(Header header, List<String> profiles);
```


**Parameter description:** 


|Parameter name |Type |Explain |
|---|---|---|
|header |Header |The reported header parameter, by calling `HeaderV3.Builder ().build ()`to build a header.<br><br><br>* The **userUniqueId** and **appId** in the header must be passed, others are not required.<br><br>* The parameters supported by the header can be referred to [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API). |
|userUniqueId |string |The unique identity of the user needs to ensure that the same user is globally unique in this application, that is, it needs to be consistent with the client side report and cannot be null. |
|appId |int |appId。 |
|profiles |Map<String,Object\> |User attribute, key is the user attribute name, value is the user attribute value. |
|profileNames |List |List of user property names. |


<span id="1f822ab0"></span>
# business object related interface

**Function:**  Set business object properties, different methods have different functions


|Function name |Effect |
|---|---|
|itemSet |Set the Item property, overwrite if it exists, and create if it does not exist. |
|itemUnset |Removes the Item property. |


**Definition:**  There are multiple interfaces related to profile, and the parameter meanings are the same.

```Java
void itemSet(int appId, String name, List<Item> items);
void itemUnset(int appId, String id, String name, List<String> params);
```


**Parameter description:** 


|Parameter name |Type |Explain |
|---|---|---|
|appId |int |App ID |
|name |String |business object name |
|items |List |Business object class, which needs to inherit from the Item class |
|id |String |business object id |
|params |List |List of business object attribute names |


&nbsp;
