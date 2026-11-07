---
title: "AddTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addtemplatedomain"
---

Add one or more domains in BytePlus CDN. When adding a domain, you must specify a published delivery policy. You can optionally specify a published encryption policy and a rules engine policy.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `AddTemplateDomain`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Indicates one or more domain names to be added. You can specify up to 50 domain names, separated by commas (,). The domain name you add must meet all of the following conditions:<br><br><br>* Length does not exceed 100 characters.<br><br>* Cannot contain uppercase letters.<br><br>* Does not include any of these suffixes: `zjgslb.com`, `yangyi19.com`, `volcgslb.com`, `veew-alb-cn1.com`, `bplgslb.com`, `bplslb.com`, `ttgslb.com`.<br><br><br>tip<br><br>When you bind your domain name with a delivery policy, the origin address specified in the policy must not be the same as your domain name. |`www.example.com` |
|ServiceTemplateId |String |Yes |Indicates a delivery policy to be bound with this domain name.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the delivery policy you want to bind. |`tpl-s2Q4mq` |
|CertId |String |No |Indicates the ID of a certificate. This certificate is stored in the BytePlus Certificate Center and will be associated with the domain name.<br><br><br>* If `HTTPSSwitch` is `on`, this parameter is required. Before using this API, you need to grant CDN access to the Certificate Center, then upload your certificate to the BytePlus Certificate Center to obtain the ID of the certificate. It is recommended to authorize CDN access to the Certificate Center using the primary account.<br><br>&nbsp;<br><br>     You can use [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/listcertinfo) to obtain the ID of the certificate you want to associate.<br><br>* If `HTTPSSwitch` is `off`, this parameter does not take effect. |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |No |Indicates an encryption policy to be bound with this domain name.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the encryption policy you want to bind.<br><br>If this parameter is not specified, it means that the domain name will not be bound to any encryption policy at present. |`tpl-cqgRvW` |
|HTTPSSwitch |String |No |Indicates whether to enable "HTTPS Encryption Service" for this domain name. This parameter can take the following values:<br><br><br>* `on`: Indicates to enable this service.<br><br>* `off`: Indicates not to enable this service.<br><br><br>The default value of this parameter is `off`. |`on` |
|Project |String |No |Indicates the project to which this domain name belongs, with the default value being `default`. |`default` |
|ServiceRegion |String |No |Indicates the service region enabled for this domain name. This parameter can take the following values:<br><br><br>* `outside_chinese_mainland`：Indicates "Global (excluding Chinese Mainland)".<br><br>* `chinese_mainland`：Indicates "Chinese Mainland".<br><br>* `global`: Indicates "Global".<br><br><br>The default value of this parameter is `outside_chinese_mainland`.<br><br>Note that `chinese_mainland` or `global` are not available by default. To make the two service regions available, please [submit a ticket](https://console.byteplus.com/workorder/create). Also, since both regions include Chinese Mainland, you must complete the following additional actions:<br><br><br>* Perform [real-name authentication](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration) for your BytePlus account.<br><br>* Perform ICP filing for your domain name. |`global` |
|Tags |Object[] |No |Indicates a list of tags. These tags will be added to `Domain`. The list can contain up to 10 tags. A tag is a key\-value pair.标签 | |
|Key |String |No |Indicates the key of a tag in the list, with a length range of 1\-128 characters. The key is case\-sensitive and can contain Unicode letters, Unicode numbers, spaces, and any of the following characters:<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |No |Indicates the value of the tag, with a length range of 1\-256 characters. This parameter is also case\-sensitive and can contain Unicode letters, Unicode numbers, spaces, and any of the following characters:<br><br><br>* _./=+\-@ |`myValue` |
|RuleTemplateIds |String[] |No |Indicates a rule engine policy that needs to be bound to the domain name.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the rules engine policy you want to bind.<br><br>If this parameter is not specified, it means that the domain name will not be bound to any rules engine policy at present. |`tpl-r18yoko` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|ResourceIds |String[] |Indicates the list of added domains. |`"www.example.com","img.example.com"]` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021-03-01
{
    "Domain": "www.example.com,img.example.com",
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2349b4b42c2e80b0aa8c23",
    "Tags": [
        {
            "Key": "myKey1",
            "Value": "myValue1"
        },
        {
            "Key": "myKey2",
            "Value": "myValue2"
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082209311384D275C0D56FB6A17884",
        "Action": "AddTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ResourceIds": [
            "www.example.com",
            "img.example.com"
        ]
    }
}
```


&nbsp;
