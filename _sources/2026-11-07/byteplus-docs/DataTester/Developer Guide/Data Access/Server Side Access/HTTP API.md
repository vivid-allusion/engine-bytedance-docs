---
title: "HTTP API"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/HTTP-API"
---

Attention


* The http interface reported by the server level is opened by default. If the application you access is not opened, please contact the customer success manager to solve it;

* The content of this document may vary between different environments such as SaaS, SaaS cloud native, and privatization. Please pay attention to the distinction.


<span id="e3ae4de4"></span>
# 1. Request interface


|Environment |URL |Method |
|---|---|---|
|Privatization |* Single data upload: https://${host}/v2/event/json<br><br>* Batch data upload (up to 50 pieces per batch): https://${host}/v2/event/list<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">${Host}: Private deployment The domain name applied by the customer for event tracking data reporting, please replace it according to the actual domain name. After the customer domain name is updated, the reported path address also needs to be updated synchronously.</div><br> | |


<span id="9999d3f1"></span>
# 2. Request specifications


1. The request header contains "Content\-Type: application/json" and "X\-MCS\-AppKey" as the identity of the app. When reporting through the http API, if you use code and some tools, the user\-agent field will be automatically attached to the request header. If you send it manually, it may prompt that the user\-agent is not allowed. You need to manually add the user\-agent field to the request header.

2. The request body contains three parts: user, header, and event, and the header is the header of the event tracking data itself;

3. The number of single upload events is recommended to be controlled within 20, and more than 50 will be reported to 413;

4. If the upload uses the/v2/event/list interface, it is recommended to control the number of jsons within 20, and 413 will be reported if there are more than 50.

    &nbsp;


<span id="_2-1-request-headers"></span>
## **2.1 Request headers**


|Field |Type |Description |
|---|---|---|
|Content\-Type |string |application/json |
|X\-MCS\-AppKey |string |APP Key of your application |


Please refer to the following screenshot for the location of APP Key:

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="9e4658e5"></span>
## **2.2 Request body**


|Field |Type |Description |
|---|---|---|
|user |object |User Attribute Dictionary, see 2.3 for details. |
|header |object |Header property dictionary, see 2.4 for details. |
|events |[object] |Events list, each element is an event, as detailed in 2.5. |


<span id="ced930e4"></span>
## **2.3 Format of users**


|Field |Type |Required |Description |
|---|---|---|---|
|user_unique_id |string |Yes |The unique identity of the user needs to ensure that the same user is globally unique within the application, that is, it needs to be consistent with the client side report. |
|device_id |string |No |App\-side device identification, note that it must be purely digital. |
|web_id |string |No |Web device identification, note that it must be purely digital. |


<span id="9d3f91f6"></span>
## **2.4 Header format**


|Field |Type |Required |Description |
|---|---|---|---|
|app_name |string |No |The English name of the application |
|app_package |string |No |package name |
|app_channel |string |No |App distribution channel |
|app_version |string |No |App version, three segments separated, such as 1.0.1 |
|app_platform |string |No |At the end of the application, custom modifications are not supported. |
|access |string |No |Network type, drop library is network_type. |
|carrier |string |No |Operator type, drop library is network_carrier. |
|platform |string |No |platform type |
|os_name |string |No |Client side system, only allowed to set to "ios", "android", "web", "wap", "mac", "windows", "linux", "ipad", "iphone", other values will be resolved to unknown. |
|os_version |string |No |Client side system version number |
|device_model |string |No |Equipment model |
|ab_sdk_version |string |No |AB experiment grouping information |
|traffic_type |string |No |traffic type |
|client_ip |string |No |Client side ip |
|custom |json object |No |Custom header field, single layer JSON map. The above fields are all reserved fields and cannot be used. Custom event public properties are placed here and are displayed under any_event events. |
|region |string |No |Country in the region (system settings), us, etc., (put in custom) |
|language |string |No |Language (system settings), en, etc., (put in custom) |
|app_region |string |No |Country (app settings), us, etc., (put in custom) |
|app_language |string |No |Language (app settings), en, etc., (put in custom) |
|timezone |string |No |Time zone, \-12~ 12, (put in custom) |
|utm_source |string |No |promotion source |
|utm_campaign |string |No |promotional activities |
|utm_medium |string |No |promotion media |
|utm_content |string |No |promotional content |
|utm_term |string |No |promotion keywords |


