---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters_Query_Analysis"
---

<span id="01b042b5"></span>
# 1. Overview

In order to better integrate with enterprise data products and better leverage the value of data, DataFinder provides the ability to conduct secondary development based on this product by opening the OpenAPI. You can obtain metric data by calling the OpenAPI for integration in other data products.

<span id="fba62137"></span>
# 2. API List

<span id="ef77bb48"></span>
# 3. How to quickly build a DSL

<span id="7693e1de"></span>
## 3.1 Obtain the DSL for page queries (recommended)

First open the browser's developer tools (shortcut F12), then configure the query conditions, view the page's `datafinder/api/v1/analysis`request, the body of the request is the DSL of the query, you can directly copy and use.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_eee3e956b032e78bb7af483650f8212d) </span>

<span id="1681cd60"></span>
## 3.2 Using DSLBuilder provided by OpenAPI

For details, please refer to the OpenAPI SDK for each language version.

<span id="8af6aa94"></span>
# 4. DSL structure description

<span id="6d573d74"></span>
## 4.1 Overall structure

```json
{
    "version": 3, # version number
    "app_ids": [164***], # query app unique identifier
    "use_app_cloud_id": True, # use app cloud unique identifier
    "resources": [ # project information, use this field in project and multiple Apps, this field is prior to app_ids
        {
            "project_ids": [2xxxx], # project id
            "subject_ids": [1], # subject id, default is 1, which is used to specify the subject that needs to be analyzed within the project.
            "app_ids": [], # specific apps in the project. When it is empty, it means to analyze all apps in the project.
        }
    ],
    "periods": [ # Definition of query time range
        {
            "granularity": "day", # time granularity, minute/ hour/ day/ week/ month
            "type": "last", # time rule, last x days or time range
            "last": { # last x days definition
                "amount": 5, # query quantity
                "unit": "day" # query unit
            },
            "timezone": "Asia/Shanghai" # time zone
        }
    ],
    "content": {
            "query_type": "event", # query type
            "profile_groups_v2": [], # public property group
            "profile_filters": [], # public property filter
            "queries": [ # query definition
                [
                    {
                        "event_type": "origin", # event type, raw event, vitual event, circle event
                        "show_name": "active user quantity", # query name
                        "event_name": "app_launch", # event name
                        "groups_v2": [], # event group
                        "filters": [], # event filters
                        "show_label": "active_user", # result label
                        "event_indicator": "event_users" # indicator name
                    }
                ]
            ],
            "option": { # query optional parameters
                "skip_cache": False # do not skip cache
            }
        }
}
```


<span id="3f2c8535"></span>
## 4.2 Field details

DSL (Domain Specific Language) is simply a JSON\-formatted text to flexibly define complex query requirements.

<span id="93d6673d"></span>
### 4.2.1 top structure

