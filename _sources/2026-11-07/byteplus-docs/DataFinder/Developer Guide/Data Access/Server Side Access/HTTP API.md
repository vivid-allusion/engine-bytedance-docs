---
title: "HTTP API"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/HTTP_API"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The http interface growth analysis platform reported by the server level is opened by default for you. If the application you access is not opened, please contact the customer success manager to solve it;</div>


* <div data-tips="true" data-tips-type="warning">Before using this feature, it is recommended that you read <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification">Supported Data Formats and Event/Property Classification</a>and <a href="https://docs.byteplus.com/docs/DataFinder/Data_Governance_Dashboard">Data Governance Dashboard</a>document the instructions to avoid reporting details.</div>



<span id="_1-请求接口"></span>
# 1. Request interface


|**Environment** |**URL** |**Methord** |
|---|---|---|
|SaaS\-Cloud Native Overseas (Johor) |* Single data upload: https://gator.uba.ap\-southeast\-1.bytepluses.com/v2/event/json<br><br>* Bulk data upload (up to 50 per batch): https://gator.uba.ap\-southeast\-1.bytepluses.com/v2/event/json | |
|Privatization |* Single data upload: https://${host}/v2/event/json<br><br>* Batch data upload (up to 50 pieces per batch): https://${host}/v2/event/list<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">${Host}: Private deployment The domain name applied by the customer for event tracking data reporting, please replace it according to the actual domain name. After the customer domain name is updated, the reported path address also needs to be updated synchronously.</div><br> ||


<span id="_2-请求规范"></span>
# 2. Request specifications


1. The header of the request contains "Content\-Type: application/json" and "X\-MCS\-AppKey" as the identifier of the app.

   * When reporting through the HTTP API, if you use code and some tools, the user\-agent field will be automatically attached to the request header (information used to identify the client side software that initiates the request, which does not affect the result of calling the API).

   * If sending manually may prompt that User\-Agent is not allowed, you need to manually add the User\-Agent field to the request header. In this scenario, you can randomly fill in the value of a user\-Agent field, or use tools like Mail carrier to call the API first and copy the user\-Agent value.

2. The body of the request contains three parts: user, header, and event, among which the header is the header of the event tracking data itself;

3. The number of single upload events is recommended to be controlled within 20, and more than 50 will be reported to 413;

4. If the upload uses the/v2/event/list interface, it is recommended to control the number of jsons within 20, and more than 50 will report 413.


<span id="_2-1-请求header"></span>
## 2.1 Request headers


|Field |Type |Explain |
|---|---|---|
|Content\-Type |string |application/json |
|X\-MCS\-AppKey |string |APP Key of your application |


<span id="_2-2-请求body"></span>
## 2.2 Request body


|Field |Type |Explain |
|---|---|---|
|user |object |The user property dictionary, which is used to set the user's unique identity, as detailed in section 2.3 below. |
|header |object |Header property dictionary, used to set global public properties, is a one\-to\-many relationship with events, and a batch of reported events will correspond to the same header public property. See section 2.4 below for details. |
|events |[object] |Events list, used to set the list of all events reported this time. Events is the main information carrier for all types of data reporting. Generally, each event contains:<br><br><br>* Event: event name, the **type name of some scenes to report special data**<br><br>* Params: data content, the content is json string or Json escape string. The key value of parmas is different in each reported event. In the behavior event report, it is the event property, the preset property and its corresponding value.<br><br><br>See section 2.5 below for details. |


<span id="_2-3-user格式"></span>
## 2.3 Format of users

The user part is used to set the unique identity of the user. The current DataFinder supports the use of device_id, user_unique_id, and ssid three ID identification devices and users. At the same time, SaaS\-cloud native and privatized environments support the use of multi\-ID criteria to more accurately identify a user. For more details on the user's unique identity, please refer to [Supported User Unique Identifiers](https://docs.byteplus.com/docs/DataFinder/Supported_User_Unique_Identifiers) the following fields for reporting the user's unique identity using the HTTP API.


|Field |Type |Required |Explain |
|---|---|---|---|
|user_unique_id |string |Yes |The unique identity of the user needs to ensure that the same user is globally unique within the application, that is, it needs to be consistent with the client side report. |
|user_unique_id_type |string |No |If the reported application involves multiple ID criteria, the reported ID type (determined by the ID Mapping scheme) needs to be filled in this field. If this field is enabled, the user_unique_id to report the specific value of the type id. (Example: user_unique_id_type is phone, user_unique_id is 183xxxxxxxx mobile phone number). |
|device_id |string |No |App\-side device identification, note that it must be purely digital. |
|web_id |string |No |Web device identification, note that it must be purely digital. |


<span id="_2-4-header格式"></span>
## 2.4 header format