<span id="abbab952"></span>
## **2.5 Format of events**


|Field |Type |Required |Description |
|---|---|---|---|
|event |string |Yes |event name |
|params |string |Yes |Event parameters, single layer json map |
|local_time_ms |long |Yes |unix_timestamp (ms) |


<span id="381006f8"></span>
# 3. HTTP Response Format


|Status code |Return information |Meaning |
|---|---|---|
|200 |{"message":"success", "sc": num}<br><br>Num is the number of successes |Success, return the number of successful events, view the event reporting format for failures, and return num = 0 for all errors. |
|400 |header/user/events empty error.<br><br>get/invalid appid error. |Request format error, see X\-MCS\-AppKey and header, user definition. |
|400 |not found app_key and not found app_id |The request is not accompanied by an X\-MCS\-AppKey, and there is no app_id in the header. |
|400 |parse POST request error! err: can not parse JSON:... |Request parameter parsing error, unable to parse JSON. |
|413 |too many element in one request! length: xx , only allow 50 |The request array is too long (only for the/json/list interface, limit 50) |
|413 |too many events in one request! length: 89 , only allow 50 |Too many events in the request (limit 50) |
|500 |UserAgent is not allowed |Invalid User\-Agent for HTTP headers, including msnbot, Sosospider, Sosoimagespider, Sogou web, spider, Googlebot, Baiduspider, 360Spider, YoudaoBot, YandexBot, EasouSpider, Mediapartners\-Google, APIs\-Google, AdsBot\-Google, JikeSpider, MJ12bot, ia_archiver, Rogerbot, exabot, DOCOMO Sprider, python\-requests, HttpClient, Go\-http\-client, Python\-urllib, gohttp, curl/, Surf/, Scrapy |


<span id="18b57ca8"></span>
# 4. Request example

<span id="b6257bac"></span>
## 4.1 /v2/event/json interface

```json
curl -X POST -H "Content-Type: application/json" -H "X-MCS-AppKey: 12345678key" -d '{"user": {...}, "header":{...}, "events":{...}}' https://gator.volces.com/v2/event/json
```


Request body:

```json
{
    "user": {
         // It is recommended to first report the user_unique_id of the user on the client side, and then use it on the server side
        "user_unique_id": "74481585297"   //user unique identifier
    },
    "header": {
        "ab_sdk_version": "91223,83097",   //AB experiment vid
        "app_channel": "App Store",    //App channel
        "app_name": "news_article",    //App nameame
        "app_package": "com.ss.android.article.news",   //App package name
        "app_version": "5.1.3",        //App versionersion
        "client_ip": "10.100.1.1",     //client side ip addressside ip address
        "device_model": "SM-G9250",    //device type
        "os_name": "Android",          //operating system
        "os_version": "6.0.1",         //operating system version
        "traffic_type": "app",
        "custom":"{\"A\":\"a\"}"         //event public property
    },
    "events": [
        {
            "ab_sdk_version": "91223,83097",   //AB experiment vid
            "event": "test_go_detail",    //event name
            "params": "{\"paramName\":\"a\"}",    //event property
            "local_time_ms": 1489573628001   //Timestamp of the event occurrence time
        }
    ]
}
```


Description

local_time_ms: This is the millisecond timestamp that identifies the moment this event occurred.

<span id="ca6e9b35"></span>
## 4.2 /v2/event/list interface

```json
curl -X POST -H "Content-Type: application/json" -H "X-MCS-AppKey: 12345678key" -d '[{"user": {...}, "header":{...}, "events":{...}}]  https://gator.volces.com/v2/event/list
```


Request body:

```json
[{
    "user": {
        "user_unique_id": "74481585297"   //user unique identifier
    },
    "header": {
        "ab_sdk_version": "91223,83097",   //AB experiment vid
        "app_channel": "App Store",    //App channel
        "app_name": "news_article",    //App name
        "app_package": "com.ss.android.article.news",   //App package name
        "app_version": "5.1.3",        //App version
        "client_ip": "10.100.1.1",     //client side ip address
        "device_model": "SM-G9250",    //device type
        "os_name": "Android",          //operating system
        "os_version": "6.0.1",         //operating system version
        "traffic_type": "app"
    },
    "events": [
        {
            "event": "test_go_detail",    //event name
            "params": "{\"paramName\":\"a\"}",    //event property
            "local_time_ms": 1489573628001   //Timestamp of the event occurrence time
        }
    ]
}]
```