```yaml
{
  "version": 3,             #DSL version, all 3 in this document
  "app_ids": [],            #Target app, supports multiple
  "use_app_cloud_id": true, #app_ids is app_cloud_id in the parameter. Please set to true, false for internal use only
  "resources": [{}],        #Project information, use this field in projects and multi-application, this field has higher priority than app_ids
  "periods": [{}],          #Query time period, support multiple
  "content": {},            #The specific query content field, one is passed with contents, and the structure is the same
  "contents": [{},{}], 
  "option": {},             #JSON format data, request related option parameters, different queries vary
  "show_option": {}         #JSON format data, return as-is in the result
}
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|version |int |The versions of DSL are all 3 in this document. |Yes |
|app_ids |int array |Target app, supports multiple. |app_ids and resources 1 |
|use_app_cloud_id |boolean |Specifies whether app_ids parameter is app_cloud_id. Please set it to true, false for internal use only. |No |
|resources |Array of JSON |Specify the project information to be analyzed, use this field in projects and multi\-application, this field has higher priority than app_ids |app_ids and resources 1 |
|periods |Array of JSON |Represents the time interval of the query and is an array that supports multiple time interval queries. See the **4.2.2 periods field** section below for the value field and format requirements for periods. |Yes |
|content |json |For the specific query content field, when there is only one query content json, use content; when there are multiple query content json, use contents. Format requirements and field descriptions are detailed in the **4.2.3 contene fields** section below. |Yes |
|contents |JSON array ||Yes |
|option |json |Request the relevant option parameters, which vary from query to query. |No |
|show_option |json |It is returned as it is in the result, and the front\-end display is used without affecting the query results. |Yes |


<span id="bb69c16f"></span>
### 4.2.2 Resources field

Resources represents querying project information, which requires:

```JSON
 [
    {
        "project_ids": [2xxxx], 
        "subject_ids": [1],
        "app_ids": [],
    }
]
```


Field description:


|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|project_ids |int array |Project id, currently only one is supported. |Yes |
|subject_ids |int array |The main ID of the analysis, multiple are supported. The main ID of the general project defaults to 1. |Yes |
|app_ids |int array |The specific application under the project that needs to be analyzed is empty\-time, indicating all applications under the analysis project |No |


<span id="b9a66aa9"></span>
### 4.2.3 periods field

Period is the time interval that the field represents the query, which is an array, and supports multiple time interval queries. Taking the event analysis query as an example, the periods field corresponds to the operation interface of the product console as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d360b866ef5b4ffe93fa10c8e3094035~tplv-goo7wpa0wc-image.image) </span>

Periods field format and field description, value examples are as follows.


* Field format

   ```json
   [{
     "type": "",
     "last": {
       "unit":"",
       "amount":int
     },
     "range": [int,int]
     "granularity": "",
     "timezone": "Asia/Shanghai",
     "interval": int,
     "real_time": boolean,
     "week_start": int
   }]
   ```
   

* Field description

   * Time range related parameters

      
      |**Field** |**Value and meaning** |**Is it necessary** |**Example** |
      |---|---|---|---|
      |**type** |Type of time frame. The enumeration value is:<br><br><br>* Range: range query<br><br>* Last: Recently<br><br>* Today: Today<br><br>* past_range: How many days have passed? |No |Default range |
      |**range** |Valid when type is range. Indicates that the time range is a specific period of time, which is an absolute time range. An integer array of length 2, the array values represent the start and end times, respectively, and the value is the time difference between 0:00 on January 1, 1970, in seconds.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">"Granularity": When "month", the data of the current month is automatically completed, and the range set at this time will be invalid. For example, when the time range is set to 2024\-01\-01 to 2024\-03\-05, "granularity": "month" returns data 2024\-01\-01 to 2024\-03\-31.</div><br> |Required parameter when type is range |```JSON```<br>```{range: [1586102400, 1588780799]}```<br> |
      |**last** |Type is valid when last. Represents a time range of the last few days, which is a time range of relative time. The value is in JSON format and contains the following fields:<br><br><br>* Amount: indicates the quantity<br><br>* Unit: represents the unit, supports day/week/month/year. |Required parameter when type is last |```JSON```<br>```last:{"unit":"day","amount":7}```<br> |
      |**spans** |Type is valid when past_range, indicating that the time range is in the past few days. The value is a list value that contains two list values, the first representing the start time and the second representing the end time. The structure of each list is:<br><br>```JSON```<br>```"spans":[```<br>```    {```<br>```    "type": "",```<br>```    "timestamp/past": "",```<br>```    "offset":```<br>```    },```<br>```    {```<br>```    "type": "",```<br>```    "timestamp/past": "",```<br>```    "offset":```<br>```    }```<br>```]```<br><br><br>The value selection description is as follows:<br><br><br>* **Type:**  The time data type representing the time range of the past few days, the enumeration values include:<br><br>   * **Timestamp:**  Represents a specific point in time, when the start/end time is a fixed time, timestamp can be used.<br><br>   * **Past:**  What time in the past, when the start/end time is dynamic time, you can use past.<br><br>* **Timestamp:**  When the value of type is timestamp, it represents the specific time point of the start time or end time of the time range, and the format is timestamp type.<br><br>* **Past:**  takes effect when the type value is past, indicating how long in the past the start or end time of the time range is.<br><br>   * **Amount:**  indicates the quantity, the unit is day time, 0 represents today; 1 represents yesterday, and so on.<br><br>   * **Unit:**  means unit, supports day, week, month, year.<br><br>* **Offset:**  The offset of time in seconds. For example, when the time range is from 01:00 yesterday to 01:00 today, the offset of the start time is 3600, and the offset of the end time is 7199, which is similar to the configuration effect of the following product console interface.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb444ac53f014ef8902e4767a939abb2~tplv-goo7wpa0wc-image.image) </span> |Type is required when past_range |```JSON```<br>```"spans":[```<br>```    {```<br>```    "type": "past",```<br>```    "past": {```<br>```        "amount": 1,```<br>```        "unit": "day"```<br>```                },```<br>```    "offset":3600```<br>```    },```<br>```    {```<br>```    "type": "past",```<br>```    "past": {```<br>```        "amount": 0,```<br>```        "unit": "day"```<br>```                },```<br>```    "offset":7199```<br>```    }```<br>```]```<br> |
      

   * Time segmentation granularity related parameters, indicating what time granularity to summarize and display query results, similar to the X\-axis effect of the product console interface analysis chart.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1640f353d73740a98d4d6779a3577a0a~tplv-goo7wpa0wc-image.image) </span>

      
      |**Field** |**Value and meaning** |**Is it necessary** |**Example** |
      |---|---|---|---|
      |granularity |Granularity of time. Splits the specified time range according to time granularity. Enumeration value:<br><br><br>* All (without splitting, aggregating values)<br><br>* second<br><br>* minute<br><br>* five_minute<br><br>* ten_minute<br><br>* fifteen_minute<br><br>* thirty_minute<br><br>* hour<br><br>* day<br><br>* week<br><br>* month<br><br>* quarter<br><br>* year<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">"Granularity": When "month", the data of the current month is automatically completed, and the range set at this time will be invalid. For example, when the time range is set to 2024\-01\-01 to 2024\-03\-05, "granularity": "month" returns data 2024\-01\-01 to 2024\-03\-31.</div><br> |No |Default all |
      |week_start |When the granularity is a week, you can specify the start date of the week, for example, 5 means Friday to Thursday. |No |Default 1, Monday to Sunday. |
      |interval |Granularity of time. Split at a custom time granularity, in seconds, such as 130 seconds. |No |*  |
      |align_unit |Alignment unit (time range calibration unit), the default is the same as the value of granularity, enumeration value:<br><br><br>* second<br><br>* minute<br><br>* five_minute<br><br>* ten_minute<br><br>* fifteen_minute<br><br>* thirty_minute<br><br>* hour<br><br>* day<br><br>* week<br><br>* month<br><br>* quarter<br><br>* year |No |*  |
      

   * Other parameters

      
      |**Field** |**Value and meaning** |**Is it necessary** |**Example** |
      |---|---|---|---|
      |timezone |Time zone of the time range |No |Default Asia/Shanghai |
      |real_time |Whether it is a real\-time query, if true, only the real\-time library will be queried. This parameter is deprecated and does not require attention. |No |*  |
      

* Value example

   * Example 1

      ```JSON
      {
          "granularity":"day",
          "type":"range",
          "range":[1586102400, 1588780799],
          "timezone": "Asia/Shanghai"
          } 
      ```
      

   * Example 2

      ```JSON
      {
          "granularity":"day",
          "type":"last",
          "last":{"amount":7,"unit":'day'},
          "timezone": "Asia/Shanghai"
          } 
      ```
      

   * Example 3

      ```JSON
      {
          "granularity":"day",
          "type":"today",
          "timezone": "Asia/Shanghai"
          } 
      ```
      

   * Example 4

      ```JSON
      {
              "granularity": "all",
              "align_unit":"day",
              "type": "past_range",
              "spans":[
                  {
                    "type": "timestamp",
                    "timestamp": "1619798400",
                    "offset":3600
                  },
                  {
                      "type": "past",
                      "past": {
                              "amount": 1,
                              "unit": "day"
                      },
                      "offset":7199
                  }
              ]
              "timezone": "Asia/Shanghai"
      }
      ```
      


<span id="15db1cad"></span>
### 4.2.4 content field

The specific query content field, taking the event analysis query as an example, is similar to the following configuration function of the product console interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19f725585b6d4157b8bfe1948a82c729~tplv-goo7wpa0wc-image.image) </span>

The parameters and descriptions of the content field are as follows.

```json
{
  "profile_filters": [{}],     #filter condition, see profile_filters below for more details
  "profile_groups_v2": [],     #group condition, only support public properties, see profile_groups_v2 below for more details
  "orders": [],                #sort rule
  "query_type": "",            #query type, see query_type below for more details
  "queries": [[],[]],          #query, Two dimensional array. Different query types require different query arrays to be set. See queries below for more details
  "option": {},                #query option
  "page": {},                  #query page, limit related configuration
}
```


<span id="12df0735"></span>
### 4.2.5 content/profile_filters

Represents the filter conditions when querying, similar to the following interface configuration functions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b2079a4e7664efdbc112af2229f4af0~tplv-goo7wpa0wc-image.image) </span>

```json
[{
  "show_name": "1",
  "show_label": 1,
  "expression": {
    "logic": "and",
    "conditions": [{
      "property_name": "custom_server_gender",
      "property_type": "profile",
      "property_operation": "=",
      "property_values": ["1"]
    }]
  }
}]
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|show_name |string |Front\-end parameters do not affect query results, no need to pay attention |No |
|show_label |string |Front\-end parameters do not affect query results, no need to pay attention |No |
|expression |json |A filter expression for a query filter, including the filter conditions and the logic between multiple filter conditions. |Yes |
|logic |string |Logical relationship between multiple filter conditions, support: and/or. |Yes |
|conditions |JSON array |The specific query filter conditions support multiple filter conditions, and the format and field requirements of each query filter condition are shown in the **condition** below. |Yes |