|Field |Type |Required |Explain |
|---|---|---|---|
|app_name |string |No |The English name of the application |
|app_package |string |No |package name |
|app_channel |string |No |App distribution channel |
|app_version |string |No |App version, three segments separated, such as 1.0.1 |
|app_platform |string |No |At the end of the application, custom modifications are not supported. |
|access（SaaS）<br><br>network_type (privatization) |string |No |Network type, drop library is network_type. |
|carrier（SaaS）<br><br>network_carrier (privatization) |string |No |Operator type, drop library is network_carrier. |
|platform |string |No |platform type |
|os_name |string |No |Client side system, only allowed to set to "ios", "android", "web", "wap", "mac", "windows", "linux", "ipad", "iphone", "harmonyos", other values will be resolved to unknown. |
|os_version |string |No |Client side system version number |
|device_model |string |No |Equipment model |
|ab_sdk_version |string |No |AB experimental grouping (vid) information |
|traffic_type |string |No |Traffic type, not recommended for reporting |
|client_ip |string |No |Client side ip |
|custom |json object |No |Custom header field, single layer JSON map. The above fields are all reserved fields and cannot be used. Custom event public properties are placed here. |
|region |string |No |Country in the region (system settings), us, etc |
|language |string |No |Language (system settings), en, etc |
|app_region |string |No |Country (app settings), us, etc |
|app_language |string |No |Language (app settings), en, etc |
|timezone |string |No |Time zone, \-12~ 12 |
|utm_source |string |No |promotion source |
|utm_campaign |string |No |promotional activities |
|utm_medium |string |No |promotion media |
|utm_content |string |No |promotional content |
|utm_term |string |No |promotion keywords |


<span id="_2-5-event格式"></span>
## 2.5 Format of events


|Field |Type |Required |Explain |
|---|---|---|---|
|event |string |Yes |event name |
|params |string |Yes |Event properties, single layer JSON map |
|local_time_ms |long |Yes |unix_timestamp (ms) |


<span id="_3-http-response-格式"></span>
# 3. HTTP Response Format


|Status code |Return information |Meaning |
|---|---|---|
|200 |* SaaS\-Cloud Native: |Success, among which:<br><br><br>* Num: The number of successful events reported.<br><br>* E: To report the number of failed events, the failed view events reporting format.<br><br>* In a SaaS\-cloud native environment:<br><br>   * The returned Type value is the interface type of the request to the end, which is meaningless and you don't need to pay attention.<br><br>   * The returned server_time is the timestamp value of the reported data. |
|400 |header/user/events empty error.<br><br>get/invalid appid error. |Request format error, see X\-MCS\-AppKey and header, user definition. |
|400 |not found app_key and not found app_id |The request is not accompanied by an X\-MCS\-AppKey, and there is no app_id in the header. |
|400 |parse POST request error! err: can not parse JSON:... |Request parameter parsing error, unable to parse JSON. |
|413 |too many element in one request! length: xx , only allow 50 |The request array is too long (only for the/json/list interface, limit 50) |
|413 |too many events in one request! length: 89 , only allow 50 |Too many events in the request (limit 50) |
|500 |UserAgent is not allowed |Invalid User\-Agent for HTTP headers, including msnbot, Sosospider, Sosoimagespider, Sogou web, spider, Googlebot, Baiduspider, 360Spider, YoudaoBot, YandexBot, EasouSpider, Mediapartners\-Google, APIs\-Google, AdsBot\-Google, JikeSpider, MJ12bot, ia_archiver, Rogerbot, exabot, DOCOMO Sprider, python\-requests, HttpClient, Go\-http\-client, Python\-urllib, gohttp, curl/, Surf/, Scrapy |


<span id="_4-请求示例"></span>
# 4. Request example

<span id="_4-1-v2-event-json接口"></span>
## 4.1 /v2/event/json interface

```json
curl -X POST -H "Content-Type: application/json" -H "X-MCS-AppKey: 12345678key" -d '{"user": {...}, "header":{...}, "events":{...}}' https://gator.volces.com/v2/event/json
```


Request body:

```json
{
    "user": {
            //It is recommended to report the user's user_unique_id on the client side first, and then use it at the server level
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
        "traffic_type": "app",
        "custom":"{\"A\":\"a\"}"         //event public property
    },
    "events": [
        {
            "ab_sdk_version": "91223,83097",   //AB test vid
            "event": "test_go_detail",    //event name
            "params": "{\"paramName\":\"a\"}",    //event property
            "local_time_ms": 1489573628001   //the timestamp of the event
        }
    ]
}
```


