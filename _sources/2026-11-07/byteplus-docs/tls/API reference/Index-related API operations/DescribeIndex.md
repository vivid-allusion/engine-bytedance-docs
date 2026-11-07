---
title: "DescribeIndex"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describeindex"
---

Invoke the DescribeIndex interface to obtain index configuration information.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s. Errors will be reported as ExceedQPSLimit when the frequency limit is exceeded.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **GET**

* Request URL: **https://tls\-{Region}.bytepluses.com/DescribeIndex**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="query"></span>
### Query


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a**********` |The ID of the topic. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|TopicId |String |`4a**********` |The ID of the topic. |
|FullText |Object of [FullTextInfo](https://docs.byteplus.com/en/docs/38/16757#fulltextinfo) |`/` |The full\-text index configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field may return null, indicating that the full\-text index is not enabled.</div><br> |
|KeyValue |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16757#keyvalueinfo) |`/` |The key\-value index configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field returns an array of length 0, indicating that the key\-value index is not enabled.</div><br> |
|UserInnerKeyValue |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16757#keyvalueinfo) |`/` |The reserved field index configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field returns an array of length 0, indicating that the reserved field index is not enabled.</div><br> |
|CreateTime |String |`2021-08-19 11:41:29` |The time of index creation. |
|ModifyTime |String |`2021-08-19 11:41:29` |The time the index was last modified. |
|MaxTextLen |Integer |`2048` |The maximum length of the statistical field value. The default value is 2048, and the value range is from 64 to 1048576, with the unit being bytes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the length of a single field value exceeds the maximum length you have specified, the part that exceeds will be truncated and will not be involved in the analysis.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the maximum length of a field is updated, it will only be effective for incremental data.</div><br> |


<span id="fulltextinfo"></span>
### FullTextInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Delimiter |String |`, ;/\n\t` |The delimiters for full\-text index.<br><br><br>* Each character in the string represents a tokenizer.<br><br>* Length is 1~256 bytes.<br><br>* Only supports one or more of the following characters `!@#%^&*()-_=\"', <>/?\|;: \n\t\r[]{}`.<br><br>* Cannot configure both Chinese and tokenizers at the same time. |
|CaseSensitive |Boolean |`false` |Specifies whether to enable case sensitivity.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IncludeChinese |Boolean |`false` |Specifies whether to include Chinese characters. The default is false, that is, not included. |


<span id="keyvalueinfo"></span>
### KeyValueInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |`"Key": "test-key1"` |The field name of the key\-value index. |
|Value |Object of [Value](https://docs.byteplus.com/en/docs/38/16757#value) |`"Value": { "ValueType": "text", "Delimiter": "", "CaseSensitive": true, "IncludeChinese": false, "SqlFlag": false }` |The description of the fields in the key\-value index. |


<span id="value"></span>
### Value


|Name |Type |Example |Description |
|---|---|---|---|
|SqlFlag |Boolean |`false` |Whether to enable the field analysis function enabled.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IndexAll |Boolean |`false` |Whether to create indexes for all fields in the JSON that have text values.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|JsonKeys |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16757#keyvalueinfo) |`[ { "Key":"key1", "Value":{ "ValueType":"text", "SqlFlag":true } }, { "Key":"key2", "Value":{ "ValueType":"long", "SqlFlag":true } }, { "Key":"key3.key4.key5", "Value":{ "ValueType":"double", "SqlFlag":true } } ]` |Return the index of the JSON subfield, whose value is an array of KeyValueInfo. |
|Delimiter |String |`, ;/\n\t` |The delimiter of the field. |
|ValueType |String |`text` |Field types, including long, double, text, and json. |
|CaseSensitive |Boolean |`true` |Whether to enable case sensitivity.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IncludeChinese |Boolean |`false` |Whether to include Chinese characters. |


<span id="sample-request-1"></span>
## Sample Request 1

```json
GET https://tls-{Region}.bytepluses.com/DescribeIndex?TopicId=c1******** HTTP/1.1
```


<span id="sample-response-1"></span>
## Sample Response 1

仅配置全文索引

```json
{
    "TopicId": "396f23d6-27bd-48eb-85d8-ee693716****",
    "FullText": {
        "Delimiter": ",-;",
        "CaseSensitive": false,
        "IncludeChinese": false
    },
    "KeyValue": [],
    "UserInnerKeyValue": [],
    "CreateTime": "2022-02-28 21:36:14",
    "ModifyTime": "2022-02-28 21:36:15"
}
```


<span id="sample-request-2"></span>
## Sample Request 2

```json
GET https://tls-{Region}.bytepluses.com/DescribeIndex?TopicId=c1******** HTTP/1.1
Content-Type: application/json
```


<span id="sample-response-2"></span>
## Sample Response 2

```json
Content-Type: application/json; charset=utf-8
{
    "TopicId":"39*************",
    "FullText":null,
    "KeyValue":[
        {
            "Key":"test1",
            "Value":{
                "ValueType":"text",
                "Delimiter":"",
                "CaseSensitive":true,
                "IncludeChinese":false,
                "SqlFlag":false
            }
        },
        {
            "Key":"test2",
            "Value":{
                "ValueType":"long",
                "Delimiter":"",
                "CaseSensitive":false,
                "IncludeChinese":false,
                "SqlFlag":true
            }
        },
        {
            "Key":"test3",
            "Value":{
                "ValueType":"json",
                "Delimiter":"",
                "CaseSensitive":false,
                "IncludeChinese":false,
                "SqlFlag":true,
                "JsonKeys":[
                    {
                        "Key":"key1",
                        "Value":{
                            "ValueType":"text",
                            "Delimiter":"",
                            "CaseSensitive":false,
                            "IncludeChinese":false,
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key2",
                        "Value":{
                            "ValueType":"long",
                            "Delimiter":"",
                            "CaseSensitive":false,
                            "IncludeChinese":false,
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key3.key4.key5",
                        "Value":{
                            "ValueType":"double",
                            "Delimiter":"",
                            "CaseSensitive":false,
                            "IncludeChinese":false,
                            "SqlFlag":true
                        }
                    }
                ]
            }
        },
        ...
    ],
    "UserInnerKeyValue": [],
    "CreateTime":"2022-02-28 21:36:14",
    "ModifyTime":"2022-02-28 21:36:15"
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|404 |TopicNotExist |Topic does not exist. |The topic does not exist. |
|404 |IndexNotExist |Index does not exist. |The index configuration does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
