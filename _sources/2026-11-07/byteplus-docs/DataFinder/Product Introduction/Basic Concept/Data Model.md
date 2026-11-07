---
title: "Data Model"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Model"
---

The basic data model includes **event + user model** and **analysis model**, which are described in detail below.

<span id="事件-用户模型"></span>
# Event + user model


* **Events:**  Users will experience a series of behavioral interactions when visiting touchpoints such as websites, APPs, Mini Programs, official accounts, etc., such as total page browsing, product purchase, customer service consultation, button clicking... In order to facilitate collection, sorting, and statistical analysis, we call one or a class of behaviors "events". Examples of a short video app event: start playing videos, collect videos, share videos, comment on videos, follow accounts, app launch, app exit, etc.

* **Event attributes:**  When the event is triggered, the form and location of the event can be collected to describe the event information, which is called event attributes. For example, the event attribute that starts playing a video can be an attribute related to the device the user is using, such as information about the operating system, software version, software channel, Internet Protocol Address, and so on. It can also be a business\-related video ID, video name, video classification, video tag, etc.

   Overall, an event involves five basic elements: who, when, where, how, and what behavior occurs. The description of the five basic elements can be called event attributes. For example:

   
   |Event |Event properties |
   |---|---|
   |Pay |Product name, product ID, product classification, product unit price, payment amount, purchased product quantity, etc |
   |Read the article for details |Content name, content ID, content classification, content tags, etc |
   |Search |Search terms, whether to use historical terms, whether to use hot words, etc |
   |Get a coupon |Coupon ID, coupon name, discount amount, etc |
   |Follow |Follow user IDs, follow user nicknames, etc |
   

* **Transaction table: The** database & table used to store event data records is'transaction table '.

* **User: The** subject of the event behavior.

* **User Attributes:** 

   * Attributes of the user's own state that are independent of behavior, such as age, gender, etc.

   * Attributes related to behavior that do not change or change frequently, such as registration time, VIP level, last payment time, etc.

* **User table:**  The \*\*\*\* database & table used to store user data records is a 'user table'.

   The transaction table and the user table are associated by BytePlus to generate a unique SSID for each user.

* **Event tracking:**  In order to quickly, efficiently and accurately obtain user behavior operation or behavior operation result data, generally through client side or server level SDK collection, or asynchronous import form, according to the requirements of data application, report data. Complete data collection through event tracking and store the data in the transaction table\-user table model.


<span id="0ae144ed"></span>
# Event properties, event public properties, user properties


|**Event/Attribute Classification** ||**Business Meaning Statement** |**SDK integration and reporting instructions** |
|---|---|---|---|
|Event public property |Preset event public properties |General properties that are reported for each event preset by the system. For example, the device information class field reported by the Finder SDK. |* SDK integration:<br><br>   * Preset event public properties: When integrating the SDK, you need to confirm that the preset event collection switch has been turned on.<br><br>   * Custom event public properties: You need to configure the custom event public properties into the SDK integration code. Usually, the public properties of custom events are configured in the public field of the SDK code \- the header related field. For detailed configuration methods, please refer to the SDK integration documentation of the corresponding collection end.<br><br>* Reporting: When the collected data is reported to the DataFinder, the event public properties (including presets and customizations) are stored in the public field header for reporting, and are not explicitly associated with an event. |
||Custom event public properties |Customer\-defined event public properties other than the preset event public properties. ||
|Events and event properties |Preset events and event properties |System preset event tracking events and event properties. |* SDK integration:<br><br>   * Preset events and event properties: When integrating the SDK, you need to confirm that the preset event collection switch has been turned on.<br><br>   * Full event tracking event and full event tracking event properties: When integrating the SDK, confirm that the full event tracking function switch is turned on.<br><br>   * Custom events and event properties: You need to configure custom events and event properties into the SDK integration code. Usually custom events and event attributes are configured through the event\-related methods of the SDK integration code. For detailed configuration methods, please refer to the SDK integration documentation of the corresponding collection end.<br><br>* Reporting: When an event is triggered, event attribute data (including presets and customizations) is reported with the event, and there is an association between the event and the event attribute. |
||Full event tracking events and full event tracking event properties |A type of event tracking event preset by the system. ||
||Custom events and event properties |Customer\-defined events and event properties other than preset events and event properties. ||
|User attributes |Preset user properties |System\-preset properties that describe the user's own state. |* SDK integration:<br><br>   * Preset user properties: When integrating the SDK, turn on the preset event collection switch.<br><br>   * Custom user properties: Custom user properties need to be configured into the SDK integration code. Usually, custom user attributes are configured through the profile\-related method of the SDK integration code. For detailed configuration methods, please refer to the SDK integration document of the corresponding collection end.<br><br>* Reporting: When the collected data is reported to the DataFinder, the user attributes are stored in the public field user for reporting and are not explicitly associated with an event. |
||Custom user properties |Customer\-defined user properties other than the preset user properties. ||


Example of reporting data:

```TypeScript
{
    "events": [
        {  //Reported events and event attributes
            "event": "report-core",
            "params": "{"timePoints":8041,"pageChanged":false,"url":"https://datarangers-onpremise.volces.com/datafinder/project/1/overview","index":6,"event_index":1723194789910}",
            "local_time_ms": 1723194773504,
            "is_bav": 1,
            "session_id": "dc3b61d7-de7d-4f8d-b5bd-2f70******"
        },
        {
            "event": "report-core",
            "params": "{"timePoints":7963,"pageChanged":false,"url":"https://e168-2-169.datarangers-onpremise.volces.com/datafinder/project/1/overview","index":3,"event_index":1723194789909}",
            "local_time_ms": 1723194773426,
            "is_bav": 1,
            "session_id": "dc3b61d7-de7d-4f8d-b5bd-2f707*******"
        }
    ],
    "user": { //reported user attributes
        "user_unique_id": "1",
        "web_id": "73742566315817*****"
    },
    "header": { //Public attributes of the reported event
        "app_id": 666***,
        "os_name": "mac",
        "os_version": "10_15_7",
        "device_model": "Macintosh",
        "language": "zh-CN",
        "platform": "web",
        "sdk_version": "5.1.25",
        "sdk_lib": "js",
        "timezone": 8,
        "tz_offset": -28800,
        "resolution": "2304x1296",
        "browser": "Chrome",
        "browser_version": "126.0.0.0",
        "referrer": "",
        "referrer_host": "",
        "width": 2304,
        "height": 1296,
        "screen_width": 2304,
        "screen_height": 1296,
        "tracer_data": "{"$utm_from_url":1}",
        "custom": "{"product_name":"DataFinder","op_project_id":1,"op_project_name":"Q2 kit linkage project","org_id":1,"org_name":"defaultgroup","overview_org_id":1,"custom_module_name":"overview"}"
    },
    "local_time": 1723194773
}
```


<span id="分析模型"></span>
# Analysis model


* **Dimension:**  In the user behavior analysis system, the dimension is the event attribute and user attribute, such as "city" is a dimension, including Beijing, Shanghai, Shenzhen, Guangzhou, etc.; another example is "operating system" including ios, android; "channel" includes app store, Huawei app store, Xiaomi app store, etc.

* **Indicator:**  is a quantitative value\*\*.\*\* Including UV, PV, number of times per capita, duration, click through rate, penetration rate, retention rate, success rate, etc. Indicators can be divided into attributes data and composite indicators, such as UV, PV, and orders.
