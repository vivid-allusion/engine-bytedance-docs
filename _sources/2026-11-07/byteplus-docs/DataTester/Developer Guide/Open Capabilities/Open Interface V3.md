---
title: "Open Interface V3"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Open-Interface-V3"
---

<span id="一-概述"></span>
# 1. Overview

This document provides a description of the Open Interface V3 version of the "A/B Testing" application.

The available range includes


* Experiment information: create experiment, get experiment details, get experiment list, modify experiment, start experiment, end experiment

* Indicator information: create indicators, delete indicators, obtain indicator details, obtain indicator lists, modify indicator information in full, and modify indicator status

* Mutual exclusion group information: get mutual exclusion group list, create mutual exclusion group

* Report page information: Obtain the basic data of the experimental report


If you need to use the old version of the open interface, please refer to:[Open Interface (Old Version)](https://docs.byteplus.com/docs/DataTester/Open-Interface-Old-Version).

<span id="二-联系开通"></span>
# 2. Contact to open

In order to ensure the security of your and your users' data, open interface permissions are turned off by default.

Before you start using it, you need to contact us to open it. (You can get in touch with us through the Lark/WeChat group connected to the service or the online customer service in the lower right corner of the page)


* After opening, we will provide you with the AK/SK required for export. Please be sure to keep and use it properly after receiving it.

* When opening, please confirm with the docking staff the interface range that needs to be opened and the interface usage quota. Interfaces that are not within the open range and interface requests that exceed the quota will be rejected.


<span id="三-使用方式"></span>
# 3. How to use

To make it easier to integrate and use OpenAPI, we provide an SDK. Its main function is to provide a wrapper for the signing process and complex query parameters.

The SDK has been open\-sourced on GitHub, and it is recommended to use the GitHub source code for integration.

The basic usage process is as follows:


1. Initialize a RangersClient according to ak, sk, API service address

2. Use RangersClient's `request` interface or `data_tester` to call the specific API (the specific method name will have different naming formats in different languages).


Since the Chinese and non\-Chinese regions are isolated and not interoperable, the service address of OpenAPI needs to be set according to the region:


* Non\-Chinese: https://analytics.byteplusapi.com

* Private deployment: Obtain according to the environment of the private deployment, that is, the domain name address of the product.


<span id="sdk使用说明"></span>
## SDK Instructions

<span id="java"></span>
### Java


* Source code: https://github.com/volcengine/datafinder\-sdk\-openapi\-java

* Package: https://github.com/volcengine/datafinder\-sdk\-openapi\-java/raw/main/release/javasdk.zip

* Initialization example:


```java
String ak = "{replace with AK}";
String sk = "{replace with SK}";

//The default URL address of the SDK points to SAAS in China
RangersClient bc = new RangersClient(ak, sk);

//Overseas and privatization need to specify the url address, you can refer to the above
String url="{Replace with non Chinese domain name or Tester server domain name}";
RangersClient bc = new RangersClient(ak, sk, url);

String result = bc.dataTester("/openapi/v1/openapi-test", "GET");
System.out.println(result);
```


<span id="python"></span>
### Python


* Source code: https://github.com/volcengine/datafinder\-sdk\-openapi\-py

* Package: https://github.com/volcengine/datafinder\-sdk\-openapi\-py/raw/main/release/rangersdk\-1.2.0.tar.gz


After downloading the Python SDK package, execute the following command in the shell to complete the installation:

```bash
Python requires version 3.7 and above
pip install rangersdk-${version}.tar.gz
```



* Initialization example:


```python
from rangersdk import RangersClient

ak = '{Replace with AK}'
sk = '{Replace with SK}'
bc = RangersClient(ak, sk)

#Overseas and privatization need to specify the url address, you can refer to the above,
url = '{Replace with non Chinese domain name or Tester server domain name}'
#Note that the parameters passed here must be written as url = url
bc = RangersClient(ak, sk, url=url)

re = bc.data_tester("/openapi/v1/openapi-test", method="GET")
print(re.json())
```


<span id="golang"></span>
### Golang


* Source code: https://github.com/volcengine/datafinder\-sdk\-openapi\-go

* Package: https://github.com/volcengine/datafinder\-sdk\-openapi\-go/raw/main/release/gosdk.zip

* Initialization example:


```go
var (
   ak = "{Replace with AK}"
   sk = "{Replace with SK}"
)
bc := dslcontent.NewRangersClient(ak, sk)

//Overseas and privatization need to specify the url address, you can refer to the above
url = '{Replace with non Chinese domain name or Tester server domain name}'
bc := dslcontent.NewRangersClientWithUrl(ak, sk, url)

res, _ := bc.DataTester("/openapi/v1/openapi-test", "GET")
data, err := ioutil.ReadAll(res.Body)
fmt.Println(err, string(data))
```


<span id="js"></span>
### JS


* Source code: https://github.com/volcengine/datafinder\-sdk\-openapi\-js

* Package: https://github.com/volcengine/datafinder\-sdk\-openapi\-js/raw/main/release/nodejssdk.zip

* Initialization example:


```js
ak = "{Replace with AK}"
sk = "{Replace with SK}"
bc = new RangersClient(ak, sk)

//Overseas and privatization need to specify the url address, you can refer to the above
url = '{Replace with non Chinese domain name or Tester server domain name}'
bc = RangersClient(ak, sk, url=url)

bc.dataTester("/openapi/v1/openapi-test", {method: "GET"})
    .then(res => res.json())
    .then(response => {
        if (200 !== response['code']) {
            throw " result is not ok, code: " + response['code'] + ", message: " + response['message'];
        }
        console.log(response)
        console.log('success.')
    })
    .catch(error => console.error('error:', error));
```


<span id="php"></span>
### PHP


* Source code: https://github.com/volcengine/datafinder\-sdk\-openapi\-php

* Package: https://github.com/volcengine/datafinder\-sdk\-openapi\-php/raw/main/release/phpsdk.zip

* Initialization example:


```php
$ak = "{Replace with AK}";
$sk = "{Replace with SK}";
$bc = new RangersClient($ak, $sk);

//Overseas and privatization need to specify the url address, you can refer to the above
$url = '{Replace with non Chinese domain name or Tester server domain name}'
$bc = new RangersClient($ak, $sk, $url);

echo $bc->dataTester("/openapi/v1/openapi-test", "GET");
```


<span id="sdk使用注意"></span>
## SDK usage attention

<span id="中文编码"></span>
### Chinese characters coding

Get the list of related interfaces (experiments, indicators, mutual exclusion group) support queries according to the keyword, if you need to query Chinese, Java, Python, PHP need to call before url transcoding.The transcoding method is as follows.

Golang SDK and nodeJs SDK do not require self\-transcoding.

**Java**

```java
import java.net.URLEncoder;

String keyword = URLEncoder.encode("Chinese key words", "UTF-8")
```


**Python**

```python
import urllib.parse

keyword = urllib.parse.quote("Chinese key words", encoding="UTF-8")
```


**PHP**

```php
$keyword = urlencode("Chinese key words");
```


<span id="四-接口说明"></span>
# 4. Interface description

<span id="bb8e535a"></span>
## Get Audience Filters

**Description:**  Get App experiment filter conditions for audience rule selection, currently only support programming experiments\-server side experiments.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Privatized 4.9.0 version has added support for this interface.</div>


**Request path:**  `/openapi/v3/apps/{app_id}/para-filters`

**Request method: GET**

**Request parameters**


|Parameter name |Parameter type |Is it required? |Description |
|---|---|---|---|
|experiment_mode |string |Yes |Experiment type, currently only programming experiments are supported, and it needs to be configured as "coding". |
|side_type |string |Yes |Experimental side type, currently only supports server side experiments, and needs to be configured as "server". |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |The server side filter returned by the interface. The structure is as follows:<br><br>```JSON```<br>```{```<br>```"list":[{},{},...]```<br>```}```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In the private\-CDP joint deployment environment, the server side programming experiment returns a list of user clusters.</div><br> |


**Data structure description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |filter parameter ID |
|name |string |Filter parameter name |
|description |string |Description information |
|key |string |Filter Parameter Key |
|type |string |Filter parameter Value type |
|owner |object |Owner information list |
|modify_time |int |Parameter update timestamp (seconds) |
|attribute |string |filter parameter properties |
|options |object |List of available filter parameters, please refer to the example below |
|op |object |Filter parameters can be operated, please refer to the example below |
|property_type |string |Filter Parameters Parameter Types |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the returned data, the following fields need to be paid attention to for the audience filtering rules of the stitching experiment:</div>



* <div data-tips="true" data-tips-type="tip">Key: Parameter Key, where <strong>cohort</strong> represents the grouping circled in the current system.</div>


* <div data-tips="true" data-tips-type="tip">Type: Parameter value type, which in turn determines the operator.</div>


* <div data-tips="true" data-tips-type="tip">OP: Operator that can be performed.</div>


* <div data-tips="true" data-tips-type="tip">property_type: Parameter type, where cdp_cohort identifier is a subgroup of cdp.</div>



**Example**

```Bash
{
    "code": 200,
    "data": {
        "list":[
                {
                    "id": 12463,
                    "name": "name",
                    "key": "name",
                    "type": "string",
                    "owner": [
                        {
                            "id": 238434,
                            "name": "zhangsan",
                            "avatar": "https://sf3-ttcdn-tos.pstatp.com/obj/byterangers-avatar/NPTDy24097558461*****.png"
                        }
                    ],
                    "modify_time": 1695108262,
                    "attribute": "profile",
                    "options": [
                        {
                            "label": "",
                            "value": "syz"
                        },
                        {
                            "label": "",
                            "value": "cy"
                        }
                    ],
                    
                },
                {
                    "id": 0,
                    "name": "user cohorts",
                    "description": "",
                    "key": "cohort",
                    "type": "int",
                    "owner": [],
                    "modify_time": 0,
                    "attribute": "common_param",
                    "options": [
                        {
                            "label": "did any event yesterday_20231206174256586",
                            "value": 1022367
                        },
                        ...
                },
                ...
            ]
    }
    "message": "success"
}
```


<span id="69896ad5"></span>
## Create an experiment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Experiments created by open interfaces can only be edited by administrators</div>


**Interface description:**  Create a programming experiment or MAB experiment.

**Request path:**  `/openapi/v3/apps/{app_id}/experiments`

**Request method: POST**

**Request parameters**


|Parameter name |Parameter type |Is it required? |Description |Remarks |
|---|---|---|---|---|
|name |string |Yes |name of experiment |It cannot be duplicated with existing experiments under the current APP, and the length is limited to 200 characters. |
|description |string |No |experimental description |Length limit 1000 characters |
|tags |string |No |experimental label |["123", "456"] |
|owners |object |No |founder |Experiment with the owner list. The owner object data structure includes two parameters: id and name.<br><br><br>* ID: Type int, required, indicates user ID.<br><br>* Name: string type, required, representing the user name.<br><br><br>You can use the **user information query** interface to get the values for experimental owners. |
|endpoint_type |int |Yes |Type of experiment |0\- client side experiment, 1\- server side experiment |
|duration |int |Yes |experiment duration |Unit days, range: [1,365] |
|major_metric |int |Yes |Core Metric ID |Must be in metrics |
|metrics |int[] |Yes |List of indicator IDs to follow |Must contain major_metric |
|versions |object[] |Yes |Experimental version configuration |Array length should be greater than or equal to 2, see version structure description for details |
|layer_info |object |Yes |experimental layer configuration |See layer_info for details |
|mab_info |object |No |MAB experimental configuration information |If you are creating a MAB experiment, this field is required. For details, please refer to the mab_info structure description below. |
|user_group_filter_rules |object[] |No |List of Audience Rules for Audience Experiment. See the **user_group_filter_rules Structure Description** section below. |4.9.0 version, when jointly deployed with CDP, it is added to support the creation of customer group experiments. This parameter needs to be configured when using customer groups for audience rule configuration. |
|manage_sub_type |string |No |Feature Experiment subtype, can only be configured as: user_group. |null |
|rehash_info |object |No |Heavy random information. If you create a non\-multiple randomized experiment, you don't need to pass in a value for this parameter. See the **rehash_info** section below for details.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The heavy randomization ability cannot be used for MAB experiment, guest group experiment and special type experiment at present.</div><br> |check\-in |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The configuration of the mab group and the corresponding non\-mab group should be the same, that is, the configuration of the mab and non\-mab groups is one\-to\-one. For example, the intelligent tuning group "control group" and the evaluation group "control group \-Besfw" are one\-to\-one correspondences.</div>


* <div data-tips="true" data-tips-type="warning">Privatization 480 version MAB core metrics only support single event conversion rate type metrics, uv_per_dau (operator: conversion rate).</div>



**Version structure description**


|Parameter name |Parameter type |Is it required? |Description |Remarks |
|---|---|---|---|---|
|type |int |Yes |Control version/experimental version |0\-Control version, 1\-Experimental version There can only be one control version in the versions array |
|name |string |Yes |version name |Length 50 characters |
|description |string |No |version description |Length 1000 characters |
|weight |float |No |Experimental version of traffic allocation |Range [0.001, 1] 0.1%~ 100%<br><br>If the versions array is not passed, it will be evenly distributed by default. If passed, it will check whether the sum of all weights is 1. |
|config |object |Yes |version configuration |The keys of all configs in the version array need to be consistent |
|users |string[] |No |whitelist user |Different versions of whitelisted users cannot intersect |
|is_mab |int |No |Whether it is a mab intelligent traffic group, value: 0 or 1 | |


**layer_info structure description**


|Parameter name |Parameter type |Is it required? |Description |Remarks |
|---|---|---|---|---|
|layer_id |int |No |Mutual exclusion group ID |The experimental layer used, use the default layer to pass \-1 or not<br><br>If layer_id is specified, the available traffic on the experimental layer is verified to meet the experimental configuration |
|version_resource |float |Yes |percentage of experimental traffic |Range [0.001, 1], with a minimum accuracy of one thousandth |


**mab_info structure description**


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |**Remarks** |
|---|---|---|---|---|
|interval_time |int |Yes |Tuning interval, in seconds |In seconds, the minimum interval is 30 minutes, and it is increased by 30 minutes, such as 1800, 3600, 5400. |
|non_mab_traffic |int |Yes |Evaluate traffic percentage |Percentage, e.g. 6 is 6%, each experimental group requires a minimum of 3% of the evaluation traffic, e.g. three experimental groups require a minimum of 9% of the evaluation traffic. |


**user_group_filter_rules structure description**


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |
|---|---|---|---|
|name |string |Yes |group name |
|type |int |Yes |Control population/experimental population<br><br><br>* 0: Control customer group<br><br>* 1: Experimental guest group<br><br><br>user_group_filter_rules can have only one control group in the array |


**rehash_info structure description**


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |**Remarks** |
|---|---|---|---|---|
|cohorts |list |No |grouping information |Other fields are consistent with programming experiments and are omitted here |
|└ cohort_id |int |Yes |cluster ID |without |
|└ type |string |No |cluster type |Fixed value `uba` |
|metrics |list |No |indicator information |check\-in |
|└ metric_group_id |int |Yes |indicator group ID |cluster ID |
|└ metrics |list |Yes |indicator information |Up to 3 indicators |
|└└ metric_id |int |Yes |indicator ID |without |
|start_ts |int |No |start time |Required when metrics are specified, accurate to the second |
|end_ts |int |No |end time |Required when metrics are specified, accurate to the second |
|launch_times |int |No |number of attempts |Default 10, i.e. try 10 random seeds |
|statistic_type |string |No |statistical type |Statistical types, fixed values: `p_value` |
|threshold_value |float |No |statistical threshold |Default 0.05 |


**return value**


|Parameter name |Type |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |Newly Created Experiment ID |


**Example**

Programming experiment, two evaluation groups, two intelligent tuning groups, a total of 4 groups, the tuning interval is 30 minutes, and the evaluation flow is 6%.

```JSON
{
    "name": "test-mab",
    "duration": 14,
    "versions": [
        {
            "name": "control group",
            "label": "control group",
            "weight": 0.47,
            "is_mab": 1,
            "type": 0,
            "config": {
                "HcCVhO": "_Lf5XM"
            },
            "users": []
        },
        {
            "name": "experimental group1",
            "label": "experimental group1",
            "weight": 0.47,
            "is_mab": 1,
            "type": 1,
            "config": {
                "HcCVhO": "TAqqd4"
            },
            "users": []
        },
        {
            "name": "control group-Besfw",
            "label": "control group",
            "weight": 0.03,
            "is_mab": 0,
            "type": 1,
            "config": {
                "HcCVhO": "ij45wC"
            },
            "users": []
        },
        {
            "name": "experimental group1-fL17k",
            "label": "experimental group1",
            "weight": 0.03,
            "is_mab": 0,
            "type": 1,
            "config": {
                "HcCVhO": "WRDoSW"
            },
            "users": []
        }
    ],
    "major_metric": 100942,
    "metrics": [
        100940,
        100941,
        100942,
        100943,
        100944,
        100945,
        100946
    ],
    "mode": 1,
    "mab_info": {
        "interval_time": 1800,
        "non_mab_traffic": 6
    },
    "endpoint_type": 0,
    "layer_info": {
        "layer_id": -1,
        "version_resource": 1
    }
    {
    "user_group_filter_rules": [
        {
            "name": "\u5ba2\u7fa4A",
            "type": 0,
            "filter_rule": [
                {
                    "logic": "||",
                    "conditions": [
                        {
                            "logic": "&&",
                            "condition": {
                                "key": "automation_copy_aaaessrssb_Int",
                                "type": "int",
                                "op": "==",
                                "value": [
                                    1
                                ],
                                "property_type": "common_param"
                            }
                        }
                    ]
                }
            ]
        },
        {
            "name": "\u5ba2\u7fa4B",
            "type": 1,
            "filter_rule": [
                {
                    "logic": "||",
                    "conditions": [
                        {
                            "logic": "&&",
                            "condition": {
                                "key": "cohort",
                                "type": "int",
                                "op": "==",
                                "value": [
                                    1000004
                                ],
                                "property_type": "cdp_cohort"
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "manage_sub_type": "user_group",      //Subtype field of the experiment, here is the guest group transfer user_group, if the user edits the rollback and passes the empty string or not, the backend will judge the corresponding update experiment table
}
}
```


<span id="f0b3261e"></span>
## Get experimental details

**Description:**  Get experiment details according to experiment ID

**Request path:**  `/openapi/v3/apps/{app_id}/experiments/{experiment_id}`

**Request method: GET**

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment information returned by the interface |


**Data information**


|Parameter name |Type |Description |
|---|---|---|
|experiment |object |experimental information |


**Experiment structure description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |The experiment_id of the experiment |
|name |string |name of experiment |
|tags |string |tag list |
|owners |object |Owner information list |
|launch_start_time |long |Experiment start time, Unix timestamp |
|end_time |long |Experiment end time, Unix timestamp |
|create_time |long |Experiment creation time, Unix timestamp |
|modify_time |long |Experimental modification time, Unix timestamp |
|test_start_time |long |Experimental debugging start time, Unix timestamp |
|duration |long |Experimental running time in seconds |
|confidence_level |int |Confidence level, 95 means the confidence level is 95% |
|version_resource |float |Experimental flow rate, range [0.001, 1], 1 is 100% |
|layer_id |int |Experimental layer id |
|freeze_status |int |Experimental freezing state 1\-frozen, 0\-not frozen |
|freeze_time |long |Experimental freeze time, Unix timestamp (only valid if the freeze state is 1) |
|version_freeze_status |boolean |Whether to enter the group or not<br><br><br>* True: yes<br><br>* False: No |
|pause_status |boolean |Is the experiment suspended?<br><br><br>* True: Pause<br><br>* False: not paused |
|endpoint_type |int |0\- client side experiment, 1\- server side experiment |
|versions |object[] |Experimental version information |
|metrics |object[] |Experimental attention indicator information |
|status |int/enum |Experimental Status, 0: Completed 1: Running 2: Pending Scheduling 3: Debugging |
|filters |string |Experimental audience target, json string |
|description |string |experimental description |
|user_group_filter_rules |List[Dict] |Audience experiment Audience rule list |
|manage_sub_type |string |Characteristic Experiment Subtype |
|rehash_info |object |Re\-random information, see **rehash_info Structure Description** section below |


**Metric structure description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |indicator id |
|name |string |indicator name |
|description |string |indicator description |
|is_primary |int |Yes No Core Indicator: 0\-No 1\-Yes |
|calculate_type |string |Types of indicator calculation |
|dsl |object |Indicator dsl |
|status |int |Indicator status 0: offline 1: not offline |
|is_composed |boolean |Whether to combine indicators: true/false |
|data_type |string |Indicator presentation value format |
|metric_type |string |Indicator types, enumeration values are as follows:<br><br><br>* TEA: Event indicator<br><br>* Funnel: funnel indicator<br><br>* retention_all: Preset retention metrics.<br><br>* custom_retention: Custom retention metrics.<br><br>* Portable: number of positions indicator.<br><br>* Event: Event indicator, used to use "event" to represent event indicators in the past, and current event indicators use "tea".<br><br>* Other enumeration values: Other indicator types. |


**Version structure description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |Version ID |
|type |int |Version type: 0\-controlled version, 1\-experimental version |
|name |string |version name |
|description |string |version description |
|config |object |Version configuration |
|weight |int |Version weight, sum is 1000, 1 represents 0.1%, and 0 is evenly distributed |
|user_list |string[] |whitelist |


**rehash_info structure description**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|rehash_id |int |re\-random task ID |
|status |int |Heavy Random Task Status:<br><br><br>* INITIALIZED = 99, "initialize"<br><br>* RUNNING = 0, "Running"<br><br>* SUCCESS = 1, "Success"<br><br>* FAILURE = 2, "failed"<br><br>* ADOPTED = 3, "Adopted"<br><br>* DEPRECATED = 5, "Cancelled" |


<span id="获取实验列表"></span>
## Get a list of experiments

**Description:**  Page to get the experimental list under the APP

**Note: If the search keyword keyword contains Chinese, you need to escape the URL first and then call it.** 

**Request path:**  `/openapi/v3/apps/< app_id >/experiments`

**Request method: GET**

**URL query parameters**


|Parameter |Type |Description |
|---|---|---|
|status |int |Experimental status, 0\-completed, 1\-running, 3\-testing; all states are defaulted if not passed |
|page |int |Paging parameter, 1 represents the first page, the default is 1 if not passed. |
|page_size |int |Number of pages, default 99 if not passed. |
|keyword |string |Search keywords, currently support fuzzy search according to experimental name and description |
|sort_by |string |Sorting rules. Currently only supports end_time end time, launch_start_time experiment start time, test_start_time test start time; no default experiment creation time is passed |
|sort_order |string |Sort order. desc/asc。 Default desc descending order without passing |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |{<br><br>"experiments": [],<br><br>"page": {<br><br>"current_page": 1,//current page<br><br>"total_pages": 0,//Total pages<br><br>"total_items": 0//Total entries<br><br>}<br><br>} |


**Structural description of experiments**


|Parameter name |Type |Description |
|---|---|---|
|id |int |Experiment ID |
|name |string |name of experiment |
|end_time |long |Experiment end time, Unix timestamp |
|test_start_time |long |Experimental debugging start time, Unix timestamp |
|launch_start_time |long |Experiment start time, Unix timestamp |
|duration |long |Experimental running time in seconds |
|version_resource |float |Experimental flow rate, range [0.001, 1], 1 is 100% |
|layer_id |int |Experimental layer id |
|freeze_status |int |Experimental freezing state 1\-frozen, 0\-not frozen |
|freeze_time |long |Experimental freeze time, Unix timestamp (only valid if the freeze state is 1) |
|version_freeze_status |boolean |Whether to enter the group or not<br><br><br>* True: yes<br><br>* False: No |
|pause_status |boolean |Is the experiment suspended?<br><br><br>* True: Pause<br><br>* False: not paused |
|endpoint_type |int |0\- client side experiment, 1\- server side experiment |
|description |string |experimental description |
|status |int/enum |Experimental Status, 0: Completed 1: Running 2: Pending Scheduling 3: Debugging |
|owner |string |Experiment creator |
|versions |object[] |Experimental version information |


<span id="修改实验信息"></span>
## **Modify experimental information**

**Description:**  Modify the configuration information of the experiment. **Method to distinguish between full modification or partial modification**.


* Full Modification: Method = PUT. All required parameters in the request parameters must be included.

* Partial modification: Method = PATCH. The supported configuration parameters can be passed arbitrarily. Only parameters in the request body will be checked and modified. Parameters not in the request body will remain in the status quo.


**Note: Since the network library itself does not support the PATCH method, the Java SDK does not support the PATCH method for the time being.** 

**Request path:**  `/openapi/v3/apps/{app_id}/experiments/< experiment_id >`

Request method: PUT/PATCH

**Request parameters**


|Parameter name |Parameter type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|name |string |Yes |name of experiment |Cannot duplicate existing experiments, length 50 characters |
|description |string |No |experimental description |Length 1000 characters |
|tags |string |No |experimental label |["123", "456"] |
|owners |object |No |founder |List of experiment owners |
|duration |int |Yes |experiment duration |Unit day, [1,365], integer |
|major_metric |int |Yes |Core Metric ID |It cannot be modified during operation, but can be modified during testing. |
|metrics |int[] |Yes |list of indicator IDs | |
|versions |object[] |Yes |Experimental version |The number of versions cannot be changed, only the version content can be modified |
|layer_info |object |No |Mutual exclusion group | |
|user_group_filter_rules |object[] |No |List of Audience Rules for Audience Experiment. See the **user_group_filter_rules Structure Description** section below. | |
|manage_sub_type |string |No |Feature Experiment subtype, can only be configured as: user_group. | |


**Version structure**


|Parameter name |Parameter type |Is it required? |Description |Remarks |
|---|---|---|---|---|
|id |int |Yes |Version ID |Modified version information Required |
|name |string |Yes |version name |Length 50 characters |
|description |string |No |version description |Length 1000 characters |
|weight |float |No |traffic allocation |Range [0.001, 1] 0.1%~ 100%<br><br>If the versions array is not passed, it will be evenly distributed by default.<br><br>If passed, the sum of all weights is checked to be 1. |
|config |object |Yes |Version parameters Key for different versions<br><br>Need to be consistent |The keys of all configs in the version array need to be the same |
|users |string[] |No |whitelist user | |


**layer_info structure**


|Parameter name |Parameter type |Is it required? |Description |Remarks |
|---|---|---|---|---|
|layer_id |int |No |Mutual exclusion group ID | |
|version_resource |float |Yes |percentage of traffic occupied |Range [0.001, 1], with a minimum accuracy of one thousandth |


**user_group_filter_rules structure**


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |
|---|---|---|---|
|name |string |Yes |group name |
|type |int |Yes |Control population/experimental population<br><br><br>* 0: Control customer group<br><br>* 1: Experimental guest group<br><br><br>user_group_filter_rules can have only one control group in the array |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment ID |


<span id="开始实验"></span>
## Start the experiment

**Description:**  Start an experiment under test. Change its status to running.

**Request path:**  `/openapi/v3/apps/< app_id >/experiments/< experiment_id >/launch`

**Request method:**  PUT

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment ID |


<span id="66038d19"></span>
## suspend the experiment

**Description:**  Pause the specified experiment, 4.9.0 version starts to support this interface

**Request path** : `/openapi/v3/apps/< app_id >/experiments/< experiment_id >/pause`

**Request method:**  POST

**Request parameters**


|Parameter name |Type |Description |
|---|---|---|
|duration |int |When suspending an experiment, the experimental flow is smooth. How many minutes does the smoothing take effect by setting this parameter? |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |


<span id="78add8af"></span>
## recovery experiment

**Description:**  Restore the specified experiment, 4.9.0 version starts to support this interface

**Request path** : `/openapi/v3/apps/< app_id >/experiments/< experiment_id >/restore`

**Request method:**  POST

**Request parameters**


|Parameter name |Type |Description |
|---|---|---|
|duration |int |When resuming an experiment, the experimental flow is smooth and effective. How many minutes does the smoothing take effect by setting this parameter? |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |


<span id="结束实验"></span>
## End the experiment

**Description:**  End the specified experiment

**Request path**: `/openapi/v3/apps/< app_id >/experiments/< experiment_id >/stop`

**Request method:**  PUT

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |The interface returns the status, 200 is successful, and the error code for non\-200 is described as follows:<br><br><br>* 400: Business logic error<br><br>* 500: Abnormal service |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment ID |


<span id="469093b0"></span>
## Close the experimental group

**Description** : Close a certain experimental group

**Request path** : `/openapi/v3/apps/< app_id >/experiments/: flight_id/versions/: version_id/close`

**Request method:**  POST

**Request parameters**


|Parameter |Type |Description |
|---|---|---|
|app_id |integer |Path parameters, the app_id of the experiment |
|flight_id |integer |Path parameter, experiment ID |
|version_id |integer |Path parameter, experimental group ID |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |The interface returns the status, 200 is successful, and the error code for non\-200 is described as follows:<br><br><br>* 400: Business logic error<br><br>* 500: Abnormal service |
|message |string |The interface returns information, and the default is success when successful. |


<span id="创建指标"></span>
## Create metrics

**Description** : Create an A/B test metric

**Request path:**  `/openapi/v3/apps/< app_id >/metrics`

**Request method**: POST

**Request parameters**


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|name |string |Yes |indicator name |The length limit is 50, and it cannot be repeated with other indicators under the same APP. |
|description |string |No |indicator description |Length limit 1000 |
|dsl |object |Yes |Indicator DSL |For details of DSL, please consult the docking staff. |
|composed |boolean |Yes |Is it a combination indicator? |true/false |
|data_type |string |No |data display type |enumeration value<br><br>number_0, number_1, number_2, number_3, number_4, number_5,<br><br>percent_0, percent_1, percent_2, percent_3, percent_4, percent_5<br><br>Default is percent_4, which is four decimal places |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |indicator ID |


<span id="基于指标模板创建指标"></span>
## **Create metrics based on metric templates**

**Description:**  Based on existing A/B test metrics, create new A/B test metrics by modifying the attribute filtering information. Only the attribute value of the same name in the template metric will be replaced, and attributes that do not exist in the template metric will be ignored. If multiple metrics are passed in, the attribute information to be modified is applied to each metric individually.

It can be simply understood as making a copy of each template indicator and then modifying its existing property information.

**Request path:**  /openapi/v3/apps/< app_id \>/metrics/create\-from\-templates

**Request method:**  POST

**Request parameters**


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|metrics |list[metric] |Yes |indicator information list |Metrics are described in the table below |
|properties |list[property] |Yes |Attribute information that needs to be modified |The properties are described in the table below |


Metric field description


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|metric_id |int |Yes |template indicator id |Existing indicator id |
|name |string |Yes |The name of the new indicator according to the template indicator |The length limit is 50, and it cannot be repeated with other indicators under the same APP. |
|description |string |No |According to the template indicator, the indicator information of the new indicator |Length limit 1000 |


Property field description


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|property_name |string |Yes |attribute name |Attribute names that do not exist in the template will be ignored directly without an error |
|property_values |String/int/float array |Yes |attribute value |The length limit is 255, or [] if empty; the attribute value type needs to be consistent with the attribute type of the template metric. For specific field descriptions, please refer to [the detailed description of the V3 DSL field](https://bytedance.feishu.cn/wiki/wikcnoc1Nr7G3hcECZeQq9zA2Pf#) |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |list[object] |Newly created indicator information |


Object field description


|Parameter name |Type |Description |
|---|---|---|
|id |int |Newly created indicator ID |
|name |string |Name of newly created indicator |


```sql
curl --location --request POST '{host}/datatester/openapi/v3/apps/253047/metrics/create-from-template' \
--header 'Content-Type: application/json' \
--data-raw '{
    "metrics": [
        {
            "metric_id": 33487,
            "name": "test event metric 5",
            "description": "this is a description"
        },
        {
            "metric_id": 33488,
            "name": "test event metric 6",
            "description": "this is a description"
        }
    ],
    "properties": [
        {
            "property_name": "app_channel",
            "property_values": [
                "channel3",
                "channel4"
            ]
        },
        {
            "property_name": "account_id",
            "property_values": [
                "1234556",
                "7654321"
            ]
        }
    ]
}'
```


<span id="删除指标"></span>
## Delete indicator

**Description:**  Deletes the specified indicator. **If the indicator has already associated experiments, it cannot be deleted**

**Request path:**  `/openapi/v3/apps/< app_id >/metrics/< metric_id >`

**Request method: DELETE**

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |indicator ID |


<span id="获取指标详情"></span>
## Get indicator details

**Description:**  Obtain detailed data for specified indicators

**Request path:**  `/openapi/v3/apps/< app_id >/metrics/< metric_id >`

**Request method: GET**

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Indicator information |


**indicator information description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |indicator ID |
|name |string |indicator name |
|description |string |describe |
|dsl |object |Indicator dsl |
|composed |boolean |Is it a combination indicator? |
|status |int |Status 0 \- offline 1 \- online |
|is_support_major |boolean |Whether to support setting as core metrics |


<span id="获取指标列表"></span>
## Get a list of metrics

**Description:**  Page to get the list of indicators under the APP

**Request path:**  `/openapi/v3/apps/< app_id >/metrics`

**Request method: GET**

**URL query parameters**


|Parameter |Type |Description |
|---|---|---|
|status |int |Indicator status, 0\-offline 1\-online, if you don't pass it on, all states will be defaulted. |
|page |int |Paging parameter, 1 represents the first page, the default is 1 if not passed. |
|page_size |int |Number of pages, default 99 if not passed. |
|keyword |string |Search keywords, currently support fuzzy search by indicator name and description |
|only_confidence |int |Only query indicators that support confidence level calculation, 1 is a valid value, no transmission or other values are invalid |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |{<br><br>"metrics": [],<br><br>"page": {<br><br>"current_page": 1,//current page<br><br>"total_pages": 0,//Total pages<br><br>"total_items": 0//Total entries<br><br>}<br><br>} |


**indicator information description**


|Parameter name |Type |Description |
|---|---|---|
|id |int |indicator ID |
|name |string |indicator name |
|description |string |describe |
|dsl |object |Indicator dsl |
|composed |boolean |Is it a combination indicator? |
|status |int |Status 0 \- offline 1 \- online |
|is_support_major |boolean |Whether to support setting as core metrics |


<span id="3c461327"></span>
## Get the indicator group details

**Description:**  Obtain detailed data for the specified indicator group

**Request path:**  `/openapi/v3/apps/< app_id >/metric-groups/< metric_group_id >`

**Request method: GET**

**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Indicator group information |


**Indicator group information description**


* body.data

   
   |Field name |Description |
   |---|---|
   |id |indicator group id |
   |name |Indicator group name |
   

* body.metrics[0]

   
   |Field name |Description |
   |---|---|
   |id |indicator id |
   |name |indicator name |
   |type |indicator type<br><br><br>* Portable: number of positions indicator<br><br>* Tea: uba indicator, other indicators except the number warehouse indicator are uba indicators of tea type |
   |composed |Whether to combine metrics<br><br><br>* True: Combination metrics<br><br>* False: single indicator |
   |is_experimental_property_filter |Whether to support flexible attributes<br><br><br>* 1: Support, return the details of the supported flexible properties, the format can be seen below: body.metrics [0]. experimental_property_filter_tpl<br><br>* 0: not supported |
   

* body.metrics[0].experimental_property_filter_tpl

   ```JSON
   {
     "A": {
       "event_id": 89,
       "event_name": "any_event",
       "properties": [
         {
           "property_type": "common_param",
           "property_value_type": "string",
           "property_name": "user_agent"
         }
       ]
     },
     "B": {
       "event_id": 91,
       "event_name": "app_launch",
       "properties": [
         {
           "property_type": "user_profile",
           "property_value_type": "datetime",
           "property_name": "first_event_time"
         }
       ]
     },
     "all": {
       "properties": [
         {
           "property_type": "user_profile",
           "property_value_type": "string",
           "property_name": "gender"
         }
       ]
     }
   }
   ```
   

   The return result field details of the flexible attribute details are similar to the DSL structure description of the DataFinder. The main fields are as follows:

   
   |Field name |Description |
   |---|---|
   |A、B |Corresponds to the show_label in the DSL. |
   |all |Properties that apply to all events |
   |properties |indicator attribute description |
   |property_name |attribute name |
   |property_type |attribute type<br><br><br>* common_param: Public Event Attribute<br><br>* user_profile: user properties |
   |property_value_type |attribute value type<br><br>int/string/long/float |
   


**Back to example**


* Query data warehouse indicator group details

   ```JSON
   {
     "code": 0,
     "data": {
       "id": 60,
       "name": "portable（single+composite metrics）45712",
       "status": 1,
       "description": "",
       "type": "portable",
       "uba_report_type": 1,
       "uba_app_id": 0,
       "owners": [
         {
           "id": 1,
           "name": "admin",
           "avatar": null,
           "is_superuser": null
         }
       ],
       "app_ids": [
         10000001
       ],
       "import_app_ids": [],
       "tags": [],
       "merge_types": {
         "total_start_time": 0,
         "support_accumulate": 0,
         "support_total": 0,
         "support_avg": 1
       },
       "metric_scenes": [],
       "sla": "",
       "metrics": [
         {
           "id": 10397,
           "name": "SUM/UV-flexible",
           "description": "",
           "status": 1,
           "dsl": {
             "version": 3,
             "content": {
               "queries": [
                 [
                   {
                     "dataset_id": 9,
                     "event_indicator": "measure",
                     "filters": [],
                     "measure_info": {
                       "field_name": "amount",
                       "measure_type": "sum",
                       "property_type": "profile",
                       "value_type": "int"
                     },
                     "nickname": "",
                     "show_label": "A"
                   }
                 ],
                 [
                   {
                     "dataset_id": 9,
                     "event_indicator": "event_users",
                     "filters": [],
                     "nickname": "",
                     "show_label": "B"
                   }
                 ],
                 [
                   {
                     "formula": "A/B",
                     "show_label": "metric_relation",
                     "show_name": "metric relation"
                   }
                 ]
               ],
               "profile_filters": [],
               "show_option": null,
               "option": null
             }
           },
           "composed": true,
           "data_type": "number_4",
           "type": "portable",
           "is_required": 0,
           "permission_type": "public",
           "calculate_type": "events_per_user",
           "create_time": 1724056602,
           "modify_time": 1724056637,
           "support_confidence": true,
           "is_support_major": true,
           "experiment_num": 2,
           "key": "",
           "file": "",
           "is_hourly": 0,
           "support_bayes": 0,
           "need_weighted": 0,
           "weighted_metric_id": null,
           "visible": true,
           "major_metric_num": 0,
           "has_running_experiments": true,
           "is_defense_metric": 0,
           "defenses": [],
           "use_pre_sql": 0,
           "pre_alert": 0,
           "merge_pre_sql": "",
           "avg_pre_sql": "",
           "first_entry_avg_pre_sql": "",
           "extra_info": "{\"is_experimental_property_filter\":1,\"experimental_property_filter_tpl\":{\"A\":{\"properties\":[{\"property_value_type\":\"int\",\"property_name\":\"amount\"}]},\"B\":{\"properties\":[{\"property_value_type\":\"string\",\"property_name\":\"order_no\"}]},\"all\":{\"properties\":[{\"property_value_type\":\"string\",\"property_name\":\"product_type\"}]}}}",
           "is_experimental_property_filter": 1,
           "experimental_property_filter_tpl": {
             "A": {
               "properties": [
                 {
                   "property_value_type": "int",
                   "property_name": "amount"
                 }
               ]
             },
             "B": {
               "properties": [
                 {
                   "property_value_type": "string",
                   "property_name": "order_no"
                 }
               ]
             },
             "all": {
               "properties": [
                 {
                   "property_value_type": "string",
                   "property_name": "product_type"
                 }
               ]
             }
           },
           "is_experimental_property_filter_editable": 0
         }
       ],
       "permission_type": "public",
       "modify_time": 1724056601,
       "metric_num": null,
       "libra_analysis_type": 0,
       "dimensions": [],
       "new_format": 1,
       "dataset_id": 5,
       "ab_analysis_type": 0
     },
     "message": ""
   }
   ```
   

* Inquire about UBA indicator group details

   ```JSON
   {
       "code": 0,
       "data": {
           "id": 2,
           "name": "default",
           "status": 1,
           "description": "App access test metric group(system built)",
           "type": "uba",
           "uba_report_type": 1,
           "uba_app_id": 0,
           "owners": [
               {
                   "id": -2,
                   "name": "InnerAPI",
                   "avatar": null,
                   "is_superuser": null
               }
           ],
           "app_ids": [
               10000001
           ],
           "import_app_ids": [],
           "tags": [],
           "merge_types": {
               "total_start_time": 0,
               "support_accumulate": 0,
               "support_total": 0,
               "support_avg": 1
           },
           "metric_scenes": [],
           "sla": "",
           "metrics": [
               {
                   "id": 10425,
                   "name": "composite metric-1-flexible",
                   "description": "composite metric-1-flexible",
                   "status": 1,
                   "dsl": {
                       "version": 3,
                       "content": {
                           "queries": [
                               [
                                   {
                                       "event_id": 89,
                                       "event_indicator": "pv_per_dau",
                                       "event_name": "any_event",
                                       "event_type": "origin",
                                       "filters": [
                                           {
                                               "expression": {
                                                   "conditions": [],
                                                   "logic": "and"
                                               }
                                           }
                                       ],
                                       "nickname": "",
                                       "show_label": "A"
                                   }
                               ],
                               [
                                   {
                                       "event_id": 91,
                                       "event_indicator": "pv_per_dau",
                                       "event_name": "app_launch",
                                       "event_type": "origin",
                                       "filters": [],
                                       "nickname": "",
                                       "show_label": "B"
                                   }
                               ],
                               [
                                   {
                                       "formula": "A/B",
                                       "show_label": "metric_relation",
                                       "show_name": "metric relation"
                                   }
                               ]
                           ],
                           "profile_filters": [],
                           "show_option": null,
                           "option": null
                       }
                   },
                   "composed": true,
                   "data_type": "number_4",
                   "type": "tea",
                   "is_required": 0,
                   "permission_type": "public",
                   "calculate_type": "",
                   "create_time": 1726024310,
                   "modify_time": 1726024483,
                   "support_confidence": false,
                   "is_support_major": false,
                   "experiment_num": 0,
                   "key": "",
                   "file": "",
                   "is_hourly": 0,
                   "support_bayes": 0,
                   "need_weighted": 0,
                   "weighted_metric_id": null,
                   "visible": true,
                   "major_metric_num": 0,
                   "has_running_experiments": false,
                   "is_defense_metric": 0,
                   "defenses": [],
                   "use_pre_sql": 0,
                   "pre_alert": 0,
                   "merge_pre_sql": "",
                   "avg_pre_sql": "",
                   "first_entry_avg_pre_sql": "",
                   "extra_info": "{\"is_experimental_property_filter\":1,\"experimental_property_filter_tpl\":{\"A\":{\"event_id\":89,\"event_name\":\"any_event\",\"properties\":[{\"property_type\":\"common_param\",\"property_value_type\":\"string\",\"property_name\":\"user_agent\"}]},\"B\":{\"event_id\":91,\"event_name\":\"app_launch\",\"properties\":[{\"property_type\":\"user_profile\",\"property_value_type\":\"datetime\",\"property_name\":\"first_event_time\"}]},\"all\":{\"properties\":[{\"property_type\":\"user_profile\",\"property_value_type\":\"string\",\"property_name\":\"gender\"}]}}}",
                   "is_experimental_property_filter": 1,
                   "experimental_property_filter_tpl": {
                       "A": {
                           "event_id": 89,
                           "event_name": "any_event",
                           "properties": [
                               {
                                   "property_type": "common_param",
                                   "property_value_type": "string",
                                   "property_name": "user_agent"
                               }
                           ]
                       },
                       "B": {
                           "event_id": 91,
                           "event_name": "app_launch",
                           "properties": [
                               {
                                   "property_type": "user_profile",
                                   "property_value_type": "datetime",
                                   "property_name": "first_event_time"
                               }
                           ]
                       },
                       "all": {
                           "properties": [
                               {
                                   "property_type": "user_profile",
                                   "property_value_type": "string",
                                   "property_name": "gender"
                               }
                           ]
                       }
                   },
                   "is_experimental_property_filter_editable": 1
               }
           ],
           "permission_type": "public",
           "modify_time": 1724814787,
           "metric_num": null,
           "libra_analysis_type": 0,
           "dimensions": [],
           "new_format": 1,
           "dataset_id": null,
           "ab_analysis_type": 0
       },
       "message": ""
   }
   ```
   


<span id="全量修改指标信息"></span>
## Modify the indicator information in full

**Description:**  Modify all the information of the indicator, DSL cannot be modified for the time being, only the name, description and data type can be modified

**Request path:**  `/openapi/v3/apps/< app_id >/metrics/< metric_id >`

**Request method: PUT**

**Request body**


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|name |string |Yes |indicator name |Maximum length 50, non\-repeatable |
|description |string |No |indicator description |Maximum length 1000 |
|data_type |string |No |Indicator data type |enumeration value<br><br>number_0, number_1, number_2, number_3, number_4, number_5,<br><br>percent_0, percent_1, percent_2, percent_3, percent_4, percent_5<br><br>Default is percent_4, which is four decimal places |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |indicator ID |


<span id="修改指标状态"></span>
## Modify indicator status

**Description:**  Modify the status of the indicator (online, offline). **The Java SDK does not currently support this interface**

**Request path:**  `/openapi/v3/apps/< app_id >/metrics/< metric_id >`

**Request method: PATCH**

**Request body**


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|status |int |Yes |indicator status |0\-offline 1\-online |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |indicator ID |


<span id="5d6cdf14"></span>
## Get experimental reports \- group conclusion overview

**Description** : Get an overview of the analysis conclusions of the experimental report

**Request path** : /openapi/v3/apps/< app_id \>/experiments/< experiment_id \>/summary\-data

**Request method: GET**

**Return value**


|code |int |Interface returns status, 200 is successful |
|---|---|---|
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Report data, please refer to the report data structure description below for details. |


**Report Data Structure Description**


|**Parameter name** |**Parameter type** |**Description** |
|---|---|---|
|summary_infos |list[object] |The report provides an overview of the data, as detailed in the summa_infos structure note below. |
|report_type |string |Report type: day: day |
|start_ts |int |Query start time, UNIX timestamp |
|end_ts |int |Query end time, UNIX timestamp |
|user_data |object |Number of users per version |


**summary_infos structure description**


|**Parameter name** |**Parameter type** |**Description** |
|---|---|---|
|major_metric_name |string |core indicator name |
|summary |list[object] |indicator overview data |


**Back to example**

```JSON
{
    "code": 200,
    "data": {
        "summary_infos": [
            {
                "major_metric_name": "any conversion rate",
                "summary": [
                    {
                        "vid": 339601,
                        "version_name": "8b4b2cfdbd73941123bce96f9ce541e2",
                        "confidence": 3,
                        "conf_interval": [
                            -0.08904,
                            0.08904
                        ],
                        "p": 1.0
                    }
                ]
            }
        ],
        "user_data": {
            "339600": 799,
            "339601": 799
        },
        "start_ts": 1708822800,
        "end_ts": 1713801599,
        "report_type": "day"
    },
    "message": "success"
}
```


<span id="473f7a2b"></span>
## **Get the Lab Report \- Overview of Core Metrics**

**Description** : Used to obtain an overview of the conclusions of the experimental report group

**Request path** : /openapi/v3/apps/< app_id \>/experiments/< experiment_id \>/metric\-data

**Request method: POST**

**Request parameters**


|Parameter name |Type |Is it necessary |Description |Remarks |
|---|---|---|---|---|
|metric_id |int |Yes |indicator ID |You can get the indicator ID through the get indicator list interface. |
|report_type |string |Yes |query type |Time granularity: days, hours, minutes.<br><br><br>* Privatization: day/hour/five_minute |
|start_ts |int |Yes |Query start time, UNIX timestamp |The default experiment start time cannot be earlier than the experiment start time |
|end_ts |int |Yes |Query end time, UNIX timestamp |Default current time, no later than the end time of the experiment |
|dim |string |No |Query data statistics dimension, default to experimental group dimension |For guest group experiment, support experiment and guest group dimension cross\-query: abversion_usergroup |


**Return value**


|Parameter name |Type |Description |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Report data, please refer to the report data structure description below for details. |


**Data (report data) structure description**


|Parameter name |Parameter type |Description |
|---|---|---|
|versions |list[object] |For experimental version information, see the version information structure description below. |
|user_groups |list[object] |Guest group information is returned only when the guest group experiment contains the guest group dimension. |
|version_usergroups |list[object] |Guest group information is returned only when the guest group experiment and dim = abversion_usergroup. |
|start_ts |int |Query start time, UNIX timestamp |
|end_ts |int |Query end time, UNIX timestamp |
|available_start_ts |int |Available report start time, UNIX timestamp<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the time range of the query exceeds the time range of the actual report data output, the return result of the calling interface is the data within the time range of the report with data. The available report start/end time here refers to the time range of the actual returned report data.</div><br> |
|available_end_ts |int |Available end time, UNIX timestamp |
|confidence_level |int |confidence level |
|metric_id |int |indicator ID |
|distribution |object |Statistical distribution data |
|daily_data |object |Sky\-level, hour\-level, 5\-minute\-level reporting data |
|user_data |object |Number of users per version |


**version information structure description**


|Parameter name |Parameter type |Description |
|---|---|---|
|id |int |Version ID |
|name |string |version name |
|config |object |version configuration information |
|type |int |0: Comparison Version 1: Experimental Version |
|weight |int |Version weight, 0 is the average |
|disabled |bool |Whether to disable |


**Back to example**

Success:

```JSON
{
    "code": 200,
    "data": {
        "available_start_ts": 1708822800,
        "available_end_ts": 1713801599,
        "start_ts": 1708822800,
        "end_ts": 1713801599,
        "versions": [
            {
                "id": "339600",
                "name": "version 1",
                "config": {
                    "0304": "111"
                },
                "type": 0,
                "weight": 0,
                "disabled": false
            },
            {
                "id": "339601",
                "name": "version 2",
                "config": {
                    "0304": "222"
                },
                "type": 1,
                "weight": 0,
                "disabled": false
            }
        ],
        "confidence_level": 80,
        "metric_id": 99196,
        "distribution": {
            "339600": {
                "339601": {
                    "p": 1,
                    "m": 0.3416771,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        -0.08904,
                        0.08904
                    ],
                    "half_interval": 0.0890367,
                    "confidence": 3,
                    "mean": {
                        "339600": 0.3416771,
                        "339601": 0.3416771
                    },
                    "variance": {
                        "339600": 0.00028152,
                        "339601": 0.00028152
                    },
                    "mde": 0.14750037,
                    "sample_size": {
                        "339600": 799,
                        "339601": 799
                    },
                    "details": {
                        "numerator": 273,
                        "denominator": 799
                    }
                }
            },
            "339601": {
                "339600": {
                    "p": 0,
                    "m": 0.3416771,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "339600": 0,
                        "339601": 0
                    },
                    "variance": {
                        "339600": 0,
                        "339601": 0
                    },
                    "details": {
                        "numerator": 273,
                        "denominator": 799
                    }
                }
            }
        },
        "daily_data": {
            "2024-03-04": {
                "339600": {
                    "339601": {
                        "p": 1,
                        "m": 0.3416771,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            -0.08904,
                            0.08904
                        ],
                        "half_interval": 0.0890367,
                        "confidence": 3,
                        "mean": {
                            "339600": 0,
                            "339601": 0
                        },
                        "variance": {
                            "339600": 0,
                            "339601": 0
                        },
                        "mde": 0.14750037,
                        "details": {
                            "numerator": 273,
                            "denominator": 799
                        }
                    }
                },
                "339601": {
                    "339600": {
                        "p": 0,
                        "m": 0.3416771,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "339600": 0,
                            "339601": 0
                        },
                        "variance": {
                            "339600": 0,
                            "339601": 0
                        },
                        "details": {
                            "numerator": 273,
                            "denominator": 799
                        }
                    }
                }
            }
        },
        "boxplot": "The current indicator does not support box plots. Please refer to the explanation below for the specific reason.",
        "user_data": {
            "339600": 799,
            "339601": 799
        }
    },
    "message": "success"
}
```


Example of a return that includes the guest dimension:

```JSON
{
    "code": 200,
    "data": {
        "available_start_ts": 1716775273,
        "available_end_ts": 1716998399,
        "start_ts": 1716775273,
        "end_ts": 1716911999,
        "versions": [
            {
                "id": "217",
                "name": "version 1",
                "config": {
                    "zgtest0524": "a"
                },
                "type": 0,
                "weight": 0,
                "disabled": false
            },
            {
                "id": "218",
                "name": "version 2",
                "config": {
                    "zgtest0524": "b"
                },
                "type": 1,
                "weight": 0,
                "disabled": false
            }
        ],
        "confidence_level": 90,
        "metric_id": 10393,
        "distribution": {
            "217_2": {
                "218_1": {
                    "p": 0,
                    "m": 0,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "217_2": 0,
                        "218_1": 0
                    },
                    "variance": {
                        "217_2": 0,
                        "218_1": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "218_2": {
                    "p": 0,
                    "m": 1.5,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "217_2": 0,
                        "218_2": 0
                    },
                    "variance": {
                        "217_2": 0,
                        "218_2": 0
                    },
                    "details": {
                        "numerator": 258,
                        "denominator": 172
                    }
                },
                "217_1": {
                    "p": 0,
                    "m": 1.5045,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "217_2": 0,
                        "217_1": 0
                    },
                    "variance": {
                        "217_2": 0,
                        "217_1": 0
                    },
                    "details": {
                        "numerator": 3009,
                        "denominator": 2000
                    }
                }
            },
            "218_1": {
                "217_2": {
                    "p": 0,
                    "m": 0,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_1": 0,
                        "217_2": 0
                    },
                    "variance": {
                        "218_1": 0,
                        "217_2": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "218_2": {
                    "p": 0,
                    "m": 1.5,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_1": 0,
                        "218_2": 0
                    },
                    "variance": {
                        "218_1": 0,
                        "218_2": 0
                    },
                    "details": {
                        "numerator": 258,
                        "denominator": 172
                    }
                },
                "217_1": {
                    "p": 0,
                    "m": 1.5045,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_1": 0,
                        "217_1": 0
                    },
                    "variance": {
                        "218_1": 0,
                        "217_1": 0
                    },
                    "details": {
                        "numerator": 3009,
                        "denominator": 2000
                    }
                }
            },
            "218_2": {
                "217_2": {
                    "p": 0,
                    "m": 0,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_2": 0,
                        "217_2": 0
                    },
                    "variance": {
                        "218_2": 0,
                        "217_2": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "218_1": {
                    "p": 0,
                    "m": 0,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_2": 0,
                        "218_1": 0
                    },
                    "variance": {
                        "218_2": 0,
                        "218_1": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "217_1": {
                    "p": 0,
                    "m": 1.5045,
                    "change": 0,
                    "change_rate": 0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "218_2": 0,
                        "217_1": 0
                    },
                    "variance": {
                        "218_2": 0,
                        "217_1": 0
                    },
                    "details": {
                        "numerator": 3009,
                        "denominator": 2000
                    }
                }
            },
            "217_1": {
                "217_2": {
                    "p": 0,
                    "m": 0,
                    "change": -1.5045,
                    "change_rate": -1.0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "217_1": 0,
                        "217_2": 0
                    },
                    "variance": {
                        "217_1": 0,
                        "217_2": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "218_1": {
                    "p": 0,
                    "m": 0,
                    "change": -1.5045,
                    "change_rate": -1.0,
                    "conf_interval": [
                        0,
                        0
                    ],
                    "half_interval": 0,
                    "confidence": 3,
                    "mean": {
                        "217_1": 0,
                        "218_1": 0
                    },
                    "variance": {
                        "217_1": 0,
                        "218_1": 0
                    },
                    "details": {
                        "numerator": 0,
                        "denominator": 0
                    }
                },
                "218_2": {
                    "p": 0.9,
                    "m": 1.5,
                    "change": -0.0045,
                    "change_rate": -0.00299103,
                    "conf_interval": [
                        -0.04927,
                        0.04329
                    ],
                    "half_interval": 0.04628192,
                    "confidence": 3,
                    "mean": {
                        "217_1": 1.5045,
                        "218_2": 1.5
                    },
                    "variance": {
                        "217_1": 0.00012505,
                        "218_2": 0.00146199
                    },
                    "mde": 0.06856722,
                    "sample_size": {
                        "217_1": 2000,
                        "218_2": 172
                    },
                    "details": {
                        "numerator": 258,
                        "denominator": 172
                    }
                }
            }
        },
        "daily_data": {
            "2024-05-27": {
                "217_1": {
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": -1.009,
                        "change_rate": -1.0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_1": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": -1.009,
                        "change_rate": -1.0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_1": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0.001,
                        "m": 1.5,
                        "change": 0.491,
                        "change_rate": 0.48662042,
                        "conf_interval": [
                            0.44702,
                            0.52622
                        ],
                        "half_interval": 0.03959949,
                        "confidence": 1,
                        "mean": {
                            "217_1": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "218_2": 0
                        },
                        "mde": 0.07158988,
                        "details": {
                            "numerator": 258,
                            "denominator": 172
                        }
                    }
                },
                "217_2": {
                    "217_1": {
                        "p": 0,
                        "m": 1.009,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 1009,
                            "denominator": 1000
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0,
                        "m": 1.5,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "218_2": 0
                        },
                        "details": {
                            "numerator": 258,
                            "denominator": 172
                        }
                    }
                },
                "218_1": {
                    "217_1": {
                        "p": 0,
                        "m": 1.009,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 1009,
                            "denominator": 1000
                        }
                    },
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0,
                        "m": 1.5,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "218_2": 0
                        },
                        "details": {
                            "numerator": 258,
                            "denominator": 172
                        }
                    }
                },
                "218_2": {
                    "217_1": {
                        "p": 0,
                        "m": 1.009,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 1009,
                            "denominator": 1000
                        }
                    },
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    }
                }
            },
            "2024-05-28": {
                "217_1": {
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": -1.0,
                        "change_rate": -1.0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_1": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": -1.0,
                        "change_rate": -1.0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_1": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0,
                        "m": 0,
                        "change": -1.0,
                        "change_rate": -1.0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_1": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "217_1": 0,
                            "218_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    }
                },
                "217_2": {
                    "217_1": {
                        "p": 0,
                        "m": 1.0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 2000,
                            "denominator": 2000
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "217_2": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "217_2": 0,
                            "218_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    }
                },
                "218_1": {
                    "217_1": {
                        "p": 0,
                        "m": 1.0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 2000,
                            "denominator": 2000
                        }
                    },
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_1": 0,
                            "218_2": 0
                        },
                        "variance": {
                            "218_1": 0,
                            "218_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    }
                },
                "218_2": {
                    "217_1": {
                        "p": 0,
                        "m": 1.0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "217_1": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "217_1": 0
                        },
                        "details": {
                            "numerator": 2000,
                            "denominator": 2000
                        }
                    },
                    "217_2": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "217_2": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "217_2": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    },
                    "218_1": {
                        "p": 0,
                        "m": 0,
                        "change": 0,
                        "change_rate": 0,
                        "conf_interval": [
                            0,
                            0
                        ],
                        "half_interval": 0,
                        "confidence": 3,
                        "mean": {
                            "218_2": 0,
                            "218_1": 0
                        },
                        "variance": {
                            "218_2": 0,
                            "218_1": 0
                        },
                        "details": {
                            "numerator": 0,
                            "denominator": 0
                        }
                    }
                }
            }
        },
        "boxplot": "The current metric does not support box plots. Please refer to the explanation below for specific reasons",
        "user_data": {
            "217_1": 2000,
            "217_2": 0,
            "218_1": 0,
            "218_2": 172
        },
        "sql": {
            "user_data": [
                null
            ],
            "distribution_data": [
                null
            ],
            "daily_data": [
                null
            ],
            "boxplot_data": [
                null
            ]
        },
        "user_groups": [
            {
                "id": "1",
                "name": "test",
                "type": 0
            },
            {
                "id": "2",
                "name": "test1",
                "type": 1
            }
        ],
        "version_usergroups": [
            {
                "id": "217_1",
                "name": "version1_test"
            },
            {
                "id": "217_2",
                "name": "version1_test1"
            },
            {
                "id": "218_1",
                "name": "version2_test"
            },
            {
                "id": "218_2",
                "name": "version2_test1"
            }
        ]
    },
    "message": "success"
}
```


**Description of failure:** 


|Failure condition |Response |
|---|---|
|Out of query range:<br><br><br>* Hour level: Last 2 days. From 00:00 on the first day.<br><br>* Minute level: current day. From 00 on the current day. |```SQL```<br>```{```<br>```    "code": 204,```<br>```    "data": null,```<br>```    "message": "The start and end times are not within the effective time range of the experimental operation"```<br>```}```<br> |
|When the experiment runs on the first day, you need to query the sky\-level data. Because the sky\-level data is T + 1, an error will be reported at this time. |```SQL```<br>```{```<br>```    "code": 301,```<br>```    "data": null,```<br>```    "message": "experimental reporting type is wrong"```<br>```}```<br> |


<span id="c28fdda7"></span>
## Get the winning rate of the MAB experiment

**Description** : Obtain the winning probability of each version of the MAB intelligent tuning experiment

**Request path:**  /openapi/v3/apps/< app_id \>/experiments/< experiment_id \>/mab\-probability

**Request method: GET**

**Return value**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Report data, see the report data notes below for details. |


**report data description**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|versions |list of object |For the basic information of each experimental version, see the basic information of the experimental version below for details. |
|probs |list of object |The winning probability of each experimental version is detailed in the experimental version winning probability below. |


**Experimental version basic information**


|**Parameter name** |**Type** |**Descriptiontion** |
|---|---|---|
|id |int |Version ID |
|name |string |version name |
|type |int |Version type, 0: control group, 1: experimental group |
|is_mab |int |Whether it is the mab experimental version, 0: no, 1: yes |


**Experimental version winning probability**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|version_id |int |Version ID |
|probability_to_beat_all |float |Winning probability, range 0\-1 |


**Back to example**

```JSON
{
    "code": 200,
    "data": {
        "versions": [
            {
                "id": "251",
                "name": "version1",
                "type": 0,
                "is_mab": 0,
            },
            {
                "id": "252",
                "name": "version2",
                "type": 1,
                "is_mab": 0,
            },
            {
                "id": "253",
                "name": "version3",
                "type": 1,
                "is_mab": 0,
            },
                        {
                "id": "254",
                "name": "version1-mab",
                "type": 0,
                "is_mab": 1,
            },
            {
                "id": "255",
                "name": "version2-mab",
                "type": 1,
                "is_mab": 1,
            },
            {
                "id": "256",
                "name": "version3-mab",
                "type": 1,
                "is_mab": 1,
            }
        ],
        "probs": [
            {
                "version_id": "251",
                "probability_to_beat_all": 0.0,
            },
            {
                "version_id": "252",
                "probability_to_beat_all": 0.85939893
            },
            {
                "version_id": "253",
                "probability_to_beat_all": 0.14060107
            }
        ],
    },
    "message": "success"
}
```


<span id="事件创建-修改"></span>
## re\-random task information query

**Description:**  According to the heavy random task ID, query the heavy random task details

**Path:**  /openapi/v3/apps/{app_id}/rehashes/{rehash_id}

**Request method** : GET

**Return value**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment information returned by the interface |


**Data information**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|cohorts |list |Grouping information, structure and submission parameters |
|└ p_value |float |Statistical p\-value |
|metrics |list |Indicator information, structure and submission parameters |
|└ p_value |float |Statistical p\-value |
|start_ts |int |start time |
|end_ts |int |end time |
|launch_times |int |number of attempts |
|statistic_type |string |statistical type |
|threshold_value |float |statistical threshold |
|optimal_result |object |task result |
|└ rehash_id |int |re\-random task ID |
|└ status |int |Heavy Random Task Status:<br><br><br>* INITIALIZED = 99, "initialize"<br><br>* RUNNING = 0, "Running"<br><br>* SUCCESS = 1, "Success"<br><br>* FAILURE = 2, "failed"<br><br>* ADOPTED = 3, "Adopted"<br><br>* DEPRECATED = 5, "Cancelled" |
|└ fail_reason |string |reason for failure |
|└ best_hash_seed |string |optimal seed |
|└ metric_target |object |indicator heavy random task result |
|└ cohort_target |object |Grouped heavy random task result |


<span id="234ee70c"></span>
## Re\-random task state modification interface (cancel/retry/adopt)

**Description:**  Page to get the list of indicators under the APP, and add the filtering parameters of indicators that support confidence level calculation

**Path** :/openapi/v3/apps/{app_id}/rehashes/{rehash_id}

**Request method:**  PATCH

**Request parameters**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|status |int |Target Status: 5 \- Abandon Re\-Random 4 \- Retry 3 \- Adopt |


**Return value**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Experiment information returned by the interface |


**Data information**


|**Parameter name** |**Type** |**Description** |
|---|---|---|
|rehash_id |int |re\-random task ID |
|original_status |int |The original state, state information enumeration:<br><br><br>* RUNNING = 0, "Running"<br><br>* SUCCESS = 1, "Success"<br><br>* FAILURE = 2, "failed"<br><br>* ADOPTED = 3, "Adopted"<br><br>* DEPRECATED = 5, "Cancelled" |
|new_status |int |Updated status, status information enumeration:<br><br><br>* RUNNING = 0, "Running"<br><br>* SUCCESS = 1, "Success"<br><br>* FAILURE = 2, "failed"<br><br>* ADOPTED = 3, "Adopted"<br><br>* DEPRECATED = 5, "Cancelled" |


<span id="48236a5d"></span>
## Mutual exclusion domain/mutual exclusion domain group interface

<span id="aa2d8f92"></span>
### Common response structure


|Parameter name |Type |**Description** |
|---|---|---|
|`code` |Integer |Business status code. `200`is a success. |
|`message` |String |Response message. Success is usually `success`. |
|`data` |Object / Array / Integer / Null |The interface returns data, and different interface structures are different. |


<span id="9cb659f6"></span>
### public enumeration


|Field |Value |Description |
|---|---|---|
|`endpoint_type` |`0` |Client side. |
|`endpoint_type` |`1` |Server side. |


<span id="070cc8b3"></span>
### Get mutual exclusion domain traffic layer

**Description** : Paging to obtain the traffic layer of the mutual exclusion group under the APP

**Request path** :/openapi/v3/apps/< app_id \>/layers

**Request method** : GET

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`domain_id` |Query |Integer |No |Query only the layers bound under a mutual exclusion domain. |
|`domain_group_id` |Query |Integer |No |Query only the layers bound under a mutual exclusion domain group. |
|`keyword` |Query |string |No |Query keywords can be obscured by name or description. |
|`endpoint_type` |Query |Integerint |No |The end type of the mutual exclusion group. `0`is the client side layer and `1`is the server side layer. |
|`page` |Query |Integerint |No |Query the page number. Default is 1. |
|`page_size` |Query |Integerint |No |Number of pages, the default is 99. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data.layers` |Array |List of mutual exclusion layers. |
|`data.layers[].id` |Integer |Mutual exclusion layer ID. |
|`data.layers[].name` |String |Mutual exclusion layer name. |
|`data.layers[].description` |String |Mutual exclusion layer description. |
|`data.layers[].endpoint_type` |Integer |End type. `0`is the client side layer and `1`is the server side layer. |
|`data.layers[].domain_id` |Integer / Null |The mutual exclusion domain ID of the tier binding. Empty when unbound. |
|`data.layers[].domain_group_id` |Integer / Null |The mutual exclusion domain group ID to which the layer belongs. Empty when the mutual exclusion field is not bound. |
|`data.layers[].available_traffic` |Float |Layer currently available traffic. |
|`data.page.current_page` |Integer |The current page number. |
|`data.page.total_pages` |Integer |Total number of pages. |
|`data.page.total_items` |Integer |Total number of articles. |


**Request example**

```HTTP
GET /datatester/openapi/v3/apps/20000930/layers?endpoint_type=1&domain_id=456
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": {
    "layers": [
      {
        "id": 1001,
        "name": "domain A layer",
        "description": "created by openapi",
        "endpoint_type": 1,
        "domain_id": 456,
        "domain_group_id": 123,
        "available_traffic": 0.9
      }
    ],
    "page": {
      "current_page": 1,
      "total_pages": 1,
      "total_items": 1
    }
  }
}
```


<span id="a2d958c8"></span>
### Mutual exclusion domains create traffic layers

**Description** : Mutual exclusion domain creates traffic layer

**Request path** : `/openapi/v3/apps/< app_id >/layers`

**Request method** : POST

**Request parameters**


|Parameter name |Location |Type |Is it necessary |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`name` |Body |String |Yes |Mutual exclusion layer name. It cannot be repeated under the same application. |
|`endpoint_type` |Body |Integer |Yes |End type. `0`is the client side layer and `1`is the server side layer. |
|`description` |Body |String |No |Mutual exclusion layer description. |
|`domain_id` |Body |Integer |No |Mutual exclusion domain ID. When passing in, the server side verifies that the mutual exclusion field exists, is not deleted, belongs to the current application, and the end type is consistent with the `endpoint_type`. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Integer |Create a successful mutual exclusion layer ID. |


**Request example**

```JSON
{
  "name": "domian A layer",
  "description": "created by openapi",
  "endpoint_type": 1,
  "domain_id": 456
}
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": 1001
}
```


<span id="ec8ab822"></span>
### Get a list of mutual exclusion domain groups

**Description**: Get mutual exclusion domain group list data, including mutual exclusion domain group name, end type, and the total number of mutual exclusion layers bound under the domain group.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups

**Request method** : GET

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`endpoint_type` |Query |Integer |No |End type. `0`is the client side layer and `1`is the server side layer. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data.domain_group` |Array |List of mutual exclusion domain groups. |
|`data.domain_group[].id` |Integer |Mutual exclusion domain group ID. |
|`data.domain_group[].name` |String |Mutual exclusion domain group name. |
|`data.domain_group[].endpoint_type` |Integer |End type. `0`is the client side layer and `1`is the server side layer. |
|`data.domain_group[].total_layer_count` |Integer |Total number of mutual exclusion layers bound under the domain group. |
|`data.domain_group[].total_domain_count` |Integer |The number of mutual exclusion domains under the domain group. |


**Request example**

```HTTP
GET /datatester/openapi/v3/apps/20000930/domain-groups?endpoint_type=1
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": {
    "domain_group": [
      {
        "id": 123,
        "name": "server side domain group",
        "endpoint_type": 1,
        "total_layer_count": 2,
        "total_domain_count": 2
      }
    ]
  }
}
```


<span id="a2b550b9"></span>
### Creating mutual exclusion domain groups

**Description**: Specify the application ID, mutual exclusion domain group name, end type and other information to create a mutual exclusion domain group.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups

**Request method**: POST

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`name` |Body |String |Yes |Mutual exclusion domain group name. |
|`endpoint_type` |Body |Integer |Yes |End type. `0`is the client side layer and `1`is the server side layer. |
|`domain_list` |Body |Array |Yes |List of mutual exclusion domains, containing at least two mutual exclusion domains. |
|`domain_list[].name` |Body |String |Yes |Mutual exclusion of domain names. |
|`domain_list[].traffic` |Body |Float |Yes |Mutual exclusion domain traffic percentage, Example `0.5`means 50%. |
|`domain_list[].layer_ids` |Body |Array |Yes |List of mutual exclusion layer IDs bound to the mutual exclusion domain. An empty array indicates that the layer is not bound. |
|`domain_list[].domain_group_ids` |Body |Array |Yes |List of child mutual exclusion domain group IDs bound to the mutual exclusion domain. An empty array indicates that the subfield group is not bound. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The request parameters only support the above fields and do not support passing in other fields.</div>


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Integer |Create a successful mutual exclusion domain group ID. |


**Request example**

```JSON
{
  "name": "server side domain group",
  "endpoint_type": 1,
  "domain_list": [
    {
      "name": "domian A",
      "traffic": 0.5,
      "layer_ids": [1001],
      "domain_group_ids": []
    },
    {
      "name": "domian B",
      "traffic": 0.5,
      "layer_ids": [],
      "domain_group_ids": [2001]
    }
  ]
}
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": 123
}
```


<span id="f894e740"></span>
### Replication mutual exclusion domain group

**Description**: Copy a new mutual exclusion domain group based on the source mutual exclusion domain group, and set the replicated mutual exclusion domain group name.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups

**Request method**: POST

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`origin_id` |Body |Integer |Yes |The source mutual exclusion domain group ID that was replicated. |
|`name` |Body |String |Yes |The mutual exclusion domain group name after replication. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Integer |New mutual exclusion domain group ID after successful replication. |


**Request example**

```JSON
{
  "origin_id": 123,
  "name": "server side domain group-copy"
}
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": 124
}
```


<span id="dbb80405"></span>
### Get mutual exclusion domain group details

**Description**: Query the details of the mutual exclusion field group, including name, end type, mutual exclusion field list under the field group, mutual exclusion field information, etc.

**Path** :/openapi/v3/apps/{app_id}/domain\-groups/{domain_group_id}

**Request method** : GET

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`domain_group_id` |Path |Integer |Yes |Mutual exclusion domain group ID. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data.id` |Integer |Mutual exclusion domain group ID. |
|`data.name` |String |Mutual exclusion domain group name. |
|`data.endpoint_type` |Integer |End type. `0`is the client side layer and `1`is the server side layer. |
|`data.domain_list` |Array |List of mutual exclusion domains under the domain group. |
|`data.domain_list[].id` |Integer |Mutual exclusion domain ID. |
|`data.domain_list[].name` |String |Mutual exclusion of domain names. |
|`data.domain_list[].traffic` |Float |Mutual exclusion domain traffic ratio. |
|`data.domain_list[].layer_ids` |Array |List of mutual exclusion layer IDs bound under this domain. |
|`data.domain_list[].domain_group_ids` |Array |List of child mutual exclusion domain group IDs bound under this domain. |


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": {
    "id": 123,
    "name": "server side domain group",
    "endpoint_type": 1,
    "domain_list": [
      {
        "id": 456,
        "name": "domian A",
        "traffic": 0.5,
        "layer_ids": [1001],
        "domain_group_ids": []
      }
    ]
  }
}
```


<span id="3f738441"></span>
### Editing mutual exclusion field groups

**Description**: Edit the name of the specified mutual exclusion field group, the mutual exclusion field list, the bound mutual exclusion layer and other information.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Editing uses full replacement semantics: the <code>domain_list</code>passed in is the full list of fields; a field pass empty <code>layer_ids</code>or <code>domain_group_ids</code>indicates unbinding the corresponding object.</div>


**Path**:/openapi/v3/apps/{app_id}/domain\-groups/{domain_group_id}

**Request method**: PUT

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`domain_group_id` |Path |Integer |Yes |Mutual exclusion domain group ID. |
|`name` |Body |String |Yes |Mutual exclusion domain group name. |
|`domain_list` |Body |Array |Yes |A complete list of mutual exclusion domains, containing at least two mutual exclusion domains. |
|`domain_list[].id` |Body |Integer |No |There is a mutual exclusion domain ID. The new domain is not uploaded. |
|`domain_list[].name` |Body |String |Yes |Mutual exclusion of domain names. |
|`domain_list[].traffic` |Body |Float |Yes |Mutual exclusion domain traffic ratio. |
|`domain_list[].layer_ids` |Body |Array |Yes |List of mutual exclusion layer IDs bound to this domain. |
|`domain_list[].domain_group_ids` |Body |Array |Yes |List of mutual exclusion domain group IDs for this domain binding. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The request parameters only support the above fields and do not support passing in other fields.</div>


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Integer |The mutual exclusion domain group ID after successful editing. |


**Request example**

```JSON
{
  "name": "server side domain group-v2",
  "domain_list": [
    {
      "id": 456,
      "name": "domian A",
      "traffic": 0.4,
      "layer_ids": [1001],
      "domain_group_ids": []
    },
    {
      "name": "domian C",
      "traffic": 0.6,
      "layer_ids": [],
      "domain_group_ids": [2001]
    }
  ]
}
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": 123
}
```


<span id="f9d837ab"></span>
### Removing mutual exclusion domain groups

**Description** : Deletes the specified mutual exclusion field group. It cannot be restored after deletion, please proceed with caution.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups/{domain_group_id}

**Request method**: DELETE

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`domain_group_id` |Path |Integer |Yes |Mutual exclusion domain group ID. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Integer |The mutual exclusion domain group ID that was successfully deleted. |


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": 123
}
```


<span id="6a7822b5"></span>
### Get a list of bindable mutual exclusion field groups

**Description**: When used to edit mutual exclusion fields, select the child mutual exclusion field group that can be bound to a mutual exclusion field. The interface excludes domain groups that have formed illegally nested links, and can filter by end type.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups/bind\-list

**Request method**: GET

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`endpoint_type` |Query |Integer |No |End type. `0`is the client side layer and `1`is the server side layer. |
|`domain_group_id` |Query |Integer |No |The mutual exclusion domain group ID currently being edited. After passing in, it excludes itself and illegal parent\-child links. |


**Response parameters**


|Parameter name |Type |Description |
|---|---|---|
|`data` |Array |List of bindable mutual exclusion domain groups. |
|`data[].id` |Integer |Mutual exclusion domain group ID. |
|`data[].name` |String |Mutual exclusion domain group name. |
|`data[].endpoint_type` |Integer |End type. |
|`data[].total_layer_count` |Integer |Total number of mutual exclusion layers bound under the domain group. |
|`data[].total_domain_count` |Integer |The number of mutual exclusion domains under the domain group. |


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": [
    {
      "id": 2001,
      "name": "can-be-binding subdomain groups",
      "endpoint_type": 1,
      "total_layer_count": 0,
      "total_domain_count": 2
    }
  ]
}
```


<span id="e0504e24"></span>
### Unbind subgroup mutual exclusion domain group

**Description**: Unbind the submutual exclusion field group.

**Path**:/openapi/v3/apps/{app_id}/domain\-groups/unbind

**Request method** : POST

**Request parameters**


|Parameter name |Location |Type |Is it required? |Description |
|---|---|---|---|---|
|`app_id` |Path |Integer |Yes |App ID. |
|`domain_group_id` |Body |Integer |Yes |The mutual exclusion domain group ID to be untied. |


**Request example**

```JSON
{
  "domain_group_id": 2001
}
```


**Response example**

```JSON
{
  "code": 200,
  "message": "success",
  "data": null
}
```


<span id="五-业务错误码说明"></span>
# 5. Business Error Code Description

Returns the detailed definition of the code in the message body


|Error code |Meaning |
|---|---|
|200 |success |
|403 |No permissions to the requested resources (apps, experiments, etc.) |
|404 |The requested resource does not exist, such as querying for a non\-existent experiment ID or metric ID. |
|410 |The requested resource has been deleted |
|40000 |Required parameters are missing |
|40001 |Parameter value error |
|40003 |No access to the requested interface |
|40010 |Excessive calls (exceeding the call per second limit) |
|40011 |Exceeds the daily call limit |
|60001 |DSL format error |
|60002 |The indicator has associated experiments and cannot be deleted. |
|60010 |Insufficient traffic to create experiments |
|60011 |The endpoint_type of the experiment is inconsistent with the mutual exclusion group |
|60012 |The experiment cannot be ended during the test |
|60013 |Draft state experiments cannot be queried or modified by openAPI |