<span id="a03a49e9"></span>
### 4.2.6 content/profile_filters/condition

Query filter criteria, format requirements and field descriptions for individual filter criteria.

```json
{
      "property_name": "custom_server_gender",
      "property_type": "profile/user_profile",
      "property_operation": "=",
      "property_values": ["1"]
 }
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|property_name |string |attribute name |No |
|property_type |string |Property types, enumeration values:<br><br><br>* Profile: user attributes, SaaS applicable<br><br>* event_param: Event Properties<br><br>* common_param: Event public properties<br><br>* Cohort: user grouping. |No |
|property_operation |string |Evaluate expressions, different property_type support different property_operation, all enumeration values are as follows:<br><br>```JSON```<br>```=```<br>```!=```<br>```is_null```<br>```is_not_null```<br>```in```<br>```not_in```<br>```>```<br>```>=```<br>```<```<br>```<=```<br>```contain```<br>```not_contain```<br> |Required when filter properties are used |
|property_values |String/int/float array |The value of the property's expression |Required when filter properties are used |


<span id="7302d05d"></span>
### 4.2.7 content/profile_groups_v2

Represents a grouping condition when querying, and only public properties are supported.

```json
"profile_groups_v2": [
    {
        "property_type":"profile",
        "property_name":"user_is_new"
    },
    {
        "property_type":"profile",
        "property_name":"os_name"
    }
]
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|profile_groups_v2 |JSON array |Represents the grouping criteria at query time as a JSON array containing the following fields:<br><br><br>* property_type: The attributes of the group, SaaS needs to be configured as profile .<br><br>* property_name: Public property name. |No |


