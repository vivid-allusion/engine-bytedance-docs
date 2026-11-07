---
title: "CreateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRuleEngineTemplate_zh-cn"
---

创建一个规则引擎策略。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=CreateRuleEngineTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `CreateRuleEngineTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Title |String |是 |表示您要创建的规则引擎策略的名称，长度不能超过 100 个字符。 |`TestPolicy` |
|Message |String |否 |表示该分发策略的描述，长度不能超过 120 个字符。 |`This is a test.` |
|Project |String |否 |表示该策略所归属的项目。该参数的默认值是 'default'，表示 Default 项目。 |`default` |
|Rule |String |否 |关于该参数的配置，参见 [UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-cn)。 | |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|TemplateId |String |表示创建的规则引擎策略的 ID。 |`tpl-rejjo23` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

<span id="示例一"></span>
#### 示例一

本示例重点展示 `Condition` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例不能直接使用。您需要先处理 <code>Rule</code> 结构体中的参数配置。参见 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-cn">UpdateRuleEngineTemplate</a> 中 <code>Rule</code> 参数的说明。</div>


```json
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


<span id="示例二"></span>
#### 示例二

本示例重点展示 `Actions` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例不能直接使用。您需要先处理 <code>Rule</code> 结构体中的参数配置。参见 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-cn">UpdateRuleEngineTemplate</a> 中 <code>Rule</code> 参数的说明。</div>


```json
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


<span id="返回示例"></span>
### 返回示例

&nbsp;
