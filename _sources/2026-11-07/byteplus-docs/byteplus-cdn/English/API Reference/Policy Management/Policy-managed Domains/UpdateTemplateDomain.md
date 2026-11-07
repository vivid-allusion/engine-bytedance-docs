---
title: "UpdateTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27"
---

Specify a list of domain names to modify the configurations for those domain names within the list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For domain names with <code>HTTPSwitch</code> turned <code>on</code>, you can only modify one at a time. In other words, the list of specified domain names must only contain one domain name.</div>


* <div data-tips="true" data-tips-type="tip">If you wish to modify configurations for multiple domain names simultaneously, all of the following conditions must be met:</div>


   * <div data-tips="true" data-tips-type="tip">For all the domain names being modified, <code>HTTPSSwitch</code> must be set to <code>off</code> in their current configurations.</div>


   * <div data-tips="true" data-tips-type="tip">When making modifications, do not specify <code>HTTPSSwitch</code>, or ensure that <code>HTTPSSwitch</code> remains <code>off</code> in the modified configurations.</div>


* <div data-tips="true" data-tips-type="tip">When using this API, if you do not specify a parameter, the existing configuration for that parameter will not change after you submit the API request.</div>



<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

For the parameters in the Body list, if you do not specify a certain parameter, it indicates that the corresponding configuration for the specified domain names will not be modified.

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateTemplateDomain`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domains |String[] |Yes |Indicates a list of domain names, modifying their configurations.<br><br>If any of the following conditions are met, you can only specify one domain name in the list.<br><br><br>* Among the domain names to be modified, there exists a domain name whose existing `HTTPSSwitch` setting is `on`.<br><br>* When calling this API, you do not specify the `HTTPSSwitch` parameter, or you specify `HTTPSSwitch` as `on`. |`["www.example.com","abc.test.com"]` |
|CertId |String |No |Indicates information about the certificate that needs to be associated with the domain name in `Domains`.<br><br><br>* If `HTTPSSwitch` is `on`, this parameter is required and represents the ID of the certificate that needs to be associated with the domain name in `Domains`. This certificate is stored at BytePlus Certificate Center.<br><br>&nbsp;<br><br>   You can use [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/listcertinfo) to obtain the ID of the certificate you want to associate.<br><br>* If `HTTPSSwitch` is `off`, this parameter is not effective. |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |No |Indicates an encryption policy. This encryption policy will be bound to the domain names in `Domains`. If, when calling this API, the domain names in `Domains` are already bound to encryption policyss, they will first be unbound from the already bound encryption policies and then bound to the encryption policy specified by `CipherTemplateId`.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the encryption policy you want to bind. |`tpl-cqgRvW` |
|HTTPSSwitch |String |No |Indicates whether to enable "HTTPS Encryption Service" for the domain names in `Domains`. This parameter has the following values:<br><br><br>* `on`: Indicates to enable the service.<br><br>* `off`: Indicates to disable the service.<br><br><br>If `Domains` includes multiple domain names, `HTTPSSwitch` must be `off`. |`on` |
|ServiceRegion |String |No |Indicates the service region enabled for the domain names in `Domains`. This parameter has the following values:<br><br><br>* `outside_chinese_mainland`: Indicates "Global (excluding Chinese Mainland)".<br><br>* `chinese_mainland`: Indicates "Chinese Mainland".<br><br>* `global`: Indicates "Global".<br><br><br>Note that `chinese_mainland` or `global` are not available by default. To make the two service regions available, please [submit a ticket](https://console.byteplus.com/workorder/create). Also, since both regions include Chinese Mainland, you must complete the following additional actions:<br><br><br>* Perform [real-name authentication](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration) for your BytePlus account.<br><br>* Perform ICP filing for your domain name. |`outside_chinese_mainland` |
|ServiceTemplateId |String |No |Indicates a delivery policy. This delivery policy will be bound to the domain names in `Domains`. If, when calling this API, the domain names in `Domains` are already bound to a certain delivery policy, they will first be unbound from the already bound delivery policy and then bound to the delivery policy specified by `ServiceTemplateId`.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the delivery policy you want to bind. |`tpl-s2Q4mq` |
|SparrowRules |Object[] |No |Indicates a set of forwarding rules for Edge Functions. Each rule includes filter condition configuration and action configuration. | |
|Condition |Object |No |Indicates the filter condition configuration in the current rule. | |
|ConditionRule |Object[] |Yes |Indicates a set of filter conditions used to filter user requests. Currently, you can only specify one filter condition. | |
|Object |String |Yes |Indicates the filter type. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete request URL. |`path` |
|Operator |String |Yes |Indicates the comparison type. The value of this parameter can only be `match`, indicating that if the `Value` is the same as the `Object` in the request, the request meets this filter condition. |`match` |
|Type |String |Yes |Indicates the object to which the `Object` belongs. Currently, the value of this parameter can only be `url`, indicating "request URL". |`url` |
|Value |String |Yes |Indicates one or more filter values, with a total length not exceeding 1,024 characters. Multiple filter values are separated by semicolons (;). Filter values cannot contain the following characters:<br><br><br>* Consecutive slashes (//), spaces, dollar signs ($), question marks (?), Delete (ASCII code 127).<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each filter value represents a request URL suffix, without starting with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each filter value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each filter value represents a URL path, starting with a slash (/). Each filter value can contain wildcards (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`/chs/foods/local*sets;/us/birds/chickadee` |
|Connective |String |Yes |Indicates the logical relationship between the filter conditions in `ConditionRule`. Currently, since you can only specify one filter condition, this parameter has no practical significance. |`OR` |
|SparrowAction |Object |No |Indicates the configuration of the action that the CDN performs when the user request meets the `Condition`. | |
|Action |String |No |Indicates the action performed by the CDN. Currently, the value of this parameter can only be `Bypass`, indicating that the CDN will hand over the user request to the function specified by `SparrowID` for processing.<br><br>The default value of this parameter is `Bypass`. |`Bypass` |
|IgnoreCase |Boolean |No |Indicates whether the `Value` in `ConditionRule` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates that `Value` is case\-insensitive.<br><br>* `false`: Indicates that `Value` is case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|SparrowID |String |No |Indicates the ID of the function that processes user requests. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the ID. |`96ec5429956c42f79a717a4649f3d455` |
|SparrowSwitch |String |No |Indicates whether to enable the Edge Functions feature. If you set this parameter, you can only specify one domain in `Domains`.<br><br>This parameter has the following values:<br><br><br>* `on`: Indicates that the feature is enabled.<br><br>* `off`: Indicates that the feature is not enabled.<br><br><br>The default value of this parameter is `off`. |`on` |
|RuleMode |String |No |规则策略修改模式，enums, append/override/delete，append表示追加，override表示覆盖, unbind表示解绑 | |
|RuleTemplateIds |String[] |No |规则策略模板id列表 | |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021-03-01
{
    "Domains": [
        "www.example.com"
    ],
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2345b4b42c2e81z0aa5c23",
    "SparrowRules": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Object": "filetype",
                        "Operator": "match",
                        "Type": "url",
                        "Value": "asp;php;jsp;ashx;aspx;do"
                    }
                ],
                "Connective": "OR"
            },
            "SparrowAction": {
                "Action": "bypass",
                "IgnoreCase": true,
                "SparrowID": "96ec5429956c42f79a717a4649f3d455"
            }
        }
    ],
    "SparrowSwitch": "on"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
