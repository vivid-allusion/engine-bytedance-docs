---
title: "Open Interface (Old Version)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Open-Interface-Old-Version"
---

<span id="一-概述"></span>
# 1. Overview

This document provides a description of the open interface in the "A/B Testing" application.

Available range includes:


* Experimental information: experimental configuration, experimental filtering parameters

* Report information: experimental index report, experimental retention report

* Experimental operation: create an experiment, modify the experimental state

* Other: list of indicators, list of mutual exclusion groups


<span id="二-联系开通"></span>
# 2. Contact us to open

In order to ensure the security of your and your users' data, open interface permissions are turned off by default.

Before you start using it, you need to contact us to open it. (You can get in touch with us through the Lark/WeChat group connected to the service or the online customer service in the lower right corner of the page)


* After opening, we will provide you with the AK/SK required for export. Please be sure to keep and use it properly after receiving it.

* When opening, please confirm the interface usage quota with the docking staff. Interface requests that exceed the quota will be rejected.


<span id="三-使用方式"></span>
# 3. How to use

<span id="sdk接入"></span>
## SDK access

The export of experimental data needs to be connected to the relevant SDK of OpenAPI. We provide Python SDK and Java SDK. SDK download address:

[SDK download](https://byterangers.bytedance.com/byterangers/api/doc?id=88&op_type=download_doc_by_id&sdk_type=openapi).

After the Python SDK is downloaded, execute the command in the shell to complete the installation.

```Plain
# python 2.7 is required.
easy_install rangersdk-0.0.1-py2.7.egg
```


<span id="调用示例"></span>
## Call example

```Plain
from rangersdk.client import RangersClient
import ujson

ak = '{replace with AK}'
sk = '{replace with SK}'
bc = RangersClient(ak, sk)

# Get Method Example
def test1():
    params = {'{key}': '{value}'} # parameter, optional
    resp = bc.data_tester('/openapi/v1/164287/details', params=params, method='get') # get request method
    print(resp.content) # print returned results
    res = resp.json() # Convert the results to JSON format
    self.assertEqual(200, res['code'], 'err message: {}'.format(res['message']))

# Post Method Example
def test2():
    params = {'{key}': '{value}'} # parameter, optional
    resp = bc.data_tester('/openapi/v1/openapi-test', body=ujson.dumps(params), method='post') # post request method
    print(resp.content) # print returned results
    res = resp.json() # Convert the results to JSON format
    self.assertEqual(200, res['code'], 'err message: {}'.format(res['message']))
```


<span id="四-可用接口"></span>
# 4. Available interface

<span id="获取实验配置"></span>
## Get experimental configuration

Interface description: Obtain basic information about the configuration of the experiment

Request path: `/openapi/v1/apps/< app_id >/experiment/< experiment_id >/details`

Request method: GET

Request required parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|experiment_id |int |ID of the experiment |


Interface return value:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Interface Return Experiment Information Configuration |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|id |int |The flight_id of the experiment |
|name |string |name of experiment |
|start_ts |string |experiment start time |
|end_ts |string |Experiment end time |
|owner |string |The experiment creator's user_id |
|description |string |experimental description |
|status |int |Experimental Status, 0: Completed 1: In Progress 2: Pending Scheduling 3: Testing 4: Draft |
|type |string |Experiment type, client: client side server: server level |
|mode |int |Experiment Mode, 1: Programming Experiment 2: Multi\-Link Experiment 3: Visualization Experiment |
|layer |object |Attributes related to the layer where the experiment is located, see the example description for details |
|version_resourse |float |The proportion of traffic allocated for this experiment |
|versions |list |Experimental version related properties, see the example description for details |
|metrics |list |Experimental metrics related properties, see the example description for details |
|features |object |Experimental features, see the example description |
|filter |string |user filter |
|whitelist |list |User whitelist, see example description for details |


Interface return example:

```Plain
{
  'code'：200
  "data": {
    "id": 3799, # Experiment ID
    "name": "real-time metric report test", # experiment name
    "start_ts": "2020-07-08 11:39:02", # experiment start time
    "end_ts": "2021-07-08 11:39:02", # experiment end time
    "owner": "203870", # creator
    "description": "", # experiment description
    "status": 1, # experiment status, 0: Completed 1: In progress 2: To be scheduled 3: Testing  4: Draft
    "type": "client", # experiment type, client: client side server: server side
    "mode": 1, # experiment mode, 1: Programming Experiment 2: Multi Link Experiment 3: Client Experiment
    "layer": { # experiment layer
      "name": "mutal exclusion group1", # mutal exclusion layer name
      "status": 1, # mutual exclusion layer status, 0: closed 1: open
       "description": "Default layer when creating LS test scenario five experiment", # mutual exclusion layer description
       "type": "NULL" # mutal exclusion layer type, default: mutex: NULL: 
    },
    "version_resource": 1.0, # traffic allocation
    "versions": [
      {
        "id": 8572, # version ID
        "name": "control version", # version name
        "type": 0, # version type，0:control version 1:experiment version 
        "config": { # version configuration
          "hello12341": false
        },
        "description": "", # version description
        "weight": 30 # Version weight
      },
      ...
    ],
    "metrics": [
      {
        "id": 10065, # metric ID
        "name": "test metric", # metric name
        "metric_description": "test metric description ", # metric description
        "type": "major", # metric type, major: core, normal: normal
        "support_conf": true, # Whether can calculate confidence
        "offline": false, # Whether is offline metric
        "dsl": {
          "queries": [ # event details
            {
              "show_label": "A",
              "event_type": "origin", # event type
              "show_name": "活跃均次（pv/au）", # event property
              "event_name": "predefine_pageview", # event name
              "filters": [ # event filter condition
                {
                  "property_operation": "!=", # filter operator
                  "property_type": "event_param", # type of filter condition
                  "property_name": "title", # name of filter condition
                  "property_values": [ # value of filter condition
                    "this is a title"
                  ]
                }
              ],
            },
            ...
          ]，
          "event_relation": "A*1" #  The relationship between mixed metrics
        },
        "composed": false # whether is composite metric
      },
    ],
    "features": {
      "id": -1, # associate feature ID. If is not associated, then fill -1
      "name": "",
      "key": ""
    },
    "filter": "", # user filter condition
    "whitelist": [ # whitelist of all experiments
      {
        "control version": [
          {
            "ssids": ["bbc33321-4352-4b95-91d1-lishanlishanlishan"], # user ssid
            "id": 81, # whitelist ID
            "is_deleted": false,
            "name": "李珊", # creator name
            "description": "", # whitelist description
            "tags": [] # whitelist tag
          }，
        ]
      },
    ],
  }
  'message'：'success'
}
```


<span id="获取实验过滤参数"></span>
## Acquire experimental filter parameters

Interface description: Get the parameters of the filter experimental report, and use the parameters returned by this interface to filter the experimental report and experimental retention

Request path: `/openapi/v1/apps/< app_id >/filters`

Request method: GET

Request required parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |


Interface return value:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Interface returns filter parameter information |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|filter_rule |list |List of filter parameters returned by the interface |


filter_rule information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|key |string |Filter parameter primary key name |
|label |string |The name of the filter parameter display can be understood as the parameter description |
|type |string |Parameter type |
|preset |int |Whether it is the default parameter, different from user\-defined properties |
|values |list |Filter parameter optional value |
|mode |string |Mode of filter parameters, fill in the blanks: input enumeration: select mix: multiple |
|operators |list |Filter parameters optional operation |


Interface return example:

```Plain
{
  "code": 200
  "data": {
    'filter_rule': [ # filter parameter 
      {
        "key": "referrer", # filter parameter key
        "label": "前向地址",  # filter parameter name
        "type": "string", # parameter type
        "preset": 1, # whether is default parameter
        "values": [
          {
            'value': 'https://www.sogou.com/web?query=xxxx' # value of 'value'
            'label': 'https://www.sogou.com/web?query=xxxx' # value name
          },
          ...
        ],
        'mode': 'multiple', # filter parameter mode, fill-in:input enumeration:select composite:multiple
        'operators': [ # filter parameter operation method
          {
            "label": "≠", # operator
            "value": "ne", # operation code
            "desc": null, # operation description
            "mode": "select" # operation input method, fill-in:input enumeration:select
          }
        ]
      },
      ...
    ]
  },
  'message': 'success'
}
```


How to use filter parameters:

```Plain
fliters = [
  {
    'type': 'string',
    'op': 'ne',
    'key': 'app_channel',
    'value': '23' / ['a', 'b'] # single value/multiple value filter
  },
  ...
]
```


<span id="计算实验指标"></span>
## Calculate experimental metrics

Interface description: Calculate and return experimental metrics reports

Request path: `/openapi/v1/apps/< app_id >/experiment/< experiment_id >/metrics`

Request method: GET

Request required parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|experiment_id |int |ID of the experiment |
|report_type |string |Report type, day: day hour: hour five_minute: five minutes |
|start_ts |string |Calculate the start time (timestamp) |
|end_ts |string |Calculate the end time (timestamp) |
|filters |list |Experimental filter parameters, obtained from the "Get Experimental Filter Parameters" interface |


Interface return value:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Interface returns experimental index information |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|report_type |string |Report type, day: day hour: hour five_minute: 5 minutes |
|versions |list |Experimental version information, see the example description for details |
|metrics |list |Experiment\-related metrics, see the example description for details |
|start_ts |string |Calculate the start time (timestamp) |
|end_ts |string |Calculate the end time (timestamp) |
|user_data |object |Total number of participants per version |
|calculation_results |object |Experimental index calculation results, see the example description for details |


Interface return example:

```Plain
{
  "code": 200,
  "data": {
    "report_type": "day", # report type, day:day hour:hour five_minute:5 minutes
    "versions": [
      {
        "id": 8572, # version ID
        "name": "control version", # version name
        "config": {
          "hello12341": false
        },
        "type": 0, # version type，0:control version 1:experiment version         
        "weight": 0  # Version weight
      },
    ],
    "metrics": [
      {
        "id": 10065,
        "name": "test metric",
        "metric_description": "test metric description ",
        "type": "major", # metric type, major: core, normal: normal
        "support_conf": true,
        "offline": false,
        "composed": false
      },
      ...
    ],
    "start_ts": 1594179542, # experiment start time
    "end_ts": 1597247999, # experiment end time
    "user_data": {
      "8572": 415248, # experiment total account of join group people
      "8573": 415261
    },
    "calculation_results": {
      "10013": { # metric ID
        "8572": { # experiment version ID, the following similar numbers represent the values calculated for this experiment relative to another experiment
          "m": 1.367, # 
          "p": {
            "8573": -1 # -1 indicates not exist, if less than 0.05, then confidence
          },
          "change": 0.09640731971910832, # variation value
          "change_rate": {
            "8573": -0.00053 # variation rate
          },
          "conf_interval": {
            "8573": [0,0] # confidence interval
          },
          "half_interval": {
            "8573": 0 # Mid point of confidence interval
          },
          "confidence": {
            "8573": 3 # confidence status, 1: positive 2: negative 3: no confidence 4: newly created experiment
                      # 5: Data to be updated 6: Confidence cannot be calculated 7: No users have joined the group 8: Paused
          }，
          "mde": 0.012623757553642818 # minimum observation differenceMDE(minimum detectable effect)
        },
        ...
      },
      ...    
    }
  },
  "message": "success"
}
```


<span id="计算实验留存"></span>
## Computational Experiment Retention

Interface description: Calculate and return experimental metrics reports

Request path: `/openapi/v1/apps/< appid >/experiment/< experiment_id >/retention`

Request method: GET

Request required parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|experiment_id |int |ID of the experiment |
|start_ts |string |Calculate the start time (timestamp) |
|end_ts |string |Calculate the end time (timestamp) |
|filters |list |Experimental filter parameters, obtained from the "Get Experimental Filter Parameters" interface |


Interface return value:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Interface returns experiment retention information |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|start_ts |string |Calculate the start time (timestamp) |
|end_ts |string |Calculate the end time (timestamp) |
|versions |object |Experimental version information, see the example description for details |
|confidence_level |int |confidence level |
|calculation_details |object |The experiment retains daily data, as detailed in the example description |
|calculation_results |object |Experiment retention statistics, as detailed in the sample description |


Interface return example:

```Plain
{
  "code": 200
  "data": {
    "available_start_ts": 1594137600, # experiment start time
    "available_end_ts": 1597247999, # experiment end time
    "start_ts": 1594656000, # start time
    "end_ts": 1597247999, # end time
    "versions": [
      {
        "id": 8572, # version ID
        "name": "control version", # version name
        "config": {
          "hello12341": false
        },
        "type": 0, # version type
        "weight": 0 # Version weight
      },
    ],
    "confidence_level": 90, # confidence
    "calculation_details": { # Retain daily data
      'Users who joined the group on that day': { # 
        '8672': [ # Experiment ID
          [
            1597161600, # date (timestamp)
            5, # retention rate，-1  indicates not exist, the value of “Users who joined the group on that day” equals account of newly joined group users
            5.0 # newly joined users number, -1 indicates not existing
          ],
          ...
        ],
        ...  
      },
      ...
    }，
    'calculation_results': { # Retain statistical data
      "second day retention": {
        "data": { # retention rate
          "8572": 0.0022,
          "8573": 0.0022
        },
        "confidence": { # confidence status, 1: positive 2: negative 3: no confidence 4: newly created experiment
                        # 5: Data to be updated 6: Confidence cannot be calculated 7: No users have joined the group 8: Paused
          "8572": {
            "8573": 0
          },
          "8573": {
            "8572": 0
          }
        },
        "p": { # p value
          "8572": {
            "8573": 0.998318
          },
          "8573": {
            "8572": 0.998318
          }
        },
        "half_interval": { # Mid point of confidence interval
          "8572": {
            "8573": 0.17499327964828007
          },
          "8573": {
            "8572": 0.17504366124523396
          }
        },
        "change_rate": { # variation rate
          "8572": {
            "8573": -0.000288
          },
          "8573": {
            "8572": 0.000288
          }
        },
        "conf_interval": { # confidence nterval
          "8572": {
            "8573": [
              -0.175281,
              0.174705
            ]
          },
          "8573": {
            "8572": [
              -0.174756,
              0.175332
            ]
          }
        },
        "nums": { # Total number of new team members on the day
          "8572": 107,
          "8573": 107
        }
      },
    }
  },
  'message': 'success'
}
```


<span id="创建实验"></span>
## Create an experiment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Experiments created by open interfaces can only be edited by administrators</div>


Interface description: Create an experiment

Request path: `/openapi/v2/apps/< app_id >/experiments`

Method: POST

Request required parameters:


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |**Remarks** |
|---|---|---|---|---|
|app_id |int |Yes |App ID | |
|name |string |Yes |name of experiment |Cannot duplicate existing experiments, length 50 characters |
|mode |int |Yes |Type of experiment |Currently only 1. |
|description |string |No |experimental description |Length 1000 characters |
|endpoint_type |int |Yes |Type of experiment |Client side experiment: 0, server level experiment: 1 |
|duration |int |Yes |experiment duration |Unit day, [1,365], integer |
|major_metric |int |Yes |Core Metric ID |Currently only one core indicator is supported. |
|metrics |list |Yes |list of indicator IDs |1. Must include [major_metric] id, 2. Must include [Must see indicator] id, 3. If there is a funnel type indicator, there can only be one |
|versions |list |Yes |Experimental version |Version structure, version number \> = 2 |
|layer_info |object |No |Mutual exclusion group |layer_info structure |


Version structure:


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |**Remarks** |
|---|---|---|---|---|
|type |int |Yes |Control version/experimental version |0: Comparison Version 1: Experimental Version |
|name |string |Yes |version name |Length 50 characters |
|description |string |No |version description |Length 1000 characters |
|weight |float |No |traffic allocation |0.5 Minimum particle size 0.01, uniform distribution without transmission |
|config |object |Yes |Version parameters Different versions of the key need to be consistent | |
|users |list |No |whitelist user |[{"ssids": ["009e50ea\-fb8e\-4bb3\-a2a1\-4b14ba9ce007","009e50ea\-fb8e\-4bb3\-a2a1\-4b14ba9ce006"],"type": "id"}] |


layer_info structure:


|**Parameter name** |**Parameter type** |**Is it required?**  |**Description** |**Remarks** |
|---|---|---|---|---|
|layer_id |int |Yes |Mutual exclusion group ID |No pass \-1 |
|version_resource |float |Yes |percentage of traffic occupied |0.7 is less than or equal to the remaining flow of the layer (available_traffic) |


Interface return value:


|**parameter name** |**Parameter type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |int |Newly Created Experiment ID |


Example of interface request parameters:

```Plain
{
    "name":"test experiment 2022041901",
    "mode": 1,
    "endpoint_type": 1,
    "duration": 20,
    "major_metric": 29806,
    "metrics": [29806],
    "versions": [
        {
            "type": 0,
            "name": "experimental group 2022041901",
            "config": {"shiyu_key": "hello"}
        },
        {
            "type": 1,
            "name": "control group 2022041901",
            "config": {"shiyu_key": "world"}
        }
    ],
    "layer_info": {
        "layer_id": -1,
        "version_resource": 0.7
    }
}
```


<span id="修改实验状态"></span>
## Modify the experimental state

Interface description: Experimental open and end state operations

Request path:


* Start experiments: `/openapi/v2/apps/< app_id >/experiments/< experiment_id >/launch/`

* End the experiment: `/openapi/v2/apps/< app_id >/experiments/< experiment_id >/stop/`


Request method: PUT

Request required parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|experiment_id |int |Experiment ID |


<span id="获取指标列表"></span>
## Get a list of metrics

Interface description: Get all indicator information under the current APP

Request path: `/openapi/v2/apps/< app_id >/metrics`

Request method: GET

Interface request parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|keyword |string |Fuzzy search keyword, space\-time query all |
|need_page |int |0: No paging is required, page and other parameters do not take effect, 1: Paging is required, page and other parameters take effect |
|page_size |int |Number of pages per page |
|page |int |Current page, starting from 1 |


Interface return information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |Interface returns indicator information and paging information |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|page |object |Paging information, page structure |
|metrics |list |Indicator name, metric structure |


Page structure:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|current_page |int |current page |
|total_page |int |total number of pages |
|total_items |int |total number of articles |


Metric structure:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|id |int |indicator ID |
|name |string |Indicator name, length 50 characters |
|description |string |Indicator description, possibly empty |
|type |string |indicator type |
|is_support_major |boolean |Can it be set as the core indicator? |
|is_required |int |Whether it is a must\-see indicator, 0: must\-see indicator, 1: non\-must\-see indicator |


<span id="获取互斥组列表"></span>
## Get a list of mutual exclusion groups

Interface description: Get all layer information under the current APP (mutual exclusion group)

Request path: `/openapi/v2/apps/< app_id >/layers`

Request method: GET

Interface request parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|app_id |int |App ID |
|keyword |string |Fuzzy search keyword, space\-time query all |
|need_page |int |0: No paging is required, page and other parameters do not take effect, 1: Paging is required, page and other parameters take effect |
|page_size |int |Number of pages per page |
|page |int |Current page, starting from 1 |


Interface return value:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |list |Interface returns mutual exclusion group list |


Data information:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|id |long |Mutual exclusion group ID |
|name |string |Mutual exclusion group name, length 50 characters |
|available_traffic |int |residual flow |
|type |string |Mutual exclusion group type, client side experiments can only add client side mutual exclusion groups, server level experiments can only add server level mutual exclusion groups. Client side: client, server level: server |


<span id="五-接口返回码列表"></span>
# 5. Interface return code list

The HTTP status code constraints are as follows:


|**HTTP status code** |**Returned module** |**Semantics** |**Description** |**How the client side handles** |
|---|---|---|---|---|
|200 |business module |The business has completed the processing of this request. (Whether it's success or failure) |In the case of failure, the specific cause of the error is defined by returning the code in the message body. |normal processing |
|302 |business module |request redirect |Redirect the request to the corresponding address |Resend request |
|403 |business module |ban access |Such as interface authentication failure, token failure, invalid access_token, the specified user has no operation authority |The client side needs to log the context in order to find the problem. |
|404 |gateway |There is no such interface. |Interface not implemented |Handle by error, do not try again |
|499 |gateway |The request has not been completed. | |According to error handling, you can try again. |
|500 |business module |During the processing of the business, an unexpected error occurred. |For example, an exception was not caught. |According to error handling, you can try again. |
|502/503 |gateway |Gateway error during forwarding request |For example, too many connections to a business module |According to error handling, you can try again. |


Returns the detailed definition of the code in the message body:


|**Error code** |**Meaning** |
|---|---|
|200 |success |
|4001 |Parameter validation failed. Details are given in the message |
|4002 |permission verification failed |
|5001 |interface internal exception |
|5002 |Database operation failed |
|5003 |dependency service request failed |
