---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters__"
---

<span id="89396d52"></span>
# 1. Overview

This document provides a description of the cluster\-related interfaces in BytePlus Growth Analysis.

Cluster\-related interface capabilities include:


* Get cluster list

* Get the specified cluster information

* Get the user list information for the specified subgroup

* Download the list of users in the specified group

* rule creation grouping

* refresh clustering

* Upload file to create cluster

* delete clustering

* Modify grouping


Note: The current upper limit of exported clustering is 300W.

<span id="7b7c1489"></span>
# 2. API public parameters

**Context\-path**: /datafinder

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|app_id |int |Yes |123456 |App ID |


**Response**:

```json
{
        "code": 200,
        "message": "success"
        "data": xxx
}
```



* Code status code, 200 indicates success, other non\-failures

* Message Success or failure message

* Data result data, refer to the specific API description for the specific structure


<span id="cc690889"></span>
# 3. Clustering OpenAPI\-DSL structure description

The following provides you with a detailed description of the DSL structure used for rule clustering.

<span id="22ee330a"></span>
## DSL structure description

<span id="06f26e76"></span>
### Get the clustering DSL from the front end (recommended)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26f03cb533b04fcf8431413841d417cd~tplv-goo7wpa0wc-image.image) </span>

Configure the rules in the cluster configuration page, open the browser console; then click "Estimated number of people" to view the dsl_content field of the overview interface. (Note: When using dsl_content, it is best to delete the show_option node as a whole)

<span id="1349ccc3"></span>
### Overall structure

The overall structure of the grouped DSL is consistent with the overall structure used by the query API. For the overall structure, please refer to: "Query API" \- \> "DSL Structure" description.

The difference in grouping is in the queries field of content, which extends the corresponding meaning. Overall structure:

```json
{
  "version": 3,             # the versions of DSL in this document are 3
  "app_ids": [],            # target app    
  "use_app_cloud_id": true, # Whether is app_cloud_id in app_ids parameter. Please set to true, false for internal use only.
  "periods": [],            # time periods, is fixed as [] in cohorts
  "content": {},            # detailed query content field
  "option": {},             # json format data, the option parameter which is request related, this field is not required in cohorts
  "show_option": {}         # json format data, return the original data in the result, this field is not required in cohorts
}
```


The specific rules are defined in the cotent field:

```json
{
  "content": {
      "query_type": "cohort_v3_idlist",  # use this type fixedly
      "queries":[                       # cohorts rule
           [{query1},{query2}], 
           [{query3},{query4}]
        ]
       "option":{},                     # cohorts parameter
       "profile_filters":[],            # fixed as[]
       "profile_groups":[]              # fixed as[]
  }
}
```


<span id="170b3380"></span>
### Field details

<span id="90cbab5f"></span>
#### Option field

```json
{
 "cohort": {
     "outer_logic": "and"
 }
}
```



|**Field** |**Value and meaning** |**Is it necessary** |**Example** |
|---|---|---|---|
|outer_logic |The outermost logical relationship: and/or |No |Default and |


<span id="d7c949d2"></span>
#### Queries field

```json
[                     
   [{query1},{query2}], 
   [{query3},{query4}]
   ...
]
```


<span id="1c5a0f03"></span>
##### Query logical relationship

A query is a two\-dimensional array that defines the relationship between each rule.

When the `outer_logic`is `and`: the relationship of the inner array is `or`, and the outer relationship is `and`. For example:

```json
"queries":[                       # cohorts rule
   [{query1},{query2}], 
   [{query3},{query4}]
 ]
"option":{
   "cohort": {
     "outer_logic": "and"
   }
},
```


Then the overall computational relationship is:

```plain
[query1  or query2] and [query3 or query4]
```


When the `outer_logic`is or: the relationship of the inner array is `and`the outer relationship is `or`. For example:

```json
"queries":[                       # cohorts rule
   [{query1},{query2}], 
   [{query3},{query4}]
 ]
"option":{
   "cohort": {
     "outer_logic": "or"
   }
},
```


Then the overall computational relationship is:

```plain
[query1  and query2] or [query3 and query4]
```


<span id="af4c7a68"></span>
##### query structure

