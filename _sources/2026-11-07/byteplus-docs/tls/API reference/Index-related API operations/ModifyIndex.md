---
title: "ModifyIndex"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-modifyindex"
---

Call the ModifyIndex interface to modify the index configuration.

<span id="usage-notes"></span>
## Usage notes

This interface is used to modify the index configuration information of the topic. The call frequency limit is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Full\-text indexing and key\-value indexing must be enabled at least one, and the log data collected when the index is closed cannot be retrieved.</div>


* <div data-tips="true" data-tips-type="tip">Torch Log Service has a 32766 character limit for words. For full\-text or overly long logs, if the word divider is not enabled, it may cause the log to be discarded.</div>


* <div data-tips="true" data-tips-type="tip">After configuring the index, you can modify the index at any time. Please note when modifying the index:</div>


   * <div data-tips="true" data-tips-type="tip">If the index is modified, the new index only takes effect for the new data collected after the modification, and the old data index that has been built will not be updated.</div>


   * <div data-tips="true" data-tips-type="tip">Query and analysis are only based on one set of index rules. Therefore, modifying the index configuration may result in the same query analysis statement calculating different results, because the new index configuration has changed the data range of the query and analysis.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyIndex**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a*********` |The ID of the Topic. |
|FullText |Object of [FullTextInfo](https://docs.byteplus.com/en/docs/38/16756#fulltextinfo) |False |`/` |The full\-text index configuration.<br><br><br>* If this field is null or not configured, it means that the full\-text index is not enabled.<br><br>* At least one of the full\-text index configuration and key\-value index configuration should be configured, that is, at least one parameter should be specified between FullText and KeyValue. |
|KeyValue |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16756#keyvalueinfo) |False |`/` |The key\-value index configuration.<br><br><br>* If the array length of this field is 0 or not configured, it means that the key\-value index is not enabled.<br><br>* At least one of the full\-text index configuration and key\-value index configuration should be set, that is, at least one parameter should be specified between FullText and KeyValue. |
|UserInnerKeyValue |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16756#keyvalueinfo) |False |`/` |The reserved field index configuration.<br><br><br>* If the length of this field array is 0 or not configured, it means that the reserved field index is not enabled.<br><br>* Full\-text index and the key\-value index of the reserved field `__content__` cannot be enabled at the same time, i.e., if the `__content__` index is set through the UserInnerKeyValue parameter, the FullText parameter cannot be set at the same time.<br><br>* In the reserved fields, currently only the `__content__` index can be manually enabled. For index settings of other reserved fields, please refer to [Reserved Fields](https://docs.byteplus.com/docs/tls/Reserved_fields). |
|MaxTextLen |Integer |False |`2048` |The maximum length of the statistical field value. The default value is 2048, and the value range is from 64 to 1048576, with the unit being bytes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the length of a single field value exceeds the maximum length you have specified, the part that exceeds will be truncated and will not be involved in the analysis.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the maximum length of a field is updated, it will only be effective for incremental data.</div><br> |


<span id="fulltextinfo"></span>
### FullTextInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Delimiter |String |True |`, ;/\n\t` |The delimiters for full\-text index.<br><br><br>* Each character in the string represents a tokenizer.<br><br>* Length is 1~256 bytes.<br><br>* Only supports one or more of the following characters `!@#%^&*()-_=\"', <>/?\|;: \n\t\r[]{}`.<br><br>* Cannot configure both Chinese and tokenizers at the same time. |
|CaseSensitive |Boolean |True |`false` |Specifies whether to enable case sensitivity.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IncludeChinese |Boolean |False |`false` |Specifies whether to include Chinese characters. The default is false, that is, not included. |