Description

local_time_ms: This is the millisecond timestamp that identifies the moment this event occurred.

<span id="7066adfe"></span>
# 5. Report user attributes

Attention

This section applies only to the [SaaS Cloud Native] and [Privatized] versions.

User properties are reported through special events, and user properties can be modified by setting the following events:


|Event name |Function |
|---|---|
|__profile_set |Set user properties. |
|__profile_set_once |Set the user property, the property is set_once, and cannot be changed after setting. |
|__profile_increment |Increases the value of a numeric class user property. |
|__profile_unset |Delete user attributes. |
|__profile_append |Increases the element of an array class user property. |
|__profile_remove |Removes the elements in the array class user properties. |


<span id="e1bd37ab"></span>
## 5.1 Reporting user attributes

User attributes are placed in `params`, example request, the function is to set a user attribute age, delete a user attribute name, body:

```json
{
    "user": {
        "user_unique_id": "74481585297"   //user unique identifier
    },
    "header": {
        "ab_sdk_version": "91223,83097",   //AB test vid
        "app_channel": "App Store",    //App channel
        "app_name": "news_article",    //App name
        "app_package": "com.ss.android.article.news",   //App package name
        "app_version": "5.1.3",        //App version
        "client_ip": "10.100.1.1",     //client side ip address
        "device_model": "SM-G9250",    //Equipment model
        "os_name": "Android",          //operating system
        "os_version": "6.0.1",         //operating system version
        "traffic_type": "app"
    },
    "events": [
        {
            "event": "__profile_set",    //operation name
            "params": "{\"age\": 10}",    //set properties
            "local_time_ms": 1489573628001   //the timestamp of the event
        }，
        {
            "event": "__profile_unset",    //operation name
            "params": "{\"name\":\"tom\"}",    //set properties
            "local_time_ms": 1489573628001   //the timestamp of the event
        }
    ]
}
```


<span id="3313502a"></span>
## 5.2 Bulk reporting of user attributes

When you need to report user attributes in batches, you can add a special field __uuid_list in params to achieve, __uuid_list is a list of user_unique_id, other fields in params except __uuid_list fields are used as attributes of all user_unique_id in this __uuid_list, refer to the code:

```matlab
{
    "user": {
        "user_unique_id": "user1"
    },
    "header":{"app_name":"init","app_id":"10000000"},
    "events": [
        {
            "event": "__profile_set",
            "params": {
                "__uuid_list": ["user1", "user2", "user3", "user4"],
                "age":20
            }
        }
    ]
}
matlab
```


Attention

This list is limited to 1000 users per report.

<span id="d2ec43f5"></span>
## 5.3 Verify the reported user attributes

You can view data for specific users in the behavioral profiling page.

<span id="6809fbbe"></span>
# 6. Import historical data

Attention

[SaaS version] Historical data import can only be viewed the next day, and the [SaaS cloud native] and [privatization] versions can be viewed in real time.

If the client side of the data is longer than seven days, it cannot be imported normally. To import historical data, you need to add the identity `__is_history`of the historical data in the `custom`field of the `header`, and the attribute value is set to string `"true"`. Examples of reporting are as follows:

```json
[{
   "user": {
       "user_unique_id": "74481585297"   //user unique identifier
   },
   "header": {

       "custom": {
              "__is_history": "true" //Import the historical data identifier, the default is false;
       }
   },
   "events": [
       {
           "event": "test_go_detail",    //event name
           "params": "{\"paramName\":\"a\"}",    //event property
           "local_time_ms": 1489573628001   //the timestamp of the event
       }
   ]
}]
```


Explain

local_time_ms: This is the millisecond timestamp, which identifies the time when this event occurred. Note that the time is not a derivative.

After the report is completed, you need to click Refresh Data on the interface to check the reported historical data.

<span id="06903b55"></span>
# 7. Restrictions on reporting data

Please refer to the documentation:


* Data reporting restrictions in data format documents: [Supported Data Formats (Custom Events/Properties)](https://docs.byteplus.com/docs/DataTester/Supported-Data-Formats-Custom-Events-Properties).


<span id="468327cc"></span>
# 8. Verify that the data is successfully reported

If you know a specific user_unique_id, you can check in behavioral details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d3f3ca8dcd240f7817dcc101bda9ac2~tplv-goo7wpa0wc-image.image) </span>