For the overall structure, refer to "Query API" \- \> "DSL Structure" \- \> "Content Fields/Queries".

```json
{
  "event_name": "any_event",
  "event_id":1,
  "event_type": "origin",
  "show_name": "总次数", //total amount
  "groups_v2": [],
  "filters": [],
  "show_label": "A",
  "event_indicator": "events",
  "measure_info": {},
  "condition":{},
  "logic": true,
  "sequence_first":true,
  "next_query_lable":"B",
}
```


Description of the meaning of the new field:


|**Field** |**Value and meaning** |**Is it necessary** |**Example** |
|---|---|---|---|
|condition |The conditions for grouping, the structure is the same as the DSL "condition" structure |Yes | |
|logic |True means the user has done it, the user is; false means the user has not done it, the user is not |Yes |Note: When logic is true, and the user has done it, such as selecting the number of events the user has done, greater than {n}, the value of n must be a value greater than 0. If you want to select "The number of times the user has done event A = 0", use "The condition that the user has not done event A" |
|sequence_first |True means "done in sequence" and is the first event done in sequence |No |"Do it in turn" is a must. |
|next_query_label |show_label value of the next event "done in sequence" |No | |


Condition structure:

Overall structure, refer to "Query API" \- \> "DSL structure" \- \> "content field/condition"

```json
{
      "property_operation": ">",
      "property_values": [0],
      "period": {}
 }
```


Description of the meaning of the new field:


|**Field** |**Value and meaning** |**Is it necessary** |**Example** |
|---|---|---|---|
|period |Time range of grouping conditions, refer to DSL period structure |No |It must take time to select events or all_value user properties |


<span id="9d8ea6dd"></span>
## Sample

<span id="d044cf9f"></span>
### User did

```json
{
    "periods": [],
    "version": 3,
    "use_app_cloud_id": true,
    "app_ids": [
        164314
    ],
    "content": {
        "option": {
            "cohort": {
                "outer_logic": "and"
            }
        },
        "query_type": "cohort_v3_idlist",
        "profile_filters": [],
        "profile_groups": [],
        "queries": [
            [
                {
                    "show_label": "c06bed36-eede-4174-91bf-8f37eac3a8ee",
                    "event_name": "any_event",
                    "event_type": "origin",
                    "logic": true,
                    "event_indicator": "events",
                    "measure_info": {},
                    "condition": {
                        "property_operation": ">=",
                        "property_values": [
                            1
                        ],
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        }
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": []
                            }
                        }
                    ]
                }
            ]
        ]
    }
}
```


<span id="bf20253b"></span>
### The user has not done it.

```json
{
    "periods": [],
    "version": 3,
    "use_app_cloud_id": true,
    "app_ids": [
        164314
    ],

    "content": {
        "option": {
            "cohort": {
                "outer_logic": "and"
            }
        },
        "query_type": "cohort_v3_idlist",
        "profile_filters": [],
        "profile_groups": [],
        "queries": [
            [
                {
                    "show_label": "c06bed36-eede-4174-91bf-8f37eac3a8ee",
                    "event_name": "any_event",
                    "event_type": "origin",
                    "logic": false,
                    "event_indicator": "events",
                    "measure_info": {},
                    "condition": {
                        "property_operation": ">=",
                        "property_values": [
                            1
                        ],
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        }
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": []
                            }
                        }
                    ]
                }
            ]
        ]
    }
}
```


<span id="b64e0c56"></span>
### User is

```json
{
    "periods": [],
    "version": 3,
    "use_app_cloud_id": true,
    "app_ids": [
        164314
    ],
    "content": {
        "option": {
            "cohort": {
                "outer_logic": "and"
            }
        },
        "query_type": "cohort_v3_idlist",
        "profile_filters": [],
        "profile_groups": [],
        "queries": [
            [
                {
                    "show_label": "c06bed36-eede-4174-91bf-8f37eac3a8ee",
                    "event_indicator": "events",
                    "logic": true,
                    "condition": {
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        },
                        "property_operation": ">",
                        "property_values": [
                            0
                        ]
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": [
                                    {
                                        "property_type": "profile",
                                        "property_name": "custom_Age",
                                        "property_compose_type": "origin",
                                        "property_operation": "=",
                                        "property_values": [
                                            35
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                }
            ]
        ]
    }
}
```