<span id="e7952615"></span>
### 4.2.8 content/**query_type**


|**Field** |**Type** |**Field description** |**Is it necessary** |
|---|---|---|---|
|query_type |string |The analysis data type of the query, enumeration values:<br><br><br>* Event query: event<br><br>* Retention query: retention<br><br>* Transform query: funnel<br><br>* User path query: path_find<br><br>* Lifecycle Query: life_cycle<br><br>* Web query: web_session<br><br>* Topk query: event_topk<br><br>* LTV query: ltv<br><br>* Attribution query: behavior_attribution<br><br>* Ingredient query: composition<br><br>* Advertising inquiry: advertising<br><br>* Confidence level query: confidence |Yes |


<span id="bfe6ee30"></span>
### 4.2.9 content/**queries**

Query conditions, two\-dimensional arrays, different query types, need to organize the corresponding query arrays. Specific reference cases:

```json
{
  "event_name": "any_event",
  "event_id":1,
  "event_type": "origin",
  "show_name": "总次数", //total count
  "groups_v2": [],
  "filters": [],
  "show_label": "A",
  "event_indicator": "events",
  "measure_info": {}
}
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|event_name |string |event name |event_name and event_id must have one |
|event_id |int |event id ||
|event_type |string |Event type, currently supports three types<br><br><br>* Origin: General Events<br><br>* Virtual: Virtual events<br><br>* BAV: Circle event |Yes |
|groups_v2 |string array |The same **profile_groups_v2, take event properties, event public properties, user properties** |No |
|filter |array |With the **profile_filters** . |No |
|event_indicator |string |Calculation metrics:<br><br><br>* Events: Total<br><br>* event_users: Total headcount<br><br>* uv_per_au: penetration rate<br><br>* events_per_user: per capita<br><br>* pv_per_au: Total active users per capita<br><br>* Measure: Calculate |Yes |
|measure_info |json |Calculation indicator supplement, used when event_indicator measure, format and details are given below.<br><br>```json```<br>```{```<br>```  "event_indicator": "measure",```<br>```  "measure_info": {```<br>```      "measure_type": "sum",```<br>```      "property_name": "time"```<br>```  }```<br>```}```<br><br><br><br>* measure_type: Measurement scale, enumeration values are as follows:<br><br>   * Sum: Sum by<br><br>   * Min: press... to find the minimum value<br><br>   * Max: press... to find the maximum value<br><br>   * Avg: average by<br><br>   * per_user: by average<br><br>   * sum_per_au: press... to find the average number of active users<br><br>   * PCT: press... for percentiles<br><br>   * Distinct: deduplicate by<br><br>   * distinct_user_attr: press... and user deduplicate<br><br>* property_name: Calculated Properties |event_indicator is required when measuring. |
|show_label |string |Front\-end parameters do not affect query results, no need to pay attention |No |


<span id="d0096052"></span>
### 4.2.10 content/profile_filters**option**

Store query\-specific configurations to set whether to use caching and other parameters.

```json
{
    "refresh_cache": false,
    "fusion": false
}
```



|**Field** |**Value and meaning** |
|---|---|
|**All query common fields** ||
|skip_cache |Whether to skip cache. True means no cache, the default is false. |
|refresh_cache |Whether to refresh the cache. The query will go to the cache by default. When you want to skip the cache and update the cached data, you can set refresh_cache to true. |
|product |Product name, default is bytefinder. If you are using tracer, set to bytetracer |
|**conversion query/user path query** ||
|window_period_type |Window time unit, with granularity |
|window_period |Window time |
|**lifecycle query** ||
|lifecycle_query_type |Value enumeration value:<br><br><br>* Active active users.<br><br>* Lost lapsed user. |
|lifecycle_period |The value is a json object, and the attributes are fixed as granularity and period:<br><br><br>* "Granularity": time granularity<br><br>* "Period": time size |
|**retention analysis** ||
|retention_type |Window time unit, with granularity |
|retention_n_days |time window size |
|**web analytics** ||
|web_session_params |Parameters set by the web query.<br><br>```JSON```<br>```{```<br>```    "session_params_type": "first",```<br>```    "session_timeout": 1200```<br>```    }```<br><br><br><br>* session_params_type: Three enumeration values are currently supported:<br><br>   * First: The properties of the session are all determined by the first pageview. Scenario: source page analysis, entry page analysis.<br><br>   * Last: The properties of the session are all determined by the last pageview. Scenario: Exit page analysis.<br><br>   * filter_first_group_last: The first attribute of the session is determined by the first pageview, and the second attribute of the session is determined by the last pageview, filtered by the first attribute, and grouped by the second attribute. Scenario: Exit page analysis from the specified source.<br><br>* session_timeout: timeout. |
|option |Whether to integrate query real\-time data and offline data at the same time, true means fusion, and the default is false. |


<span id="fc5efb98"></span>
### 4.2.11 content/**page**

Store information related to query pagination.

```Plain
"page": {
    "limit": 50,  # Specify the maximum number of return dimensions
    "offset": 0
}
```



|**Field** |**Type** |**Value and meaning** |**Is it necessary** |
|---|---|---|---|
|limit |int |Specifies the maximum number of dimension bars to return. The default is 1000, and the maximum support is 50,000.<br><br>Note: Setting the `limit`too large may cause the query to time out or fail abnormally |No |
|offset |int |`The offset`field is still in the development stage and cannot take effect at this time. |No |


<span id="0a9a3917"></span>
# 5. Typical scenario DSL example

<span id="d3ba583e"></span>
## 5.1 Event query: event

```json
{
    "use_app_cloud_id": true,
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "content": {
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "query_type": "event",
        "queries": [
            [
                {
                    "event_name": "app_launch",
                    "event_type": "origin",
                    "show_name": "应用启动", //App start
                    "groups_v2": [],
                    "filters": [],
                    "show_label": "A",
                    "event_indicator": "events",
                    "measure_info": {},
                    "indicator_show_name": "总次数" //total count
                }
            ]
        ],
        "option": {
            "refresh_cache": false,
            "fusion": false
        }
    }
}
```


<span id="8bb94e51"></span>
## 5.2 Retention queries: retention

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "content": {
        "query_type": "retention",
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "queries": [
            [
                {
                    "show_label": "A",
                    "event_name": "app_launch",
                    "event_type": "origin",
                    "groups_v2": [],
                    "filters": []
                },
                {
                    "show_label": "",
                    "event_name": "any_active_event",
                    "event_type": "origin",
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "page": {
            "limit": 50,
            "offset": 0
        },
        "option": {
            "refresh_cache": false,
            "fusion": false
        }
    },
    "use_app_cloud_id": true

}
```