<span id="_4-2-v2-event-list接口"></span>
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
            "event": "test_go_detail",    //event name
            "params": "{\"paramName\":\"a\"}",    //event property
            "local_time_ms": 1489573628001   //the timestamp of the event
        }
    ]
}]
```


The following Tips are suitable for the interfaces mentioned in Section 4:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">local_time_ms: This is the millisecond timestamp that identifies the moment this event occurred.</div>


**Multi\-ID criteria reporting** : If the reporting application uses a multi\-criteria ID, you need to report the user information (user field) in addition to user_unique_id, while carrying user_unique_id_type, the example code is as follows.

```JSON
"user": {
        "user_unique_id": "13388999999"   //user unique identifier value
        "user_unique_id_type": "phone"   //The value is id code, lowercase, and the specific value is provided by the ID involving the scheme.
    }
```


<span id="_5-上报用户属性"></span>
# 5. Report user properties

<span id="_5-2-批量上报用户属性"></span>
## 5.2 Verify the reported user properties

You can view user\-specific data in the behavior review page, and if it is a large amount of data, you can analyze user properties in the event analysis.

<span id="_6-上报业务对象属性"></span>
# 6. Report business object properties

<span id="_6-1-创建业务对象"></span>
## 6.1 Creating business objects

&nbsp;

&nbsp;

<span id="_6-2-上报关联事件"></span>
## 6.2 Reporting related events

The created item object needs to be associated with an event before it can be used.

<span id="e3fb0411"></span>
### Prerequisite

You have created a business dimension on the **Data Management** \> **Business Dimensions** page; and you have completed the above steps: Create Business Object.

<span id="3d38bc60"></span>
### Configuration item and event association: (recommended) method 1 Interface configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The SaaS\-cloud native environment supports directly configuring the associated event properties on the <strong>Data Management</strong> \> <strong>Business Dimension</strong> page. This method can flexibly associate items with events. This method is recommended.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03a3e303dc2f4c9395684bef586d1024~tplv-goo7wpa0wc-image.image) </span>

You can set event properties associated with a business dimension when you create or edit a business dimension .

<span id="758d0d3f"></span>
### Configure item association with event: Mode 2 code reporting

You can use the code event tracking report to report the association between the item and the event. When configuring data access, you need to configure the business dimension and the association rules of the event data at the same time, that is, configure the item id value of one or more specific items to the preset property of the event `params.__items`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the SaaS scenario, a single reported event can currently support up to three items. As shown in the following example, a new_order event can only have three different item names.</div>


The following sample code demonstrates how to associate **two** created business dimensions, sku and order, with event new_order. `__items`Preset properties for events for reporting business dimensions only.

Examples are as follows:

```json
...
"event": "new_order",
"params": {
    "__items": "[{\"sku\":[{\"id\":\"sku_id_1\"},{\"id\":\"sku_id_2\"}]},{\"order\":[{\"id\":\"order_id_1\"},{\"id\":\"order_id_2\"}]}]",
    ...
},
...
```


`__items`is a `json`object converted to a `string`in the format:

```json
[
    {"item_name_1": [
        {"id": "id_value_1"},
        {"id": "id_value_2"},
        ...
    ]},
    {"item_name_2": [
        {"id": "id_value_1"},
        {"id": "id_value_2"},
        ...
    ]}
]
```


`item_name_1`is the `business dimension name`defined in the previous step, such as order; `id_value_1`, `id_value_2`is the value of item id, such as order number id1, order number 2.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the item data is not defined when the event data is on (i.e. no business dimension is added to data management), the association does not take effect and item analysis cannot be used normally.</div>


<span id="_7-导入历史数据"></span>
# 7. Import historical data

If the client side of the data is longer than seven days, it cannot be imported normally. To import historical data, you need to add the identity `__is_history`of the historical data in the `custom`field of the `header`, and the property value is set to string `"true"`.

Examples of reporting are as follows:

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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">local_time_ms: This is the millisecond timestamp, which identifies the time when this event occurred. Note that the time is not a derivative.</div>


After the report is completed, you need to click Refresh Data on the interface to check the reported historical data.

<span id="_8-上报数据限制"></span>
# 8. Restrictions on reporting data

Please refer to the documentation:


* Data reporting restrictions in data format documents: [4. Data format description](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification#_4-%E6%97%A5%E5%BF%97%E7%BB%93%E6%9E%84).

* Data governance dashboard: [Data Governance Dashboard](https://docs.byteplus.com/docs/DataFinder/Data_Governance_Dashboard).


<span id="_9-验证数据上报成功"></span>
# 9. Verify that the data is successfully reported


* Method 1: You can directly query in **Analysis Tools \> Advanced Analysis \> SQL Custom Query** .

* Method 2: If you know a specific user_unique_id, you can check in the behavioral scrutiny.

* Method 3: You can perform query analysis on the event analysis page.