<span id="b4beb4f2"></span>
### User is not

```json
{
    "periods": [],
    "version": 3,
    "use_app_cloud_id": true,
    "app_ids": [
        164314
    ],
    "content": {
        "option": {
            "cohort": {
                "outer_logic": "and"
            }
        },
        "query_type": "cohort_v3_idlist",
        "profile_filters": [],
        "profile_groups": [],
        "queries": [
            [
                {
                    "show_label": "c06bed36-eede-4174-91bf-8f37eac3a8ee",
                    "event_indicator": "events",
                    "logic": false,
                    "condition": {
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        },
                        "property_operation": ">",
                        "property_values": [
                            0
                        ]
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": [
                                    {
                                        "property_type": "profile",
                                        "property_name": "custom_Age",
                                        "property_compose_type": "origin",
                                        "property_operation": "=",
                                        "property_values": [
                                            35
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                }
            ]
        ]
    }
}
```


<span id="9ccf35e5"></span>
### Behavioral sequence

```json
{
    "periods": [],
    "version": 3,
    "use_app_cloud_id": true,
    "app_ids": [
        164314
    ],
    "content": {
        "option": {
            "cohort": {
                "outer_logic": "and"
            }
        },
        "query_type": "cohort_v3_idlist",
        "profile_filters": [],
        "profile_groups": [],
        "queries": [
            [
                {
                    "show_label": "1c21dddc-bcc6-4389-90b2-09d6f66099b4",
                    "event_name": "predefine_pageview",
                    "event_id": 237198,
                    "event_type": "origin",
                    "logic": true,
                    "event_indicator": "events",
                    "sequence_first": true,
                    "next_query_label": "e0edb616-3530-4316-9604-9141099db401",
                    "condition": {
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        },
                        "property_operation": ">",
                        "property_values": [
                            0
                        ]
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": []
                            }
                        }
                    ]
                },
                {
                    "show_label": "e0edb616-3530-4316-9604-9141099db401",
                    "event_name": "order_pay_success",
                    "event_id": 298968,
                    "event_type": "origin",
                    "logic": true,
                    "event_indicator": "events",
                    "sequence_first": false,
                    "next_query_label": null,
                    "condition": {
                        "period": {
                            "granularity": "day",
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
                            "week_start": 1
                        },
                        "property_operation": ">",
                        "property_values": [
                            0
                        ]
                    },
                    "filters": [
                        {
                            "expression": {
                                "logic": "and",
                                "conditions": []
                            }
                        }
                    ]
                }
            ]
        ]
    }
}
```


<span id="9726902a"></span>
# 4. API List


|API |Explain |
|---|---|
|[Get Cohorts List](https://docs.byteplus.com/docs/DataFinder/Get_Cohorts_List) |Get cluster list |
|[Get the Specified Cohorts Information](https://docs.byteplus.com/docs/DataFinder/Get_the_Specified_Cohorts_Information) |Get the specified cluster information |
|[Get the User List Information for the Specified Cohorts](https://docs.byteplus.com/docs/DataFinder/Get_the_User_List_Information_for_the_Specified_Cohorts) |Get the user list information for the specified subgroup |
|[Download the Specified Cohorts User List Information (Streaming)](https://docs.byteplus.com/docs/DataFinder/Download_the_Specified_Cohorts_User_List_Information_Streaming) |Download the list of users in the specified group (streaming) |
|[Upload the File which is Used to Create the Cohorts](https://docs.byteplus.com/docs/DataFinder/Upload_the_File_which_is_Used_to_Create_the_Cohorts) |Upload the file used to create the cluster |
|[Create a Cohort](https://docs.byteplus.com/docs/DataFinder/Create_a_Cohort) |rule creation grouping |
|[Refresh Cohorts](https://docs.byteplus.com/docs/DataFinder/Refresh_Cohorts) |refresh clustering |
|[Delete Created Cohorts](https://docs.byteplus.com/docs/DataFinder/Delete_Created_Cohorts) |Delete create cluster |
|[Modify Created Cohorts](https://docs.byteplus.com/docs/DataFinder/Modify_Created_Cohorts) |Modify to create clusters |