<span id="keyvalueinfo"></span>
### KeyValueInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |True |`"Key": "test-key1"` |The field name of the key\-value index. |
|Value |Object of [Value](https://docs.byteplus.com/en/docs/38/16756#value) |True |`"Value": { "ValueType": "text", "Delimiter": "", "CaseSensitive": true, "IncludeChinese": false, "SqlFlag": false }` |The description of the fields in the key\-value index. |


<span id="value"></span>
### Value


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|SqlFlag |Boolean |False |`false` |Whether to enable the field analysis function enabled.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IndexAll |Boolean |False |`false` |Whether to create indexes for all fields in the JSON that have text values.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|JsonKeys |Array of [KeyValueInfo](https://docs.byteplus.com/en/docs/38/16756#keyvalueinfo) |False |`[ { "Key":"key1", "Value":{ "ValueType":"text", "SqlFlag":true } }, { "Key":"key2", "Value":{ "ValueType":"long", "SqlFlag":true } }, { "Key":"key3.key4.key5", "Value":{ "ValueType":"double", "SqlFlag":true } } ]` |Return the index of the JSON subfield, whose value is an array of KeyValueInfo. |
|Delimiter |String |False |`, ;/\n\t` |The delimiter of the field. |
|ValueType |String |True |`text` |Field types, including long, double, text, and json. |
|CaseSensitive |Boolean |False |`true` |Whether to enable case sensitivity.<br><br><br>* True: Enabled.<br><br>* False: Disabled. |
|IncludeChinese |Boolean |False |`false` |Whether to include Chinese characters. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request-1"></span>
## Sample Request 1

```json
PUT https://tls-{Region}.bytepluses.com/ModifyIndex HTTP/1.1
Content-Type: application/json
{
    "TopicId": "3***********",
    "FullText": {
        "Delimiter": ",-;",
        "CaseSensitive": false,
        "IncludeChinese": false
    }
}
```


<span id="sample-response-1"></span>
## Sample Response 1

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id="sample-request-2"></span>
## Sample Request 2

```json
PUT https://tls-{Region}.bytepluses.com/ModifyIndex HTTP/1.1
Content-Type: application/json
{
    "TopicId":"39********",
    "FullText":{
        "Delimiter":",-;"
    },
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
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key2",
                        "Value":{
                            "ValueType":"long",
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key3.key4.key5",
                        "Value":{
                            "ValueType":"double",
                            "SqlFlag":true
                        }
                    }
                ]
            }
        }
    ]
}
```


<span id="sample-response-2"></span>
## Sample Response 2

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{}
```


<span id="sample-request-3"></span>
## Sample Request 3

```json
PUT https://tls-{Region}.bytepluses.com/ModifyIndex HTTP/1.1
Content-Type: application/json
{
    "TopicId":"39********",
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
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key2",
                        "Value":{
                            "ValueType":"long",
                            "SqlFlag":true
                        }
                    },
                    {
                        "Key":"key3.key4.key5",
                        "Value":{
                            "ValueType":"double",
                            "SqlFlag":true
                        }
                    }
                ]
            }
        }
    ]，
    "UserInnerKeyValue": [
        {
            "Key": "__content__",
            "Value": {
                "ValueType": "json",
                "Delimiter": ",:-/ ",
                "CaseSensitive": false,
                "IncludeChinese": false,
                "SqlFlag": false,
                "JsonKeys": [
                    {
                        "Key": "name",
                        "Value": {
                            "ValueType": "text",
                            "SqlFlag": false
                        }
                    },
                    {
                        "Key": "age",
                        "Value": {
                            "ValueType": "long",
                            "SqlFlag": false
                        }
                    },
                    {
                        "Key": "education.master.college",
                        "Value": {
                            "ValueType": "text",
                            "SqlFlag": false
                        }
                    }
                ]
            }
        }
    ]
}
```


<span id="sample-response-3"></span>
## Sample Response 3

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8  
{}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |you cannot enable **Delimiter** and **Contains Chinese** at the same time. |
|400 |InvalidArgument |At least one of full\-text indexing and key\-value indexing must be turned on. |At least one of full\-text index and key\-value index must be enabled. |
|400 |InvalidArgument |Index key value_type:%s conflict with [includeChinese:%t, casSensitive:%t, delimiter:%s], please check argument. |The fields of the long type do not support setting **case sensitive**, **Contains Chinese**, or **Delimiter**. |
|400 |InvalidIndexJsonKeys |Non\-JSON field %s configures JsonKeys, please check argument. |Non\-JSON field configuration subfield. |
|400 |ConflictIndexJsonKeys |JsonKeys %s and %s have conflict prefix, please check argument. |The key names in JsonKeys have prefix conflicts. |
|400 |InvalidArgument |Index key sqlFlag:%t conflict with [includeChinese:%t, delimiter:%s], please check argument. |After enabling statistics, the configuration does not support **Delimiter** and **Contains Chinese**. |
|400 |IndexKeyValueQuotaExceed |Exceeded index key\-value quota. |Key\-value index limit exceeded. |
|400 |IndexKeyDuplicate |The %dth index key name:%s is duplicate, please check argument. |The key name of the index is duplicated. |
|400 |InvalidArgument |Index key delimiter:%s conflict with includeChinese:%t, please check argument. |you cannot enable **Delimiter** and **Contains Chinese** at the same time. |
|400 |IndexKVNULL |Index key value index is open, but the key value list is null, please check argument. |The number of keys configured for the key\-value index is 0. |
|404 |TopicNotExist |Topic does not exist. |The topic does not exist. |
|409 |IndexAlreadyExist |Index already exist |The index already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
|400 |IndexInnerKeyUnSupport |key\-value indexing for inner key: %v, doesn't support |Reserved field indexing for% v fields is not supported. |
|400 |IndexInnerKeyConflict |full\-text indexing and content indexing can't be set together |The configuration of the full\-text index conflicts with the `__content__` index. |


&nbsp;