<span id="afe8c64d"></span>
## 5.3 Conversion query: funnel

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "content": {
        "query_type": "funnel",
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "page": {
            "limit": 50,
            "offset": 0
        },
        "queries": [
            [
                {
                    "show_label": "1",
                    "event_id": 234***,
                    "event_name": "app_launch",
                    "event_type": "origin",
                    "show_name": "",
                    "groups_v2": [],
                    "filters": []
                },
                {
                    "show_label": "2",
                    "event_id": 234***,
                    "event_name": "app_launch",
                    "event_type": "origin",
                    "show_name": "",
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "option": {
            "window_period": 10, 
            "window_period_type": "minute",
            "fusion": false,
            "refresh_cache": false
        }
    },
    "use_app_cloud_id": true

}
```


<span id="39601940"></span>
## 5.4 User Path Query: path_find

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai",
            "interval": "604800"
        }
    ],
    "version": 3,
    "content": {
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "query_type": "path_find",
        "queries": [
            [
                {
                    "event_type": "origin",
                    "show_label": "A",
                    "groups_v2": [],
                    "filters": []
                },
                {
                    "event_type": "origin",
                    "show_label": "B",
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "option": {
            "refresh_cache": false,
            "hide_unselected": true,
            "window_period_type": "minute", 
            "window_period": 10 
        }
    },
    "use_app_cloud_id": true

}
```


<span id="74ada51a"></span>
## 5.5 Lifecycle Query: life_cycle

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "content": {
        "query_type": "life_cycle",
        "queries": [
            [
                {
                    "event_id": 516***,
                    "event_name": "any_active_event",
                    "event_type": "origin",
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "profile_filters": [
        ],
        "profile_groups_v2": [],
        "option": {
            "lifecycle_period": {
                "granularity": "day",
                "period": 1
            },
            "lifecycle_query_type": "active"
        }
    },
    "use_app_cloud_id": true

}
```


<span id="d8180e1a"></span>
## 5.6 Web queries: web_session

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "contents": [
        {
            "profile_groups_v2": [],
            "profile_filters": [],
            "orders": [],
            "query_type": "web_session",
            "queries": [
                [
                    {
                        "event_type": "none",
                        "show_name": "访客数", // visitor quantity
                        "groups_v2": [],
                        "filters": [
                            {
                                "expression": {
                                    "logic": "and",
                                    "conditions": [
                                        {
                                            "property_values": [
                                                null
                                            ],
                                            "property_type": "event_param",
                                            "property_name": "referer_type",
                                            "property_operation": "is not null"
                                        }
                                    ]
                                }
                            }
                        ],
                        "show_label": "uv",
                        "event_indicator": "uv"
                    }
                ]
            ],
            "option": {
                "refresh_cache": false,
                "fusion": true
            }
        }
    ],
    "use_app_cloud_id": true

}
```


<span id="797f19ea"></span>
## 5.7 Topk query: event_topk

```json
{
    "app_ids": [
        "164***"
    ],
    "use_app_cloud_id": true,
    "version": "3.0",
    "periods": [
        {
            "granularity": "day",
            "align_unit": "day",
            "timezone": "Asia/Shanghai",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            }
        }
    ],
    "content": {
        "show_option": {},
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "query_type": "event_topk",
        "queries": [
            [
                {
                    "event_type": "none",
                    "event_indicator": "pv",
                    "show_name": "",
                    "show_label": "",
                    "event_name": null,
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "option": {
        }
    }
}
```


<span id="8a1722ea"></span>
## 5.8 LTV query: ltv

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 60,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "version": 3,
    "content": {
        "query_type": "ltv",
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "queries": [
            [
                {
                    "show_label": "",
                    "event_name": "purchase",
                    "event_type": "origin",
                    "groups_v2": [],
                    "filters": [],
                    "event_indicator": "measure",
                    "measure_info": {
                        "measure_type": "plain",
                        "property_name": "currency_amount"
                    }
                },
                {
                    "show_label": "",
                    "event_name": "any_event",
                    "event_type": "origin",
                    "groups_v2": [],
                    "filters": []
                }
            ]
        ],
        "page": {
            "limit": 10,
            "offset": 2
        },
        "option": {}
    },
    "use_app_cloud_id": true

}
```


<span id="c0191d76"></span>
## 5.9 Attribution query: behavior_attribution

```json
{
    "use_app_cloud_id": true,
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "granularity": "all",
            "type": "last",
            "last": {
                "amount": 7,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai",
            "interval": "604800"
        }
    ],
    "version": 3,
    "content": {
        "profile_groups_v2": [],
        "profile_filters": [],
        "orders": [],
        "query_type": "behavior_attribution",
        "queries": [
            [
                {
                    "event_name": "purchase",
                    "event_type": "origin",
                    "show_name": "支付", //pay
                    "groups_v2": [],
                    "event_indicator": "events",
                    "show_label": "A",
                    "measure_info": {},
                    "filters": []
                }
            ],
            [],
            [
                {
                    "event_name": "app_launch",
                    "event_type": "origin",
                    "show_name": "应用启动", //App start
                    "groups_v2": [],
                    "event_indicator": "events",
                    "show_label": "A",
                    "measure_info": {},
                    "filters": []
                }
            ]
        ],
        "option": {
            "refresh_cache": false,
            "attribution_type": "last",
            "window_period": 0,
            "window_period_type": "day",
            "is_other_contact": false
        },
        "page": {
            "limit": 50,
            "offset": 0
        }
    }
}
```


<span id="24e48d2d"></span>
## 5.10 Component query: composition

```json
{
    "app_ids": [
        164***
    ],
    "periods": [
        {
            "type": "last",
            "last": {
                "amount": 30,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai",
            "align_unit": "day",
            "granularity": "all"
        }
    ],
    "version": 3,
    "content": {
        "query_type": "composition",
        "profile_groups_v2": [
            {
                "property_type" : "profile",
                "property_name": "age"
            }
        ],
        "profile_filters": [],
        "orders": [],
        "queries": [
            [
                {
                    "event_type": "none"
                }
            ]
        ],
        "option": {
            "refresh_cache": false
        }
    },
    "use_app_cloud_id": true

}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Privatization inside <strong>"property_type"</strong> : <strong>"profile"</strong> needs to be changed to <strong>"property_type": "user_profile"</strong>.</div>


<span id="8de5d1ba"></span>
## 5.11 Attribute query: attribute

```json
{
    "use_app_cloud_id": true,
    "app_ids": [
        164***
    ],
    "periods": [
        {
            //Only support all granularity. Grouping by time granularity is not supported.
            "granularity": "all",
            "type": "past_range",
            "spans": [
                {
                    "type": "past",
                    "past": {
                        "amount": 7,
                        "unit": "day"
                    }
                },
                {
                    "type": "past",
                    "past": {
                        "amount": 1,
                        "unit": "day"
                    }
                }
            ],
            "timezone": "Asia/Shanghai",
            "week_start": 1,
            "align_unit": "day"
        }
    ],
    "version": 3,
    "content": {
        "profile_groups_v2": [],
        "profile_filters": [],
        //Custom sort field
        "orders": [
        {   //The field form is in the form of {property_type}#{property_name}, and the direction is in descending order (desc) or ascending order (asc)
                "field": "profile#loc_city_id",
                "direction": "desc"
            }
        ],
        //Customize pagination fields, with a maximum limit of 10000. If it exceeds 10000, it will be treated as 10000
        "page": {
            "limit": 50,
            "offset": 0
        },
        //query type, only support openApi
        "query_type": "attribute",
        "queries": [
            [
                {
                    "indicator_show_name": "",
                    "measure_info": {},
                    "show_name": "",
                    "show_label": "A",
                    "event_name": "any_event",
                    "event_type": "origin",
                    "event_indicator": "None",
                    "filters": [],
                    //Properties to be queried
                    "groups_v2": [
                        {
                            "property_compose_type": "origin",
                            "property_name": "$event_name",
                            "property_type": "common_param"
                        },
                        {
                            "property_compose_type": "origin",
                            "property_name": "loc_city_id",
                            "property_type": "profile"
                        },
                        {
                            "property_compose_type": "virtual",
                            "property_name": "$_vp_zylvirtual",
                            "property_type": "common_param"
                        }
                    ],
                    "extra": {}
                }
            ]
        ],
        "option": {
            //Is pagination required (true must be passed)
            "is_paginate": true
        }
    },
    "option": {}
}
```


This DSL is especially used for query scenarios where multiple attributes are grouped and the number of grouped values is large, and paging is supported in this specific scenario.

**Query restrictions:** 


* Queries that do not support the item attribute

* Event name + date must be specified

* Only attribute queries under the same event are supported

* Support for virtual events and virtual properties

* Queries with up to 5 attributes are supported simultaneously (more than 5 will be discarded)

* Time granularity grouping is not supported, only granularity: all


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">event_indicator requires a fixed pass None.</div>


* <div data-tips="true" data-tips-type="tip">is_paginate represents whether to page, must pass true, otherwise only take the previous page.limit results.</div>


* <div data-tips="true" data-tips-type="tip">groups_v2 pass the list of attributes to be queried if the query type is attribute.</div>
