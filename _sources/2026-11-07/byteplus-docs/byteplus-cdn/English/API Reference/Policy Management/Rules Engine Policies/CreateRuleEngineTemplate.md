---
title: "CreateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRuleEngineTemplate_en-us"
---

Create a rules engine template.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CreateRuleEngineTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CreateRuleEngineTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Title |String |Yes |Indicates the name of the rules engine policy you want to create. The length cannot exceed 100 characters. |`my_title` |
|Message |String |No |Indicates the description of this delivery policy. The length cannot exceed 120 characters. |`my_desc` |
|Project |String |No |Indicates the project to which this policy belongs. The default value of this parameter is 'default', which represents the Default project. |`default` |
|Rule |String |No |For the configuration of this parameter, see [UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_en-us). | |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TemplateId |String |Indicates the ID of the created rules engine policy. |`tpl-rejjo23` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

<span id="sample-1"></span>
#### Sample 1

This sample focuses on the configuration of `Condition`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This sample cannot be used directly. You need to process the parameter configuration in the <code>Rule</code> structure first. See the description of the <code>Rule</code> parameter in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_en-us">UpdateRuleEngineTemplate</a>.</div>


<div data-tips="true" data-tips-type="tip">```json
POST https://cdn.byteplusapi.com/?Action=CreateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-conditions",
    "Message": "desc",
    "Project": "default",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [
                    {
                        "Desc": "Sub-rule1",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader2"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "myheadervalue"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "always"
                                                }
                                            },
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "path",
                                                    "Operator": "suffix_match",
                                                    "IgnoreCase": true,
                                                    "Value": [
                                                        "param=value"
                                                    ]
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader3"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Stage": "client_response",
                        "Phase": 6,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myheadervalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader1"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "jpg",
                                            "png"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path_and_param",
                                        "Operator": "prefix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/docs1/",
                                            "/docs2/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "url",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "https://www.example.com/abc/file"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "query_string",
                                        "Name": "myparam",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myvalue",
                                            "myvalue2"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_referer",
                                        "Operator": "not_equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myreferer1",
                                            "myreferere2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "match",
                                        "Value": [
                                            "1.1.1.1",
                                            "2.2.2.2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_origin",
                                        "Operator": "exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_ua",
                                        "Operator": "not_exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_header",
                                        "Name": "myhttpheader",
                                        "Operator": "regex_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^abc$",
                                            "^cde$"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_area",
                                        "Operator": "not_match",
                                        "Value": [
                                            "PNG",
                                            "FSM"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_method",
                                        "Operator": "equal",
                                        "Value": [
                                            "post",
                                            "head",
                                            "get",
                                            "put",
                                            "options",
                                            "delete",
                                            "connect",
                                            "patch"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "everyday",
                                        "Operator": "match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "02:02:02",
                                            "06:04:04"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "weekday",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "mon",
                                            "tue",
                                            "wed",
                                            "thur",
                                            "fri",
                                            "sat",
                                            "sun"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "period",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "2025-05-07 14:21:21",
                                            "2025-06-13 14:21:24"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "protocol",
                                        "Operator": "equal",
                                        "Value": [
                                            "http"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "response_header",
                                        "Name": "myresponseheader",
                                        "Operator": "regex_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^resheader1$",
                                            "^resheader2$"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_code",
                                        "Operator": "match",
                                        "Value": [
                                            "400",
                                            "500"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "prefix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/abc/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/def/"
                                        ]
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [
                    {
                        "Desc": "规则名称",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader6"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "1111"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "http_referer",
                                                    "Operator": "exist"
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader7"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Stage": "client_response",
                        "Phase": 6,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "MyHeader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```
</div>


<span id="sample-2"></span>
#### <div data-tips="true" data-tips-type="tip">Sample 2</div>


<div data-tips="true" data-tips-type="tip">This sample focuses on the configuration of <code>Action</code>.</div>


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">This sample cannot be used directly. You need to process the parameter configuration in the <code>Rule</code> structure first. See the description of the <code>Rule</code> parameter in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_en-us">UpdateRuleEngineTemplate</a>.</div>


<div data-tips="true" data-tips-type="tip">```json
POST https://cdn.byteplusapi.com/?Action=CreateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "desc",
    "Project": "default",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_request",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "redirect_request",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/docs/file1$"
                                                ]
                                            },
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "follow_client"
                                                ]
                                            },
                                            {
                                                "Name": "target_host",
                                                "Values": [
                                                    "www.example.com"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/cos1/file2$"
                                                ]
                                            },
                                            {
                                                "Name": "target_query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "allow_access",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "allow_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": []
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "download_speed_limit",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "download_speed_limit",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "rate",
                                                "Values": [
                                                    "100"
                                                ]
                                            },
                                            {
                                                "Name": "rate_unit",
                                                "Values": [
                                                    "B/s"
                                                ]
                                            },
                                            {
                                                "Name": "after_size",
                                                "Values": [
                                                    "15"
                                                ]
                                            },
                                            {
                                                "Name": "after_size_unit",
                                                "Values": [
                                                    "MB"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "request_header",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myvalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "deny_access",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "deny_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "465"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_key",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "query_string",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "myparam1",
                                                    "myparam2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "ff"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "header_names",
                                                "Values": [
                                                    "myheader",
                                                    "myheader2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_path",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/path1/$"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/path2/$"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "path_ignore_case",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "compression",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "compression",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "methods",
                                                "Values": [
                                                    "gzip",
                                                    "brotli"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size",
                                                "Values": [
                                                    "563"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size_unit",
                                                "Values": [
                                                    "KB"
                                                ]
                                            },
                                            {
                                                "Name": "format",
                                                "Values": [
                                                    "default"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "video_drag",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "video_drag",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_time",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "cache_time",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ttl",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "ttl_unit",
                                                "Values": [
                                                    "day"
                                                ]
                                            },
                                            {
                                                "Name": "cache_policy",
                                                "Values": [
                                                    "origin_first"
                                                ]
                                            },
                                            {
                                                "Name": "replenish",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_range",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_range",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_follow",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_follow",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_tcp_timeout",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_tcp_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "connect_timeout",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "connect_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_http_timeout",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_http_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "read_timeout",
                                                "Values": [
                                                    "58"
                                                ]
                                            },
                                            {
                                                "Name": "read_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_protocol",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "redirect_protocol",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "https"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```
</div>


<div data-tips="true" data-tips-type="tip"></div>
